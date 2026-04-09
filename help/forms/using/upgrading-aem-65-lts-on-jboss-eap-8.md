---
title: JBoss EAP 8(Windows)에서 AEM 6.5 LTS 업그레이드
description: 이 안내서에서는 JDK 21을 사용하여 기존 Adobe Experience Manager(AEM) 6.5 LTS 설치를 JBoss EAP 7.4에서 Windows의 JBoss EAP 8로 업그레이드하는 단계별 지침을 제공합니다.
source-git-commit: 835530039678bc16a6de87b8d580be91a2026f94
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 3%

---

# JBoss EAP 8(Windows)에서 AEM 6.5 LTS 업그레이드

## 개요

이 안내서에서는 JDK 21을 사용하여 기존 Adobe Experience Manager(AEM) 6.5 LTS 설치를 JBoss EAP 7.4에서 Windows의 JBoss EAP 8로 업그레이드하는 단계별 지침을 제공합니다.

**업그레이드 경로:** JBoss EAP 7.4(JDK 11) → JBoss EAP 8(JDK 21)

## 중요 공지

>[!NOTE]
>
>이는 중요한 업그레이드 절차입니다. 항상 비프로덕션 환경에서 이 업그레이드를 먼저 수행하고 전체 백업을 유지합니다.
>
> ** 전제 조건:** 계속하기 전에 시스템 백업을 완료하고 문서화된 롤백 계획을 작성해야 합니다.

## 업그레이드 전 요구 사항

### 시스템 요구 사항

| 구성 요소 | 요구 사항 |
|-----------|-------------|
| 운영 체제 | Windows Server 2016 이상(64비트) |
| Source 환경 | JBoss EAP 7.4, AEM 6.5 LTS |
| 대상 환경 | JBoss EAP 8.x |
| Java 개발 키트 | JDK 21(Oracle 또는 OpenJDK) |
| AEM 버전 | AEM 6.5 서비스 팩(최신 권장) |
| 디스크 공간 | 업그레이드 프로세스를 위한 최소 50GB 여유 공간 |

### 필수 다운로드

업그레이드를 시작하기 전에 다음 사항을 확인하십시오.

