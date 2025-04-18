---
title: Adobe Analytics 프레임워크 사용자 지정
description: Adobe Experience Manager용 Adobe Analytics 프레임워크를 사용자 지정하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Developer
exl-id: 6a32bd9d-268d-4d03-b495-47ec6660c138
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1610'
ht-degree: 0%

---

# Adobe Analytics 프레임워크 사용자 지정{#customizing-the-adobe-analytics-framework}

Adobe Analytics 프레임워크는 Adobe Analytics에서 추적하는 정보를 결정합니다. 기본 프레임워크를 사용자 지정하려면 JavaScript을 사용하여 사용자 지정 추적을 추가하고, Adobe Analytics 플러그인을 통합하고, 추적에 사용되는 프레임워크 내에서 일반 설정을 변경합니다.

## 생성된 프레임워크 JavaScript 정보 {#about-the-generated-javascript-for-frameworks}

페이지가 Adobe Analytics 프레임워크와 연결되어 있고 페이지에 Analytics 모듈에 대한 [참조](/help/sites-administering/adobeanalytics.md)가 포함되어 있으면 페이지에 대한 analytics.sitecatalyst.js 파일이 자동으로 생성됩니다.

페이지의 JavaScript은 s_code.js Adobe Analytics 라이브러리에서 정의하는 `s_gi`개체를 만들고 해당 속성에 값을 할당합니다. 개체 인스턴스의 이름은 `s`입니다. 이 섹션에 나와 있는 코드 예제는 이 `s` 변수를 여러 번 참조합니다.

다음 예제 코드는 analytics.sitecatalyst.js 파일의 코드와 유사합니다.

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";

/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

사용자 지정 JavaScript 코드를 사용하여 프레임워크를 사용자 지정할 때 이 파일의 내용이 변경됩니다.

## Adobe Analytics 속성 구성 {#configuring-adobe-analytics-properties}

Adobe Analytics 내에는 프레임워크에서 구성할 수 있는 몇 가지 사전 정의된 변수가 있습니다. **charset**, **cookieLifetime**, **currencyCode** 및 **trackInlineStats** 변수는 기본적으로 **일반 분석 설정** 목록에 포함되어 있습니다.

![aa-22](assets/aa-22.png)

