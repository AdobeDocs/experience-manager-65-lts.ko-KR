---
title: JEE의 AEM 6.5 Forms으로 업그레이드
description: AEM 6.1 Forms, AEM 6.2 Forms 및 LiveCycle ES4 SP1에서 AEM 6.3 Forms으로 직접 업그레이드할 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms Upgrade,AEM Forms on JEE
hide: true
hidefromtoc: true
exl-id: 643bc966-b2d8-4626-8c25-b63c8909287e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# JEE의 AEM 6.5 Forms으로 업그레이드 {#upgrade-to-aem-forms-jee}

JEE의 AEM 6.5.18.0 Forms에서는 전체 설치 관리자 및 패치 설치 관리자의 두 가지 설치 관리자를 제공합니다.

**전체 설치 관리자**: JEE의 [AEM 6.5.18.0 전체 설치 관리자](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ko)를 사용하여 새로운 AEM Forms 인스턴스를 설정하거나 JEE의 AEM 6.5.x.x Forms에서 JEE의 AEM 6.5.18.0 Forms으로 업그레이드할 수 있습니다.

**패치 설치 관리자**: [JEE 패치 설치 관리자의 AEM 6.5.18.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ko)은(는) 이미 AEM 6.5.x.x 버전을 사용 중인 고객을 위한 것입니다. 패치 설치 관리자를 사용하여 최신 버전의 AEM Forms으로 업그레이드할 수 있습니다.

다음 표에서는 전체 및 패치 설치 관리자를 사용하기 위한 시나리오를 보여 줍니다.

![전체 및 패치 설치 관리자 시나리오](assets/full-and-patch-installer.png)

전체 설치 관리자를 사용하여 기존 JEE의 AEM Forms 6.5.x.x를 JEE의 AEM 6.5.18.0 Forms으로 업그레이드하려면 다음 절차를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 JEE의 AEM 6.5 Forms 설치 관리자를 다운로드합니다. 설치 관리자를 사용하려면 유효한 유지 관리 및 지원 계약이 필요합니다.
1. 성공적인 업그레이드를 위해 수행할 검사에 대해 알아보려면 [업그레이드 검사 목록 및 계획](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65_kr)을 참조하세요.
1. 서버 가동 중지 시간을 최소화하면서 업그레이드가 올바르게 실행되도록 하는 작업을 알아보고 수행하려면 [AEM Forms으로 업그레이드 준비](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65_kr)를 참조하십시오.
1. 기존 환경 및 애플리케이션 서버에 따라 다음 문서 중 하나를 선택하고 지침을 따릅니다.

   * [AEM 6.3 또는 AEM 6.4 Forms에서 JBoss용 AEM 6.5 Forms으로 업그레이드](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65_kr)
   * [AEM 6.3 또는 AEM 6.4 Forms에서 WebSphere용 AEM 6.5 Forms으로 업그레이드](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65_kr)
   * [AEM 6.3 또는 AEM 6.4 Forms에서 JBoss 턴키용 AEM 6.5 Forms으로 업그레이드](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65_kr)

LiveCycle ES2, LiveCycle ES3, AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms에서 AEM 6.5 Forms으로 직접 업그레이드할 수 없습니다. 하나 이상의 LiveCycle 또는 AEM Forms 버전으로 중간 업그레이드를 수행한 다음 AEM 6.5 Forms으로 업그레이드할 수 있습니다. 중간 버전 목록 및 해당 업그레이드 지침은 [업그레이드 경로 선택](upgrade.md)을 참조하세요.
