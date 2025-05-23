---
title: 계획 수립
description: Adobe Experience Manager 테스트를 계획하기 위해 알아야 할 사항에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 82199140-e464-45a5-9c00-dda2d8efde74
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---

# 계획 수립{#planning}

이 문서에서는 테스트 계획을 수립하기 위해 알아야 할 사항에 대해 설명합니다. 또한 테스트를 수행하기 전에 다음 질문에 답해야 합니다.

* [어떤 테스트 환경이 필요합니까?](/help/sites-developing/test-environments.md)
* [테스트 사례 정의](/help/sites-developing/test-cases.md)
* [테스트 - 언제 누구와 함께?](/help/sites-developing/when-who.md)

## 시작하기에 앞서 {#before-you-start}

테스트의 실제 분석 및 정의를 시작하기 전에 다음 정보를 검토하십시오.

**AEM 아키텍처** - AEM의 아키텍처 및 기본 원리를 소개하는 기본 개념 을 참조하십시오.

**설명서** - 자세한 내용은 설명서 섹션 또는 방법 문서를 참조하십시오.

**테스트의 기본 원칙** - 소프트웨어 테스트 및 품질 Assurance의 기본 원칙을 알고 있어야 합니다. 프로젝트 테스트 경험이 있는 것이 좋습니다.

이러한 원칙을 다루는 많은 웹 사이트, 책 및 과정이 있으므로 이 문서에서 자세히 다루지 않습니다.

**피해야 할 가정** - 가장 큰 가정은 웹 사이트에서 매일 수백만 개의 요청을 처리해야 한다는 것입니다. 특정 상황에서 이는 사실일 수 있지만, 상정할 수는 없다.

100% 정확도로 향후 숫자를 예측할 수는 없지만 기존 사이트와 경험한 트래픽을 관찰하면 좋은 지표를 얻을 수 있습니다. 그런 다음 예상/트래픽이 증가할 것으로 기대하는 요소에 따라 예상치를 만들 수 있습니다.

**품질에 대한 약속** - 테스트하는 사람은 중립을 유지하고 테스트 결과를 단순히 보고하는 것이 무엇보다 중요합니다.

결과에 따라 작업을 결정하고 시작하는 것은 프로젝트 관리자의 책임입니다.

**참여하기** - 모든 당사자가 모든 모임(상태, 워크숍 등)에 완전히 참여하도록 하는 것은 프로젝트 관리자의 책임이지만 정보 수집 및 요구 사항 분석 프로세스를 포함하여 가능한 한 빨리 프로젝트 주기에서 참여하도록 노력해야 합니다.

**고객 참여** - 유사한 테마에서 테스트 사례 및 계획을 정의할 때 고객(가능한 경우)을 참여시키십시오.

## 테스트 유형 {#types-of-tests}

AEM 프로젝트를 테스트할 때 사용하기에 적합한 다양한 테스트 표준 분류가 있습니다. 사용할 항목을 결정하려면 다음 사항을 잘 알고 있어야 합니다.

>[!NOTE]
>
>시간 순서대로 표시됩니다.

**단위 테스트** - 개별 요소가 올바르게 동작하는지 확인하기 위해 개발 팀에서 일반적으로 수행하는 테스트입니다(격리된 테스트이지만).

**통합 테스트** - 결합할 때 모듈을 테스트합니다. 이러한 테스트는 단위 테스트 후 시스템 테스트 전에 수행됩니다.

**연기 테스트** - 소프트웨어가 실행 중이고 높은 수준의 기능을 사용할 수 있음을 증명하는 데 사용되는 빠르고 더티(dirty) 테스트입니다. 세부 사항은 테스트되지 않습니다.

**기능 테스트** - 소프트웨어의 기능을 테스트하는 데 사용됩니다. 일련의 테스트는 예상된 입력 및 예기치 않은 입력 및/또는 잘못된 입력을 모두 포함하여 모든 기능 세부 사항을 포함하도록 디자인됩니다.

블랙박스 테스트는 해당 요소의 내부 작업에 대해 알지 못한 채 수행되는 전체 단위/구성 요소/모듈에 대한 기능 테스트입니다.

