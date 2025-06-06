---
title: CSRF 보호 프레임워크
description: 프레임워크는 토큰을 사용하여 클라이언트 요청이 합법적임을 보장합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: d6bd4028-56c9-4e09-9bba-1199a41b41b8
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# CSRF 보호 프레임워크{#the-csrf-protection-framework}

Apache Sling Referrer Filter 외에도 Adobe은 이러한 유형의 공격으로부터 보호하기 위한 새로운 CSRF 보호 프레임워크를 제공합니다.

프레임워크는 토큰을 사용하여 클라이언트 요청이 합법적임을 보장합니다. 토큰은 양식을 클라이언트로 보낼 때 생성되며 양식을 다시 서버로 보낼 때 확인됩니다.

>[!NOTE]
>
>익명 사용자에 대한 게시 인스턴스에 토큰이 없습니다.

## 요구 사항 {#requirements}

### 종속성 {#dependencies}

`granite.jquery` 종속성에 의존하는 모든 구성 요소는 자동으로 CSRF 보호 프레임워크의 혜택을 받을 수 있습니다. 그렇지 않으면 구성 요소에 대해 `granite.csrf.standalone`에 대한 종속성을 선언해야 프레임워크를 사용할 수 있습니다.

### 암호화 키 복제 {#replicating-crypto-keys}

토큰을 사용하려면 HMAC 바이너리를 배포의 모든 인스턴스에 복제해야 합니다. 자세한 내용은 [HMAC 키 복제](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key)를 참조하십시오.

>[!NOTE]
>
>또한 CSRF 보호 프레임워크를 사용하기 위해 필요한 Dispatcher 구성을 변경해야 합니다.
>
>* [CSRF 공격을 방지하도록 Adobe Experience Manager Dispatcher 구성](https://experienceleague.adobe.com/ko/docs/experience-manager-dispatcher/using/configuring/configuring-dispatcher-to-prevent-csrf)
>* [Dispatcher 개요](https://experienceleague.adobe.com/ko/docs/experience-manager-dispatcher/using/dispatcher)

>[!NOTE]
>
>웹 응용 프로그램에서 매니페스트 캐시를 사용하는 경우 토큰이 CSRF 토큰 생성 호출을 오프라인으로 전환하지 않도록 매니페스트에 &quot;**&ast;**&quot;을(를) 추가해야 합니다. 자세한 내용은 이 [링크](https://www.w3.org/TR/offline-webapps/)를 참조하세요.
>
>CSRF 공격 및 이를 완화하는 방법에 대한 자세한 내용은 [크로스 사이트 요청 위조 OWASP 페이지](https://owasp.org/www-community/attacks/csrf)를 참조하십시오.
