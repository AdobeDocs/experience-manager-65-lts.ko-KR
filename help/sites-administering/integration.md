---
title: 솔루션 통합
description: Adobe Experience Manager(AEM)를 다른 Adobe 또는 타사 서비스와 통합하는 방법에 대해 자세히 알아보십시오.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: ac7f2ea1-4e0c-44da-8d1d-d65c65d817cb
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 20%

---

# 솔루션 통합{#solutions-integration}

* [Adobe Experience Cloud와 통합 사용](/help/sites-administering/marketing-cloud.md)
* [서드파티 서비스와 통합](/help/sites-administering/third-party-services.md)
* [Analytics를 외부 제공자와 통합](/help/sites-administering/external-providers.md)
* [스마트 태그 이해, 적용 및 조정](/help/assets/enhanced-smart-tags.md)

AEM을 다른 Adobe 또는 타사 서비스와 통합하는 방법에 대한 정보는 다음과 같습니다.

>[!NOTE]
>
>통합과 함께 사용자 정의 프록시 구성을 사용하는 경우 AEM의 일부 기능은 3.x API를 사용하고 다른 일부 기능은 4.x API를 사용하므로 HTTP 클라이언트 프록시 구성을 모두 구성해야 합니다.
>
>* 3.x은(는) [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)&#x200B;(으)로 구성되어 있습니다.
>* 4.x은(는) [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)&#x200B;(으)로 구성되어 있습니다.
>
