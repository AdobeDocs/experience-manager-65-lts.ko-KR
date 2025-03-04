---
title: 업그레이드 후 확인 및 문제 해결
description: 업그레이드 후 발생할 수 있는 문제를 해결하는 방법에 대해 알아봅니다.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 09b297721b08ef428f1ac8a26fec38d5a8bd34fd
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# 업그레이드 후 확인 및 문제 해결{#post-upgrade-checks-and-troubleshooting}

## 업그레이드 후 확인 {#post-upgrade-checks}

[바로 업그레이드](/help/sites-deploying/in-place-upgrade.md)를 수행한 후 다음 활동을 실행하여 업그레이드를 완료해야 합니다. AEM이 AEM 6.5 LTS jar로 시작되었고 업그레이드된 코드 베이스가 배포되었다고 가정됩니다.

* [업그레이드 성공을 위한 로그 확인](#verify-logs-for-upgrade-success)

* [OSGi 번들 확인](#verify-osgi-bundles)

* [Oak 버전 확인](#verify-oak-version)

* [페이지의 초기 유효성 검사](#initial-validation-of-pages)

* [예약된 유지 관리 구성 확인](#verify-scheduled-maintenance-configurations)

* [복제 에이전트 활성화](#enable-replication-agents)

* [사용자 지정 예약된 작업 활성화](#enable-custom-scheduled-jobs)

* [테스트 계획 실행](#execute-test-plan)


### 업그레이드 성공을 위한 로그 확인 {#verify-logs-for-upgrade-success}

**upgrade.log**

이전에는 인스턴스의 업그레이드 후 상태를 검사하려면 다양한 로그 파일, 저장소 일부 및 시작 패드를 주의 깊게 검사해야 했습니다. 업그레이드 후 보고서를 생성하면 실행 전 업그레이드 오류를 감지하는 데 도움이 될 수 있습니다.

이 기능의 주요 목적은 업그레이드의 성공을 검증하는 데 필요한 여러 엔드포인트 간에 수동 해석 또는 복잡한 구문 분석 논리의 필요성을 줄이는 것입니다. 이 솔루션은 외부 자동화 시스템이 업데이트의 성공 또는 식별된 실패에 반응할 수 있도록 모호하지 않은 정보를 제공하는 것을 목표로 합니다.

보다 구체적으로 설명하면 다음과 같습니다.

* 업그레이드 프레임워크에서 감지한 업그레이드 실패는 단일 업그레이드 보고서에서 중앙 집중화됩니다.
* 업그레이드 보고서에는 필요한 수동 개입에 대한 지표가 포함됩니다.

이를 위해 `upgrade.log` 파일에서 로그가 생성되는 방식이 변경되었습니다.

**error.log**

target 버전 jar를 사용하여 AEM을 시작할 때 및 그 이후에 error.log를 주의 깊게 검토해야 합니다. 모든 경고 또는 오류를 검토해야 합니다. 일반적으로 로그 시작 부분에서 문제를 찾는 것이 가장 좋습니다. 로그 후반부에 발생하는 오류는 실제로 파일의 초기에 호출되는 근본 원인의 부작용일 수 있습니다. 반복되는 오류와 경고가 발생하면 아래를 참조하여 [업그레이드 관련 문제 분석](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade)을 확인하십시오.

### OSGi 번들 확인 {#verify-osgi-bundles}

OSGi 콘솔 `/system/console/bundles`(으)로 이동하여 번들이 시작되지 않았는지 확인하십시오. 설치된 상태의 번들이 있는 경우 `error.log`을(를) 참조하여 루트 문제를 확인하십시오.

### Oak 버전 확인 {#verify-oak-version}

업그레이드 후 Oak 버전이 **1.68.1-B002**(으)로 업데이트되었습니다. Oak 버전을 확인하려면 OSGi 콘솔로 이동하여 Oak 번들과 연결된 버전(Oak 코어, Oak Commons, Oak 세그먼트 Tar)을 확인합니다.

### 페이지의 초기 유효성 검사 {#initial-validation-of-pages}

AEM의 여러 페이지에 대해 초기 유효성 검사를 수행합니다. 작성자 환경을 업그레이드하는 경우 시작 페이지 및 시작 페이지(`/aem/start.html`, `/libs/cq/core/content/welcome.html`)를 엽니다. 작성자 및 게시 환경 모두에서 몇 개의 애플리케이션 페이지를 열고 올바르게 렌더링하는 스모크 테스트를 수행합니다. 문제가 발생하면 `error.log`에게 문의하여 문제를 해결하십시오.

### 예약된 유지 관리 구성 확인 {#verify-scheduled-maintenance-configurations}

#### 데이터 저장소 가비지 수집 활성화 {#enable-data-store-garbage-collection}

파일 데이터 저장소를 사용하는 경우 데이터 저장소 가비지 수집 작업이 활성화되어 있고 주간 유지 관리 목록에 추가되었는지 확인하십시오. 지침은 [수정 정리](/help/sites-administering/data-store-garbage-collection.md)에서 요약되어 있습니다.

>[!NOTE]
>
>S3 사용자 지정 데이터 저장소 설치 또는 공유 데이터 저장소를 사용할 경우에는 권장되지 않습니다.

#### 온라인 개정 정리 사용 {#enable-online-revision-cleanup}

MongoMK 또는 새 TarMK 세그먼트 형식을 사용하는 경우, 개정 정리 작업이 사용으로 설정되어 있고 일별 유지 관리 목록에 추가되어 있는지 확인합니다. 지침은 [수정 정리](/help/sites-deploying/revision-cleanup.md)에서 요약되어 있습니다.

### 복제 에이전트 활성화 {#enable-replication-agents}

게시 환경이 완전히 업그레이드되고 유효성이 확인되면 작성자 환경에서 복제 에이전트를 활성화합니다. 에이전트가 각각의 게시 인스턴스에 연결할 수 있는지 확인합니다. 이벤트 순서에 대한 자세한 내용은 [업그레이드 프로시저](/help/sites-deploying/upgrade-procedure.md)를 참조하세요.

### 사용자 지정 예약된 작업 활성화 {#enable-custom-scheduled-jobs}

이때 코드 베이스의 일부로 예약된 모든 작업을 활성화할 수 있습니다.

### 테스트 계획 실행 {#execute-test-plan}

**테스트 프로시저** 섹션](/help/sites-deploying/upgrading-code-and-customizations.md#testing-procedure-testing-procedure)에서 [코드 및 사용자 지정 업그레이드에 정의된 대로 자세한 테스트 계획을 실행하십시오.

## 업그레이드 관련 문제 분석 {#analyzing-issues-with-the-upgrade}

이 섹션에는 AEM 6.5 LTS로의 업그레이드 절차 시 발생할 수 있는 몇 가지 문제 시나리오가 포함되어 있습니다.

### 패키지 및 번들 업데이트 실패  {#packages-and-bundles-fail-to-update}

업그레이드 중에 패키지를 설치하지 못하는 경우 패키지가 포함된 번들도 업데이트되지 않습니다. 이 범주의 문제는 데이터 저장소의 잘못된 구성으로 인해 발생합니다. 또한 error.log에는 **ERROR** 및 **WARN** 메시지로 표시됩니다. 이러한 대부분의 경우 기본 로그인이 작동하지 않을 수 있으므로 CRXDE를 직접 사용하여 구성 문제를 검사하고 찾을 수 있습니다.

### 업그레이드가 실행되지 않았습니다. {#the-upgrade-did-not-run}

준비 단계를 시작하기 전에 먼저 `java -jar aem-quickstart.jar` 명령으로 실행하여 **source** 인스턴스를 실행해야 합니다. 이 작업은 quickstart.properties 파일이 제대로 생성되었는지 확인하는 데 필요합니다. 누락된 경우 업그레이드가 작동하지 않습니다. 또는 소스 인스턴스의 설치 폴더에서 `crx-quickstart/conf` 아래에서 파일을 찾아 파일이 있는지 확인할 수 있습니다. 또한 업그레이드를 시작하기 위해 AEM을 시작할 때 `java -jar <aem-quickstart-6.5-LTS.jar>` 명령을 사용하여 실행해야 합니다. 시작 스크립트에서 시작해도 업그레이드 모드에서 AEM이 시작되지 않습니다.

### 일부 AEM 번들이 활성 상태로 전환되지 않음 {#some-aem-bundles-are-not-switching-to-the-active-state}

시작되지 않는 번들이 있는 경우 충족되지 않은 종속성이 있는지 확인하십시오.

이 문제가 있지만 패키지 설치 실패로 번들이 업그레이드되지 않는 경우 새 버전과 호환되지 않는 것으로 간주됩니다. 이 문제를 해결하는 방법에 대한 자세한 내용은 위의 **패키지 및 번들 업데이트 실패**&#x200B;를 참조하십시오.

또한 새로운 AEM 6.5 LTS 인스턴스의 번들 목록을 업그레이드된 인스턴스와 비교하여 업그레이드되지 않은 번들을 감지하는 것이 좋습니다. 이를 통해 `error.log`에서 검색할 내용의 범위가 더 넓어집니다.

### 사용자 정의 번들이 활성 상태로 전환되지 않음 {#custom-bundles-not-switching-to-the-active-state}

사용자 정의 번들이 활성 상태로 전환되지 않는 경우, 변경된 API를 가져오지 않는 코드가 있을 수 있습니다. 이는 종종 충족되지 않은 종속성을 초래할 것입니다.

또한 문제를 일으킨 변경 사항이 필요한지 확인하고 필요하지 않은 경우 되돌리는 것이 가장 좋습니다. 또한 엄격한 의미 체계 버전 관리를 따라 패키지 내보내기의 버전 증가가 필요 이상으로 증가했는지 확인하십시오.

### error.log 및 upgrade.log 분석 중 {#analyzing-the-error.log-and-upgrade.log}

대부분의 경우 오류의 원인을 찾기 위해 로그를 참조해야 합니다. 그러나 업그레이드 시 이전 번들이 제대로 업그레이드되지 않을 수 있으므로 종속성 문제를 모니터링해야 합니다.

이를 수행하는 가장 좋은 방법은 직면한 문제와 관련이 없을 것으로 예상되는 모든 메시지를 제거하여 error.log를 제거하는 것입니다. 다음을 사용하여 grep과 같은 도구를 통해 이 작업을 수행할 수 있습니다.

```shell
grep -v UnrelatedErrorString
```

일부 오류 메시지는 즉시 설명되지 않을 수 있습니다. 이 경우 오류가 발생한 컨텍스트를 살펴보는 것도 오류가 어디에서 생성되었는지 이해하는 데 도움이 될 수 있습니다. 다음을 사용하여 오류를 구분할 수 있습니다.

* 오류 앞에 줄을 추가하는 경우 `grep -B`

또는

* `grep -A`(이후에 줄 추가).

이 상태로 이어지는 유효한 경우가 있을 수 있고 애플리케이션이 항상 실제 오류인지 여부를 결정할 수 없으므로 몇 가지 경우에 오류가 발견될 수 있습니다. 경고 메시지. 이 메시지도 반드시 확인하십시오.

### Adobe 지원 센터 문의 {#contacting-adobe-support}

이 페이지에 대한 조언을 살펴보았으나 문제가 계속 발생하는 경우 Adobe 지원 센터에 문의하십시오. 귀하의 서비스 케이스를 담당하는 지원 엔지니어에게 최대한 많은 정보를 제공하려면 업그레이드의 `error.log` 및 `upgrade.log` 파일을 포함해야 합니다.
