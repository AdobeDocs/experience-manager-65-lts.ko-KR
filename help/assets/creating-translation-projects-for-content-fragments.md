---
title: 콘텐츠 조각에 대한 번역 프로젝트 만들기
description: Adobe Experience Manager에서 컨텐츠 조각을 번역하는 방법을 알아봅니다.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
feature: Content Fragments
role: User, Admin
solution: Experience Manager, Experience Manager Assets
exl-id: cad7253d-95fb-47eb-b1c9-2d22a9e34481
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 5%

---

# 콘텐츠 조각에 대한 번역 프로젝트 만들기 {#creating-translation-projects-for-content-fragments}

에셋 외에도 Adobe Experience Manager(AEM) Assets은 [콘텐츠 조각](/help/assets/content-fragments/content-fragments.md)(변형 포함)에 대한 언어 복사 워크플로우를 지원합니다. 콘텐츠 조각에서 언어 복사 워크플로우를 실행하는 데 추가적인 최적화가 필요하지 않습니다. 각 워크플로우에서는 번역을 위해 전체 콘텐츠 조각이 전송됩니다.

콘텐츠 조각에서 실행할 수 있는 워크플로우 유형은 에셋에 대해 실행하는 워크플로우 유형과 정확히 유사합니다. 또한 각 워크플로우 유형에서 사용할 수 있는 옵션은 에셋의 해당 워크플로우 유형에서 사용할 수 있는 옵션과 일치합니다.

콘텐츠 조각에서 다음 유형의 언어 복사 워크플로우를 실행할 수 있습니다.

**만들기 및 번역**

이 워크플로에서는 번역할 콘텐츠 조각이 번역하려는 언어의 언어 루트에 복사됩니다. 또한 선택한 옵션에 따라 프로젝트 콘솔에서 콘텐츠 조각에 대한 번역 프로젝트가 만들어집니다. 설정에 따라 번역 프로젝트를 수동으로 시작하거나 번역 프로젝트를 만드는 즉시 자동으로 실행되도록 할 수 있습니다.

**언어 사본 업데이트**

소스 콘텐츠 조각이 업데이트되거나 수정되면 해당 로케일/언어별 콘텐츠 조각은 재번역이 필요합니다. 언어 사본 업데이트 워크플로는 추가 콘텐츠 조각 그룹을 번역하여 특정 로케일의 언어 사본에 포함합니다. 이 경우 번역된 콘텐츠 조각은 이전에 번역된 콘텐츠 조각을 이미 포함하고 있는 대상 폴더에 추가됩니다.

## 워크플로우 만들기 및 번역 {#create-and-translate-workflow}

만들기 및 번역 워크플로에는 다음 옵션이 포함되어 있습니다. 각 옵션과 관련된 절차 단계는 자산에 대한 해당 옵션과 관련된 절차 단계와 유사합니다.

