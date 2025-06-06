---
title: AEM 포털 및 포틀릿
description: AEM as a portal을 구성 및 관리하는 방법과 포틀릿에 AEM 콘텐츠를 구성하고 표시하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 448715f1-ccec-4fb8-92d7-b7458cf9e6d4
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '6081'
ht-degree: 0%

---

# AEM 포털 및 포틀릿{#aem-portals-and-portlets}

이 문서에서는 다음 사항에 대해 설명합니다.

* AEM 포털 아키텍처
* AEM as a portal 관리 및 구성
* AEM을 포털로 사용
* 포틀릿(예: 웹 서버)에 AEM 컨텐츠 설치, 구성 및 표시

## AEM 포털 아키텍처 {#aem-portal-architecture}

AEM 포털 아키텍처에는 포털 및 포틀릿에 대한 정의가 포함되어 있습니다.

### 포털이란? {#what-is-a-portal}

포털은 개인화, SSO(Single Sign-On), 다양한 소스의 컨텐츠 통합을 제공하고 정보 시스템의 프레젠테이션 계층을 호스팅하는 웹 애플리케이션입니다.

AEM에서 JSR 286 호환 포틀릿을 실행할 수 있습니다. 포틀릿 구성 요소를 사용하여 페이지에 포틀릿을 포함할 수 있습니다. [AEM Content Portlet 관리](#administeringthecqcontentportlet)를 참조하십시오.

### 포틀릿이란? {#what-is-a-portlet}

포틀릿은 다이내믹 콘텐츠를 생성하는 컨테이너 내에 배포된 웹 구성 요소입니다. 포틀릿 인터페이스는 포틀릿 컨테이너 내에 .war 파일로 패키지되어 배포됩니다. AEM을 포털로 실행하는 경우 포틀릿을 실행하려면 포틀릿의 .war 파일이 필요합니다.

포털에 표시할 AEM 콘텐츠를 구성하려면 [포틀릿에서 AEM 설치, 구성 및 사용](#installingconfiguringandusingcqinaportlet)을 참조하십시오.

### AEM 포털 디렉터 {#aem-portal-director}

>[!CAUTION]
>
>AEM 포털 디렉터는 AEM 6.4 이후 더 이상 사용되지 않으며 이제 AEM 6.5 LTS에서 더 이상 지원되지 않습니다. [사용되지 않거나 제거된 기능](/help/release-notes/release-notes.md#deprecated-and-removed-features)을 참조하세요.

## AEM 컨텐트 포틀릿 관리 {#administering-the-aem-content-portlet}

AEM 컨텐츠 포틀릿을 사용하면 포털에 AEM 컨텐츠를 표시할 수 있습니다. 포틀릿은 `/crx-quickstart/opt/portal`에서 사용할 수 있으며 다양한 방법으로 사용자 지정할 수 있습니다. 예를 들어, 자체 인증 서비스를 배포하여 AEM이 기본 동작을 덮어쓰는 데 필요한 인증 정보를 생성하여 SSO/인증 처리를 사용자 지정할 수 있습니다. 플러그인은 API에 대해 플러그인을 빌드하여 고유한 기능을 추가할 수 있도록 하는 정의된 API를 사용합니다. 플러그인은 실행 중인 포틀릿에 배포할 수 있습니다. 제대로 작동하려면 시작 시 표시할 콘텐츠 경로와 함께 AEM 작성자 및 게시 인스턴스의 구성이 필요합니다.

일부 구성은 포틀릿 기본 설정을 통해 변경할 수 있으며 다른 구성은 OSGi 서비스 구성을 통해 변경할 수 있습니다. **config** 파일 또는 OSGi 웹 콘솔을 사용하여 이러한 구성을 변경합니다.

### 포틀릿 기본 설정 {#portlet-preferences}

포틀릿 웹 응용 프로그램을 배포하기 전에 포털 서버에서 배포 시 또는 **WEB-INF/portlet.xml** 파일을 편집하여 Porlet 기본 설정을 구성할 수 있습니다. portlet.xml 파일은 기본적으로 다음과 같이 나타납니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<portlet-app xmlns="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd /opt/SUNWps/dtd/portlet.xsd"
             version="1.0">
   <portlet>
      <portlet-name>RSSWeatherPortlet</portlet-name>
      <portlet-class>org.jboss.portlet.weather.WeatherPortlet</portlet-class>
      <init-param>
         <name>default_zipcode</name>
         <value>05673</value>
      </init-param>
      <init-param>
         <name>RSS_XSL</name>
         <value>/WEB-INF/Rss.xsl</value>
      </init-param>
      <init-param>
         <name>base_url</name>
         <value>https://xml.weather.yahoo.com/forecastrss?p=</value>
      </init-param>
      <expiration-cache>180</expiration-cache>
      <supports>
         <mime-type>text/html</mime-type>
         <portlet-mode>VIEW</portlet-mode>
         <portlet-mode>EDIT</portlet-mode>
      </supports>
      <portlet-info>
         <title>Weather Portlet</title>
      </portlet-info>
      <portlet-preferences>
         <preference>
            <name>expires</name>
            <value>180</value>
         </preference>
         <preference>
            <name>RssXml</name>
            <value>https://xml.weather.yahoo.com/forecastrss?p=33145</value>
            <read-only>false</read-only>
         </preference>
      </portlet-preferences>
   </portlet>
</portlet-app>
```

포틀릿은 다음과 같은 기본 설정으로 구성할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td>startPath</td>
   <td><p>포틀릿의 시작 경로입니다. 포틀릿은 처음에 표시되는 컨텐츠를 정의합니다.</p> <p><strong>중요</strong>: 포틀릿이 <strong> /</strong>과(와) 다른 컨텍스트 경로에서 실행 중인 AEM 작성자 및 게시 인스턴스에 연결하도록 구성된 경우 이러한 AEM 인스턴스의 Html 라이브러리 관리자 구성(예: Felix Webconsole을 통해)에서 강제 <strong>CQUrlInfo</strong>을(를) 활성화해야 합니다. 그렇지 않으면 편집이 작동하지 않고 환경 설정 대화 상자가 표시되지 않습니다.</p> </td>
  </tr>
  <tr>
   <td>htmlSelector</td>
   <td>각 URL에 추가되는 선택기입니다. 기본적으로 <strong>portlet</strong>이므로 html 페이지에 대한 모든 요청은 <strong>.portlet.html로 끝나는 URL을 사용합니다.</strong> 포틀릿 렌더링을 위해 AEM 내의 사용자 지정 스크립트를 사용할 수 있습니다.</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>기본적으로 AEM의 HTML 페이지에 포함된 css 파일은 포틀릿에 포함됩니다. 이 옵션을 비활성화하면 기본 css 파일이 제외됩니다.</p> <p>이 옵션을 활성화하면 포털의 동작에 따라 CSS 파일이 html 페이지의 헤드에 추가되거나 html 페이지에 포함됩니다.</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>기본적으로 관리 기능을 위해 컨텐트 포틀릿 내에 도구 모음이 렌더링됩니다. 이 옵션을 비활성화하면 도구 모음이 렌더링되지 않습니다.</td>
  </tr>
  <tr>
   <td>urlParameterNames</td>
   <td><p>포틀릿에 대해 표시할 새 컨텐츠 URL을 포함할 수 있는 대체 URL 매개 변수 이름 목록입니다. 목록은 위에서 아래로 처리되며 값이 포함된 첫 번째 매개 변수가 사용됩니다. URL이 없으면 기본 URL 매개 변수가 사용됩니다. 제공된 URL은 더 이상 수정하지 않고 그대로 사용됩니다.</p> <p>이 설정은 배포된 포틀릿마다 적용됩니다. 또한 "Day Portal Director 포틀릿 Bridge"에 대한 OSGi 구성에서 일부 URL 매개 변수를 전체적으로 구성합니다.</p> </td>
  </tr>
  <tr>
   <td>preferenceDialog</td>
   <td>AEM의 환경 설정 대화 상자 경로 - 비워 두면 내장된 환경 설정 대화 상자가 사용됩니다. 기본값은 /libs/portal/content/prefs.html입니다.</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>기본적으로 포틀릿은 첫 번째 호출 시 전체 포털 페이지의 Javascript 리디렉션을 수행합니다. 최신 포털 서버의 드래그 앤 드롭 시나리오를 지원하기 위해서입니다. 프로덕션에서 이 리디렉션은 거의 필요하지 않으므로 이 환경 설정을 <em>false</em>(으)로 설정하여 끌 수 있습니다.</td>
  </tr>
 </tbody>
</table>

#### OSGi 웹 콘솔 {#osgi-web-console}

포털 서버가 localhost, port 8080 호스트에서 실행되고 AEM 포틀릿 웹 응용 프로그램이 웹 응용 프로그램 컨텍스트 *cqportlet*&#x200B;에 마운트되어 있다고 가정할 때 웹 콘솔의 URL은 `https://localhost:8080/cqportlet/cqbridge/system/console`입니다. 기본 사용자 및 암호는 **admin**&#x200B;입니다.

**구성** 탭을 열고 **포털 디렉터리 CQ 서버 구성**&#x200B;을 선택합니다. 여기에서는 작성자 및 게시 인스턴스에 대한 기본 URL을 지정합니다. 이 절차는 [포틀릿 구성](#configuring-the-portlet)에 설명되어 있습니다.

>[!NOTE]
>
>OSGi 웹 콘솔은 개발(또는 테스트) 중에 구성을 변경하기 위한 용도로만 사용됩니다. 프로덕션 시스템에 대한 콘솔에 대한 요청을 차단해야 합니다.

### 구성 제공 {#providing-configurations}

AEM Content 포틀릿에는 자동 배포 및 구성 프로비저닝을 지원하기 위해 포틀릿 애플리케이션에 제공된 클래스 경로에서 구성을 읽도록 하는 기본 구성 지원이 있습니다.

시작 시 시스템 속성 **com.day.cq.portet.config**&#x200B;을(를) 읽어서 현재 환경을 감지합니다. 일반적으로 이 속성의 값은 **dev**, **prod**, **test** 등과 같습니다. 환경이 설정되지 않은 경우 구성을 읽지 않습니다.

환경이 설정되면 구성 파일이 ***com/day/cq/portlet/{env}.config**&#x200B;의 클래스 경로에서 검색됩니다. 여기서 **env**&#x200B;은(는) 환경의 실제 값으로 대체됩니다. 이 파일은 이 환경에 대한 모든 구성 파일을 나열해야 합니다. 이러한 파일은 구성 파일의 위치를 기준으로 검색됩니다. 예를 들어 파일에 줄 `my.service.xml,`이(가) 포함된 경우 이 파일은 `com/day/cq/portlet/my.service.config.`의 클래스 경로에서 읽혀집니다. 파일 이름은 서비스의 지속성 ID 다음에 **.config**&#x200B;가 옵니다. 이전 예제에서는 지속성 ID가 **my.service**&#x200B;입니다. 구성 파일의 형식은 Apache Sling OSGi 설치 관리자에서 사용하는 형식입니다.

즉, 각 환경에 대해 해당 구성 파일을 추가해야 합니다. 모든 환경에 적용해야 하는 구성은 이러한 모든 파일에 입력되어야 합니다. 단일 환경에 대한 구성일 경우 해당 파일에 입력됩니다. 이 메커니즘은 어느 환경에서 어떤 구성을 읽는지에 대한 완전한 제어를 보장합니다.

다른 시스템 속성을 사용하여 환경을 감지할 수 있습니다. **com.day.cq.portet.config** 대신 사용할 시스템 속성의 이름을 포함하는 시스템 속성 **com.day.cq.portet.configproperty**&#x200B;을(를) 지정하십시오.

#### 캐싱 및 캐싱 무효화 {#caching-and-caching-invalidation}

포틀릿은 기본 구성에서 AEM WCM으로부터 받은 응답을 사용자별 캐시에 저장합니다. 게시 인스턴스의 콘텐츠가 변경되면 캐시를 무효화해야 합니다. 이를 위해 AEM WCM에서는 작성자 인스턴스에 복제 에이전트를 구성해야 합니다. 캐시를 수동으로 플러시할 수도 있습니다. 이 섹션에서는 이러한 두 절차에 대해 설명합니다.

포틀릿은 자체 캐시로 구성할 수 있으므로 AEM에 액세스하지 않고도 포틀릿의 컨텐츠를 표시할 수 있습니다. 포털은 /libs/portal/director에서 콘텐츠로 사용할 수 있습니다. 콘텐츠에 액세스하려면 AEM 인스턴스를 시작하고 해당 위치에서 CRXDE Lite 또는 Webdav를 사용하여 파일을 다운로드합니다.

이 번들을 런타임에 배포하거나 배포 전에 `WEB-INF/lib/resources/bundles`에서 포틀릿 웹 응용 프로그램에 추가할 수 있습니다.

캐시가 배포되면 포틀릿은 게시 인스턴스의 내용을 캐시에 저장합니다. 포틀릿 캐시는 AEM의 Dispatcher 플러시로 무효화할 수 있습니다. 포틀릿에서 자체 캐시를 사용하도록 구성하려면 다음을 수행합니다.

1. 포털 서버를 타겟팅하는 작성자의 복제 에이전트를 구성합니다.
1. 포털 서버가 호스트 **localhost**, **port 8080**&#x200B;에서 실행되고 AEM 포틀릿 웹 응용 프로그램이 컨텍스트 **cqportlet**&#x200B;에 마운트되어 있다고 가정할 때 캐시를 플러시할 URL은 `https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)`입니다. 메서드로 GET을 사용합니다.
   **참고:** 요청 매개 변수를 사용하는 대신 **경로**(이)라는 http 헤더를 보낼 수 있습니다.

#### 복제 에이전트를 통해 캐시 플러시 {#flushing-the-cache-via-replication-agent}

일반 Dispatcher 무효화와 마찬가지로 복제 에이전트는 포털의 AEM 포틀릿 캐시를 타겟팅하도록 구성할 수 있습니다. 복제 에이전트를 구성하면 모든 일반 페이지 활성화가 포털 캐시를 플러시합니다.

AEM 포틀릿을 실행하는 여러 포털 노드를 운영하는 경우 이 절차에 설명된 대로 각 노드에 대해 에이전트를 생성해야 합니다.

포털에 대한 복제 에이전트를 구성하려면 다음을 수행합니다.

1. 작성자 인스턴스에 로그인합니다.
1. 웹 사이트 탭에서 *도구* 탭을 클릭합니다.
1. 복제 에이전트 **새로 만들기...** 메뉴에서 **새 페이지..**&#x200B;을(를) 클릭합니다.

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. *템플릿*&#x200B;에서 *복제 에이전트*&#x200B;을(를) 선택하고 에이전트 이름을 입력하십시오. *만들기*&#x200B;를 클릭합니다.

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. 생성한 복제 에이전트를 두 번 클릭합니다. 아직 구성되지 않아 잘못된 것으로 표시됩니다.

   ![screen_shot_2012-02-15at41001pm](assets/screen_shot_2012-02-15at41001pm.png)

1. **편집**&#x200B;을 클릭합니다.
1. **설정** 탭에서 **사용** 확인란을 선택하고 직렬화 유형으로 **Dispatcher 플러시**&#x200B;를 선택한 다음 다시 시도 시간 초과(예: 60000)를 입력하십시오.

   ![screen_shot_2012-02-15at42101pm](assets/screen_shot_2012-02-15at42101pm.png)

1. **전송** 탭을 클릭합니다.
1. **URI** 필드에 포틀릿의 플러시 URI(URL)를 입력합니다. URI의 형식은 다음과 같습니다.

   ```xml
   https://<wps-host>:<port>/<wps-context>/<cq5-portlet-context>/cqbridge/cqpcache
   ```

   ![screen_shot_2012-02-15at42322pm](assets/screen_shot_2012-02-15at42322pm.png)

1. **확장** 탭을 클릭합니다.

   ![screen_shot_2012-02-15at42515pm](assets/screen_shot_2012-02-15at42515pm.png)

1. **HTTP 메서드** 필드에 **GET**&#x200B;을(를) 입력합니다.
1. **HTTP 헤더** 필드에서 **+**&#x200B;을(를) 클릭하여 새 항목을 추가하고 **경로: {path}**&#x200B;을(를) 입력하십시오.
1. 필요한 경우 **프록시** 탭을 클릭하고 에이전트에 프록시 정보를 입력하십시오.
1. 변경 내용을 저장하려면 **확인**&#x200B;을 클릭하세요.
1. 연결을 테스트하려면 **연결 테스트** 링크를 클릭하십시오. 복제 테스트가 성공했는지 여부를 나타내는 로그 메시지가 나타납니다. 예:

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### 포틀릿 캐시 수동 플러시 {#manually-flushing-the-portlet-cache}

복제 에이전트에 대해 구성된 동일한 URL에 액세스하여 포틀릿 캐시를 수동으로 플러시할 수 있습니다. URL 형식은 [캐시 플러시](#flushing-the-cache-via-replication-agent)를 참조하십시오. 또한 플러시할 항목을 나타내려면 URL 매개 변수 Path=&lt;path>로 URL을 확장해야 합니다.

예:

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*`이(가) 전체 캐시를 플러시합니다. `https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz`이(가) 캐시에서 `/content/mypage/xyz`을(를) 플러시합니다.

### 포털 보안 {#portal-security}

포털은 운전 인증 메커니즘입니다. 기술 사용자, 포털 사용자, 그룹 등을 사용하여 AEM에 로그인할 수 있습니다. 포틀릿에는 포털에 있는 사용자의 암호에 대한 액세스 권한이 없으므로 포틀릿이 사용자에 성공적으로 로그인할 수 있는 모든 자격 증명을 모를 경우 SSO 솔루션을 사용해야 합니다. 이 경우 AEM 포틀릿은 필요한 모든 정보를 AEM에 전달하며, 이렇게 하면 이 정보가 기본 AEM 저장소에 전달됩니다. 이 동작은 플러그할 수 있으며 사용자 정의할 수 있습니다.

### 게시 시 인증 {#authentication-on-publish}

이 섹션에서는 포틀릿이 기본 AEM WCM 인스턴스와 통신하는 데 사용할 수 있는 인증 모드에 대해 설명합니다.

기본적으로 AEM의 게시 인스턴스에는 사용자 정보가 전송되지 않습니다. 콘텐츠는 항상 익명 사용자로 표시됩니다. AEM에서 사용자 특정 정보를 전달해야 하거나 게시를 위한 사용자 인증이 필요한 경우 이 기능을 켜야 합니다.

#### 포틀릿의 인증 구성 액세스 {#accessing-the-portlet-s-authentication-configuration}

포틀릿이 AEM WCM 인스턴스에서 사용하는 인증 구성 옵션은 웹 콘솔(OSGi 구성)에서 사용할 수 있습니다.

>[!NOTE]
>
>AEM을 사용하여 작업할 때 OSGi 서비스(콘솔 또는 저장소 노드)에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다.
>
>자세한 내용은 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 참조하십시오.

포틀릿의 인증 구성에 액세스하려면 다음을 수행합니다.

1. 다음 URL에서 웹 콘솔에 액세스합니다.

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   예를 들어 기본 구성에서:

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. 웹 콘솔에 로그인합니다. 기본 자격 증명은 `admin/admin`입니다.
1. 콘솔에서 **구성**&#x200B;을 선택합니다.
1. **구성** 메뉴에서 구성할 특정 서비스를 선택합니다. 서비스는 OSGi 프레임워크의 포틀릿에서 제공됩니다.

   | 서비스 이름 | 설명 |
   |---|---|
   | Day Portal 디렉터 인증자 | AEM WCM 인스턴스에 사용할 인증 모드를 구성합니다. 선택한 모드에 따라 기술 사용자 또는 SSO 쿠키의 이름을 지정할 수 있습니다. 또한 AEM WCM 게시 인스턴스에 대한 인증을 활성화할 수 있습니다. |
   | Day Portal 디렉터 파일 캐시 | 포틀릿이 AEM WCM 인스턴스에서 받는 응답에 대한 매개변수를 구성합니다. |
   | Day Portal Director HTTP 클라이언트 서비스 | HTTP를 통해 기본 AEM WCM 인스턴스에 포틀릿이 연결되는 방식을 구성합니다. 예를 들어 프록시 서버를 지정할 수 있습니다. |
   | 일 포털 디렉터 로케일 핸들러 | 포틀릿이 지원하는 로케일을 구성합니다. AEM WCM 인스턴스에 대한 요청은 사용자 로케일을 기반으로 합니다. 예를 들어 사용자 언어 *독일어 *는 `/content/geometrixx/de/`을(를) 요청합니다.... |
   | Day Portal 책임자 권한 관리자 | 포틀릿에서 현재 로그인한 사용자를 기준으로 웹 사이트 탭을 테스트할지 여부를 구성합니다. |
   | 일 포털 디렉터 도구 모음 렌더러 | 포틀릿의 도구 모음 렌더링을 사용자 지정합니다. |

1. 또한 웹 콘솔과 로깅 서비스를 구성할 수 있습니다. 예를 들어 Apache Felix OSGi 관리 콘솔 링크를 클릭하여 웹 콘솔에 대한 관리자 자격 증명을 변경할 수 있습니다.

#### 기술 사용자 모드 {#technical-user-mode}

기본 모드에서 AEM WCM 작성자 인스턴스에 대해 포틀릿에서 발급한 모든 요청은 현재 포털 사용자에 관계없이 동일한 기술 사용자를 사용하여 인증됩니다. 기술 사용자 모드는 기본적으로 활성화되어 있습니다. OSGi 관리 콘솔의 각 구성 화면에서 이 모드를 활성화/비활성화합니다.

**게시할 때 인증**&#x200B;이 활성화된 경우 지정된 기술 사용자가 AEM WCM 작성자 인스턴스와 게시 인스턴스에 있어야 합니다. 작성 작업에 충분한 액세스 권한을 사용자에게 부여해야 합니다.

#### SSO {#sso}

포틀릿은 AEM에서 즉시 사용할 수 있는 SSO를 지원합니다. 인증자 서비스는 SSO를 사용하여 **기본** 형식의 현재 포털 사용자를 `cqpsso`(이)라는 쿠키로 AEM에 전송하도록 구성할 수 있습니다. AEM은 경로 /에 대한 SSO 인증 핸들러를 사용하도록 구성해야 합니다. 여기서도 쿠키 이름을 구성해야 합니다.

AEM 리포지토리용 `crx-quickstart/repository/repository.xml`을(를) 그에 따라 구성해야 합니다.

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### SSO 인증 모드 {#sso-authentication-mode}

포틀릿은 SSO(Single Sign-On) 체계를 사용하여 AEM WCM을 인증할 수 있습니다. 이 모드에서는 현재 포털에 로그인한 사용자가 SSO 쿠키 형태로 AEM WCM으로 전달됩니다. SSO 모드를 사용하는 경우 AEM 포틀릿에 대한 액세스 권한이 있는 모든 포털 사용자를 기본 AEM WCM 인스턴스에 알려주어야 합니다. 가장 일반적으로 AEM WCM이 LDAP에 연결되거나 사용자를 미리 수동으로 만들어 놓는 형태로 이루어져야 합니다. 또한 포틀릿에서 SSO를 활성화하기 전에 기본 AEM WCM 작성자 인스턴스(**게시할 때 인증**&#x200B;이 활성화된 경우 게시 인스턴스)를 SSO 기반 요청을 수락하도록 구성해야 합니다.

SSO 인증 모드를 사용하도록 포틀릿을 구성하려면 다음 단계를 완료하십시오(다음 섹션에 자세히 설명됨).

* AEM WCM의 저장소가 신뢰할 수 있는 자격 증명을 수락하도록 설정합니다.
* AEM WCM에서 SSO 인증을 사용하도록 설정합니다.
* AEM 포틀릿에서 SSO 인증을 활성화합니다.

#### AEM WCM의 저장소에서 신뢰할 수 있는 자격 증명을 수락하도록 활성화 {#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

AEM WCM에 대해 SSO를 활성화하려면 먼저 AEM WCM에서 제공한 신뢰할 수 있는 자격 증명을 수락하도록 기본 저장소를 구성해야 합니다. 이를 위해 AEM의 repository.xml을 구성합니다.

1. AEM WCM이 설치된 파일 시스템에서 다음 파일을 엽니다.

   `//crx-quickstart/repository/repository.xml`

1. XML 파일에서 **LoginModule**&#x200B;의 항목을 찾아 trust_credentials_attribute를 해당 구성에 추가합니다.

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
     <param name="anonymous_principal" value="anonymous"/>
   </LoginModule>
   ```

1. 변경 사항을 적용하려면 AEM WCM을 다시 시작하십시오.

#### AEM WCM에서 SSO 인증 활성화 {#enabling-sso-authentication-in-the-aem-wcm}

AEM WCM에서 SSO를 활성화하려면 AEM WCM의 Apache Felix 웹 관리 콘솔(OSGi)에서 관련 구성 항목에 액세스합니다.

1. https://&lt;AEM-host>:&lt;port>/system/console의 URI를 통해 콘솔에 액세스합니다.
1. 구성 메뉴에서 SSO 인증 핸들러를 선택합니다. 이 예에서 SSO 처리기는 AEM 포틀릿에서 제공한 쿠키를 기반으로 모든 경로에 대한 SSO 요청을 수락합니다. 구성이 다를 수 있습니다.

   | 경로 | / | 모든 요청에 대해 SSO 처리기 활성화 |
   |---|---|---|
   | 쿠키 이름 | cqpsso | 포틀릿의 OSGi 콘솔에서 구성한 포틀릿에서 제공하는 쿠키의 이름입니다. |

1. SSO를 활성화하려면 **저장**&#x200B;을 클릭하십시오. 이제 SSO가 기본 인증 체계입니다.

AEM WCM이 받는 모든 요청에 대해 먼저 SSO 기반 인증이 시도됩니다. 실패 시 일반적인 기본 인증 체계로의 폴백이 수행됩니다. 따라서 SSO가 없는 AEM WCM에 대한 일반 연결이 가능합니다.

#### AEM 포틀릿에서 SSO 인증 활성화 {#enabling-sso-authentication-in-a-aem-portlet}

기본 AEM WCM 인스턴스가 SSO 요청을 수락하려면 포틀릿의 인증 모드를 **기술**&#x200B;에서 **SSO**(으)로 전환해야 합니다.

AEM 포틀릿에서 SSO 인증을 활성화하려면 다음을 수행합니다.

1. URI( https://&lt;aem-host>:&lt;port>/system/console)를 통해 콘솔에 액세스합니다.
1. 구성 메뉴의 사용 가능한 구성 목록에서 Day Portal Director Authenticator 를 선택합니다.
1. 모드에서 SSO를 선택합니다. 다른 매개 변수는 기본값으로 둡니다.

   ![chlimage_1-135](assets/chlimage_1-135.png)

1. 저장 을 클릭하여 포틀릿에 대한 SSO를 활성화합니다.

   테스트를 위해 AEM WCM에서 관리자 권한을 가진 동일한 사용자를 만든 후 포털의 관리 사용자로 포틀릿에 액세스합니다.

이 절차를 수행하면 요청은 SSO를 사용하여 인증됩니다. HTTP 통신의 일반적인 코드 조각은 다음 SSO 및 포틀릿 관련 헤더의 존재를 나타냅니다.

```xml
C-12-#001898 -> [GET /mynet/en/_jcr_content/par/textimage/image.img.png HTTP/1.1 ]
C-12-#001963 -> [cq5:locale: en ]
C-12-#001979 -> [cq5:used-locale: en ]
C-12-#002000 -> [cq5:locales: en,en_US ]
C-12-#002023 -> [cqp:user: wpadmin ]
C-12-#002042 -> [cqp:portal: IBM WebSphere Portal/6.1 ]
C-12-#002080 -> [cqp:windowid: 7_CGAH47L000CE302V2KFNOG0084 ]
C-12-#002124 -> [cqp:windowstate: normal ]
C-12-#002149 -> [cqp:portletmode: view ]
C-12-#002172 -> [User-Agent: Jakarta Commons-HttpClient/3.1 ]
C-12-#002216 -> [Host: 10.0.0.68:4502 ]
C-12-#002238 -> [Cookie: $Version=0; cqpsso=Basic+d3BhZG1pbg%3D%3D ]
C-12-#002289 -> [ ]
```

### PIN 인증 사용 {#enabling-pin-authentication}

AEM 컨텐츠 포틀릿의 기본 인라인 편집 기능을 사용하지 않지만 AEM 작성자 인스턴스에서 직접 포털 외부의 포틀릿에 작성 및 관리 부분을 사용하려는 경우 PIN 인증을 활성화해야 합니다. 또한 관리 버튼의 구성을 변경해야 합니다.

웹 사이트 관리 페이지를 열거나 포틀릿에서 페이지를 편집하려면 AEM 컨텐츠 포틀릿에서 새 고정 인증을 사용합니다. 기본적으로 핀 인증이 비활성화되어 있으므로 AEM에서 다음 구성을 변경해야 합니다.

1. repository.xml 파일에 신뢰할 수 있는 정보를 추가하여 AEM에서 신뢰할 수 있는 인증을 활성화합니다.

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. OSGi 구성 콘솔의 기본 위치 https://localhost:4502/system/console/configMgr에서 드롭다운 메뉴에서 **CQ PIN 인증 처리기**&#x200B;를 선택합니다.
1. 단일 값 **/**&#x200B;을(를) 포함하도록 **URL 루트 경로** 매개 변수를 편집하십시오.

### 권한 {#privileges}

포틀릿의 일부 기능은 권한으로 보호됩니다. 현재 사용자가 이 기능에 액세스하려면 이 권한이 있어야 합니다. 다음과 같은 권한이 미리 정의되어 있습니다.

* &quot;toolbar&quot; : 포틀릿에서 도구 모음을 보거나 사용할 수 있는 일반 권한입니다.
* &quot;prefs&quot; : 사용자에게 이 권한이 있는 경우 포틀릿의 기본 설정을 보거나 변경할 수 있습니다.
* &quot;cq-author:edit&quot; : 이 권한을 사용하여 사용자는 컨텐츠의 편집 보기를 호출할 수 있습니다.
* &quot;cq-author:preview&quot; : 이 권한을 사용하면 사용자는 미리보기를 볼 수 있습니다.
* &quot;cq-author:siteadmin&quot; : 이 권한을 사용하면 사용자가 AEM 내에서 siteadmin을 열 수 있습니다.

권한을 관리하는 가장 좋은 방법은 포털 역할을 사용하고 이러한 권한에 역할을 할당하는 것입니다. 이 작업은 OSGi 구성을 통해 수행할 수 있습니다. &quot;Day Portal 책임자 권한 관리자&quot;는 각 권한에 대한 일련의 역할로 구성할 수 있습니다. 사용자에게 롤 중 하나가 있는 경우 해당 권한이 있습니다.

또한 포틀릿 인스턴스 기반별로 액세스 권한을 기반으로 이 역할을 정의할 수 있습니다. 포틀릿의 기본 설정 대화 상자에는 위의 각 권한에 대한 입력 필드가 포함되어 있습니다. 각 권한에 대해 쉼표로 구분된 포틀릿 롤 목록을 구성할 수 있습니다. 값이 구성된 경우 &quot;Day Portal 디렉터 권한 관리자&quot; 서비스의 전역 구성이 재정의되며 역할이 병합되지 않으므로 이 전역 설정에서 동일한 역할을 추가해야 할 수 있습니다. 값을 지정하지 않으면 전역 구성이 사용됩니다.

### AEM 포틀릿 애플리케이션 사용자 정의 {#customizing-the-aem-portlet-application}

제공된 AEM 포틀릿 애플리케이션은 AEM과 마찬가지로 웹 애플리케이션 내에서 OSGi 컨테이너를 시작합니다. 이 아키텍처를 사용하면 OSGi의 모든 이점을 사용할 수 있습니다.

* 간편한 업데이트 및 확장
* 포털 서버의 상호 작용 없이 포틀릿의 최신 업데이트 제공
* 포틀릿의 간편한 사용자 정의

### 도구 모음 단추 {#toolbar-buttons}

도구 모음 및 해당 단추를 구성할 수 있으며 사용자 지정할 수 있습니다. 도구 모음에 사용자 지정 단추를 추가하거나 표시되는 단추를 정의할 수 있습니다. 각 버튼은 OSGi 구성을 통해 구성할 수 있는 OSGi 서비스입니다.

OSGi 웹 콘솔에는 **구성** 탭의 모든 단추 구성이 나열됩니다. 각 단추에 대해 이 단추가 표시되는 모드를 정의할 수 있습니다. 예를 들어 모든 모드를 제거하여 단추를 비활성화할 수 있습니다.

기본적으로 AEM 컨텐츠 포틀릿은 인라인 편집 기능을 사용합니다. 그러나 편집할 AEM 작성자 인스턴스로 전환하려면 **SiteAdmin 단추** 및 **ContentFinder 단추**&#x200B;을(를) 활성화하되 **편집 단추**&#x200B;는 비활성화합니다. 이 경우 AEM에서 PIN 인증을 올바르게 구성해야 합니다.

미리 정의된 위치에 사용자 정의 CSS/HTML이 포함된 포틀릿의 Felix 웹 콘솔을 통해 번들을 설치하여 포틀릿의 도구 모음 레이아웃을 사용자 정의할 수 있습니다.

#### 번들 구조 {#bundle-structure}

다음은 번들 구조의 예입니다.

```xml
$ jar tvf target/toolbarlayout-0.0.1-SNAPSHOT.jar | awk '{print $8}'
META-INF/
META-INF/MANIFEST.MF
/com/day/cq/portlet/toolbar/layout/
/com/day/cq/portlet/toolbar/layout/author.gif
/com/day/cq/portlet/toolbar/layout/back.gif
/com/day/cq/portlet/toolbar/layout/button.html
/com/day/cq/portlet/toolbar/layout/edit.gif
/com/day/cq/portlet/toolbar/layout/manage.html
/com/day/cq/portlet/toolbar/layout/publish.html
/com/day/cq/portlet/toolbar/layout/refresh.gif
/com/day/cq/portlet/toolbar/layout/siteadmin.gif
/com/day/cq/portlet/toolbar/layout/toolbar.css
```

META-INF 폴더에는 OSGi가 번들로 식별하는 데 필요한 MANIFEST.MF 파일이 포함되어 있습니다. 다음과 같이 표시됩니다.

```xml
Manifest-Version: 1.0
Built-By: djaeggi
Created-By: Apache Maven Bundle Plugin
Import-Package: com.day.cq.portlet.toolbar.layout
Bnd-LastModified: 1234178347159
Export-Package: com.day.cq.portlet.toolbar.layout
Bundle-Version: 0.0.1.SNAPSHOT
Bundle-Name: Company CQ5 Portal Director Portlet Toolbar Layout
Bundle-Description: This bundle provides a custom layout for the CQ5 P
 ortal Director Portlet Toolbar.
Build-Jdk: 1.5.0_16
Bundle-ManifestVersion: 2
Bundle-SymbolicName: com.day.cq.portlet.company.toolbarlayout
Tool: Bnd-0.0.255
```

HTML/CSS/이미지가 /com/day/cq/portlet/toolbar/layout 폴더에 있다는 사실은 포틀릿에서 지정한 것이므로 변경할 수 없습니다. 같은 행에서 MANIFEST.MF의 Import-Package 및 Export-Package 헤더도 /com/day/cq/portlet/toolbar/layout으로 호출해야 합니다. Bundle-SymbolicName은 고유하고 정규화된 패키지 이름이어야 합니다.

Maven과 같은 도구를 사용하거나 이 섹션에 표시된 대로 관련 헤더가 설정된 jar 파일을 수동으로 생성할 수 있습니다.

#### 포틀릿 도구 모음 보기 {#portlet-toolbar-views}

포틀릿의 도구 모음에는 기본적으로 두 개의 보기 상태가 있습니다. 각 보기 및 관련 버튼을 각 HTML 파일로 사용자 정의할 수 있습니다.

#### 게시 보기 {#publish-view}

게시 보기에는 도구 모음을 관리 보기로 전환하는 버튼이 한 개만 있습니다. 게시 보기는 [이전 번들](/help/sites-deploying/configuring-osgi.md#bundles)의 publish.html 파일로 표시됩니다. HTML에서는 렌더링할 때 포틀릿으로 대체되는 다음 자리 표시자를 해당 콘텐츠로 사용할 수 있습니다.

#### 보기 자리 표시자 게시 {#publish-view-placeholders}

| 자리 표시자 문자열 | 설명 |
|---|---|
| {buttonManage} | 자리 표시자는 포틀릿 상태를 관리 상태로 전환하는 **관리** 단추로 바뀝니다. |

#### 보기 관리 {#manage-view}

관리 보기에는 [편집], [웹 사이트] 탭, [새로 고침] 및 [뒤로]의 네 가지 단추가 있습니다. 관리 보기는 [이전 번들](/help/sites-deploying/configuring-osgi.md#bundles)의 manage.html 파일로 표시됩니다. HTML에서는 렌더링할 때 포틀릿으로 대체되는 다음 자리 표시자를 해당 콘텐츠로 사용할 수 있습니다.

#### 보기 자리 표시자 관리 {#manage-view-placeholders}

| 자리 표시자 문자열 | 설명 |
|---|---|
| {buttonEdit} | 자리 표시자가 **편집** 단추로 대체되며, 이 단추는 AEM의 편집 모드에서 현재 페이지가 있는 새 창을 엽니다. |
| {buttonWebsites 탭} | AEM WCM의 웹 사이트 탭을 여는 단추로 대체된 자리 표시자. |
| {buttonRefresh} | 현재 보기를 새로 고칩니다. |
| {buttonBack} | 포틀릿을 게시 보기로 다시 전환합니다. |

#### 버튼 {#buttons}

버튼은 표시되는 보기에서 button.html에 정의된 동일한 공통 HTML을 사용합니다.

HTML에서는 렌더링할 때 포틀릿으로 대체되는 다음 자리 표시자를 해당 콘텐츠로 사용할 수 있습니다.

#### 보기 관리 및 게시 단추 {#manage-and-publish-view-buttons}

| 자리 표시자 문자열 | 설명 |
|---|---|
| {name} | 버튼의 이름(예: **작성자, 뒤로, 새로 고침** 등). |
| {id} | 단추의 CSS ID입니다. |
| {url} | 단추 대상의 URL. |
| {text} | 단추의 레이블입니다. |
| {onclick} | JavaScript **onclick** 함수({url} 포함). |

button.html 파일의 예:

```xml
<div class="cqp_button">

 <a href="#" onclick="{onclick}">

 <img src="/wps/PA_CQ5_Portlet/cqbridge/static/{id}.gif" alt="{text}"
title="{text}"/>

 </a>
</div>
```

#### 사용자 지정 레이아웃 설치 {#installing-a-custom-layout}

사용자 지정 레이아웃을 설치하려면 포틀릿의 OSGI 웹 콘솔&#x200B;**번들**&#x200B;섹션에 액세스하고 번들을 업로드합니다.

#### 패키지 {#packages}

설치를 위해 패키지를 업로드하거나 만들어야 하는 경우 자세한 지침은 AEM 설명서의 패키지 관리자 를 참조하십시오.

### 링크 처리 {#link-handling}

모든 링크는 포털 컨텍스트 내에서 작동하도록 다시 작성됩니다. 기본적으로 렌더링 매개 변수가 있는 링크가 사용됩니다. 포털 디렉터 HTML 재작성기는 대신 작업 링크를 사용하도록 구성할 수 있습니다.

또한 표시되는 콘텐츠 경로에 대해 쿼리할 추가 요청 매개 변수를 정의할 수 있습니다. 이 기능은 외부에서 특정 컨텐츠로 연결되는 링크가 있는 경우 등에 유용합니다.

또한 포털 디렉터 HTML Rewriter는 링크 재작성을 위해 제외된 정규 표현식 목록으로 구성할 수 있습니다. 예를 들어 외부 시스템에 대한 상대 링크가 있는 경우 이 제외 목록에 추가해야 합니다.

### 현지화 {#localization}

AEM 컨텐츠 포틀릿에는 AEM 컨텐츠가 올바른 언어로 되어 있도록 현지화 기능이 내장되어 있습니다.

이 작업은 다음 두 단계로 수행됩니다.

1. 포털 디렉터리 로케일 감지기는 포털에서 로케일 설정을 가져와서 포털 사용자의 로케일을 검색합니다. 이 서비스는 AEM에서 사용 가능한 언어 목록으로 구성해야 합니다.
1. 포털 디렉터 로케일 핸들러가 현재 요청의 현지화를 처리합니다. 요청된 콘텐츠의 경로(예: `/content/geometrixx/en/company.html`)를 사용하며, 구성에 따라 **en**&#x200B;을(를) 사용자의 실제 로케일로 다시 씁니다.

포털 디렉터 로케일 핸들러는 로케일 정보를 확인하는 경로로 구성할 수 있습니다. 일반적으로 여기에는 `/content`의 모든 항목과 경로에서 로케일 정보의 위치가 포함됩니다. 기본적으로 로케일 핸들러는 AEM 내의 다국어 사이트를 구조화하는 권장 사항을 따릅니다.

사이트에 경로 내의 로케일 정보를 처리하는 엄격한 규칙이 없는 경우 로케일 핸들러를 자체 구현으로 바꿀 수 있습니다.

### 옵션 OSGi 서비스 {#optional-osgi-services}

포틀릿의 다양한 부분을 사용자 정의하기 위해 선택적 OSGi 서비스를 구현할 수 있습니다. 각 서비스는 Java 인터페이스에 해당합니다. 이 인터페이스는 번들을 통해 포틀릿에 구현하고 배포할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>포틀릿에 컨텐츠가 표시될 때마다 요청 추적기에 알림이 표시됩니다. 포틀릿의 호출을 추적할 수 있습니다.</td>
  </tr>
  <tr>
   <td>InvoctionContextListener</td>
   <td>포틀릿에 대한 각 요청의 시작과 끝에서 호출되는 리스너입니다. 현재 요청에 대한 정보를 변경하거나 추가하는 데 수신기를 사용할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>ErrorHandler</td>
   <td>렌더링 단계 중 오류에 대한 사용자 지정 오류 처리기입니다.</td>
  </tr>
  <tr>
   <td>HttpProcessor</td>
   <td>이 서비스를 사용하여 AEM에 대한 각 http 호출에 정보를 추가할 수 있습니다.</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>포틀릿에 고유한 작업을 추가합니다. 이 작업은 포틀릿 작업 링크를 통해 호출할 수 있습니다.</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>이 서비스는 포틀릿의 컨텐츠를 장식하는 데 사용할 수 있습니다.</td>
  </tr>
  <tr>
   <td>ResourceProvider</td>
   <td>고유한 리소스 공급자를 추가하여 클라이언트에 포틀릿 리소스 링크를 통해 일부 리소스를 제공합니다.</td>
  </tr>
  <tr>
   <td>텍스트 매퍼</td>
   <td>HTML, CSS 및 JavaScript 파일 처리를 게시할 수 있습니다.</td>
  </tr>
  <tr>
   <td>도구 모음 단추</td>
   <td>도구 모음에 나만의 버튼을 추가합니다.</td>
  </tr>
  <tr>
   <td>UrlMapper</td>
   <td>서비스를 추가하여 사용자 정의 URL 매핑 또는 재작성을 적용합니다.</td>
  </tr>
  <tr>
   <td>UserInfoProvider</td>
   <td>사용자에 대한 자체 정보를 추가합니다. 이 서비스를 사용하여 포털에서 포틀릿으로 정보를 가져올 수 있습니다.</td>
  </tr>
 </tbody>
</table>

#### 기본 서비스 바꾸기 {#replacing-default-services}

다음 서비스는 콘텐츠 포틀릿(해당 Java 인터페이스 포함)에 기본 구현이 있습니다. 사용자 정의하려면 새 서비스 구현이 포함된 번들을 포틀릿 애플리케이션에 배포해야 합니다.

이러한 서비스를 구현할 때는 서비스의 **service.ranking** 속성을 양수 값으로 설정해야 합니다. 기본 구현에서는 등급 **&#x200B; 0**&#x200B;을 사용하고 포틀릿에서는 순위가 가장 높은 서비스를 사용합니다.

| **이름** | **설명** | **기본 동작** |
|---|---|---|
| 인증자 | AEM에 인증 정보 제공 | 작성자와 게시 모두에 구성 가능한 기술 사용자를 사용합니다. 또는 SSO를 사용할 수 있습니다. |
| HTMLRewriter | 링크 및 이미지 재작성 | AEM 링크를 포털 링크에 재작성합니다. UrlMapper 및 TextMapper를 통해 확장할 수 있습니다. |
| HttpClientService | 모든 http 연결을 처리합니다. | 표준 구현 |
| LocaleHandler | 로케일 정보를 처리합니다. | 로케일을 기준으로 콘텐츠에 대한 링크를 재작성합니다. |
| 로케일 탐지기 | 사용자의 로케일을 검색합니다. | 포털에서 제공하는 로케일을 사용합니다. |
| PrivilegeManager | 사용자 권한 확인 | 사용자가 콘텐츠를 편집할 수 있는 경우 작성자 인스턴스에 대한 액세스 권한을 확인합니다. |
| ToolbarRenderer | 도구 모음 렌더링 | 도구 모음 기능 추가 |

### 포틀릿 이벤트 {#portlet-events}

포틀릿 API(JSR-286)는 포틀릿 이벤트를 지정합니다. AEM 컨텐트 포틀릿에는 통합 브리지가 있어 AEM 포틀릿에 대한 포틀릿 이벤트를 OSGi 이벤트로 분산합니다. 이렇게 하면 포틀릿 이벤트를 처리할 수 있습니다.

특정 이벤트를 처리하려면 이 이벤트를 배포 설명자에서 수신 이벤트로 선언하거나 포털 서버를 통해 구성하고 EventHandler 인터페이스를 선언하는 OSGi 서비스를 구현합니다(OSGi EventAdmin 사양 참조).

포틀릿 이벤트가 발생할 때마다 핸들러를 호출하여 특정 OSGi 이벤트가 전송됩니다. 처리기는 모든 컨텍스트 정보를 가져오고 이에 따라 포틀릿의 상태를 업데이트하거나 새 이벤트를 보낼 수 있습니다. 기본적으로 handle 메서드 내에서 포틀릿 이벤트 단계의 모든 기능을 사용할 수 있습니다.

## AEM을 포털로 사용 {#using-aem-as-a-portal}

포틀릿 구성 요소를 사용하여 AEM 페이지에 포틀릿 창을 추가합니다. 응용 프로그램 서버에 설치하는 공유 라이브러리를 사용하면 포틀릿 구성 요소가 배치된 포틀릿 응용 프로그램을 감지할 수 있습니다.

AEM을 포털로 사용하려면 다음 작업을 수행하십시오.

1. 포틀릿 구성 요소 및 공유 라이브러리를 설치합니다.
1. 포틀릿 구성 요소를 Sidekick에 추가합니다.
1. 포털 구성 요소에 표시할 포틀릿이 포함된 웹 애플리케이션을 구성하고 배포합니다.
1. 페이지에 포틀릿 구성 요소를 추가하고 표시할 포틀릿을 선택합니다.

>[!NOTE]
>
>AEM이 웹 애플리케이션으로 배포된 경우에만 포틀릿 구성 요소를 사용할 수 있습니다. ([응용 프로그램 서버에 AEM 설치 참조](/help/sites-deploying/application-server-install.md))

### 포틀릿 구성 요소 설치 {#installing-the-portlet-component}

AEM Quickstart JAR 파일에는 포틀릿 구성 요소 파일이 포함되어 있습니다. 파일(cq-portlet-components.zip)을 가져오려면 빠른 시작을 실행하거나 내용을 추출할 수 있습니다.

1. Quickstart JAR 파일의 내용을 실행하거나 압축을 푼 다음 그에 따라 cq-portlet-components.zip 파일을 찾습니다.

   * 빠른 시작 실행: crx-quickstart/opt/portal
   * 빠른 시작 콘텐츠 추출: 정적/opt/portal

1. 애플리케이션 서버에 배포된 CQ5 작성자 인스턴스의 패키지 관리자를 엽니다. (https://*appserverhost*:*port*/cq5author/crx/packmgr)

1. 패키지 관리자를 사용하여 cq-portlets-components.zip 패키지를 [업로드 및 설치](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system)합니다.

   패키지는 저장소의 /libs/portal/director 폴더에 cq-portlet-director-sharedlibs-x.x.jar를 설치합니다.

1. cq-portlet-director-sharedlibs-x.x.jar를 하드 드라이브에 복사합니다. FileVault 또는 WebDAV 클라이언트 등 모든 수단을 사용하여 파일을 가져옵니다.
1. 배포된 포틀릿 응용 프로그램에서 클래스를 사용할 수 있도록 cq-portlet-director-sharedlibs.x.x.jar 파일을 응용 프로그램 서버의 공유 라이브러리 폴더로 이동합니다.

### Sidekick에 포틀릿 구성 요소 추가 {#adding-the-portlet-component-to-sidekick}

작성자가 사용할 수 있도록 포틀릿 구성 요소를 단락 시스템에 추가합니다.

1. Sidekick에서 눈금자 아이콘을 클릭하여 디자인 모드로 들어갑니다.
1. 첫 번째 단락 위의 `Design of par` 제목 옆에서 **편집**&#x200B;을 클릭합니다.

1. **일반** 구성 요소 범주에서 포틀릿 구성 요소 옆의 확인란을 선택하고 확인을 클릭합니다.

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### 포틀릿 응용 프로그램 구성 및 배포 {#configuring-and-deploying-your-portlet-applications}

포털 구성 요소에서 사용할 수 있도록 포틀릿을 애플리케이션 서버 웹 컨테이너에 배포합니다. 포틀릿 응용 프로그램을 배포하기 전에 AEM 포털 컨테이너 서블릿을 로드하도록 응용 프로그램을 구성해야 합니다. 이 구성을 통해 포틀릿 구성 요소가 포틀릿에 액세스할 수 있습니다.

1. 포틀릿 응용 프로그램 WAR 파일의 내용을 추출합니다.

   **팁:** jar xf *nameofapp*.war 명령은 파일을 추출합니다.

1. 텍스트 편집기에서 web.xml 파일을 엽니다.
1. 웹 앱 요소 내에 다음 서블릿 구성을 추가합니다.

   ```xml
   <servlet>
           <servlet-name>slingportal</servlet-name>
           <servlet-class>org.apache.sling.portal.container.api.ContainerServlet</servlet-class>
           <load-on-startup>1</load-on-startup>
   </servlet>
   <servlet-mapping>
           <servlet-name>slingportal</servlet-name>
           <url-pattern>/SlingPortletInvoker</url-pattern>
   </servlet-mapping>
   ```

1. web.xml 파일을 저장하고 WAR 파일을 다시 패키징합니다.

   **팁:** `jar cvf nameofapp.war *` 명령은 현재 디렉터리의 내용을 nameofapp.war 파일에 추가합니다.

1. 응용 프로그램 서버에 포틀릿 응용 프로그램을 배포합니다. 자세한 내용은 애플리케이션 서버 설명서를 참조하십시오.

### AEM 페이지에 포틀릿 추가 {#adding-portlets-to-your-aem-page}

포털 구성 요소를 사용하여 웹 페이지에 포틀릿 창을 추가합니다. 구성 요소 등록 정보를 사용하여 표시할 포틀릿을 지정합니다.

1. 웹 페이지의 Sidekick에 있는 일반 그룹에서 **포틀릿** 구성 요소를 페이지로 끌어 옵니다.

   >[!NOTE]
   >
   >구성 요소를 페이지로 드래그한 후 페이지를 다시 로드하여 제대로 작동하는지 확인하십시오.

1. 구성 요소를 두 번 클릭하여 포틀릿 등록 정보를 엽니다.
1. **포틀릿 엔터티** 드롭다운 메뉴의 목록에서 포틀릿을 선택합니다.
1. 포틀릿의 제목 표시줄 표시 여부에 따라 **제목 표시줄 숨기기**&#x200B;확인란을 선택하거나 선택 취소합니다.
1. 원하는 경우 **포틀릿 창** 필드에 고유한 포틀릿 창 ID를 입력합니다.

   >[!NOTE]
   >
   >동일한 페이지에서 동일한 포틀릿을 두 번 이상 사용하려면 각 포틀릿에 다른 창 ID를 지정합니다.

1. **확인**&#x200B;을 클릭합니다. 포틀릿은 AEM 페이지에 표시됩니다.

   ![chlimage_1-136](assets/chlimage_1-136.png)

## 포틀릿에서 AEM 설치, 구성 및 사용 {#installing-configuring-and-using-aem-in-a-portlet}

AEM WCM에서 제공하는 콘텐츠에 액세스하려면 포털 서버에 AEM 포털 디렉터 포틀릿을 설치해야 합니다. 이 섹션에 제공된 단계를 사용하여 포틀릿을 설치, 구성 및 포털 페이지에 추가하면 됩니다.

기본적으로 포틀릿은 localhost:4503에 있는 게시 인스턴스와 localhost:4502에 있는 작성자 인스턴스에 연결됩니다. 이러한 값은 포틀릿을 배포하는 동안 변경할 수 있습니다. 포털 디렉터는 /libs/portal/directory 아래에 있는 저장소에서 콘텐츠로 사용할 수 있습니다. 사용하기 전에 애플리케이션 war 파일을 다운로드하십시오.

### war 파일 다운로드 {#downloading-the-war-file}

1. Webdav 또는 CRXDE Lite을 사용하여 /libs/portal/director로 이동합니다.

1. *cq-portlet-webapp.war*&#x200B;을(를) 다운로드합니다.

>[!NOTE]
>
>이러한 절차는 Websphere 포털을 예로 사용하지만 가능한 한 일반적입니다. 절차는 다른 웹 포털에 따라 다릅니다. 모든 웹 포털에 대해 단계가 기본적으로 동일하지만 특정 웹 포털에 대해 단계의 용도를 다시 지정해야 합니다.

#### 포틀릿 설치 {#installing-the-portlet}

포틀릿을 설치하려면 다음을 수행합니다.

1. 관리자 권한으로 포털에 로그인합니다.
1. 웹 포털의 포틀릿 관리 부분으로 이동합니다.
1. 설치를 누르고 다운로드한 AEM 포틀릿 응용 프로그램(cq-portlet-webapp.war)을 찾은 다음 포틀릿에 대한 다른 중요한 정보를 입력합니다.

   다른 필수 포틀릿 정보의 경우 기본값을 그대로 사용하거나 값을 변경할 수 있습니다. 기본값을 사용하는 경우 포틀릿은 https://&lt;wps-host>:&lt;port>/wps/PA_CQ5_Portlet에서 사용할 수 있습니다. 포틀릿에서 제공하는 OSGi 관리 콘솔은 https://&lt;wps-host>:&lt;port>/wps/ PA_CQ5_Portlet/cqbridge/system/console에서 사용할 수 있습니다(기본 사용자 이름/암호는 admin/admin임).

1. 해당 옵션 또는 확인란을 선택하여 포틀릿 응용 프로그램이 자동으로 시작되도록 하고 변경 사항을 저장합니다. 설치가 성공했다는 메시지가 표시됩니다.

#### 포틀릿 구성 {#configuring-the-portlet}

포틀릿을 설치한 후에는 기본 AEM 인스턴스(작성자 및 게시)의 URL을 알 수 있도록 포틀릿을 구성해야 합니다. 다른 옵션을 구성할 수도 있습니다.

포틀릿을 구성하려면 다음을 수행합니다.

1. 앱 서버의 Portal 관리 창에서 모든 포틀릿이 나열된 포틀릿 관리로 이동하고 AEM Portal Director 포틀릿을 선택합니다.
1. 필요에 따라 포틀릿을 구성합니다. 예를 들어 작성자 및 게시 인스턴스의 URL과 시작 경로의 URL을 변경해야 할 수 있습니다. 기본 구성은 [포틀릿 환경 설정](/help/sites-administering/aem-as-portal.md#portlet-preferences)에 설명되어 있습니다.

   >[!NOTE]
   >
   >포틀릿이 **/**&#x200B;과(와) 다른 컨텍스트 경로에서 실행 중인 AEM 작성자 및 게시 인스턴스에 연결하도록 구성된 경우 이러한 AEM 인스턴스의 Html 라이브러리 관리자 구성(예: Felix Webconsole을 통해)에서 강제 **CQUrlInfo**&#x200B;을(를) 활성화해야 합니다. 그렇지 않으면 편집이 작동하지 않고 환경 설정 대화 상자가 표시되지 않습니다.

1. 앱 서버에서 구성 변경 사항을 저장합니다.

1. 포틀릿에 대한 OSGI Admin Console로 이동합니다. 기본 위치는 `https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr`입니다. 기본 사용자 이름/암호는 **admin/admin**&#x200B;입니다.

1. **일 포털 디렉터 CQ 서버 구성** 구성을 선택하고 다음 값을 편집하십시오.

   * **작성자 기본 URL**: AEM 작성자 인스턴스의 기본 URL입니다.
   * **게시 기본 URL**: AEM 게시 인스턴스의 기본 URL입니다.
   * **작성자가 게시로 사용됨**: 게시로 사용되는 작성자 인스턴스입니다.
인스턴스(개발용)

   ![chlimage_1-137](assets/chlimage_1-137.png)

1. **저장**&#x200B;을 클릭합니다. 이제 포털 페이지에 포틀릿을 추가하고 포털을 사용할 수 있습니다.

### 컨텐츠 URL {#content-urls}

AEM에서 컨텐츠를 요청하면 포틀릿은 현재 표시 모드(게시 또는 작성자)와 현재 경로를 사용하여 전체 URL을 취합합니다. 기본값을 사용하는 경우 첫 번째 URL은 `https://localhost:4503/content/geometrixx/en.portlet.html`입니다. `htmlSelector` 값은 확장 전 URL에 자동으로 추가됩니다.

포틀릿이 도움말 모드로 전환되고 `appendHelpViewModeAsSelector`을(를) 선택하면 `help` 선택기도 추가됩니다(예: `https://localhost:4503/content/geometrixx/en.portlet.html.help`). 포틀릿 창을 최대화하고 `appendMaxWindowStateAsSelector`을(를) 선택하면 선택기도 추가됩니다(예: `https://localhost:4503/content/geometrixx/en.portlet.max.help`).

선택기는 AEM에서 평가할 수 있으며, 다른 템플릿을 다른 선택기에 사용할 수 있습니다.

### AEM에서 컨텐츠 Url 맵 사용 {#using-a-content-url-map-in-aem}

일반적으로 시작 경로는 AEM의 콘텐츠를 직접 가리킵니다. 그러나 포틀릿 환경 설정이 아닌 AEM에서 시작 경로를 유지하려면 `/var/portlets`과(와) 같은 AEM의 콘텐츠 맵에 대한 시작 경로를 지정할 수 있습니다. 이 경우 AEM에서 실행되는 스크립트는 포틀릿에서 제출된 정보를 사용하여 시작 URL을 결정할 수 있습니다. 올바른 URL로 리디렉션을 발행해야 합니다.

#### 포털 페이지에 포틀릿 추가 {#adding-the-portlet-to-the-portal-page}

포털 페이지에 포틀릿을 추가하려면 다음을 수행합니다.

1. 앱 서버의 관리 창에 있고 페이지를 관리하는 위치로 이동해야 합니다. 예를 들어 WebSphere 6.1에서 **페이지 관리**&#x200B;를 클릭합니다.
1. 포틀릿 이름을 선택한 다음 기존 페이지를 선택하거나 페이지를 만듭니다.
1. 페이지 레이아웃을 편집합니다.
1. 포틀릿을 선택하고 컨테이너에 추가합니다.
1. 변경 사항을 저장합니다.

#### 포틀릿 사용 {#using-the-portlet}

포틀릿에 추가한 페이지에 액세스하려면 다음을 수행합니다.

1. 포틀릿의 개인 설정 메뉴에서 포털에서 구성한 대로 포틀릿을 구성합니다.
1. 구성을 열고(포틀릿의 구성에 구성된 게시 시작 URL이 표시됨) 필요에 따라 편집한 다음 저장합니다.
