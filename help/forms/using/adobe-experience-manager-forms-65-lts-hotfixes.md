---
title: Adobe Experience Manager Forms 6.5 LTS 핫픽스
description: AEM Forms 6.5 LTS용 핫픽스를 다운로드하여 설치하는 방법에 대한 정보를 제공합니다. LTS가 아닌 AEM 6.5의 경우 AEM 6.5 Forms 핫픽스 문서를 참조하십시오.
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: e485100f-3e16-4fd4-a8ce-af771d765dd1
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ed762d86-a04b-452b-a08f-86359bb8ff27
    internal-label: Configuration and operations
subfeature_v2:
  - id: c21ccc2b-e0c8-4853-bf41-f12259ed93f8
    internal-label: Release information
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 2%
---
# Adobe Experience Manager Forms 6.5 LTS 핫픽스{#aem-form-hotfix}

이 문서에서는 알려진 문제를 해결하고, 시스템 안정성을 개선하며, AEM Forms 6.5 LTS의 전반적인 성능을 개선하기 위해 구현된 주요 수정 사항을 나열합니다.


이 문서는 AEM Forms 6.5 LTS에 적용됩니다. LTS가 아닌 AEM 6.5 배포의 경우 [Adobe Experience Manager Forms 핫픽스](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/release-notes/aem-forms-hotfix)를 참조하십시오.

>[!NOTE]
>
> 핫픽스는 이전의 모든 수정 사항을 포함하여 누적되도록 설계되었습니다. 릴리스에 최신 핫픽스를 적용하면 최신 문제를 해결할 수 있을 뿐만 아니라 이전의 모든 버그 수정 및 개선 사항이 통합되어 있습니다.

