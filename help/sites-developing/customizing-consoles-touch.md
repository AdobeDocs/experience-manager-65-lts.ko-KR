---
title: 콘솔 사용자 지정
description: AEM은 작성 인스턴스의 콘솔을 사용자 지정할 수 있는 다양한 메커니즘을 제공합니다
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 2a94ea8d-2919-4f30-be31-ce559493805d
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 22%

---

# 콘솔 사용자 지정 {#customizing-the-consoles}

>[!CAUTION]
>
>이 문서에서는 터치 기능이 지원되는 최신 UI에서 콘솔을 사용자 지정하는 방법에 대해 설명하며 클래식 UI에는 적용되지 않습니다.

AEM에서는 작성 인스턴스의 콘솔(및 [페이지 작성 기능](/help/sites-developing/customizing-page-authoring-touch.md))을 사용자 지정할 수 있는 다양한 메커니즘을 제공합니다.

* Clientlibs
Clientlibs를 사용하면 기본 구현을 확장하여 새로운 기능을 구현하는 동시에 표준 함수, 개체 및 메서드를 재사용할 수 있습니다. 사용자 지정할 때 `/apps.`에서 고유한 clientlib을 만들 수 있습니다. 예를 들어 사용자 지정 구성 요소에 필요한 코드를 저장할 수 있습니다.

* 오버레이
오버레이는 노드 정의를 기반으로 하며, 이를 통해 표준 기능(`/libs`의)을 사용자 지정된 기능(`/apps`의)과 오버레이할 수 있습니다. Sling 리소스 병합으로 상속이 허용되므로 오버레이를 만들 때 원본의 1:1 사본이 필요하지 않습니다.

여러 가지 방법으로 AEM 콘솔을 확장할 수 있습니다. 아래에 소량의 선택 항목이 있습니다(높은 수준에서).

>[!NOTE]
>
>자세한 내용은 다음을 참조하십시오.
>
>* [clientlibs](/help/sites-developing/clientlibs.md)을(를) 사용하고 만드는 중입니다.
>* [오버레이](/help/sites-developing/overlays.md)를 사용하고 만드는 중입니다.
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/index.html)
>


>[!CAUTION]
>
>***은(는) `/libs` 경로에서 아무 것도 변경하지 말아야***&#x200B;합니다.
>
>이는 다음에 인스턴스를 업그레이드할 때 `/libs`의 콘텐츠가 덮어쓰기되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수도 있음).
>
>구성 및 기타 변경에 권장되는 방법은 다음과 같습니다.
>
>1. `/apps` 아래에 필요한 항목(즉, `/libs`에 존재하는 항목)을 다시 만듭니다.
>
>1. `/apps` 내에서 변경
>

예를 들어 `/libs` 구조 내의 다음 위치를 오버레이할 수 있습니다.

* 콘솔 (Granite UI 페이지 기반의 모든 콘솔) - 예:

   * `/libs/wcm/core/content`

>[!NOTE]
>
>추가 팁과 도구는 기술 자료 문서인 [AEM TouchUI 문제 해결](https://experienceleague.adobe.com/ko/docs/experience-cloud-kcs/kbarticles/ka-16935)을 참조하십시오.

## 콘솔의 기본 보기 사용자 정의 {#customizing-the-default-view-for-a-console}

콘솔의 기본 보기(열, 카드, 목록)를 사용자 정의할 수 있습니다.

1. 아래에서 필요한 항목을 오버레이하여 뷰의 순서를 변경할 수 있습니다.

   `/libs/wcm/core/content/sites/jcr:content/views`

   첫 번째 항목이 기본값이 됩니다.

   사용 가능한 노드는 다음과 같이 사용 가능한 보기 옵션과 관련이 있습니다.

   * `column`
   * `card`
   * `list`

1. 예를 들어 목록에 대한 오버레이에서 다음을 수행합니다.

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   다음 속성을 정의합니다.

   * **이름**: `sling:orderBefore`
   * **유형**: `String`
   * **값**: `column`

### 도구 모음에 새 작업 추가 {#add-new-action-to-the-toolbar}

1. 고유한 구성 요소를 빌드하고 사용자 지정 작업에 해당하는 클라이언트 라이브러리를 포함할 수 있습니다. 예를 들어 다음 위치의 **Twitter로 승격** 작업을 참조하십시오.

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   이를 다음과 같은 콘솔의 도구 모음 항목에 연결할 수 있습니다.

   `/apps/<yourProject>/admin/ext/launches`

   예를 들어 선택 모드에서 다음과 같은 항목입니다.

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 도구 모음 작업을 특정 그룹으로 제한 {#restrict-a-toolbar-action-to-a-specific-group}

1. 사용자 정의 렌더링 조건을 사용하여 표준 작업을 오버레이하고, 렌더링되기 전에 충족되어야 하는 특정 조건을 부과할 수 있습니다.

   예를 들어, 그룹에 따라 renderconditions를 제어하는 구성 요소를 만듭니다.

   `/apps/myapp/components/renderconditions/group`

1. 사이트 콘솔의 사이트 만들기 작업에 적용하려면 다음을 수행합니다.

   `/libs/wcm/core/content/sites`

   다음과 같이 오버레이를 만듭니다.

   `/apps/wcm/core/content/sites`

1. 그런 다음 작업에 대한 rendercondition을 추가합니다.

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   이 노드의 속성을 사용하여 특정 작업을 수행할 수 있는 `groups`를 정의할 수 있습니다(예: `administrators`).

### 목록 보기에서 열 사용자 정의 {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>이 기능은 텍스트 필드의 열에 최적화되어 있습니다. 다른 데이터 형식의 경우 `/apps`에 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer`을(를) 오버레이할 수 있습니다.

목록 보기에서 열을 사용자 정의하려면 다음 작업을 수행하십시오.

1. 사용 가능한 열 목록을 오버레이합니다.

   * 다음 노드에서:

     ```
            /apps/wcm/core/content/common/availablecolumns
     ```

   * 새 열을 추가하거나 기존 열을 제거합니다.

   자세한 내용은 [오버레이 사용(및 Sling 리소스 병합)](/help/sites-developing/overlays.md)을 참조하십시오.

1. 선택적으로:

   * 추가 데이터를 연결하려면 [PageInforProvider](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageInfoProvider.html)에

     `pageInfoProviderType` 속성입니다.

   예를 들어 아래 (GitHub에서) 첨부된 클래스/번들을 참조하십시오.

1. 이제 목록 보기의 열 구성자에서 열을 선택할 수 있습니다.

### 리소스 필터링 {#filtering-resources}

콘솔을 사용할 때 일반적인 사용 사례는 사용자가 리소스(예: 페이지, 구성 요소, 에셋 등)에서 선택해야 하는 경우입니다. 예를 들어 작성자가 항목을 선택해야 하는 목록 형식을 취할 수 있습니다.

목록을 적당한 크기로 유지하고 사용 사례와도 관련되게 하려면 필터를 사용자 정의 조건자 형태로 구현할 수 있습니다. 자세한 내용은 [페이지 작성 사용자 지정 - 리소스 필터링](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources)을 참조하십시오.
