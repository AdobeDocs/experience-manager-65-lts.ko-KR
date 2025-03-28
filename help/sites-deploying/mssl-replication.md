---
title: 상호 SSL을 사용하여 복제
description: 작성자 인스턴스의 복제 에이전트가 MSSL(상호 SSL)을 사용하여 게시 인스턴스와 연결하도록 AEM을 구성하는 방법에 대해 알아봅니다. 게시 인스턴스에서 MSSL을 사용하는 복제 에이전트와 HTTP 서비스는 인증서를 사용하여 서로 인증합니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
hide: true
hidefromtoc: true
exl-id: f5944c6e-bf6f-490e-a8b1-3a01b76d32c0
source-git-commit: f145e5f0d70662aa2cbe6c8c09795ba112e896ea
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 4%

---

# 상호 SSL을 사용하여 복제{#replicating-using-mutual-ssl}

작성자 인스턴스의 복제 에이전트가 MSSL(상호 SSL)을 사용하여 게시 인스턴스와 연결하도록 AEM을 구성합니다. 게시 인스턴스에서 MSSL을 사용하는 복제 에이전트와 HTTP 서비스는 인증서를 사용하여 서로 인증합니다.

복제를 위한 MSSL 구성에는 다음 단계 수행이 포함됩니다.

1. 작성자 및 게시 인스턴스에 대한 개인 키 및 인증서를 만들거나 가져옵니다.
1. 작성자 및 게시 인스턴스에 키 및 인증서를 설치합니다.

   * 작성자: 작성자의 개인 키 및 게시의 인증서.
   * 게시: 게시의 개인 키 및 작성자의 인증서. 인증서는 복제 에이전트로 인증된 사용자 계정과 연결됩니다.

1. 게시 인스턴스에서 Jetty 기반 HTTP 서비스를 구성합니다.
1. 복제 에이전트의 전송 및 SSL 속성을 구성합니다.

![chlimage_1-64](assets/chlimage_1-64.png)

복제를 수행하는 사용자 계정을 확인합니다. 게시 인스턴스에 신뢰할 수 있는 작성자 인증서를 설치할 때 인증서가 이 사용자 계정에 연결됩니다.

## MSSL에 대한 자격 증명 가져오기 또는 만들기 {#obtaining-or-creating-credentials-for-mssl}

작성자 및 게시 인스턴스에 대해 개인 키 및 공개 인증서가 필요합니다.

* 개인 키는 pkcs#12 또는 JKS 형식으로 포함해야 합니다.
* 인증서는 pkcs#12 또는 JKS 형식이어야 합니다. &quot;CER&quot; 형식에 포함된 인증서를 Granite Truststore에 추가할 수도 있습니다.
* 인증서는 자체 서명하거나 인증된 CA에 의해 서명될 수 있습니다.

### JKS 형식 {#jks-format}

