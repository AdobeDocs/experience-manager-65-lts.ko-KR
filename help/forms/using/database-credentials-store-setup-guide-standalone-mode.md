---
title: 데이터베이스 자격 증명 저장소 설정 안내서(독립 실행형 모드)
description: 독립형 모드에서 JBoss/Red Hat EAP의 AEM Forms JEE에 대한 데이터베이스 자격 증명 저장소 설정을 찾습니다.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: 5d020671efaa4527a5f6dbb4b779c7a3351888a4
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# 데이터베이스 자격 증명 저장소 설정 안내서(독립 실행형 모드)

## 개요

이 안내서에서는 **독립 실행형 모드**&#x200B;에서 JBoss/Red Hat EAP의 AEM Forms JEE용 **데이터베이스 자격 증명 저장소 설정**&#x200B;에 대해 다룹니다. 수동 설치를 수행할 때 필요합니다.

**이 안내서는 다음을 다룹니다.**

- 데이터베이스 자격 증명 저장소(`cred-store.p12`)를 만드는 중
- 데이터베이스 암호 별칭을 안전하게 추가
- 자격 증명 저장소를 사용하도록 JBoss 구성

**중요:** 이러한 스크립트는 **오프라인 모드에서만 작동합니다**. 이러한 스크립트를 실행하기 전에 JBoss를 중지해야 합니다. 스크립트는 서버를 중지해야 하는 `embed-server` 모드를 사용합니다.

**참고:** 완전한 독립 실행형 설치 가이드는 **아님**&#x200B;입니다. 이 문서에서는 다음과 같이 가정합니다.

- JBoss가 이미 설치되었습니다.
- 독립 실행형 구성 파일(`lc_oracle.xml`, `lc_mysql.xml` 또는 `lc_mssql.xml`)이 이미 구성되어 있습니다.
- 데이터베이스가 설정되고 액세스할 수 있음

독립 실행형 설치 지침이 필요한 경우 기본 설치 안내서를 참조하십시오.

## 사전 요구 사항

이러한 스크립트를 실행하기 전에 다음을 확인하십시오.

1. **JBoss를 중지해야 함**
   - 이러한 스크립트는 **오프라인 모드에서만 작동합니다.**
   - 스크립트는 서버를 중지해야 하는 `embed-server`을(를) 사용합니다.
   - JBoss가 실행 중인 경우 스크립트가 실패합니다
   - JBoss가 실행 중인지 확인합니다.
      - Windows: `java.exe` 프로세스에 대한 작업 관리자 확인
      - Linux: `ps aux | grep jboss` 또는 `ps aux | grep java`
   - 실행 중인 경우 JBoss 중지:
      - JBoss가 실행 중인 터미널에서 `Ctrl+C`을(를) 누릅니다.
      - 또는 수동으로 프로세스를 중단합니다.

2. **데이터베이스 암호를 준비했습니다**

3. **자격 증명 저장소의 보안 암호를 결정했습니다**

4. **사용 중인 데이터베이스 구성 파일:**
   - `lc_oracle.xml`(Oracle 데이터베이스의 경우)
   - `lc_mysql.xml`(MySQL 데이터베이스용)
   - `lc_mssql.xml`(Microsoft SQL Server 데이터베이스용)

## 설정 단계

### 1단계: 데이터베이스 자격 증명 저장소 만들기

제공된 스크립트를 사용하여 데이터베이스 자격 증명 저장소를 생성하고 필요한 모든 암호 별칭을 추가합니다.

#### Windows:

**스크립트 위치:** `create-elytron-cred-standalone.bat`

`batch cd path\to\script\location create-elytron-cred-standalone.bat`

**스크립트에서 다음을 묻는 메시지를 표시합니다.**
1. **JBOSS_HOME 경로**(예: `C:\Adobe\Adobe_Experience_Manager_Forms\jboss`)
2. **구성 파일 이름**(예: `lc_oracle.xml`, `lc_mysql.xml` 또는 `lc_mssql.xml`)
3. **자격 증명 저장소 암호**(키 저장소 파일을 보호함 - 이 암호 기억)
4. **데이터베이스 암호**(실제 데이터베이스 암호)

