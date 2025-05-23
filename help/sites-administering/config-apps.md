---
title: AEM 앱에 대한 구성
description: Adobe Experience Manager 앱을 사용하여 애플리케이션 OTA(Over The Air)의 콘텐츠를 업데이트하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
exl-id: 4f36487c-45a2-4c18-b3cc-bb9284d68f49
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---

# AEM 앱에 대한 구성{#configuring-for-aem-apps}

Adobe Experience Manager 앱을 사용하면 애플리케이션 OTA의 콘텐츠를 (공중으로) 업데이트할 수 있습니다. 업데이트된 콘텐츠는 게시 인스턴스에 저장됩니다. 장치의 앱이 게시 인스턴스에 연결하고 업데이트를 확인하도록 허용하려면 빈 레퍼러 헤더를 허용하도록 게시 인스턴스를 구성해야 합니다.

## 빈 레퍼러 헤더 구성 {#configuring-empty-referrer-header}

레퍼러 필터 서비스를 구성하려면 다음 작업을 수행하십시오.

* 다음 위치에서 Apache Felix 콘솔(**구성**)을 엽니다.
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* 관리자로 로그인합니다.
* **구성** 메뉴에서 다음을 선택합니다. *Apache Sling Referrer 필터*
* 빈/누락된 레퍼러 헤더를 허용할 수 있도록 빈 허용 필드를 선택합니다.
* 변경 내용을 저장하려면 **저장**&#x200B;을 클릭하세요.

![chlimage_1-58](assets/chlimage_1-58a.png)

자세한 내용은 [OSGI 구성 설정](/help/sites-deploying/osgi-configuration-settings.md) 및 [보안 검사 목록 - 사이트 간 요청 위조 문제](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)를 참조하십시오.
