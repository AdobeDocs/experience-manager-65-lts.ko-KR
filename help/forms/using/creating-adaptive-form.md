---
title: 적응형 양식을 만드는 방법
description: ' [!DNL Experience Manager Forms]을(를) 사용하여 적응형 양식을 만드는 방법을 알아봅니다. 적응형 양식은 정보 수집 및 처리를 간소화하는 반응형 HTML 5 양식입니다. 양식 데이터 모델, XFA 양식 템플릿, XML 또는 JSON 스키마를 기반으로 적응형 양식을 만드는 방법에 대해 자세히 알아보십시오.'
role: User, Developer
level: Beginner
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
exl-id: 5d81781b-bb79-4b85-bba6-2ac67829bfcf
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1984'
ht-degree: 8%

---

# 적응형 양식 만들기 {#creating-an-adaptive-form}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ko)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=ko) |
| AEM 6.5 | 이 문서 |

## 적응형 양식 만들기 {#strong-create-an-adaptive-form-strong}

다음 단계에 따라 적응형 양식을 만듭니다.

1. `https://'[server]:[port]'/<custom-context-if-any>.`에서 [!DNL Experience Manager Forms] 작성자 인스턴스에 액세스

1. Experience Manager 로그인 페이지에서 자격 증명을 입력합니다.

   로그인 후 왼쪽 상단 모서리에서 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;를 선택합니다.

   >[!NOTE]
   >
   >기본 설치의 경우 로그인은 `admin`이고 암호는 `admin`입니다.

