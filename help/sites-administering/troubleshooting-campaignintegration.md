---
title: Adobe Campaign Classic 통합 문제 해결
description: Adobe Campaign Classic 통합과 관련된 문제를 해결하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: fc60d6a3-b2fd-4991-931f-22924ba8003d
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Adobe Campaign Classic 통합 문제 해결{#troubleshooting-your-adobe-campaign-classic-integration}

Adobe Campaign Classic(ACC) 통합 문제를 해결하는 방법을 알아봅니다.

다음 문제 해결 팁은 AEM을 ACC와 통합할 때 발생할 수 있는 가장 일반적인 문제를 해결하는 데 도움이 됩니다.

## 일반 문제 해결 팁 {#general-troubleshooting-tips}

두 솔루션(AEM > Adobe Campaign Classic, Adobe Campaign Classic > AEM)에서 HTTP 호출을 보내고 받는지 확인합니다. 이 팁은 방화벽/SSL 문제를 방지하는 데 도움이 됩니다.

* AEM 기능의 경우 AEM 작성자 인터페이스에서 JSON 호출이 요청됨을 볼 수 있습니다
   * 이러한 호출로 인해 HTTP-500 오류가 발생해서는 안 됩니다.
   * HTTP-500 오류가 표시되면 `error.log`에서 자세한 내용을 확인하십시오.
* AEM에서 캠페인 클래스에 대한 디버그 수준을 높이는 것도 문제를 해결하는 데 도움이 될 수 있습니다.

## 연결에 실패하는 경우 {#when-the-connection-fails}

Adobe Campaign Classic에서 **`aemserver`** 연산자를 구성했는지 확인하십시오.

## 이미지가 Adobe Campaign Classic 콘솔에 표시되지 않는 경우 {#if-images-do-not-appear-in-the-adobe-campaign-console}

HTML 소스를 확인하고 클라이언트 컴퓨터에서 URL을 열 수 있는지 확인합니다. URL에 `localhost:4503`이(가) 있으면 AEM 작성자 인스턴스에서 일 CQ 링크 외부화의 구성을 변경합니다. Adobe Campaign Classic 콘솔 시스템에서 연결할 수 있는 게시 인스턴스를 가리켜야 합니다.

[외부화 구성](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)을 참조하십시오.

## AEM에서 Adobe Campaign Classic으로 연결할 수 없는 경우  {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Adobe Campaign Classic에서 다음 오류 메시지를 찾습니다.

* `No datasource defined in the instance 'default'.`

* `Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

이 문제를 해결하려면 `$CAMPAIGN_HOME/conf/config-<instance-name>.xml`에서 다음을 변경하십시오.

* `<dataStore hosts="*" lang="en_GB">`

## Adobe Campaign Classic 대화 상자에 데이터가 표시되지 않는 경우 {#if-no-data-displays-in-the-adobe-campaign-dialog}

Adobe Campaign Classic에서 포트 번호 뒤에 슬래시(`/`)가 없는지 확인합니다.

![Adobe Campaign Classic - 포트 번호 뒤에 슬래시가 없는지 확인](assets/chlimage_1-149.png)

## setlocale에 대한 경고를 받는 경우 {#if-you-get-a-warning-about-your-setlocale}

Adobe Campaign Classic용 Apache HTTPD 서비스를 시작할 때 `Warning: setlocale: LC_CTYPE cannot change locale` 오류가 표시될 수 있습니다

Adobe Campaign Classic 서버에 `en_CA.ISO-8859-15 locale`이(가) 설치되어 있는지 확인하십시오.

* `local -a`을(를) 사용하여 설치 여부를 확인할 수 있습니다.
* 설치되어 있지 않으면 `/usr/local/neolane/nl6/env.sh` 스크립트를 패치하고 로케일을 설치된 로케일로 변경할 수 있습니다.

## 스크립트 &#39;get_nms_amcGetSeedMetaData_jssp&#39;를 컴파일하는 동안 오류가 발생하는 경우 {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

AEM 로그 파일에 다음 오류 메시지가 표시되는 경우:

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Adobe Campaign Classic 서버에서 다음 해결 방법을 사용하십시오.

1. `$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js` 파일 열기
1. `amcGetSeedMetaData` 메서드의 467행 수정
1. `label : [inclView.@label](mailto:inclView.@label)`을(를) `label : String([inclView.@label](mailto:inclView.@label))`(으)로 변경
1. 저장.
1. 서버를 다시 시작합니다.

## Adobe Campaign Classic에서 동기화 단추를 클릭할 때 오류가 표시되는 경우 {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Adobe Campaign Classic에서 **동기화** 단추를 클릭하면 다음 오류가 표시될 수 있습니다.

* `Error while executing the method 'aemListContent' of service [nms:delivery](https://nmsdelivery/)`

이 문제를 해결하려면 Adobe Campaign Classic의 **외부 계정**&#x200B;에 구성된 AEM 연결 URL이 컴퓨터에서 연결할 수 있는지 확인하십시오.

`localhost`에서 URL의 IP 주소로 전환하면 종종 이 문제를 해결할 수 있습니다.

## &quot;XTK 날짜+시간을 &#39;정의되지 않음&#39; 상태로 구문 분석할 수 없음&quot; 오류 수신 시 {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

AEM에서 **동기화**&#x200B;를 클릭하면 페이지의 스크립트가 발생했다는 오류가 나타날 수 있습니다.

* `Cannot parse XTK Date+Time 'undefined': not a valid XTK value.`

이 오류는 AEM 인스턴스에 오래된 Adobe Campaign Classic 정보가 있는 경우 발생합니다. 다음을 수행하여 이 문제를 해결할 수 있습니다.

1. AEM에 있는 모든 Adobe Campaign Classic 통합 구성을 제거합니다.
1. 통합을 다시 빌드합니다.
1. 템플릿을 만듭니다.

## Cloud Service을 설정할 때 SSL 연결에 오류가 표시되는 경우 {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

AEM `error.log`에 다음 내용이 표시되면 Adobe Campaign 지원 팀에 티켓을 제출합니다.

```text
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

## 동기화 대화 상자에 예상 HTTPS 링크 대신 HTTP가 표시되는 경우 {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

Adobe Campaign Classic 게재에서 콘텐츠를 동기화하려고 하면 AEM에서 뉴스레터 목록을 반환합니다. 그러나 목록의 뉴스레터에 대한 URL은 HTTPS가 아닌 HTTP 주소일 수 있습니다. 목록에서 항목 중 하나를 선택하면 오류가 발생합니다. 이 오류는 다음 설정에서 발생할 수 있습니다.

* AEM 작성자와의 통신에 https를 사용하여 호스팅된 Adobe Campaign
* SSL을 종료하는 역방향 프록시
* 온-프레미스 AEM 작성자 인스턴스

이 문제를 해결하려면 다음을 수행하십시오.

* 원래 프로토콜을 헤더로 전달하도록 AEM Dispatcher 또는 역방향 프록시를 구성해야 합니다.
* AEM의 OSGi 구성에서 **Apache Felix Http 서비스 SSL 필터**&#x200B;는 필수 헤더 설정으로 구성해야 합니다.
   * `https://<host>:<port>/system/console/configMgr`
   * [https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter](https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter) 보기

## 페이지 속성에서 사용자 지정 템플릿을 선택할 수 없음 {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

AEM for Adobe Campaign Classic에서 메일 템플릿을 만들 때 템플릿의 `jcr:content` 노드에 값이 `mapRecipient`인 `acMapping` 속성을 포함해야 합니다. 그렇지 않으면 AEM의 **페이지 속성**&#x200B;에서 Adobe Campaign Classic 템플릿을 선택할 수 없습니다. 필드가 비활성화되어 나타납니다.

## AEM 로그에 &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; 오류가 표시되는 경우 {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

사용자 지정 템플릿을 사용할 때 AEM 로그에 `com.day.cq.mcm.campaign.servlets.util.ParameterMapper` 오류가 표시될 수 있습니다.

이 오류는 `acMapping` 속성이 `recipient.firstName` 이외의 값으로 설정된 경우 발생하며, Adobe Campaign 관리자에 빈 값이 만들어집니다.

이 오류가 발생하면 [패키지 공유](/help/sites-administering/package-manager.md#package-share)에서 AEM용 기능 팩 6576을 설치하십시오.
