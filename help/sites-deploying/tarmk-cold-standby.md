---
title: TarMK 콜드 대기로 AEM을 실행하는 방법
description: TarMK 콜드 대기 설정을 생성, 구성 및 유지 관리하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 71e3d2cd-4e22-44a2-88dd-1f165bf2b3d8
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '2672'
ht-degree: 0%

---

# TarMK 콜드 대기로 AEM을 실행하는 방법{#how-to-run-aem-with-tarmk-cold-standby}

## 소개 {#introduction}

Tar 마이크로 커널의 콜드 대기 용량을 사용하면 하나 이상의 대기 Adobe Experience Manager(AEM) 인스턴스를 기본 인스턴스에 연결할 수 있습니다. 동기화 프로세스는 기본 인스턴스에서 대기 인스턴스로만 수행됨을 의미합니다.

대기 인스턴스의 목적은 마스터 저장소의 라이브 데이터 사본을 보장하고 어떤 이유로든 마스터를 사용할 수 없는 경우 데이터 손실 없이 빠른 전환을 보장하는 것입니다.

컨텐츠는 파일 또는 저장소 손상에 대한 무결성 검사 없이 기본 인스턴스와 대기 인스턴스 간에 선형적으로 동기화됩니다. 이러한 설계로 인해 대기 인스턴스는 기본 인스턴스의 정확한 복사본이며 기본 인스턴스의 불일치를 완화할 수 없습니다.

>[!NOTE]
>
>콜드 대기 기능은 **작성자** 인스턴스에서 고가용성이 필요한 시나리오를 보호하기 위한 것입니다. Adobe Tar 마이크로 커널을 사용하는 **게시** 인스턴스에서 고가용성이 필요한 경우 게시 팜을 사용하는 것이 좋습니다.
>
>사용 가능한 배포에 대한 자세한 내용은 [권장 배포](/help/sites-deploying/recommended-deploys.md) 페이지를 참조하십시오.

>[!NOTE]
>
>대기 인스턴스가 설정되거나 기본 노드에서 파생되면 관리 관련 활동의 경우 다음 콘솔에 대한 액세스만 허용합니다.
>
>* OSGI 웹 콘솔
>
>다른 콘솔은 액세스할 수 없습니다.

## 작동 방식 {#how-it-works}

기본 AEM 인스턴스에서 TCP 포트가 열려 수신 메시지를 수신 대기합니다. 현재 슬레이브가 마스터에게 보내는 메시지에는 두 가지 유형이 있습니다.

* 현재 헤드의 세그먼트 ID를 요청하는 메시지
* 지정된 ID로 세그먼트 데이터를 요청하는 메시지

대기(Standby)는 주기적으로 기본 머리의 현재 머리의 세그먼트 ID를 요청한다. 로컬에서 알 수 없는 세그먼트는 검색됩니다. 이미 존재하는 경우 필요한 경우 세그먼트를 비교하고 참조된 세그먼트도 요청합니다.

>[!NOTE]
>
>대기 인스턴스는 동기화 전용 모드에서 실행 중이므로 어떤 유형의 요청도 받지 않습니다. 대기 인스턴스에서 사용할 수 있는 유일한 섹션은 번들 및 서비스 구성을 용이하게 하는 웹 콘솔입니다.

일반적인 TarMK 콜드 대기 배포:

![chlimage_1](assets/chlimage_1.png)

## 기타 특성 {#other-characteristics}

### 견고성 {#robustness}

데이터 흐름은 연결 및 네트워크 관련 문제를 자동으로 감지하고 처리하도록 설계되었습니다. 모든 패킷은 체크섬과 함께 번들로 제공되며, 연결 문제 또는 손상된 패킷이 발생하면 재시도 메커니즘이 트리거됩니다.

#### 성능 {#performance}

기본 인스턴스에서 TarMK 콜드 대기를 활성화하는 것은 성능에 거의 영향을 미치지 않습니다. 추가 CPU 소모량이 적고 추가 하드 디스크 및 네트워크 IO로 인해 성능 문제가 발생해서는 안 됩니다.

