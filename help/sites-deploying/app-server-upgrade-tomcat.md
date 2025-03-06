---
title: Application Server 설치 업그레이드 단계(Tomcat)
description: Tomcat을 통해 배포된 AEM 인스턴스를 업그레이드하는 방법을 알아봅니다.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 7f8de16f-9e9a-4d37-9978-d26c496b911c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Application Server 설치 업그레이드 단계(Tomcat) {#upgrade-steps-for-application-server-installations-tomcat}

>[!NOTE]
>
>이 페이지에서는 Tomcat의 AEM 6.5 LTS 업그레이드 절차에 대해 간략히 설명합니다.

## 업그레이드 전 단계 {#pre-upgrade-steps}

업그레이드를 실행하기 전에 완료해야 하는 몇 가지 단계가 있습니다. 자세한 내용은 [코드 및 사용자 지정 업그레이드](/help/sites-deploying/upgrading-code-and-customizations.md) 및 [업그레이드 전 유지 관리 작업](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)을 참조하십시오. 또한 시스템이 [AEM 6.5 LTS에 대한 요구 사항](/help/sites-deploying/technical-requirements.md)을 충족하는지 확인하고 [업그레이드 계획 고려 사항](/help/sites-deploying/upgrade-planning.md) 및 [Analyzer](/help/sites-deploying/pattern-detector.md)를 통해 복잡성을 추정하는 방법을 확인하십시오.


### 마이그레이션 사전 요구 사항 {#migration-prerequisites}

* **필요한 최소 Java 버전**: Tomcat 서버에 Oracle® JRE 17을 설치했는지 확인하십시오.
* **Tomcat 서버**: 6.5 LTS에 필요한 Tomcat 서버 버전은 **11.0.x**&#x200B;입니다.

### 업그레이드 수행 {#performing-the-upgrade}

이 절차의 모든 예제에서는 Tomcat을 Application Server로 사용하며 AEM의 작업 버전이 이미 배포되어 있음을 의미합니다. 이 절차는 AEM 버전 **6.5**&#x200B;에서 **6.5 LTS**(으)로 수행된 업그레이드를 문서화하기 위한 것입니다.

1. AEM 6.5가 이미 배포된 경우 *`https://<serveraddress:port>/system/console/bundles`*&#x200B;에 액세스하여 번들이 올바르게 작동하는지 확인하십시오.
1. 그런 다음 AEM 6.5를 중지합니다. 이 작업은 Tomcat 앱 관리자(*`https://<serveraddress:port>/manager/html`*)에서 수행할 수 있습니다.
1. 업그레이드 작업을 수행하기 전에 AEM 6.5 서버 백업과 같은 [업그레이드 전](#pre-upgrade-steps) 작업을 완료했는지 확인하십시오
1. Java 17을 설치하고 다음 명령을 실행하여 올바로 설치되었는지 확인합니다.

   ```
   java –version
   ```

1. AEM 6.5 LTS 호환 Tomcat 서버 설정
1. AEM 서버에 대한 시작 매개 변수를 검토하고 시스템 요구 사항에 따라 매개 변수를 업데이트해야 합니다. 자세한 내용은 [Java 17 고려 사항](/help/sites-deploying/custom-standalone-install.md#java-17-considerations-java-considerations)을 참조하십시오
1. Java 17을 사용하여 Tomcat 서버에 새로 다운로드한 6.5 LTS war을 배포하고 다음을 실행하여 AEM 6.5 LTS Tomcat 서버를 시작합니다.

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEM이 실행되고 나면 *`https://<serveraddress:port>/cq/system/console/bundles`*&#x200B;에 액세스하여 모든 번들이 실행 중인지 확인하십시오.
1. AEM 6.5 LTS Tomcat 서버를 중지합니다. 대부분의 경우 터미널에서 이 명령을 실행하여 `./catalina.sh` 스크립트를 실행하여 이 작업을 수행할 수 있습니다.

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. 이제 다음 단계에 따라 콘텐츠를 AEM 6.5에서 AEM 6.5 LTS로 마이그레이션하십시오. [Oak 업그레이드를 사용한 AEM 6.5에서 AEM 6.5 LTS 콘텐츠 마이그레이션](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md)
1. 콘텐츠가 마이그레이션되면 `sling.properties` 파일에 필요한 사용자 지정 변경 내용을 적용합니다
1. 다음을 실행하여 AEM 6.5 LTS Tomcat 서버를 시작합니다.

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEM이 시작되는 동안 오류 로그를 모니터링하여 오류가 없고 AEM이 원활하게 실행되고 있는지 확인합니다
1. AEM 6.5 LTS가 시작되면 *`https://<serveraddress:port>/cq/system/console/bundles`*&#x200B;에 액세스하여 번들이 올바르게 작동하는지 확인하십시오.

## 업그레이드된 코드베이스 배포 {#deploy-upgraded-codebase}

업그레이드 프로세스가 완료되면 업데이트된 코드 베이스를 배포해야 합니다. 대상 버전의 AEM에서 작동하도록 코드 베이스를 업데이트하는 단계는 [코드 및 사용자 지정 업그레이드 페이지](/help/sites-deploying/upgrading-code-and-customizations.md)에서 확인할 수 있습니다.

## 업그레이드 후 확인 및 문제 해결 수행 {#perform-post-upgrade-checks-and-troubleshooting}

자세한 내용은 [업그레이드 확인 및 문제 해결 이후](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)를 참조하십시오.
