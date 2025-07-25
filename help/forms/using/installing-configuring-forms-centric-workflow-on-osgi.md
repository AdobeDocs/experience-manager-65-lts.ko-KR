---
title: OSGi에서 Forms 중심 워크플로우 설치 및 구성
description: AEM Forms Interactive Communications를 설치 및 구성하여 비즈니스 서신, 문서, 명세서, 혜택 공지, 마케팅 이메일, 청구서 및 시작 키트를 만듭니다.
topic-tags: installing
docset: aem65
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication,AEM Forms on OSGi
exl-id: 4b316ade-4431-41fc-bb8a-7262a17fb456
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 4%

---

# OSGi에서 Forms 중심 워크플로우 설치 및 구성{#installing-and-configuring-forms-centric-workflow-on-osgi}

## 소개 {#introduction}

기업은 여러 양식, 백엔드 시스템 및 기타 데이터 소스에서 데이터를 수집하고 처리합니다. 데이터 처리에는 검토 및 승인 절차, 반복 작업, 데이터 보관이 포함됩니다. 예를 들어 양식을 검토하여 PDF 문서로 변환합니다. 반복적인 작업을 수동으로 수행하는 경우 많은 시간과 많은 리소스가 소요될 수 있습니다.

[OSGi의 Forms 중심 워크플로](../../forms/using/aem-forms-workflow.md)를 사용하여 적응형 양식 기반 워크플로를 신속하게 빌드할 수 있습니다. 이러한 워크플로를 통해 검토 및 승인 워크플로, 비즈니스 프로세스 워크플로 및 기타 반복적인 작업을 자동화할 수 있습니다. 이러한 워크플로는 문서 처리(PDF 문서 만들기, 조합, 배포 및 보관, 디지털 서명 추가 등을 통해 문서 액세스를 제한, 바코드 양식 디코딩)와 양식 및 문서와 함께 Adobe Sign 서명 워크플로를 사용하는 데에도 도움이 됩니다.

설정되면 이러한 워크플로우를 수동으로 트리거하여 정의된 프로세스를 완료하거나 사용자가 양식 또는 대화형 통신을 제출할 때 프로그래밍 방식으로 실행할 수 있습니다. 이 기능은 AEM Forms 추가 기능 패키지에 포함되어 있습니다.

AEM Forms은 강력한 엔터프라이즈급 플랫폼입니다. OSGi에서의 Forms 중심 워크플로우는 AEM Forms의 기능 중 하나일 뿐입니다. 전체 기능 목록은 [AEM Forms 소개](introduction-aem-forms.md)를 참조하십시오.

>[!NOTE]
>
>OSGi의 Forms 중심 워크플로우를 사용하면 OSGi 스택에서 다양한 작업을 위한 워크플로우를 빠르게 빌드하고 배포할 수 있습니다<!--, without having to install the full-fledged Process Management capability on JEE stack-->.<!-- See a [comparison](capabilities-osgi-jee-workflows.md) of the Forms-centric AEM Workflows on OSGi and Process Management on JEE to learn the difference and similarities in the capabilities.--><!--After the comparison, If you choose to install the Process Management capability on JEE stack, see [Install or Upgrade AEM Forms on JEE](/help/forms/using/introduction-aem-forms.md) for detailed information about installing and configuring JEE stack and the Process Management capabilities.-->

## 배포 토폴로지 {#deployment-topology}

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. OSGi 기능에서 AEM 중심 워크플로를 실행하려면 Forms 작성자 또는 처리 인스턴스(프로덕션 작성자)가 최소 한 명 이상만 필요합니다. 처리 인스턴스는 [확정된 AEM 작성자](/help/forms/using/hardening-securing-aem-forms-environment.md) 인스턴스입니다. 프로덕션 작성자에서 워크플로우 또는 적응형 양식 작성과 같은 실제 작성을 수행하지 마십시오.

다음 토폴로지는 OSGi 기능에서 AEM Forms 대화형 통신, 서신 관리, AEM Forms 데이터 캡처 및 Forms 중심 워크플로우를 실행하는 토폴로지 입니다. 토폴로지에 대한 자세한 내용은 [AEM Forms의 아키텍처 및 배포 토폴로지](/help/forms/using/aem-forms-architecture-deployment.md)를 참조하십시오.

![recommended-topology](assets/recommended-topology.png)

