---
title: Application Server 설치 업그레이드 단계
description: 애플리케이션 서버를 통해 배포된 AEM의 인스턴스를 업그레이드하는 방법에 대해 알아봅니다.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 28701105452c347c5470fdb582d783e7aef1adb0
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# Application Server 설치 업그레이드 단계 {#upgrade-steps-for-application-server-installations}

>[!NOTE]
>
>이 페이지에서는 WLP(WebSphere Liberty)에 대한 AEM 6.5 LTS war의 업그레이드 절차에 대해 간략히 설명합니다.

## 업그레이드 전 단계 {#pre-upgrade-steps}

업그레이드를 실행하기 전에 완료해야 하는 몇 가지 단계가 있습니다. 자세한 내용은 [코드 및 사용자 지정 업그레이드](/help/sites-deploying/upgrading-code-and-customizations.md) 및 [업그레이드 전 유지 관리 작업](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)을 참조하십시오. 또한 시스템이 AEM 6.5 LTS의 요구 사항을 충족하는지 확인하십시오. Analyzer를 통해 업그레이드의 복잡성을 예측하고 업그레이드 계획을 수립하는 방법을 확인하십시오(자세한 내용은 [업그레이드 계획](/help/sites-deploying/upgrade-planning.md) 참조).

### 마이그레이션 사전 요구 사항 {#migration-prerequisites}

* **필요한 최소 Java 버전**: WLP 서버에 IBM Sumeru JRE 17을 설치했는지 확인하십시오.

### 업그레이드 수행 {#performing-the-upgrade}

1. 업그레이드 작업을 시작하기 전에 인스턴스의 백업을 수행하십시오.
1. 사용 중인 WLP 서버 버전에 따라 즉석 업그레이드가 필요한지 또는 옆 등급이 필요한지 식별합니다. 현재 WLP 서버가 서블릿 6을 지원하는 경우 바로 업그레이드를 수행하고 이 설명서를 계속할 수 있습니다. 그렇지 않은 경우 사이드 그레이드를 수행해야 합니다. Sidegrade의 경우 Oak 업그레이드 설명서가 포함된 콘텐츠 마이그레이션 - [추가할 TBD 링크]를 따르십시오.
1. AEM 인스턴스를 중지합니다. 일반적으로 다음 명령을 사용하여 수행할 수 있습니다.

   ```shell
   <path-to-wlp-directory>/bin/server stop server_name
   ```

1. 더 이상 필요하지 않은 파일 및 폴더를 제거합니다. 특별히 제거해야 하는 항목은 다음과 같습니다.

   * `dropins` 폴더 및 확장된 폴더의 `cq-quickstart-65.war`은(는) 일반적으로 각각 `<path-to-aem-server>/dropins/cq-quickstart-65.war` 및 `<path-to-aem-server>/apps/expanded/cq-quickstart-65.war`에 있습니다.
   * `launchpad/startup` 폴더입니다. 서버 폴더에 있다고 가정하고 터미널에서 다음 명령을 실행하여 삭제할 수 있습니다.

     ```shell
     rm -rf crx-quickstart/launchpad/startup
     ```

   * `base.jar` 파일입니다. 다음 명령을 실행하여 이 작업을 수행할 수 있습니다.

     ```shell
     find crx-quickstart/launchpad -type f -name 
     "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * `BootstrapCommandFile_timestamp.txt` 파일:

     ```shell
     rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * 다음을 실행하여 `sling.options` 파일 제거:

     ```shell
     find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * `sling.bootstrap.txt` 파일 제거:

     ```shell
     rm -rf crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. `sling.properties` 파일(일반적으로 `crx-quickstart/conf/`에 있음)을 백업하고 삭제합니다.
1. 서블릿 버전을 `server.xml` 파일에서 **6.0**(으)로 변경
1. AEM 서버에 대한 시작 매개 변수를 검토하고 시스템 요구 사항에 따라 매개 변수를 업데이트해야 합니다. 자세한 내용은 [사용자 지정 독립 실행형 설치](/help/sites-deploying/custom-standalone-install.md)를 참조하십시오
1. Java 17을 설치하고 다음을 실행하여 올바로 설치되었는지 확인합니다.

   ```shell
   java -version
   ```

1. 소프트웨어 배포에서 새 war 6.5 LTS를 다운로드하여 `/<path-to-aem-server>/dropins/`에 있는 dropins 폴더에 복사합니다.
1. AEM 인스턴스 시작: 일반적으로 다음 명령을 사용하여 수행할 수 있습니다.

   ```shell
   <path-to-wlp-directory>/bin/server start server_name
   ```

1. `sling.properties`에 사용자 지정 변경 사항이 있는 경우 아래 지침을 따르십시오.

   1. `<path-to-wlp-directory>/bin/server stop server_name`을(를) 실행하여 AEM 인스턴스 중지
   1. 새로 생성된 `sling.properties` 파일에 사용자 지정 `sling.properties` 변경 내용을 적용합니다(6단계에서 만든 백업 파일 참조)
   1. AEM 인스턴스를 시작합니다. 일반적으로 다음을 실행하여 수행할 수 있습니다. `<path-to-wlp-directory>/bin/server start server_name`

## 업그레이드된 코드베이스 배포 {#deploy-upgraded-codebase}

즉각적 업그레이드 프로세스가 완료되면 업데이트된 코드 베이스를 배포해야 합니다. 대상 버전의 AEM에서 작동하도록 코드 베이스를 업데이트하는 단계는 [코드 및 사용자 지정 업그레이드](/help/sites-deploying/upgrading-code-and-customizations.md) 페이지에서 확인할 수 있습니다.

## 업그레이드 후 확인 및 문제 해결 수행 {#perform-post-upgrade-checks-and-troubleshooting}

자세한 내용은 [업그레이드 확인 및 문제 해결 이후](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)를 참조하십시오.