---
title: AEM Content and Commerce 시작하기
description: AEM Content 및 Commerce 프로젝트를 배포하는 방법을 알아봅니다.
topics: Commerce
feature: Commerce Integration Framework
solution: Experience Manager,Commerce
role: Admin, Developer
exl-id: 15face30-3039-49a0-bfee-56bff21e5c27
source-git-commit: 2e0cbe62754866d31de69547f9af1f2f63930f2c
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---

# AEM Content and Commerce 시작하기 {#start}

AEM 컨텐츠 및 Commerce을 시작하려면 AEM 컨텐츠 및 AEM 6.5용 Commerce 추가 기능을 설치해야 합니다.


## 온보딩 {#onboarding}

AEM Content 및 Commerce에 대한 온보딩은 두 단계 과정으로 이루어집니다.

1. AEM 6.5용 AEM 컨텐츠 및 Commerce 추가 기능 설치

2. AEM과 상거래 솔루션 연결

### AEM 6.5용 AEM 컨텐츠 및 Commerce 추가 기능 설치 {#install-add-on}

[소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 포털에서 AEM 6.5용 AEM Commerce 추가 기능을 다운로드하여 설치하십시오.

필요한 AEM 6.5 서비스 팩을 시작 및 설치합니다. 사용 가능한 마지막 서비스 팩을 설치하는 것이 좋습니다.

>[!NOTE]
>
>이 작업은 CSE가 AEM Managed Service 고객을 위해 수행합니다.

### Commerce 시스템에 AEM 연결 {#connect}

AEM은 AEM에 대한 액세스 가능한 GraphQL 종단점이 있는 상거래 시스템에 연결할 수 있습니다. 이러한 끝점은 일반적으로 공개적으로 사용할 수 있거나 개별 프로젝트 설정에 따라 개인 VPN 또는 로컬 연결을 통해 연결할 수 있습니다.

선택적으로, 인증이 필요한 추가 CIF 기능을 사용하도록 인증 헤더를 제공할 수 있습니다.

[AEM Project Archetype](https://github.com/adobe/aem-project-archetype) 및 [기본 구성](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)에 이미 포함된 [AEM Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)에서 생성된 프로젝트를 조정해야 합니다.

`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`의 `url` 값을 상거래 시스템의 GraphQL 끝점으로 바꿉니다. 이 구성은 OSGI 콘솔을 통해 또는 프로젝트를 통해 OSGI 구성을 배포하여 수행할 수 있습니다. 스테이징 및 프로덕션 시스템에 대한 다양한 구성은 다양한 AEM 실행 모드를 사용하여 지원됩니다.

AEM 컨텐츠, Commerce 추가 기능 및 CIF 핵심 구성 요소는 AEM 서버측과 클라이언트측 연결을 모두 사용합니다. 클라이언트측 CIF 핵심 구성 요소 및 CIF 추가 기능 제작 도구는 기본적으로 `/api/graphql`에 연결됩니다. 필요한 경우 CIF Cloud Service 구성을 통해 조정할 수 있습니다(아래 참조).

CIF 추가 기능은 [로컬 개발](develop.md)에 선택적으로 사용할 수 있는 `/api/graphql`의 GraphQL 프록시 서블릿을 제공합니다. 프로덕션 배포의 경우 AEM Dispatcher을 통해 또는 다른 네트워크 계층(CDN 등)에서 상거래 GraphQL 엔드포인트에 대한 역방향 프록시를 설정하는 것이 좋습니다.

## 저장소 및 카탈로그 구성 {#catalog}

추가 기능 및 [CIF 핵심 구성 요소](https://github.com/adobe/aem-core-cif-components)는 서로 다른 상거래 상점(또는 스토어 보기 등)에 연결된 여러 AEM 사이트 구조에서 사용할 수 있습니다. 기본적으로 CIF 추가 기능은 Adobe Commerce의 기본 스토어 및 카탈로그에 연결하는 기본 구성으로 배포됩니다.

이 구성은 다음 단계에 따라 CIF Cloud Service 구성을 통해 프로젝트에 대해 조정할 수 있습니다.

1. AEM에서 도구 > 클라우드 서비스 > CIF 구성으로 이동합니다.

2. 변경할 상거래 구성 선택

3. 작업 표시줄을 통해 구성 속성 열기

![CIF 클라우드 서비스 구성](/help/commerce/cif/assets/cif-cloud-service-config.png)

다음 속성을 구성할 수 있습니다.

- GraphQL 클라이언트 - commerce 백엔드 통신용으로 구성된 GraphQL 클라이언트를 선택합니다. 이 옵션은 일반적으로 기본값으로 유지되어야 합니다.
- 스토어 뷰 - 스토어 뷰 식별자. 비어 있는 경우 기본 스토어 보기가 사용됩니다.
- GraphQL 프록시 경로 - AEM의 GraphQL 프록시가 상거래 백엔드 GraphQL 엔드포인트에 대한 요청을 프록시하는 데 사용하는 URL 경로.

  >[!NOTE]
  >
  >대부분의 설정에서 기본값 `/api/graphql`을(를) 변경할 수 없습니다. 제공된 GraphQL 프록시를 사용하지 않는 고급 설정만 이 설정을 변경해야 합니다.

- 카탈로그 UID 지원 활성화 - 상거래 백엔드 GraphQL 호출에서 ID 대신 UID에 대한 지원을 활성화합니다.

  >[!NOTE]
  >
  >UID에 대한 지원은 Adobe Commerce 2.4.2에서 도입되었습니다. 상거래 백엔드가 버전 2.4.2 이상의 GraphQL 스키마를 지원하는 경우에만 활성화하십시오.

- 카탈로그 루트 범주 식별자 - 스토어 카탈로그 루트의 식별자(UID 또는 ID)

  >[!CAUTION]
  >
  >CIF 핵심 구성 요소 버전 2.0.0부터 `id`에 대한 지원이 제거되고 `uid`(으)로 대체되었습니다. 프로젝트에서 CIF 핵심 구성 요소 버전 2.0.0을 사용하는 경우 카탈로그 UID 지원을 활성화하고 유효한 범주 UID을 &quot;카탈로그 루트 범주 식별자&quot;로 사용해야 합니다.

위에 표시된 구성은 참조용입니다. 프로젝트는 자체 구성을 제공해야 합니다.

서로 다른 상거래 카탈로그와 결합된 여러 AEM 사이트 구조를 사용하는 더 복잡한 설정에 대해서는 [Commerce 다중 스토어 설정](configuring/multi-store-setup.md) 자습서를 참조하십시오.

## 추가 리소스 {#additional-resources}

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)
- [Commerce 다중 스토어 설정](configuring/multi-store-setup.md)
