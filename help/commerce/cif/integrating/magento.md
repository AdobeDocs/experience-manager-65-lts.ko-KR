---
title: Commerce integration framework을 사용한 AEM 및 Adobe Commerce 통합
description: AEM과 Adobe Commerce은 Commerce integration framework(CIF)를 사용하여 원활하게 통합됩니다. CIF을 사용하면 AEM이 Adobe Commerce 인스턴스에 액세스하고 GraphQL을 통해 Adobe Commerce과 통신할 수 있습니다. 또한 AEM 작성자는 제품 및 카테고리 선택기 및 제품 콘솔 을 사용하여 Adobe Commerce에서 온디맨드로 가져온 제품 및 카테고리 데이터를 검색할 수 있습니다. 또한 CIF은 상거래 프로젝트를 가속화할 수 있는 기본 스토어프런트를 제공합니다.
thumbnail: aem-magento-architecture.jpg
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: cecd9591-bff4-4b4e-a3fd-4ab4278a0b81
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 1%

---

# Commerce integration framework을 사용하여 AEM 및 Adobe Commerce(Magento) 통합 {#aem-commerce-framework}

Experience Manager 및 Adobe Commerce은 Commerce integration framework(CIF)를 사용하여 원활하게 통합됩니다. CIF을 사용하면 AEM에서 Adobe Commerce의 [GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/)를 사용하여 상거래 인스턴스에 직접 액세스하고 통신할 수 있습니다.

>[!NOTE]
>
>지원되는 최소 GraphQL API 버전은 2.3.5입니다. 특정 기능은 최신 버전 또는 Adobe Commerce 버전에서만 지원됩니다.

## 아키텍처 개요 {#overview}

전반적인 아키텍처는 다음과 같습니다.

![CIF 아키텍처 개요](../assets/AEM_Magento_Architecture.png)

CIF 내에서는 서버측과 클라이언트측 통신 패턴을 지원합니다.
서버측 API 호출은 상거래 GraphQL 스키마에 대한 [생성된 데이터 모델 집합](https://github.com/adobe/commerce-cif-magento-graphql)과(와) 함께 빌트인, 일반 [GraphQL 클라이언트](https://github.com/adobe/commerce-cif-graphql-client)를 사용하여 구현됩니다. 또한 GraphQL 쿼리 또는 GQL 포맷 돌연변이를 사용할 수 있습니다.

[React](https://reactjs.org/)을 사용하여 빌드되는 클라이언트측 구성 요소의 경우 [Apollo Client](https://www.apollographql.com/docs/react/)이 사용됩니다.

## AEM CIF 핵심 구성 요소 아키텍처 {#cif-core-components}

![AEM CIF 핵심 구성 요소 아키텍처](../assets/cif-component-architecture.jpg)

[AEM CIF 핵심 구성 요소](https://github.com/adobe/aem-core-cif-components)는 [AEM WCM 핵심 구성 요소](https://github.com/adobe/aem-core-wcm-components)와(과) 매우 유사한 디자인 패턴 및 모범 사례를 따릅니다.

AEM CIF 핵심 구성 요소를 위한 Adobe Commerce과의 비즈니스 로직 및 백엔드 통신은 Sling 모델에서 구현됩니다. 프로젝트별 요구 사항을 충족하도록 이 논리를 사용자 정의해야 하는 경우 슬링 모델에 대한 위임 패턴 을 사용할 수 있습니다.

>[!TIP]
>
>[AEM CIF 핵심 구성 요소 사용자 지정](../customizing/customize-cif-components.md) 페이지에는 CIF 핵심 구성 요소를 사용자 지정하는 방법에 대한 자세한 예제와 모범 사례가 있습니다.

프로젝트 내에서 AEM CIF 핵심 구성 요소 및 사용자 지정 프로젝트 구성 요소는 Sling 컨텍스트 인식 구성을 통해 AEM 페이지와 연결된 Adobe Commerce 저장소에 대해 구성된 클라이언트를 쉽게 검색할 수 있습니다.
