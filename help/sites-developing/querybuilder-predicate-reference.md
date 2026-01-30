---
title: 쿼리 빌더 조건자 참조
description: Query Builder API에 대한 전체 설명 참조.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Developing,Search,Query Builder
role: Developer
exl-id: c044d541-24d6-4975-9b38-6a4317a16358
source-git-commit: a85b54d5a7c3b00f95f439941a390dcfee883187
workflow-type: tm+mt
source-wordcount: '2291'
ht-degree: 1%

---

# 쿼리 빌더 조건자 참조{#query-builder-predicate-reference}

>[!CAUTION]
>
>이 페이지의 정보는 완전하지 않습니다.
>
>자세한 내용은 Query Builder 디버거 콘솔의 **사용 가능한 조건자** 아래 목록을 참조하십시오. 예:
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>예를 들어 다음을 참조하십시오.
>
>* [http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)

## 일반 {#general}

* [루트](#root)
* [그룹](#group)
* [orderby](#orderby)

## 술어 {#predicates}

* [부울 속성](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [날짜 비교](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [다터랑주](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludepaths](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [전체 텍스트](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [언어](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [주요 자산](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [가공되지 않음](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [경로](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [속성](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [상대 날짜 범위](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [유사](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [태그](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [태그](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [유형](/help/sites-developing/querybuilder-predicate-reference.md#type)

### `boolproperty` {#boolproperty}

JCR 부울 속성에서 일치합니다. 값 &quot; `true`&quot; 및 &quot; `false`&quot;만 허용합니다. &quot; `false`&quot;(으)로 설정된 경우 속성에 &quot; `false`&quot; 값이 있는지 또는 속성이 전혀 없는 경우 일치합니다. 활성화된 경우에만 설정되는 부울 플래그를 확인하는 데 유용합니다.

상속된 &quot; `operation`&quot; 매개 변수에 의미가 없습니다.

패싯 추출을 지원합니다. 각 `true` 또는 `false` 값에 대한 버킷을 제공하지만 기존 속성에 대해서만 제공합니다.

#### 속성 {#properties}

* **부울 속성**
속성에 대한 상대 경로입니다(예: `myFeatureEnabled` 또는 `jcr:content/myFeatureEnabled`).

* **값**
속성 확인 값, &quot; `true`&quot; 또는 &quot; `false`&quot;.

### `contentfragment` {#contentfragment}

결과를 콘텐츠 조각으로 제한합니다.

필터링을 지원하지 않습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-1}

* **contentfragment**
모든 값과 함께 사용하여 콘텐츠 조각을 확인할 수 있습니다.

### `dateComparison` {#datecomparison}

두 JCR DATE 속성을 비교합니다. 같음, 같지 않음, 크거나 같음 또는 같은지 테스트할 수 있습니다.

필터링 전용 조건자이며 검색 색인을 사용할 수 없습니다.

#### 속성 {#properties-2}

* **property1**

  첫 번째 날짜 속성에 대한 경로입니다.

* **속성2**

  두 번째 날짜 속성에 대한 경로입니다.

* **작업**

  정확히 일치하는 항목의 경우 &quot; `equals`&quot;, 같지 않음 비교의 경우 &quot; `!=`&quot;, property1의 경우 property2보다 큼, property1의 경우 &quot; `greater`&quot;이 property2보다 크거나 같음. `>=` 기본값은 &quot; `equals`&quot;입니다.

### `daterange` {#daterange}

날짜 및 시간 간격에 대해 JCR DATE 속성과 일치합니다. ISO8601 사용
날짜 및 시간 형식(`YYYY-MM-DDTHH:mm:ss.SSSZ`)을 지정하고 `YYYY-MM-DD`과 같은 부분 표현도 허용합니다. 또는 UTC 시간대(UNIX® 시간 형식)에서 타임스탬프가 1970년 이후 밀리초 수로 제공될 수 있습니다.

두 타임스탬프 사이에 있는 모든 항목, 지정된 날짜보다 최신 항목 또는 오래된 항목을 찾을 수 있으며 포함 간격과 열기 간격 사이에서 선택할 수도 있습니다.

패싯 추출을 지원합니다. 버킷에 &quot;오늘&quot;, &quot;이번 주&quot;, &quot;이번 달&quot;, &quot;지난 3개월&quot;, &quot;올해&quot;, &quot;지난해&quot; 및 &quot;지난해보다 이전&quot;을 제공합니다.

필터링을 지원하지 않습니다.

#### 속성 {#properties-3}

* **속성**

  `DATE` 속성에 대한 상대 경로입니다(예: `jcr:lastModified`).

* **lowerBound**

  `2014-10-01`과(와) 같은 속성을 확인하기 위해 바인딩된 하한 날짜입니다.

* **lowerOperation**

  &quot; `>`&quot;(이후) 또는 &quot; `>=`&quot;(이후)이(가) `lowerBound`에 적용됩니다. 기본값은 &quot; `>`&quot;입니다.

* **upperBound**

  `2014-10-01T12:15:00`과(와) 같은 속성을 검사할 상한입니다.

* **upperOperation**

  &quot; `<`&quot;(이전) 또는 &quot; `<=`&quot;(이후)이(가) `upperBound`에 적용됩니다. 기본값은 &quot; `<`&quot;입니다.

* **표준 시간대**

  ISO-8601 날짜 문자열로 제공되지 않을 때 사용할 표준 시간대의 ID입니다. 기본값은 시스템의 기본 시간대입니다.

### `excludepaths` {#excludepaths}

해당 경로가 정규 표현식과 일치하는 결과에서 노드를 제외합니다.

필터링 전용 조건자이며 검색 색인을 사용할 수 없습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-4}

* **excludepaths**

  결과 경로에 대해 일치하는 정규 표현식이며 결과에서 일치하는 정규 표현식은 제외됩니다.

### `fulltext` {#fulltext}

전체 텍스트 색인에서 용어를 검색합니다.

필터링을 지원하지 않습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-5}

* **전체 텍스트**

  전체 텍스트 검색어입니다.

* **relPath**

  속성 또는 하위 노드에서 검색할 상대 경로입니다. 이 속성은 선택 사항입니다.

### `group` {#group}

중첩된 조건을 작성할 수 있습니다. 그룹은 중첩 그룹을 포함할 수 있습니다. 쿼리 빌더 쿼리의 모든 항목이 암시적으로 루트 그룹에 있으며, 여기에는 `p.or` 및 `p.not` 매개 변수도 있을 수 있습니다.

값에 대해 두 속성 중 하나를 일치시키는 예제:

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

개념적으로 `(1_property` 또는 `2_property)`입니다.

중첩 그룹의 예:

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

**의 페이지 또는**&#x200B;의 에셋에서 &quot;`/content/geometrixx/en`관리`/content/dam/geometrixx`&quot;이라는 용어를 검색합니다.

개념적으로 `fulltext AND ( (path AND type) OR (path AND type) )`입니다. 이러한 OR 조인은 성능을 위해 좋은 색인이 필요합니다.

#### 속성 {#properties-6}

* **p.or**

  &quot; `true`&quot;(으)로 설정된 경우 그룹의 한 조건자만 일치해야 합니다. 기본값은 &quot; `false`&quot;입니다. 즉, 모두 일치해야 합니다.

* **p.not**

  &quot; `true`&quot;(으)로 설정된 경우 그룹을 부정합니다(기본값: &quot; `false`&quot;).

* **&lt;조건자>**

  중첩된 술어를 추가합니다.

* **N_&lt;조건자>**

  `1_property, 2_property, ...`과(와) 같이 중첩된 여러 술어를 동시에 추가합니다.

### hasPermission {#haspermission}

현재 세션에 지정된 [JCR 권한이 있는 항목으로 결과를 제한합니다.](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

필터링 전용 조건자이며 검색 색인을 사용할 수 없습니다. 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-7}

* **hasPermission**

  현재 사용자 세션에 해당 노드가 반드시 있어야 하는 쉼표로 구분된 JCR 권한입니다. 예: `jcr:write`, `jcr:modifyAccessControl`.

### `language` {#language}

특정 언어로 CQ 페이지를 찾습니다. 이렇게 하면 페이지 언어 속성과 종종 최상위 사이트 구조에 언어 또는 로케일을 포함하는 페이지 경로를 모두 볼 수 있습니다.

필터링 전용 조건자이며 검색 색인을 사용할 수 없습니다.

패싯 추출을 지원합니다. 각 고유 언어 코드에 대한 버킷을 제공합니다.

#### 속성 {#properties-8}

* **언어**

  ISO 언어 코드(예: &quot;`de`&quot;).

### `mainasset` {#mainasset}

노드가 DAM 주 자산이고 하위 자산이 아닌지 확인합니다. 기본적으로 모든 노드는 &quot;하위 자산&quot; 노드 내에 있지 않습니다. `dam:Asset` 노드 형식을 확인하지 않습니다. 이 조건자를 사용하려면 &quot; `mainasset=true`&quot; 또는 &quot; `mainasset=false`&quot;을(를) 설정하십시오. 추가 속성이 없습니다.

필터링 전용 조건자이며 검색 색인을 사용할 수 없습니다.

Facet 추출을 지원하고 기본 및 하위 에셋에 대해 두 개의 버킷을 제공합니다.

#### 속성 {#properties-9}

* **주 자산**

  부울, 기본 자산의 경우 &quot; `true`&quot;, 하위 자산의 경우 &quot; `false`&quot;.

### memberOf {#memberof}

특정 [sling 리소스 컬렉션](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)에 속하는 항목을 찾습니다.

필터링 전용 조건자이며 검색 색인을 사용할 수 없습니다. 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-10}

* **memberOf**

  Sling 리소스 컬렉션 경로.

### `nodename` {#nodename}

JCR 노드 이름에서 일치합니다.

패싯 추출을 지원합니다. 각 고유한 노드 이름(파일 이름)에 대한 버킷을 제공합니다.

#### 속성 {#properties-11}

* **nodename**

  와일드카드를 허용하는 노드 이름 패턴입니다. `*` = any or no char, `?` = any char, `[abc]` = 대괄호 안의 문자만.

### `notexpired` {#notexpired}

JCR DATE 속성이 현재 서버 시간보다 크거나 같은지 확인하여 항목을 일치시킵니다. 날짜 속성과 같은 &quot; `expiresAt`&quot;을(를) 확인하고 아직 만료되지 않았거나( `notexpired=true`) 이미 만료된 것( `notexpired=false`)으로만 제한하는 데 사용할 수 있습니다.

필터링을 지원하지 않습니다.

데이터 범위 술어와 동일한 방식으로 패싯 추출을 지원합니다.

#### 속성 {#properties-12}

* **notexpired**

  부울, 아직 만료되지 않은 경우 &quot; `true`&quot;(미래 날짜 또는 같음), 만료된 경우 &quot; `false`&quot;(과거 날짜)(필수).

* **속성**

  확인할 `DATE` 속성에 대한 상대 경로입니다(필수).

### `orderby` {#orderby}

결과를 정렬할 수 있습니다. 여러 속성별 순서 지정이 필요한 경우 숫자 접두사를 사용하여 이 조건자를 여러 번 추가해야 합니다(예: `1_orderby=first`, `2_oderby=second`).

#### 속성 {#properties-13}

* **orderby**

  선행 @으로 표시되는 JCR 속성 이름(예: `@jcr:lastModified` 또는 `@jcr:content/jcr:title`) 또는 쿼리의 다른 조건자(예: `2_property`)로서 정렬할 대상입니다.

* **정렬**

  정렬 방향입니다. 내림차순의 경우 &quot; `desc`&quot;, 오름차순의 경우 &quot; `asc`&quot;(기본값).

* **사례**

  `ignore`(으)로 설정하면 대소문자를 구분하지 않습니다. 즉, &quot;a&quot;가 &quot;B&quot; 앞에 옵니다. 비어 있거나 누락된 경우 정렬은 대소문자를 구분합니다. 즉, &quot;B&quot;가 &quot;a&quot; 앞에 옵니다.

### `path` {#path}

지정된 경로 내에서 검색합니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-14}

* **path**

  경로 패턴. `exact=false`(기본값)이면 XPath에서 `//*`을(를) 추가하는 것과 비슷하게 지정된 경로 아래의 전체 하위 트리가 검색되지만 기본 경로 자체는 포함되지 않습니다. `exact=true`에서 검색은 `*`개의 와일드카드를 포함할 수 있는 정확한 경로만 일치시킵니다. `self`이(가) 설정된 경우 검색에는 기본 노드 및 전체 하위 트리가 포함됩니다.


* **정확한**

  `exact`이(가) true(on)이면 정확한 경로가 일치해야 하지만 이름에 일치하는 단순 와일드카드(`*`)를 포함할 수 있지만 &quot; `/`&quot;은(는) 아닙니다. false(기본값)이면 모든 하위 항목이 포함됩니다(선택 사항).

* **플랫**

  직접 하위만 검색합니다(`/*`에 &quot; `xpath`&quot; 추가 등)(&#39; `exact`&#39;이(가) true가 아닌 경우에만 사용됨, 선택 사항).

* **자체**

  하위 트리를 검색하지만 경로로 지정된 기본 노드를 포함합니다(와일드카드 없음).

### `property` {#property}

JCR 속성 및 해당 값에 대해 일치합니다.

패싯 추출을 지원합니다. 결과의 각 고유 속성 값에 대한 버킷을 제공합니다.

#### 속성 {#properties-15}

* **속성**

  속성에 대한 상대 경로입니다(예: `jcr:title`).

* **값**

  속성을 확인할 값입니다. JCR 속성 유형을 따라 문자열 전환으로 이동합니다.

* **N_value**

  `1_value`, `2_value`, ...을(를) 사용하여 여러 값(기본적으로 `OR`과(와) 결합됨, and=true인 경우 `AND`(5.3 이후) 확인

* **및**

  여러 값(`N_value`)을 AND(5.3 이후)와 결합하려면 true로 설정하십시오.

* **작업**

  정확한 일치(기본값)에는 `equals`을(를) 사용하고 같지 않음 비교에는 `unequals`을(를) 사용합니다. 선택적 `like` XPath 함수를 적용하려면 `jcr:like`을(를) 사용하십시오. 일치 항목 없이 `not`을(를) 사용합니다(예: XPath의 `not(@prop)`). 이 경우 `value` 매개 변수는 무시됩니다. `exists`을(를) 사용하여 속성이 있는지 확인합니다. `true`(기본값)에는 속성이 필요하며 `false`은(는) `not`과(와) 동일합니다.

* **깊이**

  속성과 상대 경로가 존재할 수 있는 와일드카드 수준의 수입니다. 예를 들어 `property=size depth=2`은(는) 노드 및 크기, node/&amp;ast;/size 및 node/&amp;ast;/&amp;ast;/size를 확인합니다.

### `rangeproperty` {#rangeproperty}

간격에 대해 JCR 속성과 일치합니다. `LONG`, `DOUBLE` 및 `DECIMAL`과(와) 같은 선형 형식의 속성에 적용됩니다. `DATE`에 대해 날짜 형식 입력을 최적화한 데이터 범위 조건자를 참조하십시오.

하한과 상한을 정의하거나 둘 중 하나만 정의할 수 있습니다. 작업(예: &quot;보다 작음&quot; 또는 &quot;작거나 같음&quot;)은 하한과 상한에 대해서도 개별적으로 지정할 수 있습니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-16}

* **속성**

  속성에 대한 상대 경로입니다.

* **lowerBound**

  다음에 대한 속성을 확인할 하한입니다.

* **lowerOperation**

  &quot; `>`&quot;(기본값) 또는 &quot; `>=`&quot;이(가) `lowerValue`에 적용됩니다.

* **upperBound**

  다음에 대한 속성을 확인할 상한입니다.

* **upperOperation**

  &quot; `<`&quot;(기본값) 또는 &quot; `<=`&quot;이(가) `lowerValue`에 적용됩니다.

* **소수점**

  확인된 속성이 Decimal 형식인 경우 &quot; `true`&quot;

### `relativedaterange` {#relativedaterange}

현재 서버 시간을 기준으로 시간 오프셋을 사용하여 날짜 및 시간 간격에 대해 `JCR DATE` 속성을 일치시킵니다. 밀리초 값 또는 bugzilla 구문 `lowerBound`을(를) 사용하여 `upperBound` 및 `1s 2m 3h 4d 5w 6M 7y`을(를) 지정할 수 있습니다. 현재 시간 이전의 음수 오프셋을 나타내려면 &quot; `-`&quot;을(를) 접두사로 사용하십시오. `lowerBound` 또는 `upperBound`만 지정하는 경우 나머지 값은 0으로 설정되며, 이는 현재 시간을 의미합니다.

예:

* `upperBound=1h`(및 `lowerBound` 없음)이(가) 다음 시간 내에 모든 항목을 선택합니다.
* `lowerBound=-1d`(및 `upperBound` 없음)이(가) 지난 24시간 동안 아무 것도 선택하지 않습니다.
* `lowerBound=-6M`과(와) `upperBound=-3M`이(가) 6개월에서 3개월 된 항목을 선택합니다.
* `lowerBound=-1500`과(와) `upperBound=5500`은(는) 과거 1500밀리초에서 향후 5500밀리초 사이의 모든 항목을 선택합니다.
* `lowerBound=1d` 및 `upperBound=2d`이(가) 내일 모레 아무 항목이나 선택합니다.

윤년은 고려하지 않고 모든 달은 30일입니다.

필터링을 지원하지 않습니다.

데이터 범위 술어와 동일한 방식으로 패싯 추출을 지원합니다.

#### 속성 {#properties-17}

* **upperBound**

  현재 서버 시간과 관련하여 밀리초 또는 `1s 2m 3h 4d 5w 6M 7y`(1초, 2분, 3시간, 4일, 5주, 6개월, 7년)으로 바인딩된 상한값입니다. 음수 오프셋의 경우 &quot;-&quot;를 사용하십시오.

* **lowerBound**

  현재 서버 시간과 관련하여 `1s 2m 3h 4d 5w 6M 7y`(1초, 2분, 3시간, 4일, 5주, 6개월, 7년) 또는 밀리초로 바인딩된 더 낮은 날짜에서는 음수 오프셋을 사용하려면 &quot;-&quot;를 사용하십시오.

### `root` {#root}

루트 조건자 그룹. 그룹의 모든 기능을 지원하며 전역 쿼리 매개 변수를 설정할 수 있습니다.

&quot;루트&quot;라는 이름은 쿼리에서 사용되지 않으며 암시적입니다.

#### 속성 {#properties-18}

* **p.offset**

  결과 페이지의 시작, 즉 건너뛸 항목의 수를 나타내는 숫자입니다.

* **p.limit**

  페이지 크기를 나타내는 숫자입니다.

* **p.guessTotal**

  전체 결과 합계를 계산하는 비용을 피하기 위해 모든 일치 항목을 계산하지 마십시오. 대신 최대 합계를 최대 개수(예: `1000`)로 설정하여 사용자에게 더 작은 결과에 대한 대략적인 크기와 정확한 합계를 제공합니다. 필요한 최소값(`true`)까지만 계산하도록 `p.offset + p.limit`(으)로 설정하십시오.


* **p.extrpt**

  &quot; `true`&quot;(으)로 설정된 경우 결과에 전체 텍스트 발췌문을 포함하십시오.

* **p.hits**

  (JSON 서블릿만 해당) 다음 표준 히트(ResultHitWriter 서비스를 통해 확장 가능)를 사용하여 히트가 JSON으로 기록되는 방법을 선택합니다.

   * **단순**:

     `path`, `title`, `lastmodified`, `excerpt`과(와) 같은 최소 항목(설정된 경우).

   * **전체**:

     결과는 각 노드에 대해 Sling JSON으로 렌더링되며, `jcr:path`에 히트 경로가 표시됩니다. 기본적으로 응답에는 노드의 직접 속성만 포함됩니다. 더 자세한 내용을 포함하려면 `p.nodedepth=N`을(를) 사용하십시오. 여기서 `0`은(는) 전체 하위 트리를 반환합니다. 각 항목(`p.acls=true` = `create`, `add_node` = `modify`, `set_property` = `delete`)에 대한 현재 세션의 JCR 권한을 포함하도록 `remove`을(를) 설정합니다.


   * **선택적**:

     응답에는 상대 경로의 공백으로 구분된 목록인 `p.properties`에 나열된 속성만 포함됩니다(URL에서 `+` 사용). 상대 경로의 깊이가 1보다 크면 출력에서 이 경로를 하위 개체로 중첩합니다. 특수 `jcr:path` 속성은 항상 히트 경로를 포함합니다.


### `savedquery` {#savedquery}

지속 쿼리 빌더 쿼리의 모든 술어를 하위 그룹 술어로 현재 쿼리에 포함합니다.

추가 쿼리를 실행하지 않고 현재 쿼리를 확장합니다.

쿼리는 `QueryBuilder#storeQuery()`을(를) 사용하여 프로그래밍 방식으로 유지할 수 있습니다. Java™ 속성 형식의 텍스트 파일로 쿼리를 포함하는 `nt:file` 노드 또는 여러 줄 문자열 속성일 수 있습니다.

저장된 쿼리의 술어에 대한 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-19}

* **savedquery**

  저장된 쿼리의 경로(String 속성 또는 `nt:file` 노드)입니다.

### `similar` {#similar}

JCR XPath `rep:similar()`을(를) 사용한 유사성 검색입니다.

필터링을 지원하지 않습니다. 패싯 추출을 지원하지 않습니다.

#### 속성 {#properties-20}

* **유사**
유사한 노드를 찾을 노드의 절대 경로입니다.

* **로컬**
현재 노드의 하위 노드 또는 `.`에 대한 상대 경로입니다(선택 사항, 기본값은 &quot; `.`&quot;).

### `tag` {#tag}

태그 제목 경로를 지정하여 하나 이상의 태그로 태그가 지정된 컨텐츠를 검색합니다.

패싯 추출을 지원합니다. 현재 태그 제목 경로를 사용하여 각 고유 태그에 대한 버킷을 제공합니다.

#### 속성 {#properties-21}

* **태그**

  찾을 태그 제목 경로(예: &quot;자산 속성 : 방향 / 가로&quot;).

* **N_value**

  `1_value`, `2_value`, ...을(를) 사용하여 여러 태그(기본적으로 `OR`과(와) 결합됨, and=true인 경우 `AND`(5.6 이후) 확인

* **속성**

  확인할 속성(또는 속성에 대한 상대 경로)(기본값 &quot; `cq:tags`&quot;)

### `tagid` {#tagid}

태그 ID를 지정하여 하나 이상의 태그로 태그가 지정된 컨텐츠를 검색합니다.

패싯 추출을 지원합니다. 현재 태그 ID를 사용하여 각 고유 태그에 대한 버킷을 제공합니다.

#### 속성 {#properties-22}

* **tagid**

  태그 ID를 사용하여 찾을 수 있습니다(예: &quot; `properties:orientation/landscape`&quot;).

* **N_value**

  `1_value`, `2_value`, ...을(를) 사용하여 여러 `tagids`(기본적으로 `OR`과(와) 결합됨, and=true인 경우 `AND`(5.6 이후) 확인

* **속성**

  확인할 속성(또는 속성에 대한 상대 경로)(기본값 &quot; `cq:tags`&quot;).

### `tagsearch` {#tagsearch}

키워드를 지정하여 하나 이상의 태그로 태그가 지정된 콘텐츠를 검색합니다. 먼저 제목에 이러한 키워드가 포함된 태그를 검색한 다음 태그가 지정된 항목으로만 결과를 제한합니다.

패싯 추출을 지원하지 않습니다.

#### 속성 {#Properties-1}

* **tagsearch**

  태그 제목에서 검색할 키워드입니다.

* **속성**

  확인할 속성(또는 속성에 대한 상대 경로)(기본값 `cq:tags`).

* **lang**

  지역화된 특정 태그 제목에서만 검색하려면(예: `de`).

* **모두**

  (bool) 전체 태그, 즉 모든 제목, 설명 등을 검색합니다. &quot;l `ang`&quot;보다 우선합니다.

### `type` {#type}

결과를 기본 노드 유형 또는 믹스인 유형인 특정 JCR 노드 유형으로 제한하고 해당 노드 유형의 하위 유형을 찾습니다. 저장소 검색 인덱스는 효율적인 실행을 위해 노드 유형을 포함해야 합니다.

패싯 추출을 지원합니다. 결과의 각 고유 유형에 대한 버킷을 제공합니다.

#### 속성 {#Properties-2}

* **유형**

  검색할 노드 유형 또는 mixin 이름(예: `cq:Page`).
