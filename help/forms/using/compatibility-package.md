---
title: 호환성 패키지
description: AEM Forms 6.5 LTS에 호환성 패키지를 설치하면 AEM Forms 6.5 및 이전 버전의 서신 관리 에셋과 더 이상 사용되지 않는 적응형 양식 템플릿 및 페이지를 사용할 수 있습니다
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 3a529a82-e2fd-423c-96c1-a5accc87775e
source-git-commit: 2e0cbe62754866d31de69547f9af1f2f63930f2c
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---

# 호환성 패키지{#compatibility-package}

## 개요 {#overview}

대화형 통신은 AEM Forms 6.5 LTS에서 고객 커뮤니케이션을 만들기 위한 기본적이고 권장되는 방법입니다. AEM Forms 6.5 LTS에서 문자를 계속 사용하려면 최신 [AEMFD 호환성 패키지](https://experienceleague.adobe.com/ko/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)를 설치해야 합니다.

AEMFD 호환성 패키지를 통해 [AEM Forms에서 다음 자산을 사용할 수 있습니다. 6.5.22.0, 6.4, 6.3 및 6.2(AEM Forms 6.5 LTS](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms))

* 문서 단편
* 편지
* 데이터 사전
* 적응형 양식 더 이상 사용되지 않는 템플릿 및 페이지

자세한 내용은 [호환성 패키지를 설치하여 AEM Forms 6.5와 호환되도록 만든 Assets](../../forms/using/compatibility-package.md#assetsmadecompatible)을(를) 참조하십시오.

## AEM Forms 6.5 LTS에서 AEM Forms 6.5, 6.4, 6.3 및 6.2 자산에 대한 지원 추가 {#add-support-for-aem-forms-and-assets-in-aem-forms-6.5.lts}

업그레이드를 수행한 후 다음을 수행하여 AEMFD 호환성 패키지를 설치하고 에셋을 6.5와 호환되도록 합니다.

[AEM 호환성 패키지](https://experienceleague.adobe.com/ko/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)가 미리 설치되어 있는지 확인하십시오.

1. 최신 AEM 6.5 LTS [호환성 패키지](https://experienceleague.adobe.com/ko/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)를 설치하십시오.

   패키지를 업로드하고 설치하는 방법에 대한 자세한 내용은 [패키지를 사용하여 작업하는 방법](/help/sites-administering/package-manager.md)을 참조하세요.

1. 로그가 안정되면 서버를 다시 시작합니다.
1. 자산을 6.5 LTS와 호환되도록 하려면 마이그레이션 유틸리티를 사용하십시오.

   >[!NOTE]
   >
   > `Ctrl + C` 명령을 사용하여 SDK을 다시 시작하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK을 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.

   자세한 내용은 [마이그레이션 유틸리티](../../forms/using/migration-utility.md)를 참조하십시오.

## Assets은 호환성 패키지를 설치하여 AEM Forms 6.5 LTS와 호환되도록 했습니다 {#assetsmadecompatible}

호환성 패키지를 설치하여 다음 에셋 및 템플릿을 AEM Forms 6.5 LTS와 호환되도록 할 수 있습니다.

* AEM 6.4 및 이전 버전의 서신 관리 Assets:

   * [편지](../../forms/using/create-letter.md)
   * [데이터 사전](/help/forms/using/data-dictionary.md)
   * 문서 단편

* 적응형 양식 사용 중단된 템플릿:

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabEnrollmentTemplate
   * /libs/fd/af/templates/tabEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* 적응형 양식 더 이상 사용되지 않는 페이지:

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment
