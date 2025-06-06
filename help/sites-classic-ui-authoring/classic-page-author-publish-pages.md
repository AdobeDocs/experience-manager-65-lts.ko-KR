---
title: 페이지 게시
description: 작성 환경에서 콘텐츠를 작성 및 검토한 후 공개 웹 사이트에서 사용할 수 있도록 설정합니다.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 20aea30b-9cfe-45c1-aa8d-08085f8e3e7d
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 10%

---

# 페이지 게시{#publishing-pages}

작성 환경에서 콘텐츠를 작성 및 검토한 후 공개 웹 사이트(게시 환경)에서 사용할 수 있도록 설정합니다.

이를 페이지 게시라고도 합니다. 게시 환경에서 페이지를 제거하려는 경우 게시 취소라고 합니다. 게시 및 게시 취소할 때 작성 환경에서 페이지를 삭제할 때까지 계속 변경할 수 있습니다.

페이지를 즉시 또는 미래의 미리 정의된 날짜/시간에 게시/게시 취소할 수도 있습니다.

>[!NOTE]
>
>게시와 관련된 특정 용어는 혼동될 수 있습니다.
>
>* **게시/게시 취소**
>  이 용어는 콘텐츠를 게시 환경에서 공개적으로 사용할 수 있도록(또는 사용할 수 없도록) 하는 작업을 위한 기본 용어입니다.
>
>* **활성화/비활성화**
>  게시/게시 취소와 동의어입니다.
>
>* **복제**
>  사용자 댓글을 게시하거나 역복제할 때와 같이 한 환경에서 다른 환경으로의 데이터(예: 페이지 컨텐츠, 파일, 코드, 사용자 댓글) 이동을 설명하는 기술 용어입니다.
>

>[!NOTE]
>
>특정 페이지 게시에 필요한 권한이 없는 경우:
>
>* 게시할 요청을 적절한 사람에게 알리도록 워크플로가 트리거됩니다.
>* 이를 알리는 메시지가 잠시 동안 표시됩니다.
>

## 페이지 게시 {#publishing-a-page}

페이지를 활성화하는 방법에는 두 가지가 있습니다.

