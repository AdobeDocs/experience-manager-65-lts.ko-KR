---
title: 브랜딩에 대한 조직 로고 변경
description: AEM Forms 작업 영역을 브랜딩하려면 기본 로고를 사용자 정의하여 조직의 로고를 제공합니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 3aa4aca3-3c94-4936-ba9c-484bbb196256
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 브랜딩에 대한 조직 로고 변경 {#changing-the-organization-logo-for-branding}

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
