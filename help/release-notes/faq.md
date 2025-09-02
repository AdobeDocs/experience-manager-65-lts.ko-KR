---
title: 자주 묻는 질문 (FAQ)
description: AEM 6.5 LTS에 대해 자주 묻는 질문입니다.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: d18c9dc3-fdcc-4558-b9b6-ecf1ce61048a
source-git-commit: 9f9da819550b93d7a06b151962bf41751ecbc8b3
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 49%

---

# AEM 6.5 LTS 자주 묻는 질문 (FAQ) {#faq}

이 페이지에서는 AEM 6.5 LTS에 대해 자주 묻는 몇 가지 질문에 답변합니다.

## Adobe가 AEM용 6.5 LTS를 릴리스한 이유는 무엇입니까?

Adobe는 제공하는 애플리케이션의 보안 및 안정성을 위해 최선을 다하고 있습니다. AEM 6.5 장기 지원은 AEM 6.5에 대한 향후 업데이트를 위한 기반을 마련합니다. 특히, AEM 6.5 LTS에는 Oracle Java 17 및 Java 21에 대한 지원이 포함되어 있으며, 새로운 AEM 기능 및 혁신을 제공하는 AEM 분기가 될 것입니다.

## 온프레미스 고객입니다. AEM 6.5 LTS로 업그레이드하지 않으면 어떻게 됩니까?

AEM 6.5 LTS에는 Oracle Java 17 및 Java 21에 대한 지원을 포함한 중요한 보안 및 안정성 업데이트가 포함됩니다. Adobe는 앞으로 최소 2년 동안 AEM 6.5를 계속 지원할 예정이지만, 조직에서는 6.5 LTS로의 업그레이드를 계획하기 시작하는 것이 좋습니다.

## AEM 6.5 LTS로 업그레이드할 경우 기존 사용자 지정 및 통합이 영향을 받습니까?

AEM 6.5 LTS는 이전 버전과의 호환성을 유지하는 것을 목표로 하지만, 일부 레거시 기능 및 아티팩트는 제거되었습니다.
현재 사용자 정의 및 통합에 미치는 영향을 평가하려면 [릴리스 정보](/help/release-notes/release-notes.md#deprecated-and-removed-features)와 [AEM 분석기 도구](/help/sites-deploying/aem-analyzer.md)를 검토해야 합니다.

## AEM 6.5 LTS로 원활하게 전환하려면 어떻게 해야 합니까?

원활한 전환을 위해 다음 작업을 수행하는 것이 좋습니다.

* [릴리스 정보](/help/release-notes/release-notes.md) 및 설명서를 철저히 검토합니다.
* [AEM 분석기 도구](/help/sites-deploying/aem-analyzer.md)를 사용하여 업그레이드의 복잡성을 평가합니다.
* 업그레이드 프로세스에 대해 충분한 시간과 리소스를 계획하고 할당합니다.
* Adobe 지원 및 활성화 세션에 참여하여 지침과 도움을 받습니다.

## AEM 6.5 LTS 서비스 팩이란 무엇입니까?

AEM 6.5 LTS 서비스 팩은 초기 릴리스 이후 AEM 6.5 LTS에 대한 모든 수정 사항 및 개선 사항을 포함하는 누적 업데이트입니다. AEM 인스턴스가 최신 기능 및 보안 패치를 사용하여 최신 상태인지 확인하려면 최신 서비스 팩을 적용하는 것이 좋습니다.

## 현재 AEM 6.5를 사용하고 있는데, AEM 6.5 LTS GA 릴리스로 업그레이드하지 않고 AEM 6.5 LTS 서비스 팩으로 바로 업그레이드할 수 있습니까?

예. AEM 6.5에서 AEM 6.5 LTS 서비스 팩으로 바로 업그레이드할 수 있습니다. [릴리스 정보](/help/release-notes/release-notes.md) 및 [AEM 6.5 LTS로 업그레이드](/help/sites-deploying/upgrade.md) 섹션을 검토하는 것이 좋습니다.

## 현재 AEM 6.5 LTS GA를 사용하고 있습니다. AEM 6.5 LTS 서비스 팩으로 업그레이드하려면 코드를 변경해야 합니까?

아니요. 코드를 변경하지 않아도 AEM 6.5 LTS에서 AEM 6.5 LTS 서비스 팩으로 업그레이드할 수 있습니다. 그러나 프로덕션 인스턴스에 서비스 팩을 적용하기 전에 항상 [릴리스 정보](/help/release-notes/release-notes.md)를 검토하고 스테이징 환경에서 사용자 지정 및 통합을 테스트하는 것이 좋습니다.

## 새로운 AEM 6.5 LTS 설정으로 새로 시작하려고 하는데 AEM 6.5 LTS 서비스 팩으로 바로 시작할 수 있습니까?

예. AEM 6.5 LTS GA 빌드를 설정하지 않고도 새 AEM 6.5 LTS 서비스 팩을 직접 설정할 수 있습니다. 자세한 내용은 [릴리스 정보](/help/release-notes/release-notes.md) 및 [사용자 지정 독립 실행형 설치](/help/sites-deploying/custom-standalone-install.md) 섹션을 검토하는 것이 좋습니다.