**시스템 테스트** - 전체 시스템이 완전히 통합되고 적합한 플랫폼에 설치되면 전체 시스템을 테스트합니다.

블랙박스 기준으로 기능을 테스트합니다.

**성능 테스트** - AEM을 테스트할 때 성능 테스트가 중요합니다.

서로 다른 조건에서 성능을 보여 주는 데 사용됩니다.

* 기본

  사이트에서 경험하게 될 조건은 시간의 90%라고 합니다. 예를 들어 작성자의 비율만 시스템을 사용하는 경우입니다.

* 피크

  모든 작성자가 시스템을 동시에 사용하거나 새 콘텐츠가 게시되고 사이트를 보는 방문자의 수가 증가하는 등 특별한 상황으로 인해 비례적으로 짧은 시간 동안 경험할 조건입니다.

* 극단적

  새롭고 매우 흥미로운 콘텐츠가 웹 사이트에 게시되는 경우 성능 예측을 에뮬레이션하는 데 사용할 수 있습니다. 그런 다음 극단적인 최고점이 보일 수 있습니다. 하지만 이는 항상 완전히 예측할 수 있는 것은 아닙니다.

  특정 종목의 티켓을 예매하거나 대망의 웹 사이트가 최초로 공개되는 경우, 이러한 상황이 간혹 눈에 띈다.

그런 다음 응용 프로그램을 조정하는 데 결과가 사용됩니다.

**부하 테스트** - 부하 테스트는 극단적인 조건에서 구성 요소 또는 응용 프로그램이 어떻게 작동하는지 확인하기 위해 수행됩니다. 특히 이러한 테스트는 비헤이비어가 악화되는 방식, 요소에 오류가 발생하는 방식 및 방법을 보여주는 데 사용됩니다.

**회귀 테스트** - 회귀 테스트는 소프트웨어의 이전 릴리스에서 이미 입증된 기능이 여전히 올바르게 작동하는지 확인하는 데 사용됩니다.

회귀 테스트는 빠르고 일관되게 반복할 수 있도록 자동화에 적합한 후보입니다(가능한 경우).

**승인 테스트** - 승인 테스트는 고객의 프로젝트 승인을 나타내는 데 사용되는 특별한 범주입니다.

수락 테스트 목록에는 위의 다양한 카테고리의 테스트 조합이 포함될 수 있으며 프로젝트가 고객의 요구 사항을 충족하는지 확인하기 위해 선택됩니다

자세한 내용은 [승인 및 승인](/help/sites-developing/acceptance-signoff.md)을 참조하세요.

## 시작하기 {#getting-started}

자세한 테스트 사례 및 테스트 계획을 시작하기 전에 다음을 수행할 수 있습니다.

**목표 정의** - 테스트가 진행될 때 세부 조정을 위한 시작점으로 사용할 높은 수준의 목표를 정의합니다. 다음과 같은 작업을 수행할 수 있습니다.

* 상세 요구 사항 사양에 따라 기능을 테스트합니다.
* [대상 지표](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics)에 따라 성능을 테스트합니다.

다른 사람들 사이에.

**기존 웹 사이트에서 트래픽 통계 수집** - 이 정보는 로그 파일에서 추출할 수 있습니다. 자세한 내용은 성능 모니터링을 참조하십시오.

이러한 수치는 기존 웹 사이트의 현재 트래픽(볼륨 및 스프레드)을 나타내며 새 웹 사이트의 기준점을 구성하는 데 사용할 수 있습니다.

**외부 웹 사이트에서 트래픽 통계 수집** - 가능한 경우 비교를 위해 다른 웹 사이트에서 트래픽 통계를 수집할 수 있지만 이러한 수치가 항상 게시되는 것은 아닙니다.

**대상 지표 확인** - 지표는 달성할 성능 목표를 나타내므로 웹 사이트의 품질에 대한 정량적 측정을 정의하는 데 사용됩니다.

고객과 함께 프로젝트를 시작할 때 정의해야 합니다. 자세한 내용은 [대상 지표](/help/sites-developing/planning.md)를 참조하십시오.