**스크립트의 기능:**

- `JBOSS_HOME\standalone\configuration\cred-store.p12`에 자격 증명 저장소를 만듭니다.
- 자격 증명 저장소 생성을 사용하도록 구성 파일을 임시로 수정합니다.
- 데이터베이스 암호로 다음 별칭을 추가합니다.
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- 구성 파일을 원래 상태로 복원합니다.
- 모든 별칭이 추가되었는지 확인합니다.

#### Linux의 경우:

**스크립트 위치:** `create-elytron-cred-standalone.sh`

`bash cd /path/to/script/location chmod +x create-elytron-cred-standalone.sh./create-elytron-cred-standalone.sh`

**스크립트에서 다음을 묻는 메시지를 표시합니다.**

1. **JBOSS_HOME 경로**(예: `/opt/Adobe/Adobe_Experience_Manager_Forms/jboss`)
2. **구성 파일 이름**(예: `lc_oracle.xml`, `lc_mysql.xml` 또는 `lc_mssql.xml`)
3. **자격 증명 저장소 암호**(키 저장소 파일을 보호함 - 이 암호 기억)
4. **데이터베이스 암호**(실제 데이터베이스 암호)

**스크립트의 기능:**

- `JBOSS_HOME/standalone/configuration/cred-store.p12`에 자격 증명 저장소를 만듭니다.
- 자격 증명 저장소 생성을 사용하도록 구성 파일을 임시로 수정합니다.
- 데이터베이스 암호로 다음 별칭을 추가합니다.
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- 구성 파일을 원래 상태로 복원합니다.
- 모든 별칭이 추가되었는지 확인합니다.

**예상 출력:**

```
=== JBoss Elytron Credential Store Setup ===
Enter JBOSS_HOME path (e.g. /opt/jboss): /opt/Adobe/Adobe_Experience_Manager_Forms/jboss
Enter configuration file name (e.g. lc_oracle.xml): lc_oracle.xml
Enter credential store password: ********
Confirm credential store password: ********
Enter database password: ********
Creating credential store using JBoss CLI...
Adding aliases to credential store...
Verifying credential store aliases...

All 4 aliases verified successfully!
- EncryptDBPassword
- EncryptDBPassword_IDP_DS
- EncryptDBPassword_EDC_DS
- EncryptDBPassword_AEM_DS

Credential store setup completed successfully!
```

### 2단계: 독립형 구성 파일 업데이트

스크립트를 실행한 후 시작 시 자격 증명 저장소 암호를 읽도록 JBoss를 구성해야 합니다.

#### Windows:

**파일 위치:** `<JBOSS_HOME>\bin\standalone.conf.bat`

예: `C:\Adobe\Adobe_Experience_Manager_Forms\jboss\bin\standalone.conf.bat`

다음 줄을 추가하거나 업데이트합니다.

```batch
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=YourActualPassword123"
```

`YourActualPassword123`을(를) 1단계에서 사용한 **자격 증명 저장소 암호**(으)로 바꾸십시오.

#### Linux의 경우:

**파일 위치:** `<JBOSS_HOME>/bin/standalone.conf`

예: `/opt/Adobe/Adobe_Experience_Manager_Forms/jboss/bin/standalone.conf`

다음 줄을 추가하거나 업데이트합니다.

```bash
JAVA_OPTS="$JAVA_OPTS -DCS_PASS=YourActualPassword123"
```

`YourActualPassword123`을(를) 1단계에서 사용한 **자격 증명 저장소 암호**(으)로 바꾸십시오.

### 3단계: JBoss 시작

자격 증명 저장소 설정을 완료한 후 적절한 구성 파일로 JBoss를 시작합니다.

