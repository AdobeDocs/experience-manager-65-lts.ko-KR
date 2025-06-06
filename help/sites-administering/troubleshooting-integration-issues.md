---
title: 통합 문제 해결
description: Adobe Experience Manager과 통합할 때 문제를 해결하는 방법을 알아봅니다.
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: 72293e17-bf29-4b3c-81b4-cd8372694a0d
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 1%

---

# 통합 문제 해결{#troubleshooting-integration-issues}

## 일반 문제 해결 팁 {#general-troubleshooting-tips}

### JavaScript 오류가 없는지 확인 {#ensure-there-are-no-javascript-errors}

브라우저의 JavaScript 콘솔에 오류가 표시되는지 확인합니다. 처리되지 않은 오류로 인해 후속 코드가 제대로 실행되지 않을 수 있습니다. 오류가 있는 경우 오류를 일으키는 스크립트와 영역을 확인합니다. 스크립트 경로는 스크립트가 속한 기능을 나타낼 수 있습니다.

### 구성 요소 수준 로그온 {#logging-on-component-level}

경우에 따라 구성 요소 수준에서 문을 추가하는 것이 도움이 될 수 있습니다. 구성 요소가 렌더링되므로 잠재적인 문제를 식별하는 데 도움이 될 수 있는 변수 값을 표시하는 임시 마크업을 추가할 수 있습니다. 예:

```
<%
log.info("myVariable={}", myVariable);
%>

<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

로깅에 대한 자세한 내용은 [로깅](/help/sites-deploying/configure-logging.md) 및 [감사 레코드 및 로그 파일 작업](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 페이지를 참조하십시오.

## Analytics 통합 문제 {#analytics-integration-issues}

### Report Importer로 인해 CPU/메모리 사용량이 많음 {#the-report-importer-causes-high-cpu-memory-usage}

보고서 가져오기로 인해 CPU/메모리 사용량이 많거나 `OutOfMemoryError` 예외가 발생합니다.

#### 솔루션 {#solution}

이 문제를 해결하려면 다음을 시도해 보십시오.

* 등록된 PollingImporters가 너무 많지 않은지 확인합니다(아래 &quot;PollingImporter로 인한 시스템 종료 시간&quot; 섹션 참조).
* [OSGi 콘솔](/help/sites-deploying/configuring-osgi.md)에서 `ManagedPollingImporter` 구성에 대한 CRON 식을 사용하여 하루 중 특정 시간에 보고서 가져오기를 실행합니다.

AEM에서 사용자 지정 데이터 가져오기 서비스를 만드는 방법에 대한 자세한 내용은 다음 문서 [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html)을(를) 참조하십시오.

### PollingImporter로 인해 종료가 오래 걸립니다. {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics는 상속 메커니즘을 고려하여 설계되었습니다. 일반적으로 페이지 속성 [클라우드 서비스](/help/sites-developing/extending-cloud-config.md) 탭 내에서 Analytics 구성에 대한 참조를 추가하여 사이트에 대한 Analytics를 사용하도록 설정합니다. 그런 다음 페이지에 다른 구성이 필요하지 않으면 다시 참조할 필요 없이 구성이 모든 하위 페이지에 자동으로 상속됩니다. 사이트에 참조를 추가하면 여러 개의 노드(AEM 6.3 및 이전 버전의 경우 12, AEM 6.4의 경우 6)가 자동으로 만들어집니다   Analytics 데이터를 AEM으로 가져오는 데 사용되는 PollingImporters를 인스턴스화하는 `cq;PollConfig` 형식의 버전)입니다. 그 결과는 다음과 같습니다.

* Analytics를 참조하는 페이지가 많으면 PollingImporter가 많습니다.
* 또한 Analytics 구성을 참조하여 페이지를 복사하고 붙여넣으면 해당 PollingImporter가 중복됩니다.

#### 솔루션 {#solution-1}

먼저 [error.log](/help/sites-deploying/configure-logging.md)을(를) 분석하면 활성 또는 등록된 PollingImporter 양에 대한 통찰력을 얻을 수 있습니다. 예:

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

두 번째로, 최상위 페이지(계층 구조 상단에 있음)에만 Analytics 구성이 참조되었는지 확인합니다.

AEM에서 사용자 지정 데이터 가져오기 서비스를 만드는 방법에 대한 자세한 내용은 다음 문서 [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html)을(를) 참조하십시오.

## DTM(이전) 문제 {#dtm-legacy-issues}

### DTM 스크립트 태그가 페이지 소스에서 렌더링되지 않습니다 {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

페이지 속성 [Cloud Services](/help/sites-developing/extending-cloud-config.md) 탭에서 구성을 참조했지만 [DTM](/help/sites-administering/dtm.md) 스크립트 태그가 페이지에 제대로 포함되지 않았습니다.

#### 솔루션 {#solution-2}

문제를 해결하려면 다음을 시도해 보십시오.

* 암호화된 속성의 암호를 해독할 수 있는지 확인합니다(암호화는 각 AEM 인스턴스에서 자동으로 생성된 다른 키를 사용할 수 있음). 자세한 내용은 [구성 속성에 대한 암호화 지원](/help/sites-administering/encryption-support-for-configuration-properties.md)도 참조하십시오.
* `/etc/cloudservices/dynamictagmanagement`에 있는 구성 다시 게시
* `/etc/cloudservices`에서 ACL을 확인합니다. ACL은 다음과 같아야 합니다.

   * allow; jcr:read; webservice-support-servicelibfinder
   * allow; jcr:read; everyone; `rep:glob:`&ast;`/defaults/`&ast;
   * allow; jcr:read; everyone; `rep:glob:`&ast;`/defaults`
   * allow; jcr:read; everyone; `rep:glob:`&ast;`/public/`&ast;
   * allow; jcr:read; everyone; `rep:glob:`&ast;`/public`

ACL 관리에 대한 자세한 내용은 [사용자 관리 및 보안](/help/sites-administering/security.md#permissions-in-aem) 페이지를 참조하십시오.

## Target 통합 문제 {#target-integration-issues}

### 사용자 지정 페이지 구성 요소를 사용할 때 타겟팅된 콘텐츠가 미리보기 모드에 표시되지 않음 {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

이 문제는 사용자 지정 페이지 구성 요소에 Target DTM 통합을 처리하는 올바른 JSP 또는 클라이언트 라이브러리가 포함되지 않기 때문에 발생합니다.

#### 솔루션 {#solution-3}

다음 솔루션을 시도할 수 있습니다.

* 사용자 지정 `headlibs.jsp`(있는 경우 `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`)에 다음 항목이 포함되어 있는지 확인하십시오.

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* 사용자 지정 `head.html`(`/apps/<CUSTOM-COMPONENTS-PATH>/head.html`인 경우) **이(가) 아래 예와 같이 특정 통합 헤드셋을 선택적으로 포함하지 않는지**&#x200B;확인하십시오.

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

`servicelibs.jsp`은(는) 필요한 analytics JavaScript 개체를 추가하고 웹 사이트와 연결된 클라우드 서비스 라이브러리를 로드합니다. Target 서비스의 경우 라이브러리는 `/libs/cq/analytics/components/testandtarget/headlibs.jsp`을 통해 로드됩니다.

로드되는 라이브러리 집합은 Target 구성에 사용된 대상 클라이언트 라이브러리 형식(`mbox.js` 또는 `at.js`)에 따라 다릅니다.

DTM을 사용하여 `mbox.js` 또는 `at.js`을(를) 전달할 때 콘텐츠가 렌더링되기 전에 라이브러리가 로드되었는지 확인하십시오. 이러한 라이브러리를 비동기적으로 로드하는 Tag Management 시스템을 사용하면 타겟 특정 JavaScript 코드를 실행하는 데 문제가 발생할 수 있습니다.

자세한 내용은 [타깃팅된 콘텐츠에 대한 개발](/help/sites-developing/target.md#understanding-the-target-component) 페이지를 참조하세요.

### 브라우저 콘솔에 &quot;AppMeasurement 초기화에서 보고서 세트 ID 누락&quot; 오류가 표시됩니다 {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

이 문제는 Adobe Analytics이 DTM을 사용하여 웹 사이트에서 구현되고 사용자 지정 코드를 사용할 때 나타날 수 있습니다. 원인은 `s = new AppMeasurement()`을(를) 사용하여 `s` 개체를 인스턴스화하는 것입니다.

#### 솔루션 {#solution-4}

`new AppMeasurement` 인스턴스화 메서드 대신 `s_gi` 사용. 예:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### 올바른 오퍼 대신 기본 오퍼가 임의로 표시됩니다 {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

이 문제는 다음과 같은 여러 가지 원인이 있을 수 있습니다.

* 타사 Tag Management 시스템을 사용하여 Target 클라이언트 라이브러리(`mbox.js` 또는 `at.js`)를 비동기식으로 로드하면 타깃팅이 임의로 중단될 수 있습니다. Target 라이브러리는 페이지 헤드에서 동기적으로 로드되어야 합니다. 이는 라이브러리가 AEM에서 전달될 때 항상 적용됩니다.

* 두 개의 Target 클라이언트 라이브러리(`at.js`)를 동시에 로드합니다. 예를 들어 하나는 DTM을 사용하고 다른 하나는 AEM의 Target 구성을 사용합니다. `at.js` 버전이 다른 경우 `adobe.target` 정의에 충돌이 발생할 수 있습니다.

#### 솔루션 {#solution-5}

다음 솔루션을 시도할 수 있습니다.

* DTM과 유사한 라이브러리를 로드하는 고객 코드(결과적으로 Target 라이브러리를 로드함)가 [페이지 헤드](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages)에서 동기적으로 실행되는지 확인하십시오.
* 사이트가 DTM을 사용하여 Target 라이브러리를 전달하도록 구성된 경우, [사이트에 대한 Target 구성](https://helpx.adobe.com/kr/experience-manager/6-3/sites/administering/using/target-configuring.html)에서 **DTM에 의해 전달된 Clientlib** 옵션이 선택되어 있는지 확인하십시오.

### AT.js 1.3+를 사용할 때 올바른 오퍼 대신 항상 기본 오퍼가 표시됩니다 {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

기본적으로 AEM 6.2 및 6.3은 AT.js 버전 1.3.0+와 호환되지 않습니다. AT.js 버전 1.3.0에서 해당 API에 대한 매개 변수 유효성 검사를 도입하면 `adobe.target.applyOffer()`에 `atjs-itegration.js` 코드에서 제공하지 않는 &quot;mbox&quot; 매개 변수가 필요합니다.

#### 솔루션 {#solution-6}

이 문제를 해결하려면 `atjs-itegration.js`을(를) 편집하고 `adobe.target.applyOffer()`에 대한 매개 변수 개체에 `"mbox": mboxName` 필드를 다음과 같이 추가하십시오.

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### 목표 및 설정 페이지에 보고 소스 섹션이 표시되지 않습니다 {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

이 문제는 [A4T Analytics Cloud 구성](/help/sites-administering/target-configuring.md) 프로비전 문제일 가능성이 높습니다.

#### 솔루션 {#solution-7}

AEM에 다음 확인 요청을 발행하여 Target 계정에 대해 A4T가 제대로 활성화되었는지 확인해야 합니다.

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json

{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

응답에 줄 `a4tEnabled:false`이(가) 포함된 경우 [Adobe 고객 지원 센터](https://helpx.adobe.com/kr/contact.html)에 연락하여 계정이 올바르게 프로비저닝되도록 하십시오.

### 유용한 Target API {#helpful-target-apis}

다음은 Target 문제를 해결할 때 유용할 수 있는 두 가지 Target API입니다.

* 지정된 클라이언트 코드에 대한 Target 끝점 검색

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* 클라이언트의 프로필 검색

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>

Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```