## AEM Forms 6.5 LTS에 대한 핫픽스 {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>날짜</strong></td>
    <td><strong>핫픽스 다운로드 링크(AEM 소프트웨어 배포 링크)</strong></td>
    <td><strong>해결된 문제</strong></td>
  </tr>
  <tr>
    <td>
      <strong>2026년 9월 21일</strong><br>
      <em>적용 대상:</em> AEM Forms 6.5 LTS 서비스 팩 2 JEE 배포(JBoss, WebLogic, WebSphere)<br>
    </td>
    <td>
    <p><strong>이 핫픽스를 설치하려면 다음 단계를 순서대로 완료하십시오.</strong></p>
    <p><strong>1단계: 패치 설치</strong></p>
    <ul>
    <strong>JBos:</strong>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-jboss.zip">JBoss JEE 서버용 Windows에서 AEM Forms 6.5 LTS SP2용 핫픽스</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-jboss.tar.gz">JBoss JEE 서버용 Linux에서 AEM Forms 6.5 LTS SP2용 핫픽스</a></li>
    <strong>WebLogic:</strong>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-weblogic.zip">Weblogic JEE 서버용 Windows에서 AEM Forms 6.5 LTS SP2용 핫픽스</a></li>
    <li>Linux- Weblogic JEE 서버용 Linux에서 AEM Forms 6.5 LTS SP2용 <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-weblogic.tar.gz">핫픽스</a></li>
    <strong>WebSphere:</strong>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/websphere/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-websphere.zip">Websphere JEE 서버용 Windows에서 AEM Forms 6.5 LTS SP2용 핫픽스</a></li>
    <li>Linux- Websphere JEE 서버용 Linux에서 AEM Forms 6.5 LTS SP2용 <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/websphere/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-websphere.tar.gz">핫픽스</a></li>
    </ul>
    <p>표준 AEM Forms on JEE 패치 설치 절차를 사용하여 패치를 설치합니다. <!-- TODO: link to the 6.5 LTS JEE patch installation instructions once available --></p>
    <p><strong>2단계: 취약성 수정 번들 설치</strong></p>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/SP2LTSBundles_VULN-36670.zip">AEM Forms 6.5 LTS SP2용 취약점 수정 번들</a></li>
    </ul>
    <ol>
    <li><code>http://&lt;host&gt;:&lt;port&gt;/lc/system/console/bundles</code>에서 OSGi 콘솔을 엽니다.</li>
    <li><strong>설치/업데이트</strong>를 클릭합니다.</li>
    <li><strong>번들 시작</strong> 및 <strong>패키지 새로 고침</strong> 확인란을 선택하십시오.</li>
    <li><strong>파일 선택</strong>을 클릭한 다음 다운로드한 번들을 업로드하십시오.</li>
    <li>로그가 설정되고 번들이 <strong>활성</strong>(으)로 표시될 때까지 기다리십시오.</li>
    </ol>
    <p><strong>3단계: AEM Forms Workbench 설치 관리자 업데이트</strong></p>
    <p>최신 AEM Forms Workbench 설치 관리자로 업데이트해야 합니다. <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/fd/workbench/6-5-0-20260902-1-45/Workbench_DVD.zip">AEM Forms Workbench 설치 관리자</a>에서 다운로드합니다.</p>
    <p><strong>4단계: 클라이언트 라이브러리 파일 업데이트(개발자)</strong></p>
    <p>이 패치에는 SDK 클라이언트 라이브러리 <code>adobe-livecycle-client.jar</code>에 대한 주요 업데이트가 포함되어 있습니다(<a href="/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files">AEM Forms Java 라이브러리 파일 포함</a> 참조). 프로젝트에서 이 JAR 파일을 사용하는 경우 핫픽스를 설치한 후 프로젝트의 클래스 경로에서 <code>adobe-livecycle-client.jar</code>을(를) 업데이트합니다. <code>&lt;AEM_Forms_Installation_dir&gt;\sdk\client-libs\common\adobe-livecycle-client.jar</code>에서 최신 버전을 사용할 수 있습니다.</p>
    <p>이 핫픽스는 누적되므로 서비스 팩 2를 먼저 설치하지 않고 AEM Forms 6.5 LTS 서비스 팩 2 또는 이전 서비스 팩에 적용할 수 있습니다.</p>
    </td>
    <td>
    <ul>
    <li><b>FORMS-26818</b> Apache Shiro가 버전 2.1.0으로 업데이트된 후 JEE의 AEM Forms에서 Shiro 보안 관리자용 <code>NoClassDefFoundError</code>을(를) 사용하여 부트스트랩하지 못합니다. 이 핫픽스는 성공적으로 부트스트래핑을 복원합니다.</li>
    <li>JEE의 <b>FORMS-26819</b> AEM Forms이 <code>org.owasp.esapi.reference.JavaLogFactory</code>에 대해 "클래스를 찾을 수 없음" 오류와 함께 실패합니다. 이 핫픽스는 누락된 클래스를 해결합니다.</li>
    <li><b>FORMS-26584, FORMS-26589</b> AEM Forms 6.5 LTS로 업그레이드하면 TaskManager 끝점이 제거됩니다. 이 핫픽스는 TaskManager 끝점을 복원합니다.</li>
    <li><b>FORMS-26569</b> 보안 XML 빌더로 인해 JEE에서 Configuration Manager MergeEars 단계가 실패하고 DOCTYPE 선언 오류(<code>ALC-LCM-010-200</code>)가 발생합니다. 이 핫픽스를 사용하면 MergeEar 단계를 완료할 수 있습니다.</li>
    <li><b>FORMS-25063</b> 응용 프로그램 수준 로그가 IBM WebSphere Liberty 배포에 없습니다. 이 핫픽스는 애플리케이션 수준 로깅을 복원합니다.</li>
    <li><b>FORMS-24892</b> JBoss에서 "IMAPProvider가 하위 유형이 아님"으로 전자 메일이 실패합니다. 이 핫픽스는 JBoss에서 이메일 기능을 복원합니다.</li>
    <li>WLP(WebSphere Liberty Profile)의 <b>FORMS-24692</b> 전자 메일이 "소켓을 TLS로 변환할 수 없습니다"로 실패합니다. 이 핫픽스는 WLP에서 TLS를 통해 이메일을 복원합니다.</li>
    <li><b>FORMS-26688</b> 깁슨 라이브러리를 버전 6.0.29665850으로 업데이트합니다.</li>
    <li><b>FORMS-25222</b> 백포트 SAML 어설션 유효성 검사 개선 사항.</li>
    <li><b>FORMS-26733, FORMS-26734</b> Apache Log4j가 버전 2.25.5으로 업데이트되었습니다.</li>
    <li>이 핫픽스에는 보안 수정 사항도 포함되어 있습니다.</li>
    </ul>
    <p><strong>빌드:</strong> AEMForms-6.6.0-0008</p>
    </td>
  </tr>
  <tr>
    <td>
      <strong>2025년 9월 9일</strong><br>
    <td>
    <ul>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-win-pkg-6.1.176-RHF-002.zip">Windows의 AEM 서비스 팩 6.5 LTS용 핫픽스2</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]hotfix-on-add-on/adobe-aemfd-linux-pkg-6.1.176-RHF-002.zip">Linux의 AEM 서비스 팩 6.5 LTS용 핫픽스2</a></li>
     <li>MacOS- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-osx-pkg-6.1.176-RHF-002.zip">MacOS의 AEM 서비스 팩 6.5 LTS용 핫픽스2</a></li>
    <td>
    <ul>
    <li>SSV(서버 측 유효성 검사)를 활성화했을 때 제출이 실패할 수 있는 문제를 해결하여 양식 제출 안정성을 개선했습니다. 문제가 발생하면 [Adobe Experience Manager Forms 지원](https://business.adobe.com/in/support/main.html)에 문의하십시오.
    </li>
    </ul>
    </td>    
  </tr>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## OSGi 핫픽스 다운로드 및 설치 {#download-install-hotfix}

다음 단계를 수행하여 핫픽스를 다운로드하고 설치합니다.

1. 소프트웨어 배포 링크에서 [핫픽스](#hotfix-for-adaptive-forms)를 다운로드합니다.
1. Experience Manager 패키지(.zip)를 가져오고 파일을 번들(.jar)할 수 있도록 핫픽스 아카이브 파일을 추출합니다.
1. [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing)를 통해 패키지(.zip)를 업로드하고 설치합니다.
1. Configuration Manager 번들 `https://server:host/system/console/bundles`을(를) 열고 번들(.jar)을 업로드한 후 설치합니다. 핫픽스가 설치되었습니다.
