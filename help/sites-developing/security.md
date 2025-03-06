---
title: 보안
description: 개발 단계에서 애플리케이션 보안 시작
solution: Experience Manager, Experience Manager Sites
feature: Developing,Security
role: Developer
exl-id: abc2747f-cfd8-4ee1-bbc0-5ad89beb383a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# 보안{#security}

애플리케이션 보안은 개발 단계에서 시작됩니다. Adobe에서는 다음 보안 모범 사례를 적용할 것을 권장합니다.

## 요청 세션 사용 {#use-request-session}

Adobe에서는 최소 권한의 원칙에 따라 사용자 요청에 바인딩된 세션과 적절한 액세스 제어를 사용하여 모든 저장소에 액세스할 것을 권장합니다.

## XSS(크로스 사이트 스크립팅)로부터 보호 {#protect-against-cross-site-scripting-xss}

XSS(크로스 사이트 스크립팅)를 사용하면 공격자가 다른 사용자가 본 웹 페이지에 코드를 삽입할 수 있습니다. 이 보안 취약성은 악의적인 웹 사용자가 액세스 제어를 우회하기 위해 악용될 수 있습니다.

AEM은 출력 시 사용자가 제공한 모든 콘텐츠를 필터링하는 원칙을 적용합니다. XSS 예방은 개발 및 테스트 모두에서 가장 높은 우선순위가 부여됩니다.

AEM에서 제공하는 XSS 보호 메커니즘은 [OWASP(Open Web Application Security Project)](https://owasp.org/)에서 제공하는 [AntiSamy Java™ 라이브러리](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project)를 기반으로 합니다. 기본 AntiSamy 구성은 다음에서 찾을 수 있습니다.

`/libs/cq/xssprotection/config.xml`

구성 파일을 오버레이하여 이 구성을 자체 보안 요구 사항에 맞게 조정하는 것이 중요합니다. 공식 [AntiSamy 설명서](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project)에서는 보안 요구 사항을 구현하는 데 필요한 모든 정보를 제공합니다.

>[!NOTE]
>
>Adobe에서는 AEM에서 제공한 [XSSAPI](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/xss/XSSAPI.html)를 사용하여 항상 XSS 보호 API에 액세스할 것을 권장합니다.

또한 Apache용 [mod_security](https://www.modsecurity.org)과(와) 같은 웹 응용 프로그램 방화벽은 배포 환경의 보안에 대한 신뢰할 수 있는 중앙 집중식 제어를 제공하고 이전에 탐지되지 않은 교차 사이트 스크립팅 공격으로부터 보호할 수 있습니다.

## Cloud Service 정보 액세스 {#access-to-cloud-service-information}

>[!NOTE]
>
>인스턴스 보안에 필요한 Cloud Service 정보 및 OSGi 설정에 대한 ACL은 [프로덕션 준비 모드](/help/sites-administering/production-ready.md)의 일부로 자동화됩니다. 이는 구성을 수동으로 변경할 필요가 없음을 의미하지만 배포를 시작하기 전에 구성을 검토하는 것이 좋습니다.

[AEM 인스턴스를 Adobe Experience Cloud과 통합](/help/sites-administering/marketing-cloud.md)할 때 [Cloud Service 구성](/help/sites-developing/extending-cloud-config.md)을 사용합니다. 이러한 구성에 대한 정보는 수집된 모든 통계와 함께 저장소에 저장됩니다. Adobe은 이 기능을 사용하는 경우 이 정보에 대한 기본 보안이 요구 사항과 일치하는지 검토할 것을 권장합니다.

webservicesupport 모듈은 아래에 통계 및 구성 정보를 기록합니다.

`/etc/cloudservices`

기본 권한 사용:

* 작성자 환경: `contributors`에 대한 `read`

* 게시 환경: `everyone`에 대한 `read`

## 사이트 간 요청 위조 공격으로부터 보호 {#protect-against-cross-site-request-forgery-attacks}

AEM이 CSRF 공격을 완화하는 데 사용하는 보안 메커니즘에 대한 자세한 내용은 보안 확인 목록의 [Sling Referrer 필터](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 섹션 및 [CSRF 보호 프레임워크 설명서](/help/sites-developing/csrf-protection.md)를 참조하십시오.
