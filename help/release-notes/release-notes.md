---
title: ' [!DNL Adobe Experience Manager] 6.5 LTS 릴리스 정보'
description: Adobe Experience Manager 6.5 LTS에 대한 최신 릴리스 정보를 찾아보십시오.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 70436606-d95c-4208-94f6-e33f3eefdf66
source-git-commit: 7f9f24f173604640b454449b389da9fcdcf7017d
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 94%

---

# Adobe Experience Manager 6.5 LTS의 최신 릴리스 정보 {#release-notes}

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] |
|---|---|
| 버전 | 6.5 LTS |
| 유형 | 주요 릴리스 |
| 일반 출시 | 2025년 3월 7일 |

## 새로운 기능 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 LTS는 [!DNL Adobe Experience Manager] 6.5 코드 베이스에 대한 업그레이드 릴리스입니다. 이 릴리스는 주요 고객 수정 사항, 우선순위가 높은 고객 개선 사항 및 제품 안정화를 위한 일반적인 버그 수정을 제공합니다. 또한 SP22까지의 [!DNL Adobe Experience Manager] 6.5 서비스 팩 릴리스를 포함합니다.

아래 목록은 개요를 제공하며, 다음 페이지에는 전체 세부 사항이 나열됩니다.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS의 플랫폼은 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix)와 Java™ 콘텐츠 저장소인 Apache Jackrabbit Oak 1.68.x의 업데이트된 버전을 기반으로 빌드되었습니다.

Eclipse Jetty 11.0.x는 Quickstart의 서블릿 엔진으로 사용됩니다.

#### Java™ 지원  {#java-support}

* Java™ 17 및 Java™ 21이 지원됩니다.
* 최적의 성능을 위해 기본 GC 값을 다른 값으로 재정의합니다. 자세한 내용은 [설치 및 업데이트](/help/sites-deploying/custom-standalone-install.md) 섹션을 참조하십시오.
* Adobe는 Oracle에서 공개적으로 제공되지 않는 경우 AEM 관련 프로젝트에서 고객이 사용할 수 있도록 Java™ 17 및 Java™ 21 유지 관리 업데이트를 배포합니다.

#### Uberjar 패키징 {#uber-jar-packaging}

* AEM 6.5 LTS의 Uberjar 패키징에 약간의 차이가 있습니다. 자세한 내용은 [AEM Uber Jar 버전 업데이트](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)를 참조하십시오.

#### 업그레이드 {#upgrade}

* 업그레이드 절차에 대한 자세한 내용은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.

## 설치 및 업데이트 {#install-update}

설정 요구 사항에 대한 자세한 내용은 [설치 지침](/help/sites-deploying/custom-standalone-install.md)을 참조하십시오.

세부 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.

>[!NOTE]
>
> 새 AEM 6.5 LTS 설치의 경우 인덱스 정의를 별도로 설치해야 합니다. 자세한 내용은 [이 문서](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)를 참조하세요.

## 지원되는 플랫폼 {#supported-platforms}

[AEM 6.5 LTS 기술 요구 사항](/help/sites-deploying/technical-requirements.md)에서 지원 수준을 포함한 전체 지원 플랫폼 매트릭스를 찾을 수 있습니다.

>[!NOTE]
>
>Java™ 17/Java™ 21은 AEM 6.5 LTS와 함께 사용하는 것이 권장되는 버전입니다.

## 더 이상 사용되지 않으며 제거된 기능 {#deprecated-and-removed-features}

Adobe는 기존 기능을 현대화하거나 대체하여 고객 가치를 개선하기 위해 제품 기능을 지속적으로 검토합니다. 이러한 변경 사항은 이전 버전과의 호환성을 신중하게 고려하여 적용됩니다.

Adobe Experience Manager(AEM) 기능의 제거 또는 대체 예정 사실을 알리기 위해 다음 규칙이 적용됩니다.

1. 사용 중지 공지가 먼저 표시됩니다. 사용 중지 중에도 기능이 계속 지원되지만 더 이상 개선되지는 않습니다.
1. 더 이상 사용되지 않는 기능은 이른 시일 내에 후속 주 릴리스에서 제거됩니다. 제거할 실제 목표 날짜는 추후 발표됩니다.

이 프로세스에서 고객에게 하나 이상의 릴리스 주기를 제공하여, 실제 제거 전에 더 이상 사용되지 않는 기능의 새 버전이나 후속 버전에 대한 구현을 채택할 수 있도록 합니다.

### 이제 사용되지 않는 기능 {#deprecated-features}

이 섹션에는 Adobe가 AEM 6.5 LTS에서 더 이상 사용되지 않는 기능이 나열됩니다. 일반적으로 Adobe는 향후 릴리스에서 해당 기능을 제거하기 전에 해당 기능을 더 이상 사용하지 않도록 설정하고 사용할 수 있는 대안을 제공합니다.


현재 배포에서 해당 기능을 사용 중인지 검토하고 이들 구현을 변경하여 제공되는 대체 기능을 사용하도록 계획을 세우는 것이 좋습니다.

| 영역 | 기능 | 대체 | 버전 (SP) |
|---|---|---|---|
| Sites | [SPA 편집기](/help/sites-developing/spa-overview.md) | AEM에서 Headless 콘텐츠를 관리하기 위한 권장 편집기:<br>- 시각적 편집을 위한 [범용 편집기](/help/sites-developing/universal-editor/introduction.md)<br>- 양식 기반 편집을 위한 [콘텐츠 조각 편집기](/help/assets/content-fragments/content-fragments-managing.md) | 6.5 LTS GA |

### 제거된 기능 {#removed-features}

