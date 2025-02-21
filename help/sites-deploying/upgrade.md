---
title: Adobe Experience Manager 6.5로 업그레이드
description: 이전 Adobe Experience Manager(AEM) 설치를 AEM 6.5로 업그레이드하는 기본 사항에 대해 알아봅니다.
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f66bb283e5c2a746821839269e112be8c2714ba7
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 1%

---

# Adobe Experience Manager(AEM) 6.5 LTS로 업그레이드 {#upgrading-to-aem}

>[!NOTE]
>AEM 6.5 LTS로의 업그레이드는 마지막 6개의 서비스 팩에서 지원됩니다.

이 섹션에서는 AEM 설치를 AEM 6.5로 업그레이드하는 방법에 대해 설명합니다.

<!-- Alexandru: drafting for now 

* [Planning Your Upgrade](/help/sites-deploying/upgrade-planning.md)
* [Assessing the Upgrade Complexity with Pattern Detector](/help/sites-deploying/pattern-detector.md)
* [Backward Compatibility in AEM 6.5](/help/sites-deploying/backward-compatibility.md)
  This was drafted before: * [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

<!--
* [Upgrade Procedure](/help/sites-deploying/upgrade-procedure.md)
* [Upgrading Code and Customizations](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Pre-Upgrade Maintenance Tasks](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Performing an In-Place Upgrade](/help/sites-deploying/in-place-upgrade.md)
* [Post Upgrade Checks and Troubleshooting](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Sustainable Upgrades](/help/sites-deploying/sustainable-upgrades.md)
* [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md)

-->

이러한 절차와 관련된 AEM 인스턴스를 더 쉽게 참조하기 위해 이 문서 전체에서 다음 용어가 사용됩니다.

* *source* 인스턴스는 업그레이드하는 AEM 인스턴스입니다.
* *target* 인스턴스는 업그레이드하려는 인스턴스입니다.

## 변경 사항 {#what-has-changed}

### 업데이트 {#updates}

다음은 AEM의 지난 몇 가지 릴리스에 대한 주요 참고 변경 사항입니다.

1. Foundation 계층이 Java 17(Apache Sling, Apache Felix 및 Apache Jackrabbit Oak의 오픈 소스 번들 계층으로 구성)을 지원하도록 업그레이드되었습니다

1. AEM 6.5 LTS jar 패키지는 이제 Jarkarta 서블릿 API 사양 5를 지원하며, war 패키징은 Jarkarta 서블릿 API 사양 5/6을 구현하는 서블릿 컨테이너에 배포할 수 있습니다

1. AEM 6.5 LTS uber-jar의 패키징이 변경되었습니다. 자세한 내용은 [코드 및 사용자 지정 업그레이드](/help/sites-deploying/upgrading-code-and-customizations.md)를 참조하십시오.

### 제거된 기존 기능/아티팩트 {#removed-legacy-features-artifacts}

다음 레거시 솔루션은 AEM 6.5 LTS에서 제거되었습니다. 자세한 내용은 TBD: 릴리스 정보 링크 및 업그레이드 후 제거된 [오래된 번들 목록](/help/sites-deploying/obsolete-bundles.md)을 참조하세요.

1. Social
1. 상거래
1. Screens
1. We-retail
1. Search &amp; Promote 통합

**제거된 아티팩트**

1. CRX 탐색기
1. Crx2oak
1. Google guava(보안 취약점으로 인해 제거됨)
1. Abdera-parser(보안 취약성으로 인해 제거됨)
1. jdom(`org.apache.servicemix.bundles.jdom`)(보안 취약성으로 인해 제거됨)
1. `com.github.jknack.handlebars`(보안 취약성으로 인해 제거됨)

AEM 6.5 LTS는 기능의 이전 버전과의 호환성에 중점을 두고 있으며 분석기 도구와 함께 제공됩니다. 업그레이드 계획을 시작할 때의 복잡성 평가는 [AEM 분석기를 사용한 업그레이드 복잡성 평가](/help/sites-deploying/pattern-detector.md)를 참조하십시오. 그 밖의 변경 사항에 대한 자세한 내용은 여기에서 전체 릴리스 노트를 참조하십시오. TBD: AEM 6.5 LTS의 릴리스 노트 링크