대기 모드에서는 동기화 프로세스 동안 높은 CPU 소비를 예상할 수 있습니다. 프로시저는 다중 스레드가 아니므로 여러 코어를 사용하여 속도를 높일 수 없습니다. 데이터를 변경하거나 전송하지 않으면 측정 가능한 활동이 없습니다. 연결 속도는 하드웨어 및 네트워크 환경에 따라 다르지만 저장소 크기나 SSL 사용에 따라 다르지 않습니다. 초기 동기화에 필요한 시간이나 주 노드에서 많은 데이터가 변경되었을 때를 예상할 때 이 점을 염두에 두십시오.

#### 보안 {#security}

모든 인스턴스가 동일한 인트라넷 보안 영역에서 실행된다고 가정할 경우 보안 위반 위험이 크게 줄어듭니다. 그러나 슬레이브와 마스터 간에 SSL 연결을 활성화하여 추가 보안 계층을 추가할 수 있습니다. 이렇게 하면 중간자에 의해 데이터가 손상될 가능성이 줄어듭니다.

또한 수신 요청의 IP 주소를 제한하여 연결할 수 있는 대기 인스턴스를 지정할 수 있습니다. 이렇게 하면 인트라넷의 어느 누구도 저장소를 복사할 수 없도록 하는 데 도움이 됩니다.

>[!NOTE]
>
>Dispatcher과 콜드 대기 설정의 일부인 서버 사이에 로드 밸런서를 추가하는 것이 좋습니다. 사용자 트래픽을 **primary** 인스턴스로만 보내도록 부하 분산 장치를 구성해야 합니다. 이는 일관성을 보장하고 콜드 대기 메커니즘이 아닌 다른 방법으로 대기 인스턴스에서 콘텐츠가 복사되지 않도록 하기 위해 필요합니다.

## AEM TarMK 콜드 대기 설정 생성 {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>AEM 6.3에서 세그먼트 노드 저장소 및 대기 저장소 서비스의 PID가 이전 버전과 비교하여 다음과 같이 변경되었습니다.
>
>* from org.apache.jackrabbit.oak.org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService에 대한 **plugins**.segment.standby.store.StandbyStoreService
>* from org.apache.jackrabbit.oak.org.apache.jackrabbit.oak.segment.SegmentNodeStoreService에 대한 **plugins**.segment.SegmentNodeStoreService
>
>이 변경 사항을 반영하도록 필요한 구성을 조정합니다.

TarMK 콜드 대기 설정을 생성하려면 먼저 기본 설치 폴더의 전체 설치 폴더를 새 위치로 파일 시스템 복사를 수행하여 대기 인스턴스를 생성합니다. 그런 다음 해당 역할(`primary` 또는 `standby`)을 지정하는 실행 모드로 각 인스턴스를 시작할 수 있습니다.

다음은 하나의 마스터와 하나의 대기 인스턴스로 설정을 만들기 위해 따라야 하는 절차입니다.

1. AEM을 설치합니다.

