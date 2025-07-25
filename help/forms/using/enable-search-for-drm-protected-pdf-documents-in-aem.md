---
title: AEM에서 문서 보안으로 보호된 PDF 문서를 검색할 수 있도록 설정
description: DRM으로 보호된 AEM 문서에 대해 전체 텍스트 검색을 수행할 수 있도록 기본 PDF 검색을 활성화하는 방법을 알아봅니다.
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: ad86398d-0dc9-4168-b409-4d231b8d586b
source-git-commit: 757c26274b39f5fb37a090f320493abd1af44c42
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# AEM에서 문서 보안으로 보호된 PDF 문서를 검색할 수 있도록 설정{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM 검색은 AEM assets를 검색 및 찾고 일반 텍스트 파일, Microsoft Office 문서 및 PDF 문서와 같이 일반적으로 사용되는 다양한 문서 형식에 대해 텍스트 검색을 수행할 수 있습니다. 또한 기본 검색을 확장하여 [AEM Document Security로 보호된 PDF 문서](../../forms/using/admin-help/document-security.md)에서 전체 텍스트 검색을 수행할 수도 있습니다. AEM에서 이러한 문서에 대해 전체 텍스트 검색을 수행할 수 있도록 하려면 다음 단계를 수행하십시오.

1. 보안 연결 설정
1. 정책으로 보호된 샘플 PDF 문서 색인화

## 사전 요구 사항 {#prerequisites}

* OSGi에서 AEM Forms을 사용하는 경우:

   * AEM Forms 서버에 [AEM Forms Document Security Indexer 패키지](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html)를 설치하십시오.

   * JEE 서버의 AEM Forms이 실행 중이고 JEE 서버의 해당 AEM Forms에 문서 보안이 설치되어 있는지 확인합니다. 보호된 문서를 인덱싱하려면 JEE 서버의 AEM Form이 필요합니다.

* JEE 서버에서 AEM Forms만 사용하는 경우 인덱서 패키지가 이미 설치되어 있습니다.
* 모든 번들이 실행 중인지 확인합니다. 모든 번들이 활성화되지 않은 경우 모든 번들이 실행되고 실행될 때까지 기다립니다.

   * OSGi의 AEM Forms에 대한 번들은 https://&#39;[server]:[port]&#39;/system/console/bundles에 나열됩니다.
   * JEE의 AEM Forms의 경우, 번들은 https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundles에 나열됩니다. 예: https://localhost:8080/lc/system/console/bundles.

* {sun.util.1} 패키지를 0개 허용 목록에 추가합니다. ** 패키지를 허용 목록에 추가하다에 추가하려면 다음 단계를 수행하십시오.

   1. AEM 웹 콘솔을 엽니다. URL은 https://&#39;[server]:[port]&#39;/system/console/configMgr입니다.
   1. **Deserialization Firewall Configuration**&#x200B;을 찾아 엽니다.

   1. 허용 목록에추가된 클래스 또는 패키지 접두사 필드에 sun.util.calendar 패키지를 추가하고 **저장**&#x200B;을 클릭합니다.

### AEM Forms JEE와 OSGi 스택 간의 보안 연결을 설정합니다. {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

다음 방법 중 하나를 사용하여 보안 연결을 설정할 수 있습니다.

* JEE 관리 자격 증명에서 Adobe으로 AEM Forms LiveCycle Client SDK 번들 구성
* 상호 인증을 사용하여 Adobe LiveCycle Client SDK 번들 구성

#### JEE 관리 자격 증명에서 Adobe으로 AEM Forms LiveCycle Client SDK 번들 구성 {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. AEM 웹 콘솔을 엽니다. URL은 https://&#39;[server]:[port]&#39;/system/console/configMgr입니다.
1. **Adobe LiveCycle Client SDK 번들**&#x200B;을 찾아 엽니다. 다음 필드에 대한 값을 지정하십시오.

   * **서버 URL:** JEE 서버에서 AEM Forms의 HTTPS URL을 지정합니다. https를 통해 통신하려면 -Djavax.net.ssl.trustStore=&lt;JEE 키 저장소 파일의 AEM Forms 경로> 매개 변수를 사용하여 서버를 다시 시작하십시오.
   * **서비스 이름**: 지정된 서비스 목록에 RightsManagementService를 추가합니다.
   * **사용자 이름:** AEM 서버에서 호출을 시작하는 데 사용할 JEE 계정의 AEM Forms 사용자 이름을 지정합니다. 지정된 계정에 JEE 서버의 AEM Forms에서 문서 서비스를 시작할 수 있는 권한이 있어야 합니다.
   * **암호**: 사용자 이름 필드에 언급된 JEE 계정의 AEM Forms 암호를 지정하십시오.

   **저장**&#x200B;을 클릭합니다. AEM은 문서 보안으로 보호된 PDF 문서를 검색할 수 있도록 활성화됩니다.

#### 상호 인증을 사용하여 Adobe LiveCycle Client SDK 번들 구성 {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. JEE에서 AEM Forms에 대한 상호 인증을 활성화합니다.
1. AEM 웹 콘솔을 엽니다. URL은 https://&#39;[server]:[port]&#39;/system/console/configMgr입니다.
1. **Adobe LiveCycle Client SDK** 번들을 찾아 엽니다. 다음 속성에 대한 값을 지정합니다.

   * **서버 URL**: JEE 서버에서 AEM Forms의 HTTPS URL을 지정하십시오. https를 통해 통신하려면 -Djavax.net.ssl.trustStore=&lt;JEE 키 저장소 파일의 AEM Forms 경로> 매개 변수를 사용하여 AEM 서버를 다시 시작합니다.
   * **양방향 SSL 사용**: 양방향 SSL 사용 옵션을 사용합니다.
   * **KeyStore 파일 URL**: 키 저장소 파일의 URL을 지정하십시오.
   * **TrustStore 파일 URL**: Truststore 파일의 URL을 지정하십시오.
   * **KeyStore 암호**: 키 저장소 파일의 암호를 지정하십시오.
   * **TrustStorePassword**: truststore 파일의 암호를 지정하십시오.
   * **서비스 이름**: 지정된 서비스 목록에 RightsManagementService를 추가합니다.

   **저장**&#x200B;을 클릭합니다. AEM은 문서 보안으로 보호된 PDF 문서를 검색할 수 있도록 활성화됩니다

### 정책으로 보호된 샘플 PDF 문서 색인화 {#index-a-sample-policy-protected-pdf-document}

1. 관리자로 AEM Assets에 로그인합니다.
1. AEM Digital Asset Manager에서 폴더를 만들고 정책으로 보호된 PDF 문서를 새로 만든 폴더에 업로드합니다.

   이제 AEM 검색을 사용하여 정책으로 보호된 문서를 검색할 수 있습니다.

   >[!NOTE]
   >
   > SDK을 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK을 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.
