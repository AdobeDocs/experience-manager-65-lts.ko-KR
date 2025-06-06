---
title: AEM Commerce 개발
description: AEM Project Archetype을 사용하여 상거래 지원 AEM 프로젝트를 생성하는 방법을 알아봅니다. 프로젝트를 빌드하고 로컬 개발 환경에 배포하는 방법에 대해 알아봅니다.
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
solution: Experience Manager,Commerce
role: Admin, Developer
exl-id: 22fcdadf-12c0-4545-a854-76345806386f
source-git-commit: 4c3402aa813c115625d624f3b33ca73d31bed850
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 2%

---

# AEM Commerce 개발 {#develop}

AEM용 Commerce integration framework(CIF)를 기반으로 AEM Commerce 프로젝트를 개발하는 것은 다른 AEM 프로젝트와 동일한 규칙과 모범 사례를 따릅니다. 먼저 다음 사항을 검토하십시오.

- [AEM 개발 사용 안내서](/help/sites-developing/getting-started.md)
- [AEM 핵심 개념](/help/sites-developing/the-basics.md)
- [AEM 개발 - 가이드라인 및 모범 사례](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법](/help/sites-developing/ht-projects-maven.md)

## AEM Commerce을 위한 로컬 개발 {#local}

CIF 프로젝트에서 작업하려면 로컬 개발 환경을 사용하는 것이 좋습니다.

>[!NOTE]
>
>다음 지침은 AEM 6.5 LTS에 중점을 둔 CIF을 사용하여 AEM Commerce에 대한 로컬 AEM 개발 환경을 설정하는 데 도움이 됩니다. AEM as a Cloud Service을 사용하는 경우 [AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html?lang=ko) 설명서를 참조하십시오.

AEM용 AEM Commerce 추가 기능(CIF 추가 기능)은 로컬 개발에도 사용할 수 있으며 AEM 패키지로 제공됩니다. 기능 팩으로 [소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 다운로드할 수 있습니다.

### 필수 소프트웨어

다음은 로컬에 설치해야 합니다.

- 로컬 AEM 6.5 LTS
- [Java 17/Java 21](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/)&#x200B;(3.3.9 이상)
- [노드 LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### CIF 추가 기능 액세스

CIF 추가 기능은 [소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 다운로드하여 &#39;AEM Commerce 추가 기능&#39;을 검색할 수 있습니다.

>[!TIP]
>
>항상 최신 CIF 추가 기능 버전을 사용하십시오.

### 로컬 설정

AEM 및 CIF 추가 기능을 사용하여 로컬 CIF 프로젝트를 개발하는 경우 다음 단계를 수행하십시오.

1. AEM .jar 압축을 풀고 `crx-quickstart` 폴더를 만들려면 다음을 실행하십시오.

   ```bash
   java -jar <jar name> -unpack
   ```

1. `crx-quickstart/install` 폴더 만들기

1. 소프트웨어 배포 포털에서 다운로드한 CIF 추가 기능 모든 패키지를 `crx-quickstart/install` 폴더에 복사합니다.

>[!TIP]
>
>또는 패키지 관리자를 통해 CIF 추가 기능 패키지를 설치할 수도 있습니다.

1. AEM 빠른 시작

OSGI 콘솔을 통해 설정을 확인합니다. `http://localhost:4502/system/console/osgi-installer`. 이 목록에는 CIF 추가 기능 관련 번들, 콘텐츠 패키지 및 OSGI 구성이 포함되어야 합니다. 모든 번들이 시작되었는지 확인하십시오.

## 프로젝트 설정 {#project}

CIF을 사용하여 AEM Commerce 프로젝트를 시작하는 방법에는 두 가지가 있습니다.

### AEM Project Archetype 사용

[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)은(는) CIF을 시작하기 위해 사전 구성된 프로젝트를 부트스트랩하는 기본 도구입니다. CIF 핵심 구성 요소와 필요한 모든 구성을 하나의 추가 옵션으로 생성된 프로젝트에 포함할 수 있습니다.

>[!TIP]
>
>[AEM Project Archetype 25 이상](https://github.com/adobe/aem-project-archetype/releases)을(를) 사용하여 프로젝트를 생성합니다.

AEM 프로젝트를 생성하는 방법은 AEM Project Archetype [사용 지침](https://github.com/adobe/aem-project-archetype#usage)을 참조하십시오. 프로젝트에 CIF을 포함하려면 `includeCommerce` 옵션을 사용하십시오.

예:

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

CIF 핵심 구성 요소는 제공된 `all` 패키지를 포함하거나 CIF 콘텐츠 패키지 및 관련 OSGI 번들을 사용하는 개인을 포함하여 모든 프로젝트에서 사용할 수 있습니다. 프로젝트에 CIF 핵심 구성 요소를 수동으로 추가하려면 다음 종속성을 사용하십시오.

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### AEM Venia 참조 스토어 사용

CIF 프로젝트를 시작하는 두 번째 옵션은 [AEM Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)를 복제하여 사용하는 것입니다. AEM Venia Reference Store는 AEM용 CIF 핵심 구성 요소의 사용을 보여 주는 샘플 참조 상점 첫 번째 애플리케이션입니다. 모범 사례 세트 및 고유한 기능을 개발하기 위한 잠재적인 시작점으로 설계되었습니다.

Venia 참조 저장소를 시작하려면 [Git 저장소](https://github.com/adobe/aem-cif-guides-venia)를 복제하고 필요에 따라 프로젝트를 사용자 지정하기만 하면 됩니다.

>[!NOTE]
>
>Venia 참조 스토어 프로젝트에는 AEM as a Cloud Service 및 AEM 6.5용 빌드 프로필이 두 개 포함되어 있습니다. 사용 방법을 확인하려면 [project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md)을(를) 확인하십시오. AEM 6.5의 경우 `classic` 프로필을 사용합니다.

### AEM을 Commerce 시스템에 연결

프로젝트를 상거래 시스템에 연결하려면 상거래 시스템의 GraphQL 끝점을 사용하여 AEM을 구성해야 합니다.

[AEM Project Archetype](https://github.com/adobe/aem-project-archetype) 또는 [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)에서 생성된 프로젝트에 이미 [기본 구성](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)이 포함되어 있으며 이를 조정해야 합니다.

`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`의 `url` 값을 프로젝트에서 사용하는 상거래 시스템의 GraphQL 끝점으로 바꾸십시오.

AEM Commerce 추가 기능 및 CIF 핵심 구성 요소는 AEM 서버를 통해, 그리고 브라우저를 통해 직접 상거래 GraphQL 엔드포인트에 연결합니다. 클라이언트측 CIF 핵심 구성 요소 및 CIF 추가 기능 제작 도구는 기본적으로 `/api/graphql`에 연결됩니다. 필요한 경우 CIF Cloud Service 구성(아래 참조)을 통해 조정할 수 있습니다.

CIF 추가 기능은 `/api/graphql`에서 GraphQL 프록시 서블릿을 제공합니다. 로컬 AEM Dispatcher을 사용하지 않을 계획이라면 GraphQL 프록시 서블릿도 구성하는 것이 좋습니다.

http://localhost:4502/system/console/configMgr으로 이동하여 `Adobe CIF GraphQL Proxy Configuration` 서비스에 대한 OSGI 구성을 만듭니다. 위의 GraphQL 클라이언트에 사용된 것과 동일한 상거래 시스템의 GraphQL 엔드포인트를 사용합니다.

## 추가 리소스

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)
