---
title: 경로 작업에 사용된 이미지 사용자 지정
description: LiveCycle AEM Forms 작업 영역에서 경로 작업에 사용되는 이미지를 사용자 정의하는 방법.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 782043c0-79f8-42a4-ae1b-4743b480e523
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# 경로 작업에 사용된 이미지 사용자 지정 {#customize-images-used-in-route-actions}

경로 작업에 사용되는 이미지를 사용자 지정하려면 [일반 사용자 지정 단계](/help/forms/using/generic-steps-html-workspace-customization.md)에 설명된 단계를 수행한 다음 이 문서에 설명된 단계를 수행합니다.

## 경로 작업에 대한 이미지 {#images-for-route-actions}

1. CSS의 이미지를 정의하는 스타일을 새 경로 작업의 다음 위치에 추가합니다.

   `/apps/ws/css/newStyle.css`

   예: 아래와 같이 `myStyle1`이라는 새 스타일을 추가하고 WebDAV 클라이언트를 사용하여 `myStyleIcon1.png` 이미지 파일을 `/apps/ws/image`의 폴더에 업로드합니다.

   >[!NOTE]
   >
   >자세한 내용은 [WebDAV 액세스](/help/sites-administering/webdav-access.md)를 참조하십시오.

   >[!NOTE]
   >
   >스타일 이름을 경로 작업 이름과 동일하게 사용하십시오.

   ```css
   .myStyle1{
   
           background-image: url('../images/myStyleIcon1.png');
   
       }
   ```

## 작업 목록 작업 작업 팝업 {#task-list-task-action-popup}

1. 작업 목록 작업 팝업을 만듭니다. [AEM Forms 작업 영역 코드 작성](introduction-customizing-html-workspace.md#building-html-workspace-code)을 참조하십시오. 개발 패키지를 사용해야 합니다.

1. `/libs/ws/js/runtime/templates/task.html`을(를) `/apps/ws/js/runtime/templates/task.html`에 복사합니다.

1. CSS 스타일 이름이 서버에서 들어오는 경로 작업 이름과 같으면 `/apps/ws/js/runtime/templates/task.html`에서 다음 코드를 수정합니다.

   ```jsp
   <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   
   To
   
   <%if(routeList == null){%>
               <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li class="<%= availableCommands.directCommands[i]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   ```

1. CSS 스타일 이름이 서버에서 들어오는 경로 작업 이름과 다른 경우 `/apps/ws/js/runtime/templates/task.html`에서 다음 코드를 수정하십시오. 스타일을 경로 작업 이름과 매핑하기 위해 `if-else` 서블릿 조건 스택을 추가합니다.

```jsp
<%if(routeList == null){%>
            <li>
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
            <li>
                <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
            </li>
            <%}%>
            <%}%>

To

<%if(routeList == null){%>
            <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
                <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                     <li class="myStyle1" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                     <li class="myStyle2" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}%>
            <%}%>
            <%}%>
```

## 작업 세부 사항 작업 작업 팝업 {#task-details-task-action-popup}

1. `/libs/ws/js/runtime/templates/taskdetails.html`을(를) `/apps/ws/js/runtime/templates/taskdetails.html`에 복사합니다.

1. CSS 스타일 이름이 서버에서 들어오는 경로 작업 이름과 같으면 `/apps/ws/js/runtime/templates/taskdetails.html`에서 다음 코드를 수정합니다.

   ```jsp
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                       <%}%>
   ```

1. CSS 스타일 이름이 서버에서 들어오는 경로 작업 이름과 다른 경우 `/apps/ws/js/runtime/templates/taskdetails.html`에서 다음 코드를 수정하십시오. 스타일을 경로 작업 이름과 매핑하기 위해 `if-else` 서블릿 조건 스택을 추가합니다.

   ```jsp
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                   <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle1" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle2" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}%>
               <%}%>
   ```

1. 편집할 `/apps/ws/js/registry.js`을(를) 열고 다음 텍스트를 찾습니다.
   `"text!/lc/libs/ws/js/runtime/templates/taskdetails.html"`

1. 텍스트를 다음과 같이 바꿉니다.
   `"text!/lc/apps/ws/js/runtime/templates/taskdetails.html"`
