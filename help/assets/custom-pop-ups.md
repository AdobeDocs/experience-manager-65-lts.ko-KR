---
title: 빠른 보기를 사용하여 사용자 정의 팝업 만들기
description: 기본 빠른 보기는 전자 상거래 경험에서 제품 정보와 함께 팝업이 표시되어 구매를 유도하는 데 사용됩니다. 팝업에 표시할 사용자 지정 콘텐츠를 트리거할 수 있습니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Viewers
role: User, Admin
solution: Experience Manager, Experience Manager Assets
exl-id: 37e0d7de-0f7b-475f-b508-3dd150008fee
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 2%

---

# 빠른 보기를 사용하여 사용자 정의 팝업 만들기 {#using-quickviews-to-create-custom-pop-ups}

기본 빠른 보기는 전자 상거래 경험에서 제품 정보와 함께 팝업이 표시되어 구매를 유도하는 데 사용됩니다. 하지만 사용자 지정 콘텐츠를 트리거하여 팝업에 표시할 수 있습니다. 이 기능을 사용하면 뷰어에 따라 핫스팟, 썸네일 이미지 또는 이미지 맵에서 선택하여 정보 또는 관련 콘텐츠를 볼 수 있습니다.

빠른 보기는 Dynamic Media의 다음 뷰어에서 지원됩니다.

* 대화형 이미지(클릭 가능한 핫스팟)
* 대화형 비디오(비디오 재생 중 클릭 가능한 썸네일 이미지)
* 회전 배너(클릭 가능한 핫스팟 또는 이미지 맵)

각 뷰어의 기능은 다르지만 빠른 보기를 만드는 프로세스는 지원되는 세 개의 뷰어 모두에서 동일합니다.

**빠른 보기를 사용하여 사용자 지정 팝업을 만들려면:**

1. 업로드된 에셋에 대한 빠른 보기를 만듭니다.

   일반적으로 빠른 보기는 사용 중인 뷰어와 함께 사용할 자산을 편집할 때 만듭니다.

   <table>
    <tbody>
    <tr>
    <td><strong>사용 중인 뷰어</strong></td>
    <td><strong>빠른 보기를 만들려면 다음 단계를 완료하십시오</strong></td>
    </tr>
    <tr>
    <td>대화형 이미지</td>
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">이미지 배너에 핫스팟을 추가하는 중</a>.</td>
    </tr>
    <tr>
    <td>대화형 비디오</td>
    <td><a href="/help/assets/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">비디오에 대화형 기능을 추가</a>.</td>
    </tr>
    <tr>
    <td>슬라이드 배너</td>
    <td><a href="/help/assets/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">배너에 핫스팟 또는 이미지 맵 추가</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 웹 사이트 내에서 뷰어를 통합하려면 뷰어 포함 코드를 가져옵니다.

   <table>
    <tbody>
    <tr>
    <td>사용 중인 <strong>뷰어</strong><br /> </td>
    <td><strong>뷰어를 웹 사이트와 통합하려면 다음 단계를 완료하십시오</strong></td>
    </tr>
    <tr>
    <td>대화형 이미지</td>
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">대화형 이미지를 웹 사이트와 통합</a>.<br /> </td>
    </tr>
    <tr>
    <td>대화형 비디오<br /> </td>
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">대화형 비디오와 웹 사이트 통합</a>.<br /> </td>
    </tr>
    <tr>
    <td>회전 배너</td>
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">웹 사이트 페이지에 회전 배너를 추가</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 사용 중인 뷰어는 빠른 보기를 사용하는 방법을 알고 있어야 합니다.

   뷰어에서 `QuickViewActive`(이)라는 처리기를 사용합니다.

   **예**
대화형 이미지에 대해 웹 페이지에서 다음 샘플 포함 코드를 사용한다고 가정해 보십시오.

   ![chlimage_1-291](assets/chlimage_1-291.png)

   처리기가 `setHandlers`을(를) 사용하여 뷰어에 로드되었습니다.

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **위의 샘플 포함 코드 예제를 사용하면 다음 코드가 있습니다.**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   다음에서 `setHandlers()` 메서드에 대해 자세히 알아보세요.

   * 대화형 이미지 뷰어: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html?lang=ko](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html?lang=ko)
   * 대화형 비디오 뷰어: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html?lang=ko](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html?lang=ko)

1. `quickViewActivate` 처리기를 구성합니다.

   `quickViewActivate` 처리기는 뷰어에서 빠른 보기를 제어합니다. 처리기에는 빠른 보기와 함께 사용할 변수 목록과 함수 호출이 포함되어 있습니다. 포함 코드는 빠른 보기에 설정된 SKU 변수 및 샘플 `loadQuickView` 함수 호출에 대한 매핑을 제공합니다.

   **변수 매핑**
