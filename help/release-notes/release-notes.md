---
title: Adobe Experience Manager 6.5 LTS의 최신 릴리스 정보
description: Adobe Experience Manager 6.5 LTS의 최신 릴리스 정보입니다.
source-git-commit: e062ab3ff820c85ebcbd0052c28e9e719222154f
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 23%

---


# Adobe Experience Manager 6.5 LTS의 최신 릴리스 정보 {#release-notes}

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] |
|---|---|
| 버전 | 6.5리터 |
| 유형 | 주요 릴리스 |
| 일반 가용 날짜 | 2025년 2월 28일 토요일 |

## 새로운 기능 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 LTS는 [!DNL Adobe Experience Manager] 6.5 코드 베이스에 대한 업그레이드 릴리스입니다. 새롭고 향상된 기능, 주요 고객 수정 사항, 우선 순위가 높은 고객 개선 사항 및 제품 안정화를 위한 일반적인 버그 수정을 제공합니다. 또한 SP22까지 [!DNL Adobe Experience Manager] 6.5 서비스 팩 릴리스도 포함됩니다.

아래 목록은 개요를 제공하며 후속 페이지에는 전체 세부 정보가 나열됩니다.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS의 플랫폼은 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix) 및 Java™ 콘텐츠 저장소의 업데이트된 버전 위에 빌드합니다. Apache Jackrabbit Oak 1.68.0.

Quickstart는 Eclipse Jetty 11.0.x를 서블릿 엔진으로 사용합니다.

#### Java™ 지원  {#java-support}

* Java™ 17 지원
* 최적의 성능을 위해 기본 GC 값을 다른 값으로 재정의합니다. 자세한 내용은 [설치 및 업데이트](/help/sites-deploying/custom-standalone-install.md) 섹션을 참조하십시오.
* Java™ 17 유지 관리 업데이트는 Oracle에서 공개적으로 제공되지 않을 경우 AEM 관련 프로젝트에서 고객이 사용할 수 있도록 Adobe에서 배포합니다.

#### Java™ 개발 {#java-development}

* 이제 Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)의 [두 버전, 사용 중지로 표시되지 않은 공용 인터페이스가 포함된 권장 버전 및 사용 중지로 표시된 인터페이스만 포함하는 버전이 있습니다.

#### 업그레이드 {#upgrade}

* 업그레이드 절차에 대한 자세한 내용은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하세요.

#### 저장소 {#repository}

* Adobe Experience Manager 6.5 LTS의 기반은 업데이트된 버전의 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix) 및 Java™ 콘텐츠 저장소(Apache Jackrabbit Oak 1.68.0) 위에 구축됩니다.

## 설치 및 업데이트 {#install-update}

설치 요구 사항은 [설치 지침](/help/sites-deploying/custom-standalone-install.md)을 참조하십시오.

자세한 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하세요.

## 지원되는 플랫폼 {#supported-platforms}

[AEM 6.5 LTS 기술 요구 사항](/help/sites-deploying/technical-requirements.md)에 대한 지원 수준을 포함하여 지원되는 플랫폼의 전체 행렬을 확인하십시오.

>[!NOTE]
>
>Java™ 17은 AEM 6.5 LTS와 함께 사용하기 권장되는 버전입니다.


## 더 이상 사용되지 않으며 제거된 기능 {#deprecated-and-removed-features}

Adobe는 항상 이전 기능과의 호환성을 신중하게 고려하면서 전반적인 고객 가치를 향상하도록 오랜 시간에 걸쳐 오래된 기능을 새롭게 만들거나 더 현대적인 대안으로 교체하기 위해 제품 기능을 지속해서 평가합니다.

Adobe Experience Manager(AEM) 기능의 제거 또는 교체가 임박했음을 알리기 위해 다음 규칙이 적용됩니다.

1. 사용 중지 공지가 먼저 표시됩니다. 사용 중단되는 동안에도 기능은 계속 사용할 수 있지만 더 이상 향상되지 않습니다.
1. 사용 중단되는 기능은 빠른 시일 내에 다음 주요 릴리스에서 제거됩니다. 제거에 대한 실제 목표 날짜는 나중에 발표될 예정입니다.

이 프로세스에서 고객에게 하나 이상의 릴리스 주기를 제공하여, 실제 제거 전에 더 이상 사용되지 않는 기능의 새 버전이나 후속 버전에 대한 구현을 채택할 수 있도록 합니다.

