---
title: 프로세스 인스턴스 목록 사용자 정의
description: AEM Forms 작업 영역의 프로세스 인스턴스에 표시되는 속성을 맞춤화하는 방법.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 7ffde604-2f56-4b53-88ab-5fac321e4753
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 4%

---

# 프로세스 인스턴스 목록 사용자 정의 {#customizing-the-listing-of-process-instances}

프로세스 인스턴스 목록이 AEM Forms 작업 공간의 추적 탭에 표시됩니다.

프로세스 인스턴스 목록에서 각 프로세스 인스턴스에 대해 AEM Forms 작업 공간에 해당 인스턴스의 일부 속성이 표시됩니다. 각 프로세스 인스턴스에 대해 다음 속성을 사용할 수 있습니다. 이러한 속성은 프로세스 인스턴스 구성 요소 모델에 속성으로 저장되며 해당 뷰 및 템플릿에서 사용할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>댓글</strong></td>
  </tr>
  <tr>
   <td>설명</td>
   <td>프로세스 인스턴스에 대한 설명입니다.</td>
  </tr>
  <tr>
   <td>개시자</td>
   <td>프로세스 인스턴스의 초기자 이름.</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>프로세스 인스턴스 개시자의 ID입니다.</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>프로세스 완료 시 타임스탬프.</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>프로세스 인스턴스의 ID.</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 = 시작됨<br /> 1 = 실행 중<br /> 2 = 완료<br /> 3 = 완료 중<br /> 4 = 종료됨<br /> 5 = 종료 중<br /> 6 = 일시 중단됨<br /> 7 = 일시 중단 중<br /> 8 = 일시 중단 해제 중</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>프로세스 이름.</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>프로세스가 시작된 타임스탬프.</td>
  </tr>
  <tr>
   <td>프로세스 변수</td>
   <td>프로세스 변수의 오브젝트 배열. 각 프로세스 변수 개체에는 <strong>name</strong>(프로세스 변수의 이름), <strong>value</strong>(프로세스 변수의 값) 및<strong> type</strong>(프로세스 변수의 유형)이 포함됩니다.</td>
  </tr>
 </tbody>
</table>

**예:**

프로세스 인스턴스 카드에 프로세스 인스턴스의 `description` 속성을 표시하려면 다음 단계를 수행하십시오.

1. [AEM Forms 작업 영역 사용자 지정에 대한 일반 단계](/help/forms/using/generic-steps-html-workspace-customization.md)를 따릅니다.
1. 다음 작업을 수행합니다.

   1. /libs/ws/js/runtime/templates/processinstance.html 이 없는 경우 /apps/ws/js/runtime/templates/에 복사합니다. **모두 저장**&#x200B;을 클릭합니다.
   1. 클래스 = &#39;processDescription&#39;을 inprocessinstance.html에 프로세스 설명 div를 추가합니다.

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. 다음 작업을 수행합니다.

   1. 편집하려면 /apps/ws/js/registry.js을 여십시오.
   1. `text!/lc/libs/ws/js/runtime/templates/processinstance.html`을(를) 검색하여 `text!/lc/`**앱**/ws/js/runtime/templates/processinstance.html으로 바꾸십시오.

1. 위의 변경 사항을 적용하려면 스타일 시트 /apps/ws/css/newStyle.css에 다음과 같은 방식으로 항목을 추가하여 CSS 파일을 업데이트해야 할 수 있습니다.

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement and user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
