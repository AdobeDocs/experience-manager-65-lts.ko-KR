---
title: JBoss 애플리케이션 서버(AEM 6.5 LTS JEE)용 SSL 구성
description: JBoss Application Server에 대한 SSL을 구성하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 86d6d0f7b6fe1c36349f29e45a3eee31b04e5e80
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---


# JBoss 애플리케이션 서버(AEM 6.5 LTS JEE)용 SSL 구성

## 개요

Java EE에서 실행되는 Adobe Experience Manager(AEM) 6.5 LTS용 JBoss 애플리케이션 서버에서 SSL을 구성하려면 보안 HTTPS 통신을 활성화해야 합니다. SSL을 활성화하면 클라이언트와 서버 간에 교환되는 데이터를 암호화하므로 프로덕션 AEM Forms 배포에 중요한 보안 요구 사항이 됩니다.

이 프로세스에는 두 가지 주요 단계가 포함됩니다.

- **SSL 자격 증명을 얻는 중** — 자체 서명된 인증서를 생성하거나 CA(인증 기관)에 인증서를 요청하여 얻을 수 있습니다.
- **JBoss에서 SSL 활성화** — JBoss CLI 명령을 통해 Elytron 하위 시스템 사용.

이 안내서 전체에서 다음 자리 표시자 값이 사용됩니다.

- `[appserver root]` - AEM Forms을 실행하는 JBoss 애플리케이션 서버의 홈 디렉터리입니다.
- `[type]` — 수행된 설치 유형에 따라 달라지는 폴더 이름입니다.
- `[JAVA_HOME]` — JDK가 설치된 디렉터리입니다.

## 1부: SSL 자격 증명(자체 서명) 만들기

CA의 인증서가 없으면 Java `keytool` 유틸리티를 사용하여 자체 서명된 SSL 자격 증명을 생성할 수 있습니다. 개발 또는 테스트 환경에 적합합니다.

### 1단계 — 키 저장소 생성

명령 프롬프트에서 `[JAVA_HOME]/bin`(으)로 이동하고 다음 명령을 실행하여 값을 환경에 적합한 값으로 바꿉니다. 호스트 이름은 응용 프로그램 서버의 FQDN(정규화된 도메인 이름)이어야 합니다.

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

메시지가 표시되면 `keystore_password`을(를) 입력합니다. 키 저장소의 암호와 키의 암호는 동일해야 합니다.

### 2단계 — 구성 디렉토리에 키 저장소 복사

생성된 키 저장소를 설치 유형에 적합한 구성 폴더에 복사합니다.

```bash
# Windows Single Server
copy keystorename.keystore [appserver root]\standalone\configuration

# Windows Server Cluster
copy keystorename.keystore [appserver root]\domain\configuration

# Linux Single Server
cp keystorename.keystore [appserver root]/standalone/configuration

# Linux Server Cluster
cp keystorename.keystore [appserver root]/domain/configuration
```

### 3단계 — 인증서 파일 내보내기

다음 명령 중 하나를 사용하여 키 저장소에서 인증서를 내보냅니다.

```bash
# Single Server
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/standalone/configuration/keystorename.keystore

# Server Cluster
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/domain/configuration/keystorename.keystore
```

메시지가 표시되면 `keystore_password`을(를) 입력합니다.

### 4단계 — 인증서 복사 및 확인

구성 디렉터리에 `AEMForms_cert.cer`을(를) 복사한 다음 내용을 확인합니다.

```bash
# Copy (Linux Single Server example)
cp AEMForms_cert.cer [appserver root]/standalone/configuration

# Verify certificate contents (Single Server)
keytool -printcert -v -file [appserver root]/standalone/configuration/AEMForms_cert.cer

# Verify certificate contents (Server Cluster)
keytool -printcert -v -file [appserver root]/domain/configuration/AEMForms_cert.cer
```

### 5단계 — 인증서를 Java Truststore로 가져오기

가져오기 전에 `cacerts` 파일에 쓸 수 있는지 확인하십시오.

```bash
# Windows: Right-click cacerts → Properties → deselect Read-only

# Linux:
chmod 777 [JAVA_HOME]/jre/lib/security/cacerts
```

그런 다음 인증서를 가져옵니다:

```bash
keytool -import -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [JAVA_HOME]/jre/lib/security/cacerts
```

암호를 입력하라는 메시지가 표시되면 `changeit`(기본 Java Truststore 암호 — 변경된 경우 관리자에게 확인)을 입력합니다. **이 인증서를 신뢰하라는 메시지가 표시되면 [아니요]**, 유형 `yes`. 확인 메시지가 표시됩니다. *&quot;인증서가 키 저장소에 추가되었습니다.&quot;*

>[!NOTE]
>
> Workbench에서 SSL을 통해 AEM Forms에 연결하는 경우 Workbench 컴퓨터에도 인증서를 설치해야 합니다.

## 2부: Elytron 하위 시스템을 사용하여 JBoss에서 SSL 활성화

이제 SSL 자격 증명을 통해 JBoss CLI를 통해 Elytron 보안 하위 시스템을 사용하여 JBoss에서 HTTPS를 활성화할 수 있습니다. 계속하기 전에 키 저장소 파일이 적절한 구성 디렉토리에 있는지 확인합니다.

