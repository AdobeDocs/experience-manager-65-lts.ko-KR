---
title: 업그레이드 계획
description: 이 문서는 AEM 업그레이드를 계획할 때 명확한 목표, 단계 및 결과물을 설정하는 데 도움이 됩니다.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: ac803ef9ac38380d7ce7fdf4490c428fd0039688
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# 업그레이드 계획 {#planning-your-upgrade}

## AEM 업그레이드 개요 {#aem-upgrade-overview}

AEM은 수백만 명의 사용자에게 제공될 수 있는 영향력이 큰 배포에서 종종 사용됩니다. 일반적으로 인스턴스에 배포되는 사용자 정의 애플리케이션이 있어 복잡성을 가중시킵니다. 이러한 배포를 업그레이드하기 위한 모든 노력은 체계적으로 처리되어야 합니다.

이 안내서는 업그레이드를 계획할 때 명확한 목표, 단계 및 결과물을 설정하는 데 도움이 됩니다. 전반적인 업그레이드 실행 및 지침에 중점을 둡니다. 실제 업그레이드 단계에 대한 개요를 제공하지만 적합한 경우 사용 가능한 기술 리소스를 참조합니다. 이 설명서는 문서에서 언급한 사용 가능한 기술 리소스와 함께 사용해야 합니다.

AEM 업그레이드 프로세스는 각 단계에 대해 정의된 주요 결과물을 통해 계획, 분석 및 실행 단계를 신중하게 처리해야 합니다.

>[!NOTE]
>
>AEM 6.5 LTS로의 업그레이드는 마지막 6개의 서비스 팩에서 지원됩니다

