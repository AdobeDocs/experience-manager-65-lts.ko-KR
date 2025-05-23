---
title: OSGi에서 AEM 6.5 Forms LTS로 업그레이드
description: AEM 6.5.22.0 Forms에서 AEM 6.5 Forms LTS로 직접 업그레이드할 수 있습니다.
content-type: reference
role: Admin, User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, AEM Forms on OSGi, AEM Forms Upgrade
exl-id: 9233d4b7-441c-4cbd-86f8-2c52b99c3330
source-git-commit: dd45dfe953a111ccbbc71e8e25a8a2577037587a
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 2%

---

# OSGi에서 AEM 6.5 Forms LTS로 업그레이드 {#upgrade-to-aem-forms-osgi}

[AEM 6.5에서 AEM 6.5 LTS로 업그레이드](/help/sites-deploying/upgrade.md)하려면 AEM 6.5.22.0 Forms 이상으로 업그레이드하십시오. AEM 6.5.22.0에서 AEM 6.5 Forms LTS로 직접 업그레이드할 수 있습니다.

AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms, AEM 6.3 Forms, AEM 6.4 Forms 또는 AEM 6.5 Forms을 사용하는 경우 AEM 6.5 Forms LTS로 직접 업그레이드할 수 없습니다. 자세한 업그레이드 경로는 [업그레이드 경로](/help/forms/using/upgrade.md) 설명서를 참조하십시오.

서비스 팩 AEM Forms 6.5.22.0(으)로 업그레이드한 후 다음 단계에 따라 AEM 6.5 LTS Forms으로 업그레이드하십시오.