OSGi의 AEM Forms Forms 중심 워크플로우는 AEM Forms의 작성자 인스턴스에서 AEM 받은 편지함 및 AEM 워크플로 모델 생성 UI를 실행합니다.

## 시스템 요구 사항 {#system-requirements}

>[!NOTE]
>
>[데이터 캡처 기능 설치 및 구성](../../forms/using/installing-configuring-aem-forms-osgi.md) 문서에 설명된 대로 OSGi에 AEM Forms을 이미 설치한 경우 문서의 [다음 단계](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) 섹션으로 건너뜁니다.

OSGi에서 Forms 중심 워크플로를 설치하고 구성하기 전에 다음을 확인하십시오.

* 하드웨어 및 소프트웨어 인프라가 구축되어 있습니다. 지원되는 하드웨어 및 소프트웨어에 대한 자세한 목록을 보려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하십시오.

* AEM 인스턴스의 설치 경로에 공백이 포함되어 있지 않습니다.
* AEM 인스턴스가 실행 중입니다. AEM 용어에서 &quot;인스턴스&quot;는 작성자 또는 게시 모드의 서버에서 실행되는 AEM의 사본입니다. OSGi에서 Forms 중심 워크플로우를 실행하려면 하나 이상의 AEM 인스턴스(작성자 또는 처리)가 필요합니다.

   * **작성자**: 콘텐츠를 만들고, 업로드하고, 편집하고, 웹 사이트를 관리하는 데 사용되는 AEM 인스턴스입니다. 콘텐츠를 실행할 준비가 되면 게시 인스턴스에 복제됩니다.
   * **처리 중:** 처리 인스턴스는 [확정된 AEM 작성자](/help/forms/using/hardening-securing-aem-forms-environment.md) 인스턴스입니다. 작성자 인스턴스를 설정하고 설치를 수행한 후 인스턴스를 강화할 수 있습니다.

   * **게시**: 인터넷 또는 내부 네트워크를 통해 일반에게 게시된 콘텐츠를 제공하는 AEM 인스턴스입니다.

* 메모리 요구 사항이 충족됩니다. AEM Forms 추가 기능 패키지를 사용하려면 다음 작업을 수행해야 합니다.

   * Microsoft Windows 기반 설치용 15GB의 임시 공간.
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

AEM Forms 추가 기능 패키지는 AEM에 배포된 애플리케이션입니다. 이 패키지에는 OSGi 및 기타 기능의 Forms 중심 워크플로가 포함되어 있습니다. 추가 기능 패키지를 설치하려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 헤더 메뉴에서 사용할 수 있는 **[!UICONTROL Adobe Experience Manager]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL 필터]** 섹션에서:
   1. **[!UICONTROL 솔루션]** 드롭다운 목록에서 **[!UICONTROL Forms]**&#x200B;을(를) 선택합니다.
   2. 패키지의 버전 및 유형을 선택합니다. **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수도 있습니다.
