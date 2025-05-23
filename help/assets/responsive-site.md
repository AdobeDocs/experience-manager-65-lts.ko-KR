---
title: 응답형 사이트용으로 최적화된 이미지 제공
description: 반응형 코드 기능을 사용하여 최적화된 이미지를 전달하는 방법
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Asset Management
role: User, Admin
solution: Experience Manager, Experience Manager Assets
exl-id: 053efcc4-35dd-49c8-9645-ae29aa492352
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 13%

---

# 반응형 사이트에 최적화된 이미지 게재 {#delivering-optimized-images-for-a-responsive-site}

반응형 서비스용 코드를 웹 개발자와 공유하려면 반응형 코드 기능을 사용하십시오. 웹 개발자와 공유할 수 있도록 응답형(**[!UICONTROL RESS]**) 코드를 클립보드에 복사합니다.

이 기능은 웹 사이트가 타사 WCM에 있는 경우 사용하는 것이 적절합니다. 그러나 웹 사이트가 대신 Adobe Experience Manager에 있는 경우 오프사이트 이미지 서버가 이미지를 렌더링하여 웹 페이지에 제공합니다.

[웹 페이지에 비디오 뷰어 포함](embed-code.md)도 참조하세요.

[웹 응용 프로그램에 URL 연결](linking-urls-to-yourwebapplication.md)도 참조하세요.

**응답형 사이트에 최적화된 이미지를 전달하려면:**

1. 응답형 코드를 제공할 이미지로 이동한 다음 드롭다운 메뉴에서 **[!UICONTROL 표현물]**&#x200B;을 선택합니다.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Select a responsive image preset. The **[!UICONTROL URL]** and **[!UICONTROL RESS]** buttons appear.

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >The selected asset *and* the selected image preset or viewer preset must be published to make the **[!UICONTROL URL]** or **[!UICONTROL RESS]** buttons available.
   >
   >Dynamic Media - 하이브리드 모드에서는 이미지 사전 설정을 게시해야 합니다. Dynamic Media - Scene7 모드에서는 이미지 사전 설정을 자동으로 게시합니다.

1. **[!UICONTROL RESS]**&#x200B;을(를) 선택합니다.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. **[!UICONTROL 응답형 이미지 포함]** 대화 상자에서 선택한 후 응답형 코드 텍스트를 복사하여 웹 사이트에 붙여넣어 응답형 자산에 액세스합니다.
1. 포함 코드의 기본 중단점을 편집하여 응답형 웹 사이트의 중단점과 일치시키십시오(코드에서 직접). 또한 다양한 페이지 중단점에서 제공되는 다양한 이미지 해상도를 테스트합니다.

## HTTP/2를 사용하여 Dynamic Media 에셋 전달 {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2는 새로운 업데이트된 웹 프로토콜로서 브라우저와 서버의 통신 방식을 개선합니다. 정보 전송 속도를 높이고 필요한 처리 능력을 줄일 수 있습니다. Dynamic Media 에셋의 전달은 더 나은 응답 및 로드 시간을 제공하는 HTTP/2를 사용하여 지원됩니다.

Dynamic Media 계정으로 HTTP/2를 사용하는 방법에 대한 자세한 내용은 [HTTP2 컨텐츠 배달](http2.md)을 참조하십시오.
