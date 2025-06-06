---
title: 360/VR 비디오
description: Dynamic Media에서 360 및 VR(가상 현실) 비디오로 작업하고 사용하는 방법에 대해 알아봅니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: 360 VR Video
role: User, Admin
solution: Experience Manager, Experience Manager Assets
exl-id: 17e45464-3de4-40a8-b102-ccc9eaba92a3
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---

# 360/VR 비디오 {#vr-video}

360도 비디오에서는 모든 방향에서 동시에 뷰를 기록합니다. 전방향 카메라나 카메라 모음을 이용하여 촬영합니다. 평면 디스플레이에서 재생하는 동안 사용자는 시야각을 제어할 수 있습니다. 모바일 장치에서 재생하는 경우 일반적으로 내장된 자이로스코프 컨트롤을 사용합니다.

Dynamic Media - Scene7 모드에는 360 비디오 자산의 배송에 대한 기본 지원이 포함됩니다. 기본적으로 보거나 재생하기 위해 추가 구성은 필요하지 않습니다. .mp4, .mkv 및 .mov 와 같은 표준 비디오 확장명을 사용하여 360 비디오를 제공합니다. 가장 일반적인 코덱은 H.264입니다.

이 섹션에서는 360/VR 비디오 뷰어를 사용하여 공간, 속성, 위치, 가로, 의료 시술 등의 몰입형 시청 경험을 위해 동일 사각형 비디오를 렌더링하는 방법에 대해 설명합니다.

현재 공간 오디오가 지원되지 않습니다. 오디오가 스테레오로 혼합된 경우 고객이 카메라 시야각을 변경할 때 밸런스(L/R)가 변경되지 않습니다.

[뷰어 사전 설정 관리](/help/assets/managing-viewer-presets.md)도 참조하세요.

## 360 비디오 작동 중 {#video-in-action}

