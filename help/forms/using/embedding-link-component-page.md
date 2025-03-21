---
title: 페이지에 링크 구성 요소 포함
description: 링크 구성 요소를 사용하여 모든 페이지에서 적응형 문서 또는 적응형 양식을 연결할 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
exl-id: a6ae1633-63a8-4364-b298-bc569459a136
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 페이지에 링크 구성 요소 포함{#embedding-link-component-in-a-page}

## 사전 요구 사항 {#prerequisites}

링크 구성 요소는 문서 서비스 범주의 구성원입니다. 문서 서비스 카테고리가 AEM 구성 요소 브라우저에 표시되는지 확인합니다. 범주가 나열되지 않으면 [Forms 포털 구성 요소 사용](/help/forms/using/enabling-forms-portal-components.md)에 나열된 단계를 따르십시오.

## 링크 구성 요소 {#link-component}

링크 구성 요소를 사용하여 양식 포털 작성자는 페이지의 어디에서든 적응형 양식에 대한 링크를 만들 수 있습니다. 링크 구성 요소는 구성 요소 브라우저의 문서 서비스 섹션에서 사용할 수 있습니다.

페이지에 링크 구성 요소를 추가하려면 다음 단계를 수행하십시오.

1. 페이지에서 **Link** 구성 요소를 드래그합니다. 구성 요소를 선택하고 ![cmpr](assets/cmppr.png)을(를) 선택합니다. 링크 구성 요소 편집 대화 상자가 열립니다.

   ![edit-link-component](assets/edit-link-component.png)

1. **디스플레이** 탭에서 다음을 지정하십시오.

   * **링크 캡션**: 링크의 링크 텍스트 또는 캡션입니다.
   * **링크 도구 설명**: 링크의 도구 설명.
   * **레이아웃 템플릿**: 링크 구성 요소의 레이아웃에 대한 템플릿입니다.

1. **자산 정보** 탭을 열고 자산 유형을 지정하십시오. 자산은 **양식**&#x200B;일 수 있습니다. 선택한 에셋 유형에 따라 아래 나열된 옵션이 표시됩니다.

   * **자산 경로**: 자산이 저장된 저장소 경로입니다.

   * **렌더링 형식**: 렌더링 형식(PDF, HTML 또는 자동)입니다. 자동 렌더링 유형은 사용자 환경을 감지하므로 양식을 HTML 또는 PDF으로 렌더링합니다. 예를 들어 모바일 장치에서 양식에 액세스하면 자동 렌더링 유형이 HTML에서 양식을 렌더링합니다.
   * 양식 데이터가 제출되는 서블릿에 **제출 URL:** URL을 지정합니다.
   * **HTML 프로필**: 양식을 HTML으로 렌더링하기 위한 프로필입니다.
   * **PDF 프로필**: 양식을 PDF 문서로 렌더링하기 위한 프로필입니다.

1. **고급** 탭을 엽니다. 키-값 쌍 형식으로 추가 매개변수를 지정할 수 있습니다. 링크를 클릭하면 이러한 추가 매개 변수가 양식과 함께 전달됩니다.

   **완료**&#x200B;를 선택하여 구성을 저장합니다.

## 링크 구성 요소 사용에 대한 우수 사례 {#best-practices-for-using-link-component-br}

* 양식 경로에 지정된 경로가 허용된 렌더링 형식으로 PDF이 있는 문서를 가리키는 경우 PDF을 렌더링 유형으로 선택해야 합니다.
* 양식의 제출 URL은 여러 위치에서 지정할 수 있으며, 우선 순위는 다음과 같습니다.

   1. 양식(제출 단추)에 포함된 제출 URL의 우선순위가 가장 높습니다.
   1. Forms Manager에 언급된 제출 URL은 우선 순위가 보통입니다.
   1. Forms 포털에 언급된 제출 URL의 우선 순위가 가장 낮습니다.