웹 페이지에서 사용할 변수를 빠른 보기에 포함된 SKU 값 및 일반 변수에 매핑합니다.

   `var *variable1*= inData.*quickviewVariable*`

   제공된 포함 코드에는 SKU 변수에 대한 샘플 매핑이 있습니다.

   `var sku=inData.sku`

   다음과 같이 빠른 보기에서 추가 변수를 매핑합니다.

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **함수 호출**
처리기가 작동하려면 Quickview에 대한 함수 호출도 필요합니다. 함수는 호스트 페이지에서 액세스할 수 있는 것으로 간주됩니다. 포함 코드는 샘플 함수 호출을 제공합니다.

   `loadQuickView(sku)`

   샘플 함수 호출은 함수 `loadQuickView()`이(가) 있고 액세스할 수 있다고 가정합니다.

   다음에서 `quickViewActivate` 메서드에 대해 자세히 알아보세요.

   * 대화형 이미지 뷰어: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html?lang=ko](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html?lang=ko)
   * 대화형 비디오 뷰어: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html?lang=ko](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html?lang=ko)
   * 대화형 비디오 뷰어에서 대화형 데이터 지원: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html?lang=ko](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html?lang=ko)

1. 다음 작업을 수행합니다.

   * 포함 코드의 setHandlers 섹션의 주석 처리를 제거합니다.
   * 빠른 보기에 포함된 모든 추가 변수를 매핑합니다.

      * 변수를 더 추가하는 경우 `loadQuickView(sku,*var1*,*var2*)` 호출을 업데이트하십시오.

   * 뷰어 외부의 페이지에 간단한 `loadQuickView`() 함수를 만듭니다.

     예를 들어 다음 은 브라우저 콘솔에 SKU 값을 기록합니다.

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * 웹 서버에 테스트 HTML 페이지를 업로드하고 엽니다.

     Quickview의 변수가 매핑되고 함수 호출이 있는 경우 브라우저 콘솔은 제공된 샘플 함수를 사용하여 브라우저 콘솔에 변수 값을 기록합니다.

1. 이제 함수를 사용하여 빠른 보기에서 간단한 팝업을 호출할 수 있습니다. 다음 예제에서는 팝업에 `DIV`을(를) 사용합니다.
1. 다음과 같은 방법으로 팝업 `DIV`의 스타일을 지정합니다. 원하는 대로 나만의 스타일을 추가합니다.

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. 팝업 `DIV`을(를) HTML 페이지의 본문에 배치합니다.

   요소 중 하나는 사용자가 빠른 보기를 호출할 때 SKU 값으로 업데이트되는 ID로 설정됩니다. 이 예에는 팝업이 표시된 후 다시 숨길 수 있는 간단한 버튼도 포함되어 있습니다.

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. 팝업에서 SKU 값을 업데이트할 수 있도록 함수를 추가합니다. 5단계에서 만든 간단한 함수를 교체하여 팝업을 표시할 수 있습니다. 다음을 사용하여:

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. 웹 서버에 테스트 HTML 페이지를 업로드하고 엽니다. 사용자가 빠른 보기를 호출하면 뷰어에 팝업 `DIV`이(가) 표시됩니다.
1. **전체 화면 모드에서 사용자 지정 팝업을 표시하는 방법**

   대화형 비디오 뷰어와 같은 일부 뷰어는 전체 화면 모드의 표시를 지원합니다. 그러나 이전 단계에서 설명한 대로 팝업을 사용하면 전체 화면 모드에 있는 동안 뷰어 뒤에 팝업이 표시됩니다.

   팝업이 표준 및 전체 화면 모드로 모두 표시되도록 하려면 팝업을 뷰어 컨테이너에 첨부합니다. 두 번째 처리기 메서드 `initComplete`을(를) 사용합니다.

   뷰어가 초기화된 후 `initComplete` 처리기가 호출됩니다.

   ```xml
   "initComplete":function() { code block }
   ```

   다음에서 `init()` 메서드에 대해 자세히 알아보세요.

   * 대화형 이미지 뷰어: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html?lang=ko](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html?lang=ko)
   * 대화형 비디오 뷰어: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html?lang=ko](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html?lang=ko)

1. 이전 단계에서 설명한 팝업을 뷰어에 첨부하려면 다음 코드를 사용합니다.

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   위의 코드에서 다음을 수행했습니다.

   * 사용자 지정 팝업을 식별했습니다.
   * DOM에서 제거했습니다.
   * 뷰어 컨테이너를 식별했습니다.
   * 팝업을 뷰어 컨테이너에 첨부했습니다.

1. 전체 setHandlers 코드가 다음과 유사하게 표시됩니다(대화형 비디오 뷰어가 사용됨).

   ```xml
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. 처리기가 로드되면 뷰어를 초기화합니다.

   `*viewerInstance.*init()`

   **예**
이 예제에서는 대화형 이미지 뷰어를 사용합니다.

   `s7interactiveimageviewer.init()`

   뷰어를 호스트 페이지에 포함시킨 후 `init()`을(를) 사용하여 뷰어를 호출하기 전에 뷰어 인스턴스가 만들어지고 처리기가 로드되었는지 확인하십시오.
