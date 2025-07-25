---
title: 데이터 캡처 기능 설치 및 구성
description: 적응형 양식, PDF forms 및 HTML5 Forms을 설치하고 구성합니다. 적응형 양식에 대한 Adobe Analytics 및 Adobe Target을 구성하여 양식 사용을 분석하고 프로필을 기반으로 사용자를 타겟팅합니다.
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on OSGi
exl-id: ee917b4b-fd38-4e05-8632-8efb82d9cddc
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 4%

---

# 데이터 캡처 기능 설치 및 구성{#install-and-configure-data-capture-capabilities}

## 소개 {#introduction}

AEM Forms은 최종 사용자로부터 데이터를 가져오기 위한 적응형 양식, HTML5 Forms 및 PDF forms 양식 세트를 제공합니다. 또한 웹 페이지에 사용 가능한 모든 양식을 나열하고 양식 사용을 분석하며 프로필을 기반으로 사용자를 타깃팅하는 도구를 제공합니다. 이러한 기능은 AEM Forms 추가 기능 패키지에 포함되어 있습니다. 추가 기능 패키지는 AEM의 작성자 또는 게시 인스턴스에 배포됩니다.

**적응형 양식:** 이러한 양식은 장치의 화면 크기에 따라 모양을 변경하고, 기본적으로 상호 작용합니다. 적응형 Forms은 Adobe Analytics, Adobe Sign 및 Adobe Target과도 통합할 수 있습니다. 이를 통해 인구 통계학 및 기타 기능을 기반으로 개인화된 양식 및 프로세스 지향 경험을 사용자에게 제공할 수 있습니다. 적응형 양식을 Adobe Sign과 통합할 수도 있습니다.

**PDF forms**&#x200B;은(는) PDF 문서 내에서 픽셀 단위 인쇄 및 디지털 정보 캡처에 적합합니다. 디지털 아바타에서는 Adobe Acrobat 또는 Acrobat Reader을 사용하여 이러한 양식을 채울 수 있습니다. 웹 사이트에서 이러한 양식을 호스팅하거나 양식 포털을 사용하여 AEM 사이트에 이러한 양식을 나열할 수 있습니다. 이러한 양식을 다른 사용자에게 첨부 파일로 전자 메일로 보낼 수도 있습니다. 이러한 양식은 데스크탑 환경에 가장 적합합니다.

**HTML5 Forms**&#x200B;은(는) 브라우저에 친숙한 PDF forms 버전입니다. HTML5 Forms은 PDF 플러그인을 지원하지 않는 환경에 적합합니다. HTML5 Forms을 사용하면 XFA 기반 PDF이 지원되지 않는 모바일 장치 및 데스크탑 브라우저에서 XFA 기반 양식을 렌더링할 수 있습니다. 이러한 양식은 태블릿과 데스크탑 환경에 가장 적합합니다.

AEM Forms은 강력한 엔터프라이즈급 플랫폼이며 데이터 캡처(적응형 양식, PDF forms 및 HTML5 Forms)는 AEM Forms의 기능 중 하나에 불과합니다. 전체 기능 목록은 [AEM Forms 소개](/help/forms/using/introduction-aem-forms.md)를 참조하십시오.

## 배포 토폴로지 {#deployment-topology}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. AEM Forms 데이터 캡처 기능을 실행하려면 AEM 작성자 및 AEM 게시 인스턴스가 최소 한 개 이상 있어야 합니다. AEM Forms AEM Forms 데이터 캡처 기능을 실행하려면 다음 토폴로지를 사용하는 것이 좋습니다. 토폴로지에 대한 자세한 내용은 [AEM Forms의 아키텍처 및 배포 토폴로지](/help/forms/using/aem-forms-architecture-deployment.md)를 참조하십시오.

![recommended-topology](assets/recommended-topology.png)

## 시스템 요구 사항 {#system-requirements}

AEM Forms의 데이터 캡처 기능을 설치하고 구성하기 전에 다음을 확인하십시오.

* 하드웨어 및 소프트웨어 인프라가 구축되어 있습니다. 지원되는 하드웨어 및 소프트웨어에 대한 자세한 목록을 보려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하십시오.

