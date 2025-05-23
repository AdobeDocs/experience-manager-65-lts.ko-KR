---
title: 폴더를 Brand Portal에 게시
description: 폴더를 Brand Portal에 게시 및 게시 취소하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
solution: Experience Manager, Experience Manager Assets
exl-id: b67df215-6ef9-461a-bfb8-f5b5ece8451b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 34%

---

# 폴더를 Brand Portal에 게시{#publish-folders-to-brand-portal}

Adobe Experience Manager(AEM) Assets 관리자는 자산과 폴더를 조직의 AEM Assets Brand Portal 인스턴스에 게시(또는 게시 워크플로우를 나중 날짜/시간으로 예약)할 수 있습니다. 그러나 먼저 AEM Assets을 Brand Portal과 통합해야 합니다. 자세한 내용은 [Brand Portal에서 AEM Assets 구성](/help/assets/configure-aem-assets-with-brand-portal.md)을 참조하십시오.

에셋 또는 폴더를 게시하면 Brand Portal의 사용자가 사용할 수 있습니다.

AEM Assets에서 원래 에셋 또는 폴더를 추가로 수정하는 경우, 에셋 또는 폴더를 다시 게시하기 전까지 변경 사항이 Brand Portal에 반영되지 않습니다. 이 기능은 진행 중인 작업 변경 사항을 Brand Portal에서 사용할 수 없도록 합니다. 관리자가 게시한 승인된 변경 사항만 Brand Portal에서 사용할 수 있습니다.

## 폴더를 Brand Portal에 게시 {#publish-folders-to-brand-portal-1}

1. AEM Assets 인터페이스에서 원하는 폴더 위로 마우스를 가져간 후 빠른 작업에서 **게시** 옵션을 선택합니다.

   또는 원하는 폴더를 선택하고 추가 단계를 따릅니다.

   ![publish2bp](assets/publish2bp.png)

1. **지금 폴더 게시**

   선택한 폴더를 Brand Portal에 게시하려면 다음 중 하나를 수행하십시오.

   * 도구 모음에서 **빠른 게시**&#x200B;를 선택합니다. 그런 다음 메뉴에서 **Brand Portal에 게시**&#x200B;를 선택합니다.

   * 도구 모음에서 **게시 관리**&#x200B;를 선택합니다.

   1. **작업**&#x200B;에서 **Brand Portal에 게시**&#x200B;을 선택하고 **예약**&#x200B;에서 **지금**&#x200B;을 선택한 후 **다음**&#x200B;을 클릭합니다.
   1. **범위**&#x200B;에서 선택 내용을 확인하고 **Brand Portal에 게시**&#x200B;를 클릭합니다.

   폴더가 Brand Portal에 게시하기 위한 큐에 올라갔음을 나타내는 메시지가 나타납니다. Brand Portal 인터페이스에 로그인하여 게시된 폴더를 확인합니다.

   **나중에 폴더 게시**

   자산 폴더의 Brand Portal에 게시 워크플로우를 나중 날짜 또는 시간으로 예약하려면,

   1. 게시할 자산/폴더를 선택한 후에는 맨 위의 도구 모음에서 **게시 관리**&#x200B;를 선택합니다.
   1. **작업**&#x200B;에서 **Brand Portal에 게시**&#x200B;을 선택하고 **예약**&#x200B;에서 **나중에**&#x200B;을 선택합니다.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. **활성화 날짜**&#x200B;를 선택하고 시간을 지정합니다. **다음**&#x200B;을 클릭합니다.
   1. **범위**&#x200B;에서 선택 내용을 확인합니다. **다음**&#x200B;을 클릭합니다.
   1. **워크플로**&#x200B;에서 워크플로 제목을 지정합니다. **나중에 게시**&#x200B;를 클릭합니다.

      ![manageschedulepub](assets/manageschedulepub.png)

## Brand Portal에서 폴더 게시 취소 {#unpublish-folders-from-brand-portal}

Brand Portal 작성자 인스턴스에서 게시를 취소하여 AEM에 게시된 모든 에셋 폴더를 제거할 수 있습니다. 원래 폴더를 게시 취소한 후에는 Brand Portal 사용자가 해당 복사본을 더 이상 사용할 수 없습니다.

Brand Portal에서 폴더를 빠르게 게시 취소하거나 나중 날짜 및 시간으로 예약할 수 있습니다. Brand Portal에서 자산 폴더의 게시를 취소하려면,

1. AEM 작성자 인스턴스의 AEM Assets 인터페이스에서 게시를 취소할 폴더를 선택합니다.

   ![publish2bp-1](assets/publish2bp.png)

1. 도구 모음에서 **게시 관리**&#x200B;를 클릭합니다.

1. **지금 Brand Portal에서 게시 취소**

   Brand Portal에서 원하는 폴더의 게시를 빠르게 취소하려면 다음 작업을 수행하십시오.

   1. 도구 모음에서 **게시 관리**&#x200B;를 선택합니다.
   1. **작업**&#x200B;에서 **Brand Portal에서 게시 취소**&#x200B;를 선택하고 **예약**&#x200B;에서 **지금**&#x200B;을 선택한 후 **다음**&#x200B;을 클릭합니다.
   1. **범위**&#x200B;에서 선택 내용을 확인하고 **Brand Portal에 게시 취소**&#x200B;를 클릭합니다.

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **나중에 Brand Portal에서 게시 취소**

   Brand Portal에서 나중 날짜 및 시간으로 폴더 게시를 예약하려면 다음 작업을 수행하십시오.

   1. 도구 모음에서 **게시 관리**&#x200B;를 선택합니다.
   1. **작업**&#x200B;에서 **Brand Portal에서 게시 취소**&#x200B;를 선택하고 **예약**&#x200B;에서 **나중에**&#x200B;를 선택합니다.
   1. **활성화 날짜**&#x200B;를 선택하고 시간을 지정합니다. **다음**&#x200B;을 클릭합니다.
   1. **범위**&#x200B;에서 선택 내용을 확인하고 **다음**&#x200B;을 클릭합니다.
   1. **워크플로**&#x200B;에서 **워크플로 제목**&#x200B;을 지정합니다. **나중에 게시 취소**&#x200B;를 클릭합니다.

      ![unpublishworkflows](assets/unpublishworkflows.png)

>[!NOTE]
>
>Brand Portal에서 에셋을 게시/게시 취소하는 절차는 폴더의 해당 절차와 유사합니다.
