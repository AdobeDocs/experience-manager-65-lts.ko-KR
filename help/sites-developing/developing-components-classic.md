---
title: Adobe Experience Manager 구성 요소 개발(클래식 UI)
description: 클래식 UI는 ExtJS를 사용하여 구성 요소의 디자인을 제공하는 위젯을 만듭니다. HTL은 Adobe Experience Manager(AEM)에 권장되는 스크립팅 언어가 아닙니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: d44e6ea8-b4e5-4ed7-a6d0-de1da2709e18
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '2340'
ht-degree: 1%

---

# Adobe Experience Manager(AEM) 구성 요소 개발(클래식 UI){#developing-aem-components-classic-ui}

클래식 UI는 ExtJS를 사용하여 구성 요소의 디자인을 제공하는 위젯을 만듭니다. 이러한 위젯의 특성으로 인해 구성 요소가 클래식 UI와 [터치 사용 UI](/help/sites-developing/developing-components.md)와 상호 작용하는 방법에는 몇 가지 차이점이 있습니다.

>[!NOTE]
>
>구성 요소 개발의 여러 측면은 클래식 UI와 터치 사용 UI 모두에 공통적이므로, 이 페이지에서 클래식 UI의 구체적인 사항을 다루려면 **이 페이지를 사용하기 전에 [AEM 구성 요소 - 기본 사항](/help/sites-developing/components-basics.md)을 읽어야 합니다**.

>[!NOTE]
>
>HTML 템플릿 언어(HTL)와 JSP를 모두 클래식 UI에 대한 구성 요소 개발에 사용할 수 있지만, 이 페이지에서는 JSP를 사용한 개발을 보여 줍니다. 이는 전적으로 클래식 UI 내에서 JSP를 사용한 내역이 원인입니다.
>
>이제 HTL이 AEM에 권장되는 스크립팅 언어입니다. 메서드를 비교하려면 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ko) 및 [AEM 구성 요소 개발](/help/sites-developing/developing-components.md)을 참조하십시오.

## 구조 {#structure}

