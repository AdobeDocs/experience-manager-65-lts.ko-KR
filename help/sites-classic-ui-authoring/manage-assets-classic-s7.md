---
title: 페이지에 Dynamic Media Classic(Scene7) 기능 추가
description: Adobe Dynamic Media Classic(Scene7)은 리치 미디어 자산을 웹, 모바일, 이메일 및 인터넷에 연결된 디스플레이와 인쇄를 관리, 개선, 게시 및 전달하기 위한 호스팅 솔루션입니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: e452c343-3bba-4774-b153-c5ba05f24362
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '3545'
ht-degree: 12%

---

# 페이지에 Dynamic Media Classic(Scene7) 기능 추가{#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic(Scene7)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html?lang=ko)은(는) 리치 미디어 자산을 웹, 모바일, 이메일 및 인터넷에 연결된 디스플레이와 인쇄로 관리, 개선, 게시 및 전달하기 위한 호스팅 솔루션입니다.

Dynamic Media Classic(Scene7)에 게시된 Experience Manager 에셋을 다양한 뷰어에서 볼 수 있습니다.

* 확대/축소
* 플라이아웃
* 비디오
* 이미지 템플릿
* 이미지

디지털 에셋을 Experience Manager에서 Dynamic Media Classic(Scene7)로 직접 게시하고 디지털 에셋을 Dynamic Media Classic(Scene7)에서 Experience Manager으로 게시할 수 있습니다.

이 문서에서는 Experience Manager에서 Dynamic Media Classic(Scene7)로 디지털 자산을 게시하는 방법을 설명하며, 그 반대도 마찬가지입니다. 또한 뷰어에 대한 자세한 설명이 제공됩니다. Dynamic Media Classic(Scene7)용 Experience Manager 구성에 대한 자세한 내용은 [Experience Manager과 Dynamic Media Classic(Scene7) 통합](/help/sites-administering/scene7.md)을 참조하십시오.

[이미지 맵 추가](/help/assets/image-maps.md)도 참조하세요.

Experience Manager에서 비디오 구성 요소를 사용하는 방법에 대한 자세한 내용은 다음을 참조하십시오.

