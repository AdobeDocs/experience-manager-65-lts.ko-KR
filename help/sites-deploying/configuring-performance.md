---
title: 성능 최적화
description: 성능을 최적화하기 위해 AEM의 특정 측면을 구성하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: c46d9569-23e7-44e2-a072-034450f14ca2
source-git-commit: 2fcdc5df5a4b901c177d8e4158663c6b09793146
workflow-type: tm+mt
source-wordcount: '5054'
ht-degree: 16%

---

# 성능 최적화 {#performance-optimization}

>[!NOTE]
>
>성능 문제 해결 및 해결에 대한 자세한 내용은 [성능 트리](/help/sites-deploying/performance-tree.md)를 참조하십시오.
>
>또한 [성능 조정 팁](https://experienceleague.adobe.com/ko/docs/experience-cloud-kcs/kbarticles/ka-17466)에 대한 기술 자료 문서를 검토할 수 있습니다.

핵심 문제는 웹 사이트가 방문자 요청에 응답하는 데 걸리는 시간입니다. 이 값은 요청마다 다르지만 평균 대상 값을 정의할 수 있습니다. 이 값이 달성 가능하고 유지 가능한 것으로 입증되면 웹 사이트의 성능을 모니터링하고 잠재적인 문제의 발생을 나타내는 데 사용할 수 있습니다.

목표로 하는 응답 시간은 대상 대상의 서로 다른 특성을 반영하여 작성자 및 게시 환경에서 다릅니다.

## 작성 환경 {#author-environment}

이 환경은 콘텐츠를 입력하고 업데이트하는 작성자가 사용합니다. 콘텐츠 페이지 및 해당 페이지의 개별 요소를 업데이트할 때 각각 높은 수의 성능 집약적 요청을 생성하는 일부 사용자를 대상으로 해야 합니다.

## 게시 환경 {#publish-environment}

이 환경에는 사용자가 사용할 수 있는 콘텐츠가 포함되어 있습니다. 여기에서 요청 수는 훨씬 더 많으며 속도는 매우 중요합니다. 하지만 요청의 특성이 덜 동적이기 때문에 콘텐츠 캐싱 또는 로드 밸런싱과 같은 추가적인 성능 향상 메커니즘을 적용할 수 있습니다.

>[!NOTE]
>
>* 성능 최적화를 구성한 후 [힘든 날](/help/sites-developing/tough-day.md)의 절차에 따라 부하가 큰 환경을 테스트하십시오.
>* [성능 조정 팁도 참조하십시오.](https://experienceleague.adobe.com/ko/docs/experience-cloud-kcs/kbarticles/ka-17466)

## 성능 최적화 방법론 {#performance-optimization-methodology}

AEM 프로젝트에 대한 성능 최적화 방법론은 처음부터 성능 문제를 방지하기 위해 따를 수 있는 5가지 간단한 규칙으로 요약할 수 있습니다.

1. [최적화를 위한 계획](#planning-for-optimization)
1. [현실 시뮬레이션](#simulate-reality)
1. [확실한 목표 수립](#establish-solid-goals)
1. [관련 유지](#stay-relevant)
1. [애자일 반복 주기](#agile-iteration-cycles)

이러한 규칙은 일반적으로 웹 프로젝트에 적용되며 프로젝트 관리자 및 시스템 관리자와 관련되어 있어 출시 시기가 다가올 때 프로젝트에 성능 문제가 발생하지 않도록 합니다.

### 최적화를 위한 계획 {#planning-for-optimization}

![chlimage_1-3](assets/chlimage_1-3.jpeg)

성능 최적화 단계에 대한 프로젝트 작업의 약 10%를 계획합니다. 실제 성능 최적화 요구 사항은 프로젝트의 복잡성 수준과 개발 팀의 경험에 따라 다릅니다. 프로젝트에 할당된 시간이 필요하지 않을 수 있지만 제안된 영역에서 항상 성능 최적화를 계획하는 것이 좋습니다.

가능하면 전체 발표를 따르는 추가적인 부담 없이 먼저 제한된 대상자에게 프로젝트를 소프트 론칭하여 실제 경험을 수집하고 추가 최적화를 수행해야 합니다.

라이브 상태가 되면 성능 최적화는 종료되지 않습니다. 이제 시스템에서 &quot;실제&quot; 로드가 발생합니다. 출시 이후 추가 조정에 대한 계획이 중요하다.

시스템 로드가 변경되고 시스템의 성능 프로필이 시간이 지남에 따라 변경되므로 성능 &quot;조정&quot; 또는 &quot;상태 점검&quot;을 6~12개월 간격으로 예약해야 합니다.

### 현실 시뮬레이션 {#simulate-reality}

![chlimage_1-4](assets/chlimage_1-4.jpeg)

웹 사이트를 사용하여 라이브로 이동한 다음, 론치 후에 성능 문제가 발생했음을 발견하는 경우 부하 및 성능 테스트가 현실을 충분히 시뮬레이션하지 않았기 때문일 수 있습니다.

현실을 시뮬레이션하는 것은 어렵고 &quot;실제&quot;를 얻기 위해 투자하는 노력은 프로젝트의 특성에 따라 달라집니다. &quot;실제&quot;는 &quot;실제 코드&quot; 및 &quot;실제 트래픽&quot;뿐만 아니라 특히 콘텐츠 크기 및 구조에 대해 &quot;실제 콘텐츠&quot;를 의미합니다. 템플릿은 저장소의 크기와 구조에 따라 다르게 작동할 수 있습니다.

### 확실한 목표 수립 {#establish-solid-goals}

![chlimage_1-5](assets/chlimage_1-5.jpeg)

성과목표를 적절히 설정하는 것의 중요성은 과소평가되지 않는 것이다. 종종 특정 성과 목표에 집중한 후에는 이러한 목표를 가정으로 변경하더라도 나중에 변경하기가 어렵습니다.

좋은 성과 목표 수립은 정말 가장 까다로운 영역 중 하나입니다. 비교 가능한 웹 사이트(예: 새 웹 사이트의 이전 버전)에서 실제 로그 및 벤치마크를 수집하는 것이 가장 좋은 경우가 많습니다.

### 관련 유지 {#stay-relevant}

![chlimage_1-6](assets/chlimage_1-6.jpeg)

한 번에 하나의 병목 지점을 최적화하는 것이 중요합니다. 하나의 최적화가 미치는 영향을 확인하지 않고 동시에 작업을 수행하려고 하면 어떤 최적화 측정이 도움이 되었는지 추적할 수 없습니다.

### 애자일 반복 주기 {#agile-iteration-cycles}

![chlimage_1-7](assets/chlimage_1-7.jpeg)

성능 튜닝은 목표에 도달할 때까지 측정, 분석, 최적화 및 유효성 검사를 포함하는 반복적인 프로세스입니다. 이러한 측면을 고려하려면 각 반복 후 가중치가 더 높은 테스트 프로세스가 아닌 최적화 단계에서 애자일 유효성 검사 프로세스를 구현하십시오.

이 포커스는 최적화를 구현하는 개발자가 최적화가 이미 목표에 도달했는지 여부를 신속하게 파악할 수 있는 방법을 가져야 함을 의미합니다. 이 정보는 목표에 도달하면 최적화가 종료되므로 매우 중요합니다.

## 기본 성능 지침 {#basic-performance-guidelines}

일반적으로 캐시되지 않은 html 요청을 100밀리초 미만으로 유지합니다. 보다 구체적으로, 다음은 지침의 역할을 할 수 있다.

* 페이지에 대한 요청의 70%가 100밀리초 이내에 응답해야 합니다.
* 페이지에 대한 요청의 25%가 100밀리초 - 300밀리초 내에 응답을 가져와야 합니다.
* 페이지에 대한 요청의 4%가 300밀리초 - 500밀리초 내에 응답을 가져와야 합니다.
* 페이지에 대한 요청의 1%가 500밀리초 - 1000밀리초 내에 응답을 가져와야 합니다.
* 1초보다 느리게 응답하는 페이지가 없습니다.

위의 수치는 다음 조건을 가정합니다.

* 게시 시 측정됨(작성 환경과 관련된 간접비 없음)
* 서버에서 측정됨(네트워크 오버헤드 없음)
* 캐시되지 않음(AEM 출력 캐시 없음, Dispatcher 캐시 없음)
* 많은 종속성이 있는 복잡한 항목(HTML, JS, PDF, ...)에만 해당됩니다.
* 시스템에 다른 로드 없음

다음을 포함하여 성능 문제에 자주 기여하는 몇 가지 문제가 있습니다.

* Dispatcher 캐싱 비효율성
* 일반 표시 템플릿에서 쿼리 사용.

JVM 및 OS 레벨 조정은 일반적으로 성능 향상을 가져오지 않으므로 최적화 주기의 마지막에 수행해야 합니다.

콘텐츠 저장소의 구성 방식은 성능에도 영향을 줄 수 있습니다. 최상의 성능을 위해 콘텐츠 저장소의 개별 노드에 연결된 하위 노드 수는 1,000개를 초과할 수 없습니다(규칙으로 ).

일반적인 성능 최적화 활동 중에 가장 친한 친구는 다음과 같습니다.

* `request.log`
* 구성 요소 기반 타이밍
* Java™ 프로파일러입니다.

### Digital Assets 로드 및 편집 시 성능 {#performance-when-loading-and-editing-digital-assets}

디지털 에셋을 로드하고 편집할 때 관련된 데이터 양이 많기 때문에 성능이 문제가 될 수 있습니다.

다음 두 가지 사항이 성능에 영향을 줍니다.

* CPU - 코드 변환 시 여러 코어를 사용하여 더 원활한 작업 수행
* 하드 디스크 - 병렬 RAID 디스크는 동일한 성능을 제공합니다.

성능을 향상시키려면 다음 사항을 고려하십시오.

* 하루에 몇 개의 에셋이 업로드됩니까? 적절한 예상 기준은 다음을 기반으로 할 수 있습니다.

![chlimage_1-77](assets/chlimage_1-77.png)

* 편집이 수행되는 시간대(일반적으로 국제 작업의 경우 작업일 길이)입니다.
* 업로드된 이미지의 평균 크기(및 이미지당 생성된 표현물의 크기)입니다(MB).
* 평균 데이터 속도를 결정합니다.

![chlimage_1-78](assets/chlimage_1-78.png)

* 전체 편집의 80%는 20% 동안 수행되므로 피크 타임에는 평균 데이터 전송률의 4배가 됩니다. 그런 경기력이 당신의 목표입니다.

## 성능 모니터링 {#performance-monitoring}

성능(또는 성능 부족)은 사용자가 가장 먼저 인식하는 것 중 하나이며, 따라서 사용자 인터페이스가 있는 모든 응용 프로그램과 마찬가지로 성능이 중요합니다. AEM 설치의 성능을 최적화하려면 인스턴스의 다양한 속성과 동작을 모니터링합니다.

성능 모니터링 수행 방법에 대한 자세한 내용은 [성능 모니터링](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance)을 참조하십시오.

성능 문제를 일으키는 문제는 효과를 쉽게 볼 수 있는 경우에도 추적하기가 어려운 경우가 많습니다.

기본 시작점은 시스템이 정상적으로 작동할 때 시스템에 대한 좋은 지식입니다. 제대로 수행될 때 환경이 어떻게 &quot;모양&quot;이고 &quot;동작&quot;인지 알지 못하면 성능이 저하될 때 문제를 찾는 것이 어렵습니다. 시스템이 원활하게 실행될 때 시스템을 조사하는 데 시간을 투자하고 성능 정보 수집이 지속적인 작업인지 확인하십시오. 이렇게 하면 성능이 저하되는 경우 비교할 수 있는 기반이 제공됩니다.

다음 다이어그램은 AEM 콘텐츠에 대한 요청이 수행할 수 있는 경로를 보여 주며, 따라서 성능에 영향을 줄 수 있는 다양한 요소의 수를 보여 줍니다.

![chlimage_1-79](assets/chlimage_1-79.png)

성능은 볼륨과 용량 간의 균형이기도 합니다.

* **볼륨** - 시스템에서 처리 및 배달되는 출력의 양입니다.
* **용량** - 볼륨을 전달하는 시스템의 기능입니다.

성능은 웹 체인 전체에서 다양한 위치에 표시될 수 있습니다.

![chlimage_1-80](assets/chlimage_1-80.png)

성능에 영향을 주는 몇 가지 기능 영역이 있습니다.

* 캐싱
* 애플리케이션(프로젝트) 코드
* 검색 기능

### 성능에 관한 기본 규칙 {#basic-rules-regarding-performance}

성능을 최적화할 때는 다음 규칙을 염두에 두어야 합니다.

* 성능 조정 *must*&#x200B;은(는) 모든 프로젝트의 일부입니다.
* 개발 주기 초기에 최적화하지 마십시오.
* 성능은 가장 약한 고리만큼 우수합니다.
* 항상 용량과 볼륨에 대해 생각해 보십시오.
* 먼저 중요한 것을 최적화하십시오.
* *현실적* 목표 없이 최적화하지 마십시오.

>[!NOTE]
>
>성능을 측정하는 데 사용하는 메커니즘은 종종 측정하려는 내용에 정확히 영향을 준다는 점을 기억하십시오. 이러한 불일치를 고려하여 가능한 한 많은 영향을 제거해 보십시오. 특히 브라우저 플러그인은 가능한 한 비활성화해야 합니다.

## 성능을 위한 구성 {#configuring-for-performance}

AEM(및/또는 기본 저장소)의 특정 측면을 성능을 최적화하도록 구성할 수 있습니다. 다음은 가능성 및 제안입니다. 변경하기 전에 해당 기능을 사용하는지 또는 사용하는지 확인해야 합니다.

### 색인 검색 {#search-indexing}

AEM 6.0부터 Adobe Experience Manager은 Oak 기반 저장소 아키텍처를 사용합니다.

업데이트된 색인 지정 정보는 다음 위치에서 찾을 수 있습니다.

* [쿼리 및 색인 생성에 대한 우수 사례](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [쿼리 및 색인화](/help/sites-deploying/queries-and-indexing.md)

### 동시 워크플로우 처리 {#concurrent-workflow-processing}

성능을 향상시키려면 동시에 실행되는 워크플로우 프로세스 수를 제한하십시오. 기본적으로 워크플로 엔진은 Java™ VM에서 사용할 수 있는 프로세서만큼 많은 워크플로를 동시에 처리합니다. 워크플로우 단계에 대량의 처리 리소스(RAM 또는 CPU)가 필요한 경우, 이러한 워크플로우 중 여러 개를 동시에 실행하면 사용 가능한 서버 리소스에 대한 수요가 높을 수 있습니다.

예를 들어 이미지(또는 일반적인 DAM 에셋)가 업로드되면 워크플로우는 이미지를 DAM으로 자동으로 가져옵니다. 이미지는 종종 고해상도이며 처리를 위해 수백 MB의 힙을 쉽게 사용할 수 있습니다. 이러한 이미지를 병렬로 처리하면 메모리 하위 시스템과 가비지 수집기에 높은 부하가 걸리게 됩니다.

워크플로우 엔진은 작업 항목 처리를 처리하고 예약하기 위해 Apache Sling 작업 대기열을 사용합니다. 워크플로 작업을 처리하기 위해 Apache Sling 작업 큐 구성 서비스 팩토리에서 기본적으로 다음 작업 큐 서비스를 만들었습니다.

<!-- TODO: Change the reference to 6.5 LTS javadocs -->
* Granite 워크플로우 큐: DAM 에셋을 처리하는 워크플로우 단계와 같은 대부분의 워크플로우 단계는 Granite 워크플로우 큐 서비스를 사용합니다.
* Granite Workflow 외부 프로세스 작업 큐: 이 서비스는 일반적으로 외부 시스템에 연결하고 결과를 폴링하는 데 사용되는 특수 외부 워크플로우 단계에 사용됩니다. 예를 들어 InDesign 미디어 추출 프로세스 단계는 외부 프로세스로 구현됩니다. 워크플로우 엔진은 외부 대기열을 사용하여 폴링을 처리합니다. ([com.day.cq.workflow.exec.WorkflowExternalProcess](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/workflow/exec/WorkflowExternalProcess.html)을(를) 참조하십시오.)

동시에 실행되는 최대 워크플로우 프로세스 수를 제한하도록 이러한 서비스를 구성합니다.

>[!NOTE]
>
>특정 워크플로 모델의 작업 큐를 만들지 않은 경우 이러한 작업 큐를 구성하면 모든 워크플로에 영향을 줍니다(아래 [특정 워크플로 모델의 큐 구성](/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow) 참조).

#### 저장소에서의 구성 {#configuration-in-the-repo}

sling:OsgiConfig 노드[&#128279;](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)를 사용하여  서비스를 구성하는 경우 기존 서비스의 PID를 찾아야 합니다(예: org.apache.sling.event.jobs.QueueConfiguration.370aad73-d01b-4a0b-abe4-20198d85f705). 웹 콘솔을 사용하여 PID를 검색할 수 있습니다.

이름이 `queue.maxparallel`인 속성을 구성하십시오.

#### 웹 콘솔의 구성 {#configuration-in-the-web-console}

[웹 콘솔을 사용하여](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 이러한 서비스를 구성하려면 Apache Sling 작업 큐 구성 서비스 팩토리 아래에서 기존 구성 항목을 찾습니다.

최대 병렬 작업 이라는 속성을 구성합니다.

### 특정 워크플로우에 대한 큐 구성 {#configure-the-queue-for-a-specific-workflow}

특정 워크플로 모델의 작업 처리를 구성할 수 있도록 해당 워크플로 모델에 대한 작업 큐를 만듭니다. 이러한 방식으로 구성은 특정 워크플로우의 처리에 영향을 주는 반면 기본 Granite 워크플로우 큐 구성은 다른 워크플로우의 처리를 제어합니다.

워크플로 모델이 실행되면 특정 주제에 대한 Sling 작업이 생성됩니다. 기본적으로 이 항목은 일반 Granite Workflow 대기열 또는 Granite Workflow 외부 프로세스 작업 대기열에 대해 구성된 항목과 일치합니다.

* `com/adobe/granite/workflow/job*`
* `com/adobe/granite/workflow/external/job*`

워크플로 모델이 생성하는 실제 작업 항목에는 모델별 접미사가 포함됩니다. 예를 들어 **DAM 자산 업데이트** 워크플로 모델은 다음 주제를 사용하여 작업을 생성합니다.

`com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`

따라서 워크플로우 모델의 작업 주제와 일치하는 주제에 대한 작업 대기열을 만들 수 있습니다. 대기열의 성능 관련 속성을 구성하는 것은 대기열 주제와 일치하는 작업을 생성하는 워크플로 모델에만 영향을 줍니다.

다음 절차는 **DAM 자산 업데이트** 워크플로우를 예로 사용하여 워크플로우에 대한 작업 큐를 만듭니다.

1. 작업 대기열을 생성할 워크플로우 모델을 실행하여 주제 통계를 생성합니다. 예를 들어 이미지를 Assets에 추가하여 **DAM 자산 업데이트** 워크플로우를 실행합니다.
1. Sling 작업 콘솔(`https://<host>:<port>/system/console/slingevent`)을 엽니다.
1. 콘솔에서 워크플로 관련 항목을 살펴봅니다. DAM 자산 업데이트 의 경우 다음 주제를 찾을 수 있습니다.

   * `com/adobe/granite/workflow/external/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam-xmp-writeback/jcr_content/model`

1. 이러한 각 항목에 대해 하나의 작업 큐를 만듭니다. 작업 큐를 만들려면 Apache Sling 작업 큐 팩토리 서비스에 대한 팩토리 구성을 만듭니다.

   팩터리 구성은 [동시 워크플로 처리](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing)에 설명된 Granite 워크플로 큐와 유사합니다. 단, Topics 속성은 워크플로 작업의 주제와 일치합니다.

### AEM DAM 자산 동기화 서비스 {#cq-dam-asset-synchronization-service}

`AssetSynchronizationService`은(는) 탑재된 저장소(LiveLink, Documentum® 등 포함)에서 자산을 동기화하는 데 사용됩니다. 기본적으로 이 동기화는 300초(5분)마다 정기적으로 확인되므로 탑재된 저장소를 사용하지 않는 경우 이 서비스를 비활성화할 수 있습니다.

[OSGi 서비스를 구성](/help/sites-deploying/configuring-osgi.md) **CQ DAM 자산 동기화 서비스**&#x200B;에서 **동기화 기간**(`scheduler.period`)을 1년(초 단위로 정의됨)으로 설정하는 동안 서비스를 사용하지 않도록 설정합니다.

### 여러 DAM 인스턴스 {#multiple-dam-instances}

여러 DAM 인스턴스를 배포하면 다음과 같은 경우 성능에 도움이 됩니다.

* 작성 환경에 대한 많은 에셋을 정기적으로 업로드하여 로드가 높습니다. 여기에서는 별도의 DAM 인스턴스를 작성자 서비스 전용으로 사용할 수 있습니다.
* 전세계 위치(예: 미국, 유럽, 아시아)에 여러 팀이 있습니다.

추가 고려 사항은 다음과 같습니다.

* 작성자의 &quot;진행 중인 작업&quot;과 게시의 &quot;최종&quot; 구분
* 작성자의 내부 사용자와 게시의 외부 방문자/사용자(예: 에이전트, 언론 매체 담당자, 고객 및 학생) 구분.

## 품질 Assurance 우수 사례 {#best-practices-for-quality-assurance}

성능은 게시 환경에 가장 중요합니다. 따라서 프로젝트를 구현하는 동안 게시 환경에 대해 수행하는 성능 테스트를 신중하게 계획하고 분석해야 합니다.

이 단원에서는 *publish* 환경에서 성능 테스트를 위해 테스트 개념을 정의하는 것과 관련된 문제에 대해 표준화된 개요를 제공합니다. 이 정보는 주로 QA 엔지니어, 프로젝트 관리자 및 시스템 관리자에게 유용합니다.

다음은 *Publish* 환경에서 AEM 응용 프로그램에 대한 성능 테스트에 대한 표준화된 접근 방식을 다룹니다. 이 성능 테스트에는 다음 5단계가 포함됩니다.

* [지식 검증](#verification-of-knowledge)
* [범위 정의](#scope-definition)
* [테스트 방법론](#test-methodologies)
* [성능 목표 정의](#defining-the-performance-goals)
* [최적화](#optimization)

제어는 모든 것을 아우르는 추가 프로세스이며, 반드시 필요하지만 테스트에만 국한되지는 않습니다.

### 지식 검증 {#verification-of-knowledge}

첫 번째 단계는 테스트를 시작하기 전에 알아야 하는 기본 정보를 문서화하는 것입니다.

* 테스트 환경의 아키텍처
* 테스트가 필요한 내부 요소를 자세히 설명하는 응용 프로그램 맵(격리 및 결합)

#### 테스트 아키텍처 {#test-architecture}

성능 테스트에 사용되는 테스트 환경의 아키텍처를 문서화합니다.

Dispatcher 및 로드 밸런서와 함께 프로덕션 게시 환경의 복제가 필요합니다.

#### 응용 프로그램 맵 {#application-map}

전체 애플리케이션의 맵을 만들 수 있는 명확한 개요를 얻습니다(작성 환경의 테스트에서 이 맵을 이미 가지고 있을 수 있음).

애플리케이션의 내부 요소를 보여 주는 다이어그램은 테스트 요구 사항에 대한 개요를 제공할 수 있으며 색상 코딩을 사용하여 보고의 기반으로 사용할 수도 있습니다.

### 범위 정의 {#scope-definition}

응용 프로그램에는 일반적으로 다양한 사용 사례가 있습니다. 일부 사용 사례는 중요하지만, 다른 사용 사례는 덜 중요합니다.

게시에서 성능 테스트 범위에 중점을 두려면 Adobe에서 다음을 정의하는 것이 좋습니다.

* 가장 중요한 비즈니스 사용 사례
* 가장 중요한 기술 사용 사례

사용 사례의 수는 사용자가 결정하지만, 쉽게 관리할 수 있는 수(예: 5~10개)로 제한해야 합니다.

주요 사용 사례를 선택하면 각 사례에 대한 주요 성과 지표(KPI) 및 이를 측정하는 데 사용되는 도구를 정의할 수 있습니다. 일반적인 KPI의 예는 다음과 같습니다.

* 엔드 투 엔드 응답 시간
* 서블릿 응답 시간
* 단일 구성 요소에 대한 응답 시간
* 서비스에 대한 응답 시간
* 스레드 풀의 유휴 스레드 수
* 무료 연결 수
* CPU 및 I/O 액세스와 같은 시스템 리소스

### 테스트 방법론 {#test-methodologies}

이 개념에는 성능 목표를 정의하고 테스트하는 데 사용되는 네 가지 시나리오가 있습니다.

* 단일 구성 요소 테스트
* 결합된 구성 요소 테스트
* *실행 중* 시나리오
* 오류 시나리오

다음 원칙을 기반으로 합니다.

#### 구성 요소 중단점 {#component-breakpoints}

* 각 구성 요소에는 성능과 관련된 특정 중단점이 있습니다. 즉, 구성 요소는 특정 시점에 도달할 때까지 성능이 우수함을 보여줄 수 있으며, 이후 성능이 빠르게 저하됩니다.
* 애플리케이션의 전체 개요를 보려면 먼저 구성 요소를 확인하여 각각의 중단점에 도달하는 시기를 파악해야 합니다.
* 일정 기간 동안 사용자 수를 늘려 증가하는 로드를 생성하는 로드 테스트를 수행할 수 있는 중단점을 찾으려면 이 로드와 구성 요소의 응답을 모니터링하면 구성 요소의 중단점에 도달할 때 특정 성능 동작이 발생합니다. 포인트는 동시 사용자 수(구성 요소가 이 KPI에 민감한 경우)와 함께 초당 동시 트랜잭션 수로 한정할 수 있습니다.
* 그런 다음 이 정보는 개선 사항의 벤치마크 역할을 하고, 사용 중인 측정값의 효율성을 나타내며, 테스트 시나리오를 정의하는 데 도움이 될 수 있습니다.

#### 트랜잭션 {#transactions}

* 트랜잭션이라는 용어는 페이지 자체 및 모든 후속 호출을 포함하여 전체 웹 페이지의 요청을 나타내는 데 사용됩니다. 즉, 페이지 요청, 모든 AJAX 호출, 이미지 및 기타 개체 **드릴다운 요청**&#x200B;입니다.
* 각 요청을 완전히 분석하기 위해 호출 스택의 각 요소를 표시한 다음, 각 요소에 대한 평균 처리 시간을 합산할 수 있습니다.

### 성능 목표 정의 {#defining-the-performance-goals}

범위 및 관련 KPI가 정의된 후 구체적인 성과 목표를 설정합니다. 이 프로세스에는 타겟 값과 함께 테스트 시나리오를 구상하는 작업이 포함됩니다.

평균 및 피크 조건에서 성능을 테스트합니다. 또한 웹 사이트를 처음 사용할 수 있을 때 웹 사이트에 대한 관심 증가를 지원할 수 있도록 하려면 Going Live 시나리오 테스트가 필요합니다.

기존 웹 사이트에서 수집했을 수 있는 모든 경험 또는 통계는 향후 목표를 결정하는 데에도 유용할 수 있습니다. 예를 들어 라이브 웹 사이트의 상위 트래픽입니다.

#### 단일 구성 요소 테스트 {#single-component-tests}

평균 및 최대 조건 모두에서 주요 구성 요소를 테스트해야 합니다.

두 경우 모두 사전 정의된 수의 사용자가 시스템을 사용할 때 초당 예상 트랜잭션 수를 정의할 수 있습니다.

| 구성 요소 | 테스트 유형 | 아니요. / 사용자 | Tx/sec(예상) | Tx/sec(테스트됨) | 설명 |
|---|---|---|---|---|---|
| 홈페이지 단일 사용자 | 평균 | 1 | 1 |  |  |
|   | 피크 | 1 | 3 |  |  |
| 홈페이지 사용자 100명 | 평균 | 100 | 3 |  |  |
|   | 피크 | 100 | 3 |  |

#### 결합된 구성 요소 테스트 {#combined-component-tests}

구성 요소를 함께 테스트하면 애플리케이션 동작을 보다 세밀하게 반영할 수 있습니다. 다시 평균 및 피크 조건을 테스트해야 합니다.

| 시나리오 | 구성 요소 | 아니요. / 사용자 | Tx/sec(예상) | Tx/sec(테스트됨) | 설명 |
|---|---|---|---|---|---|
| 혼합 평균 | 홈 페이지 | 10 | 1 |  |  |
|   | 검색 | 10 | 1 |  |  |
|   | 뉴스 | 10 | 2 |  |  |
|   | 이벤트 | 10 | 1 |  |  |
|   | 활성화 | 10 | 3 |  | 작성자 동작 시뮬레이션. |
| 혼합 피크 | 홈 페이지 | 100 | 5 |  |  |
|   | 검색 | 50 | 5 |  |  |
|   | 뉴스 | 100 | 10 |  |  |
|   | 이벤트 | 100 | 10 |  |  |
|   | 활성화 | 20 | 20 |  | 작성자 동작 시뮬레이션. |

#### 라이브 테스트 진행 중 {#going-live-tests}

웹 사이트를 사용 가능하게 한 후 처음 며칠 동안은 관심 수준이 높아질 것으로 예상됩니다. 이 시나리오는 테스트 중인 피크 값보다 훨씬 큽니다. Adobe에서는 실행 중 시나리오를 테스트하여 시스템이 이 상황을 지원할 수 있도록 하는 것이 좋습니다.

| 시나리오 | 테스트 유형 | 아니요. / 사용자 | Tx/sec(예상) | Tx/sec(테스트됨) | 설명 |
|---|---|---|---|---|---|
| 라이브 피크 | 홈 페이지 | 200 | 20 |  |  |
|   | 검색 | 100 | 10 |  |  |
|   | 뉴스 | 200 | 20 |  |  |
|   | 이벤트 | 200 | 20 |  |  |
|   | 활성화 | 20 | 20 |  | 작성자 동작 시뮬레이션. |

#### 오류 시나리오 테스트 {#error-scenario-tests}

오류 시나리오를 테스트하여 시스템이 올바르고 적절하게 반응하는지 확인합니다. 오류 자체가 처리되는 방법뿐만 아니라 성능에 영향을 줄 수 있습니다. 예:

* 사용자가 검색 상자에 잘못된 검색어를 입력하려고 하면 어떻게 됩니까?
* 검색어가 너무 일반적이어서 검색 결과가 과도하게 많으면 어떻게 됩니까?

이러한 검사를 고안할 때 모든 시나리오가 규칙적으로 발생하는 것은 아니라는 것을 기억해야 한다. 그러나, 그들이 전체 시스템에 미치는 영향은 중요합니다.

| 오류 시나리오 | 오류 유형 | 아니요. / 사용자 | Tx/sec(예상) | Tx/sec(테스트됨) | 설명 |
|---|---|---|---|---|---|
| 검색 구성 요소 오버로드 | 전역 와일드카드 검색(별표) | 10 | 1 |  | &ast;&ast;&ast;&ast;만 검색됩니다. |
|   | 정지어 | 20 | 2 |  | 정지어를 찾고 있습니다. |
|   | 빈 문자열 | 10 | 1 |  | 빈 문자열을 검색하는 중입니다. |
|   | 특수 문자 | 10 | 1 |  | 특수 문자를 검색하는 중입니다. |

#### 내구 시험 {#endurance-tests}

특정 문제는 시스템이 몇 시간 또는 며칠 동안 계속 실행된 후에만 발생합니다. 필요한 시간 기간 동안 일정한 평균 하중을 시험하기 위해 내구 시험을 사용한다. 그런 다음 성능 저하를 분석할 수 있습니다.

| 시나리오 | 테스트 유형 | 아니요. / 사용자 | Tx/sec(예상) | Tx/sec(테스트됨) | 설명 |
|---|---|---|---|---|---|
| 내구 시험(72시간) | 홈 페이지 | 10 | 1 |  |  |
|   | 검색 | 10 | 1 |  |  |
|   | 뉴스 | 20 | 2 |  |  |
|   | 이벤트 | 10 | 1 |  |  |
|   | 활성화 | 1 | 3 |  | 작성자 동작 시뮬레이션. |

### 최적화 {#optimization}

이후 구현 단계에서는 애플리케이션을 최적화하여 성능 목표를 달성하고 극대화합니다.

최적화를 테스트하여 다음을 확인해야 합니다.

* 기능에는 영향을 주지 않음
* 릴리스하기 전에 로드 테스트를 통해 확인됨

다양한 도구를 사용하여 로드 생성, 성능 모니터링 및 결과 분석을 수행할 수 있습니다. 이러한 도구 중 일부는 다음과 같습니다.

* [JMeter](https://jmeter.apache.org/)
* [OpenText Professional 성능 엔지니어링](https://www.opentext.com/products/professional-performance-engineering).
* [Java™ 대화형 프로필](https://jiprof.sourceforge.net/)

최적화 후 다시 테스트하여 영향을 확인합니다.

### 보고 {#reporting}

지속적인 보고를 통해 모든 사용자가 상태를 알 수 있습니다. 이전에 색상 코딩에서 언급했듯이 이 상태에 아키텍처 맵을 사용할 수 있습니다.

모든 테스트가 완료되면 다음에 대해 보고합니다.

* 발생한 모든 중대 오류
* 아직 조사가 더 필요한 중요하지 않은 문제
* 테스트 도중 가정된 사항
* 테스트에서 발생할 모든 권장 사항

## Dispatcher 사용 시 성능 최적화 {#optimizing-performance-when-using-the-dispatcher}

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ko)은(는) Adobe의 캐싱 및/또는 부하 분산 도구입니다. Dispatcher을 사용할 때는 캐시 성능을 위해 웹 사이트를 최적화하는 것이 좋습니다.

>[!NOTE]
>
>Dispatcher 버전은 AEM과 독립적이지만 Dispatcher 설명서는 AEM 설명서에 임베드되어 있습니다. 항상 최신 버전의 AEM 설명서에 임베드된 Dispatcher 설명서를 사용하십시오.
>
>이전 버전의 AEM에 대한 설명서에 임베드된 Dispatcher 설명서에 대한 링크를 따라간 경우 이 페이지로 리디렉션되었을 수 있습니다.

Dispatcher에서는 웹 사이트에서 이러한 메커니즘을 활용하는 경우 성능을 최적화하는 데 사용할 수 있는 몇 가지 내장 메커니즘을 제공합니다. 이 섹션에서는 캐싱의 이점을 극대화하기 위해 웹 사이트를 디자인하는 방법을 설명합니다.

>[!NOTE]
>
>Dispatcher가 표준 웹 서버에 캐시를 저장한다는 것을 기억하는 데 도움이 될 수 있습니다. 이 정보를 알고 있으면 페이지로 저장할 수 있는 모든 것을 캐시할 수 있고 URL을 사용하여 요청할 수 있습니다. 또한 쿠키, 세션 데이터 및 양식 데이터와 같은 다른 항목은 저장할 수 없습니다.
>
>일반적으로, 많은 캐싱 전략은 좋은 URL을 선택하고 이 추가 데이터에 의존하지 않는 것을 포함합니다.
>
>Dispatcher 버전 4.1.11을 사용하면 응답 헤더를 캐시할 수도 있습니다. [HTTP 응답 헤더 캐싱](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ko#configuring-the-dispatcher-cache-cache)을 참조하십시오.
>

### Dispatcher 캐시 비율 계산 {#calculating-the-dispatcher-cache-ratio}

캐시 비율 공식은 시스템으로 들어오는 총 요청 수 중 캐시에서 처리한 요청의 백분율을 예상합니다. 캐시 비율을 계산하려면 다음이 필요합니다.

* 총 요청 수입니다. 이 정보는 Apache `access.log`에서 사용할 수 있습니다. 자세한 내용은 [공식 Apache 설명서](https://httpd.apache.org/docs/2.4/logs.html#accesslog)를 참조하십시오.

* 게시 인스턴스가 제공한 요청 수입니다. 이 정보는 인스턴스의 `request.log`에서 사용할 수 있습니다. 자세한 내용은 [request.log 해석](/help/sites-deploying/monitoring-and-maintaining.md#interpreting-the-request-log) 및 [로그 파일 찾기](/help/sites-deploying/monitoring-and-maintaining.md#finding-the-log-files)를 참조하십시오.

캐시 비율을 계산하는 공식은 다음과 같습니다.

* (총 요청 수 **마이너스** 게시 시 요청 수) **나누기** 총 요청 수로.

예를 들어 총 요청 수가 129491 게시 인스턴스에서 제공하는 요청 수가 58959 캐시 비율은 **(129491 - 58959)/129491= 54.5%**&#x200B;입니다.

일대일 게시자/Dispatcher 연결이 없는 경우 정확한 측정을 위해 모든 Dispatcher와 게시자의 요청을 함께 추가합니다. [권장 배포](/help/sites-deploying/recommended-deploys.md)도 참조하세요.

>[!NOTE]
>
>최상의 성능을 위해 Adobe에서는 캐시 비율을 90% 대 95%로 권장합니다.

#### 일관된 페이지 인코딩 사용 {#using-consistent-page-encoding}

Dispatcher 버전 4.1.11에서는 응답 헤더를 캐시할 수 있습니다. Dispatcher에서 응답 헤더를 캐시하지 않는 경우 헤더에 페이지 인코딩 정보를 저장하면 문제가 발생할 수 있습니다. 이 상황에서 Dispatcher가 캐시에서 페이지를 제공하면 웹 서버의 기본 인코딩이 페이지에 사용됩니다. 이 문제를 방지하는 두 가지 방법이 있습니다.

* 인코딩을 하나만 사용하는 경우 웹 서버에서 사용되는 인코딩이 AEM 웹 사이트의 기본 인코딩과 동일한지 확인합니다.
* 다음 예제와 같이, 인코딩을 설정하려면 HTML `head` 섹션에서 `<META>` 태그를 사용합니다.

```xml
        <META http-equiv="Content-Type" content="text/html; charset=EUC-JP">
```

#### URL 매개변수 방지 {#avoid-url-parameters}

가능하면 캐시하려는 페이지의 URL 매개변수를 사용하지 마십시오. 예를 들어 사진 갤러리가 있는 경우 다음 URL은 캐시되지 않습니다(Dispatcher가 [적절하게 구성](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ko#configuring-the-dispatcher-cache-cache)되지 않은 경우).

```xml
www.myCompany.com/pictures/gallery.html?event=christmas&amp;page=1
```

단, 다음과 같이 이러한 매개변수를 페이지 URL에 넣을 수 있습니다.

```xml
www.myCompany.com/pictures/gallery.christmas.1.html
```

>[!NOTE]
>
>이 URL은 `gallery.html`과(와) 동일한 페이지 및 동일한 템플릿을 호출합니다. 템플릿 정의에서 페이지를 렌더링하는 스크립트를 지정하거나 모든 페이지에 대해 동일한 스크립트를 사용할 수 있습니다.

#### URL로 사용자 정의 {#customize-by-url}

사용자가 글꼴 크기(또는 기타 레이아웃 사용자 정의)를 변경할 수 있도록 허용하는 경우 다른 사용자 정의가 URL에 반영되었는지 확인합니다.

예를 들어 쿠키는 캐시되지 않으므로 글꼴 크기를 쿠키(또는 유사한 메커니즘)에 저장하면 캐시된 페이지에 대해 글꼴 크기가 유지되지 않습니다. 따라서 Dispatcher는 임의의 글꼴 크기 문서를 무작위로 반환합니다.

URL에 글꼴 크기를 선택기로 포함하면 이 문제를 피할 수 있습니다.

```xml
www.myCompany.com/news/main.large.html
```

>[!NOTE]
>
>대부분의 레이아웃 측면에서 스타일 시트 또는 클라이언트측 스크립트, 혹은 둘 다를 사용하는 것도 가능합니다. 이 악기들은 캐싱과 잘 맞는다.
>
>이 전략은 다음과 같은 URL을 사용할 수 있는 인쇄 버전에도 유용합니다.
>
>`www.myCompany.com/news/main.print.html`
>
>템플릿 정의의 스크립트 글로빙을 사용하여 인쇄 페이지를 렌더링하는 별도의 스크립트를 지정할 수 있습니다.

#### 제목으로 사용된 이미지 파일 무효화 {#invalidating-image-files-used-as-titles}

페이지 제목 또는 기타 텍스트를 사진으로 렌더링하는 경우 페이지의 콘텐츠 업데이트 시 삭제되도록 파일을 저장하는 것이 좋습니다.

1. 이미지 파일을 페이지와 동일한 폴더에 넣습니다.
1. 이미지 파일에 다음 이름 지정 형식을 사용합니다.

   `<page file name>.<image file name>`

예를 들어 `myPage.html` 페이지의 제목을 `file myPage.title.gif`에 저장할 수 있습니다. 이 파일은 페이지가 업데이트되면 자동으로 삭제되므로 페이지 제목이 변경되면 캐시에 자동으로 반영됩니다.

>[!NOTE]
>
>이미지 파일이 AEM 인스턴스에 실제로 존재할 필요는 없습니다. 이미지 파일을 동적으로 생성하는 스크립트를 사용할 수 있습니다. 그러면 Dispatcher가 웹 서버에 파일을 저장합니다.

#### 탐색에 사용된 이미지 파일 무효화 {#invalidating-image-files-used-for-navigation}

탐색 항목에 사진을 사용하는 경우 메서드는 기본적으로 제목과 동일하지만 약간 더 복잡합니다. 대상 페이지와 함께 모든 탐색 이미지를 저장합니다. 일반 및 활성에 대해 두 개의 사진을 사용하는 경우 다음 스크립트를 사용할 수 있습니다.

* 페이지를 정상적으로 표시하는 스크립트.
* “.normal” 요청을 처리하고 일반 사진을 반환하는 스크립트.
* “.active” 요청을 처리하고 활성화된 사진을 반환하는 스크립트.

컨텐츠 업데이트에서 이러한 사진 및 페이지를 삭제하도록 하려면 페이지와 동일한 이름 지정 핸들을 사용하여 이러한 사진을 만드는 것이 중요합니다.

수정되지 않은 페이지의 경우 페이지 자체가 자동 무효화되더라도 사진은 캐시에 남아 있습니다.

#### 개인화 {#personalization}

필요한 경우 개인화를 제한하는 것이 좋습니다. 이유는 다음과 같습니다.

* 자유롭게 사용자 정의할 수 있는 시작 페이지를 사용하는 경우 사용자가 요청할 때마다 해당 페이지를 구성해야 합니다.
* 반대로 10개의 서로 다른 시작 페이지를 선택할 수 있는 경우 각 시작 페이지를 캐시할 수 있으므로 성능이 향상됩니다.

>[!TIP]
>Dispatcher 캐시 구성에 대한 자세한 내용은 [AEM Dispatcher 캐시 자습서](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/overview.html?lang=ko) 및 [보호된 콘텐츠 캐싱](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/chapter-1.html?lang=ko#dispatcher-tips-and-tricks)의 해당 섹션을 참조하십시오.

사용자 이름을 제목 표시줄에 입력하여 각 페이지를 개인화하는 경우(예: ) 성능에 영향을 줍니다.

>[!TIP]
>보안 콘텐츠를 캐시하려면 Dispatcher 안내서의 [보안 콘텐츠 캐싱](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=ko)을 참조하십시오.

한 페이지에서 제한된 컨텐츠와 공개 컨텐츠를 혼합하는 경우 Dispatcher의 서버측 포함 또는 브라우저의 Ajax를 통해 클라이언트측 포함 을 사용하는 전략을 고려해 보십시오.

>[!TIP]
>
>혼합 공개 콘텐츠와 제한된 콘텐츠를 처리하려면 [Sling Dynamic Include 설정](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-sling-dynamic-include.html?lang=ko)을 참조하십시오.

#### 고정 연결 {#sticky-connections}

[고정 연결](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ko#the-benefits-of-load-balancing)은 한 명의 사용자에 대한 문서가 모두 동일한 서버에서 구성되도록 합니다. 사용자가 이 폴더를 떠났다가 나중에 다시 돌아와도 연결은 계속 유지됩니다. 웹 사이트에 고정 연결이 필요한 모든 문서를 보관하려면 폴더 하나를 정의합니다. 다른 문서는 여기에 넣지 마십시오. 이 시나리오는 개인화된 페이지 및 세션 데이터를 사용하는 경우 로드 밸런싱에 영향을 줍니다.

#### MIME 유형 {#mime-types}

브라우저가 파일 유형을 결정할 수 있는 두 가지 방법이 있습니다.

1. 확장명(예: `.html`, `.gif` 및 `.jpg`) 기준.
1. 서버가 파일과 함께 보내는 MIME 형식별

대부분의 파일에서 MIME 유형은 파일 확장자에 암시되어 있습니다. 즉,

1. 확장명(예: `.html`, `.gif` 및 `.jpg`) 기준.
1. 서버가 파일과 함께 보내는 MIME 형식별

파일 이름에 확장자가 없으면 일반 텍스트로 표시됩니다.

Dispatcher 버전 4.1.11에서는 응답 헤더를 캐시할 수 있습니다. Dispatcher에서 응답 헤더를 캐시하지 않는 경우 MIME 유형은 HTTP 헤더의 일부입니다. 따라서 AEM 애플리케이션이 파일 끝이 인식되지 않은 파일을 반환하고 대신 MIME 유형에 의존하는 경우 이러한 파일이 잘못 표시될 수 있습니다.

파일이 제대로 캐시되었는지 확인하려면 다음 지침을 따르십시오.

* 파일의 확장자가 항상 적절한지 확인하십시오.
* `download.jsp?file=2214`과(와) 같은 URL이 있는 일반 파일 서비스 스크립트를 사용하지 마십시오. 파일 사양이 포함된 URL을 사용하려면 스크립트를 다시 작성하십시오. 이전 예제의 경우 이 다시 쓰기는 `download.2214.pdf`입니다.
