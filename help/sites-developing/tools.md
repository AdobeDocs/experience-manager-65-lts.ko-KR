---
title: 테스트 및 추적 도구
description: AEM은 구성 요소 UI 테스트를 위한 프레임워크 및 구성 요소 테스트 및 디버깅을 위한 메커니즘을 제공합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 4aa0f10d-e915-4ad2-a886-080ed8b9b10f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 1%

---

# 테스트 및 추적 도구{#testing-and-tracking-tools}

## 테스트 {#testing}

AEM은 다음을 제공합니다.

* [구성 요소 UI를 테스트하기 위한 프레임워크](/help/sites-developing/hobbes.md).
* [구성 요소를 테스트하고 디버깅하는 메커니즘](/help/sites-developing/developer-mode.md).

다음은 두 개의 오픈 Source 테스트 도구입니다.

**Selenium**

Selenium은 활동당 한 명의 사용자가 있는 브라우저에서 기능 테스트에 사용됩니다. 테스트 단계(클릭 수)를 HTML 테이블 또는 Java™ 클래스로 기록합니다.

자세한 내용은 [https://www.selenium.dev/](https://www.selenium.dev/)을(를) 참조하십시오.

**JMeter**

JMeter는 요청을 추적하는 데 사용되며 기능, 성능 및 스트레스 테스트에 사용할 수 있습니다.

자세한 내용은 [https://jmeter.apache.org/](https://jmeter.apache.org/)을(를) 참조하십시오.

또한 테스트 자동화 및 테스트 계획 관리를 위한 많은 독점 툴이 있습니다.

### 추적 {#tracking}

다음 도구를 쉽게 사용할 수 있습니다. 그러나 모든 경우 핵심 문제는 프로젝트 팀의 모든 구성원(파트너 및 고객)에게 데이터를 제공하는 것입니다.

**Bugzilla**

자체 요구 사항에 맞게 구성할 수 있는 버그 추적 시스템.

**스프레드시트**

특별히 버그 추적 도구는 아니지만, 스프레드시트는 쉽게 이해할 수 있고 대부분의 사용자가 기능을 경험했기 때문에 이러한 목적으로 종종 *mis*&#x200B;사용됩니다.

이러한 스프레드시트가 추적에 사용되는 경우

* 단순하게 유지해야 합니다.
* 개별 스프레드시트의 수는 최소한으로 유지해야 합니다.
* 정기적으로 업데이트해야 합니다.
* 운영 복제본은 하나만 유지되어야 하며 모든 사람이 운영 복제본의 위치를 알아야 합니다.
* 모든 프로젝트 멤버가 액세스할 수 있어야 합니다.
* 보안이 문제이고(대기업에서 종종 발생) 공통 액세스가 불가능한 경우, 모든 사람이 이러한 스프레드시트가 복사본이며 업데이트할 수 없다는 것을 알고 있는 한 복사본이 배포될 수 있습니다.

버그 및 기능 요구 사항을 추적하기 위한 많은 독점 도구가 있습니다.
