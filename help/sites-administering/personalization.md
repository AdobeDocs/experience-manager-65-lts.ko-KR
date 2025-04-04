---
title: 개인화
description: 사용자에게 다이내믹 콘텐츠를 표시하는 맞춤형 환경을 제공하기 위한 Adobe Experience Manager의 개인화에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Administering,Personalization
role: Admin
exl-id: 558cf29b-34f4-4ead-b8d6-67ef8aaa5dc5
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 2%

---

# 개인화 {#personalization}

## Personalization란? {#what-is-personalization}

인터넷, 엑스트라넷 또는 인트라넷 웹 사이트에서 사용할 수 있는 콘텐츠의 양은 오늘날 계속해서 증가하고 있습니다.

Personalization은 사전 정의된 프로필, 사용자 선택 또는 대화형 사용자 행동을 기반으로 하는, 특정 요구 사항에 따라 선택된 다이내믹 콘텐츠를 표시하는 사용자 맞춤 환경을 사용자에게 제공하는 것을 중심으로 합니다.

개인화와 관련된 세 가지 주요 요소는 다음과 같습니다.

### 사용자 {#users}

* 개인과 그룹 모두의 프로필이 있습니다. 이러한 프로필에는 볼 수 있는 콘텐츠를 개인화하는 데 사용할 수 있는 특성(예: 작업 설명, 위치, 관심사)이 포함되어 있습니다.
* 조치를 취합니다. 그런 다음 행동 규칙을 분석하고 일치시켜 표시되는 콘텐츠를 조정할 수 있습니다.

### 콘텐츠 {#content}

* 사용자가 보려는 것입니다. 작업을 수행하기 위해 관심 있는 콘텐츠 및 사용하는 것이 좋습니다.
* 분류할 수 있으며, 따라서 사전 정의된 규칙에 따라 사용자가 사용할 수 있습니다.
* 동적이어야 합니다.

즉, 컨텐츠는 어떤 식으로든 사용자에게 의존해야 합니다. 모든 사용자가 동일한 콘텐츠를 보는 경우 개인화는 중복됩니다.

### 규칙 {#rules}

* 개인화가 실제로 발생하는 방식(사용자가 볼 수 있는 콘텐츠 및 시기)을 정의합니다.

Personalization은 다음 중 하나일 수 있습니다.

#### 명시적 {#explicit}

* 사용자 정의: 사용자는 선택한 컨텐츠 소스에서 선택합니다.

#### 암시적 {#implicit}

* 규칙 기반: 비즈니스 관리자는 특정 프로필 및/또는 행동을 기반으로 작업에 대한 특정 규칙을 정의합니다.
* 단순 필터링: 사용자 및/또는 그룹 수준에서 사전 정의된 프로필을 기반으로 선택합니다.
* 공동 작업/권장 사항 필터링: 사용자 동작은 사전 정의된 규칙에 따라 등록됩니다. 이러한 규칙은 같은 생각을 가진 개인과 관찰되는 행동을 기반으로 합니다. 수집된 정보는 사용자에게 표시되는 정보, 특히 권장 사항의 형태를 맞춤화하는 데 사용됩니다.

## Personalization은 어떻게 언제 사용할 수 있습니까? {#how-and-when-can-personalization-be-used}

Personalization은 다음과 같은 많은 경우에 사용할 수 있습니다.

### 인트라넷 페이지 {#intranet-pages}

* 내부 네트워크 내에 이미 정의된 사용자의 위치, 부서 및/또는 역할에 따라 콘텐츠를 제공할 수 있습니다.
* 사용 가능한 선택에 따라 추가 선택을 할 수 있습니다.

### 특정, 제한적, 타겟 사용자 그룹 - 엑스트라넷 {#extranets}

* 사용자는 인증을 위해 로그인해야 합니다. 이 로그인은 개인화에 필요한 정보를 제공하는 프로필에 연결됩니다. 위치, 제품과의 관계, 사용 내역, 예산 책임 등과 같은 세부 정보가 필요할 수 있습니다.
* 이러한 인스턴스는 다음과 같은 사이트에 걸쳐 다양할 수 있습니다.
* 시장에서 고도로 전문화된 섹션에 웹 사이트를 제공하는 회사(예: 의사를 위한 전문 웹 사이트를 제공하는 제약 회사).
* 고객이 현재 계정 및 청구 정보를 볼 수 있도록 웹 사이트를 제공하는 회사(예: 전화 공급자).

### 판매 및 배포 웹 사이트 {#sales-site}

* Amazon과 같은 판매 및 배포 웹 사이트에서는 사용자 프로필, 사용자의 판매 기록 및 검색 기록을 결합하여 사용자가 다음에 관심을 가질 만한 항목을 제안할 수 있습니다.

