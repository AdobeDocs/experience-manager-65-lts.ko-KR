---
title: 적응형 양식 단편
description: 적응형 양식은 적응형 양식에서 사용할 패널 또는 필드 그룹과 같은 양식 세그먼트를 만드는 메커니즘을 제공합니다. 기존 패널을 조각으로 저장할 수도 있습니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 7da165ac-2039-4ac8-810d-fbe6f771453a
source-git-commit: c03b3e3e4526530715718b68804ac26d2562bdb8
workflow-type: tm+mt
source-wordcount: '2372'
ht-degree: 6%

---

# 적응형 양식 단편{#adaptive-form-fragments}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/adaptive-form-fragments-core-components.html?lang=ko) |
| AEM 6.5 | 이 문서 |

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ko)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

모든 양식은 특정 목적을 위해 디자인되었지만 대부분의 양식에는 이름 및 주소, 가족 세부 사항 및 소득 세부 사항과 같은 개인 세부 사항을 제공하는 것과 같은 일부 일반적인 세그먼트가 있습니다. 양식 개발자는 새 양식을 만들 때마다 이러한 공통 세그먼트를 만들어야 합니다.

적응형 양식은 패널이나 필드 그룹과 같은 양식 세그먼트를 한 번만 만들어 적응형 양식 간에 재사용할 수 있는 편리한 메커니즘을 제공합니다. 이러한 재사용 가능한 독립 세그먼트를 적응형 양식 조각이라고 합니다.

