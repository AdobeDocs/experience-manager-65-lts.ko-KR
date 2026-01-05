---
title: Adobe Experience Manager Forms 6.5 LTS SP1 핫픽스
description: AEM Forms 6.5 LTS용 핫픽스를 다운로드하여 설치하는 방법에 대한 정보를 제공합니다.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 504240bdad9e964460a9fcdc555228c7cb02e314
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---


# Adobe Experience Manager Forms 6.5 LTS 핫픽스{#aem-form-hotfix}

이 문서에서는 알려진 문제를 해결하고, 시스템 안정성을 개선하며, AEM Forms 6.5 LTS의 전반적인 성능을 개선하기 위해 구현된 주요 수정 사항을 나열합니다.

>[!NOTE]
>
> 핫픽스는 이전의 모든 수정 사항을 포함하여 누적되도록 설계되었습니다. 릴리스에 최신 핫픽스를 적용하면 최신 문제를 해결할 수 있을 뿐만 아니라 이전의 모든 버그 수정 및 개선 사항이 통합되어 있습니다.

## AEM Forms 6.5 LTS에 대한 핫픽스 {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>날짜</strong></td>
    <td><strong>핫픽스 다운로드 링크(AEM 소프트웨어 배포 링크)</strong></td>
    <td><strong>해결된 문제</strong></td>
  </tr>
  <tr>
    <td>
      <strong>2025년 9월 9일</strong><br>
    <td>
    <ul>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-win-pkg-6.1.176-RHF-002.zip">Windows의 AEM 서비스 팩 6.5 LTS용 핫픽스2</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]hotfix-on-add-on/adobe-aemfd-linux-pkg-6.1.176-RHF-002.zip">Linux의 AEM 서비스 팩 6.5 LTS용 핫픽스2</a></li>
     <li>MacOS- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-osx-pkg-6.1.176-RHF-002.zip">MacOS의 AEM 서비스 팩 6.5 LTS용 핫픽스2</a></li>
    <td>
    <ul>
    <li>SSV(서버 측 유효성 검사)를 활성화했을 때 제출이 실패할 수 있는 문제를 해결하여 양식 제출 안정성을 개선했습니다. 문제가 발생하면 [Adobe Experience Manager Forms 지원](https://business.adobe.com/in/support/main.html)에 문의하십시오.
    </li>
    </ul>
    </td>    
  </tr>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## OSGi 핫픽스 다운로드 및 설치 {#download-install-hotfix}

다음 단계를 수행하여 핫픽스를 다운로드하고 설치합니다.

1. 소프트웨어 배포 링크에서 [핫픽스](#hotfix-for-adaptive-forms)를 다운로드합니다.
1. Experience Manager 패키지(.zip)를 가져오고 파일을 번들(.jar)할 수 있도록 핫픽스 아카이브 파일을 추출합니다.
1. [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing)를 통해 패키지(.zip)를 업로드하고 설치합니다.
1. Configuration Manager 번들 `https://server:host/system/console/bundles`을(를) 열고 번들(.jar)을 업로드한 후 설치합니다. 핫픽스가 설치되었습니다.