### 웹 사이트 검색 {#search-site}

* 많은 주요 검색 엔진 웹 사이트에는 사용자 행동, 그들이 사용하는 검색어 및 그들이 실제로 방문하는 웹 사이트를 기록하는 매우 강력한 분석 도구가 있습니다. 그런 다음 제공된 콘텐츠를 사용자 지정하는 데 사용됩니다(특히 광고 표시와 관련하여).

### Personalization의 강점 및 고려 사항 {#strengths-of-personalization-and-points-to-consider}

다음은 개인화를 사용해야 하는 이유입니다.

* 사용자는 편안하고 집중적인 웹 사이트를 경험할 수 있습니다.
* Personalization을 사용하여 최신 버전의 콘텐츠에 대한 액세스를 자동으로 전파할 수 있습니다.
* 소셜 공동 작업 기능은 프로필로 식별할 수 있으므로 사용자가 서로 통신할 수 있는 기능을 제공합니다.
* 사용자는 특정 작업을 수행하는 데 필요한 콘텐츠를 제공받을 수 있습니다. 회사 인트라넷 내에서 정보 확산을 위한 귀중한 도구를 제공할 수 있습니다.
* 사용자는 그들이 필요/원하는 콘텐츠를 제공받을 수 있고, 따라서 그들이 검색 동작들을 수행하는데 필요한 시간을 감소시킨다.
* 콘텐츠 제공자는 특정 범주의 사용자가 볼 수 있도록 콘텐츠를 제어할 수 있습니다.
* 사용자 특성과 비헤이비어의 조합을 기반으로 콘텐츠를 게재하기 위한 규칙을 정의할 수 있습니다. 이렇게 하면 웹 경험을 개인화하기 위한 정교한 메커니즘이 제공됩니다.

개인화를 사용할 때는 다음 사항을 고려하십시오.

#### 성능 {#performance}

* 당연히 추가 분석과 평가가 성과에 영향을 미친다. 그러나 사용되는 방법은 매우 정교하고 영향을 최소화하도록 최적화할 수 있다.

#### 승인 {#authorization}

* 웹 사이트에서 사용자를 식별할 수 있어야 하므로 Personalization에는 로그인 메커니즘이 필요합니다.

#### 캐싱 {#caching}

* 캐싱은 사용자가 성능 및 정확도 측면에서 보게 되는 측면입니다. 즉, 웹 사이트에서 얼마나 신속하게 개인화된 콘텐츠를 전달하는지, 그리고 항상 최신 상태인지 확인합니다.
* 캐싱은 개인화를 구성할 때 핵심 고려 사항이며 올바른 구현을 사용하기 위해 시간을 투자해야 합니다.

>[!TIP]
>
>성능 및 관련 캐싱 항목에 대한 Personalization의 영향은 [성능 최적화](/help/sites-deploying/configuring-performance.md) 문서에서 자세히 설명합니다.

#### 규칙의 정확성 {#accuracy}

* 사용자의 행동을 추적하거나 사용자 프로필을 기반으로 규칙을 설정하여 실현되는 Personalization은 정확하고 논리적이어야 합니다.
* 규칙의 부정확한 논리로 인해 사용자에게 강요되거나 거부되는 콘텐츠보다 사용자에게 더 좌절감을 주는 것은 없습니다.
* 따라서 규칙은 전경에서 사용자의 요구 사항을 고려하여 신중하게 생각해야 합니다. 이 작업에는 많은 노력이 소요될 수 있으며 과소 평가되지 않습니다. 비즈니스 규칙을 정의하는 것은 개인화를 구현할 때 기술적인 노력을 종종 능가합니다.

#### 사용 시기 {#when-to-use}

* 웹의 많은 기능과 마찬가지로 개인화를 신중하게 사용해야 합니다. 그 사용이 사용자에게 정말 도움이 됩니까? 은 항상 첫 번째 고려 사항이어야 합니다 - 또는 다른 방법에 의해 적은 노력으로 원하는 목표를 달성할 수 있는지 여부. Personalization은 실제 이점이 없기 때문에 사용자가 한 번(작동 방식 확인) 구성하는 기능이 될 위험이 있습니다.
* Personalization은 콘텐츠가 동적이고 어떤 식으로든 사용자에 종속될 때만 의미가 있습니다. 모든 사용자에게 동일한 콘텐츠가 표시되면 개인화가 중복됩니다.

#### 기밀 유지 {#confidentiality}

* 많은 사용자가 데이터 보호 및 보안에 대해 우려하고 있습니다. 특히 웹 서핑을 할 때 행동을 추적할 때 검색되는 데이터에 관한 것입니다.

## Personalization 및 액세스 {#personalization-and-access}

