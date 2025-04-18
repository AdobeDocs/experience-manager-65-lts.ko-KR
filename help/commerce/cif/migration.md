---
title: AEM Commerce integration framework(CIF) 추가 기능으로 마이그레이션
description: 이전 버전에서 AEM Commerce integration framework(CIF) 추가 기능으로 마이그레이션하는 방법.
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 847c33c1-17d6-447a-9f2c-91f2a81a3f04
source-git-commit: fdb84a17b3af7eaa76e5a7c30d21d7a601463278
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 4%

---

# Experience Manager 추가 기능에 대한 마이그레이션 안내서 {#cif-migration}

이 안내서는 Experience Manager 추가 기능 마이그레이션을 위해 업데이트해야 하는 영역을 식별하는 데 도움이 됩니다.

## CIF 추가 기능

CIF 추가 기능은 [소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=commerce*&amp;2_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3Aversion&amp;2_group.propertyvalues.operation=equals&amp;2_group.propertyvalues.0_values=target-version%3Aaem%2F6-5&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=16)을 통해 사용할 수 있습니다. 호환되며 Experience Manager as a Cloud Service용 CIF 추가 기능과 동일한 기능을 제공합니다.

[AEM 콘텐츠 및 Commerce 시작하기](getting-started.md)를 참조하세요.

Adobe는 CIF 배포 프로젝트를 지원하기 위해 [AEM CIF 핵심 구성 요소](https://github.com/adobe/aem-core-cif-components)를 제공합니다.

## 제품 카탈로그

CIF 추가 기능은 제품 카탈로그 데이터 가져오기를 지원하지 않습니다. CIF 추가 기능 주도자를 사용하면 외부 상거래 솔루션에 대한 실시간 호출을 통해 제품 및 카탈로그 요청이 온디맨드로 수행됩니다. 상거래 솔루션 통합에 대한 자세한 내용을 보려면 통합 장으로 이동합니다.

>[!TIP]
>
>사용 가능한 실시간 API가 없는 경우 API가 있는 외부 제품 캐시를 사용하여 통합해야 합니다. 예 [Magento 오픈 소스](https://business.adobe.com/products/magento/open-source.html).

## AEM 렌더링을 사용한 제품 카탈로그 경험

클래식 CIF과 함께 카탈로그 블루프린트를 사용하는 경우 제품 카탈로그 워크플로우를 업데이트해야 합니다. 이제 CIF 추가 기능은 AEM 카탈로그 템플릿을 사용하여 제품 카탈로그 경험을 즉시 렌더링합니다. 더 이상 제품 데이터 또는 제품 페이지 복제가 필요하지 않습니다.

## 캐시 불가능 데이터 및 쇼핑 상호 작용

캐시할 수 없는 데이터 및 상호 작용(예: 장바구니에 추가, 검색)에 대한 클라이언트측 요청은 CDN/Dispatcher을 통해 상거래 끝점(상거래 솔루션 또는 통합 계층)으로 직접 이동해야 합니다. AEM이 프록시였던 모든 호출을 제거합니다.
