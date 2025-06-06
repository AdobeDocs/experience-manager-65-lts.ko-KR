---
title: JBoss 애플리케이션 서버에 대한 SSL 구성
description: JBoss 애플리케이션 서버용 SSL을 구성하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 65e1df03-8549-4ebb-bd86-7666a19339ed
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# JBoss 애플리케이션 서버에 대한 SSL 구성 {#configuring-ssl-for-jboss-application-server}

JBoss 애플리케이션 서버에서 SSL을 구성하려면 인증을 위한 SSL 자격 증명이 필요합니다. Java 키 도구를 사용하여 자격 증명을 만들거나 CA(인증 기관)에서 자격 증명을 요청하고 가져올 수 있습니다. 그런 다음 JBoss에서 SSL을 활성화해야 합니다.

키 저장소를 만드는 데 필요한 모든 정보를 포함하는 단일 명령을 사용하여 키 도구를 실행할 수 있습니다.

이 절차에서는

* `[appserver root]`은(는) AEM forms를 실행하는 응용 프로그램 서버의 홈 디렉터리입니다.
* `[type]`은(는) 수행한 설치 유형에 따라 달라지는 폴더 이름입니다.

## SSL 자격 증명 만들기 {#create-an-ssl-credential}

1. 명령 프롬프트에서 *[JAVA HOME]*/bin으로 이동하고 다음 명령을 입력하여 자격 증명 및 키 저장소를 만듭니다.

   `keytool -genkey -dname "CN=`*호스트 이름* `, OU=`*그룹 이름* `, O=`*회사 이름* `,L=`*도시 이름* `, S=`*상태* `, C=`국가 코드&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*키_암호* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >`[JAVA_HOME]`을(를) JDK가 설치된 디렉터리로 바꾸고 텍스트를 사용자 환경에 해당하는 값으로 기울임꼴로 바꿉니다. 호스트 이름 은 애플리케이션 서버의 정규화된 도메인 이름입니다.

1. 암호를 입력하라는 메시지가 표시되면 `keystore_password`을(를) 입력하십시오. 키 저장소의 암호와 키의 암호는 동일해야 합니다.

   >[!NOTE]
   >
   >이 단계에서 입력한 `keystore_password` *은(는) 1단계에서 입력한 암호(key_password)와 동일하거나 다를 수 있습니다.*

1. 다음 명령 중 하나를 입력하여 *keystorename*.keystore를 `[appserver root]/server/[type]/conf` 디렉터리에 복사합니다.

   * (Windows 단일 서버) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * (Windows Server 클러스터) 복사본 `keystorename.keystore[appserver root]\domain\configuration`
   * (Linux 단일 서버) `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (Linux 서버 클러스터) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 다음 명령을 입력하여 인증서 파일을 내보냅니다.

   * (단일 서버) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * (서버 클러스터) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. 암호를 입력하라는 메시지가 표시되면 *keystore_password*&#x200B;를 입력하십시오.
1. 다음 명령을 입력하여 AEMForms_cert.cer 파일을 *[appserver root] \conf* 디렉터리에 복사합니다.

   * (Windows 단일 서버) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * (Windows Server 클러스터) `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * (Linux 단일 서버) `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (Linux 서버 클러스터) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 다음 명령을 입력하여 인증서의 내용을 봅니다.

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. 필요한 경우 `[JAVA_HOME]\jre\lib\security`의 cacerts 파일에 쓰기 액세스 권한을 부여하려면 다음 작업을 수행하십시오.

   * (Windows) cacerts 파일을 마우스 오른쪽 단추로 클릭하고 [속성]을 선택한 다음 [읽기 전용] 속성의 선택을 해제합니다.
   * (Linux) 유형 `chmod 777 cacerts`

1. 다음 명령을 입력하여 인증서를 가져옵니다.

   `keytool -import -alias "AEMForms Cert" -file`*AEMForms_cert* `.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. 암호로 `changeit`을(를) 입력하십시오. 이 암호는 Java 설치의 기본 암호이며 시스템 관리자가 변경했을 수 있습니다.
