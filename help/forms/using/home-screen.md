---
title: 홈 화면
description: AEM Forms 앱 홈 화면의 구성 요소에 대한 설명
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: b8e413e0-1387-46c7-891a-85d5fc61288b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 홈 화면{#home-screen}

AEM Forms 앱에 로그인하면 홈 화면으로 리디렉션됩니다.

## 기본 홈 화면 {#default-home-screen}

기본적으로 홈 화면에는 시작점 및 작업(연결된 서버가 AEM Forms Workflow가 활성화된 경우)을 포함한 모든 양식과 관련 썸네일이 표시됩니다. AEM Forms 서버에서 썸네일을 지정할 수 있습니다.

다음 그림은 기본 홈 화면에서 필수 구성 요소에 대한 콜아웃으로 주석을 추가합니다.

![Forms 앱 홈 화면](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **메뉴 단추**: **메뉴** 단추를 선택하여 작업, Forms, 보낼 편지함 및 설정으로 이동합니다. AEM Forms 앱이 AEM Forms JEE 서버에 연결되어 있으면 작업 옵션이 표시됩니다. 또한 작업 옵션에는 프로세스의 작업에서 생성된 초안이 저장됩니다. AEM Forms OSGi 서버의 경우 작업 옵션이 숨겨집니다. 보낼 편지함은 저장된 양식 및 초안을 서버와 동기화하기 전에 저장합니다. 앱이 [서버와 동기화됨](../../forms/using/sync-app.md)되면 보낼 편지함에 저장된 모든 양식 및 초안이 AEM Forms 서버로 업로드됩니다. 설정에 대한 자세한 내용은 [일반 설정 업데이트](../../forms/using/update-general-settings.md)를 참조하십시오.
1. **작업 또는 양식**: 작업할 작업 또는 양식을 선택하십시오.
1. **가로 줄임표**: 양식에 작업을 사용할 수 있음을 나타냅니다. 생략 부호를 탭하면 작성자가 제공한 작업 및 설명이 표시됩니다. 생략 부호를 선택하면 **초안 삭제** 및 **완료** 옵션이 표시됩니다.
1. **새로 고침 아이콘**: 앱을 AEM Forms 서버와 동기화할 수 있도록 새로 고침 아이콘을 선택합니다.

### 홈 화면 사용자 정의 {#customizing-the-home-screen}

![일반 설정](assets/gen-settings.png)

앱의 **[일반 설정](../../forms/using/update-general-settings.md)** 또는 HTML Workspace의 **기본 설정** 탭에서 앱의 기본 홈 화면을 변경할 수 있습니다.

앱에서 홈 화면 설정을 변경하면 현재 로그인한 사용자 또는 현재 모바일 장치에서 사용자의 홈 화면에 영향을 줍니다.

그러나 HTML Workspace의 변경 사항은 AEM Forms 서버에 로그인한 모든 AEM Forms 앱 사용자에게 영향을 줍니다.
