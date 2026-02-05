---
title: 보조 노드 인증 설정(Elytron 기반)
description: JBoss EAP 8은 Elytron을 사용하여 주 도메인 컨트롤러와 보조 노드의 보안 통신 및 등록을 가능하게 합니다.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: f093f39fb535209297940cff13a99c7631812152
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 3%

---


# 보조 노드 인증 설정(Elytron 기반)

## Elytron을 사용하여 보조 노드 인증 구성

JBoss EAP 8은 **Elytron**&#x200B;을(를) 사용하여 클러스터된 배포에서 **기본 및 보조 노드** 간의 통신을 인증합니다. 이 구성을 통해 보조 노드를 주 도메인 컨트롤러에 안전하게 등록하고 통신할 수 있습니다.

환경 및 보안 요구 사항에 따라 두 가지 설정 옵션을 사용할 수 있습니다.


## 사전 요구 사항

* **기본 노드`secondary`**&#x200B;에 이름이 **인**&#x200B;관리 사용자를 만들어야 합니다.
* 보조 노드&#x200B;**에서만 이 구성**&#x200B;을(를) 수행합니다.
* 클러스터의 **각 보조 노드**&#x200B;에 대해 구성을 반복합니다.
* 기본 및 보조 노드 모두에서 **JBoss를 완전히 중지해야 합니다**.
* 모든 자격 증명 저장소 작업은 **오프라인 모드**&#x200B;에서 수행해야 합니다.

실행 중인 경우 JBoss를 중지하려면 다음을 수행합니다.

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux/UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

## 설정 옵션 선택

* **옵션 1: 기본 자격 증명 저장소를 사용하여 빠른 설정**
낮은 환경 및 테스트에 권장됩니다.

* **옵션 2: 사용자 지정 자격 증명 저장소 설정**
프로덕션 및 보안 환경에 권장됩니다.

## 옵션 1: 기본 자격 증명 저장소를 사용하여 빠른 설정

**적합한 항목:** 개발, 테스트 및 빠른 설정 시나리오

### 개요

* 기본 자격 증명 저장소 파일(`cs_secondary_hc.p12`)이 미리 구성되어 있습니다.
* 기본 자격 증명 저장소 암호가 `domain.conf`에 이미 설정되어 있습니다.
* 인증 암호 별칭만 추가해야 합니다.

### 구성 단계

#### 1단계: 기본 자격 증명 저장소 확인

기본 자격 증명 저장소 파일이 있는지 확인합니다.

* **Windows**

  ```
  <JBOSS_HOME>\domain\configuration\cs_secondary_hc.p12
  ```

* **Linux**

  ```
  <JBOSS_HOME>/domain/configuration/cs_secondary_hc.p12
  ```

파일이 없으면 **옵션 2**&#x200B;를 사용하십시오.

#### 2단계: 인증 암호 별칭 추가

`<JBOSS_HOME>/bin`에서 다음 명령을 실행합니다.

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

> 암호 값은 주 노드에서 `secondary` 사용자를 만들 때 사용된 암호와 일치해야 합니다.

#### 3단계: domain.conf 구성 확인

다음 항목이 이미 있는지 확인합니다(변경 필요 없음).

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=password"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=password"
  ```

#### 4단계: 노드 시작

1. **기본 노드**&#x200B;를 시작하고 완전히 초기화될 때까지 기다립니다.
2. **보조 노드**&#x200B;를 시작합니다.

### 인증

로그를 확인합니다.

* **기본 노드**

  ```
  <JBOSS_HOME>/domain/log/host-controller.log
  ```

  ```
  Registered remote secondary host "secondary"
  ```

* **보조 노드**

  ```
  Connected to primary host controller
  ```

## 옵션 2: 사용자 지정 자격 증명 저장소 설정(프로덕션)

**향상된 보안이 필요한** 프로덕션 환경에 가장 적합합니다.

### 구성 단계

#### 1단계: 기본 자격 증명 저장소 제거(있는 경우)

기본 자격 증명 저장소가 있으면 이름을 바꿉니다.

* **Windows**

  ```
  rename cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

* **Linux**

  ```
  mv cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

#### 2단계: 사용자 지정 자격 증명 저장소 만들기

`<JBOSS_HOME>/bin`부터:

* **Windows**

  ```
  elytron-tool.bat credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

#### 3단계: 인증 암호 별칭 추가

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

#### 4단계: domain.conf 업데이트

자격 증명 저장소 암호 참조 업데이트:

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=YourCustomPassword"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=YourCustomPassword"
  ```

#### 5단계: XML 구성 확인

`host-secondary.xml`에 구성된 자격 증명 저장소 및 인증 클라이언트 항목이 포함되어 있는지 확인하십시오.
기본 구성이 있는 경우 변경할 필요가 없습니다.


#### 6단계: 노드 시작

1. **기본 노드**&#x200B;를 시작하고 완전히 시작될 때까지 기다리십시오.
2. **보조 노드**&#x200B;를 시작합니다.

### 인증

두 노드의 호스트 컨트롤러 로그를 사용하여 성공적으로 등록했는지 확인합니다.

## 요약

* **옵션 1**&#x200B;은(는) 미리 구성된 자격 증명 저장소를 사용하여 빠른 설정을 제공합니다.
* **옵션 2**&#x200B;은(는) 사용자 지정 자격 증명 저장소 암호를 사용하여 더 강력한 보안을 사용합니다.
* **보조 노드에서만 구성을 완료해야 합니다**.
* 주 노드 구성은 도메인 전체에서 자동으로 재사용됩니다.

