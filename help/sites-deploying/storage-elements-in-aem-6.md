---
title: AEM 6.5 LTS의 스토리지 요소
description: AEM 6.5 LTS에서 사용할 수 있는 노드 저장소 구현 및 저장소 유지 관리 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: e51842b5-fa91-42d2-a490-5a7e867dada7
source-git-commit: 0e60c406a9cf1e5fd13ddc09fd85d2a2f8a410f6
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# AEM 6.5 LTS의 스토리지 요소{#storage-elements-in-aem}

이 문서에서는 다음 사항을 다룹니다.

* [AEM 6.5 LTS의 스토리지 개요](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [저장소 유지 관리](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6.5 LTS의 스토리지 개요 {#overview-of-storage-in-aem}

AEM 6.5 LTS에서 가장 중요한 변경 사항 중 하나는 저장소 수준의 혁신입니다.

현재 AEM 6.5 LTS에서 사용할 수 있는 노드 스토리지 구현은 Tar 스토리지와 MongoDB 스토리지라는 두 가지가 있습니다.

### Tar 스토리지 {#tar-storage}

#### Tar 저장소를 사용하여 새로 설치된 AEM 인스턴스 실행 {#running-a-freshly-installed-aem-instance-with-tar-storage}

기본적으로 AEM 6.5 LTS는 기본 구성 옵션을 사용하여 Tar 저장소를 사용하여 노드 및 바이너리를 저장합니다. 다음을 수행하여 저장소 설정을 수동으로 구성할 수 있습니다.

1. AEM 6.5 LTS quickstart jar를 다운로드하여 새 폴더에 저장합니다.
1. 다음을 실행하여 AEM 압축을 풉니다.

   `java -jar <aem-65-lts>.jar -unpack`

1. 설치 디렉터리에 이름이 `crx-quickstart\install`인 폴더를 만듭니다.

1. 새로 만든 폴더에 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` 파일을 만듭니다.

1. 파일을 편집하고 구성 옵션을 설정합니다. AEM의 Tar 스토리지 구현의 기반이 되는 세그먼트 노드 스토어에 다음 옵션을 사용할 수 있습니다.

   * `repository.home`: 다양한 저장소 관련 데이터가 저장되는 저장소 홈의 경로입니다. 기본적으로 세그먼트 파일은 crx-quickstart/segmentstore 디렉토리 아래에 저장됩니다.
   * `tarmk.size`: 세그먼트의 최대 크기(MB)입니다. 기본값은 256MB입니다.

1. AEM을 시작합니다.

### Mongo 스토리지 {#mongo-storage}

>[!NOTE]
>
>Mongo의 최소 지원 버전은 Mongo 6입니다.

#### Mongo 스토리지로 새로 설치한 AEM 인스턴스 실행 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6.5 LTS는 아래 절차에 따라 MongoDB 스토리지에서 실행되도록 구성할 수 있습니다.

1. AEM 6.5 LTS quickstart jar를 다운로드하여 새 폴더에 저장합니다.
1. 다음 명령을 실행하여 AEM 압축을 풉니다.

   `java -jar <aem-65-lts>.jar -unpack`

1. MongoDB가 설치되어 있고 `mongod`의 인스턴스가 실행 중인지 확인하십시오. 자세한 내용은 [MongoDB 설치](https://docs.mongodb.org/manual/installation/)를 참조하십시오.
1. 설치 디렉터리에 이름이 `crx-quickstart\install`인 폴더를 만듭니다.
1. `crx-quickstart\install` 디렉터리에 사용할 구성의 이름으로 구성 파일을 만들어 노드 저장소를 구성합니다.

   AEM의 MongoDB 저장소 구현의 기반이 되는 문서 노드 저장소는 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` 파일을 사용합니다

1. 파일을 편집하고 구성 옵션을 설정합니다. 다음 옵션을 사용할 수 있습니다.

   * `mongouri`: Mongo 데이터베이스에 연결하는 데 필요한 [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/)입니다. 기본값은 `mongodb://localhost:27017`입니다.
   * `db`: Mongo 데이터베이스의 이름입니다. 기본적으로 새 AEM 6.5 LTS 설치에서는 **aem-author**&#x200B;을(를) 데이터베이스 이름으로 사용합니다.
   * `cache`: 캐시 크기(MB)입니다. 이 캐시 크기는 DocumentNodeStore에서 사용되는 다양한 캐시에 분산됩니다. 기본값은 256입니다.
   * `changesSize`: 비교 출력을 캐시하기 위해 Mongo에서 사용되는 제한 컬렉션 크기(MB)입니다. 기본값은 256입니다.
   * `customBlobStore`: 사용자 지정 데이터 저장소가 사용됨을 나타내는 부울 값입니다. 기본값은 false입니다.

1. 사용할 데이터 저장소의 PID로 구성 파일을 만들고 해당 파일을 편집하여 구성 옵션을 설정합니다. 자세한 내용은 [노드 저장소 및 데이터 저장소 구성](/help/sites-deploying/data-store-config.md)을 참조하세요.

1. 다음을 실행하여 MongoDB 스토리지 백엔드와 함께 AEM 6.5 LTS Jar을 시작합니다.

   ```shell
   java -jar <aem-65-lts>.jar -r crx3,crx3mongo
   ```

   백엔드 실행 모드가 **`-r`**&#x200B;인 경우 예제는 MongoDB 지원으로 시작합니다.

#### 투명한 대용량 페이지 비활성화 {#disabling-transparent-huge-pages}

Red Hat® Linux®는 THP(Transparent Huge Pages)라는 메모리 관리 알고리즘을 사용합니다. AEM은 세분화된 읽기 및 쓰기를 수행하지만 THP는 대규모 작업에 최적화되어 있습니다. 따라서 Tar 및 Mongo 스토리지에서 THP를 모두 비활성화하는 것이 좋습니다. 알고리즘을 비활성화하려면 다음 단계를 따르십시오.

1. 선택한 텍스트 편집기에서 `/etc/grub.conf` 파일을 엽니다.
1. **grub.conf** 파일에 다음 줄을 추가합니다.

   ```
   transparent_hugepage=never
   ```

1. 마지막으로 다음을 실행하여 설정이 적용되었는지 확인합니다.

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   THP가 비활성화된 경우 위 명령의 출력은 다음과 같아야 합니다.

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>다음 리소스를 참조하십시오.
>
>* Red Hat® Linux®의 투명 대용량 페이지에 대한 자세한 내용은 Red Hat® 고객 포털에서 다음 문서를 참조하십시오. [Red Hat Enterprise Linux 6, 7 및 8에서 투명 Hugepage를 사용, 모니터링 및 비활성화하는 방법](https://access.redhat.com/solutions/46111)
>* Linux® 조정 팁은 [성능 최적화](/help/sites-deploying/configuring-performance.md)를 참조하십시오.
>

## 저장소 유지 관리 {#maintaining-the-repository}

저장소에 대한 각 업데이트는 콘텐츠 개정을 만듭니다. 결과적으로 각 업데이트 시 저장소의 크기가 커집니다. 저장소 증가를 제어하지 않으려면 디스크 리소스를 확보하기 위해 이전 버전을 정리해야 합니다. 이 유지 관리 기능을 개정 정리 라고 합니다. 개정 정리 메커니즘은 저장소에서 오래된 데이터를 제거하여 디스크 공간을 확보합니다. 수정 버전 정리에 대한 자세한 내용은 [수정 버전 정리 페이지](/help/sites-deploying/revision-cleanup.md)를 참조하십시오.
