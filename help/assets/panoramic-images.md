---
title: 파노라마 이미지
description: Dynamic Media에서 파노라마 이미지로 작업하는 방법을 알아봅니다.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Panoramic Images,Asset Management
role: User, Admin
solution: Experience Manager, Experience Manager Assets
exl-id: 18458c49-ab84-4d49-95b5-52922fba1365
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 파노라마 이미지{#panoramic-images}

이 섹션에서는 파노라마 이미지 뷰어를 사용하여 공간, 속성, 위치 또는 풍경을 360도로 몰입형 방식으로 볼 수 있도록 구형 파노라마 이미지를 렌더링하는 방법에 대해 설명합니다.

[뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md)도 참조하세요.

![panoramic-image2](assets/panoramic-image2.png)

## 파노라마 이미지 뷰어에 사용할 자산 업로드 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

업로드한 에셋이 파노라마 이미지 뷰어에 사용하려는 구면 파노라마 이미지로서 적합하려면, 에셋에 다음 중 하나 또는 둘 다 있어야 합니다.

* 종횡비가 2입니다.
CRXDE Lite에서 다음과 같은 경우 기본 종횡비 설정인 2를 재정의할 수 있습니다.
  `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* 키워드 `equirectangular`, `spherical` 및 `panorama` 또는 `spherical` 및 `panoramic`을(를) 태그 지정했습니다. [태그 사용](/help/sites-authoring/tags.md)을 참조하세요.

종횡비와 키워드 기준은 모두 자산 세부 정보 페이지 및 `Panoramic Media` WCM 구성 요소의 파노라마 자산에 적용됩니다.

파노라마 이미지 뷰어에 사용할 자산을 업로드하려면 [Assets 업로드](/help/assets/manage-assets.md#uploading-assets)를 참조하십시오.

## Dynamic Media Classic 구성 {#configuring-dynamic-media-classic-scene}

Adobe Experience Manager 내에서 파노라마 이미지 뷰어가 제대로 작동하려면 파노라마 이미지 뷰어 사전 설정을 Dynamic Media Classic 및 Dynamic Media Classic 관련 메타데이터와 동기화하여 뷰어 사전 설정을 JCR에서 업데이트합니다. 이 동기화를 수행하려면 다음과 같이 Dynamic Media Classic을 구성하십시오.

1. [Dynamic Media Classic 데스크톱 응용 프로그램](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ko#getting-started)을 연 다음 계정에 로그인하세요.

1. 페이지의 오른쪽 상단 모서리에서 **[!UICONTROL 설정]** > **[!UICONTROL 응용 프로그램 설정]** > **[!UICONTROL 게시 설정]** > **[!UICONTROL 이미지 서버]**&#x200B;를 선택합니다.
1. 이미지 서버 게시 페이지의 맨 위에 있는 **[!UICONTROL 게시 컨텍스트]** 드롭다운 메뉴에서 **[!UICONTROL 이미지 제공]**&#x200B;을 선택합니다.

1. 동일한 이미지 서버 게시 페이지에서 제목 **[!UICONTROL 요청 특성]**&#x200B;을 찾습니다.
1. 요청 특성 제목에서 **[!UICONTROL 응답 이미지 크기 제한]**&#x200B;을(를) 찾습니다. 그런 다음 관련 너비 및 높이 필드에서 파노라마 이미지에 대해 허용되는 최대 이미지 크기를 늘립니다.

   Dynamic Media Classic의 픽셀 수는 25,000,000픽셀로 제한됩니다. 2:1 종횡비의 이미지에 허용되는 최대 크기는 7000 x 3500입니다. 그러나 일반적인 데스크탑 화면의 경우 4096 x 2048 픽셀이면 충분합니다.

   >[!NOTE]
   >
   >허용 가능한 최대 이미지 크기 내에 있는 이미지만 지원됩니다. 크기 제한을 초과하는 이미지에 대한 요청은 403 응답을 초래합니다.

1. 요청 속성 제목에서 다음을 수행합니다.

   * 요청 난독화 모드를 **[!UICONTROL 사용 안 함]**(으)로 설정합니다.
   * 요청 잠금 모드를 **[!UICONTROL 사용 안 함]**(으)로 설정합니다.

   이러한 설정은 Experience Manager에서 `Panoramic Media` WCM 구성 요소를 사용하는 데 필요합니다.

1. 이미지 서버 게시 페이지 하단의 왼쪽에 있는 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

1. 오른쪽 아래 모서리에서 **[!UICONTROL 닫기]**&#x200B;를 선택합니다.

### 파노라마 미디어 WCM 구성 요소 문제 해결 {#troubleshooting-the-panoramic-media-wcm-component}

이미지를 WCM의 파노라마 미디어 구성 요소에 드롭하고 구성 요소 자리 표시자가 축소된 경우 다음 문제를 해결하십시오.

* 403 금지됨 오류가 발생하는 경우 요청한 이미지 크기가 너무 크기 때문일 수 있습니다. [Dynamic Media Classic 구성](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)에서 **[!UICONTROL 응답 이미지 크기 제한]** 설정을 검토하십시오.

* 에셋에 대한 &quot;잘못된 잠금&quot; 또는 페이지에 표시되는 &quot;구문 분석 오류&quot;에 대해서는 난독화 요청 모드 및 잠금 요청 모드 를 선택하여 비활성화하십시오.
* 오염된 캔버스 오류의 경우 이미지 에셋에 대한 이전 요청에 대한 규칙 세트 정의 파일 경로 및 CTN 무효화를 설정하십시오.
* 크기가 지원되는 제한을 초과하는 이미지 요청 후에 이미지 품질이 낮은 경우 **[!UICONTROL JPEG 인코딩 특성 > 품질]** 설정이 비어 있지 않은지 확인하십시오. **[!UICONTROL 품질]** 필드에 대한 일반적인 설정은 `95`입니다. 이미지 서버 게시 페이지에서 설정을 찾을 수 있습니다. 페이지에 액세스하려면 [Dynamic Media Classic 구성](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)을 참조하십시오.

## 파노라마 이미지 미리 보기 {#previewing-panoramic-images}

[Assets 미리 보기](/help/assets/previewing-assets.md)를 참조하십시오.

## 파노라마 이미지 게시 {#publishing-panoramic-images}

[Assets 게시](/help/assets/publishing-dynamicmedia-assets.md)를 참조하십시오.