* 구조만 만들기: 절차 단계는 [자산에 대해서만 구조 만들기](translation-projects.md#create-structure-only)를 참조하십시오.
* 번역 프로젝트 만들기: 절차 단계는 [에셋에 대한 번역 프로젝트 만들기](translation-projects.md#create-a-new-translation-project)를 참조하십시오.
* 기존 번역 프로젝트에 추가: 절차 단계는 [에셋의 기존 번역 프로젝트에 추가](translation-projects.md#add-to-existing-translation-project)를 참조하십시오.

## 언어 사본 업데이트 워크플로우 {#update-language-copies-workflow}

언어 사본 업데이트 워크플로에는 다음 옵션이 포함됩니다. 각 옵션과 관련된 절차 단계는 자산에 대한 해당 옵션과 관련된 절차 단계와 유사합니다.

* 번역 프로젝트 만들기: 절차 단계는 [에셋에 대한 번역 프로젝트 만들기](translation-projects.md#create-a-new-translation-project)(워크플로우 업데이트)를 참조하십시오.
* 기존 번역 프로젝트에 추가: 절차 단계는 [에셋에 대한 기존 번역 프로젝트에 추가](translation-projects.md#add-to-existing-translation-project)(워크플로우 업데이트)를 참조하십시오.

에셋에 대한 임시 사본을 만드는 방법과 유사하게 조각에 대한 임시 언어 사본을 만들 수도 있습니다. 자세한 내용은 [자산에 대한 임시 언어 사본 만들기](translation-projects.md#creating-temporary-language-copies)를 참조하십시오.

## 혼합 미디어 조각 번역 {#translating-mixed-media-fragments}

AEM을 사용하면 다양한 유형의 미디어 에셋 및 컬렉션을 포함하는 콘텐츠 조각을 번역할 수 있습니다. 인라인 에셋이 포함된 콘텐츠 조각을 번역하는 경우 이러한 에셋의 번역된 사본은 대상 언어 루트 아래에 저장됩니다.

컨텐츠 조각에 컬렉션이 포함된 경우 컬렉션 내의 자산은 컨텐츠 조각과 함께 번역됩니다. 번역된 에셋 사본은 소스 언어 루트 아래에 있는 소스 에셋의 물리적 위치와 일치하는 위치의 적절한 타겟 언어 루트 내에 저장됩니다.

혼합 미디어를 포함하는 콘텐츠 조각을 번역하려면 먼저 기본 번역 프레임워크를 편집하여 콘텐츠 조각과 연결된 인라인 에셋 및 컬렉션의 번역을 활성화하십시오.

1. AEM 로고를 클릭하고 **[!UICONTROL 도구 > 배포 > 클라우드 서비스]**(으)로 이동합니다.
1. **[!UICONTROL Adobe Marketing Cloud]**&#x200B;에서 **[!UICONTROL 번역 통합]**&#x200B;을 찾은 다음 **[!UICONTROL 구성 표시]**&#x200B;를 클릭합니다.

   ![chlimage_1-444](assets/chlimage_1-444.png)

1. 사용 가능한 구성 목록에서 **[!UICONTROL 기본 구성(번역 통합 구성)]**&#x200B;을 클릭하여 **[!UICONTROL 기본 구성]** 페이지를 엽니다.

   ![chlimage_1-445](assets/chlimage_1-445.png)

1. 도구 모음에서 **[!UICONTROL 편집]**&#x200B;을 클릭하여 **[!UICONTROL 번역 구성]** 대화 상자를 표시합니다.

   ![chlimage_1-446](assets/chlimage_1-446.png)

1. **[!UICONTROL Assets]** 탭으로 이동한 다음 **[!UICONTROL 콘텐츠 조각 번역 Assets]** 목록에서 **[!UICONTROL 인라인 미디어 Assets 및 관련 컬렉션]**&#x200B;을 선택합니다. **[!UICONTROL 확인]**&#x200B;을 클릭하여 변경 내용을 저장합니다.

   ![chlimage_1-447](assets/chlimage_1-447.png)

1. 영어 루트 폴더 내에서 컨텐츠 조각을 엽니다.

   ![chlimage_1-448](assets/chlimage_1-448.png)

1. **[!UICONTROL 자산 삽입]** 아이콘을 클릭합니다.

   ![chlimage_1-449](assets/chlimage_1-449.png)

1. 콘텐츠 조각에 에셋을 삽입합니다.

   ![콘텐츠 조각에 에셋 삽입](assets/column-view.png)

1. **[!UICONTROL 콘텐츠 연결]** 아이콘을 클릭합니다.

   ![chlimage_1-451](assets/chlimage_1-451.png)

1. **[!UICONTROL 콘텐츠 연결]**&#x200B;을 클릭합니다.

   ![chlimage_1-452](assets/chlimage_1-452.png)

1. 컬렉션을 선택하고 컨텐츠 조각에 포함합니다. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

   ![chlimage_1-453](assets/chlimage_1-453.png)

1. 콘텐츠 조각을 선택하고 **[!UICONTROL 전역 탐색]** 아이콘을 클릭합니다.
1. 메뉴에서 **[!UICONTROL 참조]**&#x200B;을(를) 선택하여 **[!UICONTROL 참조]** 창을 표시합니다.

   ![chlimage_1-454](assets/chlimage_1-454.png)

1. 언어 사본을 표시하려면 **[!UICONTROL 사본]** 아래의 **[!UICONTROL 언어 사본]**&#x200B;을 클릭하세요.

   ![chlimage_1-455](assets/chlimage_1-455.png)

1. 패널 하단에서 **[!UICONTROL 만들기 및 번역]**&#x200B;을 클릭하여 **[!UICONTROL 만들기 및 번역]** 대화 상자를 표시합니다.

   ![chlimage_1-456](assets/chlimage_1-456.png)

1. **[!UICONTROL 대상 언어]** 목록에서 대상 언어를 선택하십시오.

   ![chlimage_1-457](assets/chlimage_1-457.png)

1. **[!UICONTROL 프로젝트]** 목록에서 번역 프로젝트 형식을 선택하십시오.

   ![chlimage_1-458](assets/chlimage_1-458.png)

1. **[!UICONTROL 프로젝트 제목]** 상자에서 프로젝트 제목을 지정한 다음 **만들기**&#x200B;를 클릭합니다.

   ![chlimage_1-459](assets/chlimage_1-459.png)

1. **[!UICONTROL 프로젝트]** 콘솔로 이동하여 만든 번역 프로젝트의 프로젝트 폴더를 엽니다.

   ![chlimage_1-460](assets/chlimage_1-460.png)

1. 프로젝트 타일을 클릭하여 프로젝트 세부 정보 페이지를 엽니다.

   ![chlimage_1-461](assets/chlimage_1-461.png)

1. 번역 작업 타일에서 번역할 에셋 수를 확인합니다.
1. **[!UICONTROL 번역 작업]** 타일에서 번역 작업을 시작합니다.

   ![chlimage_1-462](assets/chlimage_1-462.png)

1. 번역 작업 타일 하단의 생략 부호를 클릭하여 번역 작업의 상태를 표시합니다.

   ![chlimage_1-463](assets/chlimage_1-463.png)

1. 콘텐츠 조각을 클릭하여 번역된 관련 에셋의 경로를 확인합니다.

   ![chlimage_1-464](assets/chlimage_1-464.png)

1. 컬렉션 콘솔에서 컬렉션에 대한 언어 사본을 검토하십시오.

   ![chlimage_1-465](assets/chlimage_1-465.png)

   컬렉션의 콘텐츠만 번역됩니다. 컬렉션 자체는 번역되지 않습니다.

1. 번역된 관련 에셋의 경로로 이동합니다. 번역된 에셋이 타겟 언어 루트 아래에 저장되었는지 확인합니다.

   ![chlimage_1-466](assets/chlimage_1-466.png)

1. 콘텐츠 조각과 함께 번역되는 컬렉션 내의 에셋으로 이동합니다. 자산의 번역된 사본이 적절한 타겟 언어 루트에 저장되어 있는지 확인합니다.

   ![chlimage_1-467](assets/chlimage_1-467.png)

   >[!NOTE]
   >
   >기존 프로젝트에 콘텐츠 조각을 추가하거나 업데이트 워크플로우를 수행하는 절차는 에셋의 해당 절차와 유사합니다. 이러한 절차에 대한 지침은 에셋에 대해 설명된 절차를 참조하십시오.
