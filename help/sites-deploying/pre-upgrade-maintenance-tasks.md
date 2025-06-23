---
title: 업그레이드 전 유지 관리 작업
description: AEM에 권장되는 업그레이드 전 작업에 대해 알아봅니다.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 1dd5d370-d1d4-4d15-9663-35b941b9076b
source-git-commit: 8f7bbc3887601e10cf29e99ee54959a10c8a3f98
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 0%

---

# 업그레이드 전 유지 관리 작업{#pre-upgrade-maintenance-tasks}

업그레이드를 시작하기 전에 다음 유지 관리 작업을 수행하여 문제가 발생할 경우 시스템이 준비되고 롤백될 수 있는지 확인하는 것이 중요합니다.

* [색인 정의](#index-definitions)
* [충분한 디스크 공간 확인](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [AEM 전체 백업](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [quickstart.properties 파일 생성](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [워크플로우 및 감사 로그 삭제 구성](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [업그레이드 전 작업 설치, 구성 및 실행](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [/install 디렉토리에서 업데이트 제거](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [콜드 대기 인스턴스 중지](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [사용자 정의 예약된 작업 비활성화](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [오프라인 개정 정리 실행](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [데이터 저장소 가비지 수집 실행](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [필요한 경우 데이터베이스 스키마 업그레이드](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [로그 파일 회전](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## 색인 정의 {#index-definitions}

최신 AEM 6.5 서비스 팩과 함께 릴리스된 필수 인덱스 정의를 설치했는지 확인하십시오. 자세한 내용은 [AEM 6.5 servicepack 릴리스 노트](https://experienceleague.adobe.com/ko/docs/experience-manager-65/content/release-notes/release-notes)를 참조하세요.

## 충분한 디스크 공간 확인 {#ensure-sufficient-disk-space}

업그레이드를 실행할 때 디스크 공간이 충분한지 확인합니다.

## AEM 전체 백업 {#fully-back-up-aem}

업그레이드를 시작하기 전에 AEM을 완전히 백업해야 합니다. 해당되는 경우 저장소, 애플리케이션 설치, 데이터 저장소 및 Mongo 인스턴스를 백업해야 합니다. AEM 인스턴스 백업 및 복원에 대한 자세한 내용은 [백업 및 복원](/help/sites-administering/backup-and-restore.md)을 참조하십시오.

## quickstart.properties 파일 생성 {#generate-quickstart-properties}

jar 파일에서 AEM을 시작하면 `crx-quickstart/conf`에 `quickstart.properties` 파일이 생성됩니다. AEM이 이전에 시작 스크립트로만 시작된 경우에는 이 파일이 없고 업그레이드가 실패합니다. 이 파일이 있는지 확인하고 jar 파일이 없는 경우 AEM을 다시 시작합니다.

## 워크플로우 및 감사 로그 삭제 구성 {#configure-wf-audit-purging}

`WorkflowPurgeTask` 및 `com.day.cq.audit.impl.AuditLogMaintenanceTask` 작업에는 별도의 OSGi 구성이 필요하며 이 구성 없이는 작업할 수 없습니다. 업그레이드 전 작업 실행 중에 실패하는 경우 구성 누락이 가장 큰 원인입니다. 따라서 이러한 작업을 실행하지 않으려면 이러한 작업에 대한 OSGi 구성을 추가하거나 업그레이드 전 최적화 작업 목록에서 모두 제거해야 합니다. 워크플로 제거 작업을 구성하는 데 필요한 설명서는 [워크플로 인스턴스 관리](/help/sites-administering/workflows-administering.md)에서 찾을 수 있으며, 감사 로그 유지 관리 작업 구성은 [AEM의 감사 로그 유지 관리](/help/sites-administering/operations-audit-log.md)에서 찾을 수 있습니다.


## 업그레이드 전 작업 설치, 구성 및 실행 {#install-configure-run-pre-upgrade-tasks}

이전에 수동으로 수행해야 했던 업그레이드 전 유지 관리 작업이 최적화 및 자동화되고 있습니다. 업그레이드 전 유지 관리 최적화를 통해 이러한 작업을 트리거하고 요청 시 결과를 검사할 수 있는 통합된 방법을 사용할 수 있습니다.

### 사용 방법 {#how-to-use-it}

`PreUpgradeTasksMBean` OSGI 구성 요소에는 한 번에 모두 실행할 수 있는 업그레이드 전 유지 관리 작업 목록이 사전 구성되어 있습니다. 아래 절차에 따라 작업을 구성할 수 있습니다.

1. *https://serveraddress:serverport/system/console/configMgr*(으)로 이동하여 웹 콘솔로 이동

1. &quot;**preupgradetasks**&quot;을(를) 검색한 후 일치하는 첫 번째 구성 요소를 클릭합니다. 구성 요소의 전체 이름은 `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`입니다.

1. 아래와 같이 실행해야 하는 유지 관리 작업 목록을 수정합니다.

   ![1487758925984](assets/1487758925984.png)

다음은 각 유지 관리 작업이 설계된 실행 모드에 대한 설명입니다.

| 작업 | 메모 |
|---|---|
| 워크플로 제거 작업 | 실행하기 전에 Adobe Granite 워크플로우 제거 구성 OSGi를 구성해야 합니다. |
| GenerateBundlesListFileTask |   |
| 개정 정리 작업 |   |
| com.day.cq.audit.impl.AuditLogMaintenanceTask | 실행 전에 감사 로그 제거 스케줄러 OSGi 구성을 구성해야 합니다. |

### 업그레이드 전 상태 검사의 기본 구성 {#default-configuration-of-the-pre-upgrade-health-checks}

`PreUpgradeTasksMBeanImpl` OSGI 구성 요소는 `runAllPreUpgradeHealthChecks` 메서드가 호출될 때 실행할 업그레이드 전 상태 검사 태그 목록과 함께 미리 구성되어 있습니다.

* **system** - granite 유지 관리 상태 검사에 사용되는 태그입니다.

* **업그레이드 전** - 업그레이드 전에 실행되도록 설정할 수 있는 모든 상태 검사에 추가할 수 있는 사용자 지정 태그입니다.

**MBean 메서드**

관리되는 Bean 기능은 [JMX 콘솔](/help/sites-administering/jmx-console.md)을 사용하여 액세스할 수 있습니다.

다음을 수행하여 MBean에 액세스할 수 있습니다.

1. *https://serveraddress:serverport/system/console/jmx*&#x200B;의 JMX 콘솔로 이동
1. **PreUpgradeTasks**&#x200B;을(를) 검색하고 결과를 클릭합니다.

1. **작업** 섹션에서 메서드를 선택하고 다음 창에서 **호출**&#x200B;을 선택합니다.

다음은 `PreUpgradeTasksMBeanImpl`에서 노출하는 사용 가능한 모든 메서드의 목록입니다.

| 메서드 이름 | 유형 | 설명 |
|---|---|---|
| runAllPreUpgradeTasks() | 작업 | 목록의 업그레이드 전 유지 관리 작업을 모두 실행합니다. |
| runPreUpgradeTask(preUpgradeTaskName) | 작업 | 이름이 매개 변수로 지정된 업그레이드 전 유지 관리 작업을 실행합니다. |
| getPreUpgradeTaskLastRunTime(preUpgradeTaskName) | 작업 | 이름이 매개 변수로 지정된 업그레이드 전 유지 관리 작업의 정확한 실행 시간을 표시합니다. |
| getPreUpgradeTaskLastRunState(preUpgradeTaskName) | 작업 | 이름이 매개 변수로 지정된 업그레이드 전 유지 관리 작업의 마지막 실행 상태를 표시합니다. |
| runAllPreUpgradeHealthChecks(shutDownOnSuccess) | 작업 | 모든 업그레이드 전 상태 검사를 실행하고 해당 상태를 sling 홈 경로의 preUpgradeHCStatus.properties 파일에 저장합니다. shutDownOnSuccess가 true로 설정되면 AEM 인스턴스가 종료되지만 업그레이드 전 상태 검사가 모두 OK 상태인 경우에만 가능합니다. 속성 파일은 향후 업그레이드를 위한 사전 조건으로 사용되며, 사전 업그레이드 상태 검사 실행이 실패할 경우 업그레이드 프로세스가 중지됩니다. 업그레이드 전 상태 검사 결과를 무시하고 업그레이드를 시작하려면 파일을 삭제할 수 있습니다. |
| detectUsageOfUnavailableAPI(aemVersion) | 작업 | 지정된 AEM 버전으로 업그레이드할 때 더 이상 충족되지 않는 가져온 모든 패키지를 나열합니다. 대상 AEM 버전은 매개 변수로 제공되어야 합니다. |

>[!NOTE]
>
>MBean 메서드는 다음을 통해 호출할 수 있습니다.
>
>* JMX 콘솔
>* JMX에 연결하는 모든 외부 응용 프로그램
>* cURL
>

## /install 디렉토리에서 업데이트 제거 {#remove-updates-install-directory}

>[!NOTE]
>
>AEM 인스턴스를 종료한 후 crx-quickstart/install 디렉토리에서만 패키지를 제거합니다. 이 단계는 내부 업그레이드 절차를 시작하기 전 마지막 단계 중 하나입니다.

로컬 파일 시스템의 `crx-quickstart/install` 디렉터리를 통해 배포된 서비스 팩, 기능 팩 또는 핫픽스를 모두 제거하십시오. 이렇게 하면 업데이트가 완료된 후 새 AEM 버전 위에 실수로 이전 핫픽스 및 서비스 팩을 설치하지 않아도 됩니다.

## 콜드 대기 인스턴스 중지 {#stop-tarmk-coldstandby-instance}

TarMK 콜드 대기를 사용하는 경우 콜드 대기 인스턴스를 중지합니다. 이렇게 하면 업그레이드에 문제가 있는 경우 온라인으로 다시 돌아올 수 있는 효율적인 방법을 보장합니다. 업그레이드가 성공적으로 완료되면 업그레이드된 기본 인스턴스에서 콜드 대기 인스턴스를 다시 빌드해야 합니다.

## 사용자 정의 예약된 작업 비활성화 {#disable-custom-scheduled-jobs}

애플리케이션 코드에 포함된 OSGi 예약 작업을 비활성화합니다.

## 오프라인 개정 정리 실행 {#execute-offline-revision-cleanup}

>[!NOTE]
>
>이 단계는 TarMK 설치에만 필요합니다

TarMK를 사용하는 경우 업그레이드하기 전에 오프라인 개정 정리를 실행해야 합니다. 이렇게 하면 저장소 마이그레이션 단계와 후속 업그레이드 작업이 훨씬 빠르게 실행되고 업그레이드가 완료된 후 온라인 개정 정리가 성공적으로 실행될 수 있습니다. 오프라인 수정 버전 정리 실행에 대한 자세한 내용은 [오프라인 수정 버전 정리 수행](/help/sites-deploying/revision-cleanup.md#revision-cleanuprevision-cleanup)을 참조하십시오.

## 데이터 저장소 가비지 수집 실행 {#execute-datastore-garbage-collection}

CRX3 인스턴스에서 개정 정리를 실행한 후 데이터 저장소 가비지 수집을 실행하여 데이터 저장소에서 참조되지 않은 블롭을 제거해야 합니다. 지침은 [데이터 저장소 가비지 수집](/help/sites-administering/data-store-garbage-collection.md)에 대한 설명서를 참조하십시오.

## 로그 파일 회전 {#rotate-log-files}

Adobe은 업그레이드를 시작하기 전에 현재 로그 파일을 보관하는 것을 권장합니다. 이렇게 하면 업그레이드 도중 및 이후에 로그 파일을 보다 쉽게 모니터링하고 검사하여 발생할 수 있는 문제를 식별하고 해결할 수 있습니다.
