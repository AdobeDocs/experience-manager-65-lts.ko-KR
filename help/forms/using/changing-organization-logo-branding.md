---
title: 브랜딩을 위한 조직 로고 변경
description: AEM Forms 작업 영역을 브랜딩하려면 기본 로고를 사용자 정의하여 조직의 로고를 제공합니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 3aa4aca3-3c94-4936-ba9c-484bbb196256
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 10%
---
# 브랜딩을 위한 조직 로고 변경 {#changing-the-organization-logo-for-branding}

AEM Forms 작업 영역의 왼쪽 상단 모서리에 조직 로고가 표시됩니다. 로고를 업데이트하려면 [AEM Forms 작업 영역 사용자 지정의 일반 단계](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization)를 수행한 후 다음 단계를 수행합니다.

1. 로고를 만들고 파일 이름을 `NewWorkspace.png`(으)로 지정합니다. WebDAV 클라이언트를 사용하여 /apps/ws/images 폴더에 이미지 파일을 넣습니다.

   >[!NOTE]
   >
   >로고 이미지의 권장 크기는 218px × 20px입니다.

   >[!NOTE]
   >
   >자세한 내용은 [WebDAV 액세스](/help/sites-administering/webdav-access.md)를 참조하십시오.

1. 다음 스타일을 추가하여 스타일 시트(/apps/ws/css/newStyle.css)의 새 로고 이미지를 참조합니다.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