1. `Trust this certificate? [no]`을(를) 입력하라는 메시지가 표시되면 `yes`을(를) 입력하십시오. &quot;인증서가 키 저장소에 추가됨&quot; 확인이 표시됩니다.
1. Workbench에서 SSL을 통해 연결하는 경우 Workbench 컴퓨터에 인증서를 설치합니다.
1. 텍스트 편집기에서 편집할 다음 파일을 엽니다.

   * 단일 서버 - `[appserver root]`/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * 서버 클러스터 - `[appserver root]`/domain/configuration/host.xml

   * 서버 클러스터 - `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. &#x200B;
   * **단일 서버의 경우** lc_&lt;dbaname/tunkey>.xml 파일의 &lt;security-realms> 섹션 뒤에 다음을 추가하십시오.

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   다음 코드 뒤에 있는 `<server>` 섹션을 찾습니다.

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   위의 코드 뒤에 있는 &lt;server> 섹션에 다음을 추가하십시오.

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **모든 노드의 [appserver 루트]\domain\configuration\host.xml에 있는** 서버 클러스터의 경우 &lt;security-realms> 섹션 뒤에 다음을 추가하십시오.

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   서버 클러스터의 주 노드에서 [appserver root]\domain\configuration\domain_&lt;dbname>.xml의 다음 코드 뒤에 있는 &lt;server> 섹션을 찾습니다.

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   위의 코드 뒤에 있는 &lt;server> 섹션에 다음을 추가하십시오.

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. 키 저장소를 만들 때 지정한 키 저장소 암호로 `keystoreFile` 특성 및 `keystorePass` 특성의 값을 변경합니다.
1. 응용 프로그램 서버를 다시 시작합니다.

   * 턴키 설치의 경우:

      * Windows Campaign 컨트롤 패널에서 관리 도구를 클릭한 다음 서비스를 클릭합니다.
      * Adobe Experience Manager 양식에 대한 JBoss를 선택합니다.
      * [작업] > [중지]를 선택합니다.
      * 서비스 상태가 중지됨으로 나타날 때까지 기다립니다.
      * 작업 > 시작을 선택합니다.

   * 사전 구성되거나 수동으로 구성된 Adobe의 경우 JBoss 설치:

      * 명령 프롬프트에서 *`[appserver root]`*/bin으로 이동합니다.
      * 다음 명령을 입력하여 서버를 중지합니다.

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`

      * JBoss 프로세스가 완전히 종료될 때까지 기다립니다(JBoss 프로세스가 시작되었던 터미널에 제어를 반환할 때).
      * 다음 명령을 입력하여 서버를 시작합니다.

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`

1. SSL을 사용하여 관리 콘솔에 액세스하려면 웹 브라우저에 `https://[host name]:'port'/adminui`을(를) 입력하십시오.

   JBoss의 기본 SSL 포트는 8443입니다. 이제부터 AEM Forms에 액세스할 때 이 포트를 지정합니다.

## CA에서 자격 증명 요청 {#request-a-credential-from-a-ca}

1. 명령 프롬프트에서 *[JAVA HOME]*/bin으로 이동하고 다음 명령을 입력하여 키 저장소와 키를 만듭니다.

   `keytool -genkey -dname "CN=`*호스트 이름* `, OU=`*그룹 이름* `, O=`*회사 이름* `, L=`*도시 이름* `, S=`*상태* `, C=`*국가 코드*&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >*`[JAVA_HOME]`*&#x200B;을(를) JDK가 설치된 디렉터리로 바꾸고 텍스트를 사용자 환경에 해당하는 값으로 기울임꼴로 바꿉니다.

1. 다음 명령을 입력하여 인증 기관에 전송할 인증서 요청을 생성합니다.

   `keytool -certreq -alias` &quot;AEMForms 인증서&quot; `-keystore`*keystorename* `.keystore -file`*AEMFormscertRequest.csr*

1. 인증서 파일에 대한 요청이 이행되면 다음 절차를 완료합니다.

## CA에서 얻은 자격 증명을 사용하여 SSL 활성화 {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. 명령 프롬프트에서 *`[JAVA HOME]`*/bin으로 이동하고 다음 명령을 입력하여 CSR이 서명된 CA의 루트 인증서를 가져옵니다.

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   루트 인증서가 브라우저에 없으면 브라우저에서 가져오기하십시오.

   >[!NOTE]
   >
   >*`[JAVA_HOME]`을(를) JDK가 설치된 디렉터리로 바꾸고 텍스트를 사용자 환경에 해당하는 값으로 기울임꼴로 바꿉니다.*

1. 명령 프롬프트에서 *`[JAVA HOME]`*/bin으로 이동하고 다음 명령을 입력하여 키 저장소로 자격 증명을 가져옵니다.

   `keytool -import -trustcacerts -file`*CACertificateName* `.crt -keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >* `[JAVA_HOME]`을(를) JDK가 설치된 디렉터리로 바꾸고 텍스트를 사용자 환경에 해당하는 값으로 기울임꼴로 바꿉니다.
   >* 가져온 CA 서명 인증서가 있으면 자체 서명된 공개 인증서를 대체합니다.

1. SSL 자격 증명 만들기의 13~18단계를 완료합니다.
