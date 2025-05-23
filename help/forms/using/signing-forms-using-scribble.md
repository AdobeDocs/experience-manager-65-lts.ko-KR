---
title: 스크리블 서명을 사용하여 양식에 전자 서명 적용
description: 스크리블 서명을 사용하여 AEM 적응형 Forms에 서명하는 방법에 대해 알아봅니다. 낙서 서명 및 서명 단계를 사용하여 양식에 서명을 그릴 수 있습니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 9d1a22da-2eb3-4c79-8c4d-4d0a3ed7fe3b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 9%

---

# 스크리블 서명을 사용하여 양식에 전자 서명 적용{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ko)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>


| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble.html?lang=ko) |
| AEM 6.5 | 이 문서 |


**스크리블 서명** 구성 요소와 **서명 단계** 구성 요소를 사용하여 적응형 양식에 스크리블 서명을 그릴 수 있습니다. 서명 단계 구성 요소는 적응형 양식의 PDF 버전을 표시합니다. 서명 단계 구성 요소를 사용하려면 기록 문서 옵션을 활성화하거나 양식 템플릿 기반 적응형 양식이 필요합니다.

![스크리블 서명 대화 상자](/help/forms/using/assets/scribble-signature.png)

## 서명 창에서 사용할 수 있는 다양한 옵션

* **A:** 캔버스에 서명을 그리려면 **페인트 브러시** 아이콘을 클릭하세요.
* **B:** 캔버스에서 서명을 지우려면 **지우기** 아이콘을 클릭하십시오.
* **C:** **지리적 위치** 아이콘을 클릭하여 서명과 함께 지리적 위치를 추가하십시오.
* **D:** 캔버스에 이름을 입력하려면 **키보드** 아이콘을 클릭하십시오.

스크리블 서명 창에서 완료![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 선택하면 서명을 편집할 수 없습니다. 서명을 편집하려면 현재 서명을 무시하고 위의 [페인트 브러쉬/키보드] 옵션을 사용하여 다시 서명해야 합니다.

**구성** ![구성](assets/configure.png) 아이콘을 선택하여 스크리블 서명 캔버스의 종횡비를 설정할 수 있습니다.
* 스크리블 서명 캔버스의 종횡비가 1보다 작은 경우 지리적 위치 정보가 스크리블 서명 캔버스의 맨 아래에 추가됩니다.

* 스크리블 서명 캔버스의 종횡비가 1보다 큰 경우 지리적 위치 정보가 스크리블 서명 캔버스의 오른쪽에 추가됩니다.

![스크리블 서명-하단](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>서명은 항상 PNG 형식으로 저장됩니다.
>

## 스크리블 서명을 사용하도록 적응형 양식 구성 {#configure-an-adaptive-form-to-use-scribble-signature}

1. 기록 문서 만들기 옵션을 활성화하거나 양식 템플릿 기반 적응형 양식을 만듭니다. 단계별 정보는 [적응형 양식 만들기](../../forms/using/creating-adaptive-form.md)를 참조하십시오.
1. 구성 요소 브라우저에서 **스크리블 서명** 구성 요소를 적응형 양식으로 드래그 앤 드롭하십시오.
1. **구성** ![구성](assets/configure.png) 아이콘을 선택합니다. 속성 브라우저를 열고 스크리블 서명 구성 요소의 속성을 표시합니다. 스크리블 서명 구성 요소의 속성을 구성합니다.
1. 구성 요소 브라우저의 서명 단계 구성 요소를 적응형 양식으로 드래그 앤 드롭합니다.

   >[!NOTE]
   >
   >서명 단계 구성 요소는 양식에 사용할 수 있는 전체 너비를 차지합니다. 서명 단계 구성 요소가 포함된 섹션에는 다른 구성 요소가 없는 것이 좋습니다.
   >

1. 콘텐츠 브라우저에서 **양식 컨테이너**&#x200B;를 선택하고 **구성** ![구성](/help/forms/using/assets/configure.png) 아이콘을 선택합니다. 속성 브라우저를 열고 적응형 양식 컨테이너 속성을 표시합니다. **적응형 양식 컨테이너** > **전자 서명**(으)로 이동한 다음 **Adobe Sign 활성화** 옵션의 선택을 해제합니다. 완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 선택하여 변경 사항을 저장합니다.

   >[!NOTE]
   >
   >적응형 양식에 서명 단계 구성 요소를 추가하면 Adobe Sign 활성화 옵션이 자동으로 선택됩니다.
   >

1. **구성** ![구성](assets/configure.png) 아이콘을 선택합니다. 속성 브라우저를 열고 서명 단계 속성을 표시합니다. 다음 속성을 구성합니다.

   * **요소 이름**: 구성 요소의 이름을 지정하십시오.

   * **제목:** 구성 요소의 고유한 제목을 지정합니다.
   * **템플릿 메시지:** 서명 PDF을 로드하는 동안 표시할 메시지를 지정합니다. Adobe Sign 서비스는 서명 PDF을 준비하고 로드하는 데 시간이 다소 소요됩니다.
   * **서명 서비스:** **스크리블 서명** 옵션을 선택하십시오.

   * **CSS 클래스**: 클라이언트 라이브러리의 CSS 클래스(있는 경우)를 지정합니다. CSS 클래스 대신 [테마](../../forms/using/themes.md) 및 [인라인 스타일](../../forms/using/inline-style-adaptive-forms.md)을(를) 사용하십시오.

   완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 선택하여 변경 사항을 저장합니다. 서명이 구성되었습니다.

   이제 양식을 채울 때 PDF 버전의 적응형 양식이 표시되고 PDF 문서에 서명할 수 있는 옵션이 제공됩니다. 자세한 내용은 [스크리블 서명을 사용하여 적응형 양식에 서명](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)을 참조하세요.

## 스크리블 서명을 사용하여 적응형 양식에 서명 {#sign-an-adaptive-form-using-scribble-signature}

1. 적응형 양식을 작성하고 서명 단계 페이지에 도달하면 서명 화면이 표시됩니다.

   ![스크리블 서명 대화 상자](/help/forms/using/assets/esignscribblesign.jpg)

1. **[!UICONTROL 서명]**&#x200B;을 클릭합니다. 낙서 기호 대화 상자가 나타납니다. 양식에 서명하고 완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 클릭하여 서명을 저장합니다.

   ![스크리블 서명 대화 상자](/help/forms/using/assets/scribblewidget.png)

1. 완료 를 클릭하여 서명 프로세스를 완료합니다.

   ![서명 프로세스를 완료합니다](/help/forms/using/assets/scribblecomplete.jpg)

서명이 양식에 추가되고 양식 컨트롤이 다음 패널로 이동합니다.
