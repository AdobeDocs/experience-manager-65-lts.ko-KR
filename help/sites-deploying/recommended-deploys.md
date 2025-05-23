---
title: 권장 배포
description: 이 문서에서는 AEM에 대해 권장되는 토폴로지에 대해 설명합니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 9baa4111-831a-4b68-9ce5-82aeeb06e07f
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 0%

---

# 권장 배포{#recommended-deployments}

>[!NOTE]
>
>이 페이지는 AEM에 대해 권장되는 토폴로지를 참조합니다. 클러스터링 기능 및 구성 방법에 대한 자세한 내용은 [Apache Sling Discovery API 설명서](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html)를 참조하십시오.

MicroKernel은 AEM 6.2부터 지속성 관리자 역할을 합니다. 필요에 맞게 인스턴스를 선택하는 방법은 인스턴스의 목적과 고려 중인 배포 유형에 따라 다릅니다.

아래 예제는 가장 일반적인 AEM 설정에서 권장되는 사용이 무엇인지 보여 줍니다.

## 배포 시나리오 {#deployment-scenarios}

### 단일 TarMK 인스턴스 {#single-tarmk-instance}

이 시나리오에서는 단일 TarMK 인스턴스가 단일 서버에서 실행됩니다.

**작성자 인스턴스의 기본 배포입니다.**

![chlimage_1-15](assets/chlimage_1-15.png)

장점:

* 단순
* 손쉬운 유지 관리
* 우수한 성능

단점은 다음과 같습니다.

* 서버 용량의 한계를 넘어서는 확장성 없음
* 페일오버 용량 없음

### TarMK 콜드 대기 {#tarmk-cold-standby}

하나의 TarMK 인스턴스가 기본 인스턴스로 작동합니다. 기본 저장소의 저장소는 대기 페일오버 시스템으로 복제됩니다.

전체 저장소가 장애 조치(failover) 서버에 지속적으로 복제되므로 콜드 대기 메커니즘을 백업으로도 사용할 수 있습니다. 장애 조치(failover) 서버가 콜드 대기 모드에서 실행되고 있습니다. 즉, 인스턴스의 HttpReceiver만 실행되고 있습니다.

![chlimage_1-16](assets/chlimage_1-16.png)

장점:

* 단순성
* 유지 가능성
* 성능
* 페일오버

단점은 다음과 같습니다.

* 서버 용량의 한계를 넘어서는 확장 불가
* 한 대의 서버가 대부분의 경우 유휴 상태
* 장애 조치(failover)는 자동으로 수행되지 않습니다. 장애 조치(failover) 시스템에서 요청 서비스를 시작하기 전에 외부에서 검색해야 합니다.

>[!NOTE]
>
>TarMK 콜드 대기를 사용하여 AEM을 구성하는 방법에 대한 자세한 내용은 [이](/help/sites-deploying/tarmk-cold-standby.md) 문서를 참조하십시오.