Personalization은 액세스 제어와 별도로 간주해야 하지만 상호 관련성이 있습니다.

Personalization 자체는 어떠한 형태의 액세스 제어도 생성하지 않습니다. 이는 단순히 사용자가 보는 것을 제어하는 방법입니다. 사용자가 다른 콘텐츠에 액세스하는 것을 제한하지 않으며, 다른 콘텐츠와 마찬가지로 올바른 액세스 제어가 이미 할당되어 있어야 합니다.

그러나 액세스 제어를 사용하여 개인화 형식을 만들 수 있습니다. 콘텐츠에 대한 사용자 액세스를 허용 또는 거부하는 경우 해당 콘텐츠는 사용할 수 있는 콘텐츠 선택에 영향을 미칠 수 밖에 없으므로 웹 경험을 개인화합니다.

## Personalization에 사용할 수 있는 구성 요소 {#components-available-for-personalization}

개인화를 위해 AEM에는 다양한 구성 요소가 제공됩니다. 일부는 사용자가 로그인하여 프로필을 편집할 수 있도록 허용하고, 일부는 내 가젯과 같이 사용자가 특정 페이지를 구성할 수 있도록 허용합니다.

| Sidekick의 제목 | 용도 |
|---|---|
| 확인된 암호 필드 | 암호 및 암호 확인을 요청합니다. |
| 결합된 로그인 등록 | 사용자가 기존 계정에 로그인하거나 새 계정에 등록할 수 있도록 허용합니다. |
| Forms 주소 필드 | 국제 주소를 입력할 수 있는 복잡한 필드입니다. |
| Forms 시작 | 양식 정의를 시작합니다. |
| Forms Captcha | 자동으로 새로 고침되는 영숫자 단어로 구성된 필드입니다. captcha 구성 요소는 보트로부터 웹 사이트를 보호합니다. |
| Forms 확인란 그룹 | 여러 항목이 목록으로 구성되고 그 앞에 확인란이 표시됩니다. 사용자는 여러 확인란을 선택할 수 있습니다. |
| Forms 드롭다운 목록 | 드롭다운 목록으로 구성된 여러 항목. 다중 선택 가능 스위치는 목록에서 여러 요소를 선택할 수 있는지 여부를 지정합니다. |
| Forms 끝 | 양식 정의를 종료합니다. |
| Forms 파일 업로드 | 사용자가 파일을 서버에 업로드할 수 있는 업로드 요소입니다. |
| Forms 숨김 필드 | 이 필드는 사용자에게 표시되지 않습니다. 값을 클라이언트에 전송하고 서버로 다시 전송하는 데 사용할 수 있습니다. 이 필드에는 제한이 없습니다. |
| Forms 이미지 단추 | 이미지로 렌더링되는 양식에 대한 추가 제출 단추입니다. |
| Forms 암호 필드 | 텍스트 필드와 동일하지만 한 줄만 허용되고 사용자의 텍스트 입력이 필드에 표시되지 않습니다. |
| Forms 라디오 그룹 | 라디오 단추 앞에 있는 목록으로 구성된 여러 항목. 사용자는 라디오 단추를 하나만 선택해야 합니다. |
| Forms 제출 단추 | 제목이 단추에 텍스트로 표시되는 양식에 대한 추가 제출 단추입니다. |
| Forms 텍스트 필드 | 사용자가 정보를 입력할 수 있는 텍스트 필드. |
| 내 가젯 | 사용 가능한 가젯 중 하나를 포함할 수 있습니다. |
| 프로필 아바타 사진 | 아바타 사진 입력을 허용합니다. |
| 프로필 세부 이름 | 필요한 경우 제목, 중간 이름 및 접미사와 같은 요소를 포함한 이름 세부 정보를 입력합니다. |
| 프로필 표시 이름 | 표시할 이름입니다. |
| 프로필 이메일 | 이메일 주소를 입력합니다. |
| 프로필 성별 | 성별을 입력할 수 있습니다. |
| 프로필 기본 전화 번호 | 전화 번호를 입력할 수 있습니다. |
| 프로필 기본 URL | URL 입력을 허용합니다. |
| 프로필 일반 텍스트 속성 | 프로필 속성. |
| 로그인 | 로그인할 때 사용자 이름과 암호를 제출할 수 있습니다. |
| 로그아웃 | 사용자가 현재 로그인되어 있음을 나타내며 로그아웃할 수 있는 링크를 제공합니다. |
| 태그 클라우드 | 웹 사이트 내에서 그래픽으로 표시된 태그를 보여 주는 태그 클라우드 |
| 티저 | 사용자가 기본 콘텐츠에 액세스할 수 있도록 &quot;괴롭히기&quot; 위해 기본 페이지에 표시되는 콘텐츠(일반적으로 이미지)입니다. |