변수 이름과 값을 목록에 추가할 수 있습니다. 이러한 사전 정의된 변수와 추가한 모든 변수는 analytics.sitecatalyst.js 파일에서 `s` 개체의 속성을 구성하는 데 사용됩니다. 다음 예제에서는 추가된 `CONSTANT` 값의 `prop10` 속성이 JavaScript 코드에 어떻게 표시되는지 보여 줍니다.

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.prop10= 'CONSTANT';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";
```

다음 절차에 따라 변수를 목록에 추가합니다.

1. Adobe Analytics 프레임워크 페이지에서 **일반 Analytics 설정** 영역을 확장합니다.
1. 변수 목록 아래에서 항목 추가 를 클릭하여 새 변수를 목록에 추가합니다.
1. 왼쪽 셀에 변수 이름(예: `prop10`)을 입력합니다.

1. 오른쪽 열에 변수 값(예: `CONSTANT`)을 입력합니다.

1. 변수를 제거하려면 변수 옆에 있는 (-) 단추를 클릭합니다.

>[!NOTE]
>
>변수와 값을 입력할 때 형식이 올바른지, 철자가 정확한지, 또는 올바른 값/변수 쌍을 사용하여 **호출이 전송되지 않는지**&#x200B;확인합니다. 철자가 잘못된 변수와 값은 호출이 발생하지 않도록 할 수도 있습니다.
>
>이러한 변수가 올바르게 설정되었는지 확인하려면 Adobe Analytics 담당자에게 문의하십시오.

>[!CAUTION]
>
>이 목록에 있는 변수 중 일부는 Adobe Analytics 호출이 올바르게 작동하는 **필수**&#x200B;입니다(예: **currencyCode**, **charSet**).
>
>따라서 프레임워크 자체에서 제거되더라도 Adobe Analytics 호출이 수행될 때 기본값으로 계속 연결됩니다.

### Adobe Analytics 프레임워크에 사용자 정의 JavaScript 추가 {#adding-custom-javascript-to-an-adobe-analytics-framework}

**일반 Analytics 설정** 영역의 자유 형식 JavaScript 상자를 사용하면 Adobe Analytics 프레임워크에 사용자 지정 코드를 추가할 수 있습니다.

![aa-21](assets/aa-21.png)

추가하는 코드는 analytics.sitecatalyst.js 파일에 추가됩니다. 따라서 `s_code.js`에 정의된 `s_gi` JavaScript 개체의 인스턴스인 `s` 변수에 액세스할 수 있습니다. 예를 들어 다음 코드를 추가하는 것은 이전 섹션의 예인 `CONSTANT` 값의 `prop10`이라는 변수를 추가하는 것과 같습니다.

`s.prop10= 'CONSTANT';`

[analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md) 파일(Adobe Analytics `s-code.js` 파일의 콘텐츠 포함)의 코드에는 다음 코드가 포함되어 있습니다.

`if (s.usePlugins) s.doPlugins(s)`

다음 절차는 JavaScript 상자를 사용하여 Adobe Analytics 추적을 사용자 지정하는 방법을 보여 줍니다. JavaScript에서 Adobe Analytics 플러그인을 사용해야 하는 경우 [통합](/help/sites-administering/adobeanalytics.md)하여 AEM에 로그인하십시오.

1. `s.doPlugins`이(가) 실행되도록 다음 JavaScript 코드를 상자에 추가합니다.

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >이 코드는 기본 드래그 앤 드롭 인터페이스나 Adobe Analytics 보기의 인라인 JavaScript을 통해 수행할 수 없는 방식으로 사용자 지정된 Adobe Analytics 호출에서 변수를 전송하려는 경우 필요합니다.
   >
   >사용자 지정 변수가 s_doPlugins 함수 외부에 있으면 Adobe Analytics 호출에서 *정의되지 않음 *으로 전송됩니다

1. **s_doPlugins** 함수에 JavaScript 코드를 추가합니다.

다음 예제에서는 공통 구분 기호 &quot;|&quot;를 사용하여 페이지에 캡처된 데이터를 계층 구조 순서로 연결합니다.

Adobe Analytics 프레임워크는 다음과 같은 구성을 가지고 있습니다.

* `prop2` Adobe Analytics 변수가 `pagedata.sitesection` 사이트 속성에 매핑되어 있습니다.

* `prop3` Adobe Analytics 변수가 `pagedata.subsection` 사이트 속성에 매핑되어 있습니다.

* JavaScript에서 무료 상자에 다음 코드가 추가됩니다.

  ```
  s.usePlugins=true;
   function s_doPlugins(s) {
   s.prop1 = s.prop2+'|'+s.prop3;
   }
   s.doPlugins=s_doPlugins;
  ```

* 프레임워크를 사용하는 웹 페이지를 방문하면(또는 편집 모드에서 페이지를 다시 로드하거나 미리 보면) Adobe Analytics 호출이 수행됩니다.

예를 들어 Adobe Analytics에서 다음 값이 생성됩니다.

![aa-20](assets/aa-20.png)

### 모든 Adobe Analytics 프레임워크에 대한 전역 사용자 지정 코드 추가 {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

모든 Adobe Analytics 프레임워크에 통합되는 사용자 지정 JavaScript 코드를 제공합니다. 페이지의 Adobe Analytics 프레임워크에 사용자 지정 [자유 형식의 JavaScript](/help/sites-administering/adobeanalytics.md)이(가) 없으면 /libs/cq/analytics/components/sitecatalyst/config.js.jsp 스크립트가 생성하는 JavaScript이 [analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md) 파일에 추가됩니다. 기본적으로 스크립트는 주석 처리되어 있어서 영향을 주지 않습니다. 또한 이 코드는 `s.usePlugins`을(를) `false`(으)로 설정합니다.

```
/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

Adobe Analytics s_code.js 파일의 컨텐츠를 포함하는 analytics.sitecatalyst.js 파일의 코드에는 다음 코드가 포함되어 있습니다.

가정 (s.usePlugins) s.doPlugins (s)

