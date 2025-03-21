---
title: 웹 페이지에 페이지 추적기 및 포함 코드 사용
description: Adobe Analytics에서 자산에 대한 사용 데이터를 캡처할 수 있도록 웹 사이트 코드에 페이지 추적기 를 포함하고 JavaScript 코드를 포함하는 방법을 알아봅니다.
contentOwner: AG
role: Architect, Admin
feature: Asset Reports
solution: Experience Manager, Experience Manager Assets
exl-id: bf8b2e51-60f8-423e-8ed6-167d71d6ec94
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 웹 페이지에 페이지 추적기 및 포함 코드 사용 {#using-page-tracker-and-embed-code-in-web-pages}

Page Tracker는 Adobe Analytics에서 이러한 웹 사이트의 [!DNL Adobe Experience Manager Assets] 관련 사용 데이터를 캡처할 수 있도록 타사 웹 사이트의 코드에 포함하는 JavaScript 코드 조각입니다.

에셋과 관련된 클릭 수와 같은 이벤트를 캡처하려면 타사 웹 사이트의 코드에도 포함 코드를 포함합니다.

다음 샘플 코드는 페이지 추적기 코드와 포함 코드가 모두 포함된 웹 페이지의 모양을 표시합니다.

```html
<!DOCTYPE html>
<html>
    <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in milliseconds
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","xxxx","xxx","list1","eVar3","event8","event7");
            </script>

    </head>

    <body>

                                <img
            src="https://10.41.52.147:4502/xxxx/content/dam/test/abc.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
                <img
                    src="http://localhost/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
</html>
```

## 페이지 추적기 코드 추가 {#adding-page-tracker-code}

웹 사이트 코드의 헤더 섹션 내에 페이지 추적기 코드를 추가합니다. 다음 코드 조각은 샘플 웹 페이지에 포함된 페이지 추적기 코드를 표시합니다.

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```

## 포함 코드 추가 {#add-embed-code}

웹 사이트 코드의 본문 내에 포함 코드를 추가합니다. 다음 코드 조각은 샘플 웹 페이지에 포함된 포함 코드를 표시합니다.

```xml
<body>

      <img
            src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
           <img
                    src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
```