* AEM 인스턴스의 설치 경로에 공백이 포함되어 있지 않습니다.
* AEM 인스턴스가 실행 중입니다. Windows 사용자의 경우 관리자 모드로 AEM 인스턴스를 설치합니다. AEM 용어에서 &quot;인스턴스&quot;는 작성자 또는 게시 모드의 서버에서 실행되는 AEM의 사본입니다. AEM Forms 데이터 캡처 기능을 실행하려면 두 개 이상의 [AEM 인스턴스(작성자 1명 및 게시 1명)](/help/sites-deploying/deploy.md)가 필요합니다.

   * **작성자**: 콘텐츠를 만들고, 업로드하고, 편집하고, 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 콘텐츠를 실행할 준비가 되면 게시 인스턴스에 복제됩니다.
   * **게시**: 인터넷 또는 내부 네트워크를 통해 일반에게 게시된 콘텐츠를 제공하는 AEM 인스턴스입니다.

* 메모리 요구 사항이 충족됩니다. AEM Forms 추가 기능 패키지를 사용하려면 다음 작업을 수행해야 합니다.

   * Microsoft Windows 기반 설치용 15GB의 임시 공간.
   * UNIX 기반 설치의 경우 6GB의 임시 공간이 필요합니다.

* 작성자 및 게시 인스턴스에 대한 복제 및 역방향 복제가 설정되었습니다. 자세한 내용은 [복제](/help/sites-deploying/replication.md)를 참조하십시오.
* UNIX 기반 시스템의 경우:

   * 설치 미디어에서 다음 32비트 패키지를 설치합니다.

<table>
 <tbody>
  <tr>
   <td>지수</td>
   <td>fontconfig</td>
   <td>자유 형식</td>
   <td>아교</td>
  </tr>
  <tr>
   <td>라이브컬</td>
   <td>libice</td>
   <td>리비쿠</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>리부uid</td>
   <td>libX11</td>
   <td><p>libXau</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>libXinerama</td>
   <td>libXrandr</td>
   <td>libXrender</td>
  </tr>
  <tr>
   <td>nss-softokn-freebl</td>
   <td>Openssl</td>
   <td>즐리브</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* OpenSSL이 서버에 이미 설치되어 있는 경우 최신 버전으로 업그레이드합니다.
>* libcurl, libcrypto.so 및 libssl.so의 최신 버전을 각각 지정하는 심볼릭 링크를 만듭니다.
>

* 설치 미디어에서 다음 64비트 패키지를 설치합니다.

   * 리비쿠

* [Microsoft Visual Studio 2019 32비트 재배포 가능](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)을 설치합니다.


## AEM Forms 추가 기능 패키지 설치 {#install-aem-forms-add-on-package}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 이 패키지에는 AEM Forms 데이터 캡처 및 기타 기능이 포함되어 있습니다. 추가 기능 패키지를 설치하려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 헤더 메뉴에서 사용할 수 있는 **[!UICONTROL Adobe Experience Manager]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL 필터]** 섹션에서:
   1. **[!UICONTROL 솔루션]** 드롭다운 목록에서 **[!UICONTROL Forms]**&#x200B;을(를) 선택합니다.
   2. 패키지의 버전 및 유형을 선택합니다. **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수도 있습니다.