1. **[!UICONTROL 만들기]**&#x200B;를 선택하고 **[!UICONTROL 적응형 양식]**&#x200B;을 선택하세요.
1. 템플릿을 선택하는 옵션이 나타납니다. 템플릿에 대한 자세한 내용은 [적응형 양식 템플릿](creating-adaptive-form.md#p-adaptive-form-templates-p)을 참조하세요. 템플릿을 선택하여 선택하고 다음을 선택합니다.
1. &#39;속성 추가&#39; 옵션이 표시됩니다. 다음 속성 필드에 대한 값을 지정합니다. 제목 및 이름 필드는 필수입니다.

   * **[!UICONTROL 제목:]** 양식의 표시 이름을 지정합니다. 제목은 [!DNL Experience Manager Forms] 사용자 인터페이스에서 형식을 식별하는 데 도움이 됩니다.
   * **[!UICONTROL 이름:]** 양식의 이름을 지정합니다. 이름이 지정된 노드가 저장소에서 만들어집니다. 제목 입력이 시작되면 이름 필드 값이 자동으로 생성됩니다. 제안 값을 변경할 수 있습니다. 이름 필드에는 영숫자 문자, 하이픈 및 밑줄만 포함될 수 있습니다. 잘못된 모든 입력은 하이픈으로 대체됩니다.
   * **[!UICONTROL 설명:]** 양식에 대한 자세한 정보를 지정합니다.
   * **[!UICONTROL 태그:]** 적응형 양식을 고유하게 식별하는 태그를 지정합니다. 태그는 양식 검색에 도움이 됩니다. 태그를 만들려면 **[!UICONTROL 태그]** 상자에 새 태그 이름을 입력하십시오.

1. 다음 양식 모델 중 하나를 기반으로 적응형 양식을 만들 수 있습니다.

   * [양식 데이터 모델](#fdm)
   * [XFA 양식 템플릿](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [XML 또는 JSON 스키마](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * 없음 또는 양식 모델 없음

   **[!UICONTROL 속성 추가]** 페이지의 **[!UICONTROL 양식 모델]** 탭에서 구성할 수 있습니다. 기본적으로 선택된 양식 모델은 **[!UICONTROL 없음]**&#x200B;입니다.

1. **[!UICONTROL 만들기]**&#x200B;를 선택합니다. 적응형 양식이 만들어지고 편집할 양식을 여는 대화 상자가 나타납니다.

   모든 속성을 지정했으면 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 적응형 양식이 만들어지고 편집할 양식을 여는 대화 상자가 나타납니다.

   모든 속성을 지정했으면 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 적응형 양식이 만들어지고 편집할 양식을 여는 대화 상자가 나타납니다.

1. **[!UICONTROL 열기]**&#x200B;를 선택하여 새로 만든 양식을 새 탭에서 엽니다. 편집할 양식이 열리고 템플릿에서 사용할 수 있는 콘텐츠가 표시됩니다. 또한 요구 사항에 따라 새로 만든 양식을 사용자 정의할 수 있는 사이드바가 표시됩니다.

   적응형 양식 유형에 따라 연결된 XFA 양식 템플릿, XML 스키마 또는 JSON 스키마에 있는 양식 요소가 사이드바의 **[!UICONTROL 콘텐츠 브라우저]**&#x200B;에서 **[!UICONTROL 데이터 모델 개체]** 탭에 표시됩니다. 이러한 요소를 드래그 앤 드롭하여 적응형 양식을 작성할 수도 있습니다.

   적응형 양식 작성 인터페이스 및 사용 가능한 구성 요소에 대한 자세한 내용은 [적응형 양식 작성 소개](introduction-forms-authoring.md)를 참조하십시오.

   >[!NOTE]
   >
   >브라우저에서 팝업 창을 사용하여 새로 만든 양식을 새 탭에서 열 수 있습니다.

## 양식 데이터 모델을 기반으로 적응형 양식 만들기 {#fdm}

[[!DNL Experience Manager Forms] 데이터 통합](data-integration.md)을 통해 여러 데이터 소스를 통합하고 해당 엔터티와 서비스를 함께 가져와서 양식 데이터 모델을 만들 수 있습니다. JSON 스키마의 확장입니다. 양식 데이터 모델을 사용하여 적응형 양식을 만들 수 있습니다. 양식 데이터 모델에 구성된 엔티티 또는 데이터 모델 개체는 양식 작성에 데이터 모델 개체로 사용할 수 있습니다. 각 데이터 소스에 바인딩되며 양식을 미리 채우고 제출된 데이터를 각 데이터 소스에 다시 작성하는 데 사용됩니다. 적응형 양식 규칙을 사용하여 양식 데이터 모델에 구성된 서비스를 호출할 수도 있습니다.

적응형 양식을 작성하기 위해 양식 데이터 모델을 사용하려면

1. 속성 추가 화면의 양식 모델 탭에서 **[!UICONTROL 다음에서 선택]** 드롭다운 목록에서 **[!UICONTROL 양식 데이터 모델]**&#x200B;을(를) 선택합니다.

   ![create-af-1-1](assets/create-af-1-1.png)

1. **[!UICONTROL 양식 데이터 모델 선택]**&#x200B;을 확장하려면 선택하십시오. 사용 가능한 모든 양식 데이터 모델이 나열됩니다.

   데이터 모델에서 을(를) 선택합니다.

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>적응형 양식에 대한 양식 데이터 모델을 변경할 수도 있습니다. 자세한 단계는 [적응형 양식의 양식 모델 속성 편집](#edit-form-model)을 참조하십시오.

## XFA 양식 템플릿을 기반으로 적응형 양식 만들기 {#create-an-adaptive-form-based-on-an-xfa-form-template}

XFA 양식 템플릿을 다른 용도로 사용하여 적응형 양식을 만들 수 있습니다. XFA 양식 템플릿을 업로드하고 적응형 양식과 연결하려면 다음을 수행하십시오. 양식 템플릿(XFA 양식) 요소는 적응형 양식 작성 시 콘텐츠 파인더에서 사용할 수 있습니다. 콘텐츠 파인더에서 양식에 양식 템플릿 요소를 드래그 앤 드롭할 수 있습니다.

<!-- >>[!NOTE]
>
>[Upload the XFA Form Template](get-xdp-pdf-documents-aem.md) to AEM Forms before you start creating an adaptive form based on the form template.

Do the following to use an XFA form template as form model for your adaptive form:

1. On the **[!UICONTROL Add Properties]** page, open the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, from the drop-down list, select **[!UICONTROL Form Templates]**. All the form templates that are uploaded to the repository via AEM Forms UI are listed for selection. Select a template from the list.

   ![Associate XFA Form Template with an Adaptive Form](assets/form_model_xfa_associate.png)
**Figure:** *Selecting a form template*

   >[!NOTE]
   >
   >You can also change the form template for an adaptive form. For detailed steps, see [Edit Form Model properties of an adaptive form](#edit-form-model). -->

## XML 또는 JSON 스키마를 기반으로 적응형 양식 만들기 {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML 및 JSON 스키마는 조직의 백엔드 시스템이 데이터를 생성하거나 사용하는 구조를 나타냅니다. 스키마를 적응형 양식에 연결하고 해당 요소를 사용하여 적응형 양식에 다이내믹 콘텐츠를 추가할 수 있습니다. 스키마의 요소는 적응형 양식을 작성하는 콘텐츠 브라우저의 데이터 모델 개체 탭에서 사용할 수 있습니다. 스키마 요소를 끌어 놓아 양식을 작성할 수 있습니다.

적응형 양식 작성을 위해 XML 또는 JSON 스키마를 디자인하는 방법을 이해하려면 다음 문서를 참조하십시오.

* [XML 스키마를 사용하여 적응형 양식 만들기](adaptive-form-xml-schema-form-model.md)
* [JSON 스키마를 사용하여 적응형 양식 만들기](adaptive-form-json-schema-form-model.md)

XML 또는 JSON 스키마를 적응형 양식의 양식 모델로 사용하려면 다음을 수행하십시오.

1. 적응형 양식 만들기 페이지의 **[!UICONTROL 속성 추가]** 단계에서 **[!UICONTROL 양식 모델]** 탭을 선택합니다.
1. 양식 모델 탭의 **[!UICONTROL 다음에서 선택]** 드롭다운 필드에서 **[!UICONTROL 스키마]**&#x200B;을(를) 선택합니다.

1. **[!UICONTROL 스키마 선택]**&#x200B;을 선택하고 다음 중 하나를 수행합니다.

   * **[!UICONTROL 디스크에서 업로드]** - 이 옵션을 선택하고 스키마 정의 업로드 를 선택하여 파일 시스템에서 XML 스키마 또는 JSON 스키마를 찾아 업로드합니다. 업로드된 스키마 파일은 양식과 함께 있으며 다른 적응형 양식에 액세스할 수 없습니다.
   * **[!UICONTROL 저장소에서 검색]** - 저장소에서 사용할 수 있는 스키마 정의 파일 목록에서 선택하려면 이 옵션을 선택하십시오. XML 또는 JSON 스키마 파일을 양식 모델로 선택합니다. 선택한 스키마는 참조로 양식과 연결되고, 다른 적응형 양식에서 사용할 수 있습니다.

   >[!CAUTION]
   >
   >JSON 스키마 파일 이름이 **.schema.json**(으)로 끝나는지 확인하십시오. 예: mySchema.schema.json

   ![XML 또는 JSON 스키마 선택](assets/upload-schema.png)
   **그림:** *XML 또는 JSON 스키마 선택*

1. (XML 스키마만 해당) XML 스키마를 선택하거나 업로드한 후 적응형 양식에 매핑할 선택한 XSD 파일의 루트 요소를 지정합니다.

   ![XSD 루트 요소 선택](assets/xsd-root-element.png)
   **그림:** *XSD 루트 요소 선택*

>[!NOTE]
>
>적응형 양식에 대한 스키마를 변경할 수도 있습니다. 자세한 단계는 [적응형 양식의 양식 모델 속성 편집](#edit-form-model)을 참조하십시오.

## 적응형 양식 템플릿 {#adaptive-form-templates}

템플릿은 기본 구조를 제공하고 적응형 양식의 모양(레이아웃 및 스타일)을 정의합니다. 여기에는 특정 속성 및 콘텐츠 구조를 포함하는 미리 형식이 지정된 구성 요소가 있습니다. <!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

또한 템플릿 편집기를 사용하여 나만의 템플릿을 만들 수도 있습니다. 템플릿 작업에 대한 자세한 내용은 [적응형 양식 템플릿](template-editor.md)을 참조하세요.

>[!NOTE]
>
>편집을 위해 고급 템플릿을 사용하여 만든 적응형 양식을 열면 오류 메시지가 나타납니다. 고급 템플릿에는 서명 단계 구성 요소가 있으며 기본적으로 Adobe Sign이 활성화되어 있습니다. 오류를 해결하려면 [Adobe Sign 클라우드 구성](adobe-sign-integration-adaptive-forms.md)을 만들고 선택하고 [서명자 구성](working-with-adobe-sign.md#addsignerstoanadaptiveform)을 하세요.

## 적응형 양식의 양식 모델 속성 편집 {#edit-form-model}

적응형 양식은 양식 모델 없이(양식 모델에 대해 없음 옵션 사용) 또는 양식 템플릿, XML 스키마 또는 JSON 스키마와 같은 양식 모델 또는 양식 데이터 모델을 사용하여 만들어집니다. 적응형 양식의 양식 모델을 없음에서 다른 양식 모델로 변경할 수 있습니다. 양식 모델을 기반으로 하는 적응형 양식의 경우 동일한 양식 모델에 대해 다른 양식 템플릿, XML 스키마, JSON 스키마 또는 양식 데이터 모델을 선택할 수 있습니다. 그러나 양식 모델 간에 변경할 수는 없습니다.

1. 적응형 양식을 선택하고 **속성** 아이콘을 선택합니다.
1. **[!UICONTROL 양식 모델]** 탭을 열고 다음 중 하나를 수행합니다.

   * 적응형 양식에 양식 모델이 없는 경우 다른 양식 모델을 선택할 수 있으며, 이에 따라 양식 템플릿, XML 또는 JSON 스키마 또는 양식 데이터 모델을 선택할 수 있습니다.
   * 적응형 양식이 양식 모델을 기반으로 하는 경우 동일한 양식 모델에 대해 다른 양식 템플릿, XML 또는 JSON 스키마 또는 양식 데이터 모델을 선택할 수 있습니다.

1. 속성을 저장하려면 **[!UICONTROL 저장]**&#x200B;을(를) 선택하십시오.

## 적응형 양식 자동 저장 {#auto-save-an-adaptive-form}

기본적으로 적응형 양식의 콘텐츠는 저장 버튼을 누르는 것과 같은 사용자 작업 시 저장됩니다. 이벤트 또는 시간 간격에 따라 콘텐츠 저장을 자동으로 시작하도록 적응형 양식을 구성할 수도 있습니다. 자동 저장 옵션은 다음 경우에 유용합니다.

* 익명 및 로그인한 사용자를 위한 콘텐츠 자동 저장
* 사용자 개입 없이 또는 최소한의 양식 콘텐츠 저장
* 사용자 이벤트를 기반으로 양식의 콘텐츠 저장 시작
* 지정된 시간 간격 후 반복적으로 양식 콘텐츠 저장

### 적응형 양식에 대해 자동 저장 활성화 {#enable-auto-save-for-an-adaptive-form}

기본적으로 자동 저장 옵션은 활성화되어 있지 않습니다. 적응형 양식의 자동 저장 탭에서 자동 저장 옵션을 활성화할 수 있습니다. 자동 저장 탭에는 다른 몇 가지 구성 옵션도 있습니다. 적응형 양식에 대해 자동 저장 옵션을 활성화하고 구성하려면 다음 단계를 수행하십시오.

1. 속성의 자동 저장 섹션에 액세스하려면 구성 요소를 선택한 다음 ![필드 수준](assets/field-level.png) > **[!UICONTROL 적응형 양식 컨테이너]**&#x200B;를 선택하고 ![cmpr](assets/cmppr.png)을 선택합니다.
1. **[!UICONTROL 자동 저장]** 섹션에서 자동 저장 옵션을 **[!UICONTROL 활성화]**&#x200B;합니다.
1. **[!UICONTROL 적응형 양식 이벤트]** 상자에서 1 또는 TRUE를 지정하여 양식을 브라우저에 로드할 때 자동으로 양식 저장을 시작합니다. 이벤트에 대해 트리거되고 true를 반환하면 양식의 콘텐츠 저장을 시작하는 조건식을 지정할 수도 있습니다.
1. [트리거]를 지정합니다. 자동 저장은 구성에 따라 트리거됩니다. 옵션은 다음과 같습니다.

   * **[!UICONTROL 시간 기준:]** 특정 시간 간격을 기준으로 콘텐츠 저장을 시작하려면 옵션을 선택하십시오.
   * **[!UICONTROL 이벤트 기반:]** 이벤트가 트리거될 때 콘텐츠 저장을 시작하려면 옵션을 선택하십시오.

   트리거를 선택하면 전략 구성 상자가 활성화됩니다. 전략 구성 상자를 사용하면 다음 작업을 수행할 수 있습니다.

   * **[!UICONTROL 시간 기반]** 트리거를 선택하는 경우 시간 간격을 지정하십시오.
   * **[!UICONTROL 이벤트 기반]** 트리거를 선택하는 경우 이벤트 이름을 지정하십시오.

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. (시간 기반 자동 저장만 해당) 다음 단계를 수행하여 시간 기반 자동 저장에 대한 옵션을 구성합니다.

   1. **[!UICONTROL 이 간격에 자동 저장]** 상자에서 시간 간격을 초 단위로 지정합니다. 간격 상자에 지정된 초 수가 경과하면 양식이 반복적으로 저장됩니다.

1. (이벤트 기반 자동 저장만 해당) 다음 단계를 수행하여 이벤트 기반 자동 저장에 대한 옵션을 구성합니다.

   1. **[!UICONTROL 이 이벤트 후 자동 저장]** 상자에서 [GuideBridge](https://helpx.adobe.com/kr/aem-forms/6/javascript-api/GuideBridge.html) 이벤트를 지정합니다. 표현식이 TRUE로 평가될 때마다 양식이 저장됩니다.

1. (선택 사항) 익명 사용자에 대한 콘텐츠를 자동으로 저장하려면 **[!UICONTROL 익명 사용자에 대한 자동 저장 사용]** 옵션을 선택하고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >익명 사용자에 대해 자동 저장 옵션이 작동하려면 모든 사용자가 양식을 미리 보고, 확인하고, 서명할 수 있도록 Forms 일반 구성 서비스를 구성해야 합니다.
   >
   >서비스를 구성하려면 `https://'[server]:[port]'system/console/configMgr`의 Adobe Experience Manager 웹 콘솔 구성으로 이동하여 **[!UICONTROL Forms 일반 구성 서비스]**&#x200B;를 편집하여 **[!UICONTROL 허용]** 필드에서 **[!UICONTROL 모든 사용자]** 옵션을 선택한 다음 구성을 저장합니다.


## AEM 적응형 양식의 이름을 변경하는 방법 {#rename-an-AEM-Adaptive-Form}

적응형 양식의 이름을 변경하려면 다음 단계를 수행하십시오.

1. AEM Forms 사용자 인터페이스에서 적응형 양식을 선택합니다.
1. 위쪽 레일에 있는 **속성**&#x200B;을 클릭합니다.

   ![속성](/help/forms/using/assets/rename-form-properties.png)

1. 아래 그림과 같이 **제목** 탭에서 양식 이름을 변경합니다.
1. **저장 후 닫기**&#x200B;를 클릭합니다.

   ![AEM 적응형 양식 이름 바꾸기](/help/forms/using/assets/rename-form-title.png)