>[!NOTE]
>
> Windows에서는 각 CLI 명령을 줄바꿈 없이 한 줄로 입력해야 합니다. `keystorename.keystore`을(를) 실제 파일 이름으로 바꾸고 `changeit`을(를) 키 저장소/키 암호로 바꿉니다.

### 6a단계 — Elytron Key-Store 만들기

```bash
/subsystem=elytron/key-store=aemKeyStore:add(
  path="keystorename.keystore",
  relative-to=jboss.server.config.dir,
  type="JKS",
  credential-reference={clear-text="changeit"})
```

키 저장소에서 해당 형식을 사용하는 경우 `JKS`을(를) `PKCS12`(으)로 바꿉니다.

### 6b 단계 — Elytron 키 관리자 만들기

```bash
/subsystem=elytron/key-manager=aemKeyManager:add(
  key-store=aemKeyStore,
  credential-reference={clear-text="changeit"})
```

키 저장소에 인증서 항목이 여러 개 있는 경우 명시적으로 별칭을 지정하십시오.

```bash
/subsystem=elytron/key-manager=aemKeyManager:add(
  key-store=aemKeyStore,
  alias="AEMForms Cert",
  credential-reference={clear-text="changeit"})
```

### 6c 단계 — 서버 SSL 컨텍스트 업데이트

```bash
/subsystem=elytron/server-ssl-context=applicationSSC:write-attribute(
  name=key-manager,
  value=aemKeyManager)
```

### 6d 단계 — Undertow HTTPS 수신기 구성

HTTPS 리스너를 활성화하려면 SSL 컨텍스트를 Undertow(JBoss 웹 서버)로 전송하십시오.

```bash
/subsystem=undertow/server=default-server/https-listener=https:add(
  socket-binding=https,
  ssl-context=applicationSSC)
```

## 3부: 응용 프로그램 서버 재시작

Elytron 구성을 완료한 후 JBoss를 재시작하여 변경 사항을 적용합니다.

### 턴키 설치(Windows 서비스)

- **Campaign 컨트롤 패널 > 관리 도구 > 서비스**&#x200B;를 엽니다.
- **Adobe Experience Manager 양식에 대한 JBoss**&#x200B;을(를) 선택합니다.
- **작업 > 중지**&#x200B;를 선택하고 서비스가 중지될 때까지 기다립니다.
- **작업 > 시작**&#x200B;을 선택합니다.

### 사전 구성 또는 수동 JBoss 설치

명령 프롬프트에서 `[appserver root]/bin`(으)로 이동합니다.

```bash
# Stop the server
Windows: shutdown.bat -S
Linux:   ./shutdown.sh -S

# Wait until JBoss fully shuts down, then start the server
Windows: run.bat -c <profile>
Linux:   ./run.sh -c <profile>
```

## 4부: 인증 기관에 자격 증명 요청

프로덕션 환경의 경우 신뢰할 수 있는 CA(인증 기관)에서 발급한 인증서를 사용해야 합니다. 프로세스에는 키 쌍을 생성하고 CSR(인증서 서명 요청)을 생성한 다음 CA 서명 인증서를 가져오는 작업이 포함됩니다.

### 키 저장소 생성 및 CSR 만들기

`[JAVA_HOME]/bin`(으)로 이동하여 키 저장소 생성:

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

그런 다음 CSR을 생성하여 CA에 제출합니다.

```bash
keytool -certreq -alias "AEMForms Cert" \
  -keystore keystorename.keystore \
  -file AEMFormscertRequest.csr
```

CA에 `.csr` 파일을 제출합니다. 서명된 인증서를 다시 받으면 아래 단계를 따르십시오.

### CA 서명 인증서 가져오기

먼저 CA 루트 인증서를 가져옵니다.

```bash
keytool -import -trustcacerts -file rootcert.pem \
  -keystore keystorename.keystore -alias root
```

브라우저가 루트 인증서를 아직 신뢰하지 않는 경우 루트 인증서를 브라우저에서 가져오십시오. 그런 다음 CA 서명 인증서를 가져옵니다.

```bash
keytool -import -trustcacerts -file CACertificateName.crt \
  -keystore keystorename.keystore
```

>[!NOTE]
>
> 가져온 CA 서명 인증서는 자체 서명된 기존 공개 인증서가 키 저장소에 있는 경우 이 인증서를 대체합니다.

CA 인증서를 가져온 후에는 2부(Elytron 구성)에서 **6a-6d**&#x200B;단계를 진행하고 서버를 다시 시작한 후(3부) SSL 액세스를 확인합니다.

## SSL 액세스 확인

서버를 다시 시작한 후 HTTPS를 통해 AEM Forms 관리 콘솔에 액세스하여 SSL이 올바르게 작동하는지 확인합니다. JBoss의 기본 SSL 포트는 `8443`입니다.

```
https://[host name]:8443/adminui
```

관리 콘솔이 HTTPS를 통해 성공적으로 로드되면 SSL이 올바르게 구성되었습니다. AEM Forms에 대한 모든 후속 SSL 연결에 `8443` 포트를 사용합니다.
