---
title: Brand Portal에 자산 게시
description: Brand Portal에 에셋을 게시하고 게시 취소하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 9eba1e3f-9251-445e-b791-2be0a92aebd1
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 40%

---

# Brand Portal에 자산 게시 {#publish-assets-to-brand-portal}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=ko) |
| AEM 6.5 | 이 문서 |

Adobe Experience Manager(AEM) Assets 관리자는 자산과 폴더를 조직의 AEM Assets Brand Portal 인스턴스에 게시(또는 게시 워크플로우를 나중 날짜/시간으로 예약)할 수 있습니다. 하지만 먼저 Brand Portal에서 AEM Assets를 구성해야 합니다. 자세한 내용은 [Brand Portal에서 AEM Assets 구성](/help/assets/configure-aem-assets-with-brand-portal.md)을 참조하십시오.

복제가 성공하면 에셋, 폴더 및 컬렉션을 Brand Portal에 게시할 수 있습니다. 자산을 Brand Portal에 게시하려면 다음 단계를 따르십시오.

>[!NOTE]
>
>AEM 작성자가 초과 리소스를 차지하지 않도록 가급적이면 피크가 아닌 시간에, 시차 게시를 수행하는 것이 좋습니다.

1. Assets 콘솔에서 게시하려는 자산/폴더를 선택하고 도구 모음에서 **[!UICONTROL 빠른 게시]** 옵션을 클릭합니다.

   또는 Brand Portal에 게시할 자산을 선택합니다.

   ![publish2bp-2](assets/publish2bp.png)

1. 자산을 Brand Portal에 게시하려면 다음 두 가지 옵션을 사용할 수 있습니다.
   * [자산을 즉시 게시합니다.](#publish-to-bp-now)
   * [나중에 자산 게시](#publish-to-bp-now)

## 지금 자산 게시 {#publish-to-bp-now}

선택한 자산을 Brand Portal에 게시하려면 다음 중 하나를 수행하십시오.

* 도구 모음에서 **[!UICONTROL 빠른 게시]**&#x200B;를 선택합니다. 그런 다음 메뉴에서 **[!UICONTROL Brand Portal에 게시]**&#x200B;를 선택합니다.

* 도구 모음에서 **[!UICONTROL 게시 관리]**&#x200B;를 선택합니다.

   1. 그런 다음 **[!UICONTROL 작업]**&#x200B;에서 **[!UICONTROL Brand Portal에 게시]**&#x200B;를 선택하고 **[!UICONTROL 예약]**&#x200B;에서 **[!UICONTROL 지금]**&#x200B;을 선택합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   2. **[!UICONTROL 범위]** 내에서 선택 내용을 확인하고 **[!UICONTROL Brand Portal에 게시]**&#x200B;를 클릭합니다.

자산이 Brand Portal에 게시하기 위한 큐에 올라갔음을 나타내는 메시지가 나타납니다. Brand Portal 인터페이스에 로그인하여 게시된 자산을 확인합니다.

## 나중에 자산 게시 {#publish-to-bp-later}

나중 날짜 또는 시간에 Brand Portal에 자산을 게시하는 일정을 예약하려면,

1. 게시할 자산/폴더를 선택한 후에는 맨 위의 도구 모음에서 **[!UICONTROL 게시 관리]**&#x200B;를 선택합니다.

1. **[!UICONTROL 게시 관리]** 페이지의 **[!UICONTROL 작업]**&#x200B;에서 **[!UICONTROL Brand Portal에 게시]**&#x200B;를 선택하고 **[!UICONTROL 예약]**&#x200B;에서 **[!UICONTROL 나중에]**&#x200B;를 선택합니다.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. **[!UICONTROL 활성화 날짜]**&#x200B;를 선택하고 시간을 지정합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. **활성화 날짜**&#x200B;를 선택하고 시간을 지정합니다. **다음**&#x200B;을 클릭합니다.

1. **[!UICONTROL 워크플로]**&#x200B;에서 **[!UICONTROL 워크플로 제목]**&#x200B;을 지정합니다. **[!UICONTROL 나중에 게시]**&#x200B;를 클릭합니다.

   ![publishworkflow](assets/publishworkflow.png)

이제 Brand Portal에 로그인하여 게시된 자산을 Brand Portal 인터페이스에서 사용할 수 있는지 확인합니다.

![bp_landingpage](assets/bp_landingpage.png)

## Brand Portal에 게시된 파일 또는 폴더 보기 {#view-published-file-folder}

1. Brand Portal 인터페이스에 로그인하여 게시된 자산을 확인합니다(예약된 날짜 또는 시간에 따라 다름).

   ![bp_landingpage](assets/bp_landingpage.png)

1. 에셋의 현재 게시 상태를 보려면 목록 보기 ![목록 보기](assets/list-view.svg)(으)로 전환하십시오.

<!--2. On the [Asset Reports page](#https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/assets/admin/asset-reports), you can see the current state of the report job, for example, Success, Failed, Queued, or Scheduled.-->

![생성된 보고서 상태](assets/report-status.JPG)