따라서 `s_doPlugins` 함수의 모든 코드가 실행되도록 JavaScript에서 `s.usePlugins`을(를) `true`(으)로 설정해야 합니다. 코드를 사용자 정의하려면 config.js.jsp 파일을 고유한 JavaScript을 사용하는 파일과 오버레이합니다. JavaScript에서 Adobe Analytics 플러그인을 사용해야 하는 경우 [통합](/help/sites-administering/adobeanalytics.md)하여 AEM에 로그인하십시오.

>[!NOTE]
>
>/libs/cq/analytics/components/sitecatalyst/config.js.jsp 파일을 편집하지 마십시오. 특정 AEM 업그레이드 또는 유지 관리 작업에서 원본 파일을 다시 설치하여 변경 사항을 제거할 수 있습니다.

1. CRXDE Lite에서 /apps/cq/analytics/components 폴더 구조를 만듭니다.

   1. /apps 폴더를 마우스 오른쪽 단추로 클릭하고 만들기 > 폴더 만들기 를 클릭합니다.
   1. `cq`을(를) 폴더 이름으로 지정하고 [확인]을 클릭합니다.
   1. 마찬가지로 `analytics` 및 `components` 폴더를 만듭니다.

1. 만든 `components` 폴더를 마우스 오른쪽 단추로 클릭하고 만들기 > 구성 요소 만들기를 클릭합니다. 다음 속성 값을 지정합니다.

   * 레이블: `sitecatalyst`
   * 제목: `sitecatalyst`
   * 상위 유형: `/libs/cq/analytics/components/sitecatalyst`
   * 그룹: `hidden`

1. 확인(OK) 단추가 활성화될 때까지 다음(Next)을 반복적으로 클릭한 다음 확인(OK)을 클릭합니다.

   Sitecatalyst 구성 요소에는 자동으로 생성된 sitecatalyst.jsp 파일이 포함되어 있습니다.

1. Sitecatalyst.jsp 파일을 마우스 오른쪽 단추로 클릭하고 삭제를 클릭합니다.

1. Sitecatalyst 구성 요소를 마우스 오른쪽 단추로 클릭하고 만들기 > 파일 만들기를 클릭합니다. `config.js.jsp` 이름을 지정한 다음 [확인]을 클릭합니다.

   편집을 위해 config.js.jsp 파일이 자동으로 열립니다.

1. 파일에 다음 텍스트를 추가한 다음 모두 저장을 클릭합니다.

   ```java
   <%@page session="true"%>
   /* Plugin Config */
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom plugin code here
   }
   s.doPlugins=s_doPlugins;
   ```

   이제 /apps/cq/analytics/components/sitecatalyst/config.js.jsp 스크립트가 생성하는 JavaScript 코드가 Adobe Analytics 프레임워크를 사용하는 모든 페이지의 analytics.sitecatalyst.js 파일에 삽입됩니다.

1. `s_doPlugins` 함수에서 실행할 JavaScript 코드를 추가한 다음 모두 저장을 클릭합니다.

>[!CAUTION]
>
>페이지 프레임워크의 자유 형식 JavaScript(공백만 포함)에 텍스트가 있는 경우 config.js.jsp가 무시됩니다.

### AEM에서 Adobe Analytics 플러그인 사용 {#using-adobe-analytics-plugins-in-aem}

Adobe Analytics 플러그인에 대한 JavaScript 코드를 가져와 AEM의 Adobe Analytics 프레임워크에 통합합니다. 사용자 지정 JavaScript 코드에서 사용할 수 있도록 `sitecatalyst.plugins` 범주의 클라이언트 라이브러리 폴더에 코드를 추가합니다.

예를 들어 `getQueryParams` 플러그인을 통합하는 경우 사용자 지정 JavaScript의 `s_doPlugins` 함수에서 플러그인을 호출할 수 있습니다. 다음 예제 코드는 Adobe Analytics 호출이 트리거될 때 레퍼러의 URL에서 **&quot;pid&quot;**&#x200B;의 쿼리 문자열을 **eVar1**(으)로 보냅니다.

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM은 기본적으로 사용할 수 있도록 다음 Adobe Analytics 플러그인을 설치합니다.

