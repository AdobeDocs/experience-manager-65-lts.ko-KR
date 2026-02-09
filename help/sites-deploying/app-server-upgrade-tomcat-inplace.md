---
title: Application Server 설치 업그레이드 단계(Tomcat)
description: Tomcat을 통해 배포된 AEM 인스턴스를 업그레이드하는 방법을 알아봅니다.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: b3c4e946a3f235fa0e3a0945f1ad692ee195e3ef
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Application Server 설치 업그레이드 단계(Tomcat - 즉석 업그레이드) {#upgrade-steps-for-application-server-installations-tomcat-inplace}

>[!NOTE]
>
>이 페이지에서는 Tomcat의 AEM 6.5 LTS에서 AEM 6.5 LTS Servicepack으로 업그레이드하는 절차(즉석 업그레이드)에 대해 간략히 설명합니다. AEM 6.5에서 6.5 LTS로 업그레이드하려면 [다음을 참조하세요](/help/sites-deploying/app-server-upgrade-tomcat.md).

## 업그레이드 전 단계 {#pre-upgrade-steps}

업그레이드를 실행하기 전에 완료해야 하는 몇 가지 단계가 있습니다. 자세한 내용은 [업그레이드 전 유지 관리 작업](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)을 참조하세요. 또한 시스템이 [AEM 6.5 LTS Servicepack에 대한 요구 사항](/help/sites-deploying/technical-requirements.md)을 충족하는지 확인하고 [업그레이드 계획 고려 사항](/help/sites-deploying/upgrade-planning.md)을 참조하십시오.


### 마이그레이션 사전 요구 사항 {#migration-prerequisites}

* **필요한 최소 Java 버전**: Tomcat 서버에 Oracle® JRE 17/21을 설치했는지 확인하십시오.
* **Tomcat 서버**: AEM 6.5 LTS 및 해당 ServicePack용 Tomcat 서버의 지원 버전은 **10.0.x** 및 **10.1.x**&#x200B;입니다.

### 업그레이드 수행 {#performing-the-upgrade}

이 절차의 모든 예는 Tomcat을 애플리케이션 서버로 사용하며 AEM 6.5 LTS의 작업 버전이 이미 배포되어 있음을 의미합니다. 이 절차는 AEM 버전 **6.5** LTS에서 **6.5 LTS** Servicepack으로 수행한 업그레이드를 문서화하기 위한 것입니다.

1. AEM 6.5 LTS가 이미 배포된 경우 *`https://<serveraddress:port>/system/console/bundles`*&#x200B;에 액세스하여 번들이 올바르게 작동하는지 확인하십시오.
1. 그런 다음 AEM 6.5 LTS를 중지합니다. 이 작업은 Tomcat 앱 관리자(*`https://<serveraddress:port>/manager/html`*)에서 수행할 수 있습니다.
1. 업그레이드 작업을 수행하기 전에 AEM 6.5 LTS 서버 백업과 같은 [업그레이드 전](#pre-upgrade-steps) 작업을 완료했는지 확인하십시오
1. AEM 6.5 LTS Tomcat 서버를 중지합니다. 대부분의 경우 터미널에서 이 명령을 실행하여 `./catalina.sh` 스크립트를 실행하여 이 작업을 수행할 수 있습니다.

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. 더 이상 필요하지 않은 파일 및 폴더를 제거합니다. 특별히 제거해야 하는 항목은 다음과 같습니다.

   * **cq-quickstart-65.war** 파일 및 `cq-quickstart-65` 폴더의 `webapps` 폴더는 일반적으로 `<path-to-aem-server>/webapps`에 있습니다.
   * `launchpad/startup` 폴더입니다. 서버 폴더에 있다고 가정하고 터미널에서 다음 명령을 실행하여 삭제할 수 있습니다.

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/startup
     ```

   * `base.jar` 파일입니다. 다음 명령을 실행하여 이 작업을 수행할 수 있습니다.

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * `BootstrapCommandFile_timestamp.txt` 파일:

     ```shell
     rm -f <path-to-aem-server>/bin/crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * 다음을 실행하여 `sling.options` 파일 제거:

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * `sling.bootstrap.txt` 파일 제거:

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. `sling.properties` 파일(일반적으로 `<path-to-aem-server>/bin/crx-quickstart/launchpad/`에 있음)을 백업하고 삭제합니다.
1. AEM 6.5 LTS Servicepack war 파일을 `<path-to-aem-server>/webapps` 폴더에 복사
1. 다음을 실행하여 AEM 6.5 LTS Tomcat 서버를 시작합니다.

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEM이 시작되는 동안 오류 로그를 모니터링하여 오류가 없고 AEM이 원활하게 실행되고 있는지 확인합니다
1. AEM 6.5 LTS가 시작되면 *`https://<serveraddress:port>/cq/system/console/bundles`*&#x200B;에 액세스하여 번들이 올바르게 작동하는지 확인하십시오.

## 업그레이드 후 확인 및 문제 해결 수행 {#perform-post-upgrade-checks-and-troubleshooting}

자세한 내용은 [업그레이드 확인 및 문제 해결 이후](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)를 참조하십시오.
