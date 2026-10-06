---
title: 테마 사용자 정의
description: AEM Forms 애플리케이션의 테마를 맞춤화하는 방법에 대해 알아봅니다. HTML 코드 및 CSS 파일을 사용자 정의하여 조직별 모양과 느낌을 제공할 수 있습니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 5765b456-c6e8-4498-ade0-b36c95aadd71
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
source-git-commit: 2b710c6ef8d291a42b4a7658bf84f5e764422d5c
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 5%
---
# 테마 사용자 정의 {#theme-customization}

>[!NOTE]
>
>AEM Forms 앱의 Android 및 iOS 버전은 단종되었습니다. Android 앱은 2026년 9월에 Google Play에서 게시 취소되었으며 iOS 앱은 Apple App Store에서 제거되었습니다.
>이러한 앱은 더 이상 설치할 수 없습니다. Android 앱에 대한 도움이 필요하면 [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com)에 문의하십시오.

HTML 코드 및 CSS 파일을 사용자 정의하여 AEM Forms 앱에 고유한 조직별 모양과 느낌을 제공할 수 있습니다. 예를 들어 작업 또는 시작점의 배경색 및 높이를 변경할 수 있습니다. 다음 예에서는 변경 지침을 제공합니다.

* 설명 대신 지침 표시
* 표시 경로 수
* 배경 그라데이션 색상

## 단계 {#steps}

1. 프로젝트를 엽니다.

   * iOS의 경우 Xcode에서 `Capture.xcodeproj` 열기
   * Android의 경우 Eclipse에서 Android 프로젝트를 엽니다.
   * Windows의 경우 Visual Studio에서 `MWSWindows.sln`을(를) 엽니다.

1. 템플릿 폴더로 이동합니다.

   * Xcode에서 **캡처 > www > wsmobile > js > 런타임 > 템플릿** 폴더로 이동합니다.
   * Eclipse에서 **자산 > www > wsmobile > js > 런타임 > 템플릿** 폴더로 이동합니다.
   * Visual Studio에서 **MWSWindows > www > wsmobile > js > runtime > templates** 폴더로 이동합니다.

1. 편집할 `template.html` 페이지를 엽니다.
1. 다음 문자열을 찾습니다.

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   `<%`(으)로 바꿉니다.

1. `template.html` 파일에서 다음 코드를 찾습니다.

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. 다음 줄을 주석 처리하고 파일을 저장합니다.

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. css 폴더로 이동합니다.

   * Xcode에서 **캡처 > www > wsmobile > css**&#x200B;로 이동합니다.
   * Eclipse에서 **자산 > www > wsmobile > css**&#x200B;로 이동합니다.
   * Visual Studio에서 **MWSWindows > www > wsmobile > css**&#x200B;로 이동합니다.

1. 편집할 `_style.css` 페이지를 엽니다.
1. 배경 이미지의 경우 `#323232`을(를) `#fff`(으)로 변경하십시오.
1. 변경 내용을 저장하고 `_style.css` 파일을 닫습니다.
1. AEM Forms 앱을 엽니다.

   이제 AEM Forms 앱에 설명 대신 지침이 표시됩니다.