* [웹 사이트 콘솔에서](#activating-a-page-from-the-websites-console)
* [페이지 자체의 사이드 킥에서](#activating-a-page-from-sidekick)

>[!NOTE]
>
>도구 콘솔에서 [트리 활성화](#howtoactivateacompletesectiontreeofyourwebsite)를 사용하여 여러 페이지의 하위 트리를 활성화할 수도 있습니다.

### 웹 사이트 콘솔에서 페이지 활성화 {#activating-a-page-from-the-websites-console}

웹 사이트 콘솔에서 페이지를 활성화할 수 있습니다. 페이지를 열고 내용을 수정한 후 웹 사이트 콘솔로 돌아갑니다.

1. 웹 사이트 콘솔에서 활성화할 페이지를 선택합니다.
1. 상단 메뉴 또는 선택한 페이지 항목의 드롭다운 메뉴에서 **활성화**&#x200B;를 선택합니다.

   페이지 및 모든 하위 페이지의 콘텐츠를 활성화하려면 [**도구** 콘솔](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#howtoactivateacompletesectiontreeofyourwebsite)을 사용하십시오.

   ![screen_shot_2012-02-08at13817pm](assets/screen_shot_2012-02-08at13817pm.png)

   >[!NOTE]
   >
   >필요한 경우 AEM은 페이지에 연결된 에셋을 활성화하거나 다시 활성화하도록 요청합니다. 확인란을 선택하거나 선택을 취소하여 해당 에셋을 활성화할 수 있습니다.
   >
   >

1. 필요한 경우 AEM은 페이지에 연결된 에셋을 활성화하거나 다시 활성화하도록 요청합니다. 확인란을 선택하거나 선택을 취소하여 해당 에셋을 활성화할 수 있습니다.

   ![chlimage_1-100](assets/chlimage_1-100.png)

1. AEM WCM은 선택한 컨텐츠를 활성화합니다. 게시된 페이지는 [웹 사이트 콘솔](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console)(녹색으로 표시)에 콘텐츠 및 활성화 날짜/시간에 대한 정보가 표시됩니다.

   ![screen_shot_2012-02-08at14335pm](assets/screen_shot_2012-02-08at14335pm.png)

### Sidekick에서 페이지 활성화 {#activating-a-page-from-sidekick}

편집을 위해 페이지를 열면 해당 페이지를 활성화할 수도 있습니다.

페이지를 열고 내용을 수정한 후에는 다음 작업을 수행합니다.

1. Sidekick에서 **페이지** 탭을 선택합니다.
1. **페이지 활성화**&#x200B;를 클릭합니다.
페이지가 활성화되었음을 확인하는 메시지가 창 오른쪽 상단에 표시됩니다.

## 페이지 게시 취소 {#unpublishing-a-page}

게시 환경에서 페이지를 제거하려면 콘텐츠를 비활성화합니다.

페이지를 비활성화하려면 다음 작업을 수행하십시오.

1. 웹 사이트 콘솔에서 비활성화할 페이지를 선택합니다.
1. 상단 메뉴 또는 선택한 페이지 항목의 드롭다운 메뉴에서 **비활성화**&#x200B;를 선택합니다. 삭제를 확인하는 메시지가 표시됩니다.

   ![screen_shot_2012-02-08at14859pm](assets/screen_shot_2012-02-08at14859pm.png)

1. [웹 사이트 콘솔](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console)을 새로 고치면 콘텐츠가 더 이상 게시되지 않음을 나타내는 빨간색으로 표시됩니다.

   ![screen_shot_2012-02-08at15018pm](assets/screen_shot_2012-02-08at15018pm.png)

## 나중에 활성화/비활성화 {#activate-deactivate-later}

### 나중에 활성화 {#activate-later}

나중에 활성화를 예약하려면 다음 작업을 수행하십시오.

1. 웹 사이트 콘솔에서 **활성화** 메뉴로 이동한 다음 **나중에 활성화**&#x200B;를 선택합니다.
1. 대화 상자가 열리면 활성화 날짜와 시간을 입력하고 **확인**&#x200B;을 클릭합니다. 이렇게 하면 지정된 시간에 활성화되는 페이지의 버전이 만들어집니다.

   ![screen_shot_2012-02-08at14751pm](assets/screen_shot_2012-02-08at14751pm.png)

나중에 활성화하면 지정된 시간에 이 페이지 버전을 활성화하는 워크플로우가 시작됩니다. 반대로 나중에 비활성화하면 특정 시간에 이 페이지 버전을 비활성화하는 워크플로우가 시작됩니다.

이 활성화/비활성화를 취소하려면 [워크플로 콘솔](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd)로 이동하여 해당 워크플로를 종료하십시오.

### 나중에 비활성화 {#deactivate-later}

나중에 비활성화 일정을 예약하려면 다음을 수행합니다.

1. 웹 사이트 콘솔에서 **비활성화** 메뉴로 이동한 다음 **나중에 비활성화**&#x200B;를 선택합니다.

1. 대화 상자가 열리면 비활성화 날짜와 시간을 입력하고 **확인**&#x200B;을 클릭합니다.

   ![screen_shot_2012-02-08at15129pm](assets/screen_shot_2012-02-08at15129pm.png)

**늦게 비활성화** r을(를) 사용하면 특정 시간에 이 페이지 버전을 비활성화하는 워크플로가 시작됩니다.

이 비활성화를 취소하려면 [워크플로 콘솔](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd)(으)로 이동하여 해당 워크플로를 종료합니다.

## 예약된 활성화/비활성화(설정/해제 시간) {#scheduled-activation-deactivation-on-off-time}

[페이지 속성](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)에서 정의할 수 있는 **설정 시간** 및 **해제 시간**&#x200B;을 사용하여 페이지를 게시/게시 취소하도록 예약할 수 있습니다.

### 페이지 게시 상태 확인 {#determining-page-publication-status-classic-ui}

[웹 사이트 콘솔](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console)에서 상태를 볼 수 있습니다. 색상이 게시 상태를 나타냅니다.

## 웹 사이트의 전체 섹션(트리) 활성화 {#activating-a-complete-section-tree-of-your-website}

**웹 사이트** 탭에서 개별 페이지를 활성화할 수 있습니다. 동일한 루트 페이지 아래에 있는 상당한 수의 콘텐츠 페이지를 입력하거나 업데이트한 경우 전체 트리를 한 번에 더 쉽게 활성화할 수 있습니다. 또한 드라이 실행 을 수행하여 활성화를 에뮬레이션하고 활성화할 페이지를 강조 표시할 수 있습니다.

1. **시작** 페이지에서 **도구** 콘솔을 선택한 다음 **복제**&#x200B;를 두 번 클릭하여 콘솔(`https://localhost:4502/etc/replication.html`)을 엽니다.

   ![screen_shot_2012-02-08at125033pm](assets/screen_shot_2012-02-08at125033pm.png)

1. **복제** 콘솔에서 **트리 활성화**&#x200B;를 클릭합니다.

   다음 창(`https://localhost:4502/etc/replication/treeactivation.html`)이 표시됩니다.

   ![screen_shot_2012-02-08at125033pm-1](assets/screen_shot_2012-02-08at125033pm-1.png)

1. **시작 경로**&#x200B;를 입력하십시오. 활성화(게시)할 섹션의 루트에 대한 경로를 지정합니다. 이 페이지와 아래의 모든 페이지는 활성화(또는 시험 실행(Dry Run)을 선택한 경우 에뮬레이션에서 사용됨)용으로 간주됩니다.
1. 필요에 따라 선택 기준을 활성화합니다.

   * **수정된 페이지만**: 수정된 페이지만 활성화합니다.
   * **활성화됨**: 이미 활성화된 페이지만 활성화합니다. 재활성화의 한 형태로 작동합니다.
   * **비활성화됨 무시**: 비활성화된 모든 페이지를 무시합니다.

1. 수행할 작업을 선택합니다.

   1. 활성화된 *페이지*&#x200B;를 확인하려면 **시험 실행**&#x200B;을 선택하세요. 에뮬레이션일 뿐이며, 페이지가 활성화되지 않습니다.

   1. 페이지를 활성화하려면 **활성화**&#x200B;를 선택합니다.
