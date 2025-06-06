---
title: 리디렉션 페이지 구성
description: 적응형 양식을 작성한 후 사용자는 양식을 작성하는 동안 양식 작성자가 구성할 수 있는 웹 페이지로 리디렉션될 수 있습니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: dba191d6-4fe9-40e7-a995-00f0c3fd335d
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 21%

---

# 리디렉션 페이지 구성{#configuring-redirect-page}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ko)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-redirect-page.html?lang=ko) |
| AEM 6.5 | 이 문서 |

양식 작성자는 양식을 제출한 후 양식 사용자가 리디렉션되는 각 양식에 대한 페이지를 구성할 수 있습니다.

1. 편집 모드에서 구성 요소를 선택한 다음 ![필드 수준](assets/field-level.png) > **적응형 양식 컨테이너**&#x200B;를 클릭하고 ![cmpr](assets/cmppr.png)을 클릭합니다.

1. 사이드바에서 **제출**&#x200B;을 클릭합니다.

1. 제출 섹션의 감사 페이지 아래에 리디렉션 페이지의 URL을 입력합니다.
1. 선택 사항으로, 제출 작업에서 REST에 제출 엔드포인트 작업의 경우 리디렉션 페이지에 전달할 매개 변수를 구성할 수 있습니다.

![페이지 구성 리디렉션](assets/thank-you-setting-1.png)

페이지 구성 리디렉션

양식 작성자는 감사 인사 페이지에 전달되는 다음 매개 변수를 사용할 수 있습니다. 사용 가능한 모든 제출 액션에 대해 `status` 및 `owner` 매개 변수가 전달됩니다. 이 두 매개 변수 외에도 다음 제출 작업에 대해 몇 가지 추가 매개 변수가 전달됩니다.

* **콘텐츠 저장 작업**(더 이상 사용되지 않음) : `contentPath`(제출된 데이터가 저장된 저장소의 노드 경로)이 전달됩니다.

* **PDF 저장 작업**(더 이상 사용되지 않음): 저장소에 PDF 파일을 저장하는 노드에 대해 제출된 데이터 및 경로 중 `contentPath`이(가) 전달됩니다.

* **Forms 워크플로우에 제출**: 양식 워크플로우에서 반환된 출력 매개 변수가 전달됩니다.

* **REST 끝점에 제출**: 필드 대 매개 변수 매핑에 대해 추가된 매개 변수가 전달됩니다. 이 제출 액션에서 `status` 및 `owner` 매개 변수가 전달되지 않습니다. 자세한 내용은 [REST 끝점에 제출 작업 구성](../../forms/using/configuring-submit-actions.md)을 참조하십시오.