* [비디오](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>Dynamic Media Classic(Scene7) 자산이 제대로 표시되지 않으면 Dynamic Media가 [비활성화됨](/help/assets/config-dynamic.md#disabling-dynamic-media)인지 확인한 후 페이지를 새로 고치십시오.

## Assets에서 Dynamic Media Classic(Scene7)에 수동으로 게시 {#manually-publishing-to-scene-from-assets}

클래식 UI의 Assets 콘솔에서 또는 자산에서 직접 Dynamic Media Classic(Scene7)에 디지털 자산을 게시할 수 있습니다.

>[!NOTE]
>
>Experience Manager은 비동기적으로 Dynamic Media Classic(Scene7)에 게시합니다. **[!UICONTROL 게시]**&#x200B;를 선택한 후 자산이 Dynamic Media Classic(Scene7)에 게시되는 데 몇 초 정도 걸릴 수 있습니다.
>

### Assets 콘솔에서 게시 {#publishing-from-the-assets-console}

자산이 Dynamic Media Classic(Scene7) 대상 폴더에 있는 경우 Assets 콘솔에서 Dynamic Media Classic(Scene7)에 게시할 수 있습니다.

1. Experience Manager 클래식 UI에서 **[!UICONTROL 디지털 Assets]**&#x200B;를 선택하여 디지털 에셋 관리자에 액세스합니다.

1. Dynamic Media Classic(Scene7)에 게시할 대상 폴더 내에서 자산 또는 폴더를 선택하고 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL Dynamic Media Classic(Scene7)에 게시]**&#x200B;를 선택합니다. 또는 **[!UICONTROL 도구]** 메뉴에서 **[!UICONTROL Dynamic Media Classic(Scene7)에 게시]**&#x200B;를 선택할 수 있습니다.

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. Dynamic Media Classic(Scene7)로 이동하여 자산을 사용할 수 있는지 확인합니다.

   >[!NOTE]
   >
   >자산이 Dynamic Media Classic(Scene7) 동기화 폴더에 없는 경우 두 메뉴의 **[!UICONTROL Dynamic Media Classic(Scene7)에 게시]**&#x200B;이 표시되지만 비활성화됩니다.

### 에셋에서 게시 {#publishing-from-an-asset}

자산이 동기화된 Dynamic Media Classic(Scene7) 폴더 내에 있는 한, 자산을 수동으로 게시할 수 있습니다.

>[!NOTE]
>
>자산이 Dynamic Media Classic(Scene7) 동기화 폴더에 없는 경우 **[!UICONTROL Dynamic Media Classic(Scene7)에 게시]**&#x200B;에 대한 링크가 나타나지 않습니다.

디지털 자산에서 직접 Dynamic Media Classic(Scene7)에 게시하려면 다음을 수행하십시오.

1. Experience Manager에서 **[!UICONTROL 디지털 Assets]**&#x200B;을(를) 선택하여 디지털 에셋 관리자에 액세스합니다.

1. 자산을 두 번 클릭하여 엽니다.

1. 자산 세부 정보 창에서 **[!UICONTROL Dynamic Media Classic(Scene7)에 게시]**&#x200B;를 선택합니다.

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. 링크가 **[!UICONTROL 게시 중...]**, **[!UICONTROL 게시됨]**(으)로 변경됩니다. Dynamic Media Classic(Scene7)로 이동하여 자산을 사용할 수 있는지 확인합니다.

   >[!NOTE]
   >
   >자산이 Dynamic Media Classic(Scene7)에 제대로 게시되지 않으면 링크가 **[!UICONTROL 게시 실패]**(으)로 변경됩니다. 자산이 이미 Dynamic Media Classic(Scene7)에 게시되어 있으면 링크는 **[!UICONTROL Dynamic Media Classic(Scene7)에 다시 게시]**&#x200B;를 읽습니다. 다시 게시를 사용하면 Experience Manager에서 자산을 변경하고 다시 게시할 수 있습니다.

### CQ 대상 폴더 외부에서 자산 게시 {#publishing-assets-from-outside-the-cq-target-folder}

Adobe에서는 Dynamic Media Classic(Scene7) 대상 폴더 내의 자산에서만 Dynamic Media Classic(Scene7)에 자산을 게시할 것을 권장합니다. 그러나 대상 폴더 외부의 폴더에서 자산을 업로드해야 하는 경우에도 Dynamic Media Classic(Scene7)의 온디맨드 폴더로 업로드하여 이 작업을 수행할 수 있습니다. 먼저 자산을 표시할 페이지에 대한 클라우드 구성을 구성합니다. 그런 다음 Dynamic Media Classic(Scene7) 구성 요소를 페이지에 추가하고 자산을 구성 요소에 끌어다 놓습니다. 페이지 속성이 해당 페이지에 대해 설정되면 선택 시 Dynamic Media Classic(Scene7)에 대한 업로드를 트리거하는 **[!UICONTROL Dynamic Media Classic에 게시]** 링크가 나타납니다.

>[!NOTE]
>
>온디맨드 폴더에 있는 Assets은 Dynamic Media Classic(Scene7) 컨텐츠 브라우저에 표시되지 않습니다.

**CQ 대상 폴더 외부에서 자산을 게시하려면:**

1. 클래식 UI의 Experience Manager에서 **[!UICONTROL 웹 사이트]**&#x200B;를 선택하고 아직 Dynamic Media Classic(Scene7)에 게시되지 않은 디지털 에셋을 추가할 웹 페이지로 이동합니다. (일반 페이지 상속 규칙이 적용됩니다.)

1. 사이드 킥에서 **[!UICONTROL 페이지]** 아이콘을 선택하고 **[!UICONTROL 페이지 속성]**&#x200B;을 선택합니다.

1. **[!UICONTROL 클라우드 서비스]**&#x200B;를 선택하십시오.
1. **[!UICONTROL 서비스 추가]**&#x200B;를 선택합니다.
1. **[!UICONTROL Dynamic Media Classic(Scene7)]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL Adobe Dynamic Media Classic(Scene7)]** 드롭다운 목록에서 원하는 구성을 선택하고 **[!UICONTROL 확인]**&#x200B;을 선택합니다.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 웹 페이지에서 Dynamic Media Classic(Scene7) 구성 요소를 페이지의 원하는 위치에 추가합니다.
1. 콘텐츠 파인더에서 디지털 에셋을 구성 요소로 드래그합니다. **[!UICONTROL Dynamic Media Classic(Scene7) 게시 상태 확인]**&#x200B;에 대한 링크가 표시됩니다.

   >[!NOTE]
   >
   >디지털 자산이 CQ 대상 폴더에 있으면 **[!UICONTROL Dynamic Media Classic(Scene7) 게시 상태 확인]**&#x200B;에 대한 링크가 나타나지 않습니다. 자산이 구성 요소에 배치됩니다.

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. **[!UICONTROL Dynamic Media Classic(Scene7) 게시 상태 확인]**&#x200B;을 선택합니다. 자산이 게시되지 않은 경우 Experience Manager은 해당 자산을 Dynamic Media Classic(Scene7)에 게시합니다. 업로드된 자산은 온디맨드 폴더에서 찾을 수 있습니다. 기본적으로 온디맨드 폴더는 **[!UICONTROL name_of_the_company/CQ5_adhoc]**&#x200B;에 있습니다. 필요한 경우 [온디맨드 폴더를 구성](#configuringtheadhocfolder)할 수 있습니다.

   >[!NOTE]
   >
   >자산이 Dynamic Media Classic(Scene7) 동기화 폴더에 없고 현재 페이지와 연결된 Dynamic Media Classic(Scene7) 클라우드 구성이 없는 경우 업로드가 실패합니다.