* getQueryParam()
* getPreviousValue()
* split()

/libs/cq/analytics/clientlibs/sitecatalyst/plugins 클라이언트 라이브러리 폴더에는 sitecatalyst.plugins 카테고리에 이러한 플러그인이 포함되어 있습니다.

>[!NOTE]
>
>플러그인에 대한 클라이언트 라이브러리 폴더를 만듭니다. `/libs/cq/analytics/clientlibs/sitecatalyst/plugins` 폴더에 플러그인을 추가하지 마십시오. 이 방법을 사용하면 AEM을 다시 설치하거나 업그레이드하는 동안 `sitecatalyst.plugins` 범주에 대한 기여도를 덮어쓰지 않습니다.

다음 절차에 따라 플러그인의 클라이언트 라이브러리 폴더를 만듭니다. 이 절차는 한 번만 수행하면 됩니다. 플러그인을 클라이언트 라이브러리 폴더에 추가하려면 다음 절차를 사용합니다.

1. 웹 브라우저에서 CRXDE Lite을 엽니다. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. /apps/my-app/clientlibs 폴더를 마우스 오른쪽 단추로 클릭하고 만들기 > 노드 만들기를 클릭합니다. 다음 속성 값을 입력한 다음 확인을 클릭합니다.

   * 이름: my-plugins와 같은 클라이언트 라이브러리 폴더의 이름입니다.

   * 유형: cq:ClientLibraryFolder

1. 만든 클라이언트 라이브러리 폴더를 선택하고 오른쪽 아래 속성 막대를 사용하여 다음 속성을 추가합니다.

   * 이름: 카테고리
   * 유형: 문자열
   * 값: sitecatalyst.plugins
   * 다중: 선택됨

   편집 창에서 확인 을 클릭하여 속성 값을 확인합니다.

1. 만든 클라이언트 라이브러리 폴더를 마우스 오른쪽 단추로 클릭하고 만들기 > 파일 만들기를 클릭합니다. 파일 이름에 js.txt를 입력한 다음 확인을 누릅니다.

1. 모두 저장을 클릭합니다.

다음 절차를 사용하여 플러그인 코드를 가져와 AEM 저장소에 코드를 저장한 다음 클라이언트 라이브러리 폴더에 코드를 추가합니다.

1. Adobe Analytics 계정을 사용하여 [sc.omniture.com](https://sc.omniture.com/login/)에 로그인합니다.
1. 랜딩 페이지에서 도움말 > 도움말 홈으로 이동합니다.
1. 왼쪽의 목차에서 구현 플러그인 을 클릭합니다.
1. 추가하려는 플러그인에 대한 링크를 클릭하고 페이지가 열리면 플러그인에 대한 JavaScript 소스 코드를 찾은 다음 코드를 선택하고 복사합니다.

1. 클라이언트 라이브러리 폴더를 마우스 오른쪽 단추로 클릭하고 만들기 > 파일 만들기를 클릭합니다. 파일 이름에 통합할 플러그인의 이름 뒤에 .js를 입력하고 확인을 클릭합니다. 예를 들어 getQueryParam 플러그인을 통합하는 경우 파일 이름을 getQueryParam.js로 지정합니다.

   파일을 만들면 편집할 수 있도록 열립니다.

1. 플러그인 JavaScript 코드를 파일에 붙여넣고 모두 저장 을 클릭한 다음 파일을 닫습니다.

1. 클라이언트 라이브러리 폴더에서 js.txt 파일을 엽니다.

1. 새 행에서 플러그인이 포함된 파일의 이름을 추가합니다(예: getQueryParam.js). 그런 다음 모두 저장 을 클릭하고 파일을 닫습니다.

>[!NOTE]
>
>플러그인을 사용할 때 지원 플러그인도 통합해야 합니다. 그렇지 않으면 플러그인 JavaScript은 지원 플러그인의 함수에 대한 호출을 인식하지 못합니다. 예를 들어 getPreviousValue() 플러그인이 제대로 작동하려면 split() 플러그인이 필요합니다.
>
>**js.txt**&#x200B;에도 지원 플러그 인의 이름을 추가해야 합니다.
