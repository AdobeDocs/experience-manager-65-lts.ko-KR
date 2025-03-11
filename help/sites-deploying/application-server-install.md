---
title: Application Server 설치
description: 애플리케이션 서버에 Adobe Experience Manager을 설치하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 09d54b52-485a-453c-a2d0-535adead9e6c
source-git-commit: 5f968f5dc0696a683cc063d330c8edfba05f11ab
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# Application Server 설치{#application-server-install}

>[!NOTE]
>
>`JAR` 및 `WAR`은(는) Adobe Experience Manager(AEM)가 출시된 파일 유형입니다. 이러한 포맷은 Adobe이 약속한 지원 수준에 맞게 품질 보증을 받고 있습니다.
>

이 섹션에서는 애플리케이션 서버와 함께 Adobe Experience Manager(AEM)를 설치하는 방법을 설명합니다. 개별 애플리케이션 서버에 대해 제공된 특정 지원 수준에 대한 자세한 내용은 [지원되는 플랫폼](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) 섹션을 참조하십시오.

다음 애플리케이션 서버의 설치 단계가 설명되어 있습니다.

* [WebSphere](#websphere)
* [Tomcat 11.0.x](#tomcat)

웹 애플리케이션 설치, 서버 구성 및 서버 시작 및 중지 방법에 대한 자세한 내용은 해당 애플리케이션 서버 설명서를 참조하십시오.

<!-- >[!NOTE]
>
>If you are using Dynamic Media in a WAR deployment, see [Dynamic Media documentation](/help/assets/config-dynamic.md#enabling-dynamic-media). -->

## 일반 설명 {#general-description}

### 애플리케이션 서버에 AEM 설치 시 기본 동작 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM은 단일 war 파일로 제공됩니다.

배포된 경우 기본적으로 다음 상황이 발생합니다.

* 실행 모드는 `author`입니다.
* 인스턴스(저장소, Felix OSGI 환경, 번들 등)가 `${user.dir}/crx-quickstart`에 설치되어 있습니다. 여기서 `${user.dir}`은(는) 현재 작업 디렉터리입니다. crx-quickstart에 대한 이 경로를 `sling.home`이라고 합니다.

* 컨텍스트 루트는 war 파일 이름입니다. 예: `aem-65-lts`

#### 구성 {#configuration}

다음과 같은 방법으로 기본 동작을 변경할 수 있습니다.

* 실행 모드 : 배포 전에 AEM war 파일의 `WEB-INF/web.xml` 파일에서 `sling.run.modes` 매개 변수를 구성합니다.

* sling.home: 배포하기 전에 AEM war 파일의 `WEB-INF/web.xml` 파일에서 `sling.home` 매개 변수를 구성합니다.

* 컨텍스트 루트: AEM war 파일 이름 바꾸기

#### 설치 게시 {#publish-installation}

게시 인스턴스를 배포하려면 실행 모드를 게시로 설정해야 합니다.

* AEM war 파일에서 `WEB-INF/web.xml` 압축 풀기
* `sling.run.modes` 매개 변수를 게시로 변경
* `web.xml` 파일을 AEM war 파일로 다시 압축
* AEM war 파일 배포

#### 설치 확인 {#installation-check}

모든 것이 설치되어 있는지 확인하려면 다음을 수행할 수 있습니다.

* `error.log`파일을 추적하여 모든 콘텐츠가 설치되었는지 확인합니다.
* `/system/console`에서 모든 번들이 설치되어 있는지 확인합니다.

#### 동일한 애플리케이션 서버에 두 개의 인스턴스 {#two-instances-on-the-same-application-server}

데모용으로 작성자와 게시 인스턴스를 하나의 애플리케이션 서버에 모두 설치하는 것이 적절할 수 있습니다. 이를 위해서는 다음을 수행해야 합니다.

1. 게시 인스턴스의 `sling.home` 변수 및 `sling.run.modes` 변수 변경
1. AEM war 파일에서 `WEB-INF/web.xml` 파일 압축 풀기
1. `sling.home` 매개 변수를 다른 경로로 변경합니다(절대 및 상대 경로가 가능).
1. 게시 인스턴스에 대해 `sling.run.modes`을(를) `publish`(으)로 변경
1. `web.xml` 파일 다시 압축
1. war 파일의 이름이 다르도록 이름을 변경합니다. 예를 들어, 이름을 `aemauthor.war`(으)로 바꾸고 다른 이름을 `aempublish.war`(으)로 바꿉니다
1. 더 높은 메모리 설정을 사용하십시오. 예를 들어 기본 AEM 인스턴스는 `-Xmx3072m`을(를) 사용합니다
1. 두 웹 애플리케이션 배포
1. 배포 후 두 웹 응용 프로그램 중지
1. 작성자 및 게시 인스턴스 모두에서 `sling.properties` 파일에서 속성 `felix.service.urlhandlers`이(가) `false`(으)로 설정되어 있는지 확인하십시오. (기본값은 `true`(으)로 설정되어 있습니다.)
1. 두 웹 애플리케이션을 다시 시작합니다.

## 애플리케이션 서버 설치 절차 {#application-servers-installation-procedures}

### WebSphere® 24.0.0.7 {#websphere}

배포하기 전에 위의 [일반 설명](#general-description)을 읽어 보십시오.

**서버 준비**

* 기본 인증 헤더가 통과하도록 허용:

   * AEM에서 사용자를 인증하는 한 가지 방법은 WebSphere® 서버의 전역 관리 보안을 비활성화하는 것입니다. 이렇게 하려면 **보안 > 전역 보안**(으)로 이동하여 **관리 보안 활성화** 확인란의 선택을 취소하고 서버를 저장한 후 다시 시작하십시오.

* `"JAVA_OPTS= -Xmx2048m"` 설정
* 컨텍스트 루트 = /를 사용하여 AEM을 설치하려면 기존 기본 웹 애플리케이션의 컨텍스트 루트를 변경합니다.

**AEM 웹 응용 프로그램 배포**

* AEM war 파일 다운로드
* 필요한 경우 `web.xml` 파일에서 구성을 만드십시오. 자세한 내용은 위의 [일반 설명](#general-description)을 참조하세요.

   * `WEB-INF/web.xml` 파일 압축 풀기
   * `sling.run.modes` 매개 변수를 `publish`(으)로 변경
   * 초기 `sling.home` 매개 변수의 주석 처리를 제거하고 필요에 따라 이 경로를 설정하십시오.
   * `web.xml` 파일을 다시 압축합니다.

* AEM war 파일 배포

   * 컨텍스트 루트를 선택합니다. 슬링 실행 모드를 설정하려면 배포 마법사의 자세한 단계를 선택한 다음 마법사의 6단계에서 이를 지정해야 합니다.

* AEM 웹 애플리케이션 시작

#### Tomcat 11.0.x {#tomcat}

배포하기 전에 위의 [일반 설명](#general-description)을 읽으십시오.

* **Tomcat 서버 준비**

   * VM 메모리 설정 늘리기:

      * `bin/catalina.bat`(UNIX의 경우 `catalina.sh` 다시 ®)에서 다음 설정을 추가합니다.

        ```
        set "JAVA_OPTS= -Xmx2048m`
        ```

   * Tomcat은 설치 시 관리자 또는 관리자 액세스를 활성화하지 않습니다. 따라서 다음 계정에 대한 액세스를 허용하려면 `tomcat-users.xml`을(를) 수동으로 편집해야 합니다.

      * 관리자 및 관리자에 대한 액세스 권한을 포함하도록 `tomcat-users.xml`을(를) 편집합니다. 구성은 다음 예제와 유사해야 합니다.

        ```xml
        <?xml version='1.0' encoding='utf-8'?>
        <tomcat-users>
        role rolename="manager"/>
        role rolename="tomcat"/>
        <role rolename="admin"/>
        <role rolename="role1"/>
        <role rolename="manager-gui"/>
        <user username="both" password="tomcat" roles="tomcat,role1"/>
        <user username="tomcat" password="tomcat" roles="tomcat"/>
        <user username="admin" password="admin" roles="admin,manager-gui"/>
        <user username="role1" password="tomcat" roles="role1"/>
        </tomcat-users>
        ```

   * 컨텍스트 루트 &quot;/&quot;와 함께 AEM을 배포하려면 기존 ROOT 웹 앱의 컨텍스트 루트를 변경해야 합니다.

      * ROOT 웹 앱 중지 및 배포 취소
      * Tomcat의 웹 앱 폴더에서 `ROOT.war` 폴더 이름 바꾸기
      * 웹 앱 다시 시작

   * Manager-gui를 사용하여 AEM 웹 애플리케이션을 설치하는 경우 기본적으로 50MB의 업로드 크기만 허용하므로 업로드된 파일의 최대 크기를 늘려야 합니다. 관리자 웹 응용 프로그램의 `web.xml`을(를) 열려면 다음을 수행하십시오.

     `webapps/manager/WEB-INF/web.xml`

     `max-file-size` 및 `max-request-size`을(를) 최소 500MB로 늘립니다. 아래 예제 `web.xml` 파일에서 다음 `multipart-config`을(를) 참조하십시오.

     ```xml
     <multipart-config>
     <!-- 500MB max -->
     <max-file-size>524288000</max-file-size>
     <max-request-size>524288000</max-request-size>
     <file-size-threshold>0</file-size-threshold>
     </multipart-config>
     ```

* **AEM 웹 응용 프로그램 배포**

   * AEM war 파일을 다운로드합니다.
   * 필요한 경우 `web.xml` 파일에서 구성을 만드십시오.

      * `WEB-INF/web.xml` 파일 압축 풀기
      * `sling.run.modes` 매개 변수를 `publish`(으)로 변경
      * 초기 `sling.home` 매개 변수의 주석 처리를 제거하고 필요에 따라 이 경로를 설정하십시오.
      * `web.xml` 파일을 다시 압축합니다.

   * AEM war 파일을 루트 웹 앱으로 배포하려면 이름을 `ROOT.war`(으)로 바꾸십시오. `aemauthor`을(를) 컨텍스트 루트로 사용하려면 이름을 `aemauthor.war`(으)로 바꾸십시오.
   * Tomcat의 webapps 폴더에 복사
   * AEM이 설치될 때까지 기다립니다.