구성 요소의 기본 구조는 [AEM 구성 요소 - 기본 사항](/help/sites-developing/components-basics.md#structure) 페이지에서 다룹니다. 이 페이지는 터치 패널 및 클래식 UI를 모두 적용합니다. 새 구성 요소에서 터치 지원 UI에 대한 설정을 사용할 필요가 없는 경우에도 기존 구성 요소에서 상속할 때 설정을 인식하는 데 도움이 될 수 있습니다.

## JSP 스크립트 {#jsp-scripts}

JSP 스크립트 또는 서블릿을 사용하여 구성 요소를 렌더링할 수 있습니다. Sling의 요청 처리 규칙에 따라 기본 스크립트의 이름은 다음과 같습니다.

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

JSP 스크립트 파일 `global.jsp`은(는) 구성 요소를 렌더링하는 데 사용되는 모든 JSP 스크립트 파일에 대한 특정 개체(즉, 콘텐츠 액세스)에 대한 빠른 액세스를 제공하는 데 사용됩니다.

따라서 `global.jsp`은(는) `global.jsp`에 제공된 하나 이상의 개체가 사용되는 모든 구성 요소 렌더링 JSP 스크립트에 포함되어야 합니다.

기본 `global.jsp`의 위치는 다음과 같습니다.

`/libs/foundation/global.jsp`

>[!NOTE]
>
>CQ 5.3 및 이전 버전에서 사용한 `/libs/wcm/global.jsp` 경로는 이제 사용되지 않습니다.

### global.jsp, 사용된 API 및 Taglib의 함수 {#function-of-global-jsp-used-apis-and-taglibs}

다음은 기본값 `global.jsp`에서 제공된 가장 중요한 개체를 나열합니다.

요약:

* `<cq:defineObjects />`

   * `slingRequest` - 래핑된 요청 개체( `SlingHttpServletRequest`).
   * `slingResponse` - 래핑된 응답 개체( `SlingHttpServletResponse`).
   * `resource` - Sling 리소스 개체( `slingRequest.getResource();`)입니다.
   * `resourceResolver` - Sling Resource Resolver 개체( `slingRequest.getResoucreResolver();`)입니다.
   * `currentNode` - 요청에 대해 확인된 JCR 노드입니다.
   * `log` - 기본 로거().
   * `sling` - Sling 스크립트 도우미입니다.
   * `properties` - 주소가 지정된 리소스(`resource.adaptTo(ValueMap.class);`)의 속성입니다.
   * `pageProperties` - 주소가 지정된 리소스의 페이지 속성입니다.
   * `pageManager` - AEM 콘텐츠 페이지에 액세스하기 위한 페이지 관리자(`resourceResolver.adaptTo(PageManager.class);`)입니다.
   * `component` - 현재 AEM 구성 요소의 구성 요소 개체입니다.
   * `designer` - 디자인 정보를 검색하기 위한 Designer 개체(`resourceResolver.adaptTo(Designer.class);`)입니다.
   * `currentDesign` - 주소가 지정된 리소스의 디자인입니다.
   * `currentStyle` - 주소가 지정된 리소스의 스타일입니다.

### 컨텐츠 액세스 {#accessing-content}

AEM WCM의 콘텐츠에 액세스하는 방법에는 세 가지가 있습니다.

* `global.jsp`에 도입된 속성 개체를 통해:

  속성 개체는 ValueMap([Sling API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html) 참조)의 인스턴스이며, 현재 리소스의 모든 속성을 포함합니다.

  예: 페이지 구성 요소의 렌더링 스크립트에 사용되는 `String pageTitle = properties.get("jcr:title", "no title");`.

  예: 표준 단락 구성 요소의 렌더링 스크립트에 사용되는 `String paragraphTitle = properties.get("jcr:title", "no title");`.

* `global.jsp`에 도입된 `currentPage` 개체를 통해:

  `currentPage` 개체는 페이지의 인스턴스입니다([AEM API](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/Page.html) 참조). 페이지 클래스는 콘텐츠에 액세스하는 몇 가지 메서드를 제공합니다.

  예: `String pageTitle = currentPage.getTitle();`

* `global.jsp`에 도입된 `currentNode` 개체를 통해:

  `currentNode` 개체는 노드의 인스턴스입니다([JCR API](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html) 참조). `getProperty()` 메서드로 노드의 속성에 액세스할 수 있습니다.

  예: `String pageTitle = currentNode.getProperty("jcr:title");`

## JSP 태그 라이브러리 {#jsp-tag-libraries}

CQ 및 Sling 태그 라이브러리를 사용하면 템플릿 및 구성 요소의 JSP 스크립트에 사용할 특정 기능에 액세스할 수 있습니다.

자세한 내용은 [태그 라이브러리](/help/sites-developing/taglib.md) 문서를 참조하십시오.

## 클라이언트측 HTML 라이브러리 사용 {#using-client-side-html-libraries}

최신 웹 사이트는 복잡한 JavaScript 및 CSS 코드로 구동되는 클라이언트측 처리에 크게 의존합니다. 이 코드의 제공을 구성하고 최적화하는 것은 복잡한 문제가 될 수 있습니다.

이 문제를 해결하는 데 도움이 되도록 AEM에서는 클라이언트측 코드를 저장소에 저장하고, 범주로 구성하고, 각 코드 범주가 클라이언트에 제공되는 시기와 방법을 정의할 수 있는 **클라이언트측 라이브러리 폴더**&#x200B;를 제공합니다. 그런 다음 클라이언트측 라이브러리 시스템은 올바른 코드를 로드하기 위해 최종 웹 페이지에서 올바른 링크를 생성합니다.

자세한 내용은 [클라이언트측 HTML 라이브러리 사용](/help/sites-developing/clientlibs.md) 문서를 참조하십시오.

## 대화 상자 {#dialog}

작성자가 콘텐츠를 추가하고 구성하려면 구성 요소에 대화 상자가 필요합니다.

자세한 내용은 [AEM 구성 요소 - 기본 사항](/help/sites-developing/components-basics.md#dialogs)을 참조하십시오.

## 비헤이비어 편집 구성 {#configuring-the-edit-behavior}

구성 요소의 편집 동작을 구성할 수 있습니다. 여기에는 구성 요소에 사용할 수 있는 작업, 즉석 편집기의 특성 및 구성 요소의 이벤트와 관련된 리스너와 같은 속성이 포함됩니다. 이 구성은 터치 지원 UI와 클래식 UI에 공통되지만, 특정 차이점이 있습니다.

`cq:Component` 형식의 구성 요소 노드 아래에 `cq:EditConfig` 형식의 `cq:editConfig` 노드를 추가하고 특정 속성 및 자식 노드를 추가하여 구성 요소의 [편집 동작이 구성](/help/sites-developing/components-basics.md#edit-behavior)됩니다.

## ExtJS 위젯 사용 및 확장 {#using-and-extending-extjs-widgets}

자세한 내용은 [ExtJS 위젯 사용 및 확장](/help/sites-developing/widgets.md)을 참조하십시오.

## ExtJS 위젯에 xtype 사용 {#using-xtypes-for-extjs-widgets}

자세한 내용은 [xtypes 사용](/help/sites-developing/xtypes.md)을 참조하십시오.

## 새 구성 요소 개발 {#developing-new-components}

이 섹션에서는 고유한 구성 요소를 만들고 단락 시스템에 추가하는 방법에 대해 설명합니다.

기존 구성 요소를 복사한 다음 원하는 대로 변경하는 것이 가장 빠른 시작 방법입니다.

구성 요소를 개발하는 방법의 예는 [텍스트 및 이미지 구성 요소 확장 - 예제](#extending-the-text-and-image-component-an-example)에 자세히 설명되어 있습니다.

### 새 구성 요소 개발(기존 구성 요소 적용) {#develop-a-new-component-adapt-existing-component}

기존 구성 요소를 기반으로 AEM의 새 구성 요소를 개발하려면 구성 요소를 복사하고, 새 구성 요소에 대한 JavaScript 파일을 만든 다음, AEM에서 액세스할 수 있는 위치에 저장할 수 있습니다([구성 요소 및 기타 요소 사용자 지정](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements) 참조).

1. CRXDE Lite을 사용하여에 구성 요소 폴더를 만듭니다.

   / `apps/<myProject>/components/<myComponent>`

   libs에서와 같이 노드 구조를 다시 만든 다음 텍스트 구성 요소와 같은 기존 구성 요소의 정의를 복사합니다. 예를 들어 텍스트 구성 요소 사본을 사용자 정의하려면 다음을 수행합니다.

   * 변환 전: `/libs/foundation/components/text`
   * `/apps/myProject/components/text`에

1. 새 이름을 반영하도록 `jcr:title`을(를) 수정하십시오.
1. 새 구성 요소 폴더를 열고 필요한 사항을 변경합니다. 또한 폴더에서 관련 없는 정보를 삭제합니다.

   다음과 같이 변경할 수 있습니다.

   * 대화 상자에 필드 추가

      * `cq:dialog` - 터치 사용 UI에 대한 대화 상자
      * `dialog` - 클래식 UI 대화 상자

   * `.jsp` 파일 바꾸기(새 구성 요소 뒤에 이름 지정)
   * 또는 원하는 경우 전체 구성 요소를 완전히 다시 작업

   예를 들어 표준 텍스트 구성 요소의 복사본을 가져오면 대화 상자에 필드를 추가한 다음 `.jsp`을(를) 업데이트하여 입력한 내용을 처리할 수 있습니다.

   >[!NOTE]
   >
   >다음에 대한 구성 요소:
   >
   >* 터치 사용 UI에서 [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 구성 요소를 사용합니다.
   >* 클래식 UI는 [ExtJS 위젯](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)을 사용합니다.

   >[!NOTE]
   >
   >클래식 UI에 대해 정의된 대화 상자는 터치 사용 UI 내에서 작동합니다.
   >
   >터치 지원 UI에 대해 정의된 대화 상자가 클래식 UI 내에서 작동하지 않습니다.
   >
   >인스턴스 및 작성자 환경에 따라 구성 요소에 대해 두 가지 유형의 대화 상자를 모두 정의할 수 있습니다.

1. 다음 노드 중 하나가 존재해야 하며 새 구성 요소가 나타나도록 제대로 초기화되어야 합니다.

   * `cq:dialog` - 터치 사용 UI에 대한 대화 상자
   * `dialog` - 클래식 UI 대화 상자
   * `cq:editConfig` - 구성 요소가 편집 환경에서 작동하는 방식(예: 끌어서 놓기)
   * `design_dialog` - 디자인 모드 대화 상자(클래식 UI만 해당)

1. 다음 중 하나를 수행하여 단락 시스템에서 새 구성 요소를 활성화합니다.

   * CRXDE Lite을 사용하여 `/etc/designs/geometrixx/jcr:content/contentpage/par` 노드의 속성 구성 요소에 값 `<path-to-component>`(예: `/apps/geometrixx/components/myComponent`)을(를) 추가합니다.
   * [단락 시스템에 새 구성 요소 추가](#adding-a-new-component-to-the-paragraph-system-design-mode)의 지침에 따라

1. AEM WCM에서 웹 사이트의 페이지를 열고 구성 요소가 제대로 작동하는지 확인하기 위해 만든 유형의 단락을 삽입합니다.

>[!NOTE]
>
>페이지 로드에 대한 타이밍 통계를 보려면 URL에 `?debugClientLibs=true`이(가) 설정된 Ctrl-Shift-U를 사용할 수 있습니다.

### 단락 시스템에 새 구성 요소 추가(디자인 모드) {#adding-a-new-component-to-the-paragraph-system-design-mode}

구성 요소가 개발되면 단락 시스템에 구성 요소를 추가하여 작성자가 페이지를 편집할 때 구성 요소를 선택하고 사용할 수 있습니다.

1. 작성 환경에서 단락 시스템을 사용하는 페이지(예: `<contentPath>/Test.html`)에 액세스합니다.
1. 다음 중 하나를 수행하여 디자인 모드로 전환합니다.

   * URL의 끝에 `?wcmmode=design`을(를) 추가하고 다시 액세스합니다. 예:

     `<contextPath>/ Test.html?wcmmode=design`

   * Sidekick에서 디자인 클릭

   이제 디자인 모드에 있으며 단락 시스템을 편집할 수 있습니다.

1. 편집을 클릭합니다.

   단락 시스템에 속하는 구성 요소 목록이 표시됩니다. 새 구성 요소도 나열됩니다.

   구성 요소를 활성화(또는 비활성화)하여 페이지 편집 시 작성자에게 제공되는 구성 요소를 결정할 수 있습니다.

1. 구성 요소를 활성화한 다음 일반 편집 모드로 돌아가 사용할 수 있는지 확인합니다.

### 텍스트 및 이미지 구성 요소 확장 - 예제 {#extending-the-text-and-image-component-an-example}

이 섹션에서는 구성 가능한 이미지 배치 기능을 사용하여 널리 사용되는 텍스트 및 이미지 표준 구성 요소를 확장하는 방법에 대한 예를 제공합니다.

텍스트 및 이미지 구성 요소에 대한 확장을 사용하면 편집자가 구성 요소의 기존 기능을 모두 사용할 수 있고 이미지의 배치를 지정하는 추가 옵션이 있습니다.

* 텍스트 왼쪽(현재 비헤이비어 및 새 기본값)
* 오른쪽은

이 구성 요소를 확장한 후 구성 요소의 대화 상자를 통해 이미지 배치를 구성할 수 있습니다.

이 연습에서는 다음 기술에 대해 설명합니다.

* 기존 구성 요소 노드 복사 및 해당 메타데이터 수정
* 상위 대화 상자에서 위젯의 상속을 포함하여 구성 요소의 대화 상자 수정
* 구성 요소의 스크립트를 수정하여 새 기능 구현

>[!NOTE]
>
>이 예제는 클래식 UI를 대상으로 합니다.

>[!NOTE]
>
>이 예제는 더 이상 AEM과 함께 제공되지 않고 We.Retail로 대체된 Geometrixx 샘플 콘텐츠를 기반으로 합니다. Geometrixx을 다운로드하고 설치하는 방법은 [We.Retail 참조 구현](/help/sites-developing/we-retail.md#we-retail-geometrixx) 문서를 참조하십시오.

#### 기존 textimage 구성 요소 확장 {#extending-the-existing-textimage-component}

구성 요소를 만들려면 표준 textimage 구성 요소를 기준으로 사용하고 수정합니다. Geometrixx AEM WCM 예제 애플리케이션에 새 구성 요소를 저장합니다.

1. textimage를 대상 노드 이름으로 사용하여 `/libs/foundation/components/textimage`에서 Geometrixx 구성 요소 폴더 `/apps/geometrixx/components`(으)로 표준 textimage 구성 요소를 복사합니다. (구성 요소로 이동하고 마우스 오른쪽 단추를 클릭한 다음 복사 를 선택하고 대상 디렉토리로 이동하여 구성 요소를 복사합니다.)

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. 이 예를 간단하게 유지하려면 복사한 구성 요소로 이동한 후 다음 하위 노드를 제외한 새 textimage 노드의 모든 하위 노드를 삭제합니다.

   * 대화 상자 정의: `textimage/dialog`
   * 구성 요소 스크립트: `textimage/textimage.jsp`
   * 구성 노드 편집(자산 드래그 앤 드롭 허용): `textimage/cq:editConfig`

   >[!NOTE]
   >
   >대화 상자 정의는 UI에 따라 다릅니다.
   >
   >* 터치 사용 UI: `textimage/cq:dialog`
   >* 클래식 UI: `textimage/dialog`

1. 구성 요소 메타데이터 편집:

   * 구성 요소 이름

      * `jcr:description`을(를) `Text Image Component (Extended)`(으)로 설정
      * `jcr:title`을(를) `Text Image (Extended)`(으)로 설정

   * 구성 요소가 사이드 킥에 나열되는 그룹(그대로 유지)

      * `componentGroup`을(를) `General`(으)로 설정

   * 새 구성 요소의 상위 구성 요소(표준 Textimage 구성 요소)

      * `sling:resourceSuperType`을(를) `foundation/components/textimage`(으)로 설정

   이 단계 후에 구성 요소 노드는 다음과 같이 표시됩니다.

   ![chlimage_1-60](assets/chlimage_1-60a.png)

1. 이미지의 구성 노드 편집의 `sling:resourceType` 속성(속성: `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`)을 `geometrixx/components/textimage.`(으)로 변경합니다.

   이렇게 하면 페이지의 구성 요소에 이미지를 끌어 놓으면 확장된 textimage 구성 요소의 `sling:resourceType` 속성이 `geometrixx/components/textimage.`(으)로 설정됩니다.

1. 새 옵션을 포함하도록 구성 요소의 대화 상자를 수정합니다. 새 구성 요소는 원본과 동일한 대화 상자의 부분을 상속합니다. **고급** 탭을 확장하여 **이미지 위치** 드롭다운 목록을 추가하고 **왼쪽** 및 **오른쪽** 옵션을 사용하는 것뿐입니다.

   * `textimage/dialog`속성을 변경하지 마십시오.

   `textimage/dialog/items`에 textimage 대화 상자의 4개 탭을 나타내는 tab1 ~ tab4의 하위 노드가 4개 있는 방법을 확인합니다.

   * 처음 두 탭(tab1 및 tab2)의 경우:

      * xtype을 cqinclude(표준 구성 요소에서 상속)로 변경합니다.
      * 각각 값이 `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json` 및 `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json`인 경로 속성을 추가하십시오.
      * 다른 모든 속성 또는 하위 노드를 제거합니다.

   * Tab3의 경우:

      * 속성 및 하위 노드를 변경하지 않고 그대로 둡니다.
      * `tab3/items`, `cq:Widget` 유형의 노드 위치에 필드 정의 추가
      * 새 `tab3/items/position`노드에 대해 다음 속성(문자열 유형)을 설정합니다.

         * `name`: `./imagePosition`
         * `xtype`: `selection`
         * `fieldLabel`: `Image Position`
         * `type`: `select`

      * 이미지 배치에 대한 두 가지 선택 사항을 나타내려면 `cq:WidgetCollection` 유형의 하위 노드 `position/options`을(를) 추가하고 그 아래에 `nt:unstructured` 유형의 o1 및 o2인 두 개의 노드를 만듭니다.
      * `position/options/o1` 노드의 경우 `text`을(를) `Left`(으)로, `value`을(를) `left.`(으)로 설정합니다.
      * `position/options/o2` 노드의 경우 `text`을(를) `Right`(으)로, `value`을(를) `right`(으)로 설정합니다.

   * Tab4를 삭제합니다.

   이미지 위치는 콘텐츠에서 `textimage` 단락을 나타내는 노드의 `imagePosition` 속성으로 유지됩니다. 이러한 단계를 수행하면 구성 요소 대화 상자가 다음과 같이 표시됩니다.

   ![chlimage_1-61](assets/chlimage_1-61a.png)

1. 새 매개 변수를 추가로 처리하여 구성 요소 스크립트 `textimage.jsp`을(를) 확장합니다.

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   강조된 코드 조각 *%>&lt;div class=&quot;image&quot;>&lt;%*&#x200B;을(를) 이 태그에 대한 사용자 지정 스타일을 생성하는 새 코드로 바꾸려고 합니다.

   ```xml
   // todo: add new CSS class for the 'right image' instead of using
   // the style attribute
   String style="";
        if (properties.get("imagePosition", "left").equals("right")) {
             style = "style=\"float:right\"";
        }
        %><div <%= style %> class="image"><%
   ```

1. 구성 요소를 저장소에 저장합니다. 구성 요소를 테스트할 준비가 되었습니다.

#### 새 구성 요소 확인 {#checking-the-new-component}

구성 요소가 개발되면 단락 시스템에 구성 요소를 추가하여 작성자가 페이지를 편집할 때 구성 요소를 선택하고 사용할 수 있습니다. 다음 단계를 통해 구성 요소를 테스트할 수 있습니다.

1. Geometrixx에서 영어/회사와 같은 페이지를 엽니다.
1. Sidekick에서 디자인 을 클릭하여 디자인 모드로 전환합니다.
1. 페이지 중간에 있는 단락 시스템에서 편집 을 클릭하여 단락 시스템 디자인을 편집합니다. 단락 시스템에 배치할 수 있는 구성 요소 목록이 표시되고 새로 개발된 구성 요소인 텍스트 이미지(확장) 가 포함되어야 합니다. 단락 시스템을 선택하고 확인 을 클릭하여 단락 시스템에 대해 활성화합니다.
1. 편집 모드로 다시 전환합니다.
1. 텍스트 이미지(확장) 단락을 단락 시스템에 추가하고 샘플 콘텐츠로 텍스트 및 이미지를 초기화합니다. 변경 사항을 저장합니다.
1. 텍스트 및 이미지 단락의 대화 상자를 열고 고급 탭에서 이미지 위치를 오른쪽 로 변경하고 확인 을 클릭하여 변경 사항을 저장합니다.
1. 단락은 오른쪽에 있는 이미지로 렌더링됩니다.
1. 이제 구성 요소를 사용할 준비가 되었습니다.

구성 요소는 회사 페이지의 단락에 콘텐츠를 저장합니다.

### 이미지 구성 요소의 업로드 기능 비활성화 {#disable-upload-capability-of-the-image-component}

이 기능을 비활성화하려면 표준 이미지 구성 요소를 기준으로 사용하고 수정합니다. Geometrixx 예제 애플리케이션에 새 구성 요소를 저장합니다.

1. 이미지를 대상 노드 이름으로 사용하여 `/libs/foundation/components/image`의 표준 이미지 구성 요소를 Geometrixx 구성 요소 폴더 `/apps/geometrixx/components`(으)로 복사합니다.

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. 구성 요소 메타데이터 편집:

   * **jcr:title**&#x200B;을(를) `Image (Extended)`(으)로 설정

1. 다음으로 이동 `/apps/geometrixx/components/image/dialog/items/image`.
1. 속성 추가:

   * **이름**: `allowUpload`
   * **유형**: `String`
   * **값**: `false`

   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. **모두 저장**&#x200B;을 클릭합니다. 구성 요소를 테스트할 준비가 되었습니다.
1. Geometrixx에서 영어/회사와 같은 페이지를 엽니다.
1. 디자인 모드로 전환하고 이미지(확장)를 활성화합니다.
1. 편집 모드로 다시 전환하고 단락 시스템에 추가합니다. 다음 그림에서는 원본 이미지 구성 요소와 만든 이미지 구성 요소의 차이점을 확인할 수 있습니다.

   원본 이미지 구성 요소:

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   새 이미지 구성 요소:

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. 이제 구성 요소를 사용할 준비가 되었습니다.
