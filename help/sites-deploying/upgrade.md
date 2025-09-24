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
exl-id: ebc34847-dc3d-41ed-b0d6-f004c3debcd9
source-git-commit: 57bf39aa914bddca05d526b46b581579965069d6
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Adobe Experience Manager(AEM) 6.5 LTS로 업그레이드 {#upgrading-to-aem}

>[!NOTE]
>지원되는 모든 6.5 서비스 팩에서 AEM 6.5 LTS로 업그레이드할 수 있습니다.

>[!NOTE]
>
>기술적인 측면에서 AEM 6.5 LTS에서 AEM 6.5 LTS 서비스 팩으로의 업그레이드 프로세스는 매끄러운 [내부 업그레이드](/help/sites-deploying/in-place-upgrade.md)가 되도록 설계되었습니다. 릴리스 노트에 구체적으로 명시되어 있지 않는 한, 이 프로세스는 일반적으로 고객의 코드 변경을 필요로 하지 않습니다.

이 섹션에서는 AEM 설치를 AEM 6.5 LTS로 업그레이드하는 방법에 대해 설명합니다.

<!-- Alexandru: drafting for now 

* [Planning Your Upgrade](/help/sites-deploying/upgrade-planning.md)
* [Assessing the Upgrade Complexity with Pattern Detector](/help/sites-deploying/pattern-detector.md)
* [Backward Compatibility in AEM 6.5](/help/sites-deploying/backward-compatibility.md)
-->

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

Foundation 계층은 이제 Apache Sling, Felix 및 Jackrabbit Oak의 최신 오픈 소스 번들을 통합하여 Java 17 및 Java 21을 지원합니다. 또한 AEM 6.5 LTS uber-jar의 패키징이 변경되었습니다. 또한 몇 가지 레거시 기능이 AEM 6.5 LTS에서 제거되었습니다. 자세한 내용은 [릴리스 정보](/help/release-notes/release-notes.md#whats-new-what-s-new) 및 [업그레이드 후 제거된 오래된 번들 목록](/help/sites-deploying/obsolete-bundles.md)을 참조하세요.

AEM 6.5 LTS는 기능의 이전 버전과의 호환성에 중점을 두고 있으며 분석기 도구와 함께 제공됩니다. [업그레이드 계획](/help/sites-deploying/aem-analyzer.md)을 시작할 때 복잡성을 평가하려면 [AEM 분석기를 사용하여 업그레이드 복잡성 평가](/help/sites-deploying/upgrade-planning.md)를 참조하십시오.
