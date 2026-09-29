---
title: Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법
description: 이 문서에서는 Apache Maven을 기반으로 하는 AEM 프로젝트를 설정하는 방법에 대해 설명합니다.
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
exl-id: ddc629ac-cf76-4608-9e9b-c8bd3e89da3c
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 21%
---
# Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법 {#how-to-build-aem-projects-using-apache-maven}

AEM 6.5는 패키지 관리 및 프로젝트 구조에 대한 최신 모범 사례를 따릅니다. 온-프레미스 및 AMS 구현 모두에 최신 AEM Project Archetype을 사용합니다.

>[!TIP]
>
>자세한 내용은 다음을 참조하십시오.
>
>* 최신 AEM 프로젝트를 구성하는 방법에 대한 AEM as a Cloud Service 설명서의 [AEM 프로젝트 구조](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure) 문서입니다.
>* Archetype을 사용하여 새 AEM 프로젝트를 시작하는 방법에 대한 [AEM Project Archetype](https://experienceleague.adobe.com/ko/docs/experience-manager-core-components/using/developing/archetype/overview) 설명서입니다.
>* AEM 응용 프로그램을 배포하는 방법에 대한 AEM as a Cloud Service 설명서의 [Adobe Content Package Maven Plugin](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/maven-plugin#developer-tools) 문서입니다.
>
>세 문서 모두 AEM 6.5에 적용됩니다.
