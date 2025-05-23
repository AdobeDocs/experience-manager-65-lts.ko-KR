---
title: '자습서: 대화형 통신 계획'
description: 대화형 커뮤니케이션에 대한 구조 계획
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 8591214f-9c11-4cd3-b2a1-c83040507b20
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 2%

---

# 자습서: 대화형 통신 계획 {#tutorial-plan-the-interactive-communication}

대화형 커뮤니케이션에 대한 구조 계획

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

이 자습서는 [첫 번째 대화형 통신 만들기](/help/forms/using/create-your-first-interactive-communication.md) 시리즈의 단계입니다. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하려면 연대순으로 시리즈를 따르는 것이 좋습니다.

대화형 통신을 계획하는 첫 번째 단계는 대화형 통신의 내용을 완료하는 것입니다. 법률, 재무, 지원 또는 마케팅 등의 부서의 주제 전문가가 콘텐츠 최종 작성에 도움을 줄 수 있습니다. 콘텐츠가 완료되면 이를 분석하여 대화형 커뮤니케이션을 만드는 데 필요한 다양한 에셋 유형을 식별해야 합니다.

## 계획 고려 사항 {#planning-considerations}

대화형 통신에는 다음 요소가 포함됩니다.

* **정적 텍스트**&#x200B;에는 대부분 기본적으로 일반적이고 모든 고객과의 통신에 포함되는 대화형 통신의 일부가 포함됩니다. 예: 머리글, 바닥글, 인사말 또는 면책조항.
* **백엔드 시스템(양식 데이터 모델)에서 가져온 데이터**&#x200B;은(는) 고객별로 다르며 대화형 통신과 동적으로 병합됩니다. 예를 들어 양식 데이터 모델을 사용하여 정책 번호 또는 주소를 가져올 수 있습니다.
* 대화형 통신의 인쇄 및 웹 버전용 **레이아웃 또는 템플릿**.
* 대화형 통신에 다양한 텍스트 단락이 표시되는 **순서**.
* **최전선 직원(에이전트 UI)이 입력한 데이터**. 이 사용자는 메시지를 보내기 전에 메시지를 사용자 지정합니다. 예: 결제 기한.

* 미리 정의된 조건을 기반으로 채워지는 **조건부 데이터**. 예를 들어 대화형 통신이 생성된 날짜입니다.
* 로고 및 서명 이미지와 같은 **저장소에 저장된 이미지**. 기업 로고와 같은 이미지는 대부분의 또는 모든 대화형 통신에 나타납니다.
* 대화형 통신에서 복잡한 데이터의 표시를 단순화하는 데 **차트 및 표**&#x200B;가 필요합니다.

## 대화형 통신의 해부학 {#anatomy-of-the-interactive-communication}

대화형 통신을 만드는 데 사용되는 콘텐츠 및 요소를 완료하면 대화형 통신의 구조를 만들 수 있습니다. 구조에 [계획 고려 사항](/help/forms/using/planning-interactive-communications.md#planning-considerations) 섹션에 나열된 세부 정보가 있어야 합니다. 당사의 사용 사례를 토대로, 통신사가 고객에게 보내는 월별 청구서의 해부학적 구조를 예시하면 다음과 같습니다.

해부학에는 다음과 같은 입력 모드가 있는 데이터가 포함됩니다.

* 정적 텍스트
* 양식 데이터 모델
* 에이전트 UI
* 조건부 데이터
* 이미지

각 섹션에서 굵은 글꼴의 텍스트는 정적 텍스트를 나타냅니다. 데이터베이스에는 고객, 청구서 및 호출 테이블이 포함됩니다. 양식 데이터 모델은 이러한 테이블 중 하나에서 데이터를 받을 수 있습니다. 자세한 내용은 [양식 데이터 모델 만들기](/help/forms/using/create-form-data-model0.md)를 참조하십시오.

다음 표는 대화형 통신 구조의 각 필드에 대한 데이터 소스를 보여 줍니다.

<table>
 <tbody>
  <tr>
   <td>섹션</td>
   <td>정적 텍스트</td>
   <td>FDM </td>
   <td>에이전트 UI</td>
   <td>이미지</td>
  </tr>
  <tr>
   <td>청구 세부 정보</td>
   <td><p>송장 번호</p> <p>청구 일자</p> <p>청구 기간</p> <p>내 플랜</p> </td>
   <td><p><strong>내 플랜 </strong>필드 값</p> <p>표 - 고객</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>송장 번호</li>
     <li>청구 일자</li>
     <li>청구 기간</li>
    </ul> <p> </p> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>고객 세부 정보</td>
   <td><p>공급 장소</p> <p>상태 코드</p> <p>모바일 번호</p> <p>대체 연락처 번호</p> <p>관계 번호</p> <p>연결 수</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>이름</li>
     <li>주소</li>
     <li>모바일 번호</li>
     <li>대체 연락처 번호</li>
     <li>관계 번호</li>
    </ul> <p>표 - 고객</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>공급 장소</li>
     <li>상태 코드</li>
     <li>연결 수</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>청구 요약</td>
   <td><p>이전 잔액</p> <p>결제</p> <p>조정</p> <p>현재 청구 기간 청구</p> <p>미수금</p> <p>기한</p> </td>
   <td><p><strong>현재 청구 기간 </strong> 필드에 대한 값</p> <p>테이블 - 청구서</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>이전 잔액</li>
     <li>결제</li>
     <li>조정</li>
     <li>미수금</li>
     <li>기한</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>청구 요약</td>
   <td><p>통화 요금</p> <p>전화 회의 비용</p> <p>SMS 요금 </p> <p>모바일 인터넷 요금</p> <p>국가 로밍 요금</p> <p>국제 로밍 요금</p> <p>부가 서비스 요금</p> <p>총 청구 요금</p> <p>총 지불 금액</p> <p>부가 서비스 비용 필드의 조건</p> </td>
   <td><p>다음 필드의 값:</p>
    <ul>
     <li>통화 요금</li>
     <li>전화 회의 비용</li>
     <li>SMS 요금 </li>
     <li>모바일 인터넷 요금</li>
     <li>국가 로밍 요금</li>
     <li>국제 로밍 요금</li>
     <li>부가 서비스 요금</li>
     <li>총 요금(usagecharges 계산 필드)</li>
     <li>총 AP(usagecharges 계산 필드)</li>
    </ul> <p>테이블 - 청구서</p> </td>
   <td>필드 없음</td>
   <td>—</td>
  </tr>
  <tr>
   <td>항목별 통화 - 발신</td>
   <td><p>열 이름:</p>
    <ul>
     <li>날짜</li>
     <li>시간</li>
     <li>숫자</li>
     <li>기간</li>
     <li>청구</li>
    </ul> </td>
   <td><p>모든 값</p> <p>테이블 - 호출</p> </td>
   <td>필드 없음</td>
   <td>—</td>
  </tr>
  <tr>
   <td>지금 결제</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>부가 가치 서비스</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>
