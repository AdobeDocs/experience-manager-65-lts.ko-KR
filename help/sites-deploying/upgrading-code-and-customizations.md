---
title: 코드 및 사용자 지정 업그레이드
description: AEM에서 코드 및 사용자 지정을 업그레이드하는 방법에 대해 자세히 알아보십시오.
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 3d4e458e4c96c547b94c08d100271ca6cf96f707
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---

# 코드 및 사용자 지정 업그레이드{#upgrading-code-and-customizations}

업그레이드를 계획할 때 다음과 같은 구현 영역을 조사하고 해결해야 합니다.

* [코드 베이스 업그레이드](#upgrade-code-base)
* [테스트 절차](#testing-procedure)

## 개요 {#overview}

1. **AEM 분석기** - [AEM 분석기를 사용한 업그레이드 복잡성 평가](/help/sites-deploying/pattern-detector.md) 페이지에서 정의한 대로 AEM 분석기를 실행합니다. AEM Target 버전에서 사용할 수 없는 API/번들 외에도 해결해야 하는 영역에 대한 자세한 내용을 포함하는 AEM Analyzer 보고서를 가져옵니다. AEM 분석기 보고서는 코드의 비호환성을 나타냅니다. 존재하지 않는 경우 배포는 AEM 6.5 LTS와 호환됩니다. AEM 6.5 LTS를 사용하기 위해 새로운 개발을 수행하도록 선택할 수는 있지만, 단순히 호환성을 유지하기 위해 필요한 것은 아닙니다.
1. **6.5 LTS용 코드 베이스 개발**- Target AEM 버전의 코드 베이스에 대한 전용 분기 또는 저장소를 만듭니다. 업그레이드 전 호환성의 정보를 사용하여 업데이트할 코드 영역을 계획합니다.
1. **6.5 LTS Uber jar로 컴파일**- 코드 기본 POM을 업데이트하여 AEM 6.5 LTS uber jar를 가리키도록 하고 그에 대한 코드를 컴파일합니다.
1. **6.5 LTS 환경에 배포** - 개발/QA 환경에서 AEM 6.5 LTS의 깨끗한 인스턴스(작성자 + 게시)를 설정해야 합니다. 업데이트된 코드 베이스와 대표적인 콘텐츠 샘플(현재 프로덕션)을 배포해야 합니다.
1. **QA 유효성 검사 및 버그 수정** - QA는 AEM 6.5 LTS의 작성자 및 게시 인스턴스 모두에서 응용 프로그램의 유효성을 검사해야 합니다. 발견된 모든 버그를 수정하고 AEM 6.5 LTS 코드 베이스에 커밋해야 합니다. 모든 버그가 수정될 때까지 필요에 따라 개발-주기를 반복합니다.

업그레이드를 진행하기 전에 AEM 6.5 LTS에 대해 철저하게 테스트된 안정적인 애플리케이션 코드 베이스가 있어야 합니다.

## 코드 베이스 업그레이드 {#upgrade-code-base}

### 버전 제어 {#create-a-dedicated-branch-for-6.5-lts-code-in-version-control}에서 6.5 LTS 코드에 대한 전용 분기 만들기

AEM 구현에 필요한 모든 코드 및 구성은 일부 버전의 제어를 사용하여 관리되어야 합니다. AEM 타겟 버전의 코드 베이스에 필요한 변경 사항을 관리하기 위해 버전 제어의 전용 분기를 만들어야 합니다. AEM의 대상 버전 및 후속 버그 수정에 대한 코드 베이스의 반복적인 테스트는 이 분기에서 관리됩니다.

### AEM Uber Jar 버전 업데이트 {#update-the-aem-uber-jar-version}

AEM Uber jar에는 Maven 프로젝트의 `pom.xml`에 단일 종속으로 모든 AEM API가 포함되어 있습니다. 개별 AEM API 종속성을 포함하는 대신 Uber Jar를 단일 종속성으로 포함하는 것이 항상 모범 사례입니다. 코드 베이스를 업그레이드할 때 AEM의 6.5 LTS 버전을 가리키도록 Uber Jar 버전을 변경합니다. 더 이상 사용되지 않는 API 또는 메서드를 AEM의 대상 버전과 호환되도록 업데이트합니다. 새 버전의 Uber Jar에 대해 코드 베이스를 다시 컴파일합니다.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>AEM 6.5와 AEM 6.5 LTS Uber Jar를 포장하는 방식에는 약간의 차이가 있다. 아래 섹션을 참조하십시오.

**AEM 6.5용 Uber Jars**

1. `uber-jar-6.5.x.jar` - AEM 6.5의 모든 공개 API를 포함합니다.
1. `uber-jar-6.5.x-apis-with-deprecations.jar` - 공개 API와 AEM 6.5에서 더 이상 사용되지 않는 API를 모두 포함합니다.

**AEM 6.5 LTS용 Uber Jars**

AEM 6.5 LTS의 경우 두 가지 유형의 Uber Jar가 있습니다.

1. `uber-jar-6.6.x-apis.jar` - AEM 6.5 LTS의 모든 공개 API를 포함합니다.
1. `uber-jar-6.6.x-deprecated-apis.jar` - AEM 6.5 LTS에서 더 이상 사용되지 않는 API만 포함합니다.

**주요 차이점: AEM 6.5와 AEM 6.5 LTS Uber Jars**

* AEM 6.5에서 공개 API와 더 이상 사용되지 않는 API가 모두 필요한 경우 `pom.xml` 파일에 include single jar, `uber-jar-6.5.x-apis-with-deprecations.jar`을(를) 사용할 수 있습니다.
* AEM 6.5 LTS에서 공개 API와 더 이상 사용되지 않는 API가 모두 필요한 경우 공개 API의 경우 `uber-jar-6.6.x-apis.jar`, 더 이상 사용되지 않는 API의 경우 `uber-jar-6.6.x-deprecated-apis.jar`인 두 개의 개별 jar를 포함해야 합니다.

더 이상 사용되지 않는 API Jar에 대한 **Maven 좌표**

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 개발자 노트 {#developer-notes}

* AEM 6.5 LTS에는 Google guava 라이브러리가 기본적으로 포함되어 있지 않으므로 요구 사항에 따라 필요한 버전을 설치할 수 있습니다.
* 이제 Sling XSS 번들은 Java HTML Sanitizer 라이브러리를 사용하며 `XSSAPI#filterHTML()` 메서드는 데이터를 다른 API로 전달하는 것이 아니라 HTML 콘텐츠를 안전하게 렌더링하는 데 사용해야 합니다.

## 테스트 절차 {#testing-procedure}

업그레이드를 테스트할 수 있는 포괄적인 테스트 계획을 마련해야 합니다. 업그레이드된 코드 베이스와 애플리케이션을 먼저 낮은 환경에서 테스트해야 합니다. 발견된 모든 버그는 코드 베이스가 안정될 때까지 반복적인 방식으로 수정해야 하며 상위 수준의 환경만 업그레이드해야 합니다.

### 업그레이드 프로시저 테스트 {#testing-upgrade-procedure}

여기에 설명된 업그레이드 절차는 사용자 지정된 실행 설명서에 설명된 대로 개발 및 QA 환경에서 테스트해야 합니다([업그레이드 계획](/help/sites-deploying/upgrade-planning.md) 참조). 업그레이드 절차는 업그레이드 실행 설명서에 모든 단계가 문서화되고 업그레이드 프로세스가 원활해질 때까지 반복해야 합니다.

### 구현 테스트 영역  {#implementation-test-areas-}

다음은 환경이 업그레이드되고 업그레이드된 코드 베이스가 배포된 후 테스트 계획에서 다루어야 하는 모든 AEM 구현의 중요한 영역입니다.

<table>
 <tbody>
  <tr>
   <td><strong>기능 테스트 영역</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>게시된 사이트</td>
   <td>Dispatcher을 통해 게시 계층 <br />에서 AEM 구현 및 관련 코드를 테스트하는 중입니다. 페이지 업데이트 및 <br /> 캐시 무효화에 대한 기준을 포함해야 합니다.</td>
  </tr>
  <tr>
   <td>작성</td>
   <td>작성자 계층에서 AEM 구현 및 관련 코드 테스트. 페이지, 구성 요소 작성 및 대화 상자를 포함해야 합니다.</td>
  </tr>
  <tr>
   <td>Experience Cloud 솔루션과 통합</td>
   <td>Analytics와 같은 제품과의 통합 확인.</td>
  </tr>
  <tr>
   <td>서드파티 시스템과 통합</td>
   <td>작성자 및 게시 계층 모두에서 서드파티 통합의 유효성을 검사합니다.</td>
  </tr>
  <tr>
   <td>인증, 보안 및 권한</td>
   <td>LDAP/SAML과 같은 모든 인증 메커니즘은 유효성을 검사해야 합니다.<br /> 권한 및 그룹은 작성자 및 게시<br /> 계층 모두에서 테스트해야 합니다.</td>
  </tr>
  <tr>
   <td>쿼리</td>
   <td>쿼리 성능과 함께 사용자 지정 인덱스 및 쿼리를 테스트해야 합니다.</td>
  </tr>
  <tr>
   <td>UI 사용자 지정</td>
   <td>작성 환경에서 AEM UI에 대한 모든 확장 또는 사용자 정의.</td>
  </tr>
  <tr>
   <td>워크플로</td>
   <td>사용자 지정 및/또는 기본 제공 워크플로 및 기능입니다.</td>
  </tr>
  <tr>
   <td>성능 테스트</td>
   <td>로드 테스트는 실제 시나리오를 시뮬레이션하는 작성자 및 게시 계층 모두에서 수행해야 합니다.</td>
  </tr>
 </tbody>
</table>

### 문서 테스트 계획 및 결과 {#document-test-plan-and-results}

위의 구현 테스트 영역을 다루는 테스트 계획을 만들어야 합니다. 테스트 계획을 작성자 및 게시 작업 목록으로 구분하는 것이 적합한 경우가 많습니다. 프로덕션 환경을 업그레이드하기 전에 개발, QA 및 스테이징 환경에서 이 테스트 계획을 실행해야 합니다. 스테이지 및 프로덕션 환경을 업그레이드할 때 비교할 수 있도록 테스트 결과 및 성능 지표를 낮은 환경에서 캡처해야 합니다.
