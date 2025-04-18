---
title: Adobe Campaign 타기팅
description: 세그먼테이션을 설정한 후 Adobe Campaign에 대한 타겟팅된 경험을 만들 수 있습니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
exl-id: ce6ebfff-3a1d-4c9f-aa50-23d1c3afc852
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 1%

---

# Adobe Campaign 타기팅{#targeting-your-adobe-campaign}

Adobe Campaign 뉴스레터를 타겟팅하려면 먼저 Classic UI에서만 사용할 수 있는 세그먼테이션을 설정해야 합니다(클라이언트 컨텍스트용). 그런 다음 Adobe Campaign에 대한 타겟팅된 경험을 만들 수 있습니다. 두 가지 모두 이 섹션에 설명되어 있습니다.

## AEM에서 세그먼테이션 설정 {#setting-up-segmentation-in-aem}

세그먼테이션을 설정하려면 클래식 UI를 사용하여 세그먼트를 설정해야 합니다. 나머지 단계는 표준 UI에서 수행할 수 있습니다.

세그먼테이션 설정에는 세그먼트, 브랜드, 캠페인 및 경험 만들기가 포함됩니다.

>[!NOTE]
>
>세그먼트 ID는 Adobe Campaign 측의 세그먼트 ID에 매핑해야 합니다.

### 세그먼트 만들기 {#creating-segments}

세그먼트를 만들려면 다음 작업을 수행하십시오.

1. **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**&#x200B;에서 [세그먼테이션 콘솔](http://localhost:4502/miscadmin#/etc/segmentation)을 엽니다.
1. 페이지를 만들고 제목(예: **AC 세그먼트**)을 입력한 다음 **세그먼트(Adobe Campaign)** 템플릿을 선택합니다.
1. 왼쪽의 트리 보기에서 만든 페이지를 선택합니다.
1. 만든 세그먼트 아래에 Male이라는 페이지를 만들어 남성 사용자를 타깃팅하는 등의 방법으로 세그먼트를 만들고 **세그먼트(Adobe Campaign)** 템플릿을 선택합니다.
1. 만든 세그먼트 페이지를 열고 **세그먼트 ID**&#x200B;를 사이드 킥에서 페이지로 끌어다 놓습니다.
1. 트레이트를 두 번 클릭하고, 이 경우 Adobe Campaign에 정의된 남성 세그먼트를 나타내는 ID를 입력한 다음(예: **MALE**) **확인**&#x200B;을 클릭합니다. 다음 메시지가 표시됩니다. *`targetData.segmentCode == "MALE"`*
1. 다른 세그먼트(예: 여성 사용자를 타겟팅하는 세그먼트)에 대해 단계를 반복합니다.

### 브랜드 만들기 {#creating-a-brand}

브랜드를 만들려면:

1. **사이트**&#x200B;에서 **캠페인** 폴더(예: We.Retail)로 이동합니다.
1. **페이지 만들기**&#x200B;를 클릭하고 페이지 제목(예: We.Retail 브랜드)을 입력한 다음 **브랜드** 템플릿을 선택합니다.

### 캠페인 생성 {#creating-a-campaign}

캠페인을 만들려면 다음 작업을 수행하십시오.

1. 만든 **브랜드** 페이지를 엽니다.
1. **페이지 만들기**&#x200B;를 클릭하고 페이지 제목(예: We.Retail 캠페인)을 입력한 다음 **캠페인** 템플릿을 선택하고 **만들기**&#x200B;를 클릭합니다.

### 경험 만들기 {#creating-experiences}

세그먼트를 위한 경험을 만들려면 다음 작업을 수행하십시오.

1. 만든 **Campaign** 페이지를 엽니다.
1. **페이지 만들기**&#x200B;를 클릭하고 페이지의 제목(예: 남성 세그먼트에 대한 경험을 만들 때 남성)을 입력하여 세그먼트에 대한 경험을 만들고 **경험** 템플릿을 선택합니다.
1. 생성된 경험 페이지를 엽니다.
1. **편집**&#x200B;을 클릭한 다음 세그먼트 아래에서 **항목 추가**&#x200B;를 클릭합니다.
1. 남성 세그먼트의 경로(예: **/etc/segmentation/ac-segments/male**)를 입력하고 **확인**&#x200B;을 클릭합니다. 다음 메시지가 표시되어야 합니다. *경험이 타깃팅됨: 남성*
1. 모든 세그먼트(예: 여성 타겟)에 대한 경험을 만들려면 이전 단계를 반복하십시오.