## Dynamic Media Classic(Scene7) 구성 요소 {#scene-components}

Experience Manager에서 사용할 수 있는 Dynamic Media Classic(Scene7) 구성 요소는 다음과 같습니다.

* 확대/축소
* 플라이아웃(확대/축소)
* 이미지 템플릿
* 이미지
* 비디오

>[!NOTE]
>
>이러한 구성 요소는 기본적으로 사용할 수 없으며 사용하기 전에 디자인 모드에서 선택해야 합니다.

디자인 모드에서 사용할 수 있게 되면 다른 Experience Manager 구성 요소처럼 페이지에 구성 요소를 추가할 수 있습니다. Dynamic Media Classic(Scene7)에 아직 게시되지 않은 Assets은 동기화된 폴더 또는 페이지나 Dynamic Media Classic(Scene7) 클라우드 구성을 통해 Dynamic Media Classic(Scene7)에 게시됩니다.

>[!NOTE]
>
>사용자 지정 S7 뷰어를 만들고 개발하면서 콘텐츠 파인더를 사용하는 경우 `allowfullscreen` 매개 변수를 명시적으로 추가해야 합니다.

### Flash 뷰어 지원 중단 알림 {#flash-viewers-end-of-life-notice}

2017년 1월 31일부터 Adobe Dynamic Media Classic(Scene7)는 공식적으로 Flash 뷰어 플랫폼에 대한 지원을 중단했습니다.

### 페이지에 Dynamic Media Classic(Scene7) 구성 요소 추가 {#adding-a-scene-component-to-a-page}

페이지에 Dynamic Media Classic(Scene7) 구성 요소를 추가하는 것은 페이지에 구성 요소를 추가하는 것과 같습니다. Dynamic Media Classic(Scene7) 구성 요소는 다음 섹션에 자세히 설명되어 있습니다.

클래식 UI의 페이지에 Dynamic Media Classic(Scene7) 구성 요소/뷰어를 추가하려면 다음을 수행하십시오.

1. Experience Manager에서 Dynamic Media Classic(Scene7) 구성 요소를 추가할 페이지를 엽니다.

1. 사용 가능한 Dynamic Media Classic(Scene7) 구성 요소가 없는 경우 사이드 킥에서 눈금자를 선택하여 **디자인** 모드를 시작하고 **[!UICONTROL 편집]** parsys를 선택한 다음, 모든 **[!UICONTROL Dynamic Media Classic(Scene7)]** 구성 요소를 선택하여 사용 가능하게 만드십시오.

1. 사이드 킥에서 연필을 선택하여 **편집** 모드로 돌아갑니다.

1. 사이드 킥의 **[!UICONTROL Dynamic Media Classic(Scene7)]** 그룹에서 원하는 위치의 페이지로 구성 요소를 끌어옵니다.

1. 구성 요소를 열 수 있도록 ***[!UICONTROL 편집]**&#x200B;을 선택합니다.

1. 필요에 따라 구성 요소를 편집하고 **[!UICONTROL 확인]**&#x200B;을 선택하여 변경 내용을 저장합니다.

### 반응형 웹 사이트에 대화형 보기 환경 추가 {#adding-interactive-viewing-experiences-to-a-responsive-website}

에셋에 대한 응답형 디자인은 에셋이 표시되는 위치에 따라 조정됨을 의미합니다. 반응형 디자인을 통해 동일한 에셋을 여러 디바이스에 효과적으로 표시할 수 있습니다.

