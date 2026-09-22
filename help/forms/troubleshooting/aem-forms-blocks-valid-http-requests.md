---
title: AEM Forms이 유효한 HTTP 요청을 차단합니다.
description: AEM Forms XSS 유효성 검사는 사용자 지정 구성 요소를 사용하는 고객에 대한 유효한 HTTP 요청을 차단할 수 있습니다. 문제를 식별하고 유효성 검사를 일시적으로 완화하는 방법을 알아봅니다.
solution: Experience Manager, Experience Manager Forms
feature: Security
role: Admin,Developer
exl-id: 10a02e57-7ff8-42d8-b31e-f714c0dd8338
source-git-commit: 4df5a9888532afd86562678a76c35841ac5634b8
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 2%
---
# AEM Forms이 유효한 HTTP 요청을 차단합니다. {#aem-forms-blocks-valid-http-requests}

## 문제 {#issue}

AEM Forms에는 XSS(크로스 사이트 스크립팅) 공격을 방지하기 위한 보안 검사가 포함되어 있습니다. 이러한 검사는 AEM Forms에서 사용자 지정 구성 요소를 사용하는 고객에 대한 일부 유효한 HTTP 요청을 차단할 수 있습니다. 요청이 차단되면 서버 로그에 다음 메시지가 표시됩니다.

```text
Got Exception while Validating XSS: HTTP parameter name: params[browserLocale]: Invalid input. Please conform to regex ^[a-zA-Z0-9_]{1,32}$ with a maximum length of 2000: org.owasp.esapi.errors.ValidationException: HTTP parameter name: params[browserLocale]: Invalid input. Please conform to regex ^[a-zA-Z0-9_]{1,32}$ with a maximum length of 2000.
```

>[!NOTE]
>
>POST 요청의 경우 매개 변수의 기본값은 **1048576**&#x200B;입니다. GET 요청의 경우 매개 변수의 기본값은 **2000**&#x200B;입니다. POST 요청의 매개 변수 값을 수정하려면 서버를 시작하는 동안 `com.adobe.idp.dsc.provider.rest.httpParamMaxSize` 인수를 전달합니다.

## 원인 {#cause}

XSS 유효성 검사 regex는 사용자 지정 구성 요소에서 보낸 매개 변수 값의 형식보다 엄격하므로 AEM Forms은 요청을 거부합니다.

## 해결 방법 {#resolution}

>[!CAUTION]
>
>보안 검사를 제거하면 시스템이 XSS(크로스 사이트 스크립팅) 공격에 취약해집니다. 임시 해결 방법으로만 보안 검사를 제거하십시오.

보안 검사를 일시적으로 제거하고 모든 HTTP 요청을 허용하려면 다음을 수행하십시오.

1. AEM Forms 서버를 중지합니다.

1. `[AEM-Forms-Installation-Directory]/configurationManager/export/adobe-livecycle-<application_server_name>.ear` 파일의 백업을 만듭니다.

1. `adobe-livecycle-<server_name>.ear` 파일에서 `esapi-helper-2.x.x.jar` 파일의 압축을 풉니다. `esapi-helper-2.x.x.jar` 파일의 위치는 각 응용 프로그램 서버마다 다릅니다.

   | 응용 프로그램 서버 | esapi-helper-2.x.x.jar 파일의 위치 |
   | --- | --- |
   | JBoss | `adobe-livecycle-jboss.ear/lib` |
   | Oracle WebLogic | `adobe-livecycle-weblogic.ear/APP-INF/lib` |
   | IBM WebSphere | `adobe-livecycle-websphere.ear/` |

1. 편집할 `[extracted esapi-helper-2.x.x.jar]/esapi/validation.properties` 및 `[extracted esapi-helper-2.x.x.jar]/esapi/ESAPI.properties` 파일을 엽니다.

1. 다음 속성의 값을 `^[\\s\\S]*$`(으)로 설정하십시오. 예를 들어, `Validator.HTTPParameterName=^[\\s\\S]*$`과 같이 입력합니다. 파일을 저장하고 닫습니다.

   * `Validator.HTTPQueryString`
   * `Validator.PMCallParameterName`
   * `Validator.PMCallParameterValue`
   * `Validator.HTTPParameterName`
   * `Validator.HTTPParameterValue`
   * `Validator.xssSafeString`

1. 업데이트된 `esapi-helper-2.x.x.jar`을(를) `adobe-livecycle-<application_server_name>.ear`에 패키징합니다. 업데이트된 `adobe-livecycle-<application_server_name>.ear`을(를) 응용 프로그램 서버에 배포합니다.

1. AEM Forms 서버를 시작합니다.

## 참조 {#references}

* [JEE 6.5 LTS SP2에서 AEM Forms의 SSRF(서버측 요청 위조) 취약성 완화](/help/forms/troubleshooting/mitigating-server-side-request-forgery-vulnerabilities-for-aem-forms-on-jee-65-lts-sp2.md)
