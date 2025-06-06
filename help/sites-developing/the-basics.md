---
title: AEM 핵심 개념
description: JCR, Sling, OSGi, Dispatcher, 워크플로우 및 MSM을 이해하는 등 Adobe Experience Manager(AEM)를 구성하는 방식과 그 위에서 개발하는 방법에 대한 핵심 개념에 대한 개요입니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: fe3735ff-5c9b-4eb8-bf1d-f2189ec7e26f
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '3251'
ht-degree: 0%

---

# AEM 핵심 개념 {#aem-core-concepts}

>[!NOTE]
>
>Adobe Experience Manager(AEM)의 핵심 개념을 시작하기 전에 Adobe은 [AEM Sites 개발 시작하기](/help/sites-developing/getting-started.md) 문서에서 WKND 자습서를 완료해 줄 것을 권장합니다. 여기에는 AEM 개발 프로세스에 대한 개요와 핵심 개념에 대한 소개가 포함되어 있습니다.

## AEM에서 개발하기 위한 사전 요구 사항 {#prerequisites-for-developing-on-aem}

AEM을 기반으로 개발하려면 다음 기술이 필요합니다.

* 다음을 포함한 웹 애플리케이션 기술에 대한 기본 지식:

   * 요청 -응답(XMLHttpRequest / XMLHttpResponse) 주기
   * HTML
   * CSS
   * JavaScript

* Content Explorer를 포함한 Experience Server(CRX)의 작업 지식
* 클래식 UI에서 개발하려면 간단한 JSP 예를 이해하고 수정하는 기능을 비롯한 JSP(JavaServer Pages)에 대한 기본 지식도 필요합니다.

또한 [지침 및 모범 사례](/help/sites-developing/dev-guidelines-bestpractices.md)를 읽고 따르는 것이 좋습니다.

## Java™ 콘텐츠 저장소 {#java-content-repository}

Java™ JCR(Content Repository) 표준 [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)은(는) 콘텐츠 저장소 내의 세분화된 수준에서 양방향으로 콘텐츠에 액세스하는 공급업체 독립적이고 구현 독립적인 방법을 지정합니다.

사양 리드는 Adobe Research (스위스) AG가 담당합니다.

[JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) 패키지, javax.jcr.&ast;는 저장소 콘텐츠에 직접 액세스하고 조작하는 데 사용됩니다.

## Experience Server(CRX) 및 Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server는 AEM이 기반으로 하고 사용자 지정 애플리케이션을 빌드하는 데 사용할 수 있는 Experience Services를 제공하며 Jackrabbit을 기반으로 콘텐츠 저장소를 임베드합니다.

[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html)은(는) JCR API 2.0의 구현을 완전히 준수하는 오픈 소스입니다.

## Sling 요청 처리 {#sling-request-processing}

### Sling 소개 {#introduction-to-sling}