## 타겟팅된 콘텐츠로 뉴스레터 만들기 {#creating-a-newsletter-with-targeted-content}

세그먼트, 브랜드, 캠페인 및 경험을 만든 후에는 타겟팅된 콘텐츠로 뉴스레터를 만들 수 있습니다. 경험을 만든 후에는 경험을 세그먼트에 연결합니다.

>[!NOTE]
>
>[전자 메일 샘플은 Geometrixx에서만 사용할 수 있습니다](/help/sites-developing/we-retail.md). 패키지 공유에서 샘플 Geometrixx 콘텐츠를 다운로드합니다.

타겟팅된 콘텐츠로 뉴스레터를 만들려면 다음 작업을 수행하십시오.

1. 타겟팅된 콘텐츠로 뉴스레터 만들기: Geometrixx Outdoors의 이메일 캠페인 아래에서 **만들기** > **페이지**&#x200B;를 클릭하고 Adobe Campaign 메일 템플릿 중 하나를 선택하십시오.

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 뉴스레터에서 텍스트 및 Personalization 구성 요소를 추가합니다.
1. 텍스트 및 Personalization 구성 요소에 &quot;기본값입니다.&quot;와 같은 텍스트를 추가합니다.
1. **편집** 옆에 있는 화살표를 클릭하고 **타깃팅**&#x200B;을 선택합니다.
1. 브랜드 드롭다운 메뉴에서 브랜드를 선택하고 캠페인을 선택합니다. (이전에 만든 브랜드 및 캠페인입니다.)
1. **타깃팅 시작**&#x200B;을 클릭합니다. 세그먼트가 대상자 영역에 표시되는 것을 볼 수 있습니다. 정의된 세그먼트 중 어느 하나도 일치하지 않는 경우 기본 경험이 사용됩니다.

   >[!NOTE]
   >
   >기본적으로 AEM에 포함된 이메일 샘플은 Adobe Campaign을 타겟팅 엔진으로 사용합니다. 사용자 지정 뉴스레터의 경우 타겟팅 엔진으로 Adobe Campaign을 선택해야 할 수 있습니다. 타깃팅할 때 도구 모음에서 +를 클릭하고 새 활동의 제목을 입력한 다음 타깃팅 엔진으로 **Adobe Campaign**&#x200B;을(를) 선택합니다.

1. **기본값**&#x200B;을 클릭한 다음 추가한 텍스트 및 Personalization 구성 요소를 클릭하면 화살표가 있는 별표가 표시됩니다. 아이콘을 클릭하여 이 구성 요소를 타겟팅합니다.

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. 다른 세그먼트(남성)로 이동한 다음 **오퍼 추가**&#x200B;를 클릭하고 더하기 아이콘 + 을 클릭합니다. 그런 다음 오퍼를 편집합니다.
1. 다른 세그먼트(여성)로 이동한 다음 **오퍼 추가** 및 더하기 아이콘 + 을 클릭합니다. 그런 다음 이 오퍼를 편집합니다.
1. 매핑을 보려면 **다음**&#x200B;을 클릭하고 Adobe Campaign에 적용되지 않는 설정을 보려면 **다음**&#x200B;을 클릭한 다음 **저장**&#x200B;을 클릭합니다.

   AEM은 콘텐츠가 Adobe Campaign 내의 게재에 사용될 때 Adobe Campaign에 대한 올바른 타깃팅 코드를 자동으로 생성합니다

1. Adobe Campaign에서 게재를 만듭니다. **AEM 콘텐츠가 포함된 전자 메일 게재**&#x200B;를 선택하고 로컬 AEM 계정을 적절하게 선택한 다음 변경 내용을 확인합니다.

   HTML 보기에서는 타깃팅된 구성 요소의 다른 경험이 Adobe Campaign 타깃팅 코드에 포함되어 있습니다.

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >Adobe Campaign에서도 세그먼트를 설정하는 경우 **미리 보기**&#x200B;를 클릭하면 각 세그먼트에 대한 경험이 표시됩니다.
