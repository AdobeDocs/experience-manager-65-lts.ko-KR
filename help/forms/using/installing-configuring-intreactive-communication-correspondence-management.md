---
title: 대화형 통신 설치 및 구성
description: AEM Forms Interactive Communications를 설치 및 구성하여 비즈니스 서신, 문서, 명세서, 혜택 공지, 마케팅 이메일, 청구서 및 시작 키트를 만듭니다.
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication,Correspondence Management
exl-id: d03965e1-4fa3-414c-80b6-c9fca281bee4
source-git-commit: bd33420307a7be6664b6bbb52677af66edaa9c0e
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 2%

---

# 대화형 통신 설치 및 구성{#install-and-configure-interactive-communications}

## 소개 {#introduction}

AEM Form은 비즈니스 서신, 문서, 명세서, 혜택 공지, 마케팅 이메일, 청구서 및 환영 키트와 같은 안전한 대화형 문서의 작성, 조립, 관리 및 전달을 중앙에서 관리할 수 있는 기능을 제공합니다. 이 기능을 대화형 통신이라고 합니다. 이 기능은 AEM Forms 추가 기능 패키지에 포함되어 있습니다. 추가 기능 패키지는 AEM의 작성자 또는 게시 인스턴스에 배포됩니다.

대화형 통신 기능을 사용하여 여러 형식으로 통신을 생성할 수 있습니다. 예: 웹 및 PDF. AEM Workflow와 대화형 커뮤니케이션을 통합하여 고객이 선택한 채널에서 조립된 커뮤니케이션을 처리하고 고객에게 전달할 수 있습니다. (예: 이메일을 통해 최종 사용자에게 커뮤니케이션 전송)

이전 버전에서 업그레이드하고 서신 관리에 이미 투자한 경우 [호환성 패키지](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package)를 설치하여 서신 관리를 계속 사용할 수 있습니다. 대화형 통신과 서신 관리의 차이점에 대한 자세한 내용은 [대화형 통신 개요](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management)를 참조하십시오.

AEM Forms은 강력한 엔터프라이즈급 플랫폼입니다. 대화형 통신은 AEM Forms의 기능 중 하나일 뿐입니다. 전체 기능 목록은 [AEM Forms 소개](../../forms/using/introduction-aem-forms.md)를 참조하십시오.

## 배포 토폴로지 {#deployment-topology}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 대화형 통신 기능을 실행하려면 최소 하나의 AEM 작성자 및 처리 인스턴스만 필요합니다. 다음 토폴로지는 OSGi 기능에서 AEM Forms 대화형 통신, 서신 관리, AEM Forms 데이터 캡처 및 Forms 중심 워크플로우를 실행하는 토폴로지 입니다. 토폴로지에 대한 자세한 내용은 [AEM Forms의 아키텍처 및 배포 토폴로지](/help/forms/using/aem-forms-architecture-deployment.md)를 참조하십시오.

![recommended-topology](assets/recommended-topology.png)

AEM Forms Interactive Communications는 AEM Forms 작성자 인스턴스에서 관리, 작성 및 에이전트 사용자 인터페이스를 실행합니다. 게시 인스턴스는 최종 사용자가 사용할 수 있는 대화형 통신의 최종 버전을 호스팅합니다.

## 시스템 요구 사항 {#system-requirements}

AEM Forms의 대화형 통신 및 서신 관리 기능을 설치하고 구성하기 전에 다음을 확인하십시오.

* 하드웨어 및 소프트웨어 인프라가 구축되어 있습니다. 지원되는 하드웨어 및 소프트웨어에 대한 자세한 목록을 보려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하십시오.

* AEM 인스턴스의 설치 경로에 공백이 포함되어 있지 않습니다.
* AEM 인스턴스가 실행 중입니다. AEM 용어에서 &quot;인스턴스&quot;는 작성자 또는 게시 모드의 서버에서 실행되는 AEM의 사본입니다. AEM Forms 대화형 통신 및 서신 관리 기능을 실행하려면 AEM 인스턴스(작성자 또는 처리)가 하나 이상 있어야 합니다.

   * **작성자**: 콘텐츠를 만들고, 업로드하고, 편집하고, 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 콘텐츠를 실행할 준비가 되면 게시 인스턴스에 복제됩니다.
   * **처리 중:** 처리 인스턴스는 [확정된 AEM 작성자](/help/forms/using/hardening-securing-aem-forms-environment.md) 인스턴스입니다. 작성자 인스턴스를 설정하고 설치를 수행한 후 인스턴스를 강화할 수 있습니다.

   * **게시**: 인터넷 또는 내부 네트워크를 통해 일반에게 게시된 콘텐츠를 제공하는 AEM 인스턴스입니다.

