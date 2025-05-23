---
title: 쿼리 및 색인 생성에 대한 우수 사례
description: 이 문서에서는 색인 및 쿼리를 최적화하는 방법에 대한 지침을 제공합니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 3ffa7c80-ce59-41cf-bb50-c6caf77d9baa
source-git-commit: 09f3d38e9f9c7f882d8b03dcf86db68cb8885a08
workflow-type: tm+mt
source-wordcount: '4196'
ht-degree: 6%

---

# 쿼리 및 색인 생성에 대한 우수 사례{#best-practices-for-queries-and-indexing}

AEM 6에서 Oak으로 전환하는 것과 함께 쿼리 및 색인을 관리하는 방식이 크게 변경되었습니다. Jackrabbit 2에서는 모든 콘텐츠를 기본적으로 색인화하여 자유롭게 쿼리할 수 있었습니다. Oak에서 `oak:index` 노드 아래에 인덱스를 수동으로 만들어야 합니다. 색인 없이 쿼리를 실행할 수 있지만 큰 데이터 세트의 경우 쿼리가 느리게 실행되거나 중단됩니다.

이 문서에서는 색인을 만들 시기와 색인이 필요하지 않은 시기, 색인이 필요하지 않은 경우 쿼리를 사용하지 않는 요령, 색인 및 쿼리를 최적화하여 가능한 한 최적으로 수행하기 위한 팁에 대해 설명합니다.

또한 쿼리 및 인덱스 작성에 대한 [Oak 설명서를 읽어보세요](/help/sites-deploying/queries-and-indexing.md). 색인이 AEM 6의 새로운 개념인 것 외에도 이전 AEM 설치에서 코드를 마이그레이션할 때 고려해야 하는 Oak 쿼리의 구문 차이가 있습니다.

## 쿼리 사용 시기 {#when-to-use-queries}

### 저장소 및 분류법 디자인 {#repository-and-taxonomy-design}

저장소 분류법을 디자인할 때 여러 가지 요인을 고려해야 합니다. 여기에는 액세스 제어, 현지화, 구성 요소 및 페이지 속성 상속 등이 포함됩니다.

이러한 우려사항을 고려한 분류법을 디자인하는 동안, 색인화 디자인의 &quot;트래버스 가능성&quot; 또한 고려하는 것이 중요합니다. 이 맥락에서 트래버스 가능성이란 콘텐츠가 그 경로에 따라 예측 가능한 방식으로 액세스될 수 있게 하는 분류법의 기능을 말합니다. 이렇게 하면 많은 쿼리를 실행해야 하는 시스템보다 유지 관리가 더 용이한 보다 성능이 좋은 시스템을 구축할 수 있습니다.

또한 분류법을 디자인할 때는 순서 지정 여부가 중요한지 고려해야 합니다. 명확한 순서 지정이 필요하지 않고 많은 형제 노드가 예상되는 경우에는 `sling:Folder` 또는 `oak:Unstructured`과(와) 같은 비순차 노드 유형을 사용하는 것이 좋습니다. 순서 지정이 필요한 경우에는 `nt:unstructured` 및 `sling:OrderedFolder`이(가) 더 적절합니다.

### 구성 요소에서의 쿼리 {#queries-in-components}

쿼리는 AEM 시스템에서 수행하는 것보다 더 까다로운 작업들 중 하나일 수 있으므로 구성 요소에서는 이를 피하는 것이 좋습니다. 페이지가 렌더링될 때마다 여러 쿼리가 실행되도록 할 경우 종종 시스템 성능이 저하될 수 있습니다. 구성 요소 렌더링 시 쿼리 실행을 피하는 데 사용할 수 있는 전략은 두 가지가 있습니다. **노드 트래버스** 및 **결과 프리페치**.

#### 노드 트래버스 {#traversing-nodes}

필요한 데이터의 위치를 미리 알 수 있도록 저장소를 디자인한 경우 쿼리를 실행하여 찾을 필요 없이 필요한 경로에서 이 데이터를 검색하는 코드를 배포할 수 있습니다.

예를 들어 특정 카테고리에 부합하는 콘텐츠를 렌더링하는 경우가 있습니다. 한 가지 접근법은 카테고리에서 항목을 표시하는 구성 요소를 채우도록 쿼리할 수 있는 카테고리 속성을 가진 콘텐츠를 구성하는 것입니다.

그보다 나은 접근법은 이 콘텐츠를 카테고리별 분류법에 따라 구성하여 수동으로 가져올 수 있도록 하는 것입니다.

예를 들어 콘텐츠가 다음과 유사한 분류법으로 저장된다고 가정해봅시다.

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

`/content/myUnstructuredContent/parentCategory/childCategory` 노드를 간편하게 가져올 수 있으며, 그 자식 항목들은 구문 분석되어 구성 요소 렌더링에 사용될 수 있습니다.

