---
title: WLP(Application Server 설치)에 대한 업그레이드 단계
description: Webspehere Liberty를 통해 배포된 AEM의 인스턴스를 업그레이드하는 방법에 대해 알아봅니다.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: cd04a7a493a575cabf416b53869dd3fe4df7ab6b
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# WLP(Application Server 설치)에 대한 업그레이드 단계 {#upgrade-steps-for-application-server-installations-wlp}

>[!NOTE]
>
>이 페이지에서는 WLP(WebSphere® Liberty)의 AEM 6.5 LTS에 대한 업그레이드 절차를 간략하게 설명합니다.

## 업그레이드 전 단계 {#pre-upgrade-steps}

업그레이드를 실행하기 전에 완료해야 하는 몇 가지 단계가 있습니다. 자세한 내용은 [코드 및 사용자 지정 업그레이드](/help/sites-deploying/upgrading-code-and-customizations.md) 및 [업그레이드 전 유지 관리 작업](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)을 참조하십시오. 또한 시스템이 [AEM 6.5 LTS에 대한 요구 사항](/help/sites-deploying/technical-requirements.md)을 충족하는지 확인하십시오.

[업그레이드 계획](/help/sites-deploying/upgrade-planning.md) 및 [AEM 분석기](/help/sites-deploying/pattern-detector.md)를 통해 AEM 업그레이드의 복잡성을 추정하는 방법을 확인하십시오.

### 마이그레이션 사전 요구 사항 {#migration-prerequisites}

* **필요한 최소 Java 버전**: WLP 서버에 IBM® Sumeru JRE 17을 설치했는지 확인하십시오.

### 업그레이드 수행 {#performing-the-upgrade}

1. 업그레이드 작업을 수행하기 전에 AEM 6.5 서버 백업과 같은 [사전 업그레이드](#pre-upgrade-steps) 단계를 완료했는지 확인하십시오
1. 요구 사항에 따라 다음 업그레이드 경로 중 하나를 선택합니다.
   1. **원본 위치 업그레이드**: 현재 WLP 서버가 서블릿 6을 지원하는 경우 원본 위치 업그레이드를 수행하고 3단계로 계속할 수 있습니다.
   1. **Sidegrade**: 새로운 설정을 원하거나 WLP 서버가 Servlet 6을 지원하지 않는 경우 AEM 6.5 LTS로 새 WLP 인스턴스를 설정하고 [AEM 6.5에서 AEM 6.5 LTS로 콘텐츠 마이그레이션 사용 Oak-upgrade](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md) 안내서에 따라 콘텐츠를 마이그레이션한 다음 [업그레이드된 Codebase 배포](#deploy-upgraded-codebase) 섹션으로 건너뜁니다.

1. AEM 인스턴스를 중지합니다. 일반적으로 다음 명령을 사용하여 수행할 수 있습니다.

   ```shell
   <path-to-wlp-directory>/bin/server stop server_name
   ```

1. 더 이상 필요하지 않은 파일 및 폴더를 제거합니다. 특별히 제거해야 하는 항목은 다음과 같습니다.

   * `dropins` 폴더 및 `expanded` 폴더의 **cq-quickstart-65.war**&#x200B;은(는) 일반적으로 각각 `<path-to-aem-server>/dropins/cq-quickstart-65.war` 및 `<path-to-aem-server>/apps/expanded/cq-quickstart-65.war`에 있습니다.
   * `launchpad/startup` 폴더입니다. 서버 폴더에 있다고 가정하고 터미널에서 다음 명령을 실행하여 삭제할 수 있습니다.

     ```shell
     rm -rf crx-quickstart/launchpad/startup
     ```

   * `base.jar` 파일입니다. 다음 명령을 실행하여 이 작업을 수행할 수 있습니다.

     ```shell
     find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
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
1. Java 17을 설치하고 다음을 실행하여 올바로 설치되었는지 확인합니다.

   ```shell
   java -version
   ```

1. AEM 서버에 대한 시작 매개 변수를 검토하고 요구 사항에 따라 매개 변수를 업데이트해야 합니다. 자세한 내용은 [Java 17 고려 사항](/help/sites-deploying/custom-standalone-install.md#java-17-considerations-java-considerations)을 참조하십시오
1. 새 6.5 LTS war을 다운로드하여 `/<path-to-aem-server>/dropins/`에 있는 dropins 폴더에 복사합니다.
1. AEM 인스턴스 시작: 일반적으로 다음 명령을 사용하여 수행할 수 있습니다.

   ```shell
   <path-to-wlp-directory>/bin/server start server_name
   ```

1. `sling.properties`에 사용자 지정 변경 사항이 있는 경우 아래 지침을 따르십시오.

   1. `<path-to-wlp-directory>/bin/server stop server_name`을(를) 실행하여 AEM 인스턴스 중지
   1. 사용자 지정 `sling.properties` 변경 내용을 새로 생성된 `sling.properties` 파일에 적용합니다(5단계에서 만든 백업 파일 참조)
   1. AEM 인스턴스를 시작합니다. 일반적으로 다음을 실행하여 수행할 수 있습니다. `<path-to-wlp-directory>/bin/server start server_name`

## 업그레이드된 코드베이스 배포 {#deploy-upgraded-codebase}

업그레이드 프로세스가 완료되면 업데이트된 코드 베이스를 배포해야 합니다. 대상 버전의 AEM에서 작동하도록 코드 베이스를 업데이트하는 단계는 [코드 및 사용자 지정 업그레이드 페이지](/help/sites-deploying/upgrading-code-and-customizations.md)에서 확인할 수 있습니다.

## 업그레이드 후 확인 및 문제 해결 수행 {#perform-post-upgrade-checks-and-troubleshooting}

[업그레이드 확인 후 및 문제 해결](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)을 참조하세요.