1. **JBoss EAP 8.0 배포**\
   다운로드 위치: [https://developers.redhat.com/products/eap/download](https://developers.redhat.com/products/eap/download)

2. **JDK 21 설치 관리자**\
   Oracle JDK 21 또는 OpenJDK 21 for Windows(64비트) 다운로드

3. **AEM 6.5 LTS WAR 파일**\
   Adobe 소프트웨어 배포에서 최신 AEM 6.5 서비스 팩 WAR 받기

## 1단계: 전체 백업 만들기

>[!IMPORTANT]
>
> 계속하기 전에 포괄적인 백업을 수행합니다.

### 백업 검사 목록

- [ ] 기존 JBoss EAP 7.4 설치 디렉터리의 전체 백업
- [ ] 폴더의 `crx-repository` 백업
- [ ] 폴더의 `crx-quickstart` 백업
- [ 모든 사용자 지정 구성의 ] 내보내기
- [ ] 데이터베이스 백업(외부 데이터베이스를 사용하는 경우)
- [ ] 문서 현재 시스템 상태 및 구성

### 백업 만들기

```cmd
# Example backup location
C:\AEM-Backups\Pre-Upgrade-<date>

# Copy entire JBoss 7.4 directory
xcopy "C:\jboss-eap-7.4" "C:\AEM-Backups\Pre-Upgrade-<date>\jboss-eap-7.4" /E /I /H
```

**권장:** 별도의 드라이브 또는 네트워크 위치에 백업을 저장합니다.

## 2단계: JBoss EAP 8 설치

### JBoss EAP 8 추출

1. JBoss EAP 8 ZIP 배포를 대상 설치 디렉터리로 추출합니다.

   ```
   C:\jboss-eap-8.0
   ```

2. 이 안내서 전체에서 사용할 디렉터리 경로는 `<JBOSS_HOME>`입니다.

### 디렉터리 구조 복제

새 JBoss EAP 8 설치에 이전 JBoss EAP 7.4 설정과 동일한 사용자 지정 디렉토리 구조가 있는지 확인합니다. 특히

- 사용자 지정 배포 디렉터리
- 외부 구성 폴더
- 로그 파일 위치
- 모든 사용자 지정 모듈 또는 라이브러리

## 3단계: 저장소 데이터 마이그레이션

### CRX 저장소 복사

1. 기존 JBoss EAP 7.4 설치로 이동합니다.

   ```
   <OLD_JBOSS_HOME>\bin\crx-repository
   ```

2. 전체 `crx-repository` 폴더를 새 JBoss EAP 8 설치에 복사합니다.

   ```cmd
   xcopy "C:\jboss-eap-7.4\bin\crx-repository" "C:\jboss-eap-8.0\bin\crx-repository" /E /I /H
   ```

**중요:** 이 폴더에는 콘텐츠 저장소가 있으므로 완전히 전송해야 합니다.

### 저장소 복사본 확인

복사 후 저장소 크기 및 구조가 소스와 일치하는지 확인합니다.

```cmd
dir "C:\jboss-eap-8.0\bin\crx-repository" /s
```

## 4단계: AEM 인스턴스 중지

변경하기 전에 AEM이 완전히 중지되었는지 확인하십시오.

### Windows 서비스를 통해 중지

1. **서비스** 열기(실행: `services.msc`)
2. AEM/JBoss 서비스 찾기
3. 마우스 오른쪽 단추를 클릭하고 **중지** 선택
4. 서비스가 완전히 중지될 때까지 대기

### 명령줄을 통해 중지

AEM이 수동으로 시작된 경우:

1. JBoss 콘솔 창으로 이동합니다.
2. `Ctrl+C` 누르기
3. 정상 종료가 완료될 때까지 대기

### 종료 확인

Java 프로세스가 더 이상 실행되고 있지 않은지 확인합니다.

```cmd
tasklist | findstr java
```

## 5단계: 이전 AEM 파일 정리

`crx-quickstart` 디렉터리에서 오래된 파일을 제거하여 깔끔하게 업그레이드하십시오.

>[!CAUTION]
>
> 아래 나열된 특정 파일 및 폴더만 삭제합니다. 다른 구성 파일, 사용자 지정 코드 또는 저장소 데이터를 제거하지 마십시오.

### 5.1 Launchpad 시작 폴더 제거

**위치:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\startup
```

**작업:**

```cmd
rd /s /q "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\startup"
```

**목적:** 이 폴더에는 업그레이드 중에 다시 생성될 이전 OSGi 번들이 포함되어 있습니다.

### 5.2 기본 JAR 파일 제거

**위치:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\org.apache.sling.launchpad.base.jar
```

**작업:**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\org.apache.sling.launchpad.base.jar"
```

**목적:** 이 JAR은 새 WAR 파일의 버전으로 대체됩니다.

### 5.3 Bootstrap 명령 파일 제거

**위치:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\felix\bundle0\BootstrapCommandFile_*.txt
```

**작업:**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\felix\bundle0\BootstrapCommandFile_*.txt"
```

**목적:** 새 환경에 대해 Bootstrap 명령이 다시 생성됩니다.

### 5.4 sling.options 파일 제거

**위치:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\felix\sling.options.file
```

**작업:**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\felix\sling.options.file"
```

### 5.5 sling_bootstrap.txt 파일 제거

**위치:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\sling_bootstrap.txt
```

**작업:**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\sling_bootstrap.txt"
```

### 5.6 sling.properties 파일 백업 및 제거

이 파일에는 나중에 병합해야 하는 환경별 구성이 포함되어 있습니다.

**위치:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\conf\sling.properties
```

**작업:**

1. **백업 만들기:**

   ```cmd
   copy "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\conf\sling.properties" "C:\AEM-Backups\sling.properties.backup"
   ```

2. **원본 삭제:**

   ```cmd
   del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\conf\sling.properties"
   ```

**목적:** 새 `sling.properties`이(가) 생성됩니다. 업그레이드 후 사용자 정의 구성을 복원하려면 백업을 검토하십시오.

## 6단계: JDK 21 설치 및 구성

### JDK 21 설치

1. Windows용 JDK 21 설치 관리자 실행
2. 표준 위치(예: `C:\Program Files\Java\jdk-21`)에 설치
3. 설치 마법사 완료

### 환경 변수 구성

#### JAVA_HOME 설정

1. **시스템 속성** → **고급** → **환경 변수** 열기
2. **시스템 변수**&#x200B;에서 **새로 만들기**&#x200B;를 클릭합니다.
3. 설정:
   - 변수 이름: `JAVA_HOME`
   - 변수 값: `C:\Program Files\Java\jdk-21`
4. **확인** 클릭

#### 경로 변수 업데이트

1. **시스템 변수**&#x200B;에서 `Path`을(를) 선택하고 **편집**&#x200B;을(를) 클릭합니다
2. 새 항목 추가:

   ```
   %JAVA_HOME%\bin
   ```

3. 이 항목을 목록의 맨 위로 이동하여 JDK 21이 우선하도록 합니다.
4. 모든 대화 상자에서 **확인**&#x200B;을 클릭합니다.

### Java 설치 확인

1. 업데이트된 환경 변수를 로드하려면 **new** 명령 프롬프트 열기
2. Java 버전 확인:

   ```cmd
   java -version
   ```

   예상 출력:

   ```
   java version "21.0.x"
   Java(TM) SE Runtime Environment (build 21.0.x+...)
   Java HotSpot(TM) 64-Bit Server VM (build 21.0.x+..., mixed mode, sharing)
   ```

3. JAVA 확인(_L):

   ```cmd
   echo %JAVA_HOME%
   ```

## 7단계: JVM 설정 구성

AEM을 배포하기 전에 프로덕션 사용을 위해 적절한 JVM 메모리 설정을 구성합니다.

### standalone.conf.bat 편집

1. 다음으로 이동합니다.

   ```
   <JBOSS_HOME>\bin
   ```

2. 텍스트 편집기에서 `standalone.conf.bat`을(를) 엽니다(관리자로).

3. `JAVA_OPTS` 구성을 찾거나 추가합니다.

   ```batch
   rem # AEM Production JVM Settings
   set "JAVA_OPTS=-Xms4096m -Xmx4096m -XX:MaxMetaspaceSize=768m"
   set "JAVA_OPTS=%JAVA_OPTS% -Djava.net.preferIPv4Stack=true"
   set "JAVA_OPTS=%JAVA_OPTS% -Dfile.encoding=UTF-8"
   set "JAVA_OPTS=%JAVA_OPTS% -server"
   ```

4. 파일 저장 및 닫기

**권장 설정:**

| 매개변수 | 권장 값 | 설명 |
|-----------|-------------------|-------------|
| `-Xms` | 4096m - 8192m | 초기 힙 크기 |
| `-Xmx` | 4096m - 8192m | 최대 힙 크기 |
| `-XX:MaxMetaspaceSize` | 768m - 1024m | Metaspace 제한 |

**참고:** 서버의 사용 가능한 메모리 및 작업 부하 요구 사항에 따라 값을 조정합니다.

## 8단계: AEM 6.5 LTS WAR 배포

### WAR 파일 준비

배포 안내서에 따라 AEM WAR 파일이 올바르게 구성되었는지 확인합니다.

- `jboss-deployment-structure.xml`이(가) 있음
- `web.xml`에 multipart-config 설정이 포함되어 있습니다
- 만약 수정이 이루어진다면 WAR은 재포장된다

### JBoss에 배포

1. AEM 6.5 LTS WAR 파일을 배포 디렉터리에 복사합니다.

   ```cmd
   copy "C:\AEM-Downloads\cq-quickstart-6.5.xx.war" "C:\jboss-eap-8.0\standalone\deployments\cq-quickstart.war"
   ```

**중요:** WAR 파일 이름이 원하는 URL 컨텍스트 경로와 일치하는지 확인하십시오.

## 9단계: AEM과 JBoss EAP 8 시작

### 서버 시작

1. **관리자**(으)로 **명령 프롬프트** 열기

2. JBoss bin 디렉토리로 이동합니다.

   ```cmd
   cd C:\jboss-eap-8.0\bin
   ```

3. JBoss EAP 8 시작:

   ```cmd
   standalone.bat -b 0.0.0.0 -bmanagement 0.0.0.0
   ```

### 초기 시작 모니터링

콘솔 출력 보기:

1. **WAR 배포:**

   ```
   Deployed "cq-quickstart.war" (runtime-name : "cq-quickstart.war")
   ```

2. **AEM 초기화 메시지:**

   ```
   Apache Sling Application Launcher
   Sling Home: crx-repository/crx-quickstart
   ```

3. **저장소 업그레이드(해당되는 경우):**

   ```
   Performing repository migration...
   ```

**예상 시작 시간:** 저장소 크기 및 시스템 리소스에 따라 5~15분.

## 10단계: 업그레이드 성공 확인

### AEM 시작 확인

JBoss 콘솔에서 최종 시작 메시지를 모니터링합니다.

```
**** AEM started successfully ****
```

### AEM 인터페이스 액세스

1. 웹 브라우저 열기
2. 다음으로 이동합니다.

   ```
   http://localhost:8080/cq-quickstart
   ```

3. 관리자 자격 증명으로 로그인:
   - 사용자 이름: `admin`
   - 암호: `admin`(또는 사용자 지정 암호)

### 시스템 정보 확인

1. **도구** → **작업** → **웹 콘솔**(으)로 이동

   ```
   http://localhost:8080/cq-quickstart/system/console
   ```

2. **시스템 정보** 클릭

3. 확인:

   - **JVM 버전:**&#x200B;에 Java 21이 표시되어야 함
   - **JBoss 버전:**&#x200B;에 EAP 8.x가 표시되어야 함
   - **AEM 버전:**&#x200B;에 6.5.xx가 표시되어야 합니다.

### 시스템 상태 확인

상태 검사를 실행하려면 **도구** → **작업** → **진단**(으)로 이동합니다.

- 번들 상태: 모든 번들은 &quot;활성&quot;이어야 합니다.
- 리소스 해결: 정상 상태를 표시해야 함
- 쿼리 성능: 성능 저하를 검토합니다.

## 업그레이드 후 작업

### 사용자 정의 구성 복원

1. 백업된 `sling.properties` 파일 검토
2. 사용자 지정 실행 모드 또는 구성을 새 파일에 복원합니다.

   ```
   <JBOSS_HOME>\bin\crx-repository\crx-quickstart\conf\sling.properties
   ```

3. 구성이 변경된 경우 AEM 다시 시작

### 복제 에이전트 업데이트

1. **도구** → **배포** → **복제** → **작성자의 에이전트**(으)로 이동
2. 모든 복제 에이전트 검토 및 테스트
3. 하드 코딩된 참조를 이전 서버 경로로 업데이트

### 주요 기능 테스트

- [ ] 콘텐츠 작성 및 게시
- [ ] 자산 업로드 및 처리 중
- [ ] 워크플로 실행
- [ ] 사용자 인증
- [ ] 통합 끝점
- [ ] 사용자 지정 구성 요소 및 템플릿

### 성능 최적화

1. 임시 캐시 검토 및 지우기
2. 초기 사용 중 시스템 성능 모니터링
3. 필요한 경우 실제 사용 패턴을 기반으로 JVM 설정 조정

## 문제 해결

### 일반 문제

| 문제 | 가능한 원인 | 솔루션 |
|-------|---------------|----------|
| AEM 시작 실패 | 잘못된 Java 버전 | JDK 21에 대한 `JAVA_HOME`점 확인 |
| 저장소 손상 오류 | 불완전한 저장소 사본 | 백업에서 복원 및 저장소 다시 복사 |
| OutOfMemoryError | 힙 메모리 부족 | `-Xmx`에서 `standalone.conf.bat` 늘리기 |
| &quot;설치됨&quot; 상태의 번들 | 종속성 누락 | 웹 콘솔에서 번들 종속성 확인 |
| 포트 8080이 이미 사용 중입니다. | 포트를 사용하는 다른 서비스 | 충돌하는 서비스 중지 또는 JBoss 포트 변경 |

### 로그 파일 위치

- **JBoss 서버 로그:**\
  `<JBOSS_HOME>\standalone\log\server.log`

- **AEM 오류 로그:**\
  `<JBOSS_HOME>\bin\crx-repository\crx-quickstart\logs\error.log`

- **AEM 액세스 로그:**\
  `<JBOSS_HOME>\bin\crx-repository\crx-quickstart\logs\access.log`

### 롤백 프로시저

업그레이드가 실패하여 해결할 수 없는 경우:

1. JBoss EAP 8 중지
2. JBoss EAP 7.4의 전체 백업 복원
3. `crx-repository` 폴더 복원
4. JDK 11에 대한 `JAVA_HOME`점 확인(롤백하는 경우)
5. 이전 환경 시작

## 모범 사례

### 프로덕션 배포 전

- [ ] 개발 환경에서 전체 업그레이드 프로세스를 테스트합니다
- [ 프로덕션 유사 데이터를 사용하는 스테이징 환경에서 ] 테스트
- [ ] 모든 사용자 지정 구성 및 통합 문서화
- [ ] 자세한 롤백 계획 만들기
- [ ] 유지 관리 기간 동안 업그레이드 예약
- [ ] 모든 이해 당사자에게 계획된 가동 중지 시간 알림

### 업그레이드 성공 후

- [ ] 48-72시간 동안 시스템 로그 모니터링
- [ ] 부하 테스트를 수행하여 성능 문제를 식별합니다
- [ ] 시스템 설명서 업데이트
- [ JBoss EAP 8 차이점에 대한 ] 교육 팀
- [ ] 모든 업그레이드 설명서 및 백업 보관

## 관련 설명서

- [JBoss EAP 8 마이그레이션 안내서](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8.0/html/migration_guide/)
- [Adobe Experience Manager 6.5 업그레이드 안내서](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade.html)
- [AEM 서비스 팩 설치](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html?lang=ko-KR)

## 문서 정보

| 필드 | 값 |
|-------|-------|
| 문서 버전 | 1.0 |
| 마지막 업데이트 | 2026년 2월 |
| AEM 버전 | 6.5 LTS |
| Source 플랫폼 | JBoss EAP 7.4 / JDK 11 |
| Target 플랫폼 | JBoss EAP 8.x / JDK 21 |
| 운영 체제 | Windows Server |

**법적 고지 사항:** Adobe, Adobe Experience Manager 및 AEM은 Adobe Inc.의 등록 상표입니다. JBoss 및 Red Hat은 Red Hat, Inc.의 등록 상표입니다.
