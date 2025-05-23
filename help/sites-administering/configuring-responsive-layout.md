---
title: 레이아웃 컨테이너 및 레이아웃 모드 구성
description: 레이아웃 컨테이너 및 레이아웃 모드를 구성하는 방법에 대해 알아봅니다.
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
exl-id: 413f15c9-5b51-4d8d-8cf0-3e98608b9d9e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 4%

---

# 레이아웃 컨테이너 및 레이아웃 모드 구성{#configuring-layout-container-and-layout-mode}

레이아웃 컨테이너 및 레이아웃 모드를 구성하는 방법에 대해 알아봅니다.

>[!TIP]
>
>이 문서에서는 AEM의 기능을 구현하는 방법을 설명하는 사이트 관리자 및 개발자를 위한 반응형 디자인에 대한 개요를 제공합니다.
>
>콘텐츠 작성자의 경우 콘텐츠 페이지에서 응답형 디자인 기능을 사용하는 방법에 대한 자세한 내용은 콘텐츠 페이지의 [응답형 레이아웃](/help/sites-authoring/responsive-layout.md) 문서에서 확인할 수 있습니다.

## 개요 {#overview}

[응답형 레이아웃](/help/sites-authoring/responsive-layout.md)은(는) [응답형 웹 디자인](https://en.wikipedia.org/wiki/Responsive_web_design)을 구현하기 위한 메커니즘입니다. 이렇게 하면 사용자가 사용하는 장치에 따라 레이아웃과 차원이 다른 웹 페이지를 만들 수 있습니다.

AEM에서는 메커니즘을 조합하여 페이지에 대한 반응형 레이아웃을 실현합니다.

* [**레이아웃 컨테이너**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode) 구성 요소

  이 구성 요소는 응답형 그리드 내에 구성 요소를 추가 및 배치할 수 있도록 해주는 그리드 단락 시스템을 제공합니다. 페이지의 기본 parsys로 사용하거나 구성 요소 브라우저에서 작성자가 사용할 수 있습니다.

   * 기본 **레이아웃 컨테이너** 구성 요소는 아래에 정의되어 있습니다.

     /libs/wcm/foundation/components/responsivegrid

   * 레이아웃 컨테이너를 정의할 수 있습니다.

      * 사용자가 페이지에 추가할 수 있는 구성 요소입니다.
      * 를 페이지의 기본 parsys로 사용합니다.
      * 둘 다.

        레이아웃 컨테이너를 페이지의 표준으로 사용할 수 있으며, 사용자가 이 내에 레이아웃 컨테이너를 더 추가할 수 있습니다(예: 열 제어 달성).

* **[레이아웃 모드](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
레이아웃 컨테이너를 페이지에 배치하면 **레이아웃** 모드를 사용하여 콘텐츠를 응답형 그리드 내에 배치할 수 있습니다.

* [**에뮬레이터**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
이를 사용하여 구성 요소의 크기를 상호 작용 방식으로 조정하여 디바이스/창 크기에 따라 레이아웃을 재정렬하는 반응형 웹 사이트를 만들고 편집할 수 있습니다. 그러면 사용자는 콘텐츠가 에뮬레이터를 사용하여 어떻게 렌더링되는지 볼 수 있습니다.

이러한 응답형 격자 메커니즘을 사용하여 다음과 같은 작업을 수행할 수 있습니다.

* 장치 레이아웃을 기반으로 달라지는 콘텐츠 동작을 정의하려면 중단점 (장치 그룹화를 나타냄)을 사용하십시오.
* 장치 그룹에 따라 구성 요소를 숨깁니다(구성 요소를 숨길 중단점을 정의하십시오).
* 수평 격자에 맞춤(구성 요소를 격자에 배치하고, 필요에 따라 크기를 변경하고, 언제 구성 요소가 나란히 또는 위/아래에 있도록 축소되거나 리플로우되어야 하는지 정의합니다.)
* 열 컨트롤을 구현할 수 있습니다.

>[!TIP]
>
>Adobe은 응답형 레이아웃의 [GitHub 설명서](https://adobe-marketing-cloud.github.io/aem-responsivegrid/)를 프런트엔드 개발자에게 참조용으로 제공하여 AEM 외부 AEM 그리드를 사용할 수 있도록 합니다. 예를 들어 나중에 사용하기 위해 AEM 사이트에 대한 정적 HTML mock-up을 생성할 때 이를 사용할 수 있습니다.

>[!NOTE]
>
>기본 설치에서 [We.Retail 참조 사이트](/help/sites-developing/we-retail.md)에 대해 응답형 레이아웃이 구성되었습니다. 다른 페이지에 대해 [레이아웃 컨테이너 구성 요소를 활성화](#enable-the-layout-container-component-for-page)합니다.

>[!CAUTION]
>
>**레이아웃 컨테이너** 구성 요소는 클래식 UI에서 사용할 수 있지만, 전체 기능은 터치 사용 UI에서만 사용할 수 있습니다.

## 사이트에 대한 레이아웃 모드 활성화 {#activate-layout-mode-for-your-site}

이러한 절차는 사이트에서 **레이아웃** 모드를 활성화하는 데 사용됩니다.

### 중단점 구성 {#configure-the-breakpoints}

[중단점](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* 응답형 디자인에 사용됩니다.
* 다음을 정의할 수 있습니다.

   * 페이지 템플릿에서 해당 템플릿으로 만든 페이지에 설정이 복사됩니다.
   * 페이지 노드에서 설정이 하위 페이지에 상속됩니다.

* 제목 및 너비 정의:

   * 제목은 전화, 태블릿, 태블릿 등과 같이 필요한 경우 방향을 사용하여 일반 장치 그룹화를 설명합니다.
   * 너비는 일반 장치 그룹화에 대한 최대 너비(픽셀 단위)를 정의합니다. 예를 들어, 중단점 전화기의 너비가 768이라면 전화 디바이스에 사용되는 레이아웃의 최대 너비입니다.

* 에뮬레이터를 사용할 때 페이지 편집기 맨 위에 마커로 표시됩니다.
* 상위 노드 계층에서 상속되며 마음대로 재정의할 수 있습니다.
* 마지막 *구성된* 중단점 위의 모든 항목을 포함하는 기본(기본) 중단점이 있습니다.

CRXDE Lite 또는 XML을 사용하여 정의할 수 있습니다.

>[!NOTE]
>
>새 프로젝트를 설정하는 경우:
>
>* 템플릿에 중단점을 추가합니다.
>
>기존 콘텐츠를 사용하여 기존 프로젝트를 마이그레이션하는 경우 다음을 수행해야 합니다.
>
>* 템플릿에 중단점 추가
>* 기존 페이지에 동일한 중단점 추가
>
>  상속이 작동 중이므로 콘텐츠의 루트 페이지로 제한할 수 있습니다.

#### CRXDE Lite을 사용하여 중단점 구성 {#configuring-breakpoints-using-crxde-lite}

1. CRXDE Lite(또는 이에 해당)를 사용하여 다음 중 하나로 이동합니다.

   * 템플릿 정의.
   * 페이지의 `jcr:content` 노드입니다.

1. `jcr:content`에서 노드를 만듭니다.

   * 이름: `cq:responsive`
   * 유형: `nt:unstructured`

1. 이 아래에서 노드를 만듭니다.

   * 이름: `breakpoints`
   * 유형: `nt:unstructured`

1. 중단점 노드 아래에서 중단점을 원하는 수만큼 만들 수 있습니다. 각 정의는 다음 속성을 갖는 단일 노드입니다.

   * 이름: `<descriptive name>`
   * 유형: `nt:unstructured`
   * 제목: `String` * `<descriptive title seen in Emulator>`*
   * 너비: `Decimal` * `<value of breakpoint>`*

#### XML을 사용하여 중단점 구성 {#configuring-breakpoints-using-xml}

중단점은 적절한 템플릿(또는 콘텐츠) 폴더 아래의 `.context.html`의 `<jcr:content>` 섹션 내에 있습니다.

예제 정의:

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### 응답형 정보 공급자 추가 {#add-a-responsive-information-provider}

>[!NOTE]
>
>페이지 구성 요소가 기초 페이지 구성 요소를 기반으로 하지 않는 경우에만 필요합니다.

다음 `cq:infoProviders` 노드 구조를 상위 페이지 구성 요소에 복사합니다.

`/libs/foundation/components/page/cq:infoProviders/responsive`

## 페이지에 대한 구성 요소 크기 조정 활성화 {#enable-component-resizing-for-the-page}

**레이아웃** 모드에서 구성 요소의 크기를 조정할 수 있으려면 다음 절차가 필요합니다.

### 레이아웃 컨테이너를 기본 Parsys로 설정 {#set-layout-container-as-main-parsys}

페이지의 기본 parsys를 레이아웃 컨테이너로 설정하려면 parsys를 다음과 같이 정의합니다.

`wcm/foundation/components/responsivegrid`

다음 중 하나에서:

* 페이지 구성 요소
* 페이지 템플릿(나중에 사용)

다음 두 예는 정의를 보여 줍니다.

* **HTL:**

  ```html
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP:**

  ```html
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### 반응형 CSS 포함 {#include-the-responsive-css}

#### LESS를 사용하는 중단점용 CSS {#css-for-breakpoints-using-less}

AEM에서는 LESS를 사용하여 필요한 CSS의 일부를 생성합니다. 프로젝트에 이러한 부분을 포함해야 합니다.

또한 추가 구성 및 함수 호출을 제공하려면 [클라이언트 라이브러리](https://experienceleague.adobe.com/docs/?lang=ko)를 만들어야 합니다. 다음 LESS 추출은 프로젝트에 추가해야 하는 최소값의 예입니다.

```css
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

기본 격자선 정의는 다음 위치에 있습니다.

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### 스타일 고려 사항 {#styling-considerations}

응답형 컨테이너 내에 있는 구성 요소의 크기는 응답형 격자 크기에 따라 해당 HTML DOM 요소와 함께 조정됩니다. 따라서 이러한 상황에서는 고정 너비(포함된) DOM 요소의 정의를 피하거나 업데이트하는 것이 좋습니다.

예:

* 전:

   * `width=100px`

* 이후:

   * `max-width=100px`

#### 크기 조정 및 적응형 이미지 규정 준수 {#resizing-and-adaptive-image-compliance}

그리드 내의 구성 요소 크기를 조정하면 다음 리스너가 적절하게 트리거됩니다.

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

응답형 격자에 포함된 응용 이미지의 내용을 올바르게 크기 조정하고 업데이트하려면 `REFRESH_PAGE` 수신자로 설정된 `afterEdit`을(를) 포함된 모든 구성 요소의 `EditConfig` 파일에 추가해야 합니다.

예:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

적응형 이미지 메커니즘은 윈도우의 현재 크기에 대한 정확한 이미지의 선택을 제어하는 스크립트를 통해 이용 가능하게 된다. DOM이 준비된 후 또는 전용 이벤트를 수신할 때 활성화됩니다. 현재 사용자의 작업 결과를 제대로 반영하려면 페이지를 새로 고쳐야 합니다.

>[!CAUTION]
>
>사용자 지정 스타일시트 clientlibs를 작성자 및 게시에서 제대로 작동하려면 헤더의 일부로 로드해야 합니다.

## 페이지에 대한 레이아웃 컨테이너 구성 요소 활성화 {#enable-the-layout-container-component-for-page}

이러한 작업을 통해 작성자는 **레이아웃 컨테이너** 구성 요소의 인스턴스를 페이지로 끌 수 있습니다.

### 페이지 편집을 위해 레이아웃 컨테이너 구성 요소 활성화 {#enable-the-layout-container-component-for-page-editing}

작성자가 컨텐츠 페이지에 응답형 그리드를 더 추가할 수 있도록 하려면 페이지에 대해 레이아웃 컨테이너 구성 요소를 활성화해야 합니다. 다음 중 하나를 사용하여 이 작업을 수행할 수 있습니다.

* **작성 환경**

  [디자인 모드](/help/sites-authoring/default-components-designmode.md)를 사용하여 페이지에 대한 **레이어 컨테이너** 구성 요소를 활성화합니다.

* **구성 요소 정의**

  구성 요소를 정의할 때 `allowedComponent` 또는 정적 포함을 사용하십시오.

### 레이아웃 컨테이너의 그리드 구성 {#configure-the-grid-of-the-layout-container}

레이아웃 컨테이너의 각 특정 인스턴스에 사용할 수 있는 열 수를 구성할 수 있습니다.

1. **작성 환경**

   레이아웃 컨테이너의 각 특정 인스턴스에 사용할 수 있는 열 수를 구성할 수 있습니다.

   이렇게 하려면 [디자인 모드](/help/sites-authoring/default-components-designmode.md)를 사용한 다음 필요한 컨테이너에 대한 디자인 대화 상자를 엽니다. 여기에서 위치 지정 및 크기 조정에 사용할 수 있는 열의 수를 지정할 수 있습니다. 기본값은 12입니다.

1. **XML**

   응답형 격자에 대한 정의는 다음에서 지정합니다.

   `etc/design/<*your-project-name*>/.content.xml`

   다음 매개 변수를 정의할 수 있습니다.

   * 사용 가능한 열 수:

      * `columns="{String}8"`

   * 현재 구성 요소에 추가할 수 있는 구성 요소:

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`

## 중첩된 응답형 격자 {#nested-responsive-grids}

프로젝트의 요구 사항을 지원하기 위해 응답형 그리드를 중첩해야 하는 경우가 있을 수 있습니다. 그러나 Adobe이 권장하는 모범 사례는 구조를 최대한 평평하게 유지하는 것입니다.

중첩된 응답형 격자를 사용하지 않을 수 없는 경우에는 다음을 확인하십시오.

* 모든 컨테이너(컨테이너, 탭, 아코디언 등)에는 `layout = responsiveGrid` 속성이 있습니다.
* 컨테이너 계층 구조에서 `layout = simple` 속성을 혼합하지 마십시오.

페이지 템플릿의 모든 구조적 컨테이너가 여기에 포함됩니다.

내부 컨테이너의 열 번호는 외부 컨테이너의 열 번호보다 커서는 안 됩니다. 다음 예제는 이 조건을 충족합니다. 기본(데스크탑) 화면의 경우 외부 컨테이너의 열 번호가 8이면 내부 컨테이너의 열 번호는 4입니다.

>[!BEGINTABS]

>[!TAB 노드 구조 예]

```text
container
  @layout = responsiveGrid
  cq:responsive
    default
      @offset = 0
      @width = 8
  container
  @layout = responsiveGrid
    cq:responsive
      default
        @offset = 0
        @width = 4
    text
      @text =" Text Column 1"
```

>[!TAB 결과 HTML 예제]

```html
<div class="container responsivegrid aem-GridColumn--default--none aem-GridColumn aem-GridColumn--default--8 aem-GridColumn--offset--default--0">
  <div id="container-c9955c233c" class="cmp-container">
    <div class="aem-Grid aem-Grid--8 aem-Grid--default--8 ">
      <div class="container responsivegrid aem-GridColumn--default--none aem-GridColumn aem-GridColumn--offset--default--0 aem-GridColumn--default--4">
        <div id="container-8414e95866" class="cmp-container">
          <div class="aem-Grid aem-Grid--4 aem-Grid--default--4 ">
            <div class="text aem-GridColumn aem-GridColumn--default--4">
              <div data-cmp-data-layer="..." id="text-1234567890" class="cmp-text">
                <p>Text Column 1</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
```

>[!ENDTABS]