또한 작은 크기 또는 같은 형식의 결과 세트를 다룰 때, 동일한 결과 세트를 반환하는 쿼리를 만드는 것보다 저장소를 트래버스하고 필요한 노드를 모으는 것이 더 빠를 수 있습니다. 일반적인 고려사항은 가능하면 쿼리를 피하는 것입니다.

#### 결과 프리페치 {#prefetching-results}

경우에 따라 콘텐츠나 구성 요소에 대한 요구 사항 때문에 필요한 데이터를 검색하는 방법으로 노드 트래버스를 사용할 수 없습니다. 이러한 경우 최종 사용자에 대해 최적의 성능이 보장되도록 구성 요소가 렌더링되기 전에 필요한 쿼리를 실행해야 합니다.

구성 요소에 필요한 결과를 구성 요소 작성 시에 계산할 수 있고 콘텐츠가 변경될 것으로 예상되지 않는 경우 작성자가 대화 상자의 설정을 적용할 때 쿼리를 실행할 수 있습니다.

데이터나 콘텐츠가 규칙적으로 변경되는 경우에는 일정에 따라 쿼리를 실행하거나 기반 데이터의 업데이트에 대한 리스너를 사용하여 쿼리를 실행할 수 있습니다. 그러면 저장소의 공유 위치에 결과를 작성할 수 있습니다. 이 경우, 런타임 시 쿼리를 실행할 필요 없이 이 데이터를 필요로 하는 모든 구성 요소가 이 단일 노드에서 해당 값을 가져올 수 있습니다.

## 쿼리 최적화 {#query-optimization}