이 섹션에는 AEM 6.5 LTS에서 제거된 기능이 나열됩니다. 이전 릴리스에서는 이러한 기능이 더 이상 사용되지 않는다고 표시되었습니다.

| 영역 | 기능 | 대체 | 버전 (SP) |
|--- |--- |--- |--- |
| Commerce | AEM CIF Classic은 지원되지 않습니다. | [AEM CIF](/help/commerce/cif/migration.md)로 마이그레이션합니다. | 6.5 LTS GA |
| 솔루션 | 소셜/Communities는 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| Screens | Screens는 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| 자산 | 번들이 소셜에 종속되므로 `dam-pim` 및 `dam-rating`은 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| 자산 | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()`는 제거되었습니다. | 추가된 대체 API `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()` 를 사용하십시오. | 6.5 LTS GA |
| 포털 | AEM Portal Director는 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| Granite | 번들 `com.adobe.granite.socketio` 는 제거되었습니다 | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| Granite | `com.adobe.granite.crx-explorer`는 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| Granite | `crx2oak`는 지원되지 않습니다. | [Oak 업그레이드](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade)의 관련 버전을 선택하십시오. | 6.5 LTS GA |
| Adobe | `com.adobe.cq.cq-searchpromote-integration`는 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| Guava | 이제 AEM에서 모든 Guava 종속성이 제거되었으므로 `com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` 번들은 AEM의 일부가 아닙니다. | 고객은 Guava에 종속된 경우 직접 추가하거나, 가능한 경우 Guava 코드를 Java 컬렉션 또는 다른 대체 기능으로 바꿀 수 있습니다. | 6.5 LTS GA |
| `We.Retail` | `We-retail` 샘플 사이트는 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| 공개 소스 | `oak-solr-osgi` 번들은 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| 공개 소스 | `org.apache.servicemix.bundles.abdera-parser`, `org.apache.servicemix.bundles.jdom` 및 `org.apache.sling.atom.taglib`은 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| 공개 소스 | `org.apache.commons.io` 패키지는 이제 `org.apache.commons.commons-io`에서 내보내집니다. | 변경 작업을 수행할 필요가 없습니다. | 6.5 LTS GA |
| 공개 소스 | `javax.mail` 패키지는 이제 `com.sun.javax.mail` 번들에서 내보내집니다. | 변경 작업을 수행할 필요가 없습니다. | 6.5 LTS GA |
| 공개 소스 | `org.apache.jackrabbit.api` 패키지는 이제 `org.apache.jackrabbit.oak-jackrabbit-api` 번들에서 내보내집니다. | 변경 작업을 수행할 필요가 없습니다. | 6.5 LTS GA |
| 공개 소스 | `com.github.jknack.handlebars`는 지원되지 않음 | 관련 [버전](https://mvnrepository.com/artifact/com.github.jknack/handlebars)을 선택합니다. | 6.5 LTS GA |

## 알려진 문제 {#known-issues}

### AEM 6.5.21-6.5.23 및 AEM 6.5 LTS GA의 JSP 스크립팅 번들 문제

AEM 6.5.21, 6.5.22, 6.5.23 및 AEM 6.5 LTS GA는 알려진 문제가 포함된 `org.apache.sling.scripting.jsp:2.6.0` 번들과 함께 제공됩니다. 이 문제는 AEM 인스턴스가 많은 동시 요청을 처리할 때 높은 부하 상태에서 일반적으로 발생합니다.

이 문제가 발생하면 `org.apache.sling.scripting.jsp:2.6.0`에 대한 참조와 함께 오류 로그에 다음 예외 중 하나가 나타날 수 있습니다.

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

이 문제를 해결하기 위해 핫픽스 [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip)이 제공됩니다.

### SSL 전용 기능으로 인한 Dispatcher 연결 실패 {#ssl-only-feature}

AEM 배포에서 SSL 전용 기능을 활성화하면 Dispatcher와 AEM 인스턴스 간의 연결에 영향을 미치는 알려진 문제가 있습니다. 이 기능을 활성화한 후에는 상태 검사가 실패할 수 있으며 Dispatcher와 AEM 인스턴스 간의 통신이 중단될 수 있습니다. 이 문제는 특히 고객이 `https + IP`을(를) 통해 Dispatcher 인스턴스에서 AEM 인스턴스로 연결하려고 할 때 발생합니다. SNI(Server Name Indication) 유효성 검사 문제와 관련되어 있습니다.

**영향:**

* HTTP 400 응답 코드로 인한 상태 검사 실패
* Dispatcher와 AEM 인스턴스 간의 손상된 트래픽
* Dispatcher를 통해 콘텐츠를 제대로 제공할 수 없음
* Dispatcher 구성에서 IP 주소로 HTTPS를 사용할 때 연결 실패
* HTTPS + IP를 통해 연결할 때 HTTP 400 “잘못된 SNI” 오류

**영향을 받는 환경:**

* Dispatcher 구성을 사용한 AEM 배포
* SSL 전용 기능이 활성화된 시스템
* AEM 인스턴스에 대한 `https + IP` 연결 방법을 사용하는 Dispatcher 구성

**솔루션:**
이 문제가 발생하면 Adobe 고객 지원 센터에 문의하십시오. 이 문제를 해결하기 위해 핫픽스 [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip)이 제공됩니다. 필요한 핫픽스를 적용하기 전에는 SSL 전용 기능을 활성화하지 마십시오.

## 제한된 웹 사이트{#restricted-sites}

이들 웹 사이트는 고객만 사용할 수 있습니다. 고객이시며 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 센터](https://experienceleague.adobe.com/ko/docs/customer-one/using/home)에 문의하십시오.