브라우저 창을 열고 360도 비디오를 보려면 [Space Station 360](https://s7d1.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS)을(를) 선택하십시오. 비디오 재생 중에 마우스 포인터를 새 위치로 드래그하여 보기 각도를 변경합니다.

국제 우주 정거장이 우주에 떠 있고 지구 뒤에 태양이 떠 있는 ![360 비디오 샘플입니다.](assets/6_5_360videoiss_simplified.png)
*Space Station 360의 비디오 프레임*

## 360/VR 비디오 및 Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

Adobe Premier Pro를 사용하여 360/VR 푸티지를 보고 편집할 수 있습니다. 예를 들어, 장면에 로고와 텍스트를 적절하게 배치하고, 등장방형 미디어용으로 특별히 설계된 효과와 전환을 적용할 수 있습니다.

[360/VR 비디오 편집](https://helpx.adobe.com/kr/premiere-pro/how-to/edit-360-vr-video.html)을 참조하세요.

## 360 비디오 뷰어에 사용할 자산 업로드 {#uploading-assets-for-use-with-the-video-viewer}

Adobe Experience Manager에 업로드된 360개의 비디오 자산은 자산 페이지에서 일반 비디오 자산과 유사하게 **멀티미디어**(으)로 레이블이 지정됩니다.

![6_5_360video-selecttopreview](assets/6_5_360video-selecttopreview.png)
*업로드된 360개의 비디오 자산이 카드 보기에 표시됩니다. 자산이 멀티미디어로 레이블이 지정되었습니다.*

**360 비디오 뷰어에 사용할 자산을 업로드합니다.**

1. 360 비디오 자산 전용의 폴더를 만들었습니다.
1. [응용 비디오 프로필을 폴더에 적용](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   360 비디오 콘텐츠를 렌더링하면 표준 비 360 비디오 콘텐츠보다 소스 비디오 해상도 및 인코딩된 표현물 해상도에 대한 요구 사항이 더 높아집니다.

   Dynamic Media와 함께 제공되는 바로 사용 가능한 응용 비디오 프로필을 사용할 수 있습니다. 그러나 360이 아닌 비디오 뷰어로 렌더링된 동일한 설정으로 인코딩된 360이 아닌 비디오에 대해 얻는 것보다 360이 아닌 비디오 품질이 눈에 띄게 더 낮습니다. 따라서 고화질 360 비디오가 필요한 경우 다음 작업을 수행하십시오.

   * 가장 좋은 방법은 원본 360 비디오 콘텐츠에서 다음 해상도 중 하나를 사용하는 것입니다.

      * 1080p - 1920 x 1080, Full HD 또는 FHD 해상도로 알려짐,
      * 2160p - 3840 x 2160, 4k, UHD 또는 Ultra HD 해상도로 알려짐. 이 대형 디스플레이 해상도는 프리미엄 TV 세트와 컴퓨터 모니터에서 가장 많이 발견됩니다. 너비가 4000픽셀에 가깝기 때문에 2160p 해상도를 &quot;4k&quot;라고 하는 경우가 많습니다. 즉, 1080p의 4배 픽셀을 제공합니다.

   * 고품질 표현물로 [사용자 지정 응용 비디오 프로필을 만듭니다](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming). 예를 들어 다음 세 가지 설정이 포함된 응용 비디오 프로필을 만듭니다.

      * width=auto; height=720; bitrate=2500kbps
      * width=auto; height=1080; bitrate=5000kbps
      * width=auto; height=1440; bitrate=6600kbps

   * 360 비디오 자산에만 사용되는 폴더에서 360 비디오 콘텐츠를 처리합니다.

   이 접근 방식은 최종 사용자의 네트워크 및 CPU에 더 많은 요구를 제공합니다.

1. [비디오를 폴더에 업로드](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

## 360개 비디오의 기본 종횡비 재정의  {#overriding-the-default-aspect-ratio-of-videos}

업로드된 에셋이 360 비디오 뷰어에 사용하려는 360 비디오에 적합하려면 에셋의 종횡비가 2여야 합니다.

기본적으로 Experience Manager은 종횡비(폭/높이)가 2.0이면 비디오를 &quot;360&quot;으로 감지합니다. 관리자는 CRXDE Lite에서 다음과 같이 선택적 `s7video360AR` 속성을 설정하여 기본 종횡비 설정인 2를 재정의할 수 있습니다.

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **속성 형식** - Double
   * **값** - 부동 소수점 종횡비, 기본값 2.0.

이 속성을 설정하면 기존 비디오와 새로 업로드한 비디오 모두에 즉시 적용됩니다.

종횡비는 자산 세부 정보 페이지 및 [Video 360 Media WCM 구성 요소](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components)에 대한 360개의 비디오 자산에 적용됩니다.

360개의 비디오를 업로드하여 시작하십시오.

## 360 비디오 미리 보기 {#previewing-video}

미리보기 를 사용하여 고객에게 360 비디오가 어떻게 보이는지 확인하고 예상대로 작동하는지 확인할 수 있습니다.

[뷰어 사전 설정 편집](/help/assets/managing-viewer-presets.md#editing-viewer-presets)도 참조하세요.

360 비디오가 만족스러우면 게시할 수 있습니다.

[웹 페이지에 비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md)을 참조하십시오.
[웹 응용 프로그램에 URL 연결](/help/assets/linking-urls-to-yourwebapplication.md)을 참조하십시오. 대화형 콘텐츠에 상대 URL이 있는 링크, 특히 Experience Manager Sites 페이지에 대한 링크가 있는 경우에는 URL 기반 연결 방법이 불가능합니다.
[페이지에 Dynamic Media Assets 추가](/help/assets/adding-dynamic-media-assets-to-pages.md)를 참조하십시오.

**360 비디오를 미리 보려면:**

1. **[!UICONTROL Assets]**&#x200B;에서 생성한 기존 360 비디오로 이동합니다. 미리보기 모드에서 열 수 있도록 360 비디오 자산을 선택합니다.

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   비디오를 미리 볼 수 있도록 360 비디오 에셋을 선택합니다.

1. 미리 보기 페이지에서 페이지의 왼쪽 상단 근처에 있는 드롭다운 목록을 선택한 다음 **[!UICONTROL 뷰어]**&#x200B;를 선택합니다.

   ![6_5_360video-preview-viewers](assets/6_5_360video-preview-viewers.png)

   뷰어 목록에서 **[!UICONTROL Video360_social]**&#x200B;을(를) 선택한 후 다음 중 하나를 수행합니다.

   * 정적 장면의 시야각을 변경하려면 비디오 위로 마우스 포인터를 드래그합니다.
   * 재생을 시작하려면 비디오의 **[!UICONTROL 재생]** 단추를 선택하십시오. 비디오가 재생될 때 비디오 위로 마우스 포인터를 끌어 시야각을 변경합니다.

   ![지구 및 태양이 배경에 있는 우주 공간에 떠 있는 국제 우주 정거장의 스크린샷&#x200B;](assets/6_5_360video-preview-video360-social.png)*360 비디오 스크린샷*

   * 뷰어 목록에서 **[!UICONTROL Video360VR]**&#x200B;을(를) 선택합니다.

     가상 현실(VR) 비디오는 가상 현실 헤드셋을 사용함으로써 액세스되는 몰입형 비디오 콘텐츠이다. 일반 비디오와 마찬가지로 360도 비디오 카메라를 사용하여 비디오를 녹화하고 캡처할 때 VR 비디오를 처음부터 만듭니다.

   ![지구와 태양이 있는 우주 공간에 떠 있는 국제 우주 정거장의 근접 촬영 스크린샷이 배경에 부분적으로 표시됩니다](assets/6_5_360video-preview-video360vr.png)
   *360 VR 비디오 스크린샷입니다.*

1. 미리 보기 페이지의 오른쪽 상단 근처에서 **[!UICONTROL 닫기]**&#x200B;를 선택합니다.

## 360 비디오 게시 {#publishing-video}

사용할 수 있도록 360 비디오를 게시합니다. 360 비디오를 게시하면 URL 및 포함 코드가 활성화됩니다. 또한 확장 가능하고 성능이 뛰어난 전송을 위해 CDN과 통합된 Dynamic Media 클라우드에 360 비디오를 게시합니다.

360 비디오를 게시하는 방법에 대한 자세한 내용은 [Dynamic Media 자산 게시](/help/assets/publishing-dynamicmedia-assets.md)를 참조하십시오.
[웹 페이지에 비디오 또는 이미지 뷰어 포함](/help/assets/embed-code.md)도 참조하세요.
[웹 응용 프로그램에 URL 연결](/help/assets/linking-urls-to-yourwebapplication.md)도 참조하세요. 대화형 콘텐츠에 상대 URL이 있는 링크, 특히 Experience Manager Sites 페이지에 대한 링크가 있는 경우에는 URL 기반 연결 방법이 불가능합니다.
[페이지에 Dynamic Media 자산 추가](/help/assets/adding-dynamic-media-assets-to-pages.md)도 참조하세요.
