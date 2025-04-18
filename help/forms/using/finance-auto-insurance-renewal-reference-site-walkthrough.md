---
title: We.Finance 자동차 보험 갱신 참조 사이트 안내
description: 연습을 통해 We.Finance 자동차 보험 갱신 참조 사이트에 대해 알아보십시오.
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: User, Developer
exl-id: 3f9f1a20-9029-4e30-9c9d-ef452512f7e9
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---

# We.Finance 자동차 보험 갱신 참조 사이트 안내{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## We.Finance 참조 사이트 시나리오  {#we-finance-reference-site-scenario}

We.Finance 사이트는 AEM Forms의 대화형 통신 기능을 학습할 수 있도록 설계된 금융 서비스 사이트입니다.

AEM forms 및 Microsoft® Dynamics와의 통합을 통해 금융 서비스 회사에서 고객 경험을 개인화하는 방법을 보여주는 We.Finance 자동 보험 사용 사례에 대한 자세한 설명을 읽어 보십시오. 이 대화형 연습은 금융 회사에서 복잡한 디지털 거래와 고객 커뮤니케이션을 쉽게 구현할 수 있도록 설계되었습니다.

**여정은 사용 사례**(으)로 시작합니다.

Sarah Rose는 기존 We.Finance 고객이며 자동차 보험에 가입했습니다. 새라가 보험 증권을 갱신해야 할 때가 바로 그때이다. 글로리아 리오스는 보험 담당자예요 We.Finance에서 Sarah에게 정책 갱신에 대한 알림 메시지를 보냅니다. Sarah는 이메일에 제공된 지침을 따르고 프로세스를 성공적으로 완료합니다.

## 자동 보험 애플리케이션 워크스루 {#auto-insurance-application-walkthrough}

We.Finance 자동 보험 응용 프로그램 시나리오는 사용자를 위한 시각적 설명이며 다음 두 가지 성향에 기반합니다.

* We.Finance 고객인 Sarah Rose
* Gloria Rios, 보험 대리점, We.Finance

### Gloria가 We.Finance에서 보험 증서 갱신 통신을 보냅니다. {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria가 AEM 인스턴스에 로그인하고 **자동 보험 갱신,**&#x200B;을 클릭한 다음 **에이전트 UI 열기**&#x200B;를 클릭합니다. 클릭으로 보험 문서에 Sarah Rose의 보험 세부 정보가 미리 채워진다. Gloria가 **Submit**&#x200B;을(를) 클릭하면 &quot;Submission Initiated&quot; 화면에 메시지가 표시된 다음 몇 초 후에 &quot;Submitted Successfully&quot;가 표시됩니다.

Sarah는 &quot;자동차 보험 갱신&quot;이라는 제목이 포함된 이메일을 수신합니다.

![에이전트 UI](assets/agent_ui_email_new.png)

#### 직접 확인 {#see-it-yourself}

**Adobe Experience Manager** > **Forms** > **Forms 및 문서** > **We.Finance** > **자동차 보험**&#x200B;으로 이동합니다. 자동 보험 갱신 **대화형 통신**&#x200B;을 선택하고 **에이전트 UI 열기**&#x200B;를 클릭합니다. 대화형 통신이 에이전트 UI에서 열립니다. 정책 문서가 첨부된 이메일을 받을 수 있도록 유효한 이메일 주소를 입력하고 제출을 클릭합니다.

`https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`에서 바로 자동 보험 갱신 대화형 통신에 액세스하고 검토할 수 있습니다.

### Sarah는 We.Finance에서 보험 갱신 커뮤니케이션을 받고 갱신을 결정합니다 {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah는 We.Finance로부터 첨부 파일이 포함된 이메일을 수신하며 자신의 자동차 보험 정책이 곧 만료된다는 사실을 Sarah에게 상기시킵니다. 첨부파일은 Sarah의 자동차 보험 편지의 인쇄본이다.

Sarah가 **지금 갱신**&#x200B;을 클릭하여 자동차 보험 서신의 웹 버전으로 이동합니다. 이 편지 맨 위에서, Sarah는 자신의 정책이 만료되기 전까지 남은 시간을 찾는다. 이 페이지에서는 Sarah에게 보험 번호, 만기 금액 등 자신의 보험 세부 정보와 할인 제안 및 충성도 보상 등 기타 정보에 대한 기본 개요를 제공합니다. Sarah가 다시 정책 하단의 **지금 갱신**&#x200B;을 클릭합니다.

![ref1](assets/ref1.png)

#### 작동 방식 {#how-it-works}

자동차 보험 편지의 웹 및 인쇄 출력은 Interactive Communications의 멀티채널 기능을 사용하여 생성됩니다.

이메일의 지금 갱신 버튼은 게시 인스턴스의 대화형 커뮤니케이션인 자동 보험 갱신 애플리케이션에 연결됩니다.

#### 직접 확인 {#see-it-yourself-1}

PDF이 첨부된 이메일을 받았어야 합니다. PDF은 자동차 보험 편지의 인쇄 버전입니다. 정책의 웹 버전에 도달하려면 **지금 갱신**&#x200B;을 클릭하세요. 개인 정보 및 정책 세부 정보를 확인하고 **지금 갱신**&#x200B;을 클릭하면 다른 대화형 통신으로 이동합니다.

전자 메일의 **지금 갱신** 단추는 Sarah를 웹의 정책으로 보냅니다. 다음 URL을 방문할 수 있습니다.

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

자동차 보험 갱신에 대한 자세한 요약을 확인하고 페이지 하단의 **지금 갱신**&#x200B;을 클릭할 수 있습니다.

### Sarah가 결제 페이지에 도달 {#sarah-reaches-the-payment-page}

We.Finance는 Sarah를 지불 페이지로 안내합니다. Sarah는 자신의 기록을 가지고 자신의 정책 번호와 만료일을 다시 확인합니다. 페이지 오른쪽에서 Sarah는 총 금액에 대해 10% 할인이 적용된 갱신 결제 요약을 확인합니다.

#### 작동 방식 {#how-it-works-1}

지금 갱신 버튼을 누르면 Sarah가 결제 페이지로 이동합니다. 결제 페이지가 적응형 양식입니다.

#### 직접 확인 {#see-it-yourself-2}

**지금 갱신**&#x200B;을 클릭하여 결제 페이지로 이동합니다. 신용 카드 정보를 입력하고 **결제**&#x200B;를 클릭하세요.

다음 위치에서 작성 인스턴스의 결제 페이지에 연결할 수 있습니다.

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah가 결제를 완료하고 프로세스를 완료합니다 {#sarah-makes-the-payment-and-completes-the-process}

Sarah가 신용 카드 세부 정보를 입력하고 **결제**&#x200B;을(를) 클릭합니다.

#### 작동 방식 {#how-it-works-2}

Sarah가 신용 카드 세부 사항을 입력하고 Submit을 클릭하면 신용 카드 결제가 처리되고 적응형 양식에 구성된 감사 메시지가 화면에 나타납니다.

#### 직접 확인 {#see-it-yourself-3}

다음에서 결제 클릭 후 확인 메시지를 볼 수 있습니다.

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