클래식 UI에서 응답형 사이트에 대화형 보기 환경을 추가하려면:

1. Experience Manager에 로그인하고 [구성된 Adobe Dynamic Media Classic(Scene7) 클라우드 서비스](/help/sites-administering/scene7.md#configuring-scene-integration)가 있으며 Dynamic Media Classic(Scene7) 구성 요소를 사용할 수 있는지 확인하십시오.

   >[!NOTE]
   >
   >Dynamic Media Classic(Scene7) WCM 구성 요소를 사용할 수 없는 경우 디자인 모드를 통해 활성화해야 합니다.

1. Dynamic Media Classic(Scene7) 구성 요소가 활성화된 웹 사이트에서 **[!UICONTROL 이미지]** 뷰어를 페이지로 드래그합니다.
1. **[!UICONTROL Dynamic Media Classic(Scene7) 설정]** 탭에서 구성 요소를 편집하고 중단점을 조정하십시오.

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. 뷰어의 크기가 응답적으로 조정되는지 확인하고 모든 상호 작용이 데스크탑, 태블릿 및 모바일에 최적화되어 있는지 확인합니다.

### 모든 Dynamic Media Classic(Scene7) 구성 요소에 공통되는 설정 {#settings-common-to-all-scene-components}

구성 옵션은 다르지만 모든 Dynamic Media Classic(Scene7) 구성 요소에는 다음과 같은 공통점이 있습니다.

* **파일 참조** - 참조할 파일을 찾아 봅니다. 파일 참조는 자산 URL을 보여주며 URL 명령 및 매개 변수를 포함하는 전체 Dynamic Media Classic(Scene7) URL일 필요는 없습니다. 이 필드에는 Dynamic Media Classic(Scene7) URL 명령과 매개 변수를 추가할 수 없습니다. 대신 구성 요소에서 해당 기능을 통해 추가해야 합니다.
* **너비** - 너비를 설정할 수 있습니다.
* **높이** - 높이를 설정할 수 있습니다.

이러한 구성 옵션은 Dynamic Media Classic(Scene7) 구성 요소(예: **Zoom** 구성 요소를 열 때 두 번 클릭)를 통해 설정합니다.

![chlimage_1-52](assets/chlimage_1-52.png)

### 확대/축소 {#zoom}

HTML5 확대/축소 구성 요소가 더 큰 이미지를 표시하려면 + 단추를 누릅니다.

에셋 하단에는 확대/축소 도구가 있습니다. 확대하려면 **[!UICONTROL +]**&#x200B;을(를) 선택하십시오. 줄이려면 **[!UICONTROL -]**&#x200B;을(를) 선택하십시오. **[!UICONTROL x]** 또는 확대/축소 재설정 화살표를 선택하면 이미지가 가져온 원래 크기로 돌아갑니다. 전체 화면으로 만들 수 있도록 대각선 화살표를 선택합니다. 구성 요소를 구성할 수 있도록 **[!UICONTROL 편집]**&#x200B;을 선택하십시오. 이 구성 요소를 사용하여 [모든 Dynamic Media Classic(Scene7) 구성 요소에 공통되는 설정](#settings-common-to-all-scene-components)을 구성할 수 있습니다.

![HTML5 확대/축소 구성 요소 내부의 튤립 꽃 이미지](do-not-localize/chlimage_1-3.png)

### 플라이아웃 {#flyout}

HTML5 플라이아웃 구성 요소에서 자산은 분할 화면으로 표시됩니다. 왼쪽에는 지정된 크기의 자산이 표시되고, 오른쪽에는 확대/축소 부분이 표시됩니다. 구성 요소를 구성할 수 있도록 **[!UICONTROL 편집]**&#x200B;을 선택하십시오. 이 구성 요소를 사용하여 [모든 Dynamic Media Classic(Scene7) 구성 요소에 공통되는 설정](/help/sites-administering/scene7.md#settingscommontoallscene7components)을 구성할 수 있습니다.

>[!NOTE]
>
>플라이아웃 구성 요소가 사용자 지정 크기를 사용하는 경우 해당 사용자 지정 크기가 사용되고 구성 요소의 응답형 설정이 비활성화됩니다.
>
>플라이아웃 구성 요소가 기본 크기를 사용하는 경우, 디자인 보기에서 설정된 대로 기본 크기가 사용됩니다. 구성 요소는 구성 요소의 응답형 설정이 활성화되면 페이지 레이아웃 크기에 맞게 확장됩니다. 그러나 구성 요소의 응답형 설정에는 제한이 있습니다. 응답형 설정이 있는 플라이아웃 구성 요소를 사용하는 경우 전체 페이지 늘리기를 함께 사용하면 안 됩니다. 그러지 않으면, 플라이아웃이 확장되어 페이지의 오른쪽 테두리를 넘어갈 수 있습니다.

![chlimage_1-53](assets/chlimage_1-53.png)

### 이미지 {#image}

Dynamic Media Classic(Scene7) 이미지 구성 요소를 사용하여 Dynamic Media Classic(Scene7) 수정자, 이미지 또는 뷰어 사전 설정, 선명하게 하기 등의 Dynamic Media Classic(Scene7) 기능을 이미지에 추가할 수 있습니다. Dynamic Media Classic(Scene7) 이미지 구성 요소는 특별한 Dynamic Media Classic(Scene7) 기능이 있는 Experience Manager의 다른 이미지 구성 요소와 유사합니다. 이 예의 이미지에는 Dynamic Media Classic(Scene7) URL 수정자 `&op_invert=1`이(가) 적용되어 있습니다.

![Dynamic Media Classic(Scene 7) 이미지 구성 요소 내부의 구 이미지](do-not-localize/chlimage_1-4.png)

**제목, 대체 텍스트** - 고급 탭에서 이미지에 제목을 추가하고, 그래픽을 해제한 사용자를 위한 대체 텍스트를 추가합니다.

**URL, 여는 위치** - 링크를 열 자산을 설정할 수 있습니다. URL을 설정하고 여는 위치에 같은 창에서 열지 또는 새 창에서 열지를 지정합니다.

![chlimage_1-54](assets/chlimage_1-54.png)

**뷰어 사전 설정** - 드롭다운 메뉴에서 기존 뷰어 사전 설정을 선택합니다. 보려는 뷰어 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 합니다. 뷰어 사전 설정 관리를 참조하십시오. 이미지 사전 설정을 사용 중이고 이와 반대로 뷰어 사전 설정을 선택할 수 없습니다.

**Dynamic Media Classic(Scene7) 구성** - SPS에서 활성 이미지 사전 설정을 가져오는 데 사용할 Dynamic Media Classic(Scene7) 구성을 선택합니다.

**이미지 사전 설정** - 드롭다운 메뉴에서 기존 이미지 사전 설정을 선택합니다. 보려는 이미지 사전 설정이 표시되지 않을 경우 표시되도록 설정해야 합니다. 이미지 사전 설정 관리를 참조하십시오. 이미지 사전 설정을 사용 중이고 이와 반대로 뷰어 사전 설정을 선택할 수 없습니다.

**출력 형식** - 이미지의 출력 형식(예: jpeg)을 선택하십시오. 선택한 출력 형식에 따라 추가 구성 옵션이 있을 수 있습니다. 이미지 사전 설정 우수 사례를 참조하십시오.

**선명하게 하기** - 이미지를 선명하게 할 방법을 선택합니다. 선명하게 하기는 이미지 사전 설정 우수 사례 및 선명하게 하기 우수 사례에 자세히 설명되어 있습니다.

**URL 수정자** - 추가 S7 이미지 명령을 제공하여 이미지 효과를 변경할 수 있습니다. 이러한 명령은 이미지 사전 설정 및 명령 참조에 설명되어 있습니다.

**중단점** - 웹 사이트가 응답형인 경우 중단점을 조정할 수 있습니다. 중단점은 쉼표(,)로 구분해야 합니다.

### 이미지 템플릿 {#image-template}

Dynamic Media Classic(Scene7) 이미지 템플릿은 Dynamic Media Classic(Scene7)로 가져온 계층화된 Photoshop 컨텐츠입니다. 여기서 컨텐츠 및 속성은 가변성을 위해 매개 변수화됩니다. **[!UICONTROL 이미지 템플릿]** 구성 요소를 사용하여 이미지를 가져오고 Experience Manager에서 텍스트를 동적으로 변경할 수 있습니다. 또한 클라이언트 컨텍스트의 값을 사용하도록 **[!UICONTROL 이미지 템플릿]** 구성 요소를 구성할 수 있으므로 각 사용자는 개인화된 방식으로 이미지를 경험하게 됩니다.

구성 요소를 구성하려면 **[!UICONTROL 편집]** - 을 선택합니다. 모든 Dynamic Media Classic(Scene7) 구성 요소에 공통되는 [설정](/help/sites-administering/scene7.md#settingscommontoallscene7components) 및 이 섹션에서 설명하는 기타 설정을 구성할 수 있습니다.

![chlimage_1-55](assets/chlimage_1-55.png)

**파일 참조, 너비, 높이** - [모든 Dynamic Media Classic(Scene7) 구성 요소에 공통인 설정](/help/sites-administering/scene7.md#settingscommontoallscene7components)을 참조하십시오.

>[!NOTE]
>
>Dynamic Media Classic(Scene7) URL 명령 및 매개 변수를 파일 참조 URL에 바로 추가할 수 없습니다. **[!UICONTROL 매개 변수]** 패널의 구성 요소 UI에서만 정의할 수 있습니다.

**제목, 대체 텍스트** - Dynamic Media Classic(Scene7) 이미지 템플릿 탭에서 이미지에 제목을 추가하고, 그래픽을 해제한 사용자를 위한 대체 텍스트를 추가합니다.

**URL, 여는 위치** - 링크를 열 자산을 설정할 수 있습니다. URL을 설정하고 여는 위치에 같은 창에서 열지 또는 새 창에서 열지를 지정합니다.

![chlimage_1-56](assets/chlimage_1-56.png)

**매개 변수 패널** - 이미지를 가져올 때 매개 변수는 이미지의 정보로 미리 채워집니다. 동적으로 변경할 수 있는 컨텐츠가 없는 경우 이 창은 비어 있습니다.

![chlimage_1-57](assets/chlimage_1-57.png)

#### 동적으로 텍스트 변경 {#changing-text-dynamically}

텍스트를 동적으로 변경하려면 필드에 새 텍스트를 입력하고 **[!UICONTROL 확인]**&#x200B;을 선택합니다. 이 예제에서 **가격**&#x200B;은 이제 $50이고 배송은 99센트입니다.

![chlimage_1-58](assets/chlimage_1-58.png)

이미지의 텍스트가 변경됩니다. 필드 옆에 있는 **[!UICONTROL 재설정]**&#x200B;을 선택하여 텍스트를 원래 값으로 다시 설정할 수 있습니다.

![chlimage_1-59](assets/chlimage_1-59.png)

#### 클라이언트 컨텍스트 값을 반영하도록 텍스트 변경 {#changing-text-to-reflect-the-value-of-a-client-context-value}

필드를 클라이언트 컨텍스트 값에 연결하려면 **[!UICONTROL 선택]**&#x200B;을 선택하여 클라이언트 컨텍스트 메뉴를 열고 클라이언트 컨텍스트를 선택한 후 **[!UICONTROL 확인]**&#x200B;을 선택합니다. 이 예제에서 이름은 프로필의 형식이 지정된 이름과 연결되어 변경됩니다.

![chlimage_1-60](assets/chlimage_1-60.png)

텍스트는 현재 로그인한 사용자의 이름을 반영합니다. 필드 옆에 있는 **[!UICONTROL 재설정]**&#x200B;을 선택하여 텍스트를 원래 값으로 다시 설정할 수 있습니다.

![chlimage_1-61](assets/chlimage_1-61.png)

#### Dynamic Media Classic(Scene7) 이미지 템플릿을 링크로 지정 {#making-the-scene-image-template-a-link}

Dynamic Media Classic(Scene7) 이미지 템플릿 구성 요소를 클릭 가능한 링크로 만들 수 있습니다.

1. Dynamic Media Classic(Scene7) 이미지 템플릿 구성 요소가 있는 페이지에서 **[!UICONTROL 편집]**&#x200B;을 선택합니다.
1. **[!UICONTROL URL]** 필드에 이미지를 클릭할 때 사용자가 이동하는 URL을 입력합니다. **[!UICONTROL 여는 위치]** 필드에서 대상을 새 창 또는 동일한 창 중 어떤 창에서 열지를 선택합니다.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. **[!UICONTROL 확인]**&#x200B;을 선택합니다.

### 비디오 구성 요소 {#video-component}

Dynamic Media Classic(Scene7) **[!UICONTROL 비디오]** 구성 요소(사이드 킥의 Dynamic Media Classic(Scene7) 섹션에서 사용 가능)는 장치 및 대역폭 검색을 사용하여 각 화면에 올바른 비디오를 제공합니다. 이 구성 요소는 HTML5 비디오 플레이어로, 채널 간에 사용할 수 있는 단일 뷰어입니다.

응용 비디오 세트, 단일 MP4 비디오 또는 단일 F4V 비디오에 사용할 수 있습니다.

비디오가 Dynamic Media Classic(Scene7) 통합에 따라 작동하는 방식에 대한 자세한 내용은 [비디오](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)를 참조하십시오. 또한 [**Dynamic Media Classic(Scene7) 비디오** 구성 요소와 기본 **비디오** 구성 요소](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)를 비교한 결과도 참조하십시오.

![chlimage_1-63](assets/chlimage_1-63.png)

### 비디오 구성 요소의 알려진 제한 사항 {#known-limitations-for-the-video-component}

Adobe DAM 및 WCM은 기본 소스 비디오가 업로드되었는지 보여 줍니다. 이러한 프록시 자산은 표시되지 않습니다.

* Dynamic Media Classic(Scene7) 인코딩 표현물
* Dynamic Media Classic(Scene7) 응용 비디오 세트

Dynamic Media Classic(Scene7) 비디오 구성 요소와 함께 응용 비디오 세트를 사용할 때는 비디오 크기에 맞게 구성 요소의 크기를 조정해야 합니다.

## Dynamic Media Classic(Scene7) 컨텐츠 브라우저 {#scene-content-browser}

Dynamic Media Classic(Scene7) 컨텐츠 브라우저를 사용하면 Dynamic Media Classic(Scene7)의 컨텐츠를 Experience Manager에서 바로 볼 수 있습니다. 컨텐츠 브라우저에 액세스하려면 컨텐츠 파인더의 터치 최적화 사용자 인터페이스에서 **Dynamic Media Classic(Scene7)**&#x200B;을(를) 선택하거나, 클래식 사용자 인터페이스에서 **S7** 아이콘을 선택하십시오. 기능은 두 사용자 인터페이스 간에 동일합니다.

구성이 여러 개인 경우 기본적으로 Experience Manager은 [기본 구성](/help/sites-administering/scene7.md#configuring-a-default-configuration)을 표시합니다. 드롭다운 메뉴의 Dynamic Media Classic(Scene7) 컨텐츠 브라우저에서 직접 다른 구성을 선택할 수 있습니다.

>[!NOTE]
>
>* 온디맨드 폴더의 Assets이 Dynamic Media Classic(Scene7) 컨텐츠 브라우저에 표시되지 않습니다.
>* [보안 미리 보기가 활성화된 경우](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) Dynamic Media Classic(Scene7)에 게시된 자산과 게시되지 않은 자산이 모두 Dynamic Media Classic(Scene7) 콘텐츠 브라우저에 나타나지 않습니다.
>* **[!UICONTROL Dynamic Media Classic(Scene7)]** 또는 **[!UICONTROL S7]** 아이콘이 컨텐츠 브라우저에 옵션으로 표시되지 않는 경우 [Experience Manager에서 작동하도록 Dynamic Media Classic(Scene7)을 구성](/help/sites-administering/scene7.md)해야 합니다.
>* 비디오의 경우 Dynamic Media Classic(Scene7) 컨텐츠 브라우저는 다음을 지원합니다.
>   * 응용 비디오 세트: 여러 화면 간에 원활하게 재생되는 데 필요한 모든 비디오 표현물의 컨테이너
>   * 단일 MP4 비디오
>   * 단일 F4V 동영상

### 콘텐츠 찾아보기 {#browsing-content-in-the-classic-ui}

**[!UICONTROL S7]** 탭을 선택하여 Dynamic Media Classic(Scene7)에서 콘텐츠를 찾아봅니다.

구성을 선택하여 액세스 중인 구성을 변경할 수 있습니다. 폴더는 선택한 구성에 따라 변경됩니다.

![chlimage_1-64](assets/chlimage_1-64.png)

Assets용 컨텐츠 파인더와 마찬가지로 자산을 검색하고 결과를 필터링할 수 있습니다. 그러나 Assets 파인더와 달리 **S7** 탭에 키워드를 입력하면 파일 이름 **은(는) 파일 이름에 키워드를**&#x200B;포함&#x200B;**하는 대신 입력한 문자열로 시작**&#x200B;합니다.

기본적으로 에셋은 파일 이름별로 표시됩니다. 그러나 결과를 에셋 유형별로 필터링할 수도 있습니다.

>[!NOTE]
>
>비디오의 경우 WCM의 Dynamic Media Classic(Scene7) 컨텐츠 브라우저는 다음을 지원합니다.
>
>* 응용 비디오 세트: 여러 화면 간에 원활하게 재생되는 데 필요한 모든 비디오 표현물의 컨테이너
>* 단일 MP4 비디오
>* 단일 F4V 동영상
>

### 컨텐츠 브라우저로 Dynamic Media Classic(Scene7) 자산 검색 {#searching-for-scene-assets-with-the-content-browser}

Dynamic Media Classic(Scene7) 에셋을 검색하는 것은 Experience Manager 에셋 검색과 유사합니다. 단, 검색할 때 자산을 Experience Manager으로 직접 가져오는 대신 Dynamic Media Classic(Scene7) 시스템에서 자산의 원격 보기가 실제로 표시됩니다.

클래식 UI 또는 터치에 적합한 UI를 사용하여 에셋을 보고 검색할 수 있습니다. 인터페이스에 따라 검색 방법이 약간 다릅니다.

UI에서 검색할 때 다음 기준(터치에 적합한 UI에서 여기에 표시됨)에 따라 필터링할 수 있습니다.

**키워드 입력** - 이름별로 자산을 검색할 수 있습니다. 키워드를 검색할 때 파일 이름의 시작 문자를 입력합니다. 예를 들어 &quot;swimming&quot;이라는 단어를 입력하면 해당 문자로 시작하는 모든 에셋 파일 이름을 해당 순서로 찾습니다. 자산을 찾을 용어를 입력한 후 `Enter`을(를) 선택하십시오.

![chlimage_1-65](assets/chlimage_1-65.png)

**폴더/경로** - 폴더 이름은 선택한 구성을 기반으로 합니다. 폴더 아이콘을 선택하고 하위 폴더를 선택한 다음 선택 표시를 선택하여 하위 레벨로 드릴다운할 수 있습니다.

키워드를 입력하고 폴더를 선택하면 Experience Manager은 해당 폴더 및 하위 폴더를 검색합니다. 그러나 검색할 때 키워드를 입력하지 않으면 폴더를 선택하면 해당 폴더의 자산만 표시되고 하위 폴더는 포함되지 않습니다.

기본적으로 Experience Manager은 선택한 폴더 및 모든 하위 폴더를 검색합니다.

![chlimage_1-66](assets/chlimage_1-66.png)

**에셋 유형** - Dynamic Media Classic(Scene7) 콘텐츠를 찾아보려면 Dynamic Media Classic(Scene7)을 선택합니다. 이 옵션은 Dynamic Media Classic(Scene7)이 구성된 경우에만 사용할 수 있습니다.

![chlimage_1-67](assets/chlimage_1-67.png)

**구성** - 클라우드 서비스에 둘 이상의 Dynamic Media Classic(Scene7) 구성이 정의되어 있는 경우 여기에서 선택할 수 있습니다. 따라서 폴더는 선택한 구성에 따라 변경됩니다.

![chlimage_1-68](assets/chlimage_1-68.png)

**자산 유형** - Dynamic Media Classic(Scene7) 브라우저 내에서, 이미지, 템플릿, 비디오 및 응용 비디오 세트 중 하나를 포함하도록 결과를 필터링할 수 있습니다. 자산 유형을 선택하지 않으면 기본적으로 Experience Manager은 모든 자산 유형을 검색합니다.

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* 클래식 UI에서는 **Flash** 및 **FXG**&#x200B;도 검색할 수 있습니다. 터치에 적합한 UI에서 이 두 용어에 대한 필터링은 지원되지 않습니다.
>
>* 비디오를 검색할 때 단일 렌디션을 검색합니다. 원본 렌디션(&#42;.mp4만) 및 인코딩된 렌디션을 반환합니다.
>* 응용 비디오 세트를 검색할 때 폴더 및 모든 하위 폴더를 검색하게 되지만, 검색에 키워드를 추가한 경우에만 해당됩니다. 키워드를 추가하지 않은 경우 Experience Manager이 하위 폴더를 검색하지 않습니다.
>

**게시 상태** - 게시 상태(게시 취소됨 또는 게시됨)에 따라 자산을 필터링할 수 있습니다. 게시 상태를 선택하지 않으면 기본적으로 Experience Manager은 모든 게시 상태를 검색합니다.

![chlimage_1-70](assets/chlimage_1-70.png)