1. 운영 체제에 적용할 수 있는 패키지 이름을 선택하고 **[!UICONTROL EULA 약관 동의]**&#x200B;를 선택한 다음 **[!UICONTROL 다운로드]**&#x200B;를 선택합니다.
1. [패키지 관리자](/help/sites-administering/package-manager.md)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

   [AEM Forms 릴리스](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 문서에 나열된 직접 링크를 통해 패키지를 다운로드할 수도 있습니다.
1. 패키지를 설치한 후 AEM 인스턴스를 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 다시 시작하지 마십시오.** AEM Forms 서버를 중지하기 전에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTERED 메시지가 `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` 파일에 표시되지 않고 로그가 안정될 때까지 기다리십시오.

   >[!NOTE]
   >
   > SDK을 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK을 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.

1. 모든 Author 및 Publish 인스턴스에서 1~7단계를 반복합니다.

### (Windows만 해당) Visual Studio 재배포용 파일 자동 설치 {#automatic-installation-visual-studio-redistributables}

관리자 모드로 AEM 인스턴스를 설치하는 경우 AEM Forms 추가 기능 패키지를 설치하는 동안 32비트 Visual Studio 재배포 가능 패키지가 자동으로 설치됩니다.

Visual Studio 재배포용 파일을 자동으로 설치했는지 평가하려면 `/crx-repository/logs/` 디렉터리에서 사용할 수 있는 `error.log` 파일을 여십시오. 로그에는 다음 메시지가 포함됩니다.

`Redist <service name> already installed on system, will not attempt re-installation`

재배포 가능 패키지를 설치하지 못하면 로그에 다음 메시지가 포함됩니다.

`Current user does not have elevated privileges, aborting installation of redist <service name>`

이 문제를 해결하려면 AEM 서버를 다시 시작하고 관리자 모드로 AEM을 설치한 다음 AEM Forms 추가 기능 패키지를 설치하십시오.

권한 검사에 실패하면 로그에는 다음 메시지가 포함됩니다.

`Privilege escalation check failed with error: <error message>`

## 설치 후 구성 {#post-installation-configurations}

AEM Forms에는 몇 가지 필수 구성과 선택적 구성이 있습니다. 필수 구성에는 BouncyCastle 라이브러리 및 직렬화 에이전트 구성이 포함됩니다. 선택적 구성에는 Dispatcher, Forms 포털, Adobe Sign, Adobe Analytics 및 Adobe Target 구성이 포함됩니다.

### 필수 사후 설치 구성 {#mandatory-post-installation-configurations}

#### RSA 및 BouncyCastle 라이브러리 구성  {#configure-rsa-and-bouncycastle-libraries}

모든 작성자 및 게시 인스턴스에서 다음 단계를 수행하여 라이브러리를 부팅합니다.

1. 기본 AEM 인스턴스를 중지합니다.
1. 편집할 `[AEM installation directory]\crx-quickstart\conf\sling.properties` 페이지를 엽니다.

   `[AEM installation directory]\crx-quickstart\bin\start.bat`을(를) 사용하여 AEM을 시작한 경우 `[AEM_root]\crx-quickstart\`에 있는 sling.properties를 편집하십시오.

1. sling.properties 파일에 다음 속성을 추가합니다.

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 파일을 저장하고 닫은 다음 AEM 인스턴스를 시작합니다.
1. 모든 Author 및 Publish 인스턴스에서 1~4단계를 반복합니다.

#### 직렬화 에이전트 구성 {#configure-the-serialization-agent}

모든 작성자 및 게시 인스턴스에서 다음 단계를 수행하여 패키지를 허용 목록에 추가하다에 추가합니다.

1. 브라우저 창에서 AEM 구성 관리자를 엽니다. 기본 URL은 `https://'[server]:[port]'/system/console/configMgr`입니다.
1. **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name**&#x200B;을(를) 검색하고 구성을 엽니다.
1. **sun.util.calendar** 패키지를 **허용 목록** 필드에 추가합니다. **저장**&#x200B;을 클릭합니다.
1. 모든 Author 및 Publish 인스턴스에서 1~3단계를 반복합니다.

### 설치 후 구성 옵션 {#optional-post-installation-configurations}

#### Dispatcher 구성 {#configure-dispatcher}

Dispatcher은 엔터프라이즈급 웹 서버와 함께 사용할 수 있는 Adobe Experience Manager의 캐싱 및/또는 로드 밸런싱 도구입니다. [Dispatcher](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html)을(를) 사용하는 경우 AEM Forms에 대해 다음 구성을 수행하십시오.

1. AEM Forms에 대한 액세스 구성:

   편집할 dispatcher.any 파일을 엽니다. 필터 섹션으로 이동하고 필터 섹션에 다음 필터를 추가합니다.

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   파일을 저장하고 닫습니다. 필터에 대한 자세한 내용은 [Dispatcher 설명서](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html)를 참조하세요.

1. 레퍼러 필터 서비스를 구성합니다.

   Apache Felix 구성 관리자에 관리자로 로그인합니다. 구성 관리자의 기본 URL은 `https://[server]:[port_number]/system/console/configMgr`입니다. **구성** 메뉴에서 **Apache Sling Referrer 필터** 옵션을 선택합니다. 호스트 허용 필드에 레퍼러로 허용할 디스패처의 호스트 이름을 입력하고 **저장**&#x200B;을 클릭합니다. 항목의 형식은 `https://[server]:[port]`입니다.

#### 캐시 구성 {#configure-cache}

캐싱은 데이터 액세스 시간을 단축하고, 지연을 줄이고, 입출력(I/O) 속도를 향상시키는 메커니즘입니다. 적응형 양식 캐시는 미리 채워진 데이터를 저장하지 않고 적응형 양식의 HTML 콘텐츠 및 JSON 구조만 저장합니다. 적응형 양식을 렌더링하는 데 필요한 시간을 줄이는 데 도움이 됩니다.

* 적응형 양식 캐시를 사용할 때 [AEM Dispatcher](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html)을(를) 사용하여 적응형 양식의 클라이언트 라이브러리(CSS 및 JavaScript)를 캐시합니다.
* 사용자 지정 구성 요소를 개발하는 동안 개발에 사용되는 서버에서 적응형 양식 캐시를 비활성화 상태로 유지합니다.

다음 단계를 수행하여 적응형 양식 캐시를 구성합니다.

1. https://&#39;[server]:[port]&#39;/system/console/configMgr에서 AEM 웹 콘솔 구성 관리자로 이동합니다.
1. 구성 값을 편집하려면 **적응형 양식 및 대화형 통신 웹 채널 구성**&#x200B;을 클릭하십시오. 구성 값 편집 대화 상자에서 AEM Forms 서버 인스턴스가 캐시할 수 있는 양식 또는 문서의 최대 수를 **적응형 Forms 수** 필드에 지정합니다. 기본값은 100입니다. **저장**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >캐시를 비활성화하려면 적응형 Forms 수 필드의 값을 **0**(으)로 설정합니다. 캐시 구성을 비활성화하거나 변경하면 캐시가 재설정되고 모든 양식 및 문서가 캐시에서 제거됩니다.

#### 양식 데이터 모델에 대한 SSL 통신 구성 {#configure-ssl-communcation-for-form-data-model}

양식 데이터 모델에 대해 SSL 통신을 활성화할 수 있습니다. 양식 데이터 모델에 대해 SSL 통신을 활성화하려면 AEM Forms 인스턴스를 시작하기 전에 모든 인스턴스의 Java Trust Store에 인증서를 추가합니다. 아래 명령을 실행하여 인증서를 추가할 수 있습니다. &quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Adobe Sign 구성 {#configure-adobe-sign}

Adobe Sign을 사용하면 적응형 양식용 전자 서명 워크플로를 사용할 수 있습니다. 전자 서명은 법무, 판매, 임금, 인적 자원 관리 등의 다양한 분야에서 문서를 처리하는 워크플로를 개선합니다.

일반적인 Adobe Sign 및 적응형 양식 시나리오에서 사용자는 적응형 양식에 **서비스를 신청**&#x200B;합니다. 신용 카드 신청 양식과 시민 혜택 양식을 예로 들 수 있습니다. 사용자가 신청 양식에 정보를 입력하고 이를 제출한 뒤 서명하면, 이후의 액션이 가능하도록 양식이 서비스 제공자에게 전달됩니다. 서비스 공급자는 애플리케이션을 검토하고 Adobe Sign을 사용하여 애플리케이션을 승인된 것으로 표시합니다. Adobe Sign을 AEM Forms과 통합하여 유사한 전자 서명 워크플로를 활성화할 수 있습니다.

AEM Forms에서 Adobe Sign을 사용하려면 [AEM Forms과 Adobe Sign을 통합](/help/forms/using/adobe-sign-integration-adaptive-forms.md)하십시오.

#### Adobe Analytics 구성 {#configure-adobe-analytics}

AEM Forms은 Adobe Analytics과 통합되어 게시된 양식 및 문서에 대한 성능 지표를 캡처하고 추적할 수 있습니다. 이러한 지표를 분석하는 목표는 양식이나 문서를 보다 유용하게 만드는 데 필요한 변경 사항에 대한 데이터를 기반으로 정보에 입각한 결정을 내리는 것입니다.

AEM Forms에서 Adobe Analytics을 사용하려면 [분석 및 보고서 구성](/help/forms/using/configure-analytics-forms-documents.md)을 참조하세요.

#### Adobe Target 통합 {#integrate-adobe-target}

고객이 제공하는 경험이 매력적이지 않을 경우 양식을 포기할 가능성이 높습니다. 고객에게는 번거로운 일이지만, 조직의 지원 규모와 비용도 증가할 수 있습니다. 전환율을 높이는 올바른 고객 경험을 파악하고 제공하는 것은 중요하고 어려운 일입니다. 이 문제의 핵심은 AEM forms입니다.

AEM forms는 Adobe Marketing Cloud 솔루션인 Adobe Target과 통합되어 여러 디지털 채널에서 개인화되고 매력적인 고객 경험을 제공합니다. Adobe Target을 사용하여 A/B 테스트 적응형 양식을 만들려면 [Adobe Target과 AEM Forms을 통합](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)하십시오.

## 다음 단계 {#next-steps}

AEM Forms 데이터 캡처 기능을 사용할 환경을 구성했습니다. 이제 기능을 사용하기 위한 다음 단계는 다음과 같습니다.

* [첫 번째 적응형 양식 만들기](/help/forms/using/create-your-first-adaptive-form.md)
* [첫 번째 PDF 양식 만들기](https://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [HTML5 Forms 소개](/help/forms/using/introduction.md)
