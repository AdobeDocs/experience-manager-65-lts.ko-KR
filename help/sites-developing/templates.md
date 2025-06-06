---
title: 템플릿
description: 템플릿은 새 페이지의 기반으로 사용되는 페이지를 만들 때 사용됩니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 3b3cff43-4edc-4250-8e6d-08eb5906ffcd
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 1%

---

# 템플릿{#templates}

템플릿은 AEM의 다양한 지점에서 사용됩니다.

* [페이지를 만들 때 템플릿을 선택합니다](#templates-pages). 이 템플릿은 새 페이지의 기반으로 사용됩니다. 템플릿은 페이지 구조, 초기 콘텐츠 및 사용할 수 있는 [구성 요소](/help/sites-authoring/default-components.md)(디자인 속성)를 정의합니다.

다음 템플릿에 대해 자세히 설명합니다.

* [페이지 템플릿 - 편집 가능](/help/sites-developing/page-templates-editable.md)

## 템플릿 - 페이지 {#templates-pages}

이제 AEM은 페이지를 만들기 위한 두 가지 기본 템플릿 유형을 제공합니다.

>[!NOTE]
>
>템플릿을 사용하여 [페이지 만들기](/help/sites-authoring/managing-pages.md#creating-a-new-page)를 수행하는 경우 페이지 작성자에게는 보이는 차이가 없으며 사용 중인 템플릿 유형도 표시되지 않습니다.

### 편집 가능한 템플릿 {#editable-templates}

이제 편집 가능한 템플릿은 AEM을 사용한 개발 우수 사례로 간주됩니다.

편집 가능한 템플릿의 장점:

* 작성자가 [생성](/help/sites-authoring/templates.md#creating-a-new-template-template-author) 및 [편집](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)할 수 있습니다.

* 템플릿으로 만든 페이지에 대해 다음 사항을 정의할 수 있도록 도입되었습니다.

   * 구조
   * 초기 콘텐츠
   * 콘텐츠 정책

* 새 페이지가 만들어지면 페이지와 템플릿 간에 동적 연결이 유지됩니다. 이 연결은 템플릿 구조의 변경 사항이 해당 템플릿으로 만든 페이지에 반영됨을 의미합니다. 초기 콘텐츠에 대한 변경 사항은 반영되지 않습니다.
* 콘텐츠 정책(템플릿 편집기에서 편집됨)을 사용하여 디자인 속성을 유지합니다(페이지 편집기 내에서 디자인 모드를 사용하지 않음).
* `/conf` 아래에 저장됨
* 자세한 내용은 [편집 가능한 템플릿](/help/sites-developing/page-templates-editable.md)을 참조하십시오.

>[!NOTE]
>
>[편집 가능한 페이지 템플릿을 사용하여 Experience Manager 사이트 개발](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=ko)을 참조하십시오.

### 정적 템플릿 {#static-templates}

정적 템플릿:

* 개발자가 정의 및 구성해야 합니다.
* 여러 버전에서 사용할 수 있었던 AEM의 원래 템플릿 시스템입니다.
* 정적 템플릿은 만들 페이지와 구조가 동일하지만 실제 컨텐츠는 없는 노드의 계층입니다.
* 복사되어 페이지를 만듭니다. 이후에 동적 연결이 존재하지 않습니다.
* [디자인 모드](/help/sites-authoring/default-components-designmode.md)를 사용하여 디자인 속성을 유지합니다.
* `/apps` 아래에 저장됨

>[!NOTE]
>
>AEM 6.5부터는 정적 템플릿을 사용하는 것이 모범 사례로 간주되지 않습니다. 대신 편집 가능한 템플릿을 사용하십시오.
>
>[AEM 현대화](modernization-tools.md) 도구를 사용하면 정적 템플릿에서 편집 가능한 템플릿으로 마이그레이션할 수 있습니다.

### 템플릿 가용성 {#template-availability}

>[!CAUTION]
>
>AEM에서는 **사이트**&#x200B;에서 허용되는 템플릿을 제어할 수 있는 여러 속성을 제공합니다. 하지만 이를 결합하면 추적 및 관리가 어려운 복잡한 규칙이 발생할 수 있다.
>
>따라서 Adobe에서는 다음을 정의하여 간단하게 시작하는 것이 좋습니다.
>
>* `cq:allowedTemplates` 속성만
>
>* 사이트 루트에서만
>
>예를 들어 We.Retail: `/content/we-retail/jcr:content`을(를) 참조하십시오.
>
>`allowedPaths`, `allowedParents` 및 `allowedChildren` 속성을 템플릿에 배치하여 보다 정교한 규칙을 정의할 수도 있습니다. 그러나 허용된 템플릿을 추가로 제한해야 하는 경우 가능한 경우 사이트의 하위 섹션에서 `cq:allowedTemplates` 속성을 추가로 정의하는 것이 *훨씬*&#x200B;입니다.
>
>**페이지 속성**&#x200B;의 **고급** 탭에서 작성자가 `cq:allowedTemplates` 속성을 업데이트할 수 있다는 장점이 있습니다. 다른 템플릿 속성은 (표준) UI를 사용하여 업데이트할 수 없으므로 개발자는 모든 변경 사항에 대한 규칙 및 코드 배포를 유지 관리해야 합니다.

사이트 관리 인터페이스에서 페이지를 만들 때 사용 가능한 템플릿 목록은 새 페이지의 위치와 각 템플릿에 지정된 배치 제한에 따라 다릅니다.

다음 속성은 템플릿 `T`을(를) 사용하여 새 페이지를 `P` 페이지의 자식으로 배치할지 여부를 결정합니다. 이러한 각 속성은 경로와의 일치에 사용되는 0개 이상의 정규 표현식을 포함하는 다중 값 문자열입니다.

* `P`의 `jcr:content` 하위 노드 또는 `P`의 상위 노드의 `cq:allowedTemplates` 속성입니다.

* `T`의 `allowedPaths` 속성입니다.

* `T`의 `allowedParents` 속성입니다.

* `P` 템플릿의 `allowedChildren` 속성입니다.

평가는 다음과 같이 작동합니다.

* `P`(으)로 시작하는 페이지 계층 구조를 오름차순으로 계산하는 동안 비어 있지 않은 첫 번째 `cq:allowedTemplates` 속성이 `T`의 경로에 대해 일치합니다. 일치하는 값이 없으면 `T`이(가) 거부됩니다.

* `T`에 비어 있지 않은 `allowedPaths` 속성이 있지만 `P`의 경로와 일치하는 값이 없으면 `T`이(가) 거부됩니다.

* 위의 두 속성이 모두 비어 있거나 존재하지 않으면 `T`은(는) `P`과(와) 같은 응용 프로그램에 속하지 않는 한 거부됩니다. `T` 경로의 두 번째 수준 이름이 `P` 경로의 두 번째 수준 이름과 동일한 경우에만 `T`이(가) `P`과(와) 동일한 응용 프로그램에 속합니다. 예를 들어 템플릿 `/apps/geometrixx/templates/foo`이(가) 페이지 `/content/geometrixx`과(와) 동일한 애플리케이션에 속합니다.

* `T`에 비어 있지 않은 `allowedParents` 속성이 있지만 `P`의 경로와 일치하는 값이 없으면 `T`이(가) 거부됩니다.

* `P`의 템플릿에 비어 있지 않은 `allowedChildren` 속성이 있지만 `T`의 경로와 일치하는 값이 없으면 `T`이(가) 거부됩니다.

* 다른 모든 경우에는 `T`이(가) 허용됩니다.

다음 다이어그램은 템플리트 평가 프로세스를 보여 줍니다.

![chlimage_1-176](assets/chlimage_1-176.png)

#### 하위 페이지에 사용되는 템플릿 제한 {#limiting-templates-used-in-child-pages}

지정된 페이지에서 하위 페이지를 만드는 데 사용할 수 있는 템플릿을 제한하려면 페이지의 `jcr:content` 노드의 `cq:allowedTemplates` 속성을 사용하여 하위 페이지로 허용할 템플릿 목록을 지정하십시오. 목록의 각 값은 허용된 하위 페이지(예: `/apps/geometrixx/templates/contentpage`)에 대한 템플릿의 절대 경로여야 합니다.

템플릿의 `jcr:content` 노드에서 `cq:allowedTemplates` 속성을 사용하여 이 템플릿을 사용하는 새로 만든 모든 페이지에 이 구성을 적용할 수 있습니다.

템플릿 계층 구조와 관련하여 제한을 더 추가하려면 템플릿의 `allowedParents/allowedChildren` 속성을 사용할 수 있습니다. 그런 다음 템플릿 T에서 만든 페이지가 템플릿 T에서 만든 페이지의 상위/하위 페이지가 되도록 명시적으로 지정할 수 있습니다.