1. 인스턴스를 종료하고 설치 폴더를 콜드 대기 인스턴스가 실행되는 위치에 복사합니다. 다른 컴퓨터에서 실행 중인 경우에도 인스턴스를 구분하려면 각 폴더에 수사적 이름(*aem-primary* 또는 *aem-standby*)을 지정해야 합니다.
1. 기본 인스턴스의 설치 폴더로 이동하여 다음을 수행합니다.

   1. `aem-primary/crx-quickstart/install` 아래에 있을 수 있는 이전 OSGi 구성을 확인하고 삭제합니다.

   1. `aem-primary/crx-quickstart/install` 아래에 `install.primary` 폴더 만들기

   1. `aem-primary/crx-quickstart/install/install.primary` 아래에 기본 설정 노드 저장소 및 데이터 저장소에 필요한 구성을 만듭니다.
   1. 같은 위치에 `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`이라는 파일을 만든 다음 적절하게 구성하십시오. 구성 옵션에 대한 자세한 내용은 [구성](/help/sites-deploying/tarmk-cold-standby.md#configuration)을 참조하십시오.

   1. 외부 데이터 저장소와 함께 AEM TarMK 인스턴스를 사용하는 경우 `crx3`(이)라는 `aem-primary/crx-quickstart/install` 아래에 `crx3` 폴더를 만듭니다.

   1. 데이터 저장소 구성 파일을 `crx3` 폴더에 넣습니다.

   예를 들어, 외부 파일 데이터 저장소로 AEM TarMK 인스턴스를 실행하는 경우 다음 구성 파일이 필요합니다.

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   아래에서는 기본 인스턴스에 대한 샘플 구성을 찾습니다.

   **샘플** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config 샘플**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config 샘플**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 기본 실행 모드를 지정했는지 확인하기 위해 기본 실행 모드를 시작합니다.

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. **org.apache.jackrabbit.oak.segment** 패키지에 대한 Apache Sling 로깅 로거를 만듭니다. 로그 수준을 &quot;Debug&quot;로 설정하고 로그 출력을 */logs/tarmk-coldstandby.log*&#x200B;과(와) 같은 별도의 로그 파일로 지정합니다. 자세한 내용은 [로깅](/help/sites-deploying/configure-logging.md)을 참조하십시오.
1. **standby** 인스턴스의 위치로 이동하여 Jar를 실행하여 시작하십시오.
1. 기본 로깅 구성과 동일한 로깅 구성을 만듭니다. 그런 다음 인스턴스를 중지합니다.
1. 그런 다음 대기 인스턴스를 준비합니다. 기본 인스턴스와 동일한 단계를 수행하여 이 작업을 수행할 수 있습니다.

   1. `aem-standby/crx-quickstart/install`에 포함될 수 있는 모든 파일을 삭제합니다.
   1. `aem-standby/crx-quickstart/install` 아래에 `install.standby` 폴더 만들기

   1. 라는 두 개의 구성 파일을 만듭니다.

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`

   1. `aem-standby/crx-quickstart/install` 아래에 `crx3` 폴더 만들기

   1. 데이터 저장소 구성을 만들어 `aem-standby/crx-quickstart/install/crx3` 아래에 배치합니다. 이 예제에서 만들어야 하는 파일은 다음과 같습니다.

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config

   1. 파일을 편집하고 필요한 구성을 만듭니다.

   다음은 일반적인 대기 인스턴스에 대한 샘플 구성 파일입니다.

   **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config의 샘플**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config 샘플**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config 샘플**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 대기 실행 모드를 사용하여 **standby** 인스턴스를 시작합니다.

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

또한 다음과 같이 웹 콘솔을 통해 서비스를 구성할 수 있습니다.

1. *https://serveraddress:serverport/system/console/configMgr*&#x200B;의 웹 콘솔로 이동
1. **Apache Jackrabbit Oak 세그먼트 Tar 콜드 대기 서비스**&#x200B;라는 서비스를 찾고 두 번 클릭하여 설정을 편집합니다.
1. 새 설정을 적용할 수 있도록 설정을 저장하고 인스턴스를 다시 시작합니다.

>[!NOTE]
>
>언제든지 Sling 설정 웹 콘솔에서 **기본** 또는 **대기** 실행 모드가 있는지 확인하여 인스턴스의 역할을 확인할 수 있습니다.
>
>*https://localhost:4502/system/console/status-slingsettings*(으)로 이동하여 **&quot;실행 모드&quot;** 줄을 확인하면 이 작업을 수행할 수 있습니다.

## 최초 동기화 {#first-time-synchronization}

준비가 완료되고 대기가 처음 시작된 후 대기가 기본 인스턴스로 올라가면 인스턴스 간 네트워크 트래픽이 많이 발생합니다. 로그를 참조하여 동기화 상태를 확인할 수 있습니다.

대기 *tarmk-coldstandby.log*&#x200B;에서 다음과 같은 항목을 볼 수 있습니다.

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

대기의 *error.log*&#x200B;에 다음과 같은 항목이 표시됩니다.

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

위의 로그 스니펫에서 *10.20.30.40*&#x200B;은(는) 기본 항목의 IP 주소입니다.

**primary** *tarmk-coldstandby.log*&#x200B;에 다음과 같은 항목이 표시됩니다.

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message 's.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd' from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

이 경우 로그에 언급된 &quot;클라이언트&quot;는 **대기** 인스턴스입니다.

이러한 항목이 로그에 표시되지 않으면 동기화 프로세스가 완료되었다고 가정할 수 있습니다.

위의 항목은 폴링 메커니즘이 제대로 작동하고 있음을 보여주지만, 폴링이 발생할 때 동기화되는 데이터가 있는지 파악하는 것이 유용한 경우가 많습니다. 이렇게 하려면 다음과 같은 항목을 찾습니다.

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

또한 비공유 `FileDataStore`을(를) 사용하여 실행할 때 다음과 같은 메시지가 이진 파일이 제대로 전송되고 있는지 확인합니다.

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### 구성 {#configuration}

콜드 대기 서비스에 사용할 수 있는 OSGi 설정은 다음과 같습니다.

* **구성 유지:** 사용 가능한 경우 기존 OSGi 구성 파일 대신 저장소에 구성이 저장됩니다. Adobe에서는 기본 구성이 대기 모드로 설정되지 않도록 프로덕션 시스템에서 이 설정을 비활성화하는 것이 좋습니다.

* **모드(`mode`):** 인스턴스의 실행 모드를 선택합니다.

* **포트(포트):** 통신에 사용할 포트입니다. 기본값은 `8023`입니다.

* **기본 호스트(`primary.host`):** - 기본 인스턴스의 호스트입니다. 이 설정은 대기 모드에만 적용할 수 있습니다.
* **동기화 간격(`interval`):** - 이 설정은 동기화 요청 사이의 간격을 결정하며 대기 인스턴스에만 적용할 수 있습니다.

* **허용된 IP 범위(`primary.allowed-client-ip-ranges`):** - 기본 연결이 허용되는 IP 범위입니다.
* **보안(`secure`):** SSL 암호화를 사용하도록 설정합니다. 이 설정을 사용하려면 모든 인스턴스에서 활성화해야 합니다.
* **대기 읽기 시간 제한(`standby.readtimeout`):** 대기 인스턴스에서 실행된 요청의 시간 제한(밀리초)입니다. 사용되는 기본값은 60000(1분)입니다.

* **대기 자동 정리(`standby.autoclean`):** 동기화 주기에 저장소 크기가 증가하는 경우 정리 메서드를 호출합니다.

>[!NOTE]
>
>Adobe에서는 기본 및 대기 ID가 서로 다르므로 오프로딩과 같은 서비스에 대해 별도로 식별할 수 있도록 권장합니다.
>
>대기 모드에서 *sling.id*&#x200B;을(를) 삭제하고 인스턴스를 다시 시작하면 이 문제가 해결됩니다.

## 페일오버 절차 {#failover-procedures}

어떤 이유로든 기본 인스턴스가 실패할 경우 아래에 자세히 설명된 대로 시작 실행 모드를 변경하여 기본 역할을 수행하도록 대기 인스턴스 중 하나를 설정할 수 있습니다.

>[!NOTE]
>
>기본 인스턴스에 사용된 설정과 일치하도록 구성 파일을 편집합니다.

1. 대기 인스턴스가 설치된 위치로 이동하여 중지합니다.

1. 설정으로 구성된 로드 밸런서가 있는 경우 이 시점에서 로드 밸런서의 구성에서 기본 을 제거할 수 있습니다.
1. 대기 설치 폴더에서 `crx-quickstart` 폴더를 백업합니다. 대기 모드를 새로 설정할 때 시작점으로 사용할 수 있다.

1. `primary` 실행 모드를 사용하여 인스턴스를 다시 시작하십시오.

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 로드 밸런서에 새 기본 을 추가합니다.
1. 새 대기 인스턴스를 생성 및 시작합니다. 자세한 정보는 [AEM TarMK 콜드 대기 설정 만들기](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)에 대한 위의 절차를 참조하십시오.

## 콜드 대기 설정에 핫픽스 적용 {#applying-hotfixes-to-a-cold-standby-setup}

콜드 대기 모드에 핫픽스를 적용하는 권장 방법은 해당 핫픽스를 기본 인스턴스에 설치한 다음 핫픽스가 설치된 새 콜드 대기 인스턴스에 복제하는 것입니다.

아래 설명된 단계에 따라 이 작업을 수행할 수 있습니다.

1. JMX 콘솔로 이동하여 **org.apache.jackrabbit.oak: Status(&quot;Standby&quot;).bean을 사용하여 콜드 대기 인스턴스에서 동기화 프로세스** 중지합니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 [모니터링](#monitoring)의 섹션을 참조하십시오.
1. 콜드 대기 인스턴스를 중지합니다.
1. 기본 인스턴스에 핫픽스를 설치합니다. 핫픽스를 설치하는 방법에 대한 자세한 내용은 [패키지를 사용하여 작업하는 방법](/help/sites-administering/package-manager.md)을 참조하십시오.
1. 설치 후 인스턴스에 문제가 있는지 테스트합니다.
1. 설치 폴더를 삭제하여 콜드 대기 인스턴스를 제거합니다.
1. 운영 인스턴스를 중지하고 전체 설치 폴더의 파일 시스템 복제본을 콜드 대기 위치에 수행하여 복제합니다.
1. 콜드 대기 인스턴스로 작동하도록 새로 생성된 클론을 다시 구성합니다. [AEM TarMK 콜드 대기 설정 만들기](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)를 참조하십시오.
1. 기본 및 콜드 대기 인스턴스를 모두 시작합니다.

## 모니터링 {#monitoring}

이 기능은 JMX 또는 MBean을 사용하여 정보를 노출합니다. [JMX 콘솔](/help/sites-administering/jmx-console.md)을 사용하여 대기 및 마스터의 현재 상태를 검사할 수 있습니다. `type org.apache.jackrabbit.oak:type="Standby"`의 MBean에서 `Status`(이)라는 정보를 찾을 수 있습니다.

**대기**

대기 인스턴스를 관찰하면 한 개의 노드가 표시됩니다. ID는 일반적으로 일반 UUID입니다.

이 노드에는 5개의 읽기 전용 속성이 있습니다.

* 동기화 프로세스가 실행 중인지 여부를 나타내는 `Running:` 부울 값입니다.

* `Mode:` 클라이언트: 뒤에 인스턴스를 식별하는 데 사용되는 UUID가 옵니다. 이 UUID는 구성이 업데이트될 때마다 변경됩니다.

* `Status:` 현재 상태의 텍스트 표시(예: `running` 또는 `stopped`).

* `FailedRequests:`연속 오류 수.
* `SecondsSinceLastSuccess:` 서버와의 통신이 마지막으로 성공한 이후 경과된 시간(초)입니다. 성공적으로 통신하지 못한 경우 `-1`이(가) 표시됩니다.

다음과 같은 세 가지 무효화 방법도 있습니다.

* `start():`이(가) 동기화 프로세스를 시작합니다.
* `stop():`이(가) 동기화 프로세스를 중지합니다.
* `cleanup():`이(가) 대기 상태에서 정리 작업을 실행합니다.

**기본**

기본 항목을 관찰하면 ID 값이 TarMK 대기 서비스가 사용 중인 포트 번호(기본적으로 8023)인 MBean을 통해 일부 일반 정보가 노출됩니다. 대부분의 메소드 및 속성은 대기와 동일하지만 일부는 다릅니다.

* `Mode:`은(는) 항상 `primary` 값을 표시합니다.

또한 마스터에 연결된 최대 10개의 클라이언트(대기 인스턴스)에 대한 정보를 검색할 수 있습니다. MBean ID는 인스턴스의 UUID입니다. 이러한 MBean에는 호출할 수 있는 메서드가 없지만 몇 가지 유용한 읽기 전용 특성은 다음과 같습니다.

* `Name:` 클라이언트의 ID입니다.
* `LastSeenTimestamp:` 텍스트 표시 중 마지막 요청의 타임스탬프입니다.
* `LastRequest:` 클라이언트의 마지막 요청입니다.
* `RemoteAddress:` 클라이언트의 IP 주소입니다.
* `RemotePort:` 클라이언트가 마지막 요청에 사용한 포트입니다.
* `TransferredSegments:` 이 클라이언트로 전송된 총 세그먼트 수입니다.
* `TransferredSegmentBytes:`이 클라이언트로 전송된 총 바이트 수입니다.

## 콜드 대기 저장소 유지 관리 {#cold-standby-repository-maintenance}

### 개정 정리 {#revision-clean}

>[!NOTE]
>
>기본 인스턴스에서 [온라인 수정 정리](/help/sites-deploying/revision-cleanup.md)를 실행하는 경우 아래에 제시된 수동 절차가 필요하지 않습니다. 또한 온라인 수정 버전 정리를 사용하는 경우 대기 인스턴스의 `cleanup ()` 작업이 자동으로 수행됩니다.

>[!NOTE]
>
>대기 모드에서 오프라인 개정 정리를 실행하지 마십시오. 필요하지 않으며 세그먼트 저장소 크기를 줄이지 않습니다.

Adobe에서는 시간이 지남에 따라 과도한 저장소 증가를 방지하기 위해 유지 관리를 정기적으로 실행하는 것이 좋습니다. 콜드 대기 저장소 유지 관리를 수동으로 수행하려면 아래 단계를 따르십시오.

1. JMX 콘솔로 이동하여 **org.apache.jackrabbit.oak: Status(&quot;Standby&quot;)** Bean을 사용하여 대기 인스턴스에서 대기 프로세스를 중지합니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 [모니터링](/help/sites-deploying/tarmk-cold-standby.md#monitoring)에 대한 위의 섹션을 참조하십시오.

1. 기본 AEM 인스턴스를 중지합니다.
1. 기본 인스턴스에서 Oak 압축 도구를 실행합니다. 자세한 내용은 [저장소 유지 관리](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)를 참조하십시오.
1. 기본 인스턴스를 시작합니다.
1. 첫 번째 단계에 설명된 것과 동일한 JMX 빈을 사용하여 대기 인스턴스에서 대기 프로세스를 시작합니다.
1. 로그를 보고 동기화가 완료될 때까지 기다립니다. 현재 대기 저장소의 실질적인 증가가 나타날 수 있습니다.
1. 첫 번째 단계에 설명된 것과 동일한 JMX 빈을 사용하여 대기 인스턴스에서 `cleanup()` 작업을 실행합니다.

오프라인 압축이 저장소 내역을 효과적으로 재작성하므로 대기 인스턴스가 기본 인스턴스와 동기화를 완료하는 데 평소보다 오래 걸릴 수 있으므로 저장소의 변경 사항을 계산하는 데 더 많은 시간이 걸릴 수 있습니다. 이 프로세스가 완료되면 대기 상태의 저장소 크기는 기본 상태의 저장소와 대략 동일한 크기가 됩니다.

또는 기본 저장소에서 압축을 실행한 후 수동으로 기본 저장소를 대기 저장소에 복사할 수 있습니다. 기본적으로 압축이 실행될 때마다 대기 저장소를 다시 빌드합니다.

### 데이터 저장소 가비지 컬렉션 {#data-store-garbage-collection}

그렇지 않으면 삭제된 바이너리가 파일 시스템에 남아 결국 드라이브를 채우게 되므로 파일 데이터 저장소 인스턴스에서 가비지 수집을 수시로 실행하는 것이 중요합니다. 가비지 수집을 실행하려면 아래 절차를 따르십시오.

1. [위의](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance) 섹션에 설명된 대로 콜드 대기 저장소 유지 관리를 실행합니다.
1. 유지 관리 프로세스가 완료되고 인스턴스가 다시 시작된 후:

   * [JMX 콘솔을 통해 데이터 저장소 가비지 컬렉션 실행](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console)에 설명된 대로 기본 데이터 저장소에서 관련 JMX Bean을 통해 데이터 저장소 가비지 컬렉션을 실행합니다.
   * 대기 모드에서는 **BlobGarbageCollection** MBean - `startBlobGC()`을 통해서만 데이터 저장소 가비지 컬렉션을 사용할 수 있습니다. **RepositoryManagement** MBean을 대기 모드에서 사용할 수 없습니다.

   >[!NOTE]
   >
   >공유 데이터 저장소를 사용하지 않는 경우 기본 데이터 저장소에서 먼저 가비지 수집을 실행한 다음 대기 데이터베이스에서 실행합니다.