JKS 형식의 개인 키 및 인증서를 생성합니다. 개인 키는 KeyStore 파일에 저장되고 인증서는 TrustStore 파일에 저장됩니다. [Java `keytool`](https://docs.oracle.com/javase/7/docs/technotes/tools/solaris/keytool.html)을(를) 사용하여 둘 다 만드십시오.

Java `keytool`을(를) 사용하여 개인 키 및 자격 증명을 만들려면 다음 단계를 수행하십시오.

1. KeyStore에서 개인-공개 키 쌍을 생성합니다.
1. 인증서를 만들거나 가져옵니다.

   * 자체 서명됨: KeyStore에서 인증서를 내보냅니다.
   * CA 서명: 인증서 요청을 생성하여 CA로 보냅니다.

1. 인증서를 TrustStore로 가져옵니다.

다음 절차를 사용하여 작성자 및 게시 인스턴스 모두에 대한 개인 키 및 자체 서명된 인증서를 만듭니다. 그에 따라 명령 옵션에 다른 값을 사용합니다.

1. 명령줄 창이나 터미널을 엽니다. 개인-공개 키 쌍을 만들려면 아래 표의 옵션 값을 사용하여 다음 명령을 입력합니다.

   ```shell
   keytool -genkeypair -keyalg RSA -validity 3650 -alias alias -keystore keystorename.keystore  -keypass key_password -storepass  store_password -dname "CN=Host Name, OU=Group Name, O=Company Name,L=City Name, S=State, C=Country_ Code"
   ```

   | 옵션 | 작성 | 게시 |
   |---|---|---|
   | -alias | 작성자 | 게시 |
   | -keystore | author.keystore | publish.keystore |

1. 인증서를 내보내려면 아래 표의 옵션 값을 사용하여 다음 명령을 입력합니다.

   ```shell
   keytool -exportcert -alias alias -file cert_file -storetype jks -keystore keystore -storepass store_password
   ```

   | 옵션 | 작성 | 게시 |
   |---|---|---|
   | -alias | 작성자 | 게시 |
   | -file | author.cer | publish.cer |
   | -keystore | author.keystore | publish.keystore |

### pkcs#12 형식 {#pkcs-format}

pkcs#12 형식의 개인 키와 인증서를 생성합니다. [openSSL](https://www.openssl.org/)을 사용하여 생성합니다. 다음 절차를 사용하여 개인 키 및 인증서 요청을 생성합니다. 인증서를 받으려면 개인 키(자체 서명된 인증서)로 요청에 서명하거나 요청을 CA로 보냅니다. 그런 다음 개인 키와 인증서가 포함된 pkcs#12 아카이브를 생성합니다.

1. 명령줄 창이나 터미널을 엽니다. 개인 키를 만들려면 아래 표의 옵션 값을 사용하여 다음 명령을 입력합니다.

   ```shell
   openssl genrsa -out keyname.key 2048
   ```

   | 옵션 | 작성 | 게시 |
   |---|---|---|
   | -out | author.key | publish.key |

1. 인증서 요청을 생성하려면 아래 표의 옵션 값을 사용하여 다음 명령을 입력합니다.

   ```shell
   openssl req -new -key keyname.key -out key_request.csr
   ```

   | 옵션 | 작성 | 게시 |
   |---|---|---|
   | -key | author.key | publish.key |
   | -out | author_request.csr | publish_request.csr |

   인증서 요청에 서명하거나 요청을 CA에 보냅니다.

1. 인증서 요청에 서명하려면 아래 표의 옵션 값을 사용하여 다음 명령을 입력합니다.

   ```shell
   openssl x509 -req -days 3650 -in key_request.csr -signkey keyname.key -out certificate.cer
   ```

   | 옵션 | 작성 | 게시 |
   |---|---|---|
   | -signkey | author.key | publish.key |
   | -in | author_request.csr | publish_request.csr |
   | -out | author.cer | publish.cer |

1. 개인 키와 서명된 인증서를 pkcs#12 파일에 추가하려면 아래 표의 옵션 값을 사용하여 다음 명령을 입력합니다.

   ```shell
   openssl pkcs12 -keypbe PBE-SHA1-3DES -certpbe PBE-SHA1-3DES -export -in certificate.cer -inkey keyname.key -out pkcs12_archive.pfx -name "alias"
   ```

   | 옵션 | 작성 | 게시 |
   |---|---|---|
   | -inkey | author.key | publish.key |
   | -out | author.pfx | publish.pfx |
   | -in | author.cer | publish.cer |
   | -name | 작성자 | 게시 |

## 작성자에 개인 키 및 TrustStore 설치 {#install-the-private-key-and-truststore-on-author}

작성자 인스턴스에 다음 항목을 설치합니다.

* 작성자 인스턴스의 개인 키.
* 게시 인스턴스의 인증서.

다음 절차를 수행하려면 작성자 인스턴스의 관리자로 로그인해야 합니다.

### 작성자 개인 키 설치 {#install-the-author-private-key}

1. 작성자 인스턴스의 사용자 관리 페이지를 엽니다. ([http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html))
1. 사용자 계정의 속성을 열려면 사용자 이름을 클릭합니다.
1. 계정 설정 영역에 KeyStore 만들기 링크가 나타나면 링크를 클릭합니다. 암호를 구성하고 [확인]을 클릭합니다.
1. 계정 설정 영역에서 키 저장소 관리를 클릭합니다.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 키 저장소 파일에서 개인 키 추가를 클릭합니다.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 키 저장소 파일 선택을 클릭한 다음 pkcs#12를 사용하는 경우 author.keystore 파일 또는 author.pfx 파일을 찾아 선택한 다음 열기를 클릭합니다.
1. 키 저장소에 대한 별칭 및 암호를 입력합니다. 개인 키에 대한 별칭 및 암호를 입력한 다음 제출을 누릅니다.
1. KeyStore 관리 대화 상자를 닫습니다.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 게시 인증서 설치 {#install-the-publish-certificate}

1. 작성자 인스턴스의 사용자 관리 페이지를 엽니다. ([http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html))
1. 사용자 계정의 속성을 열려면 사용자 이름을 클릭합니다.
1. [계정 설정] 영역에 [TrustStore 생성] 링크가 나타나면 링크를 클릭하고 TrustStore에 대한 암호를 만든 다음 [확인]을 클릭합니다.
1. 계정 설정 영역에서 TrustStore 관리를 클릭합니다.
1. CER 파일에서 인증서 추가를 클릭합니다.

   ![chlimage_1-68](assets/chlimage_1-68.png)

1. 사용자에 인증서 매핑 옵션을 지웁니다. 인증서 파일 선택 을 클릭하고 publish.cer를 선택한 다음 열기 를 클릭합니다.
1. TrustStore 관리 대화 상자를 닫습니다.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 게시할 때 개인 키 및 TrustStore 설치 {#install-private-key-and-truststore-on-publish}

게시 인스턴스에 다음 항목을 설치합니다.

* 게시 인스턴스의 개인 키.
* 작성자 인스턴스의 인증서. 인증서를 복제 요청을 실행하는 데 사용되는 사용자와 연결합니다.

다음 절차를 수행하려면 게시 인스턴스의 관리자로 로그인해야 합니다.

### Publish 개인 키 설치 {#install-the-publish-private-key}

1. 게시 인스턴스에 대한 [사용자 관리] 페이지를 엽니다. ([http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html))
1. 사용자 계정의 속성을 열려면 사용자 이름을 클릭합니다.
1. 계정 설정 영역에 KeyStore 만들기 링크가 나타나면 링크를 클릭합니다. 암호를 구성하고 [확인]을 클릭합니다.
1. 계정 설정 영역에서 키 저장소 관리를 클릭합니다.
1. 키 저장소 파일에서 개인 키 추가를 클릭합니다.
1. 키 저장소 파일 선택을 클릭한 다음 pkcs#12를 사용하는 경우 publish.keystore 파일 또는 publish.pfx 파일을 찾아 선택한 다음 열기를 클릭합니다.
1. 키 저장소에 대한 별칭 및 암호를 입력합니다. 개인 키에 대한 별칭 및 암호를 입력한 다음 제출을 누릅니다.
1. KeyStore 관리 대화 상자를 닫습니다.

### 작성자 인증서 설치 {#install-the-author-certificate}

1. 게시 인스턴스에 대한 [사용자 관리] 페이지를 엽니다. ([http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html))
1. Create TrustStore 링크가 글로벌 Trust Store 영역에 나타나면 링크를 클릭하고 TrustStore에 대한 암호를 만든 다음 확인을 클릭합니다.
1. 계정 설정 영역에서 TrustStore 관리를 클릭합니다.
1. CER 파일에서 인증서 추가를 클릭합니다.
1. 인증서를 사용자에게 매핑 옵션이 선택되어 있는지 확인합니다. 인증서 파일 선택 을 클릭하고 author.cer 를 선택한 다음 열기 를 클릭합니다.
1. 제출을 클릭한 다음 TrustStore 관리 대화 상자를 닫습니다.

## 게시할 때 HTTP 서비스 구성 {#configure-the-http-service-on-publish}

Granite 키 저장소에 액세스하는 동안 HTTPS를 사용하도록 게시 인스턴스에서 Apache Felix Jetty 기반 HTTP 서비스의 속성을 구성합니다. 서비스의 PID는 `org.apache.felix.http`입니다.

다음 표에는 웹 콘솔 사용 여부를 구성하는 데 필요한 OSGi 속성이 나열되어 있습니다.

| 웹 콘솔의 속성 이름 | OSGi 속성 이름 | 값 |
|---|---|---|
| HTTPS 활성화 | org.apache.felix.https.enable | true |
| Granite KeyStore를 사용하려면 HTTPS 활성화 | org.apache.felix.https.use.granite.keystore | true |
| HTTPS 포트 | org.osgi.service.http.port.secure | 8443(또는 기타 원하는 포트) |
| 클라이언트 인증서 | org.apache.felix.https.clientcertificate | &quot;클라이언트 인증서 필요&quot; |

## 작성자의 복제 에이전트 구성 {#configure-the-replication-agent-on-author}

게시 인스턴스에 연결할 때 HTTPS 프로토콜을 사용하도록 작성자 인스턴스에서 복제 에이전트를 구성합니다. 복제 에이전트 구성에 대한 자세한 내용은 [복제 에이전트 구성](/help/sites-deploying/replication.md#configuring-your-replication-agents)을 참조하십시오.

MSSL을 활성화하려면 다음 표에 따라 전송 탭에서 속성을 구성합니다.

<table>
 <tbody>
  <tr>
   <th>속성</th>
   <th>값</th>
  </tr>
  <tr>
   <td>URI</td>
   <td><p>https://server_name:SSL_port/bin/receive?sling:authRequestLogin=1</p> <p>예:</p> <p>http://localhost:8443/bin/receive?sling:authRequestLogin=1</p> </td>
  </tr>
  <tr>
   <td>사용자</td>
   <td>값 없음</td>
  </tr>
  <tr>
   <td>암호</td>
   <td>값 없음</td>
  </tr>
  <tr>
   <td>SSL</td>
   <td>클라이언트 인증</td>
  </tr>
 </tbody>
</table>

![chlimage_1-70](assets/chlimage_1-70.png)

복제 에이전트를 구성한 후 연결을 테스트하여 MSSL이 올바르게 구성되었는지 확인합니다.

```xml
29.08.2014 14:02:46 - Create new HttpClient for Default Agent
29.08.2014 14:02:46 - * HTTP Version: 1.1
29.08.2014 14:02:46 - * Using Client Auth SSL configuration *
29.08.2014 14:02:46 - adding header: Action:Test
29.08.2014 14:02:46 - adding header: Path:/content
29.08.2014 14:02:46 - adding header: Handle:/content
29.08.2014 14:02:46 - deserialize content for delivery
29.08.2014 14:02:46 - No message body: Content ReplicationContent.VOID is empty
29.08.2014 14:02:46 - Sending POST request to http://localhost:8443/bin/receive?sling:authRequestLogin=1
29.08.2014 14:02:46 - sent. Response: 200 OK
29.08.2014 14:02:46 - ------------------------------------------------
29.08.2014 14:02:46 - Sending message to localhost:8443
29.08.2014 14:02:46 - >> POST /bin/receive HTTP/1.0
29.08.2014 14:02:46 - >> Action: Test
29.08.2014 14:02:46 - >> Path: /content
29.08.2014 14:02:46 - >> Handle: /content
29.08.2014 14:02:46 - >> Referer: about:blank
29.08.2014 14:02:46 - >> Content-Length: 0
29.08.2014 14:02:46 - >> Content-Type: application/octet-stream
29.08.2014 14:02:46 - --
29.08.2014 14:02:46 - << HTTP/1.1 200 OK
29.08.2014 14:02:46 - << Connection: Keep-Alive
29.08.2014 14:02:46 - << Server: Day-Servlet-Engine/4.1.64
29.08.2014 14:02:46 - << Content-Type: text/plain;charset=utf-8
29.08.2014 14:02:46 - << Content-Length: 26
29.08.2014 14:02:46 - << Date: Fri, 29 Aug 2014 18:02:46 GMT
29.08.2014 14:02:46 - << Set-Cookie: login-token=3529326c-1500-4888-a4a3-93d299726f28%3ac8be86c6-04bb-4d18-80d6-91278e08d720_98797d969258a669%3acrx.default; Path=/; HttpOnly; Secure
29.08.2014 14:02:46 - << Set-Cookie: cq-authoring-mode=CLASSIC; Path=/; Secure
29.08.2014 14:02:46 - <<
29.08.2014 14:02:46 - << R
29.08.2014 14:02:46 - << eplicationAction TEST ok.
29.08.2014 14:02:46 - Message sent.
29.08.2014 14:02:46 - ------------------------------------------------
29.08.2014 14:02:46 - Replication (TEST) of /content successful.
Replication test succeeded
```
