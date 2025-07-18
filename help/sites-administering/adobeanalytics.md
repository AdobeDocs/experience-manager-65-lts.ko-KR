---
title: Adobe Analytics와 통합
description: Adobe Experience Manager(AEM)를 Adobe Analytics과 통합하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: 4f7e1794-af5a-45a2-8dc6-80029c47caeb
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 53%

---

# Adobe Analytics와 통합{#integrating-with-adobe-analytics}

Adobe Analytics과 AEM을 통합하여 웹 페이지 활동을 추적할 수 있습니다.

* Adobe Analytics 구성을 사용하면 AEM에서 Adobe Analytics를 인증할 수 있습니다.
* 프레임워크는 Adobe Analytics 보고서 세트로 전송되는 데이터를 식별합니다.

데이터에는 페이지 및 사용자 데이터가 포함됩니다. 예를 들면 다음과 같습니다.

* AEM 구성 요소가 수집하는 데이터
* 링크 클릭
* 비디오 사용 정보
* Adobe Analytics에서의 페이지 방문 횟수

다음 페이지는 통합을 구성하는 데 도움이 됩니다.

* [Adobe Analytics 연결 및 프레임워크 만들기](/help/sites-administering/adobeanalytics-connect.md)
* [Adobe Analytics에 대한 링크 추적 구성](/help/sites-administering/adobeanalytics-link.md)
* [Adobe Analytics 속성을 사용하여 구성 요소 데이터 매핑](/help/sites-administering/adobeanalytics-mapping.md)
* [Adobe Analytics에 대한 비디오 추적 구성](/help/sites-administering/adobeanalytics-video.md)
* [Adobe 분류](/help/sites-administering/adobeanalytics-classifications.md)

[옵트인 마법사](/help/sites-administering/opt-in.md)를 사용하여 쉽게 통합을 수행할 수도 있습니다.

>[!NOTE]
>
>방법 문서를 참조하십시오. [DTM을 사용하여 AEM과 Adobe Target 및 Adobe Analytics 통합](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## 추가 정보 {#further-information}

다음을 참조하십시오.

* 사용자 데이터를 수집하는 구성 요소 개발 및 Adobe Analytics 프레임워크 사용자 지정에 대한 자세한 내용은 [Adobe Analytics 통합 확장](/help/sites-developing/extending-analytics.md)을 참조하십시오.

>[!NOTE]
>
>If you are using Adobe Analytics with a custom proxy configuration, you need to [configure two OSGi bundles](/help/sites-deploying/configuring-osgi.md) (for example, with the Web console) required for the **Apache HTTP Client** proxy configurations. Both are required as some functionalities of AEM use the 3.x APIs, while others use the 4.x APIs. 다음을 구성하십시오.
>
>* 3.x API 구성을 위한 **Day Commons HTTP 클라이언트 3.1**
>  &#x200B;>  (예: [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient))
>
>* 4.x API 구성을 위한 **Apache HTTP 구성 요소 프록시 구성**
>  &#x200B;>  (예: [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator))
>