색인을 사용하지 않는 쿼리를 실행할 때 노드 트래버스에 대한 경고가 기록됩니다. 자주 실행되는 쿼리인 경우 인덱스를 만듭니다. 지정된 쿼리에서 사용 중인 인덱스를 확인하려면 [쿼리 설명 도구](/help/sites-administering/operations-dashboard.md#explain-query)를 사용하는 것이 좋습니다. 자세한 내용은 관련 검색 API에 대해 디버그 로깅을 활성화할 수 있습니다.

>[!NOTE]
>
>색인 정의를 수정한 후에는 색인을 다시 작성(색인 재지정)해야 합니다. 인덱스 크기에 따라 완료하는 데 시간이 걸릴 수 있습니다.

복잡한 쿼리를 실행할 때 쿼리를 더 작은 여러 쿼리로 세분화하고 팩트 후에 코드를 통해 데이터를 결합하는 경우가 있을 수 있습니다. 이러한 경우에 대한 권장 사항은 두 접근 방식의 성능을 비교하여 해당 사용 사례에 더 적합한 옵션을 결정하는 것입니다.

AEM에서는 다음 세 가지 방법 중 하나로 쿼리를 작성할 수 있습니다.

* [QueryBuilder API](/help/sites-developing/querybuilder-api.md)을(를) 통해(권장)
* XPath 사용(권장)
* SQL2 사용

모든 쿼리가 실행되기 전에 SQL2로 변환되지만 쿼리 변환의 오버헤드가 최소화되므로 쿼리 언어를 선택할 때 개발 팀의 가독성과 편안함이 가장 큰 문제가 됩니다.

>[!NOTE]
>
>QueryBuilder를 사용하는 경우 기본적으로 결과 수가 결정되는데, 이는 이전 버전의 Jackrabbit과 비교하여 Oak에서 더 느립니다. 이를 보완하기 위해 [guessTotal 매개 변수](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results)를 사용할 수 있습니다.

### 쿼리 설명 도구 {#the-explain-query-tool}

모든 쿼리 언어와 마찬가지로, 쿼리를 최적화하는 첫 번째 단계는 쿼리 실행 방법을 이해하는 것입니다. 이 활동을 사용하려면 작업 대시보드에 포함된 [쿼리 설명 도구](/help/sites-administering/operations-dashboard.md#explain-query)를 사용할 수 있습니다. 이 도구를 사용하면 쿼리를 연결하고 설명할 수 있습니다. 쿼리로 인해 대형 저장소 및 런타임 시 문제가 발생하고 사용된 색인이 있는 경우 경고가 표시됩니다. 또한 이 도구는 설명 및 최적화할 수 있는 느리고 인기 있는 쿼리 목록을 로드할 수 있습니다.

### 쿼리에 대한 디버그 로깅 {#debug-logging-for-queries}

Oak에서 사용할 인덱스를 선택하는 방법과 쿼리 엔진이 실제로 쿼리를 실행하는 방법에 대한 추가 정보를 얻으려면 다음 패키지에 대해 **DEBUG** 로깅 구성을 추가할 수 있습니다.

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

쿼리 디버깅을 마치면 이 로거를 제거해야 합니다. 많은 양의 작업을 출력하는 경향이 있으며 결국 디스크를 로그 파일로 채울 수 있습니다.

이 작업을 수행하는 방법에 대한 자세한 내용은 [로깅 설명서](/help/sites-deploying/configure-logging.md)를 참조하십시오.

### 색인 통계 {#index-statistics}

Lucene은 각 인덱스에 있는 문서의 크기 및 수를 포함하여 인덱싱된 컨텐츠에 대한 세부 정보를 제공하는 JMX Bean을 등록합니다.

`https://server:port/system/console/jmx`의 JMX 콘솔에 액세스하여 연결할 수 있습니다.

JMX 콘솔에 로그인되면 **Lucene 인덱스 통계**&#x200B;를 검색하여 찾으십시오. 다른 인덱스 통계는 **IndexStats** MBean에서 찾을 수 있습니다.

쿼리 통계를 보려면 이름이 **Oak 쿼리 통계**&#x200B;인 MBean을 확인하십시오.

[Luke](https://code.google.com/archive/p/luke/)과(와) 같은 도구를 사용하여 인덱스를 자세히 살펴보려면 Oak 콘솔을 사용하여 `NodeStore`에서 파일 시스템 디렉터리로 인덱스를 덤프해야 합니다. 이 방법에 대한 지침은 [Lucene 설명서](https://jackrabbit.apache.org/oak/docs/query/lucene.html)를 참조하세요.

시스템의 인덱스를 JSON 형식으로 추출할 수도 있습니다. 이렇게 하려면 `https://server:port/oak:index.tidy.-1.json`에 액세스해야 합니다.

### 쿼리 제한 {#query-limits}

**개발 중**

`oak.queryLimitInMemory`(예: 10000) 및 Oak에 대해 낮은 임계값을 설정하십시오. `queryLimitReads`(예: 5000) &quot;쿼리가 x개 이상의 노드를 읽었습니다...&quot;라는 UnsupportedOperationException이 발생할 때 값비싼 쿼리를 최적화합니다.

이렇게 하면 리소스 집약적인 쿼리(즉, 색인이나 덜 포함되는 색인으로 뒷받침되지 않음)를 방지할 수 있습니다. 예를 들어, 100만 개의 노드를 읽는 쿼리는 I/O 증가로 이어져 전체 애플리케이션 성능에 부정적인 영향을 줍니다. 초과 제한으로 인해 실패한 모든 쿼리는 분석 및 최적화되어야 합니다.

#### **배포 후** {#post-deployment}

* 큰 노드 트래버스 또는 큰 힙 메모리 소비를 트리거하는 쿼리에 대해 로그를 모니터링합니다.&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 쿼리를 최적화하여 트래버스된 노드 수 감소

* 대용량 힙 메모리 소비를 트리거하는 쿼리에 대한 로그 모니터링 :

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 쿼리를 최적화하여 힙 메모리 소모 감소

AEM 6.0 - 6.2 버전의 경우, 큰 쿼리가 환경을 오버로드할 수 없도록 AEM 시작 스크립트의 JVM 매개변수를 통해 노드 트래버스에 대한 임계값을 조정할 수 있습니다.

권장되는 값은 다음과 같습니다.

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

AEM 6.3 이상에서는 위의 두 매개 변수가 즉시 사전 구성되어 있으며 OSGi QueryEngineSettings를 통해 지속할 수 있습니다.

추가 정보는 [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)에서 확인할 수 있습니다.

## 효율적인 인덱스 생성 팁 {#tips-for-creating-efficient-indexes}

### 색인을 생성해야 합니까? {#should-i-create-an-index}

색인을 만들거나 최적화할 때 가장 먼저 묻는 질문은 주어진 상황에서 색인이 필요한지 여부이다. 일괄 처리 프로세스를 통해 해당 쿼리를 한 번만 또는 가끔 실행하고 시스템이 사용량이 적은 시간에 실행하려는 경우 색인을 전혀 만들지 않는 것이 좋습니다.

색인을 만든 후에는 색인화된 데이터가 업데이트될 때마다 색인도 업데이트해야 합니다. 이 경우 시스템에 대한 성능이 저하되므로 필요한 경우에만 인덱스를 만들어야 합니다.

또한 색인은 색인 내에 포함된 데이터가 신뢰할 수 있을 만큼 고유한 경우에만 유용합니다. 책의 색인과 그것이 다루고 있는 주제들을 고려하라. 텍스트에 있는 주제 집합을 색인화할 때 일반적으로 수백 또는 수천 개의 항목이 있으므로 페이지 하위 집합으로 빠르게 이동하여 원하는 정보를 빠르게 찾을 수 있습니다. 색인에 각각 수백 페이지를 가리키는 항목이 두 개 또는 세 개만 있는 경우 색인이 유용하지 않습니다. 이와 동일한 개념이 데이터베이스 인덱스에 적용됩니다. 두 개의 고유 값만 있는 경우 색인이 유용하지 않습니다. 즉, 지수가 너무 커져 유용하지 않을 수도 있습니다. 색인 통계를 보려면 위의 [색인 통계](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics)를 참조하십시오.

### Lucene 또는 속성 인덱스 {#lucene-or-property-indexes}

Lucene 색인은 Oak 1.0.9에서 도입되었으며 AEM 6 초기 출시에서 도입된 속성 색인에 비해 몇 가지 강력한 최적화 기능을 제공합니다. Lucene 인덱스 또는 속성 인덱스 사용 여부를 결정할 때 다음 사항을 고려하십시오.

* Lucene 인덱스는 속성 인덱스보다 많은 기능을 제공합니다. 예를 들어 속성 인덱스는 단일 속성만 인덱싱할 수 있는 반면 Lucene 인덱스는 여러 속성을 포함할 수 있습니다. Lucene 인덱스에서 사용할 수 있는 모든 기능에 대한 자세한 내용은 [설명서](https://jackrabbit.apache.org/oak/docs/query/lucene.html)를 참조하십시오.
* Lucene 색인은 비동기적입니다. 이렇게 하면 상당한 성능 향상을 얻을 수 있지만, 데이터가 저장소에 기록되는 시점과 색인이 업데이트되는 시점 사이에 지연이 발생할 수도 있습니다. 쿼리가 100% 정확한 결과를 반환하도록 하는 것이 중요한 경우 속성 색인이 필요합니다.
* 비동기적이기 때문에 Lucene 색인은 고유성 제약 조건을 적용할 수 없습니다. 필요한 경우 속성 인덱스를 배치해야 합니다.

일반적으로 높은 성능과 유연성의 이점을 얻을 수 있도록 속성 색인을 사용해야 하는 경우가 아니라면 Lucene 색인을 사용하는 것이 좋습니다.

### 디자인 고려 사항 {#design-considerations}

Lucene 색인에 대한 Oak 설명서에는 색인을 디자인할 때 고려해야 할 몇 가지 사항이 나와 있습니다.

* 쿼리에서 다른 경로 제한을 사용하는 경우 `evaluatePathRestrictions`을(를) 사용합니다. 이렇게 하면 쿼리가 지정된 경로 아래의 결과 하위 집합을 반환한 다음 쿼리를 기반으로 필터링할 수 있습니다. 그렇지 않으면 쿼리가 저장소의 쿼리 매개 변수와 일치하는 모든 결과를 검색한 다음 경로를 기반으로 필터링합니다.
* 쿼리에서 정렬을 사용하는 경우 정렬된 속성에 대한 명시적 속성 정의를 사용하고 해당 속성에 대해 `ordered`을(를) `true`(으)로 설정하십시오. 이렇게 하면 인덱스에서 결과를 정렬하고 쿼리 실행 시 비용이 많이 드는 정렬 작업을 절약할 수 있습니다.

* 필요한 것만 색인에 넣으세요. 불필요한 기능이나 속성을 추가하면 색인이 커지고 성능이 저하됩니다.
* 속성 인덱스에서 고유한 속성 이름을 사용하면 인덱스의 크기를 줄이는 데 도움이 되지만 Lucene 인덱스의 경우 `nodeTypes` 및 `mixins`을(를) 사용하여 일관된 인덱스를 만들어야 합니다. 특정 `nodeType` 또는 `mixin`을(를) 쿼리하는 것이 `nt:base`을(를) 쿼리하는 것보다 성능이 향상됩니다. 이 방법을 사용하는 경우 해당 `nodeTypes`에 대해 `indexRules`을(를) 정의합니다.

* 쿼리가 특정 경로에서만 실행되는 경우 해당 경로 아래에 인덱스를 만듭니다. 색인이 저장소의 루트에 상주할 필요는 없습니다.
* 색인화되는 모든 속성이 Lucene에서 기본적으로 가능한 한 많은 속성 제한을 평가할 수 있도록 하는 것과 관련된 경우 단일 색인을 사용하십시오. 또한 조인을 수행하는 경우에도 쿼리는 하나의 색인만 사용합니다.

### 복사 시 읽기 {#copyonread}

`NodeStore`이(가) 원격으로 저장되는 경우 `CopyOnRead` 옵션을 사용할 수 있습니다. 이 옵션을 사용하면 원격 인덱스를 읽을 때 로컬 파일 시스템에 작성됩니다. 이렇게 하면 이러한 원격 인덱스에 대해 자주 실행되는 쿼리의 성능을 개선하는 데 도움이 될 수 있습니다.

이는 **LuceneIndexProvider** 서비스 아래의 OSGi 콘솔에서 구성할 수 있으며 Oak 1.0.13부터 기본적으로 활성화됩니다.

### 인덱스 제거 중 {#removing-indexes}

색인을 제거할 때는 항상 `type` 속성을 `disabled`(으)로 설정하여 색인을 일시적으로 비활성화하고 응용 프로그램이 제대로 작동하는지 확인한 후에 실제로 삭제하는 것이 좋습니다. 색인은 비활성화 상태에서 업데이트되지 않으므로 다시 활성화하면 올바른 콘텐츠가 없을 수 있으며 색인을 다시 지정해야 할 수 있습니다.

TarMK 인스턴스에서 속성 인덱스를 제거한 후 압축을 실행하여 사용 중이던 디스크 공간을 회수해야 합니다. Lucene 인덱스의 경우 실제 인덱스 컨텐츠가 BlobStore에 있으므로 데이터 저장소 가비지 수집이 필요합니다.

MongoDB 인스턴스에서 인덱스를 제거할 때 삭제 비용은 인덱스의 노드 수에 비례합니다. 큰 색인을 삭제하면 문제가 발생할 수 있으므로 권장 접근 방법은 **oak-mongo.js**&#x200B;와 같은 도구를 사용하여 색인을 비활성화하고 유지 관리 기간 동안에만 삭제하는 것입니다. 이 접근 방식은 데이터 불일치를 초래할 수 있으므로 일반 노드 콘텐츠에 대해서는 사용해서는 안 됩니다.

>[!NOTE]
>
>oak-mongo.js에 대한 자세한 내용은 Oak 설명서의 [명령줄 도구 섹션](https://jackrabbit.apache.org/oak/docs/command_line.html)을 참조하십시오.

### JCR 쿼리 치트 시트 {#jcrquerycheatsheet}

효율적인 JCR 쿼리 및 색인 정의를 만들 수 있도록 [JCR 쿼리 치트 시트](assets/JCR_query_cheatsheet-v1.1.pdf)를 다운로드하여 개발 중 참조할 수 있습니다. 여기에는 쿼리 성능이 다양한 여러 시나리오를 포괄하는 QueryBuilder, XPath, SQL-2에 대한 샘플 쿼리가 포함되어 있습니다. 이 치트시트는 또한 Oak 색인을 구축하거나 사용자 정의하는 방법에 대한 권장 사항도 제공합니다. 이 치트시트의 콘텐츠는 AEM 6.5, AEM 6.5 LTS 및 AEM as a Cloud Service에 적용됩니다.

## 리인덱싱 {#re-indexing}

이 섹션에서는 Oak 색인을 다시 색인화하는 **only** 허용 이유에 대해 간략히 설명합니다.

아래 설명된 이유 외에 Oak 인덱스 리인덱스를 시작하면 동작이 변경되거나 문제가 해결되고, AEM에서 로드가 불필요하게 증가합니다. **아니요**.

아래 표에서 이유를 다루지 않는 한 Oak 인덱스의 리인덱싱을 피해야 합니다.

>[!NOTE]
>
>리인덱싱이 유용한지 확인하기 위해 아래 표를 참조하기 전에 **always**:
>
>* 쿼리가 올바릅니다
>* 쿼리가 예상 인덱스로 확인됩니다([쿼리 설명](/help/sites-administering/operations-dashboard.md#diagnosis-tools) 사용).
>* 색인 지정 프로세스가 완료되었습니다.
>

### Oak 색인 구성 변경 사항 {#oak-index-configuration-changes}

Oak 색인을 다시 색인화하는 데 허용되는 유일한 조건은 Oak 색인의 구성이 변경된 경우입니다.

*리인덱싱은 항상 AEM의 전체 성능에 미치는 영향을 적절히 고려하여 접근해야 하며 활동이 적은 기간 또는 유지 관리 기간 동안 수행되어야 합니다.*

해결책과 함께 다음과 같은 가능한 문제에 대해 자세히 설명합니다.

* [속성 인덱스 정의 변경](#property-index-definition-change)
* [Lucene 색인 정의 변경](#lucene-index-definition-change)

#### 속성 인덱스 정의 변경 {#property-index-definition-change}

* 적용 대상/경우:

   * 모든 Oak 버전
   * [속성 인덱스](https://jackrabbit.apache.org/oak/docs/query/property-index.html)만

* 증상:

   * 속성 인덱스의 정의 업데이트 이전에 존재하는 노드가 결과에서 누락됨

* 확인 방법:

   * 업데이트된 인덱스 정의를 배포하기 전에 누락된 노드가 생성/수정되었는지 확인합니다.
   * 인덱스의 수정 시간과 비교하여 누락된 노드의 `jcr:created` 또는 `jcr:lastModified` 속성을 확인합니다.

* 해결 방법:

   * Lucene 인덱스를 [다시 인덱싱](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index)
   * 또는 누락된 노드에 대한 터치(양성 쓰기 작업 수행)

      * 수동 터치 또는 사용자 지정 코드 필요
      * 누락된 노드 집합을 알아야 함
      * 노드의 모든 속성을 변경해야 합니다.

#### Lucene 색인 정의 변경 {#lucene-index-definition-change}

* 적용 대상/경우:

   * 모든 Oak 버전
   * [Lucene 인덱스](https://jackrabbit.apache.org/oak/docs/query/lucene.html)만

* 증상:

   * Lucene 인덱스에 예상 결과를 포함하지 않음
   * 쿼리 결과가 색인 정의의 예상 동작을 반영하지 않습니다.
   * 쿼리 계획이 색인 정의를 기반으로 예상 출력을 보고하지 않음

* 확인 방법:

   * Lucene 인덱스 통계 JMX Mbean(LuceneIndex), 메서드 `diffStoredIndexDefinition`을(를) 사용하여 인덱스 정의가 변경되었는지 확인하십시오.

* 해결 방법:

   * 1.6 이전 Oak 버전:

      * Lucene 인덱스를 [다시 인덱싱](#how-to-re-index)

   * Oak 버전 1.6+

      * 기존 콘텐츠가 변경 사항의 영향을 받지 않는 경우 새로 고침만 필요합니다

         * [oak:queryIndexDefinition]@refresh=true를 설정하여 lucene 인덱스를 [새로 고침](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition)

      * Lucene 인덱스를 [다시 인덱싱](#how-to-re-index)합니다.

         * 참고: 마지막 양호한 리인덱싱 (또는 초기 인덱싱)의 인덱스 상태는 새 리인덱싱이 트리거될 때까지 사용됩니다

### 오류 및 예외 상황 {#erring-and-exceptional-situations}

다음 표에서는 Oak 인덱스를 리인덱싱하여 문제를 해결하는 허용되는 오류 및 예외적인 상황만 설명합니다.

AEM에서 아래 설명된 기준과 일치하지 않는 문제가 발생하는 경우 문제를 해결하지 않으므로 **색인을 다시 색인화하지 마십시오**.

해결책과 함께 다음과 같은 가능한 문제에 대해 자세히 설명합니다.

* [Lucene 인덱스 바이너리가 누락되었습니다.](#lucene-index-binary-is-missing)
* [Lucene 인덱스 바이너리가 손상되었습니다.](#lucene-index-binary-is-corrupt)

#### Lucene 인덱스 바이너리가 누락되었습니다. {#lucene-index-binary-is-missing}

* 적용 대상/경우:

   * 모든 Oak 버전
   * [Lucene 인덱스](https://jackrabbit.apache.org/oak/docs/query/lucene.html)만

* 증상:

   * Lucene 인덱스에 예상 결과를 포함하지 않음

* 확인 방법:

   * 오류 로그 파일에 Lucene 인덱스의 바이너리가 누락되었다는 예외가 있습니다.

* 해결 방법:

   * 트래버스 저장소 검사를 수행합니다. 예를 들면 다음과 같습니다.

     [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

     저장소를 트래버스하면 다른 바이너리(lucene 파일 제외)가 누락되었는지 여부를 결정합니다

   * Lucene 인덱스 이외의 바이너리가 누락된 경우 백업에서 복원
   * 그렇지 않으면 [다시 인덱싱](#how-to-re-index) *모두* Lucene 인덱스
   * 메모:

     이 조건은 모든 바이너리(예: 에셋 바이너리)가 누락될 수 있는 잘못 구성된 데이터 저장소를 나타냅니다.

     이 경우 저장소의 마지막 알려진 양호한 버전으로 복원하여 누락된 모든 바이너리를 복구합니다.

#### Lucene 인덱스 바이너리가 손상되었습니다. {#lucene-index-binary-is-corrupt}

* 적용 대상/경우:

   * 모든 Oak 버전
   * [Lucene 인덱스](https://jackrabbit.apache.org/oak/docs/query/lucene.html)만

* 증상:

   * Lucene 인덱스에 예상 결과를 포함하지 않음

* 확인 방법:

   * `AsyncIndexUpdate`(5초마다)이(가) 실패하고 error.log에 예외가 발생합니다.

     `...a Lucene index file is corrupt...`

* 해결 방법:

   * Lucene 인덱스의 로컬 복사본 제거

      1. AEM 중지
      1. `crx-quickstart/repository/index`에서 Lucene 인덱스의 로컬 복사본을 삭제합니다.
      1. AEM 다시 시작

   * 이렇게 해도 문제가 해결되지 않고 `AsyncIndexUpdate` 예외가 지속되는 경우:

      1. 오류 인덱스를 [다시 인덱싱](#how-to-re-index)
      1. [Adobe 지원](https://helpx.adobe.com/kr/support.html) 티켓도 제출하세요.

### 색인 재지정 방법 {#how-to-re-index}

>[!NOTE]
>
>AEM 6.5 LTS에서 [oak-run.jar은(는) MongoMK 또는 RDBMK 리포지토리에서 리인덱싱하는 유일한 지원 방법](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree)입니다.

#### 속성 인덱스 리인덱싱 {#re-indexing-property-indexes}

* [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing)을(를) 사용하여 속성 인덱스를 다시 인덱싱하십시오.
* 속성 인덱스에서 async-reindex 속성을 true로 설정합니다.

   * `[oak:queryIndexDefinition]@reindex-async=true`

* **PropertyIndexAsyncReindex** MBean;

  예를 들어,

  [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Lucene 속성 인덱스 리인덱싱 {#re-indexing-lucene-property-indexes}

* [oak-run.jar를 사용하여 Lucene 속성 인덱스를 다시 인덱싱](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing)합니다.
* lucene 속성 인덱스에서 async-reindex 속성을 true로 설정합니다.

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>이전 섹션에서는 Oak 컨텍스트에서 [Apache Oak 설명서](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)의 AEM 리인덱싱 지침을 요약하고 프레임화합니다.

### 바이너리의 텍스트 사전 추출 {#text-pre-extraction-of-binaries}

텍스트 사전 추출은 바이너리에서 텍스트를 추출 및 처리하고, 격리된 프로세스를 통해 데이터 저장소에서 직접 텍스트를 추출하고, 추출된 텍스트를 Oak 인덱스의 후속 리인덱싱에 직접 노출하는 프로세스입니다.

* Oak 텍스트 사전 추출은 추출 가능한 텍스트(예: PDF, Word 문서, PPT, TXT 등)가 포함된 대량의 파일(바이너리)이 있는 저장소에서 배포된 Oak 인덱스를 통해 전체 텍스트 검색에 적합한 Lucene 인덱스(예: `/oak:index/damAssetLucene`)를 다시 인덱싱/인덱싱하는 데 권장됩니다.
* 텍스트 사전 추출은 속성 색인이 바이너리에서 텍스트를 추출하지 않으므로 Oak 속성 색인이 아닌 Lucene 색인의 재색인화에만 도움이 됩니다.
* 텍스트 사전 추출은 텍스트가 많은 바이너리(PDF, Doc, TXT 등)를 전체 텍스트 리인덱싱하는 경우 긍정적인 영향이 크지만, 이미지에 추출 가능한 텍스트가 포함되어 있지 않아 이미지 리포지토리의 효율성이 동일하지 않습니다.
* 텍스트 사전 추출은 전체 텍스트 검색 관련 텍스트 추출을 매우 효율적인 방식으로 수행하고, 이를 사용하기 매우 효율적인 방식으로 Oak 재인덱싱 프로세스에 노출합니다.

#### 텍스트 사전 추출은 언제 사용할 수 있습니까? {#when-can-text-pre-extraction-be-used}

이진 추출이 활성화된 **기존** Lucene 인덱스 리인덱싱

* 리포지토리의 **모두** 후보 콘텐츠 처리를 리인덱싱합니다. 따라서 전체 텍스트를 추출할 바이너리가 많거나 복잡하면 전체 텍스트 추출을 수행하는 데 더 많은 계산 부담이 AEM에 발생합니다. 텍스트 사전 추출은 텍스트 추출의 &quot;계산적으로 비용이 많이 드는 작업&quot;을 AEM의 데이터 저장소에 직접 액세스하는 격리된 프로세스로 이동하여 AEM에서의 오버헤드와 리소스 경합을 방지합니다.

이진 추출을 사용하여 AEM에 **new** Lucene 인덱스 배포를 지원합니다.

* 이진 추출이 활성화된 새 색인이 AEM에 배포되면 Oak은 다음에 비동기 전체 텍스트 색인 실행을 위해 모든 후보 콘텐츠를 자동으로 색인화합니다. 위의 리인덱싱에 설명된 것과 동일한 이유로 AEM에 과도한 부하가 걸릴 수 있습니다.

#### 텍스트 사전 추출을 사용할 수 없는 경우는 언제입니까? {#when-can-text-pre-extraction-not-be-used}

텍스트 사전 추출은 저장소에 추가된 새 콘텐츠에 사용할 수 없으며 필요하지 않습니다.

새 콘텐츠가 저장소에 추가되면 비동기 전체 텍스트 인덱싱 프로세스(기본적으로 5초마다)에 의해 자연스럽고 점진적으로 인덱싱됩니다.

AEM의 정상적인 작동 시(예: 웹 UI를 통해 Assets을 업로드하거나 Assets의 프로그래밍 방식 수집) AEM은 자동으로 증분 전체 텍스트 색인에 새 바이너리 콘텐츠를 기록합니다. 데이터의 양이 증분적이고 비교적 적기 때문에(약 5초 내에 저장소에 지속할 수 있는 데이터의 양) AEM은 전체 시스템 성능에 영향을 주지 않고 색인화 중에 바이너리에서 전체 텍스트 추출을 수행할 수 있습니다.

#### 텍스트 사전 추출 사용 사전 요구 사항 {#prerequisites-to-using-text-pre-extraction}

* 전체 텍스트 이진 추출을 수행하는 Lucene 인덱스를 리인덱싱하거나 기존 콘텐츠의 전체 텍스트 인덱스 바이너리를 만드는 새 인덱스를 배포하게 됩니다
* 텍스트를 사전 추출할 컨텐츠(바이너리)는 저장소에 있어야 합니다
* CSV 파일을 생성하고 최종 리인덱싱을 수행하는 유지 관리 창
* Oak 버전: 1.0.18+, 1.2.3+
* [oak-run.jar](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)버전 1.7.4+
* 인덱싱 AEM 인스턴스에서 액세스할 수 있는 추출된 텍스트를 저장하는 파일 시스템 폴더/공유

   * 텍스트 사전 추출 OSGi 구성에는 추출된 텍스트 파일에 대한 파일 시스템 경로가 필요하므로 AEM 인스턴스(로컬 드라이브 또는 파일 공유 마운트)에서 직접 액세스할 수 있어야 합니다

#### 텍스트 사전 추출을 수행하는 방법 {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***아래에 요약된 oak-run.jar 명령이 [https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***&#x200B;에서 완전히 열거되었습니다.
>
>위의 다이어그램과 아래 단계는 Apache Oak 설명서에 요약된 기술 텍스트 사전 추출 단계를 설명하고 보완하는 역할을 합니다.

![텍스트 추출 전 프로세스 흐름](assets/chlimage_1-139.png)

**미리 추출할 콘텐츠 목록 생성**

*유지 관리 기간/사용 빈도가 낮은 기간 동안 이 작업 중에 노드 저장소가 통과하므로 1단계(a-b)를 실행하십시오. 시스템에 상당한 부하가 발생할 수 있습니다.*

1a. 텍스트를 미리 추출할 노드 목록을 만들려면 `oak-run.jar --generate`을(를) 실행하십시오.

1b. 노드 목록(1a)은 파일 시스템에 CSV 파일로 저장됩니다

`--generate`이(가) 실행되고 **new** CSV 파일이 생성될 때마다 oak-run 명령의 경로에 지정된 대로 전체 노드 저장소가 트래버스됩니다. CSV 파일이 텍스트 추출 전 프로세스의 개별 실행(단계 1 - 2) 간에 **다시 사용되지 않음**&#x200B;입니다.

**파일 시스템에 텍스트 미리 추출**

*단계 2(a-c)는 AEM이 데이터 저장소와만 상호 작용하므로 정상적인 작동 중에 실행될 수 있습니다.*

2a. `oak-run.jar --tika`을(를) 실행하여 (1b)에서 생성된 CSV 파일에 열거된 이진 노드에 대한 텍스트를 미리 추출합니다.

2b. (2a)에서 시작된 프로세스는 데이터 저장소의 CSV에 정의된 이진 노드에 직접 액세스하고 텍스트를 추출합니다.

2c. 추출된 텍스트는 Oak 리인덱싱 프로세스 (3a)에서 수집하는 형식으로 파일 시스템에 저장됩니다

미리 추출된 텍스트는 바이너리 지문에 의해 CSV로 식별된다. 이진 파일이 동일한 경우 AEM 인스턴스 간에 동일한 미리 추출된 텍스트를 사용할 수 있습니다. AEM Publish는 일반적으로 AEM Author의 하위 집합이므로 AEM Author에서 미리 추출된 텍스트는 종종 AEM Publish를 다시 색인화하는 데 사용할 수 있습니다(AEM Publish에 추출된 텍스트 파일에 대한 파일 시스템 액세스 권한이 있다고 가정).

미리 추출된 텍스트는 시간이 지남에 따라 증분적으로에 추가될 수 있습니다. 텍스트 사전 추출은 이전에 추출된 바이너리에 대한 추출을 건너뛰므로 나중에 다시 인덱싱해야 하는 경우(추출된 콘텐츠가 엄청나게 크지 않다고 가정할 경우) 사전 추출된 텍스트를 유지하는 것이 좋습니다. 그럴 경우 텍스트가 잘 압축되므로 중간에 내용을 압축하는 것을 평가합니다.

**Oak 인덱스 다시 인덱싱, 추출된 텍스트 파일에서 전체 텍스트 소싱**

*유지 관리/사용 중지 기간 동안 이 작업 중에 노드 저장소가 통과되어 시스템에 상당한 부하가 발생할 수 있으므로 리인덱싱을 실행합니다(3a-b단계).*

3a. AEM에서 Lucene 인덱스 [리인덱싱](#how-to-re-index)을(를) 호출합니다.

3b. Apache Jackrabbit Oak DataStore PreExtractedTextProvider OSGi 구성(파일 시스템 경로를 통해 추출된 텍스트를 가리키도록 구성됨)은 Oak이 추출된 파일에서 전체 텍스트 텍스트를 소스화하도록 지시하고 저장소에 저장된 데이터에 직접 부딪치고 처리하지 않습니다.