지원되는 운영 체제, Java™ 런타임, httpd 및 Dispatcher 버전을 실행 중인지 확인하는 것이 중요합니다. 자세한 내용은 [AEM 6.5 LTS에 대한 기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하세요. 이러한 구성 요소 업그레이드는 업그레이드 계획에서 고려해야 하며 AEM을 업그레이드하기 전에 수행해야 합니다.

<!-- Alexandru: drafting for now

## Upgrade Scope and Requirements {#upgrade-scope-requirements}

Below you will find a list of areas that are impacted in a typical AEM Upgrade project:

<table>
 <tbody>
  <tr>
   <td><strong>Component</strong></td>
   <td><strong>Impact</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>Operating System</td>
   <td>Uncertain, but subtle effects</td>
   <td>At the time of the AEM upgrade, it may be time to upgrade the operating system as well and this might have some impact.</td>
  </tr>
  <tr>
   <td>Java&trade; Runtime</td>
   <td>Moderate Impact</td>
   <td>AEM 6.3 requires JRE 1.7.x (64 bit) or later. JRE 1.8 is the only version currently supported by Oracle.</td>
  </tr>
  <tr>
   <td>Hardware</td>
   <td>Moderate Impact</td>
   <td>Online Revision Cleanup requires free<br /> disk space equal to 25% of the repository's size and 15% free heap space<br /> to complete successfully. You may need to upgrade your hardware to<br /> ensure sufficient resources for Online Revision Cleanup to fully<br /> run. Also, if upgrading from a version prior to AEM 6, there<br /> may be additional storage requirements.</td>
  </tr>
  <tr>
   <td>Content Repository (CRX or Oak)</td>
   <td>High Impact</td>
   <td>Starting from version 6.1, AEM does not support CRX2, so a migration to<br /> Oak (CRX3) is required if upgrading from an older version. AEM 6.3 has<br /> implemented a new Segment Node Store that also requires a migration. The<br /> crx2oak tool is used for this purpose.</td>
  </tr>
  <tr>
   <td>AEM Components/Content</td>
   <td>Moderate Impact</td>
   <td><code>/libs</code> and <code>/apps</code> are easily handled through the upgrade, but <code>/etc</code> usually requires some manual reapplication of customizations.</td>
  </tr>
  <tr>
   <td>AEM Services</td>
   <td>Low Impact</td>
   <td>Most AEM core services are tested for upgrade. This is an area of low impact.</td>
  </tr>
  <tr>
   <td>Custom Application Services</td>
   <td>Low to High Impact</td>
   <td>Depending on the application and customization, there may be<br /> dependencies on JVM, operating system versions, and some indexing related<br /> changes, as indexes are not generated automatically in Oak.</td>
  </tr>
  <tr>
   <td>Custom Application Content</td>
   <td>Low to High Impact</td>
   <td>Content that will not be handled through the upgrade can be backed up<br /> before the upgrade takes place and then moved back into the repository.<br /> Most content can be handled through the migration tool.</td>
  </tr>
 </tbody>
</table>

It is important to ensure that you are running a supported operating system, Java&trade; runtime, httpd, and Dispatcher version. For more information, see the [AEM 6.5 Technical Requirements page](/help/sites-deploying/technical-requirements.md). Upgrading these components must be accounted for in your project plan and should take place before upgrading AEM. -->

## 업그레이드 단계 {#upgrade-phases}

AEM 업그레이드 계획 및 실행에 많은 작업이 필요합니다. Adobe은 이 프로세스에 들어가는 다양한 노력을 명확히 하기 위해 계획 및 실행 연습을 별도의 단계로 분류했습니다. 아래 섹션에서 각 단계는 업그레이드의 향후 단계에서 자주 사용되는 결과물을 생성합니다.

<!-- Alexandru:drafting for now

### Planning for Author Training {#planning-for-author-training}

With any new release, there are potential changes to the UI and user workflows that may be introduced. Also, new releases introduce new features that may be beneficial for the business to use. Adobe recommends reviewing the functional changes that have been introduced and organizing a plan to train your users on using them effectively.

![unu_cropped](assets/unu_cropped.png)

New features in AEM 6.5 can be found in [the AEM section of adobe.com](/help/release-notes/release-notes.md). Make sure to note any changes to UIs or product features that are commonly used in your organization. As you look through the new features, also take note of any that can be of value to your organization. After looking through what has changed in AEM 6.5, develop a training plan for your authors. This could involve using freely available resources like the help feature videos or formal training offered through [Adobe Digital Learning Services](https://learning.adobe.com/). -->

### 테스트 계획 만들기 {#creating-a-test-plan}

각 고객의 AEM 구현은 고유하며 비즈니스 요구 사항을 충족하도록 사용자 정의되었습니다. 따라서 테스트 계획에 포함될 수 있도록 시스템에 적용된 모든 사용자 지정을 결정하는 것이 중요합니다.

모든 애플리케이션과 사용자 정의 코드가 원하는 대로 계속 실행되는지 확인하려면 업그레이드 후 정확한 프로덕션 환경을 복제하고 테스트해야 합니다. 모든 사용자 지정을 취소하고 성능, 로드 및 보안 테스트를 실행합니다. 테스트 계획을 구성할 때는 일상적인 작업에 사용되는 기본 UI 및 워크플로뿐만 아니라 시스템에 적용된 모든 사용자 지정 사항도 다루어야 합니다. 여기에는 사용자 지정 OSGI 서비스 및 서블릿, Adobe Experience Cloud에 대한 통합, AEM 커넥터를 통한 서드파티와의 통합, 사용자 지정 서드파티 통합, 사용자 지정 구성 요소 및 템플릿, AEM의 사용자 지정 UI 오버레이 및 사용자 지정 워크플로가 포함될 수 있습니다. 또한 사용자 정의 쿼리는 업그레이드 후에도 색인이 계속 효과적으로 작동하는지 확인하기 위해 계속 테스트해야 합니다.

### 업그레이드 복잡성 평가 {#assessing-upgrade-complexity}

Adobe 고객이 AEM 환경에 적용하는 맞춤화의 양과 특성이 매우 다양하므로, 업그레이드 시 예상되는 전반적인 작업 수준을 파악하기 위해 미리 시간을 투자하는 것이 중요합니다. [AEM 6.5 LTS용 AEM 분석기](/help/sites-deploying/pattern-detector.md)를 통해 업그레이드의 복잡성을 평가할 수 있습니다.

[AEM 6.5 LTS용 AEM Analyzer](/help/sites-deploying/pattern-detector.md)을(를) 사용하면 대부분의 경우 업그레이드 중에 예상할 수 있는 사항을 상당히 정확하게 예측할 수 있습니다. 그러나 변경 내용이 호환되지 않는 복잡한 사용자 지정 및 배포의 경우 [바로 업그레이드 수행](/help/sites-deploying/in-place-upgrade.md)의 지침에 따라 개발 인스턴스를 AEM 6.5 LTS로 업그레이드할 수 있습니다. 완료되면 이 환경에서 높은 수준의 스모크 테스트를 수행합니다. 이 연습의 목표는 테스트 사례 인벤토리를 완전히 완료하고 정식 결함 인벤토리를 작성하는 것이 아니라 AEM 6.5 LTS 호환성에 대한 코드를 업그레이드하는 데 필요한 작업 양에 대한 대략적인 견적을 제공하는 것입니다. [AEM 분석기](/help/sites-deploying/pattern-detector.md) 및 이전 섹션에서 결정된 아키텍처 변경 사항과 결합하면 프로젝트 관리 팀에 대략적인 견적을 제공하여 업그레이드를 계획할 수 있습니다.

### 업그레이드 및 롤백 Runbook 구축 {#building-the-upgrade-and-rollback-runbook}

Adobe은 AEM 인스턴스 업그레이드 프로세스를 문서화했지만 각 고객의 네트워크 레이아웃, 배포 아키텍처 및 맞춤화는 이 접근 방식을 미세 조정하고 맞춤화해야 합니다. 따라서 Adobe에서는 제공된 모든 설명서를 검토하고 이를 사용하여 사용자 환경에서 수행할 특정 업그레이드 및 롤백 절차를 요약한 업그레이드별 Runbook을 알릴 것을 권장합니다.

<!--Alexandru:drafting for now

![runbook-diagram](assets/runbook-diagram.png) -->

Adobe은 [업그레이드 프로시저](/help/sites-deploying/upgrade-procedure.md)의 업그레이드 및 롤백 절차와 [바로 업그레이드 수행](/help/sites-deploying/in-place-upgrade.md)에서 업그레이드를 적용하기 위한 단계별 지침을 제공했습니다. 업그레이드 중에 실행할 적절한 전환 및 롤백 절차를 결정하려면 시스템 아키텍처, 사용자 정의 및 가동 중지 시간 허용 범위와 함께 이러한 지침을 검토하고 고려해야 합니다. 사용자 지정된 Runbook을 작성할 때 아키텍처 또는 서버 크기에 대한 모든 변경 사항을 포함해야 합니다.

### 업그레이드 계획 개발 {#developing-an-upgrade-plan}

이전 연습의 결과를 사용하여 테스트 또는 개발 노력의 예상 타임라인 및 실제 업그레이드 실행을 다루는 업그레이드 계획을 작성할 수 있습니다.

<!--Alexandru: drafting for now

![develop-project-plan](assets/develop-project-plan.png) -->

포괄적인 프로젝트 계획에는 다음이 포함되어야 합니다.

* 개발 및 테스트 계획 확정
* 개발 및 QA 환경 업그레이드
* AEM 6.5 LTS에 대한 사용자 지정 코드 베이스 업데이트
* QA 테스트 및 수정 주기
* 스테이징 환경 업그레이드
* 통합, 성능 및 로드 테스트
* 환경 인증
* 라이브 진행

### 개발 및 QA 수행 {#performing-development-and-qa}

Adobe은 [코드 및 사용자 지정 업그레이드](/help/sites-deploying/upgrading-code-and-customizations.md)를 위한 절차를 AEM 6.5 LTS와 호환되도록 제공했습니다. 이 반복 프로세스가 실행되면 필요에 따라 Runbook을 변경해야 합니다.

<!--Alexandru: drafting for now

![patru_cropped](assets/patru_cropped.png) -->

개발 및 테스트 프로세스는 일반적으로 반복적인 프로세스입니다. 업그레이드 프로세스를 조정해야 하는 문제가 발견되면 사용자 지정 업그레이드 Runbook에 추가해야 합니다. 테스트 및 수정을 여러 번 반복한 후 코드 베이스의 유효성을 완전히 검사하고 스테이징 환경에 배포할 준비가 되어야 합니다.

### 최종 테스트 {#final-testing}

Adobe은 코드베이스가 조직의 QA 팀에서 인증한 후 최종 테스트를 수행할 것을 권장합니다. 이 테스트에는 스테이징 환경에서 Runbook의 유효성을 검사한 다음 사용자 승인, 성능 및 보안 테스트를 수행하는 작업이 포함됩니다.

<!--Alexandru: drafting for now

![cinci_cropped](assets/cinci_cropped.png) -->

이 단계는 프로덕션 유사 환경에 대해 Runbook의 단계를 확인할 수 있는 유일한 시간이므로 중요합니다. 환경이 업그레이드되면 최종 사용자가 일상적인 활동에서 시스템을 사용할 때 로그인하고 수행하는 활동을 수행할 수 있는 시간을 갖도록 하는 것이 중요합니다. 가동 전에 이러한 영역에서 문제를 찾아 수정하면 많은 비용이 드는 생산 중단을 방지하는 데 도움이 될 수 있습니다.

### 업그레이드 수행 {#performing-the-upgrade}

모든 이해 당사자로부터 최종 승인을 받은 후에는 정의된 Runbook 프로시저에서 실행할 차례입니다. Adobe은 [업그레이드 프로시저](/help/sites-deploying/upgrade-procedure.md)의 업그레이드 및 롤백에 대한 단계와 [바로 업그레이드 수행](/help/sites-deploying/in-place-upgrade.md)의 설치 단계를 참조점으로 제공했습니다.

![업그레이드 수행](assets/perform-upgrade.png)

Adobe은 환경 유효성 검사에 대한 업그레이드 지침에 몇 가지 단계를 제공했습니다. 여기에는 업그레이드 로그 스캔 및 모든 OSGi 번들이 제대로 시작되었는지 확인하는 것과 같은 기본 검사가 포함되지만, Adobe에서는 비즈니스 프로세스를 기반으로 자체 테스트 사례로 확인하는 것을 권장합니다. Adobe은 또한 AEM의 온라인 수정 정리 일정 및 관련 루틴을 확인하여 회사의 조용한 시간 동안 발생할 수 있도록 할 것을 권장합니다. 이러한 루틴은 AEM의 장기적인 성능에 필수적입니다.
