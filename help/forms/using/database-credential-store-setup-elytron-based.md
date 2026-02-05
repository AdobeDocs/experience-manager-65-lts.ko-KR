---
title: 데이터베이스 자격 증명 저장소 설정(Elytron 기반)
description: JBoss EAP 8은 도메인 모드 설정을 위해 AEM Forms에서 보안 데이터베이스 암호 관리를 위한 Elytron 자격 증명 저장소를 지원합니다.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: f093f39fb535209297940cff13a99c7631812152
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 2%

---


# 데이터베이스 자격 증명 저장소 설정(Elytron 기반)

## Elytron을 사용하여 데이터베이스 자격 증명 저장소 구성

JBoss EAP 8은 **Elytron 자격 증명 저장소**&#x200B;를 사용하여 AEM Forms 배포에 대한 데이터베이스 암호를 안전하게 관리합니다. Adobe은 도메인 모드에서 Elytron 기반 자격 증명 저장소의 만들기 및 구성을 단순화할 수 있도록 **자동화된 스크립트**&#x200B;를 제공합니다.


JBoss 도메인 컨트롤러&#x200B;**를 시작하기 전에**&#x200B;이 설치를 완료해야 합니다.

### 사전 요구 사항

* 자격 증명 저장소 생성 스크립트를 실행하기 전에 **JBoss 서버를 완전히 중지해야 합니다**.
* 자격 증명 저장소를 만들려면 **오프라인 모드에서만**&#x200B;해야 합니다.

실행 중인 경우 JBoss를 중지하려면 다음을 수행합니다.

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux/UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

### 스크립트 다운로드

운영 체제에 따라 적절한 스크립트를 다운로드합니다.

| 스크립트 이름 | 운영 체제 |
| -------------------------------- | ---------------- |
| `create-elytron-cred-domain.bat` | Windows |
| `create-elytron-cred-domain.sh` | Linux / UNIX |

Linux의 경우 스크립트를 실행 파일로 만듭니다.

```
chmod +x create-elytron-cred-domain.sh
```

### 구성 단계

#### 1단계: 스크립트 다운로드 및 배치

적절한 스크립트를 다운로드하고 다음 디렉토리에 넣습니다.

```
<JBOSS_HOME>/bin
```

#### 2단계: 스크립트 실행

* **Windows**

  ```
  cd <JBOSS_HOME>\bin
  create-elytron-cred-domain.bat
  ```

* **Linux/UNIX**

  ```
  cd <JBOSS_HOME>/bin
  ./create-elytron-cred-domain.sh
  ```

#### 3단계: 필요한 정보 제공

실행 중에 스크립트는 다음 입력을 묻는 메시지를 표시합니다.

1. **JBOSS_HOME 경로**
JBoss 설치 디렉토리의 전체 경로를 입력합니다.

2. **데이터베이스 구성 파일 이름**
데이터베이스를 기반으로 다음 중 하나를 입력합니다.

   * `domain_oracle.xml`
   * `domain_mysql.xml`
   * `domain_mssql.xml`

3. **자격 증명 저장소 암호**
자격 증명 저장소를 보호하려면 강력한 암호를 입력하십시오.

   > 이 암호는 입력 중에 숨겨지므로 이후 단계를 위해 기억해야 합니다.

4. **데이터베이스 암호**
실제 데이터베이스 연결 암호를 입력합니다.

#### 4단계: 스크립트 실행 및 유효성 검사

스크립트는 다음 작업을 자동으로 수행합니다.

* 다음 위치에 `cred-store.p12`을(를) 만듭니다.

  ```
  <JBOSS_HOME>/domain/configuration/
  ```

* 다음 자격 증명 별칭을 만듭니다.

   * `EncryptDBPassword`
   * `EncryptDBPassword_IDP_DS`
   * `EncryptDBPassword_EDC_DS`
   * `EncryptDBPassword_AEM_DS`
* 모든 별칭이 추가되었는지 확인합니다.

실행이 성공하면 자격 증명 저장소 만들기와 별칭 확인이 확인됩니다.

#### 5단계: JVM 옵션 구성

JBoss 도메인 시작 구성을 업데이트하여 자격 증명 저장소 암호를 제공합니다.

* **Linux**
편집:

  ```
  <JBOSS_HOME>/bin/domain.conf
  ```

  추가:

  ```
  JAVA_OPTS="$JAVA_OPTS -DCS_PASS=YourCredStorePassword"
  ```

* **Windows**
편집:

  ```
  <JBOSS_HOME>/bin/domain.conf.bat
  ```

  추가:

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=YourCredStorePassword"
  ```

자격 증명 저장소를 만드는 동안 입력한 암호로 `YourCredStorePassword`을(를) 바꾸십시오.

도메인 구성 파일이 `${CS_PASS}` 변수를 사용하여 이 값을 참조합니다.


#### 6단계: 도메인 구성 확인

데이터베이스 도메인 구성 파일을 엽니다.

```
<JBOSS_HOME>/domain/configuration/<domain_*.xml>
```

데이터 소스가 Elytron 자격 증명 저장소를 참조하는지 확인합니다.

```xml
<security>
    <user-name>your_database_username</user-name>
    <credential-reference store="db-creds" alias="EncryptDBPassword_IDP_DS"/>
</security>
```

각 데이터 소스는 특정 별칭을 사용합니다.

* **IDP_DS:** `EncryptDBPassword_IDP_DS`
* **EDC_DS:** `EncryptDBPassword_EDC_DS`
* **AEM_DS:** `EncryptDBPassword_AEM_DS`
* **DefaultDS / ExampleDS:** `EncryptDBPassword`

모든 별칭은 자격 증명 저장소에 저장된 동일한 데이터베이스 암호를 참조합니다.

>[!NOTE]
>
>* 기본 노드에서만 자격 증명 저장소를 구성합니다.
>* 보조 노드는 주 노드에서 동기화된 도메인 구성을 자동으로 사용합니다.