>[!NOTE]
>
>이 TarMK 예제의 콜드 대기 배포는 페일오버 서버에 대한 지속적인 복제가 있으므로 기본 인스턴스와 대기 인스턴스 모두 개별적으로 라이센스를 받아야 합니다. 라이선스에 대한 자세한 내용은 [Adobe 일반 라이선스 사용 약관](https://www.adobe.com/kr/legal/terms/enterprise-licensing.html)을 참조하세요.

### Tarmk 팜 {#tarmk-farm}

여러 Oak 인스턴스는 각각 하나의 TarMK 인스턴스로 실행됩니다. TarMK 저장소는 독립적이며 동기화를 유지해야 합니다.

저장소 동기화 상태를 유지하면 작성자 서버가 각 팜 멤버에 동일한 콘텐츠를 게시하고 있다는 사실이 제공됩니다. 자세한 내용은 [복제](/help/sites-deploying/replication.md)를 참조하십시오.

**게시 환경에 대한 기본 배포입니다.**

![chlimage_1-17](assets/chlimage_1-17.png)

장점:

* 성능
* 읽기 액세스를 위한 확장성
* 페일오버

### 단일 데이터 센터에서 고가용성을 위한 MongoMK 장애 조치 기능이 있는 Oak 클러스터 {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

>[!NOTE]
>
>Mongo의 최소 지원 버전은 Mongo 6입니다.

이 접근 방식은 여러 Oak 인스턴스가 단일 데이터 센터 내의 MongoDB 복제본 세트에 액세스하고 결과적으로 AEM 작성 환경에 대한 활성-활성 클러스터를 생성함을 의미합니다. MongoDB의 복제본 세트는 하드웨어나 네트워크 장애 시 고가용성과 이중화를 제공하는 데 사용됩니다.

![chlimage_1-18](assets/chlimage_1-18.png)

장점:

* 새로운 AEM 작성자 인스턴스를 사용하여 수평 확장 기능
* 데이터 계층의 고가용성, 이중화 및 자동 페일오버

단점은 다음과 같습니다.

* 일부 시나리오의 경우 성능이 TarMK보다 낮을 수 있습니다.

### 여러 데이터 센터에서 MongoMK 장애 조치를 사용하는 Oak 클러스터 {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

이 접근 방식은 여러 Oak 인스턴스가 여러 데이터 센터에 걸쳐 MongoDB 복제본 세트에 액세스하는 것을 의미하며, 결과적으로 AEM 작성 환경에 대한 활성-활성 클러스터를 생성합니다. MongoDB 복제는 여러 데이터 센터를 통해 동일한 고가용성 및 이중화를 제공하지만, 이제는 데이터 센터 가동 중단을 처리할 수 있는 기능도 제공합니다.

![oakclustermongofailover2datacenter](assets/oakclustermongofailover2datacenters.png)

장점:

* 새로운 AEM 작성자 인스턴스를 사용하여 수평 확장 기능
* 데이터 계층의 고가용성, 이중화 및 자동 페일오버(데이터 센터 중단 포함)

>[!NOTE]
>
>위의 다이어그램에서 AEM Server 3 및 AEM Server 4는 데이터 센터 2의 AEM 서버와 데이터 센터 1의 MongoDB 기본 노드 사이에서 [MongoDB가 있는 Adobe Experience Manager - 확인 목록](/help/sites-deploying/aem-with-mongodb.md#checklists)에 설명된 요구 사항보다 네트워크 지연이 있다고 가정하는 비활성 상태로 표시됩니다. 예를 들어 가용성 영역을 사용하여 최대 지연 시간이 요구 사항과 호환되는 경우 데이터 센터 2의 AEM 서버도 활성 상태가 되어 여러 데이터 센터에 걸쳐 활성 상태의 AEM 클러스터가 생성될 수 있습니다.

>[!NOTE]
>
>이 섹션에서 설명한 MongoDB 아키텍처 개념에 대한 자세한 내용은 [MongoDB 복제](https://docs.mongodb.org/manual/replication/)를 참조하십시오.

## 마이크로커널: 사용할 마이크로커널 {#microkernels-which-one-to-use}

사용 가능한 두 개의 마이크로 커널 중에서 선택할 때 고려해야 할 기본 규칙은 TarMK는 성능을 위해 설계된 반면, MongoMK는 확장성을 위해 사용된다는 것입니다.

이러한 의사 결정 행렬을 사용하여 요구 사항에 맞는 최적의 배포 유형을 설정할 수 있습니다.

Adobe은 아래에 요약된 사용 사례를 제외하고 AEM 작성자 및 게시 인스턴스 모두에 대해 모든 배포 시나리오에서 고객이 사용하는 기본 지속성 기술로 TarMK를 강력히 권장합니다.

### 작성자 인스턴스에서 TarMK보다 AEM MongoMK를 선택하기 위한 예외 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

TarMK보다 MongoMK 지속성 백엔드를 선택하는 주된 이유는 인스턴스의 크기를 수평으로 확장하기 위해서입니다. 즉, 두 개 이상의 활성 작성자 인스턴스가 항상 실행되고 MongoDB를 지속성 스토리지 시스템으로 사용합니다. 두 개 이상의 작성자 인스턴스를 실행해야 하는 이유는 일반적으로 모든 동시 작성 활동을 지원하는 단일 서버의 CPU 및 메모리 용량이 더 이상 지속 가능하지 않기 때문입니다.

새로운 사이트가 생기고 난 후 정확한 동시성 모델이 무엇인지 예상하는 것은 거의 불가능하다. 따라서 Adobe에서는 MongoMK 및 둘 이상의 작성자 활성 노드 사용 여부를 평가할 때 다음 기준을 고려하는 것이 좋습니다.

1. 하루에 연결된 명명된 사용자 수(천 명 이상).
1. 동시 사용자 수: 100명 이상
1. 일별 자산 수집 볼륨: 수십만 개 이상.
1. 일별 페이지 편집 볼륨: 수십만 개 이상(예: 다중 사이트 관리자 또는 뉴스 피드 수집을 통한 자동화된 업데이트 포함).
1. 일별 검색 볼륨: 수만 개 이상.

>[!NOTE]
>
>[힘든 날](/help/sites-developing/tough-day.md)을(를) 사용하여 배포된 하드웨어 구성의 컨텍스트에서 고객 응용 프로그램의 성능을 평가할 수 있습니다.

MongoDB를 사용하는 최소 배포에는 일반적으로 다음 토폴로지가 포함됩니다.

* MongoDB 복제 세트로서, 기본 노드 1개, 보조 노드 2개로 구성되며, 각 MongoDB 인스턴스는 각 노드에서 15밀리초 미만의 지연 시간으로 가용 영역에서 실행됩니다.
* 리더 노드가 하나이고, 리더가 아닌 노드가 하나이며, 두 노드가 모두 동시에 활성 상태인 작성자 인스턴스의 클러스터로, 각 작성자 인스턴스는 MongoDB 기본 및 보조 인스턴스가 실행 중인 각 데이터 센터에서 실행됩니다.

또한 에셋 또는 바이너리가 MongoDB 내에 저장되지 않도록 공유 파일 시스템 또는 Amazon S3에 데이터 저장소를 구성하는 것이 좋습니다. 이렇게 하면 배포 내에서 최적의 성능을 보장할 수 있습니다.

작성자 인스턴스, MongoDB 복제본 또는 전체 데이터 센터 오류가 있는 경우 가동 중지 시간을 최소화하면서 MongoDB 복제본 세트를 두 개 이상의 작성자 인스턴스로 배포하면 추가적인 이점 중 하나가 자동화된 복구 시나리오입니다. 그럼에도 불구하고 TarMK는 제어 장애 조치 메커니즘을 통해 최소한의 다운타임 솔루션을 제공할 수 있으므로 TarMK보다 MongoMK를 선택하는 것이 복구 요구 사항에만 의존해서는 안 됩니다.

배포 후 처음 18개월 동안 상기 기준을 충족하지 못할 것으로 예상되는 경우 먼저 TarMK를 사용하여 AEM을 배포한 다음 나중에 상기 기준이 적용될 때 구성을 다시 평가하고 TarMK에 남아 있는지 또는 MongoMK로 마이그레이션할지를 최종적으로 결정하는 것이 좋습니다.

### 게시 인스턴스에서 TarMK보다 AEM MongoMK를 선택하는 예외 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

게시 인스턴스용으로 MongoMK를 배포하지 않는 것이 좋습니다. 배포의 게시 계층은 거의 항상 작성자 인스턴스의 콘텐츠를 복제하여 동기화 상태를 유지하는 TarMK를 실행하는 완전히 독립적인 게시 인스턴스의 팜으로 배포됩니다. 게시 인스턴스에 적절한 이 &quot;공유되지 않는&quot; 아키텍처를 사용하면 게시 계층의 배포가 선형 방식으로 수평으로 확장할 수 있습니다. 또한 팜 토폴로지를 사용하면 게시 계층을 변경하지 않아도 되도록 업데이트 또는 업그레이드를 순차적으로 게시 인스턴스에 적용할 수 있습니다.

### MongoMK와 함께 AEM 배포 시 사전 요구 사항 및 권장 사항 {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

AEM용 MongoMK 배포를 고려하는 경우 사전 요구 사항 및 권장 사항 세트를 사용할 수 있습니다.

**MongoDB 배포에 대한 필수 필수 사전 요구 사항:**

1. MongoDB 배포 아키텍처 및 크기 조정은 Adobe Consulting 또는 AEM에 익숙한 MongoDB 설계자의 도움을 받아 프로젝트 구현의 일부여야 합니다.
1. 기존 또는 새로운 MongoDB 환경을 유지 및 유지할 수 있다는 자신감을 갖도록 파트너 또는 고객 팀 내에 MongoDB 전문 지식이 있어야 합니다.
1. MongoDB의 상업용 또는 오픈 소스 버전을 배포하도록 선택할 수 있지만(AEM은 두 버전 모두 지원), MongoDB 유지 관리 및 지원 계약은 MongoDB Inc.에서 직접 구매해야 합니다.
1. 전체 AEM 및 MongoDB 아키텍처와 인프라는 Adobe AEM Architect에서 잘 정의하고 검증해야 합니다.
1. MongoDB가 포함된 AEM 배포에 대한 지원 모델을 검토하십시오.

**MongoDB 배포에 대한 강력한 권장 사항:**

* Adobe Experience Manager에 대한 [MongoDB 배포 검토](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)를 참조하십시오.
* [MongoDB 작업 검사 목록](https://docs.mongodb.org/manual/administration/production-checklist/)을 검토합니다.
* MongoDB의 [인증 클래스 참석 - 온라인으로 사용 가능](https://university.mongodb.com/).

>[!NOTE]
>
>이 지침, 사전 요구 사항 및 권장 사항에 대한 모든 추가 질문은 [Adobe 고객 지원 센터](https://helpx.adobe.com/kr/marketing-cloud/contact-support.html)에 문의하십시오.