1. AEM Forms 추가 기능 패키지를 설치합니다. 다음 단계가 나와 있습니다.

   1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
   1. 헤더 메뉴에서 사용할 수 있는 **[!UICONTROL Adobe Experience Manager]**&#x200B;을(를) 선택합니다.
   1. **[!UICONTROL 필터]** 섹션에서:
      1. **[!UICONTROL 솔루션]** 드롭다운 목록에서 **[!UICONTROL Forms]**&#x200B;을(를) 선택합니다.
      1. 패키지의 버전 및 유형을 선택합니다. **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수도 있습니다.
   1. 운영 체제에 적용할 수 있는 패키지 이름을 선택하고 **[!UICONTROL EULA 약관 동의]**&#x200B;를 선택한 다음 **[!UICONTROL 다운로드]**&#x200B;를 선택합니다.
   1. [패키지 관리자](/help/sites-administering/package-manager.md)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
   1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

      [AEM Forms 릴리스](https://experienceleague.adobe.com/ko/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) 문서에 나열된 직접 링크를 사용하여 패키지를 다운로드할 수도 있습니다.

      패키지를 설치한 후 AEM 인스턴스를 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 중지하지 마십시오.** AEM Forms 서버를 중지하기 전에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTERED 메시지가 &lt;crx-repository>/error.log 파일에 나타나고 로그가 안정될 때까지 기다립니다. 또한 몇 가지 패키지는 설치된 상태로 유지될 수 있습니다. 이러한 패키지의 상태를 무시해도 됩니다.


      **다음 추가 JVM 명령줄 매개 변수를 사용하여 AEM 인스턴스를 다시 시작하십시오**:
      `--add-opens java.base/java.util=ALL-UNNAMED --add-exports=java.xml/com.sun.org.apache.xml.internal.serialize=ALL-UNNAMED`

      서버가 스크립트나 서비스를 통해 시작되는 경우 후속 재시작 후에도 유효하도록 위의 내용을 포함하도록 적절하게 업데이트하십시오.

      >[!NOTE]
      >
      > SDK을 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK을 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.

1. 설치 후 작업을 수행합니다.

   * **마이그레이션 유틸리티 실행**

     마이그레이션 유틸리티를 사용하면 이전 버전의 적응형 양식 및 서신 관리 에셋이 AEM 6.5 양식과 호환될 수 있습니다. 이 유틸리티는 AEM 소프트웨어 배포에서 다운로드할 수 있습니다. 마이그레이션 유틸리티를 구성하고 사용하는 방법에 대한 단계별 정보는 [마이그레이션 유틸리티](../../forms/using/migration-utility.md)를 참조하십시오.

     [초안 및 제출 구성 요소 통합](https://helpx.adobe.com/kr/experience-manager/6-3/forms/using/integrate-draft-submission-database.html)에 샘플 을 사용하고 있으며 이전 버전에서 업그레이드하는 경우 업그레이드를 수행한 후 다음 SQL 쿼리를 실행하십시오.

     ```sql
     UPDATE metadata m, additionalmetadatatable am
     SET m.dataType = am.value
     WHERE m.id = am.id
     AND am.key = 'dataType'
     ```

     ```sql
     DELETE from additionalmetadatatable
     WHERE `key` = 'dataType'
     ```

   * **(AEM 6.2 Forms 또는 이전 버전에서만 업그레이드하는 경우) Adobe Sign을 다시 구성하십시오**

     이전 버전의 AEM Forms에서 Adobe Sign을 구성한 경우 AEM 클라우드 서비스에서 Adobe Sign을 다시 구성합니다. 자세한 내용은 [Adobe Sign과 AEM Forms 통합](../../forms/using/adobe-sign-integration-adaptive-forms.md)을 참조하십시오.

   * **jQuery 지원**

     AEM 6.5 Forms에서 jQuery의 버전은 3.2.1로 업데이트되고 jQuery UI 버전은 1.12.1로 업데이트됩니다. AEM Form은 **noConflict** 모드에서 JQuery를 사용합니다. 따라서 다른 jQuery 버전을 사용하는 경우 업그레이드를 수행하는 동안 문제가 표시되지 않습니다. 하지만 AEM 6.5 Forms으로 업그레이드할 때는:

      * 사용자 지정 구성 요소(있는 경우)가 지원되는 jQuery 버전과 호환되는지 확인합니다.
      * 사용자 지정 구성 요소에서 지원되지 않는 API를 제거합니다. 제거된 API 목록은 [업그레이드 안내서](https://jquery.com/upgrade-guide/3.0/)를 참조하십시오. 예를 들어 load(), .unload() 및 .error() API에 대한 지원이 제거됩니다. 앞서 설명한 API 대신 .on() 메서드를 사용합니다. 예를 들어 $(&quot;img&quot;).load(fn)를 $(&quot;img&quot;).on(&quot;load&quot;, fn)으로 변경합니다.

   * **(AEM 6.2 Forms 또는 이전 버전에서만 업그레이드하는 경우) 분석 및 보고서를 다시 구성하십시오**

     AEM 6.4 Forms에서는 소스 및 노출에 대한 성공 이벤트에 대한 트래픽 변수를 사용할 수 없습니다. 따라서 AEM 6.2 Forms 또는 이전 버전에서 업그레이드하면 AEM Forms에서 Adobe Analytics 서버로 데이터 전송을 중단하고 적응형 양식에 대한 분석 보고서를 사용할 수 없습니다. 또한 AEM 6.4 Forms에서는 필드에서 보낸 시간에 대한 양식 분석 버전 트래픽 변수 및 성공 이벤트를 도입했습니다. 따라서 AEM Forms 환경에 대한 분석 및 보고서를 다시 구성합니다. 자세한 단계는 [분석 및 보고서 구성](../../forms/using/configure-analytics-forms-documents.md)을 참조하십시오.

1. 서버가 성공적으로 업그레이드되었는지, 모든 데이터도 성공적으로 마이그레이션되었는지, 정상적으로 작동할 수 있는지 확인하십시오.

   * **번들 상태를 확인합니다.** 모든 번들이 활성 상태인지 확인합니다.
   * **복제 및 역방향 복제 확인:** 마이그레이션된 양식을 게시하고 채우고 제출합니다. 제출된 데이터도 확인합니다.
   * **관리자 및 개발자 사용자 인터페이스에 대한 액세스 권한을 확인합니다.** 관리자 계정에서 AEM 인스턴스에 로그인하고 다음 URL에 대한 액세스 권한이 있는지 확인합니다.

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   >AEM 6.4 Forms에서 crx-repository 구조가 변경되었습니다. 6.3 Forms에서 AEM 6.5 Forms으로 업그레이드하는 경우 새로 만드는 사용자 지정에 변경된 경로를 사용합니다. 변경된 경로의 전체 목록은 [AEM의 Forms 저장소 재구성](https://experienceleague.adobe.com/ko/docs/experience-manager-65/content/implementing/deploying/restructuring/forms-repository-restructuring-in-aem-6-5)을 참조하십시오.