AEM은 콘텐츠 기반 응용 프로그램을 쉽게 개발할 수 있도록 하는 REST 원칙을 기반으로 한 웹 응용 프로그램 프레임워크인 [Sling](https://sling.apache.org/index.html)을(를) 사용하여 빌드되었습니다. Sling은 Apache Jackrabbit과 같은 JCR 저장소 또는 AEM이 있는 경우 CRX 컨텐츠 저장소를 데이터 저장소로 사용합니다. Sling은 Apache Software Foundation에 기여했습니다. 자세한 내용은 Apache에서 확인할 수 있습니다.

Sling을 사용하면 렌더링되는 콘텐츠 유형이 첫 번째 처리 고려 사항이 아닙니다. 대신 URL이 렌더링을 수행하는 스크립트를 찾을 수 있는 콘텐츠 객체로 확인되는지 여부가 주요 고려 사항입니다. 이렇게 하면 웹 콘텐츠 작성자가 요구 사항에 맞게 쉽게 사용자 지정된 페이지를 작성할 수 있습니다.

이러한 유연성의 장점은 다양한 콘텐츠 요소의 범위가 있는 응용 프로그램이나 쉽게 사용자 지정할 수 있는 페이지가 필요한 경우에 명확하게 나타납니다. 특히 AEM 솔루션에서 WCM과 같은 웹 컨텐츠 관리 시스템을 구현할 때

Sling을 사용하여 개발하는 첫 번째 단계는 [15분 후에 Sling 검색](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html)을 참조하십시오.

다음 다이어그램에서는 Sling 스크립트 해상도를 설명합니다. HTTP 요청에서 콘텐츠 노드로, 콘텐츠 노드에서 리소스 유형으로, 리소스 유형에서 스크립트로 가져오는 방법과 사용 가능한 스크립팅 변수를 보여 줍니다.

![Apache Sling 스크립트 해상도 이해](assets/sling-cheatsheet-01.png)

다음 다이어그램은 SlingPostServlet을 처리할 때 사용할 수 있는 숨겨져 있지만 강력한 모든 요청 매개 변수에 대해 설명합니다. 여기에는 저장소의 노드를 생성, 수정, 삭제, 복사 및 이동할 수 있는 끝없는 옵션을 제공하는 모든 POST 요청에 대한 기본 처리기가 포함되어 있습니다.

![SlingPostServlet 사용](assets/sling-cheatsheet-02.png)

### Sling은 콘텐츠 중심적입니다. {#sling-is-content-centric}

Sling은 *콘텐츠 중심*&#x200B;입니다. 즉, 각 (HTTP) 요청이 JCR 리소스(저장소 노드) 형태의 콘텐츠에 매핑되므로 콘텐츠에 처리가 집중됩니다.

* 첫 번째 타겟은 콘텐츠를 보유하는 리소스(JCR 노드)입니다
* 두 번째로, 표시 또는 스크립트는 요청의 특정 부분(예: 선택기 및/또는 확장)과 결합된 리소스 속성에서 가져옵니다

### RESTful Sling {#restful-sling}

콘텐츠 중심 철학으로 인해 Sling은 REST 기반 서버를 구현하므로 웹 애플리케이션 프레임워크에 새로운 개념이 도입되었습니다. 장점은 다음과 같습니다.

* 표면뿐만 아니라 RESTful입니다. 리소스와 표현은 서버 내부에서 올바르게 모델링됩니다.
* 하나 이상의 데이터 모델 제거

   * 이전에는 URL 구조, 비즈니스 개체, DB 스키마,
   * 이제 다음으로 줄임: URL = resource = JCR 구조

### URL 분해 {#url-decomposition}

Sling에서 처리는 사용자 요청의 URL에 의해 결정됩니다. 적절한 스크립트로 표시할 콘텐츠를 정의합니다. 이를 위해 URL에서 정보가 추출됩니다.

다음 URL을 분석하는 경우:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

이를 복합 부품으로 분류할 수 있습니다.

| 프로토콜 | 호스트 | 콘텐츠 경로 | 선택기 | 확장 |  | 접미사 |  | 매개 변수 |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | 도구/스파이 | .printable.a4. | html | / | a/b | ? | x=12 |

**프로토콜** HTTP

웹 사이트의 **호스트** 이름입니다.

**콘텐츠 경로** 렌더링할 콘텐츠를 지정하는 경로입니다. 확장과 함께 사용됩니다. 이 예제에서는 `tools/spy.html`(으)로 변환됩니다.

**선택기** 콘텐츠를 렌더링하는 다른 방법에 사용됩니다. 이 예제에서는 프린터에 친숙한 A4 형식의 버전을 사용합니다.

**확장** 콘텐츠 형식; 렌더링에 사용할 스크립트도 지정합니다.

**접미사**&#x200B;를 사용하여 추가 정보를 지정할 수 있습니다.

**params** 동적 콘텐츠에 필요한 모든 매개 변수입니다.

#### URL에서 컨텐츠 및 스크립트로 {#from-url-to-content-and-scripts}

다음 원칙을 사용합니다.

* 매핑은 요청에서 추출된 콘텐츠 경로를 사용하여 리소스를 찾습니다
* 적절한 리소스가 있으면 sling 리소스 유형이 추출되고, 콘텐츠 렌더링에 사용할 스크립트를 찾는 데 사용됩니다

아래 이미지는 사용된 메커니즘을 보여 주는 이미지이며, 이 메커니즘에 대해서는 다음 섹션에서 자세히 설명합니다.

![chlimage_1-86](assets/chlimage_1-86a.png)

Sling을 사용하면 JCR 노드에서 `sling:resourceType` 속성을 설정하여 특정 엔터티를 렌더링하는 스크립트를 지정할 수 있습니다. 이 메커니즘은 리소스가 여러 변환을 가질 수 있으므로 스크립트가 데이터 엔티티에 액세스하는 것(PHP 스크립트의 SQL 문처럼)보다 더 많은 자유를 제공합니다.

#### 리소스에 요청 매핑 {#mapping-requests-to-resources}

요청이 분류되고 필요한 정보가 추출됩니다. 요청된 리소스(컨텐츠 노드)에 대해 저장소가 검색됩니다.

* 첫 번째 Sling은 노드가 요청에 지정된 위치에 있는지 확인합니다(예: `../content/corporate/jobs/developer.html`).
* 노드가 없으면 확장이 삭제되고 검색이 반복됩니다(예: `../content/corporate/jobs/developer`).
* 노드를 찾을 수 없으면 Sling은 http 코드 404(찾을 수 없음)를 반환합니다.

또한 Sling을 사용하면 JCR 노드 이외의 항목을 리소스가 될 수 있지만, 이는 고급 기능입니다.

### 스크립트 찾기 {#locating-the-script}

적절한 리소스(콘텐츠 노드)가 있으면 **sling 리소스 유형**&#x200B;이 추출됩니다. 콘텐츠 렌더링에 사용할 스크립트를 찾는 경로입니다.

`sling:resourceType`에서 지정한 경로는 다음 중 하나일 수 있습니다.

* 절대
* 구성 매개 변수 관련

  상대 경로는 휴대성을 높이므로 Adobe에서 권장합니다.

모든 Sling 스크립트는 `/apps` 또는 `/libs`의 하위 폴더에 저장되며 이 순서대로 검색됩니다([구성 요소 및 기타 요소 사용자 지정](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements) 참조).

몇 가지 주목할 사항은 다음과 같습니다.

* 메서드(GET, POST)가 필요한 경우 HTTP 사양(예: jobs.POST.esp)에 따라 대문자로 지정됩니다(아래 참조)
* 다양한 스크립트 엔진이 지원됩니다.

   * HTL(HTML Template Language - Adobe Experience Manager의 HTML 기본 및 권장 서버측 템플릿 시스템): `.html`
   * ECMAScript(JavaScript) 페이지(서버측 실행): `.esp, .ecma`
   * Java™ 서버 페이지(서버측 실행): `.jsp`
   * Java™ 서블릿 컴파일러(서버측 실행): `.java`
   * JavaScript 템플릿(클라이언트측 실행): `.jst`

지정된 AEM 인스턴스에서 지원하는 스크립트 엔진 목록이 Felix 관리 콘솔(`http://<host>:<port>/system/console/slingscripting`)에 나열됩니다.

또한 Apache Sling은 다른 인기 있는 스크립팅 엔진(예: Groovy, JRuby, Freemarker)과의 통합을 지원하며 새로운 스크립팅 엔진을 통합하는 방법을 제공합니다.

위의 예를 사용하여 `sling:resourceType`이(가) `hr/jobs`인 경우 다음 작업을 수행합니다.

* GET/HEAD 요청 및 .html로 끝나는 URL(기본 요청 유형, 기본 형식)

  스크립트는 /apps/hr/jobs/jobs.esp이며 sling:resourceType의 마지막 섹션이 파일 이름을 형성합니다.

* POST 요청(GET/HEAD을 제외한 모든 요청 유형, 메서드 이름은 대문자여야 함)

  스크립트 이름에는 POST가 사용됩니다.

  스크립트는 `/apps/hr/jobs/jobs.POST.esp`입니다.

* .html로 끝나지 않는 다른 형식의 URL

  예, `../content/corporate/jobs/developer.pdf`

  스크립트는 `/apps/hr/jobs/jobs.pdf.esp`입니다. 스크립트 이름에 접미사가 추가됩니다.

* 선택기가 있는 URL

  선택기를 사용하여 동일한 콘텐츠를 대체 형식으로 표시할 수 있습니다. 예를 들어 프린터에 친숙한 버전, rss 피드 또는 요약이 있습니다.

  선택기가 `../content/corporate/jobs/developer.print.html`과(와) 같이 *인쇄*&#x200B;일 수 있는 프린터 전용 버전을 확인하는 경우

  스크립트가 `/apps/hr/jobs/jobs.print.esp`입니다. 선택기가 스크립트 이름에 추가됩니다.

* sling:resourceType이 정의되지 않은 경우 다음을 수행합니다.

   * 콘텐츠 경로는 적절한 스크립트를 검색하는 데 사용됩니다(경로 기반 ResourceTypeProvider가 활성화된 경우).

     예를 들어 `../content/corporate/jobs/developer.html`에 대한 스크립트는 `/apps/content/corporate/jobs/`에서 검색을 생성합니다.

   * 기본 노드 유형이 사용됩니다.

* 스크립트가 없으면 기본 스크립트가 사용됩니다.

  기본 렌디션은 일반 텍스트(.txt), HTML(.html) 및 JSON(.json)으로 지원되며, 이 모든 렌디션은 노드의 속성(적절한 형식)을 나열합니다. 확장 .res의 기본 렌디션 또는 요청 확장명이 없는 요청은 리소스를 스풀 처리하는 것입니다(가능한 경우).
* HTTP 오류 처리(코드 403 또는 404)의 경우 Sling은 다음 중 하나에서 스크립트를 찾습니다.

   * [사용자 지정된 스크립트](/help/sites-developing/customizing-errorhandler-pages.md)에 대한 위치 /apps/sling/servlet/errorhandler
   * 또는 각각 표준 스크립트 /libs/sling/servlet/errorhandler/403.esp 또는 404.esp의 위치입니다.

주어진 요청에 여러 스크립트가 적용되는 경우 가장 일치하는 스크립트를 선택합니다. 일치가 구체적일수록 더 좋습니다. 즉, 요청 확장이나 메서드 이름 일치에 관계없이 더 많은 선택기가 더 잘 일치합니다.

예를 들어 리소스에 대한 액세스 요청을 고려해 보십시오
`/content/corporate/jobs/developer.print.a4.html`
유형
`sling:resourceType="hr/jobs"`

올바른 위치에 다음 스크립트 목록이 있다고 가정합니다.

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

기본 설정 순서는 (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1)입니다.

주로 `sling:resourceType` 속성으로 정의되는 리소스 형식 외에도 리소스 슈퍼 형식도 있습니다. 이는 `sling:resourceSuperType` 속성으로 표시됩니다. 이러한 슈퍼 유형은 스크립트를 찾으려고 할 때도 고려됩니다. 리소스 슈퍼 유형의 장점은 기본 리소스 유형 `sling/servlet/default`(기본 서블릿에서 사용)이 루트인 리소스의 계층 구조를 형성할 수 있다는 것입니다.

리소스의 리소스 슈퍼 타입은 두 가지 방식으로 정의될 수 있다:

* 리소스의 `sling:resourceSuperType` 속성별.
* `sling:resourceType`이(가) 가리키는 노드의 `sling:resourceSuperType` 속성별.

예:

* /

   * a
   * b

      * sling:resourceSuperType = a

   * c

      * sling:resourceSuperType = b

   * x

      * sling:resourceType = c

   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a

유형 계층:

* `/x`
   * 은(는) `[ c, b, a, <default>]`임
* 동안 `/y`
   * 계층 구조는 `[ c, a, <default>]`입니다.

이는 `/y`에는 `sling:resourceSuperType` 속성이 있지만 `/x`에는 없으므로 해당 슈퍼타입을 리소스 형식에서 가져오기 때문입니다.

#### Sling 스크립트는 직접 호출할 수 없습니다. {#sling-scripts-cannot-be-called-directly}

Sling에서 스크립트는 REST 서버의 엄격한 개념을 손상시킬 수 있으므로 직접 호출할 수 없습니다. 리소스와 표현을 혼합해야 합니다.

표현(스크립트)을 직접 호출하는 경우 스크립트 내에 리소스를 숨김으로써 프레임워크(Sling)가 더 이상 해당 리소스를 알지 못합니다. 따라서 다음과 같은 특정 기능이 손실됩니다.

* 다음을 포함한 GET 이외의 http 메서드 자동 처리:

   * POST, PUT 및 DELETE - 슬링 기본 구현으로 처리됨
   * sling:resourceType 위치의 `POST.jsp` 스크립트

* 코드 아키텍처가 더 이상 깔끔하거나 구조화되지 않으므로 대규모 개발의 경우 매우 중요합니다

### Sling API {#sling-api}

Sling API 패키지 org.apache.sling을 사용합니다.&ast; 및 태그 라이브러리

### sling:include를 사용하여 기존 요소 참조 {#referencing-existing-elements-using-sling-include}

마지막으로 스크립트 내의 기존 요소를 참조해야 한다는 점을 고려해야 합니다.

더 복잡한 스크립트(집계 스크립트)는 여러 리소스(예: 탐색, 사이드바, 바닥글, 목록의 요소)에 액세스해야 하며 *resource*&#x200B;을(를) 포함하여 액세스해야 합니다.

이렇게 하려면 sling:include(&quot;/&lt;경로>/&lt;리소스>&quot;) 명령을 사용합니다. 여기에는 이미지 렌더링에 대한 기존 정의를 참조하는 다음 문과 같이 참조된 리소스의 정의가 효과적으로 포함됩니다.

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi는 모듈식 애플리케이션과 라이브러리(Java™용 동적 모듈 시스템이라고도 함)를 개발 및 배포하기 위한 아키텍처를 정의합니다. OSGi 컨테이너를 사용하여 애플리케이션을 개별 모듈(추가 메타 정보가 있는 jar 파일이며 OSGi 용어로 번들이라고 함)로 분류하고 다음과 같이 애플리케이션 간의 상호 종속성을 관리할 수 있습니다.

* 컨테이너 내에서 구현된 서비스
* 컨테이너와 애플리케이션 간의 계약

이러한 서비스 및 계약은 개별 요소가 협업을 위해 서로를 동적으로 발견할 수 있도록 하는 아키텍처를 제공합니다.

그런 다음 OSGi 프레임워크는 다시 시작할 필요 없이 이러한 번들의 동적 로딩/언로딩, 구성 및 제어를 제공합니다.

>[!NOTE]
>
>OSGi 기술에 대한 전체 정보는 [OSGi 웹 사이트](https://www.osgi.org)에서 찾을 수 있습니다.
>
>특히 그들의 기초학력페이지에는 발표와 자습서 모음집이 실려 있다.

이 아키텍처를 사용하면 애플리케이션별 모듈로 Sling을 확장할 수 있습니다. Sling과 CQ5는 OSGI(Open Services Gateway 이니셔티브)의 [Apache Felix](https://felix.apache.org/documentation/index.html) 구현을 사용하며 OSGi 서비스 플랫폼 릴리스 4 버전 4.2 사양을 기반으로 합니다. 둘 다 OSGi 프레임워크 내에서 실행되는 OSGi 번들의 컬렉션입니다.

이렇게 하면 설치 내의 패키지에 대해 다음 작업을 수행할 수 있습니다.

* 설치
* 시작
* stop
* 업데이트
* 제거
* 상태 보기
* 특정 번들에 대한 자세한 정보(예: 기호 이름, 버전 및 위치)에 액세스합니다

자세한 내용은 [웹 콘솔](/help/sites-deploying/web-console.md), [OSGI 구성](/help/sites-deploying/configuring-osgi.md) 및 [OSGi 구성 설정](/help/sites-deploying/osgi-configuration-settings.md)을 참조하십시오.

## AEM 환경의 개발 개체 {#development-objects-in-the-aem-environment}

다음은 개발의 관심사입니다.

**항목** 항목이 노드 또는 속성입니다.

Item 개체 조작에 대한 자세한 내용은 javax.jcr.Item 인터페이스의 [Java™ 문서](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html)를 참조하십시오

**노드(및 해당 속성)** 노드 및 해당 속성은 JCR API 2.0 사양(JSR 283)에 정의되어 있습니다. 컨텐츠, 객체 정의, 렌더링 스크립트 및 기타 데이터를 저장합니다.

노드는 콘텐츠 구조를 정의하며 해당 속성은 실제 콘텐츠와 메타데이터를 저장합니다.

컨텐츠 노드는 렌더링을 구동합니다. Sling은 수신 요청에서 콘텐츠 노드를 가져옵니다. 이 노드의 sling:resourceType 속성은 사용할 Sling 렌더링 구성 요소를 가리킵니다.

JCR 이름인 노드는 Sling 환경에서 리소스라고도 합니다.

예를 들어 현재 노드의 속성을 가져오려면 스크립트에서 다음 코드를 사용할 수 있습니다.

`PropertyIterator properties = currentNode.getProperties();`

현재 노드 개체가 되는 currentNode입니다.

노드 개체 조작에 대한 자세한 내용은 [Java™ 문서](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html)를 참조하십시오.

**위젯** AEM의 모든 사용자 입력은 위젯에 의해 관리됩니다. 이러한 속성은 종종 콘텐츠 편집을 제어하는 데 사용됩니다.

대화 상자는 위젯을 결합하여 작성됩니다.

AEM은 위젯의 ExtJS 라이브러리를 사용하여 개발되었습니다.

**대화 상자** 대화 상자는 특수한 유형의 위젯입니다.

콘텐츠를 편집하기 위해 AEM에서는 애플리케이션 개발자가 정의한 대화 상자를 사용합니다. 이러한 구성 요소는 일련의 위젯을 결합하여 사용자에게 관련 컨텐츠를 편집하는 데 필요한 모든 필드 및 작업을 제공합니다.

대화 상자는 메타데이터 편집 및 다양한 관리 도구에도 사용됩니다.

**구성 요소** 소프트웨어 구성 요소는 미리 정의된 서비스 또는 이벤트를 제공하는 시스템 요소이며 다른 구성 요소와 통신할 수 있습니다.

AEM 내에서 구성 요소는 리소스의 콘텐츠를 렌더링하는 데 종종 사용됩니다. 리소스가 페이지인 경우 렌더링하는 구성 요소를 최상위 구성 요소 또는 페이지 구성 요소라고 합니다. 그러나 구성 요소는 콘텐츠를 렌더링하거나 특정 리소스에 연결할 필요가 없습니다. 예를 들어 탐색 구성 요소는 여러 리소스에 대한 정보를 표시합니다.

구성 요소의 정의에는 다음이 포함됩니다.

* 콘텐츠를 렌더링하는 데 사용되는 코드
* 사용자 입력 및 결과 컨텐츠 구성을 위한 대화 상자입니다.

**템플릿** 템플릿은 특정 유형의 페이지에 대한 기준입니다. 웹 사이트 탭에서 페이지를 만들 때 사용자는 템플릿을 선택해야 합니다. 그런 다음 이 템플릿을 복사하여 새 페이지가 만들어집니다.

템플릿은 만들 페이지와 구조가 동일하지만 실제 컨텐츠는 없는 노드의 계층입니다.

페이지 렌더링에 사용되는 페이지 구성 요소와 기본 콘텐츠(기본 최상위 콘텐츠)를 정의합니다. 콘텐츠는 AEM이 콘텐츠 중심적이므로 렌더링하는 방법을 정의합니다.

**페이지 구성 요소(최상위 구성 요소)** 페이지를 렌더링하는 데 사용할 구성 요소입니다.

**페이지** 페이지는 템플릿의 &#39;인스턴스&#39;입니다.

페이지에는 cq:Page 유형의 계층 구조 노드와 cq:PageContent 유형의 콘텐츠 노드가 있습니다. 콘텐츠 노드의 sling:resourceType 속성은 페이지 렌더링에 사용되는 페이지 구성 요소를 가리킵니다.

예를 들어 현재 페이지의 이름을 가져오려면 스크립트에서 다음 코드를 사용할 수 있습니다.

S`tring pageName = currentPage.getName();`

현재 페이지 개체인 TcurrentPage입니다. 페이지 개체 조작에 대한 자세한 내용은 [Java™ 문서](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/Page.html)를 참조하십시오.

**페이지 관리자** 페이지 관리자는 페이지 수준 작업을 위한 메서드를 제공하는 인터페이스입니다.

예를 들어, 리소스의 포함 페이지를 가져오려면 스크립트에서 다음 코드를 사용할 수 있습니다.

Page myPage = pageManager.getContainingPage(myResource);

pageManager 개체는 pageManager 개체이고 myResource는 리소스 개체입니다. 페이지 관리자에서 제공하는 메서드에 대한 자세한 내용은 [Java™ 문서](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageManager.html)를 참조하십시오.

## 저장소 내의 구조 {#structure-within-the-repository}

다음 목록은 저장소 내에 표시되는 구조에 대한 개요를 제공합니다.

>[!CAUTION]
>
>이 구조 또는 구조 내의 파일에 대한 변경은 신중하게 이루어져야 합니다.
>
>개발 중에는 변경 사항이 필요하지만, 변경 사항이 미치는 영향을 완전히 이해해야 합니다.

>[!CAUTION]
>
>`/libs` 경로에서 아무 것도 변경하지 마십시오. 구성 및 기타 변경 내용을 보려면 항목을 `/libs`에서 `/apps`(으)로 복사하고 `/apps` 내에서 변경합니다.

* `/apps`

  애플리케이션 관련. 웹 사이트와 관련된 구성 요소 정의를 포함합니다. 개발하는 구성 요소는 `/libs/foundation/components`에서 사용할 수 있는 기본 구성 요소를 기반으로 할 수 있습니다.

* `/content`

  웹 사이트용으로 생성된 콘텐츠.

* `/etc`

* `/home`

  사용자 및 그룹 정보.

* `/libs`

  AEM의 핵에 속하는 라이브러리 및 정의입니다. `/libs`의 하위 폴더는 검색 또는 복제와 같은 기본 AEM 기능을 나타냅니다. `/libs`의 콘텐츠는 AEM 작동 방식에 영향을 주므로 수정해서는 안 됩니다. 웹 사이트 관련 기능은 `/apps`에서 개발해야 합니다([구성 요소 및 기타 요소 사용자 지정](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements) 참조).

* `/tmp`

  임시 작업 영역.

* `/var`

  감사 로그, 통계, 이벤트 처리 등 시스템에서 변경 및 업데이트되는 파일.

## 환경 {#environments}

AEM을 사용하면 프로덕션 환경은 종종 [작성자 및 게시 인스턴스](/help/sites-deploying/deploy.md#author-and-publish-installs)의 두 가지 다른 유형의 인스턴스로 구성됩니다.

## 더 Dispatcher {#the-dispatcher}

Dispatcher은 캐싱 및/또는 로드 밸런싱을 위한 Adobe의 도구입니다. 자세한 내용은 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ko-KR)에서 확인할 수 있습니다.

## FileVault(소스 버전 시스템) {#filevault-source-revision-system}

FileVault는 JCR 저장소에 파일 시스템 매핑 및 버전 제어를 제공합니다. 표준 버전 제어 시스템(예: Subversion)에서 프로젝트 코드, 콘텐츠, 구성 등을 저장하고 버전 관리하는 데 필요한 모든 지원을 받아 AEM 개발 프로젝트를 관리하는 데 사용할 수 있습니다.

자세한 내용은 [FileVault 도구](/help/sites-developing/ht-vlttool.md) 설명서를 참조하십시오.

## 워크플로 {#workflows}

컨텐츠는 여러 참가자의 승인 및 승인과 같은 단계를 비롯한 조직 프로세스의 영향을 받습니다. 이러한 프로세스는 워크플로우로 [정의되고 AEM 내에서 개발](/help/sites-developing/workflows-models.md)된 다음 필요에 따라 [적절한 컨텐츠 페이지](/help/sites-administering/workflows.md) 또는 [디지털 자산](/help/assets/assets-workflow.md)에 적용할 수 있습니다.

워크플로 엔진은 워크플로의 구현과 해당 콘텐츠에 대한 후속 응용 프로그램을 관리하는 데 사용됩니다.

## 다중 사이트 관리 {#multi-site-management}

MSM(다중 사이트 관리자)을 사용하면 공통 콘텐츠를 공유하는 여러 웹 사이트를 쉽게 관리할 수 있습니다. MSM을 사용하면 한 사이트의 콘텐츠 변경 내용이 다른 사이트에서 자동으로 복제되도록 사이트 간의 관계를 정의할 수 있습니다.

예를 들어 웹 사이트는 국제 대상자를 위해 여러 언어로 제공되는 경우가 많습니다. 동일한 언어의 사이트 수가 적은 경우(3~5개), 사이트 간 콘텐츠를 동기화하는 수동 프로세스가 가능합니다. 그러나 사이트 수가 증가하거나 여러 언어가 관여하는 경우 프로세스를 자동화하는 것이 더 효율적입니다.

* 웹 사이트의 다양한 언어 버전을 효율적으로 관리합니다.
* 소스 사이트를 기반으로 하나 이상의 사이트를 자동으로 업데이트:

   * 공통 기본 구조를 적용하고 여러 사이트에서 공통 콘텐츠를 사용합니다.
   * 사용 가능한 리소스의 사용을 극대화합니다.
   * 일반적인 모양과 느낌을 유지하십시오.
   * 사이트 간에 차이가 있는 콘텐츠를 관리하는 데 노력을 집중하십시오.

자세한 내용은 [다중 사이트 관리자](/help/sites-administering/msm.md)를 참조하십시오.