**참고:** 독립 실행형 모드에서 JBoss를 시작하기 위한 정확한 시작 명령 및 절차는 **기본 설치 안내서**&#x200B;를 참조하십시오. 시작 명령은 특정 구성 및 데이터베이스 유형(`lc_oracle.xml`, `lc_mysql.xml` 또는 `lc_mssql.xml`)에 따라 달라질 수 있습니다.

## 인증

### 서버 로그 확인

**로그 위치:**

- Windows: `<JBOSS_HOME>\standalone\log\server.log`
- Linux: `<JBOSS_HOME>/standalone/log/server.log`

**성공한 시작 메시지 찾기:**

```
INFO  [org.jboss.as.server] WFLYSRV0025: JBoss EAP started
INFO  [org.jboss.as.connector.deployers.jdbc] Bound data source [java:/AdobeDataSource]
```

**관련 오류 없음:**

- 자격 증명 저장소 로드 중
- 데이터베이스 연결
- 별칭 누락

## 문제 해결

### 문제 1: 자격 증명 저장소를 찾을 수 없음

**오류 메시지:**

```
ERROR Unable to load credential store
```

**솔루션:**

1. 자격 증명 저장소 파일이 있는지 확인합니다.
   - Windows: `dir <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux: `ls -l <JBOSS_HOME>/standalone/configuration/cred-store.p12`
2. 누락된 경우 자격 증명 저장소 생성 스크립트를 다시 실행합니다(1단계).

### 문제 2: 잘못된 자격 증명 저장소 암호

**오류 메시지:**

```
ERROR Unable to load credential store - Invalid password
```

**솔루션:**
`standalone.conf.bat` / `standalone.conf`(2단계)의 암호가 자격 증명 저장소를 만들 때 사용된 암호(1단계)와 일치하는지 확인하십시오.

**수정하려면:**
`standalone.conf.bat`/`standalone.conf`을(를) 편집하고 암호를 업데이트하십시오.

```
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=CorrectPassword"
```

### 문제 3: 데이터베이스 연결 실패

**오류 메시지:**

```
ERROR Failed to obtain connection
```

**솔루션:**

1. 자격 증명 저장소에 사용된 데이터베이스 암호가 올바른지 확인합니다.
2. 데이터 소스 구성이 올바른 별칭을 참조하는지 확인합니다.
3. 데이터베이스 서버에 대한 네트워크 연결 확인

**자격 증명 저장소를 다시 만들려면:**

1. JBoss 중지
2. 기존 자격 증명 저장소를 삭제합니다.
   - Windows: `del <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux: `rm <JBOSS_HOME>/standalone/configuration/cred-store.p12`
3. 올바른 데이터베이스 암호를 사용하여 자격 증명 저장소 만들기 스크립트를 다시 실행합니다.

### 문제 4: 실행 중 스크립트 실패

**오류 메시지:**

```
ERROR: jboss-cli.bat is not found
```

**솔루션:**
JBOSS_HOME 경로가 올바른지 확인하고 JBoss 설치 디렉토리를 가리킵니다.

**오류 메시지:**

```
ERROR: Configuration file not found
```

**솔루션:**

1. 구성 파일 이름이 올바른지 확인합니다.
2. 파일이 `JBOSS_HOME\standalone\configuration\` 디렉터리에 있는지 확인합니다.
3. 올바른 데이터베이스별 구성 파일을 사용하고 있는지 확인합니다.

## 빠른 참조

### 데이터베이스 자격 증명 저장소(독립 실행형 모드)

**목적:** 데이터베이스 암호를 안전하게 저장

**스크립트:**

- Windows: `create-elytron-cred-standalone.bat`
- Linux: `create-elytron-cred-standalone.sh`

**만들기:**

- 파일: `standalone/configuration/cred-store.p12`
- 별칭: `EncryptDBPassword`, `EncryptDBPassword_IDP_DS`, `EncryptDBPassword_EDC_DS`, `EncryptDBPassword_AEM_DS`

**구성:**

- 변수: `-DCS_PASS=password`
- 파일: `standalone.conf.bat`(Windows) 또는 `standalone.conf`(Linux)