### 더 이상 사용되지 않는 기능 {#deprecated-features}

이 섹션에는 AEM 6.5 LTS에서 더 이상 사용되지 않는 것으로 표시된 기능이 나와 있습니다. 일반적으로 향후 릴리스에서 제거될 예정인 기능은 먼저 대체 기능을 제공하며 사용 중단되는 것으로 설정됩니다.

현재 배포에서 해당 기능을 사용 중인지 검토하고 이들 구현을 변경하여 제공되는 대체 기능을 사용하도록 계획을 세우는 것이 좋습니다.

| 영역 | 기능 | 대체 | 버전(SP) |
|---|---|---|---|
| Sites | [SPA 편집기](/help/sites-developing/spa-overview.md) | AEM에서 Headless 콘텐츠를 관리하기 위한 권장 편집기는 다음과 같습니다<br>.- 시각적 편집을 위한 [범용 편집기](/help/sites-developing/universal-editor/introduction.md)<br>- 양식 기반 편집을 위한 [콘텐츠 조각 편집기](/help/assets/content-fragments/content-fragments-managing.md) | 6.5LTS GA |

### 제거된 기능 {#removed-features}

이 섹션에는 AEM 6.5 LTS에서 제거된 기능과 성능이 나열됩니다. 이전 릴리스에는 이러한 기능이 더 이상 사용되지 않는 것으로 표시되었습니다.

| 영역 | 기능 | 대체 | 버전(SP) |
|--- |--- |--- |--- |
| 상거래 | AEM CIF Classic은 지원되지 않습니다. | [AEM CIF](/help/commerce/cif/migration.md)로 마이그레이션해야 합니다. | 6.5LTS GA |
| 솔루션 | 소셜/커뮤니티는 지원되지 않습니다. | 대체할 수 있는 항목이 없습니다. | 6.5LTS GA |
| Screens | Screens은 지원되지 않습니다. | 대체할 수 있는 항목이 없습니다. | 6.5LTS GA |
| 자산 | 번들이 social에 종속되어 있으므로 `dam-pim` 및 `dam-rating`은(는) 지원되지 않습니다. | 대체할 수 있는 항목이 없습니다. | 6.5LTS GA |
| Granite | `com.adobe.granite.socketio` 번들이 제거되었습니다. | 대체할 수 있는 항목이 없습니다. | 6.5LTS GA |
| Granite | `com.adobe.granite.crx-explorer`은(는) 지원되지 않습니다. | 대체할 수 있는 항목이 없습니다. | 6.5LTS GA |
| 구아바 | 이제 모든 guava 종속성이 AEM에서 제거되었으므로 `com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` 번들은 AEM의 일부가 아닙니다. | 고객이 guava에 의존하는 경우 고객이 직접 guava를 추가하거나 가능한 경우 guava 코드를 java 컬렉션 또는 기타 대체 요소로 대체할 수 있습니다. | 6.5LTS GA |
| We.Retail | We-retail 샘플 사이트는 지원되지 않습니다. | 대체할 수 있는 항목이 없습니다. | 6.5LTS GA |
| 공개 소스 | `oak-solr-osgi` 번들은 지원되지 않습니다. | 대체할 수 있는 항목이 없습니다. | 6.5LTS GA |
| 공개 소스 | `org.apache.servicemix.bundles.abdera-parser`, `org.apache.servicemix.bundles.jdom` 및 `org.apache.sling.atom.taglib`은(는) 지원되지 않습니다. | 대체할 수 있는 항목이 없습니다. | 6.5LTS GA |
| 공개 소스 | 이제 `org.apache.commons.io packages`을(를) `org.apache.commons.commons-io`에서 내보냈습니다. | 변경할 필요가 없습니다. | 6.5LTS GA |
| 공개 소스 | `com.sun.javax.mail` 번들에서 `javax.mail` 패키지를 내보내는 중입니다. | 변경할 필요가 없습니다. | 6.5LTS GA |
| 공개 소스 | 이제 `org.apache.jackrabbit.oak-jackrabbit-api` 번들에서 `org.apache.jackrabbit.api` 패키지를 내보냅니다. | 변경할 필요가 없습니다. | 6.5LTS GA |

## 제한된 웹 사이트{#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 고객이고 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 센터에 문의](https://experienceleague.adobe.com/en/docs/customer-one/using/home).