* 메모리 요구 사항이 충족됩니다. AEM Forms 추가 기능 패키지를 사용하려면 다음 작업을 수행해야 합니다.

   * Microsoft® Windows 기반 설치용 15GB의 임시 공간.
   * UNIX 기반 설치의 경우 6GB의 임시 공간이 필요합니다.

* UNIX 기반 시스템에 대한 추가 요구 사항: UNIX 기반 운영 체제를 사용하는 경우 해당 운영 체제의 설치 미디어에서 다음 패키지를 설치합니다.

<table>
 <tbody>
  <tr>
   <td>지수</td>
   <td>libxcb</td>
   <td>자유 형식</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>즐리브</td>
   <td>libice</td>
   <td>리부uid</td>
  </tr>
  <tr>
   <td>아교</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## AEM Forms 추가 기능 패키지 설치 {#install-aem-forms-add-on-package}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 이 패키지에는 AEM Forms 대화형 통신, 서신 관리 및 기타 기능이 포함되어 있습니다. 추가 기능 패키지를 설치하려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 헤더 메뉴에서 사용할 수 있는 **[!UICONTROL Adobe Experience Manager]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL 필터]** 섹션에서:
   1. **[!UICONTROL 솔루션]** 드롭다운 목록에서 **[!UICONTROL Forms]**&#x200B;을(를) 선택합니다.
   2. 패키지의 버전 및 유형을 선택합니다. **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수도 있습니다.
1. 운영 체제에 적용할 수 있는 패키지 이름을 선택하고 **[!UICONTROL EULA 약관 동의]**&#x200B;를 선택한 다음 **[!UICONTROL 다운로드]**&#x200B;를 선택합니다.
1. [패키지 관리자](/help/sites-administering/package-manager.md)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

   [AEM Forms 릴리스](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ko) 문서에 나열된 직접 링크를 통해 패키지를 다운로드할 수도 있습니다.

1. 패키지를 설치한 후 AEM 인스턴스를 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 다시 시작하지 마십시오.** AEM Forms 서버를 중지하기 전에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTERED 메시지가 [AEM-Installation-Directory]/crx-quickstart/logs/error.log 파일에 나타나지 않고 로그가 안정될 때까지 기다리십시오.

   >[!NOTE]
   >
   > SDK을 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK을 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.

1. 모든 Author 및 Publish 인스턴스에서 1~7단계를 반복합니다.

## 설치 후 구성 {#post-installation-configurations}

AEM Forms에는 몇 가지 필수 구성과 선택적 구성이 있습니다. 필수 구성에는 BouncyCastle 라이브러리 및 직렬화 에이전트 구성이 포함됩니다. 선택적 구성에는 Dispatcher 및 Adobe Target 구성이 포함됩니다.

### 필수 사후 설치 구성 {#mandatory-post-installation-configurations}

#### RSA 및 BouncyCastle 라이브러리 구성  {#configure-rsa-and-bouncycastle-libraries}

모든 작성자 및 게시 인스턴스에서 다음 단계를 수행하여 라이브러리를 부팅합니다.

1. 기본 AEM 인스턴스를 중지합니다.
1. 편집할 [AEM 설치 디렉터리]\crx-quickstart\conf\sling.properties 파일을 엽니다.

   [AEM 설치 디렉터리]\crx-quickstart\bin\start.bat을 사용하여 AEM을 시작한 경우 [AEM_root]\crx-quickstart\에서 sling.properties를 편집합니다.

1. sling.properties 파일에 다음 속성을 추가합니다.

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. 파일을 저장하고 닫은 다음 AEM 인스턴스를 시작합니다.
1. 모든 Author 및 Publish 인스턴스에서 1~4단계를 반복합니다.

#### 직렬화 에이전트 구성 {#configure-the-serialization-agent}

모든 작성자 및 게시 인스턴스에서 다음 단계를 수행하여 패키지를 허용 목록에 추가하다에 추가합니다.

