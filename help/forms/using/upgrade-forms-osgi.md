---
title: OSGi에서 AEM 6.5 Forms LTS로 업그레이드
description: AEM 6.5.22.0 Forms에서 AEM 6.5 Forms LTS로 직접 업그레이드할 수 있습니다.
content-type: reference
role: Admin, User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, AEM Forms on OSGi, AEM Forms Upgrade
exl-id: 9233d4b7-441c-4cbd-86f8-2c52b99c3330
source-git-commit: b7aa877f9e782b0568adc7baa440dc630c690454
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 6%

---

# OSGi에서 AEM 6.5 Forms LTS로 업그레이드 {#upgrade-to-aem-forms-osgi}

[AEM 6.5에서 AEM 6.5 LTS로 업그레이드](/help/sites-deploying/upgrade.md)하려면 AEM 6.5.22.0 Forms 이상으로 업그레이드하십시오. AEM 6.5.22.0에서 AEM 6.5 Forms LTS로 직접 업그레이드할 수 있습니다.

AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms, AEM 6.3 Forms, AEM 6.4 Forms 또는 AEM 6.5 Forms을 사용하는 경우 AEM 6.5 Forms LTS로 직접 업그레이드할 수 없습니다. 자세한 업그레이드 경로는 [업그레이드 경로](/help/forms/using/upgrade.md) 설명서를 참조하십시오.

서비스 팩 AEM Forms 6.5.22.0(으)로 업그레이드한 후 다음 단계에 따라 AEM 6.5 LTS Forms으로 업그레이드하십시오.

1. AEM Forms 추가 기능 패키지를 설치합니다. 다음 단계가 나와 있습니다.

   1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
   1. 헤더 메뉴에서 사용할 수 있는 **[!UICONTROL Adobe Experience Manager]**&#x200B;을(를) 선택합니다.
   1. **[!UICONTROL 필터]** 섹션에서:
      1. **[!UICONTROL 솔루션]** 드롭다운 목록에서 **[!UICONTROL Forms]**&#x200B;을(를) 선택합니다.
      1. 패키지의 버전 및 유형을 선택합니다. **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수도 있습니다.
   1. 운영 체제에 적용할 수 있는 패키지 이름을 선택하고 **[!UICONTROL EULA 약관 동의]**&#x200B;를 선택한 다음 **[!UICONTROL 다운로드]**&#x200B;를 선택합니다.
   1. [패키지 관리자](/help/sites-administering/package-manager.md)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
   1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

      [AEM Forms 릴리스](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) 문서에 나열된 직접 링크를 사용하여 패키지를 다운로드할 수도 있습니다.

      패키지를 설치한 후 AEM 인스턴스를 다시 시작하라는 메시지가 표시됩니다. **서버를 즉시 중지하지 마십시오.** AEM Forms 서버를 중지하기 전에 ServiceEvent REGISTERED 및 ServiceEvent UNREGISTERED 메시지가 &lt;crx-repository>/error.log 파일에 나타나고 로그가 안정될 때까지 기다립니다. 또한 몇 가지 패키지는 설치된 상태로 유지될 수 있습니다. 이러한 패키지의 상태를 무시해도 됩니다.


      **다음 추가 JVM 명령줄 매개 변수를 사용하여 AEM 인스턴스를 다시 시작하십시오**:
      `--add-opens java.base/java.util=ALL-UNNAMED --add-exports=java.xml/com.sun.org.apache.xml.internal.serialize=ALL-UNNAMED`

      서버가 스크립트나 서비스를 통해 시작되는 경우 후속 재시작 후에도 유효하도록 위의 내용을 포함하도록 적절하게 업데이트하십시오.

      >[!NOTE]
      >
      > SDK를 다시 시작하려면 &#39;Ctrl+C&#39; 명령을 사용하는 것이 좋습니다. 예를 들어 Java 프로세스를 중지하는 것과 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경에서 불일치가 발생할 수 있습니다.

