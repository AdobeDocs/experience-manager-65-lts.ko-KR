---
title: Commerce integration framework(CIF) 추가 기능의 주요 변경 사항
description: 이전 CIF 버전과 비교한 Commerce integration framework(CIF) 추가 기능의 주요 변경 사항.
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: aced89a0-dec1-49fe-afbc-3ddf1318b900
source-git-commit: 79cce324382bada2e9aec107b8e494723bf490e9
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Commerce integration framework(CIF) 추가 기능의 주요 변경 사항{#notable-changes}

이 문서에서는 Commerce integration framework(CIF) 추가 기능과 이전 CIF 버전(주로 CIF Classic(Quickstart) 및 CIF Open-source로 알려짐) 간의 중요한 차이점을 조명합니다.

## 설치 및 업데이트

AEM CIF 추가 기능 패키지가 AEM 패키지 관리자에 설치되고 업데이트됩니다.

**이전 CIF 버전**

* CIF Classic: 설치할 필요가 없습니다. CIF은 빠른 시작에 속했습니다. CIF 업데이트는 일반 AEM 또는 서비스 팩 업데이트의 일부였습니다
* CIF 오픈 소스: GitHub를 통해 설치. 업데이트는 수동 업데이트/유지 관리 작업의 일부였습니다.

## 끝점 구성

끝점은 OSGi 콘솔을 통해 구성됩니다.

**이전 CIF 버전**

* CIF Classic: AEM에서 OSGi 구성을 통해
* CIF 오픈 소스: CIF 구성 브라우저 사용

## CIF Venia 프로젝트 배포

프로젝트는 [GitHub AEM Guides - CIF Venia 프로젝트](https://github.com/adobe/aem-cif-guides-venia)에서 사용할 수 있으며 AEM 패키지 관리자를 통해 배포됩니다.

**이전 CIF 버전**

* CIF Classic: AEM 패키지 설치 사용

## 제품 카탈로그 데이터

제품 카탈로그 데이터는 필요한 GraphQL API를 지원하는 외부 엔드포인트에 대한 실시간 호출을 통해 온디맨드로 요청됩니다. 이러한 API는 지정된 날짜에 라이브 또는 스테이징된 데이터에 대한 액세스를 지원합니다. 복제 불필요.

**이전 CIF 버전**

* CIF Classic: 라이브 및 스테이징된 제품 데이터를 가져와 전체 또는 델타 제품 가져오기를 통해 AEM Author의 JCR에서 지속됩니다. 라이브 제품 데이터가 AEM 게시로 복제됩니다.

## AEM 렌더링을 사용한 제품 카탈로그 경험

AEM은 제품 및 범주에 할당된 AEM 카탈로그 템플릿을 사용하여 제품 카탈로그 경험을 즉시 렌더링합니다. 복제 불필요.

**이전 CIF 버전**

* CIF Classic: AEM 작성자는 카탈로그 블루프린트 도구를 사용하여 모든 카테고리/제품에 대한 AEM 페이지를 만듭니다. 이러한 페이지는 AEM 게시로 복제됩니다.

>[!NOTE]
>
>AEM Managed Service 또는 AEM On-Premise와 함께 CIF을 사용하는 방법에 대한 추가 설명서는 [Commerce integration framework](https://developer.adobe.com/apis/experiencecloud/commerce-integration-framework/getting-started.html)을(를) 참조하십시오.