1. 브라우저 창에서 AEM 구성 관리자를 엽니다. 기본 URL은 https://&#39;[server]:[port]&#39;/system/console/configMgr입니다.
1. **Deserialization Firewall Configuration**&#x200B;을 검색하여 엽니다.
1. **sun.util.calendar** 패키지를 **허용 목록** 필드에 추가합니다. 저장을 클릭합니다.
1. 모든 Author 및 Publish 인스턴스에서 1~3단계를 반복합니다.

### 설치 후 구성 옵션 {#optional-post-installation-configurations}

#### 호환성 패키지 설치 {#install-compatibility-package}

대화형 통신은 AEM 6.5 Forms에서 고객 커뮤니케이션을 만들기 위한 기본적이고 권장되는 방법입니다. 이전 버전에서 업그레이드하거나 마이그레이션한 후 편지(서신 관리)를 계속 사용할 계획이라면 [AEMFD 호환성 패키지](/help/forms/using/compatibility-package.md)를 설치하십시오.

AEMFD 호환성 패키지를 통해 AEM 6.5 Forms에서 AEM 6.4 Forms, AEM 6.3 Forms 및 AEM 6.2 Forms의 다음 자산을 사용할 수 있습니다.

* 문서 단편
* 편지
* 데이터 사전
* 적응형 양식 더 이상 사용되지 않는 템플릿 및 페이지

#### Dispatcher 구성 {#configure-dispatcher}

Dispatcher은 엔터프라이즈급 웹 서버와 함께 사용되는 Adobe Experience Manager의 캐싱 및 로드 밸런싱 도구입니다. [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ko-KR)을(를) 사용하는 경우 AEM Forms에 대해 다음 구성을 수행하십시오.

1. AEM Forms에 대한 액세스 구성:

   편집할 dispatcher.any 파일을 엽니다. 필터 섹션으로 이동하고 필터 섹션에 다음 필터를 추가합니다.

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   파일을 저장하고 닫습니다. 필터에 대한 자세한 내용은 [Dispatcher 설명서](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ko-KR)를 참조하세요.

1. 레퍼러 필터 서비스를 구성합니다.

   Apache Felix 구성 관리자에 관리자로 로그인합니다. 구성 관리자의 기본 URL은 https://&#39;server&#39;:[port_number]/system/console/configMgr입니다. **구성** 메뉴에서 **Apache Sling Referrer 필터** 옵션을 선택합니다. 호스트 허용 필드에 레퍼러로 허용할 Dispatcher의 호스트 이름을 입력하고 **저장**&#x200B;을 클릭합니다. 항목의 형식은 https://&#39;[server]:[port]&#39;입니다.

#### Adobe Target 통합 {#integrate-adobe-target}

고객은 대화형 커뮤니케이션이 제공하는 경험이 도움이 되지 않을 경우 이를 포기할 가능성이 높습니다. 고객에게는 번거로운 일이지만, 조직의 지원 규모와 비용도 늘어납니다. 전환율을 높이는 올바른 고객 경험을 파악하고 제공하는 것은 중요하고 어려운 일입니다. 이 문제의 핵심은 AEM forms입니다.

AEM forms는 Adobe Experience Cloud 솔루션인 Adobe Target과 통합되어 여러 디지털 채널에서 개인화되고 매력적인 고객 경험을 제공합니다. Adobe Target을 사용하여 대화형 통신을 개인화하려면 [AEM Forms과 Adobe Target 통합](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)을 하세요.

#### 양식 데이터 모델에 대한 SSL 통신 구성  {#configure-ssl-communcation-for-form-data-model}

양식 데이터 모델에 대해 SSL 통신을 활성화할 수 있습니다. 양식 데이터 모델에 대해 SSL 통신을 활성화하려면 AEM Forms 인스턴스를 시작하기 전에 모든 인스턴스의 Java™ Trust Store에 인증서를 추가합니다. 아래 명령을 실행하여 인증서를 추가할 수 있습니다.

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 다음 단계 {#next-steps}

대화형 통신 및 서신 관리 기능을 사용할 환경을 구성했습니다. 이제 기능을 사용하는 단계는 다음과 같습니다.

* [서신 관리 개요](/help/forms/using/interactive-communications-overview.md)

* [대화형 통신 만들기](../../forms/using/create-interactive-communication.md)

* [서신 관리 편지 만들기](../../forms/using/create-letter.md)