1. 설치 후 작업을 수행합니다.

   * **마이그레이션 유틸리티 실행**

     마이그레이션 유틸리티를 사용하면 이전 버전의 적응형 양식 및 서신 관리 에셋이 AEM 6.5 양식과 호환될 수 있습니다. 이 유틸리티는 AEM 소프트웨어 배포에서 다운로드할 수 있습니다. 마이그레이션 유틸리티를 구성하고 사용하는 방법에 대한 단계별 정보는 [마이그레이션 유틸리티](../../forms/using/migration-utility.md)를 참조하십시오.

     [초안 및 제출 구성 요소 통합](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html)에 샘플 을 사용하고 있으며 이전 버전에서 업그레이드하는 경우 업그레이드를 수행한 후 다음 SQL 쿼리를 실행하십시오.

     ```sql
     UPDATE metadata m, additionalmetadatatable am
     SET m.dataType = am.value
     WHERE m.id = am.id
     AND am.key = 'dataType'
     ```

     ```sql
     DELETE from additionalmetadatatable
     WHERE `key` = 'dataType'
     ```

   * **(AEM 6.2 Forms 또는 이전 버전에서만 업그레이드하는 경우) Adobe Sign을 다시 구성하십시오**

     이전 버전의 AEM Forms에서 Adobe Sign을 구성한 경우 AEM 클라우드 서비스에서 Adobe Sign을 다시 구성합니다. 자세한 내용은 [Adobe Sign과 AEM Forms 통합](../../forms/using/adobe-sign-integration-adaptive-forms.md)을 참조하십시오.

   * **jQuery 지원**

     AEM 6.5 Forms에서 jQuery의 버전은 3.2.1로 업데이트되고 jQuery UI 버전은 1.12.1로 업데이트됩니다. AEM Form은 **noConflict** 모드에서 JQuery를 사용합니다. 따라서 다른 jQuery 버전을 사용하는 경우 업그레이드를 수행하는 동안 문제가 표시되지 않습니다. 하지만 AEM 6.5 Forms으로 업그레이드할 때는:

      * 사용자 지정 구성 요소(있는 경우)가 지원되는 jQuery 버전과 호환되는지 확인합니다.
      * 사용자 지정 구성 요소에서 지원되지 않는 API를 제거합니다. 제거된 API 목록은 [업그레이드 안내서](https://jquery.com/upgrade-guide/3.0/)를 참조하십시오. 예를 들어 load(), .unload() 및 .error() API에 대한 지원이 제거됩니다. 앞서 설명한 API 대신 .on() 메서드를 사용합니다. 예를 들어 $(&quot;img&quot;).load(fn)를 $(&quot;img&quot;).on(&quot;load&quot;, fn)으로 변경합니다.

   * **(AEM 6.2 Forms 또는 이전 버전에서만 업그레이드하는 경우) 분석 및 보고서를 다시 구성하십시오**

     AEM 6.4 Forms에서는 소스 및 노출에 대한 성공 이벤트에 대한 트래픽 변수를 사용할 수 없습니다. 따라서 AEM 6.2 Forms 또는 이전 버전에서 업그레이드하면 AEM Forms에서 Adobe Analytics 서버로 데이터 전송을 중단하고 적응형 양식에 대한 분석 보고서를 사용할 수 없습니다. 또한 AEM 6.4 Forms에서는 필드에서 보낸 시간에 대한 양식 분석 버전 트래픽 변수 및 성공 이벤트를 도입했습니다. 따라서 AEM Forms 환경에 대한 분석 및 보고서를 다시 구성합니다. 자세한 단계는 [분석 및 보고서 구성](../../forms/using/configure-analytics-forms-documents.md)을 참조하십시오.

1. 서버가 성공적으로 업그레이드되었는지, 모든 데이터도 성공적으로 마이그레이션되었는지, 정상적으로 작동할 수 있는지 확인하십시오.

   * **번들 상태를 확인합니다.** 모든 번들이 활성 상태인지 확인합니다.
   * **복제 및 역방향 복제 확인:** 마이그레이션된 양식을 게시하고 채우고 제출합니다. 제출된 데이터도 확인합니다.
   * **관리자 및 개발자 사용자 인터페이스에 대한 액세스 권한을 확인합니다.** 관리자 계정에서 AEM 인스턴스에 로그인하고 다음 URL에 대한 액세스 권한이 있는지 확인합니다.

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   >AEM 6.4 Forms에서 crx-repository 구조가 변경되었습니다. 6.3 Forms에서 AEM 6.5 Forms으로 업그레이드하는 경우 새로 만드는 사용자 지정에 변경된 경로를 사용합니다. 변경된 경로의 전체 목록은 [AEM의 Forms 저장소 재구성](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/restructuring/forms-repository-restructuring-in-aem-6-5)을 참조하십시오.


## JBoss EAP 8(Windows)에서 AEM 배포

### 개요

이 안내서에서는 JDK 21을 사용하여 Windows 환경에서 JBoss EAP(Enterprise Application Platform) 8에 독립형 OSGi WAR 파일로 Adobe Experience Manager(AEM)를 배포하는 단계별 지침을 제공합니다.

### 시스템 요구 사항

배포 프로세스를 시작하기 전에 환경이 다음 요구 사항을 충족하는지 확인하십시오.

| 구성 요소 | 요구 사항 |
|-----------|-------------|
| 운영 체제 | Windows Server 2016 이상(64비트) |
| Java 개발 키트 | JDK 21(Oracle 또는 OpenJDK) |
| 응용 프로그램 서버 | JBoss EAP 8.x |
| AEM 배포 | AEM WAR 파일(Adobe에서 가져옴) |

>[!NOTE]
>
> `JAVA_HOME` 환경 변수가 JDK 21 설치 디렉터리를 가리키는지 확인합니다.

### 1단계: JBoss EAP 8 설치

#### JBoss EAP 다운로드

1. Red Hat Developer Portal로 이동합니다.\
   [https://developers.redhat.com/products/eap/download](https://developers.redhat.com/products/eap/download)

2. Windows용 JBoss EAP 8 ZIP 배포 를 다운로드합니다.

#### JBoss EAP 추출

1. 다운로드한 ZIP 파일의 압축을 원하는 설치 디렉토리에 풉니다.

2. 이 안내서 전체에서 사용할 디렉터리 경로는 `<JBOSS_HOME>`입니다.

   **예:**\
   ```C:\jboss-eap-8.0```

### 2단계: AEM WAR 파일 준비

#### AEM 전쟁 얻기

Adobe Software Distribution 또는 Adobe 담당자로부터 AEM WAR 파일을 얻습니다.

#### WAR 파일 이름 바꾸기

원하는 URL 컨텍스트 경로를 반영하도록 WAR 파일의 이름을 변경합니다.

```
cq-quickstart.war
```

>[!IMPORTANT]
>
> WAR 파일 이름은 응용 프로그램의 URL 컨텍스트를 결정합니다. 예를 들어 `cq-quickstart.war`은(는) `/cq-quickstart`에서 액세스할 수 있습니다.


### 3단계: AEM WAR 구성

JBoss에 배포하기 **전에**&#x200B;모든 구성 수정을 완료해야 합니다.

#### 작업 디렉터리 만들기

1. 임시 작업 디렉터리 만들기:

   ```
   C:\aem\war-config
   ```

2. `cq-quickstart.war`를 이 디렉터리에 복사합니다.

#### WAR 콘텐츠 추출

1. **명령 프롬프트**&#x200B;를 열고 작업 디렉터리로 이동합니다.

   ```cmd
   cd C:\aem\war-config
   ```

2. WAR 파일 추출:

   ```cmd
   jar -xvf cq-quickstart.war
   ```

   `WEB-INF` 및 기타 응용 프로그램 파일을 사용하여 디렉터리 구조를 만듭니다.

### 4단계: JBoss 배포 설명자 구성

#### 배포 구조 파일 만들기

1. 추출된 WAR 내에서 `WEB-INF` 디렉터리로 이동합니다.

   ```cmd
   cd WEB-INF
   ```

2. 이름이 `jboss-deployment-structure.xml`인 새 파일을 만듭니다.

3. 다음 XML 콘텐츠를 추가합니다.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jboss-deployment-structure xmlns="urn:jboss:deployment-structure:1.2">
       <deployment>
           <dependencies>
               <module name="jdk.unsupported" />
           </dependencies>
       </deployment>
   </jboss-deployment-structure>
   ```

4. 파일을 저장하고 닫습니다.

**목적:** 이 구성은 AEM에 필요한 JDK 내부 모듈에 대한 액세스를 제공합니다.

### 5단계: 다중 부분 업로드 설정 구성

>[!NOTE]
>
> 5단계는 **AEM Forms**&#x200B;에만 적용됩니다. **AEM 전용**&#x200B;을 설정하는 경우 이 단계를 건너뛸 수 있습니다.


#### web.xml 수정

1. 텍스트 편집기에서 `WEB-INF\web.xml` 열기

2. 실행 모드 구성이 포함된 `<servlet>` 섹션을 찾습니다.

   ```xml
   <!-- Set the runmode per default to author -->
   <init-param>
       <param-name>sling.run.modes</param-name>
       <param-value>author</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

3. 닫는 `</servlet>` 태그와 선행 줄을 다음으로 바꾸기:

   ```xml
   <init-param>
       <param-name>sling.run.modes</param-name>
       <param-value>author</param-value>
   </init-param>
   <multipart-config>
       <max-file-size>1048576000</max-file-size>
       <max-request-size>1048576000</max-request-size>
       <file-size-threshold>0</file-size-threshold>
   </multipart-config>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

4. `web.xml`을(를) 저장하고 닫습니다.

**목적:** 이러한 설정을 통해 AEM Forms 및 Digital Asset Management에 대한 대용량 파일 업로드(최대 1GB)를 할 수 있습니다.

### 6단계: WAR 파일 다시 패키지

모든 구성 변경을 완료한 후 WAR 파일을 다시 패키징합니다.

1. 추출된 콘텐츠가 포함된 작업 디렉토리로 다시 이동합니다.

   ```cmd
   cd C:\aem\war-config
   ```

2. 새 WAR 파일을 만듭니다.

   ```cmd
   jar -cvf cq-quickstart.war *
   ```

>[!IMPORTANT]
>
> 모든 구성이 완료된 후 이 단계를 한 번만 수행합니다.

### 7단계: AEM 배포 및 시작

#### JBoss에 WAR 배포

1. 다시 패키징된 `cq-quickstart.war`을(를) JBoss 배포 디렉터리에 복사합니다.

   ```
   <JBOSS_HOME>\standalone\deployments
   ```

   **예:**
   ```C:\jboss-eap-8.0\standalone\deployments```

#### JVM 설정 구성(선택 사항이지만 권장됨)

JBoss를 시작하기 전에 JVM 메모리 설정을 구성합니다.

1. 텍스트 편집기에서 `<JBOSS_HOME>\bin\standalone.conf.bat` 열기

1. 힙 메모리를 설정하려면 다음 줄을 수정하거나 추가합니다.

   ```batch
   set "JAVA_OPTS=-Xms4096m -Xmx4096m -XX:MaxMetaspaceSize=512m"
   ```

>[!NOTE]
>
> 서버 용량 및 AEM 요구 사항에 따라 메모리 값을 조정합니다.

1. 파일을 저장하고 닫습니다.

#### JBoss EAP 시작

1. **명령 프롬프트**&#x200B;을(를) **관리자**(으)로 엽니다.

1. JBoss bin 디렉토리로 이동합니다.

   ```cmd
   cd <JBOSS_HOME>\bin
   ```

   **예:**
   ```cmd cd C:\jboss-eap-8.0\bin```

1. JBoss 서버를 시작합니다.

   ```cmd
   standalone.bat -b 0.0.0.0 -bmanagement 0.0.0.0
   ```

   **매개 변수:**
   * `-b 0.0.0.0` — 서버를 모든 네트워크 인터페이스에 바인딩합니다.
   * `-bmanagement 0.0.0.0` — 관리 인터페이스를 모든 네트워크 인터페이스에 바인딩합니다.

#### 배포 모니터링

배포 메시지에 대한 콘솔 출력을 봅니다. 성공적인 배포는 다음으로 표시됩니다.

```
Deployed "cq-quickstart.war" (runtime-name : "cq-quickstart.war")
```

### 8단계: AEM 액세스

배포가 완료되고 AEM이 완전히 시작되면 다음 작업을 수행하십시오.

**AEM 작성자 URL:**
```http://<server-ip>:8080/cq-quickstart```

**기본 자격 증명:**

* 사용자 이름: `admin`
* 암호: `admin`

**중요:** 처음 로그인하면 바로 기본 암호를 변경합니다.

### 문제 해결

#### 일반 문제

| 문제 | 솔루션 |
|-------|----------|
| ClassNotFoundException으로 배포가 실패합니다. | `jboss-deployment-structure.xml`이(가) 올바르게 구성되었는지 확인 |
| 시작하는 동안 OutOfMemoryError | `standalone.conf.bat`에서 힙 메모리 늘리기 |
| AEM이 배포 후 시작되지 않음 | `<JBOSS_HOME>\standalone\log\server.log`에서 JBoss 로그 확인 |
| 브라우저에서 AEM에 액세스할 수 없음 | 방화벽 설정이 포트 8080을 허용하는지 확인 |

#### 로그 파일

* **JBoss 서버 로그:** `<JBOSS_HOME>\standalone\log\server.log`
* **AEM 오류 로그:** 시작 후 AEM 웹 콘솔을 통해 사용할 수 있습니다.\
  `http://<server-ip>:8080/cq-quickstart/system/console`

### 추가 구성

#### 실행 모드 구성

AEM 실행 모드(작성자/게시)를 변경하려면 WAR을 다시 패키징하기 전에 `sling.run.modes`에서 `WEB-INF\web.xml` 매개 변수를 수정하십시오.

```xml
<init-param>
    <param-name>sling.run.modes</param-name>
    <param-value>publish</param-value>
</init-param>
```

#### 프로덕션 권장 사항

프로덕션 환경의 경우:

* JBoss에서 SSL/TLS 인증서 구성
* AEM 복제 에이전트 설정
* 로드 밸런싱을 위한 Dispatcher 구성
* 자동화된 백업 사용
* 모니터링 및 경고 구현

### 관련 설명서

* [JBoss EAP 8 설명서](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8.0)
* [Adobe Experience Manager 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html)
* [AEM 설치 및 배포 안내서](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html)

### 문서 정보

| 필드 | 값 |
|-------|-------|
| 마지막 업데이트 | 2026년 2월 |
| AEM 버전 | 6.5+(LTS) |
| JBoss 버전 | EAP 8.x |
| JSDK 버전 | 21 |
| Platform | Windows |


