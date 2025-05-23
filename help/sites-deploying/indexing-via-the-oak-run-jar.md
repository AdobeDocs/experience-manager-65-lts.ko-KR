---
title: Oak 실행 Jar를 통한 인덱싱
description: Oak 실행 Jar를 통해 색인화를 수행하는 방법을 알아봅니다.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
exl-id: a6344463-7796-4ee3-8b2e-b3bfd2aec99a
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Oak 실행 Jar를 통한 인덱싱 {#indexing-via-the-oak-run-jar}

Oak-run은 JMX 수준에서 작업할 필요 없이 명령줄에서 모든 인덱싱 사용 사례를 지원합니다. oak-run 접근 방식의 장점은 다음과 같습니다.

1. AEM 6.4 이후 새로운 인덱싱 도구 세트입니다.
1. 다시 색인화하는 데 걸리는 시간을 단축하여 더 큰 저장소의 색인 재지정에 유리하게 영향을 미칩니다
1. AEM에서 리인덱싱하는 동안 리소스 소비를 줄여 다른 AEM 활동에 대한 시스템 성능을 개선합니다
1. Oak-run은 대역 외 지원을 제공합니다. 프로덕션 조건에서 프로덕션 인스턴스에서 다시 색인을 실행할 수 없는 경우 중요한 성능에 영향을 주지 않도록 색인을 다시 지정하는 데 복제된 환경을 사용할 수 있습니다.

다음은 `oak-run` 도구를 통해 인덱싱 작업을 수행할 때 사용할 수 있는 사용 사례 목록입니다.

## 색인 일관성 검사 {#indexconsistencychecks}

>[!NOTE]
>
>이 시나리오에 대한 자세한 내용은 [사용 사례 1 - 인덱스 일관성 검사](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck)를 참조하십시오.

* `oak-run.jar`Lucene Oak 색인이 손상되었는지 빠르게 확인합니다.
* 일관성 검사 수준 1과 2를 위해 사용 중인 AEM 인스턴스에서 실행되는 것이 안전합니다.

![인덱스 일관성 검사](assets/screen_shot_2017-12-14at135758.png)

## 색인 통계 {#indexstatistics}

>[!NOTE]
>
>이 시나리오에 대한 자세한 내용은 [사용 사례 2 - 색인 통계](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)를 참조하세요.

* `oak-run.jar`이(가) 오프라인 분석을 위해 모든 인덱스 정의, 중요한 인덱스 통계 및 인덱스 컨텐츠를 덤프합니다.
* 사용 중인 AEM 인스턴스에서 안전하게 실행됩니다.

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## 접근 방식 결정 트리 리인덱싱 {#reindexingapproachdecisiontree}

이 다이어그램은 다양한 리인덱싱 접근 방식을 사용할 시기에 대한 의사 결정 트리입니다.

![oak_-_reindexingwithoak-run](assets/oak_-_reindexingwithoak-run.png)

## MongoMK / RDMBMK 리인덱싱 {#reindexingmongomk}

>[!NOTE]
>
>이 시나리오에 대한 자세한 내용은 [사용 사례 3 - 리인덱싱](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing)을 참조하십시오.

### SegmentNodeStore 및 DocumentNodeStore에 대한 텍스트 사전 추출 {#textpre-extraction}

[텍스트 사전 추출](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction)(AEM 6.3 이후 존재하는 기능)을 사용하여 다시 색인화하는 시간을 줄일 수 있습니다. 텍스트 사전 추출은 모든 리인덱싱 접근 방식과 함께 사용할 수 있습니다.

`oak-run.jar` 색인화 방법에 따라 아래 다이어그램의 색인 재지정 수행 단계 양쪽에 여러 단계가 있습니다.

![SegmentNodeStore 및 DocumentNodeStore에 대한 텍스트 사전 추출](assets/4.png)

>[!NOTE]
>
>주황색은 AEM이 유지 관리 창에 있어야 하는 활동을 나타냅니다.

### oak-run.jar를 사용하여 MongoMK 또는 RDBMK에 대한 온라인 리인덱싱 {#onlinere-indexingformongomk}

>[!NOTE]
>
>이 시나리오에 대한 자세한 내용은 [다시 인덱싱 - DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore)를 참조하십시오.

MongoMK(및 RDBMK) AEM 설치를 리인덱싱하는 권장 방법입니다. 다른 방법은 사용할 수 없습니다.

클러스터의 단일 AEM 인스턴스에 대해서만 이 프로세스를 실행합니다.

![oak-run.jar를 사용하여 MongoMK 또는 RDBMK에 대한 온라인 다시 인덱싱](assets/5.png)

## TarMK 리인덱싱 {#re-indexingtarmk}

>[!NOTE]
>
>이 시나리오에 대한 자세한 내용은 [다시 인덱싱 - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore)을 참조하십시오.

* **콜드 대기 고려 사항(TarMK)**

   * 콜드 대기에 대한 특별한 고려 사항은 없으며 콜드 대기 인스턴스 동기화는 평소대로 변경됩니다.

* **AEM 게시 팜(AE 게시 팜은 항상 TarMK여야 함)**

   * 게시 팜의 경우 모든 OR에 대해 수행해야 합니다. 단일 게시에서 단계를 실행해야 합니다. 그런 다음 다른 사용자에 대한 설정을 복제합니다(AEM 인스턴스를 복제할 때 일반적인 모든 절차를 따릅니다. sling.id - 여기에서 링크해야 함).

### TarMK에 대한 온라인 리인덱싱 {#onlinere-indexingfortarmk}

>[!NOTE]
>
>이 시나리오에 대한 자세한 내용은 [온라인 다시 인덱스 - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore)을(를) 참조하십시오.

oak-run.jar의 새 인덱싱 기능을 도입하기 전에 사용한 메서드입니다. 이 작업은 Oak 인덱스에서 `reindex=true` 속성을 설정하여 수행됩니다.

지표에 대한 시간 및 성과 효과를 고객이 수용할 수 있는 경우 이 접근법을 사용할 수 있습니다. 중소 규모의 AEM 설치의 경우 이러한 경우가 많습니다.

![TarMK에 대한 온라인 다시 인덱싱](assets/6.png)

### oak-run.jar를 사용하여 TarMK를 온라인 리인덱싱하는 방법 {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>이 시나리오에 대한 자세한 내용은 [온라인 색인 재지정 - SegmentNodeStore - AEM 인스턴스가 실행 중](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning)을 참조하십시오.

oak-run.jar를 사용한 TarMK의 온라인 리인덱싱은 위에서 설명한 [TarMK에 대한 온라인 리인덱싱](#onlinere-indexingfortarmk)보다 빠릅니다. 그러나 유지 관리 기간 동안 실행해야 합니다. 기간이 더 짧고 리인덱싱을 수행하기 위해 더 많은 단계가 필요합니다.

>[!NOTE]
>
>주황색은 유지 관리 기간 동안 AEM을 수행해야 하는 작업을 나타냅니다.

![oak-run.jar를 사용하여 TarMK를 온라인 다시 인덱싱합니다](assets/7.png)

### oak-run.jar를 사용하여 TarMK를 오프라인으로 다시 색인화 {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>이 시나리오에 대한 자세한 내용은 [온라인 색인 재지정 - SegmentNodeStore - AEM 인스턴스가 종료됨](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown)을 참조하십시오.

TarMK의 오프라인 리인덱싱은 단일 `oak-run.jar` 주석이 필요하므로 TarMK에 대한 가장 간단한 `oak-run.jar` 기반 리인덱싱 접근 방식입니다. 하지만 AEM 인스턴스를 종료해야 합니다.

>[!NOTE]
>
>빨간색은 AEM을 종료해야 하는 작업을 나타냅니다.

![oak-run.jar를 사용하여 TarMK를 오프라인 다시 색인화](assets/8.png)

### oak-run.jar를 사용하여 대역 외 TarMK 리인덱싱  {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>이 시나리오에 대한 자세한 내용은 [대역 외 리인덱스 - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore)를 참조하십시오.

대역 외 리인덱싱은 리인덱싱이 사용 중인 AEM 인스턴스에 미치는 영향을 최소화합니다.

>[!NOTE]
>
>빨간색은 AEM이 종료될 수 있는 작업을 나타냅니다.

![oak-run.jar를 사용하여 대역 외 TarMK 리인덱싱](assets/9.png)

## 색인 정의 업데이트 중 {#updatingindexingdefinitions}

>[!NOTE]
>
>이 시나리오에 대한 자세한 내용은 [사용 사례 4 - 인덱스 정의 업데이트](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions)를 참조하십시오.

### ACS Ensure Index를 사용하여 TarMK에서 색인 정의 생성 및 업데이트 {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Ensure Index 는 커뮤니티 지원 프로젝트이며 Adobe 지원에서 지원되지 않습니다.

이렇게 하면 콘텐츠 패키지를 통해 색인 정의를 전달할 수 있으며 나중에 색인 재지정 플래그를 `true`(으)로 설정하여 색인 재지정을 수행합니다. 이는 리인덱싱하는 데 시간이 오래 걸리지 않는 소규모 설정에 대해 작동합니다.

자세한 내용은 [ACS 인덱스 확인 설명서](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)를 참조하십시오.

### oak-run.jar를 사용하여 TarMK에 대한 인덱스 정의 생성 및 갱신 {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

`oak-run.jar`이 아닌 메서드를 사용하여 다시 인덱싱하는 데 시간 또는 성능에 미치는 영향이 너무 큰 경우 다음 `oak-run.jar` 기반 접근 방식을 사용하여 TarMK 기반 AEM 설치에서 Lucene 인덱스 정의를 가져오고 다시 인덱싱할 수 있습니다.

![oak-run.jar를 사용하여 TarMK에서 인덱스 정의 만들기 및 업데이트](assets/10.png)

### oak-run.jar를 사용하여 MonogMK에 대한 인덱스 정의 생성 및 갱신 {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

`oak-run.jar`이 아닌 메서드를 사용하여 다시 인덱싱하는 데 시간 또는 성능에 미치는 영향이 너무 크면 다음 `oak-run.jar` 기반 접근 방식을 사용하여 MongoMK 기반 AEM 설치에서 Lucene 인덱스 정의를 가져오고 다시 인덱싱할 수 있습니다.

![oak-run.jar를 사용하여 MonogMK에 대한 인덱스 정의 만들기 및 업데이트](assets/11.png)