1. 운영 체제에 적용할 수 있는 패키지 이름을 선택하고 **[!UICONTROL EULA 약관 동의]**&#x200B;를 선택한 다음 **[!UICONTROL 다운로드]**&#x200B;를 선택합니다.
1. [패키지 관리자](/help/sites-administering/package-manager.md)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

   [AEM Forms 릴리스](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 문서에 나열된 직접 링크를 통해 패키지를 다운로드할 수도 있습니다.

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

   [AEM 설치 디렉터리]\crx-quickstart\bin\start.bat을 사용하여 AEM을 시작한 경우 [AEM_root]\crx-quickstart\에 있는 sling.properties를 편집합니다.

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

#### Dispatcher 구성 {#configure-dispatcher}

Dispatcher은 AEM용 캐싱 및 로드 밸런싱 도구입니다. AEM Dispatcher은 또한 공격으로부터 AEM 서버를 보호하는 데 도움이 됩니다. Dispatcher과 엔터프라이즈급 웹 서버를 함께 사용하여 AEM 인스턴스의 보안을 강화할 수 있습니다. [Dispatcher](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html)을(를) 사용하는 경우 AEM Forms에 대해 다음 구성을 수행하십시오.

1. AEM Forms에 대한 액세스 구성:

   편집할 dispatcher.any 파일을 엽니다. 필터 섹션으로 이동하고 필터 섹션에 다음 필터를 추가합니다.

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   파일을 저장하고 닫습니다. 필터에 대한 자세한 내용은 [Dispatcher 설명서](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html)를 참조하세요.

1. 레퍼러 필터 서비스를 구성합니다.

   Apache Felix 구성 관리자에 관리자로 로그인합니다. 구성 관리자의 기본 URL은 https://&#39;server&#39;:[port_number]/system/console/configMgr입니다. **구성** 메뉴에서 **Apache Sling Referrer 필터** 옵션을 선택합니다. 호스트 허용 필드에 레퍼러로 허용할 디스패처의 호스트 이름을 입력하고 **저장**&#x200B;을 클릭합니다. 항목의 형식은 `https://'[server]:[port]'`입니다.

#### 캐시 구성 {#configure-cache}

캐싱은 데이터 액세스 시간을 단축하고, 지연을 줄이고, 입출력(I/O) 속도를 향상시키는 메커니즘입니다. 적응형 양식 캐시는 미리 채워진 데이터를 저장하지 않고 적응형 양식의 HTML 콘텐츠 및 JSON 구조만 저장합니다. 적응형 양식을 렌더링하는 데 필요한 시간을 줄이는 데 도움이 됩니다.

* 적응형 양식 캐시를 사용할 때 [AEM Dispatcher](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html)을(를) 사용하여 적응형 양식의 클라이언트 라이브러리(CSS 및 JavaScript)를 캐시합니다.
* 사용자 지정 구성 요소를 개발하는 동안 개발에 사용되는 서버에서 적응형 양식 캐시를 비활성화 상태로 유지합니다.

다음 단계를 수행하여 적응형 양식 캐시를 구성합니다.

1. `https://'[server]:[port]'/system/console/configMgr`의 AEM 웹 콘솔 구성 관리자로 이동합니다.
1. 구성 값을 편집하려면 **[!UICONTROL 적응형 양식 및 대화형 통신 웹 채널 구성]**&#x200B;을 클릭하십시오. 구성 값 편집 대화 상자에서 AEM Forms 서버 인스턴스가 캐시할 수 있는 양식 또는 문서의 최대 수를 **적응형 Forms 수** 필드에 지정합니다. 기본값은 100입니다. **저장**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >캐시를 비활성화하려면 적응형 Forms 수 필드의 값을 **0**(으)로 설정합니다. 캐시 구성을 비활성화하거나 변경하면 캐시가 재설정되고 모든 양식 및 문서가 캐시에서 제거됩니다.

#### Adobe Sign 구성 {#configure-adobe-sign}

Adobe Sign을 사용하면 적응형 양식용 전자 서명 워크플로를 사용할 수 있습니다. 전자 서명은 법무, 판매, 임금, 인적 자원 관리 등의 다양한 분야에서 문서를 처리하는 워크플로를 개선합니다.

OSGi 시나리오의 일반적인 Adobe Sign 및 Forms 중심 워크플로에서 사용자는 **서비스 신청**&#x200B;에 적응형 양식을 작성합니다. 신용 카드 신청 양식과 시민 혜택 양식을 예로 들 수 있습니다. 사용자가 신청 양식에 정보를 입력하고 이를 제출한 뒤 서명하면 승인/거부 워크플로가 시작됩니다. 서비스 공급자는 AEM 받은 편지함에서 애플리케이션을 검토하고 Adobe Sign을 사용하여 애플리케이션에 전자적으로 서명합니다. Adobe Sign을 AEM Forms과 통합하여 유사한 전자 서명 워크플로를 활성화할 수 있습니다.

AEM Forms에서 Adobe Sign을 사용하려면 [AEM Forms과 Adobe Sign을 통합](../../forms/using/adobe-sign-integration-adaptive-forms.md)하십시오.

## 다음 단계 {#next-steps}

OSGi 기능에서 Forms 중심 워크플로를 사용하도록 환경을 구성했습니다. 이제 기능을 사용하는 단계는 다음과 같습니다.

* [OSGi에서 Forms 중심 워크플로우 사용](../../forms/using/aem-forms-workflow.md)
* [워크플로 단계 참조](/help/sites-developing/workflows-step-ref.md)
* [편지 및 대화형 커뮤니케이션의 사후 처리](../../forms/using/submit-letter-topostprocess.md)