>[!NOTE]
>
> [양식 조각 구성 요소의 구성 대화 상자 및 디자인 대화 상자](https://experienceleague.adobe.com/ko/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/adaptive-form-fragment)를 통해 사용자의 조각 환경을 손쉽게 사용자 지정할 수 있습니다.

## 조각 만들기 {#create-a-fragment}

적응형 양식 조각을 처음부터 만들거나 기존 적응형 양식에 패널을 조각으로 저장할 수 있습니다.

### 처음부터 조각 만들기 {#create-fragment-from-scratch}

1. https://[*호스트 이름*]:[*포트*]/aem/forms.html에서 AEM Forms 작성자 인스턴스에 로그인합니다.
1. **만들기 > 적응형 양식 조각**&#x200B;을 클릭합니다.
1. 조각의 제목, 이름, 설명 및 태그를 지정합니다.

   >[!NOTE]
   >
   >조각에 고유한 이름을 지정해야 합니다. 같은 이름의 다른 조각이 있는 경우 조각을 만들 수 없습니다.

1. 클릭하여 **양식 모델** 탭을 열고 **다음에서 선택** 드롭다운 메뉴에서 조각에 대해 다음 모델 중 하나를 선택합니다.

   * **없음**: 양식 모델을 사용하지 않고 처음부터 조각을 만들도록 지정합니다.

     >[!NOTE]
     >
     > 핵심 구성 요소를 기반으로 하는 적응형 Forms에서는 양식에서 단일 양식 조각을 여러 번 사용할 수 있습니다. none 기반 양식 조각과 schema 기반 양식 조각을 모두 지원합니다.

   * **양식 서식 파일**: AEM Forms에 업로드된 XDP 서식 파일을 사용하여 조각을 만들도록 지정합니다. 조각의 양식 모델로 적절한 XDP 템플릿을 선택합니다.

   ![양식 템플릿을 모델로 사용하여 적응형 양식 만들기](assets/form-template-model.png)

   선택한 양식 템플릿에서 조각으로 표시된 하위 양식도 표시됩니다. 드롭다운 목록에서 적응형 양식 조각에 대한 하위 양식을 선택할 수 있습니다.

   ![지정된 양식 서식 파일에서 하위 양식 선택](assets/fragment-subform.png)

   또한 드롭다운 상자에서 하위 양식에 대한 SOM 표현식을 지정하여 양식 템플릿에서 조각으로 표시되지 않은 하위 양식을 사용하여 적응형 양식 조각을 만들 수 있습니다.

   * **XML 스키마**: AEM Forms에 업로드된 XML 스키마를 사용하여 조각을 만들도록 지정합니다. 사용 가능한 XML 스키마를 업로드하거나 조각의 양식 모델로 선택할 수 있습니다.

   ![XML 스키마를 기반으로 하는 적응형 양식 조각을 모델로 만들기](assets/xml-schema-model.png)

   드롭다운 상자에서 선택한 스키마에 있는 complexType을 선택하여 적응형 양식 조각을 만들 수도 있습니다.

   ![지정한 XML 스키마 모델에서 복합 형식을 선택하십시오](assets/complex-type.png)

1. **만들기**&#x200B;를 클릭한 다음 **열기**&#x200B;를 클릭하여 기본 템플릿으로 편집 모드에서 조각을 엽니다.

편집 모드에서 적응형 양식 구성 요소를 AEM 사이드 킥에서 조각으로 드래그 앤 드롭할 수 있습니다. 적응형 양식 구성 요소에 대한 자세한 내용은 [적응형 양식 작성 소개](../../forms/using/introduction-forms-authoring.md)를 참조하십시오.

또한 조각에 대한 양식 모델로 XML 스키마 또는 XDP 양식 템플릿을 선택한 경우 양식 모델 계층을 표시하는 새 탭이 콘텐츠 파인더에 나타납니다. 양식 모델 요소를 조각으로 드래그 앤 드롭할 수 있습니다. 추가된 양식 모델 요소는 연결된 XDP 또는 XSD의 원래 속성을 유지하면서 양식 구성 요소로 변환됩니다.

### 패널을 조각으로 저장 {#save-panel-as-a-fragment}

1. 적응형 양식 조각으로 저장할 패널이 포함된 적응형 양식을 엽니다.
1. 패널 도구 모음에서 **[!UICONTROL 조각으로 저장]**&#x200B;을 클릭합니다. 조각으로 저장 대화 상자가 열립니다.

   >[!NOTE]
   >
   >조각으로 저장하는 패널에 하위 패널이 포함된 경우 결과 조각에 하위 패널이 포함됩니다.

1. 조각 생성 대화 상자에서 다음 정보를 지정합니다.

   * **이름**: 조각의 이름입니다. 기본값은 패널의 요소 이름입니다. 필수 필드입니다.

     >[!NOTE]
     >
     >조각에 고유한 이름을 지정해야 합니다. 같은 이름의 다른 조각이 있는 경우 조각을 만들 수 없습니다.

   * **제목**: 조각의 제목입니다. 기본값은 패널 제목입니다.

   * **설명**: 조각에 대한 설명입니다.

   * **태그**: 조각에 대한 태그 메타데이터입니다.

   * **대상 경로**: 조각이 저장되는 저장소 경로입니다. 경로를 지정하지 않으면 조각 이름과 동일한 이름의 노드가 적응형 양식을 포함하는 노드 옆에 만들어집니다. 조각은 이 노드에 저장됩니다.

   * **양식 모델**: 적응형 양식의 양식 모델에 따라 이 필드에는 **XML 스키마**, **양식 서식 파일** 또는 **없음**&#x200B;이 표시됩니다. 편집할 수 없는 필드입니다.

   * **조각 모델 루트**: XSD 기반 적응형 양식에만 나타납니다. 조각 모델의 루트를 지정합니다. 드롭다운에서 **/** 또는 XSD 복합 형식을 선택할 수 있습니다. 복잡한 유형을 조각 모델 루트로 선택하는 경우에만 다른 적응형 양식에서 조각을 재사용할 수 있습니다.
**/**&#x200B;을(를) 조각 모델 루트로 선택하면 루트의 전체 XSD 트리가 적응형 양식 데이터 모델 탭에 표시됩니다. 복합 유형 조각 모델 루트의 경우 적응형 양식 데이터 모델 탭에 선택한 복합 유형의 하위 항목만 표시됩니다. 조각을 만들고 **조각 모델 루트**(으)로 복합 형식을 선택하면 해당 복합 형식이 사용되는 모든 형식(동일한 양식 내 또는 여러 양식 간에)으로 사용할 수 있습니다.

   * **XSD 참조**: XSD 기반 적응형 양식에만 나타납니다. XML 스키마의 위치를 표시합니다.

   * **XDP Ref**: XDP 기반 적응형 양식에만 나타납니다. XDP 양식 템플릿의 위치를 표시합니다.

   ![조각 저장](assets/save-fragment.png)

   조각으로 저장 대화 상자

1. **확인**&#x200B;을 클릭합니다.

   패널은 저장소의 지정된 위치 또는 기본 위치에 저장됩니다. 적응형 양식에서 패널은 조각의 스냅샷으로 대체됩니다. 아래 그림과 같이 일반 정보 패널과 해당 하위 패널인 개인 정보 및 주소는 조각으로 저장됩니다.

   조각을 편집하려면 패널 도구 모음에서 **[!UICONTROL 에셋 편집]**&#x200B;을 클릭합니다. 조각이 편집 모드의 새 탭이나 창에서 열립니다.

   ![조각 편집](assets/edit-fragment.png)

## 조각을 사용한 작업 {#working-with-fragments}

### 조각 모양 구성 {#configure-fragment-appearance}

적응형 양식에 삽입하는 모든 조각은 자리 표시자 이미지로 나타납니다. 이 자리 표시자는 조각에 최대 10개의 하위 패널 제목을 표시합니다. 자리 표시자 이미지 대신 전체 조각을 표시하도록 AEM Forms을 구성할 수 있습니다.

양식에서 전체 조각을 표시할 수 있도록 다음 단계를 수행합니다.

1. https:[*host*]:[*port*]/system/console/configMgr의 AEM 웹 콘솔 구성 페이지로 이동합니다.

1. **[!UICONTROL 적응형 양식 및 대화형 통신 웹 채널 구성]**&#x200B;을 검색하여 선택하여 편집 모드로 엽니다.
1. **[!UICONTROL 조각 대신 자리 표시자 활성화]** 확인란을 비활성화하면 자리 표시자 이미지가 아닌 전체 조각을 표시할 수 있습니다.

### 적응형 양식에 조각 삽입 {#insert-a-fragment-in-an-adaptive-form}

만든 적응형 양식 조각은 AEM 콘텐츠 파인더의 적응형 양식 조각 탭에 표시됩니다. 적응형 양식에 적응형 양식 단편을 삽입하려면 다음 작업을 수행하십시오.

1. 적응형 양식 단편을 삽입할 적응형 양식을 편집 모드로 엽니다.
1. 사이드바에서 **Assets** ![에셋-브라우저](assets/assets-browser.png)을 클릭합니다. 에셋 브라우저의 드롭다운에서 **적응형 양식 조각**&#x200B;을 선택합니다.

   모든 적응형 양식 조각 또는 필터를 해당 양식 모델(양식 템플릿, XML 스키마 또는 기본)을 기반으로 표시하도록 선택할 수도 있습니다.

1. 적응형 양식 조각을 적응형 양식에 드래그 앤 드롭합니다.

   >[!NOTE]
   >
   >적응형 양식 내에서 작성하려면 적응형 양식 조각을 사용할 수 없습니다. 또한 JSON 기반 적응형 양식 및 이와 반대의 방법으로 XSD 기반 조각을 사용할 수 없습니다.

적응형 양식 조각은 적응형 양식에서 참조에 의해 삽입되며 독립형 적응형 양식 조각과 동기화됩니다. 즉, 적응형 양식 조각을 업데이트할 때 변경 사항은 조각이 사용되는 모든 적응형 양식에 반영됩니다.

### 적응형 양식에 단편 포함 {#embed-a-fragment-in-adaptive-form}

다음 예제 이미지와 같이 추가된 조각의 패널 도구 모음에서 **자산 포함: &lt;*fragmentName*>** 단추를 클릭하여 적응형 양식에 적응형 양식 조각을 포함하도록 선택할 수 있습니다.

![적응형 양식에 양식 단편 포함](assets/embed-fragment.png)

>[!NOTE]
>
>임베드된 조각은 더 이상 독립형 조각과 연결되지 않습니다. 적응형 양식 내에서 임베드된 조각의 구성 요소를 편집할 수 있습니다.

### 조각 내 조각 사용 {#using-fragments-within-fragments}

중첩된 적응형 양식 조각을 만들 수 있습니다. 즉, 다른 조각에서 조각을 드래그 앤 드롭할 수 있고 중첩된 조각 구조를 가질 수 있습니다.

### 조각 변경 {#change-fragments}

적응형 양식 단편 패널에 대한 구성 요소 편집 대화 상자에서 **단편 자산 선택** 속성을 사용하여 적응형 양식 단편을 다른 단편으로 바꾸거나 변경할 수 있습니다.

### 적응형 양식 단편을 위한 기록 문서 생성 {#generate-DOR-for-fragments}

DOR(Document of Record)은 양식 정보를 인쇄 또는 문서 형식으로 유지하는 데 도움이 됩니다. 따라서 나중에 언제든지 고객에 대한 정보를 추적할 수 있으며, 기록 문서를 사용하여 양식과 콘텐츠를 PDF 형식으로 함께 보관할 수도 있습니다. [적응형 양식 조각에 대한 기록 문서를 생성하는 방법을 알아봅니다](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).

### 적응형 양식에서 양식 단편 여러 번 사용 {#using-form-fragment-mutiple-times-in-af}

적응형 양식에서 스키마 기반 양식 조각을 여러 번 사용하여 각 양식 조각 필드에 대해 고유하게 데이터를 저장할 수 있습니다. 예를 들어 주소 양식 조각을 사용하여 대출 신청 양식에 영구, 통신 및 현재 거주 주소에 대한 주소 세부 정보를 수집할 수 있습니다.

![적응형 양식에서 여러 조각 사용](/help/forms/using/assets/using-multiple-fragment-af.gif)

>[!NOTE]
>
> * 적응형 양식에서 비 기반 양식 조각을 여러 번 사용하는 경우 조각 필드 간에 데이터 동기화가 발생합니다. 양식에서 스키마 기반 또는 없음 기반 조각을 여러 번 사용할 수 있는 핵심 구성 요소 기반 양식 조각에서는 데이터 동기화 문제가 발생하지 않습니다.

## 데이터 바인딩을 위한 조각 자동 매핑 {#auto-mapping-of-fragments-for-data-binding}

XFA 양식 템플릿 또는 XSD 복합 유형을 사용하여 적응형 양식 조각을 만들고 이 조각을 적응형 양식으로 드래그 앤 드롭하면 조각 모델 루트가 XFA 조각 또는 XSD 복합 유형에 매핑된 해당 적응형 양식 조각으로 XFA 조각 또는 XSD 복합 유형이 자동으로 대체됩니다.

구성 요소 편집 대화 상자에서 조각 에셋과 해당 바인딩을 변경할 수 있습니다.

>[!NOTE]
>
>AEM 컨텐츠 파인더의 적응형 양식 단편 라이브러리에서 바인딩된 적응형 양식 단편을 드래그 앤 드롭하고 적응형 양식 단편 패널의 구성 요소 편집 대화 상자에서 올바른 바인딩 참조를 제공할 수도 있습니다.

## 조각 관리 {#manage-fragments}

AEM Forms UI를 사용하여 적응형 양식 조각에 대해 여러 작업을 수행할 수 있습니다.

1. `https://[hostname]:'port'/aem/forms.html`로 이동합니다.

1. AEM Forms UI 도구 모음에서 **선택**&#x200B;을 클릭하고 적응형 양식 조각을 선택합니다. 도구 모음에는 선택한 적응형 양식 조각에서 수행할 수 있는 다음 작업이 표시됩니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>작업</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p>열기</p> </td>
   <td><p>선택한 적응형 양식 단편을 편집 모드로 엽니다.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>속성 보기</p> </td>
   <td><p>속성 패널을 엽니다. [속성] 패널에서 속성을 확인 및 편집하고, 미리 보기를 생성하고, 선택한 조각에 대한 썸네일 이미지를 업로드할 수 있습니다. 자세한 내용은 <a href="../../forms/using/manage-form-metadata.md" target="_blank">메타데이터 관리</a>.<br /> <br />를 참조하십시오. </p> </td>
  </tr>
  <tr>
   <td><p>복사</p> </td>
   <td><p>선택한 조각을 복사합니다. 도구 모음에 붙여넣기 단추가 나타납니다.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>다운로드</p> </td>
   <td><p>선택한 조각을 다운로드합니다.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>미리보기</p> </td>
   <td><p>XML 파일의 데이터를 조각과 병합하여 조각을 HTML 또는 사용자 지정 미리 보기로 미리 볼 수 있는 옵션을 제공합니다. 자세한 내용은 <a href="/help/forms/using/previewing-forms.md" target="_blank">양식 미리 보기</a>.<br /> <br />를 참조하세요. </p> </td>
  </tr>
  <tr>
   <td><p>검토 시작/검토 관리</p> </td>
   <td><p>선택한 조각의 검토를 시작하고 관리할 수 있습니다. 자세한 내용은 <a href="../../forms/using/create-reviews-forms.md" target="_blank">리뷰 만들기 및 관리</a>를 참조하십시오.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>사전 만들기</p> </td>
   <td><p>선택한 조각을 현지화하기 위한 사전을 생성합니다. 자세한 내용은 <a href="/help/forms/using/lazy-loading-adaptive-forms.md" target="_blank">적응형 양식 지역화</a>.<br /> <br />을 참조하세요. </p> </td>
  </tr>
  <tr>
   <td><p>게시/게시 취소</p> </td>
   <td><p>선택한 조각을 게시/게시 취소합니다.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>삭제</p> </td>
   <td><p>선택한 조각을 삭제합니다.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## 조각이 포함된 적응형 양식 현지화 {#localizing-adaptive-form-containing-fragments}

적응형 양식 조각이 포함된 적응형 양식을 현지화하려면 조각과 양식을 별도로 현지화해야 합니다. 조각을 한 번 현지화하여 여러 적응형 양식에서 재사용하는 것이 좋습니다.

>[!NOTE]
>
>조각의 현지화 키가 적응형 양식의 XLIFF 파일에 표시되지 않습니다.

## 조각을 사용하여 작업할 때 기억해야 할 주요 사항 {#key-points-to-remember-when-working-with-fragments}

* 조각 이름이 고유한지 확인하십시오. 동일한 이름의 조각이 이미 있는 경우 조각을 만들 수 없습니다.
* XDP 기반 적응형 양식에서 다른 XDP 조각을 포함하는 조각으로 패널을 저장하면 결과 조각이 하위 XDP 조각에 자동으로 바인딩됩니다. XSD 기반 적응형 양식이 있는 경우 결과 조각은 스키마 루트에 바인딩됩니다.
* 적응형 양식 조각을 만들면 CRXDE Lite에서 적응형 양식에 대한 guideContainer 노드와 유사한 조각 노드가 만들어집니다.
* 다른 양식 데이터 모델을 사용하는 적응형 양식의 조각은 지원되지 않습니다. 예를 들어 XDP 기반 조각은 XSD 기반 적응형 양식에서 지원되지 않으며, 이와 반대입니다.
* 적응형 양식 조각은 AEM 콘텐츠 파인더의 적응형 양식 조각 탭을 통해 사용할 수 있습니다.
* 독립형 적응형 양식 조각의 모든 표현식, 스크립트 또는 스타일은 참조로 삽입되거나 적응형 양식에 임베드될 때 유지됩니다.
* 참조에 의해 삽입된 적응형 양식 단편을 적응형 양식 내에서 편집할 수 없습니다. 편집하려면 독립 실행형 적응형 양식 조각을 편집하거나 적응형 양식에 조각을 임베드하십시오.
* 적응형 양식을 게시할 때 적응형 양식에 참조로 삽입된 독립형 적응형 양식 조각을 게시해야 합니다.
* 업데이트된 적응형 양식 조각을 다시 게시하면 변경 사항이 조각이 사용되는 적응형 양식의 게시된 인스턴스에 반영됩니다.
* 확인 구성 요소가 포함된 적응형 양식은 익명 사용자를 지원하지 않습니다. 또한 적응형 양식 조각에서 확인 구성 요소를 사용하지 않는 것이 좋습니다.
* (**Mac만 해당**) 양식 조각 기능이 모든 시나리오에서 완벽하게 작동하도록 하려면 다음 항목을 /private/etc/hosts 파일에 추가하십시오.
  `127.0.0.1 <Host machine>` **호스트 컴퓨터**: AEM Forms이 배포된 Apple Mac 컴퓨터입니다.

## 참조 조각 {#reference-fragments}

양식을 만드는 데 사용할 수 있는 적응형 양식 조각을 참조할 수 있습니다. 자세한 내용은 [참조 조각](../../forms/using/reference-adaptive-form-fragments.md)을 참조하세요.
