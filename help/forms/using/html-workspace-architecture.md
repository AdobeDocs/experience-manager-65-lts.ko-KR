---
title: AEM Forms Workspace 아키텍처
description: LiveCycle AEM Forms workspace의 개념 정보 및 아키텍처 개요.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
exl-id: d317274f-2c9a-4809-b43e-2efebc8fcb3f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# AEM Forms Workspace 아키텍처 {#aem-forms-workspace-architecture}

AEM Forms workspace 는 CRX™에서 호스팅되는 웹 애플리케이션입니다. 작업 영역이 브라우저에서 열리면 CRX 리소스에 액세스되고 애플리케이션이 브라우저에서 HTML 페이지로 렌더링됩니다.

애플리케이션이 REST 끝점의 AEM Forms 서버에 액세스하여 다음을 수행합니다.

* 사용자 작업, 프로세스 시작 지점, 프로세스 내역 및 사용자 정보 가져오기
* 작업에 대한 작업 수행
* 데이터베이스의 쿼리 작업
* 사용자 환경 설정 등 업데이트

AEM Forms 서버는 JDBC를 통해 AEM Forms 데이터베이스에 액세스합니다. 데이터베이스는 작업, 프로세스 및 인스턴스, 사용자 및 관련 정보를 유지합니다.

AEM Forms 작업 영역은 개별적으로 사용자 정의하고 다른 웹 애플리케이션에서 재사용할 수 있는 모듈식 JavaScript™ 구성 요소로 설계되었습니다. 구성 요소는 웹 애플리케이션에 구조를 제공하는 JavaScript 라이브러리인 BackBone을 기반으로 합니다. BackBone과의 구성 요소 상호 작용을 설명하는 자세한 문서는 [여기](/help/forms/using/backbone-interaction.md)입니다. CRX 폴더 구조의 구성 요소 구성에 대해서는 [이](/help/forms/using/folder-structure.md) 문서에서 설명합니다.

AEM Forms 작업 영역용으로 제공된 패키지:

* `adobe-lc-workspace-pkg-<version>.zip`: CRX 패키지입니다. 즉, 패키지 관리자를 사용하여 CRX에 배포할 수 있습니다.
* `adobe-lc-workspace-<version>-src.zip`: 배포 패키지(배달, 디버그 및 개발 패키지)를 만드는 AEM Forms 작업 영역의 전체 코드와 스크립트가 포함된 아카이브입니다.
