---
title: Dynamic Media 이미지 사전 설정 적용
description: 에셋이 다른 크기, 다른 형식 또는 동적으로 생성된 다른 이미지 속성으로 이미지를 동적으로 게재할 수 있도록 하는 방법에 대해 알아봅니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Image Presets
role: User,Admin
solution: Experience Manager, Experience Manager Assets
exl-id: f4d3a5f1-9348-433f-9c9f-84075a7ab912
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 13%

---

# Dynamic Media 이미지 사전 설정 적용 {#applying-image-presets}

이미지 사전 설정을 사용하면 에셋이 다른 크기, 다른 형식 또는 동적으로 생성되는 다른 이미지 속성으로 이미지를 동적으로 전달할 수 있습니다. 이미지를 내보낼 때 사전 설정을 선택할 수 있습니다. 사전 설정은 관리자가 지정한 사양에 맞게 이미지 형식을 다시 지정합니다.

또한 응답형 이미지 사전 설정을 선택할 수 있습니다(선택한 후 **[!UICONTROL RESS]** 단추로 지정).

이 섹션에서는 이미지 사전 설정을 사용하는 방법에 대해 설명합니다. [관리자가 이미지 사전 설정을 만들고 구성할 수 있습니다](managing-image-presets.md).

>[!NOTE]
>
>스마트 이미징은 기존 이미지 사전 설정에서 작동하며 마지막 전달 순간에 인텔리전스를 사용하여 브라우저 또는 네트워크 연결 속도에 따라 이미지 파일 크기를 더 줄입니다. 자세한 내용은 [스마트 이미징](imaging-faq.md)을 참조하세요.

미리 볼 때마다 이미지 사전 설정을 이미지에 적용할 수 있습니다.

>[!NOTE]
>
>Dynamic Media - Scene7 모드에서 이미지 사전 설정은 이미지 자산에 대해서만 지원됩니다.

**Dynamic Media 이미지 사전 설정을 적용하려면:**

1. 에셋을 열고 왼쪽 레일에서 드롭다운 메뉴를 선택한 다음 **[!UICONTROL 렌디션]**&#x200B;을 선택합니다.

   >[!NOTE]
   >
   >* 정적 렌디션은 창의 맨 위에 나타납니다. 동적 렌디션은 하반기에 나타납니다. 동적 변환에만 해당 URL을 사용하여 이미지를 표시할 수 있습니다. **[!UICONTROL URL]** 단추는 동적 변환을 선택한 경우에만 나타납니다. **[!UICONTROL RESS]** 단추는 응답형 이미지 사전 설정을 선택한 경우에만 나타납니다.
   >
   >* 자산의 세부 정보 보기에서 **[!UICONTROL 렌디션]**&#x200B;을 선택하면 시스템에 다양한 렌디션이 표시됩니다. You can increase the number of presets seen. [표시되는 이미지 사전 설정 수 늘리기](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display)를 참조하십시오.

   ![chlimage_1-208](assets/chlimage_1-208.png)

1. 다음 중 하나를 수행합니다.

   * 이미지 사전 설정을 미리 볼 수 있도록 동적 렌디션을 선택합니다.
   * 팝업을 표시하려면 **[!UICONTROL URL]**, **[!UICONTROL 포함]** 또는 **[!UICONTROL RESS]**&#x200B;을(를) 선택하십시오.

   >[!NOTE]
   >
   >에셋 *및* 이미지 사전 설정이 아직 게시되지 않은 경우 **[!UICONTROL URL]** 단추(또는 해당하는 경우 **[!UICONTROL URL]** 및 **[!UICONTROL RESS]** 단추)를 사용할 수 없습니다.
   >
   >또한 이미지 사전 설정은 Dynamic Media 서버에 자동으로 게시됩니다.
