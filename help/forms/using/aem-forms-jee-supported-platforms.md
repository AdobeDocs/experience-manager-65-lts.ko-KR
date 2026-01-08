---
title: JEE에서 AEM Forms에 대해 지원되는 플랫폼
description: JEE에 AEM Forms을 설치하는 데 필요하고 지원되는 인프라 구성 요소 목록
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE,Platform Matrix
source-git-commit: 4097adf1dd533bbf21c8635a1948f9ef4c294896
workflow-type: tm+mt
source-wordcount: '2982'
ht-degree: 3%

---


# JEE에서 AEM Forms에 대해 지원되는 플랫폼 {#supported-platforms-for-aem-forms-on-jee}

## 지원 수준 {#support-levels}

AEM Forms on JEE 서버는 지원되는 운영 체제, 애플리케이션 서버, 데이터베이스, 데이터베이스 드라이버, JDK, LDAP 서버 및 이메일 서버의 조합을 사용하여 설정할 수 있습니다.

이 문서에서는 JEE에서 AEM Forms에 대해 지원되는 클라이언트 및 서버 플랫폼을 나열합니다. Adobe은 Adobe 권장 구성 및 기타 구성 모두에 대해 여러 수준의 지원을 제공합니다. 지원되는 다른 소프트웨어와 해당 버전, 예외, 패치 정의 및 타사 소프트웨어 패치 지원 정책 목록도 제공됩니다.

>[!NOTE]
>
>- 지원되는 서버 플랫폼에 대한 전체 예외 목록은 [지원되는 서버 플랫폼에 대한 예외](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p)를 참조하십시오.
>- AEM Forms on JEE는 지원되는 운영 체제 및 애플리케이션의 영어, 프랑스어, 독일어 및 일본어 버전만 지원합니다.

### 업그레이드 및 지원 정책

#### 전체 설치 관리자

- **전체 설치 관리자에 대한 업그레이드 지원**: 전체 설치 관리자는 여섯 번째 AEM 서비스 팩마다 릴리스됩니다. AEM 6.5.23.0부터 전체 설치 관리자 기반 업그레이드가 지원됩니다.

- **사용 중단 및 제거**: 플랫폼 지원은 전체 설치 관리자 릴리스마다 업데이트됩니다. 전체 설치 프로그램 릴리스 동안 platform matrix에서 더 이상 사용되지 않는 것으로 표시된 모든 소프트웨어는 후속 전체 설치 프로그램 릴리스에서 지원되는 platform matrix에서 제거될 수 있으며, 이는 소프트웨어에 대한 지원이 종료되었음을 나타냅니다.

#### 서비스 팩

- **서비스 팩 범위**: Adobe에서는 최신 6개의 서비스 팩을 사용하는 AEM Forms 환경에 대한 기술 지원을 제공합니다. Adobe 현재 버전이 마지막 6개의 서비스 팩보다 빠른 경우 최적의 성능, 보안 및 지속적인 지원을 위해 최신 버전으로 업그레이드하는 것이 좋습니다.

- **패치 설치 관리자 지침**: 패치 설치 관리자를 사용하여 업데이트하는 동안 기본 전체 설치 관리자 버전이 두 개 이하의 이전 릴리스인지 확인하는 것이 중요합니다. 예를 들어 서비스 팩 6.5.19.0을(를) 설치하는 동안 기본 전체 설치 관리자 버전이 6.5.18.0 또는 6.5.12.0인지 확인하십시오.

- **패치 업그레이드 지원**: 지원되는 최신 플랫폼으로 업그레이드하기 전까지 최신 서비스 팩으로 계속 업그레이드할 수 있습니다. 예를 들어 6.5.12.0에 대해 지원되는 플랫폼 조합으로 전환하는 경우 서비스 팩 6.5.19.0에서 6.5.19.0(으)로 업그레이드할 수 있습니다.

### 권장 구성 {#recommendedconfigurations}

Adobe은 이러한 구성을 권장하며 표준 소프트웨어 유지 관리 계약의 일부로 전체 또는 제한된 지원을 제공합니다.

<table>
 <tbody>
  <tr>
   <th>지원 수준</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>A: 지원됨<br /> </td>
   <td>Adobe는 이 구성에 대한 전체 지원과 유지 관리를 제공합니다. 이 구성은 Adobe 품질 보증 프로세스에 따라 처리됩니다.</td>
  </tr>
  <tr>
   <td>R: 제한된 지원</td>
   <td>Adobe은 특정 전제 조건이 충족되면 이 구성을 완벽하게 지원합니다. 사전 요구 사항에 대해 알아보고 지원 요청을 제기하려면 Adobe 엔터프라이즈 지원에 문의하십시오.</td>
  </tr>
  <tr>
   <td>L: 제한된 지원</td>
   <td>Adobe은 특정 전제 조건이 충족되면 이 구성에 대한 전체 지원 및 유지 관리를 제공합니다. 일부 기능은 구성에서 사용할 수 없습니다. 전제 조건에 대해 알아보고 지원 요청을 제기하려면 Adobe 엔터프라이즈 지원에 문의하십시오.<br /> </td>
  </tr>
 </tbody>
</table>

### 지원되지 않는 구성 {#unsupported-configurations}

| 지원 수준 | 설명 |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E: 작동 예정 | 구성이 작동할 것으로 예상되며, 반대의 보고서는 없습니다. |
| Z: 지원되지 않음 | 구성이 지원되지 않습니다. Adobe은 구성의 작동 여부에 대해 설명하지 않으며 이를 지원하지 않습니다. |

>[!NOTE]
>
>AEM Forms 고객이 소유 비용을 절감하고, 배포 아키텍처를 단순화하고, 개발 스택을 현대화할 수 있도록 Adobe Experience Manager 엔터프라이즈 플랫폼은 독립형 OSGi 기반 배포를 위해 애플리케이션 서버 기반 배포에서 탈피하고 있습니다. Adobe은 인프라 구성 요소 매트릭스가 축소된 AEM Forms JEE 스택을 계속 지원합니다.
>새 설치의 경우, 가능한 경우 양식 데이터 모델을 사용한 모바일, 다중 채널 대화형 통신 및 백엔드 데이터 통합용 응답형 Forms에 대한 최신 혁신 기능을 사용하도록 최신 OSGi 스택에 AEM Forms을 배포하는 것이 좋습니다.
>
>Adobe은 기존 사용자가 JEE 스택에 AEM Forms을 계속 배포해야 한다는 것을 인지합니다. 이러한 시나리오에서 Adobe은 이 설명서에 설명된 대로 지원되는 인프라에 AEM Forms JEE를 배포해야 합니다. AEM 6.5 Forzms로 업그레이드하고 이전 AEM Forms 릴리스에서 지원되지 않는 플랫폼을 사용하는 경우 Adobe 지원팀에 문의하여 지원되는 플랫폼으로 업그레이드하는 데 도움을 받을 수 있습니다.

### Java™ 가상 시스템(JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms을 실행하려면 Java™ Virtual Machine이 필요하며, 이 시스템은 JDK(Java™ Development Kit) 배포에서 제공합니다. Adobe Experience Manager은 다음 버전의 Java™ 가상 시스템과 함께 작동합니다.

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>지원 수준</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
   <tr> 
   <td><p>Oracle Java™ SE 21(64비트) <sup> [8] </sup> </p>  </td>
   <td><p>A: 지원됨</p> </td>
   <td><p>마이너 릴리스 및 업데이트 </p> </td>
  </tr>
  <tr> 
   <td><p>Oracle Java™ SE 17(64비트) <sup> [8] </sup> </p>  </td>
   <td><p>A: 지원됨</p> </td>
   <td><p>마이너 릴리스 및 업데이트 </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>- Java™ 공급업체의 보안 게시판을 추적하여 프로덕션 환경의 안전과 보안을 보장하고 최신 Java™ 업데이트를 설치합니다.
>- JEE의 AEM Forms은 프로덕션 환경에서 64비트 JVM만 지원합니다.

### 데이터베이스 및 CRX 지속성 {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>Platform</strong></p> </td>
   <td><p><strong> 설명</strong></p> </td>
   <td><p><strong>지원 수준</strong></p> </td>
  </tr>
  <tr>
   <td><p>파일 시스템</p> </td>
   <td><p>저장소 마이크로커널(TAR MK 파일)</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 9.0 </p> </td>
   <td><p>저장소 마이크로커널</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 8.0</p> </td>
   <td><p>저장소 마이크로커널</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
    <tr>
   <td><p> MongoDB Enterprise 7.0 </p> </td>
   <td><p>저장소 마이크로커널</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
   <tr>
   <td>Oracle Database 19c(Standard, RAC(Real Application Clusters) 및 Enterprise Edition) </td>
   <td>-</td>
   <td>지원됨</td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2022 </p> </td>
   <td><p>-</p> </td>
   <td><p>지원됨</p> </td>
  </tr>
  <tr>
   <td>MySQL 8.4</td>
   <td>-</td>
   <td>R: 제한된 지원</td>
  </tr>
 </tbody>
</table>

- MongoDB는 타사 소프트웨어이며 AEM 라이선스 패키지에 포함되어 있지 않습니다. 자세한 내용은 [MongoDB 라이선스 정책](https://www.mongodb.org/about/licensing/)을 참조하세요.
- Adobe에서는 AEM 배포를 최대한 활용하기 위해 MongoDB Enterprise 버전에 라이선스를 부여하여 전문적인 지원을 받을 것을 권장합니다.
- Adobe 고객 지원 센터는 AEM에서의 MongoDB 사용과 관련된 자격 부여 문제를 지원합니다. 자세한 내용은 [Adobe Experience Manager용 MongoDB 페이지](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)를 참조하세요.
- &#39;파일 시스템&#39;에는 POSIX와 호환되는 블록 저장소가 포함되어 있습니다. 여기에는 네트워크 스토리지 기술이 포함됩니다. 파일 시스템 성능이 달라질 수 있으며 전체 성능에 영향을 줄 수 있습니다. 네트워크/원격 파일 시스템으로 테스트 AEM을 로드하는 것이 좋습니다.
- MongoDB 스토리지 엔진 WiredTiger만 지원됩니다.
- MongoDB 분할은 AEM에서 지원되지 않습니다.
- Document Security 모듈은 콘텐츠 저장소를 사용하지 않습니다. 이는 Document Security만 사용하고 있고 HTML Workspace, HTML 5 양식 또는 적응형 양식을 사용할 계획이 없는 경우 컨텐츠 저장소를 설치하지 말라는 의미입니다.

### 데이터베이스 드라이버 {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>데이터베이스 </th>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL 커넥터/J 8.4</p> </td>
   <td><p>JEE 설치 시 AEM Forms 제공</p> </td>
  </tr>
  <tr>
   <td>Microsoft® SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC 드라이버 12.10.0<br /> </p> <p>sqljdbc12.10.0.jar</p> </td>
   <td><p>Microsoft® 웹 사이트에서 다운로드합니다.</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Oracle 데이터베이스 19.3.0.0.0 JDBC 드라이버</p> <p>ojdbc8.jar(버전 19.3.0.0.0)<br /> </p> </td>
   <td><p><a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">Oracle 웹 사이트</a>에서 다운로드합니다.</p> </td>
  </tr>
 </tbody>
</table>

### 애플리케이션 서버 {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> Platform</strong></p> </td>
   <td><p><strong>지원 수준</strong></p> </td>
   <td><p><strong>지원되는 패치 정의</strong></p> </td>
  </tr>
  <tr>
   <td><p>JBoss® 엔터프라이즈 응용 프로그램 플랫폼(EAP) 8.0.6 <sup>[2] [3] [7]</sup> </p> </td>
   <td><p>A: 지원됨</p> </td>
   <td><p>지원되는 EAP 버전에 대한 패치 및 누적 패치</p> </td>
  </tr>
 </tbody>
</table>

### 서버 운영 체제 {#server-operating-systems}

#### 프로덕션 환경 {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> Platform</strong></p> </th>
   <th><p><strong>지원 수준</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
     <tr>
   <td>Microsoft® Windows Server 2022(64비트)</td>
   <td>A: 지원됨</td>
   <td>서비스 팩 및 주요 업데이트</td>
  </tr>
  <tr>
   <td>Ubuntu 20.04</td>
   <td>A: 지원됨</td>
   <td>서비스 팩 및 주요 업데이트</td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 9(커널 5.x)(64비트)</p> </td>
   <td><p>A: 지원됨</p> </td>
   <td><p>마이너 릴리스, 누적 업데이트 및 중요 업데이트</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 8(커널 4.x)(64비트)</td>
   <td><p>A: 지원됨</p> </td>
   <td><p>마이너 릴리스, 누적 업데이트 및 중요 업데이트</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 15-SP6(64비트)</p> </td>
   <td><p>A: 지원됨</p> </td>
   <td><p>서비스 팩, 누적 패치 및 중요 보안 업데이트</p> </td>
  </tr>
 </tbody>
</table>

#### 가상화 환경 {#virtualized-environment}

물리적 컴퓨터 또는 가상 환경에서 JEE에서 AEM Forms을 실행할 수 있습니다. 그러나 가상 환경에서 AEM Forms에 문제가 발생하면 물리적 컴퓨터에서 문제를 복제해 보십시오. 물리적 시스템에서 문제가 지속되면 Adobe 지원 센터에 문의하여 해결 방법을 확인하십시오. 물리적 시스템에서 복제할 수 없는 문제는 가상 환경 공급업체에 문의하십시오.

#### 개발 환경 {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>플랫폼(기본 버전)</strong></p> </th>
   <th>지원 수준</th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 64비트</p> </td>
   <td>E: 작동 예정</td>
   <td><p>서비스 팩 및 주요 업데이트</p> </td>
  </tr>
 </tbody>
</table>

### 지원되는 서버 플랫폼에 대한 예외 {#exceptions-to-supported-server-platforms}

JEE 서버에서 AEM Forms을 설정할 플랫폼을 선택할 때 다음 예외를 고려하십시오.

1. CRX 리포지토리는 TarMK 및 MongoDB 유형의 지속성을 지원합니다.
1. JEE의 AEM Forms은 JBoss® RBAC(역할 기반 액세스 제어)를 지원하지 않습니다.

<!-- 
1. [!DNL Microsoft&reg; Windows Server 2019] does not support [!DNL MySQL 5.7] and [!DNL JBoss&reg; EAP 7.1], [!DNL Microsoft&reg; Windows Server 2019] does not support turnkey installations for [!DNL Experience Manager Forms Service Pack 6.5.10.0 and later]. (CQDOC-18312) 
-->

또한 Adobe AEM Forms on JEE 배포용 소프트웨어를 선택할 때 다음 사항을 고려하십시오.

- AEM Forms on JEE는 지원되는 소프트웨어의 지정된 주 버전 및 부 버전 위에 업데이트, 패치 및 수정 팩을 지원합니다. 그러나 지정하지 않는 한 다음 주 버전 또는 부 버전으로의 업데이트는 지원되지 않습니다.
- 클러스터 기반 설치는 TarMK 지속성을 지원하지 않습니다. 지원되는 지속성에 대한 자세한 내용은 [AEM Forms 설치를 위한 지속성 유형 선택](/help/forms/using/choosing-persistence-type-for-aem-forms.md)을 참조하십시오.
- AEM Forms on JEE는 Adobe의 [타사 소프트웨어 지원 정책](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p)에 따라 다양한 타사 소프트웨어를 지원합니다.
- 타사 공급업체에서 제공한 지원에 따라 JEE의 AEM Forms 지원 플랫폼입니다. 일부 조합은 서드파티 공급업체에서 허용하지 않을 수 있습니다. 예를 들어 많은 공급업체가 Oracle을 통해 애플리케이션 서버를 인증하지 않았습니다. 따라서 JEE의 AEM Forms 또한 이러한 조합을 지원하지 않습니다. 지원되는 소프트웨어 버전을 선택하려면 서드파티 공급업체의 지원 매트릭스도 확인하십시오.
- JEE의 AEM Forms은 TarMK 콜드 대기를 지원하지 않습니다.
- JEE의 AEM Forms은 수직 클러스터링을 지원하지 않습니다.
- JEE의 AEM Forms은 클러스터된 환경에서 MySQL 데이터베이스를 지원하지 않습니다.

### LDAP 서버(선택 사항) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>제품(기본 버전)</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft® Active Directory 2022</td>
   <td>유지 관리 릴리스 및 수정 팩</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>기능 팩 및 임시 수정 사항</p> </td>
  </tr>
 </tbody>
</table>

### 이메일 서버(선택 사항) {#email-servers-optional}

| 제품 |
| ----------------------- |
| Microsoft® Exchange 2013 |
| Microsoft® Office 365 |

### 콘텐츠 관리자 및 해당 커넥터 {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>제품<br /> </strong></td>
   <td><strong>버전</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum®</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM® 파일</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM® Content Manager Server(더 이상 사용되지 않음) </td>
   <td>8.5 수정 팩 2</td>
  </tr>
  <tr>
   <td> IBM® Content Manager 클라이언트</td>
   <td>8.7 </td>
  </tr>
  <tr>
   <td> IBM® Content Manager 클라이언트(더 이상 사용되지 않음)</td>
   <td>8.5 </td>
  </tr>
   <td>Microsoft® Sharepoint </td>
   <td>2019<br /> </td>
  </tr>
 </tbody>
</table>

### Cordova 지원 {#support-for-cordova}

AEM Forms 앱은 이제 Apache Cordova를 지원합니다. 지원되는 Cordova의 플랫폼별 버전은 다음과 같습니다.

- Apache Cordova 6.4.0
- Cordova iOS 4.3.0
- Cordova Android™ 6.0.0
- Cordova 윈도우 4.4.3

### PDF Generator 소프트웨어 지원 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>제품</strong></p> </th>
   <th><p><strong>PDF으로 전환하기 위해 지원되는 형식</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/kr/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat Pro DC</a> 최신 버전</td>
   <td>XPS, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML 및 HTM</td>
  </tr>

<tr>
   <td>Microsoft® Office 2021 Professional Plus, 소매 및 볼륨 라이선스</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF 및 TXT</td>
  </tr>
  <tr>
   <td>
    <strong>OpenOffice 4.1.15</strong>   </td>
   <td>
    ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, 이미지 형식(BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF, TXT<br>

</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>- PDF Generator은 지원되는 운영 체제 및 애플리케이션의 영어, 프랑스어, 독일어 및 일본어 버전만 지원합니다.
>- PDF Generator에서 변환을 수행하려면 Adobe Acrobat Pro DC(32비트)가 필요합니다.
>- PDF Generator은 변환에 필요한 Microsoft® Office Professional Plus 및 기타 소프트웨어의 32비트 버전만 지원합니다.
>- 볼륨 라이선스가 있는 설치가 지정된 기간 내에 KMS 호스트를 찾을 수 없는 것과 같은 이유로 Microsoft® Office 설치가 비활성화되거나 사용이 허가되지 않는 경우, 설치 라이선스를 다시 취득하고 다시 활성화하기 전까지 전환이 실패할 수 있습니다.
>- PDF Generator은 Microsoft® Office 365를 지원하지 않습니다.
>- OpenOffice용 PDF Generator 전환은 Windows와 Linux® 모두에서 지원됩니다.
>- OCR PDF, PDF 최적화 및 Export PDF 기능은 Windows에서만 지원됩니다.
>- PDF Generator 서비스는 Microsoft® Windows 11을 지원하지 않습니다

<!-- Removed lines: >- PDF Generator fails to convert files using Microsoft&reg; Visio 2019. You can continue to use Microsoft&reg; Visio 2016 to convert .VSD and .VSDX files.
>- PDF Generator fails to convert files using Microsoft&reg; Project 2019. You can continue to use Microsoft&reg; Project 2016 to convert .MPP files.-->

### 접근성 지원에 대한 예외 {#exceptions-to-accessibility-support}

AEM Forms의 다음 하위 시스템은 [508](https://www.section508.gov/)과(와) 호환되지 않습니다.

- 적응형 Forms 작성 UI
- Forms Manager 작성 UI
- 서신 관리 작성 UI
- 관리 UI(관리 콘솔 UI)

## JEE의 AEM Forms에 대한 시스템 요구 사항 {#system-requirements-for-aem-forms-on-jee}

### 최소 하드웨어 요구 사항 {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>Platform</td>
   <td>최소 하드웨어 요구 사항</td>
  </tr>
  <tr>
   <td>Microsoft® Windows Server</td>
   <td>Intel Xeon® E5-2680, 2.4GHz 프로세서 또는 동급 <br /> VMWare ESX 5.1 이상<br /> RAM: 6GB(64비트 JVM이 있는 64비트 OS)<br /> 사용 가능한 디스크 공간: 15GB의 임시 공간 + 22GB의 AEM Forms ON JEE용 <br /></td>
  </tr>
  <tr>
   <td>SUSE® Linux® 엔터프라이즈 서버</td>
   <td>Intel Xeon® E5-2670v2, vCPU 1개, 2.5GHz 프로세서<br /> AWS m3.medium(ECU 3개)<br /> RAM: 6GB(64비트 JVM이 있는 64비트 OS)<br /> 사용 가능한 디스크 공간: 6GB의 임시 공간과 JEE의 AEM Forms용 22GB<br /></td>
  </tr>
  <tr>
   <td>Red Hat® Enterprise Linux®</td>
   <td>Intel Xeon® E5-2670v2, vCPU 1개, 2.5GHz 프로세서<br /> AWS m3.medium(ECU 3개)<br /> RAM: 6GB(64비트 JVM이 있는 64비트 OS)<br /> 사용 가능한 디스크 공간: 6GB의 임시 공간과 JEE의 AEM Forms용 <br /><br /> </td>
  </tr>
  <tr>
   <td>소규모 운영 환경에 필요한 하드웨어 요구 사항</td>
   <td>
    <ul>
     <li><strong>인텔® 기반 환경</strong>: 인텔 제온® E5-2680, 2.4 GHz 이상 듀얼 코어 프로세서를 사용하면 성능이 더욱 향상됩니다.</li>
     <li><strong>메모리: </strong>4GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

추가 요구 사항은 다음을 참조하십시오.

- [JEE 배포의 단일 서버 AEM Forms에 대한 시스템 요구 사항](https://www.adobe.com/go/learn_aemforms_sysreq_single_65_kr)
- [JEE 배포의 클러스터된 AEM Forms에 대한 시스템 요구 사항](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65_kr)

### Adobe Acrobat 및 Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat 및 Adobe Reader(기본)</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2020 (클래식 트랙)</td>
   <td>버전 20.004.30006 이상<br /> </td>
  </tr>

</tbody>
</table>

>[!NOTE]
>
>Acrobat DC 제품군은 Acrobat과 Reader에 대해 &quot;Classic&quot;과 &quot;Continuous&quot;의 두 가지 제품을 도입합니다. 두 트랙에 대한 자세한 내용 및 비교는 [https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html)을(를) 참조하십시오.

## JEE에서 AEM Forms에 대해 지원되는 클라이언트 {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10(Enterprise, Pro, Basic)</p> <p>32비트 또는 64비트 버전</p> <p> </p> </td>
   <td>서비스 팩 및 주요 업데이트</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2022 Server</td>
   <td>서비스 팩 및 주요 업데이트</td>
  </tr>
 </tbody>
</table>

- 설치할 디스크 공간: Workbench에만 1.7GB, Workbench, Designer의 전체 설치를 위해 단일 드라이브에 2.7GB, 임시 설치 디렉토리의 샘플 어셈블리 400MB - 사용자 임시 디렉토리의 경우 200MB, Windows 임시 디렉토리의 경우 200MB. 이러한 위치가 모두 단일 드라이브에 있는 경우 설치하는 동안 사용할 수 있는 공간이 1.5GB여야 합니다. 임시 디렉토리에 복사된 파일은 설치가 완료되면 삭제됩니다.

- Workbench를 실행하기 위한 메모리: 2GB RAM
- 하드웨어 요구 사항: Intel® Pentium® 4 또는 AMD® 동급, 1GHz 프로세서
- 최소 1024X768픽셀 이상의 모니터 해상도(16비트 색상 이상)
- JEE 서버의 AEM Forms에 대한 TCP/IPv4 또는 TCP/IPv6 네트워크 연결
- Windows에 Workbench를 설치하려면 관리 권한이 있어야 합니다. 관리자가 아닌 계정을 사용하여 설치하는 경우 설치 프로그램에서 적절한 계정에 대한 자격 증명을 입력하라는 메시지가 표시됩니다.

### Designer {#designer}

- Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server, Microsoft® Windows® 10 또는 Windows® 11
- PAE, NX 및 SSE2를 지원하는 1GHz 이상의 프로세서
- 32비트용 RAM 1GB 또는 64비트 OS용 RAM 2GB
- 32비트용 16GB 디스크 공간 또는 64비트 OS용 20GB 디스크 공간
- 그래픽 메모리 - 128MB GPU(256MB 권장)
- 2.35GB의 사용 가능한 하드 디스크 공간
- 1024 X 768 픽셀 이상의 모니터 해상도
- 비디오 하드웨어 가속(옵션)
- Acrobat Pro DC, Acrobat Standard DC 또는 Adobe Acrobat Reader DC
- Designer을 설치할 수 있는 관리 권한
- Microsoft® Visual C++ 2019(VC 14.28 이상) 32비트 런타임

### 브라우저 {#browsers}

#### 데스크탑 {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>브라우저(기본)</strong></p> </th>
   <th><p><strong>지원 수준</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Edge(에버그린)</p> </td>
   <td><p>A: 지원됨</p> </td>
   <td><p>서비스 팩 및 업데이트</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox (Evergreen)</p> </td>
   <td><p>A: 지원됨</p> </td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ESR</td>
   <td>E: 작동 예정</td>
   <td> 모든 업데이트</td>
  </tr>
  <tr>
   <td><p>Google Chrome (Evergreen)</p> </td>
   <td><p>A: 지원됨</p> </td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>macOS의 Apple Safari</td>
   <td>A: 지원됨</td>
   <td>모든 업데이트</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>데스크탑에 대한 일부 브라우저 관련 예외는 다음과 같습니다.
>
>- Safari는 Macintosh OS X에서만 지원됩니다.
>- Workspace은 Macintosh OS X 10.6 및 10.7에서 Safari 5.1(Acrobat DC 이상 버전 포함)을 지원합니다. Adobe Reader, Acrobat과의 Safari 5.1 호환성에 대한 자세한 내용은 [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html)을(를) 참조하십시오.
>- 관리 콘솔은 Safari에서 지원되지 않습니다.
>- 서신 관리는 AEM 6.1 forms용 Windows® Internet Explorer 9.0을 지원하지 않습니다.
>- Forms 포털은 접근성을 위해 Internet Explorer 11에서 JAWS 14.0 화면 판독기 소프트웨어를 지원합니다.

#### 모바일 클라이언트 {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>브라우저(기본)</strong></p> </th>
   <th><p><strong>지원되는 패치 정의</strong></p> </th>
  </tr>
  <tr>
   <td><p>Android™ 4.1.2 이상 버전의 Chrome</p> </td>
   <td><p>모든 업데이트</p> </td>
  </tr>
  <tr>
   <td>iOS 15.1 이상 버전의 Safari</td>
   <td>모든 업데이트</td>
  </tr>
  <tr>
   <td>Microsoft® Edge<br /> </td>
   <td>모든 업데이트<br /> </td>
  </tr>
  <tr>
   <td>Android™ 4.4 이상 버전의 기본 Android™ 브라우저</td>
   <td>모든 업데이트</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>- Forms 포털은 iPad의 Safari에서만 지원됩니다.

### AEM Forms 앱 {#aem-forms-workspace-app}

#### 모바일 장치 지원 {#mobile-device-support}

AEM Forms 앱은 다음 플랫폼에서 사용할 수 있습니다.

| **플랫폼** | **지원되는 장치** |
| --- | --- |
| Apple iOS | Apple iPhone, iPad, iPad Air 및 iPad mini(iOS 15.1 이상 실행) |
| Google Android™ | Android™ 5.1 이상 AEM Forms 앱은 7인치 및 10인치 삼성 갤럭시 태블릿과 인기 있는 스마트폰에서 인증을 받았습니다. |
| Microsoft® Windows | Microsoft® Microsoft® Windows 10 운영 체제를 실행하는 표면 장치, 태블릿, 노트북 및 데스크탑 |

### Microsoft® Office용 Adobe 문서 보안 확장 {#adobe-rights-management-extension-for-microsoft-office}

Microsoft® Office용 Adobe Document Security Extension에 대한 시스템 요구 사항을 보려면 [여기](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html)를 클릭하십시오.

### 클라이언트 지원에 대한 예외 {#exceptions-to-client-support}

AEM Forms on JEE는 지원되는 소프트웨어의 지정된 주 버전 및 부 버전 위에 업데이트, 패치 및 수정 팩을 지원합니다. 그러나 지정하지 않는 한 다음 주 버전 또는 부 버전으로의 업데이트는 지원되지 않습니다.

## 타사 패치 지원 정책 {#third-party-patch-support-policy}

AEM Forms on JEE에 대한 타사 소프트웨어 요구 사항은 해당 제품 문서의 &quot;시스템 요구 사항&quot; 섹션에 설명되어 있습니다. [https://adobe.com/go/learn_aemforms_documentation_65_kr](https://adobe.com/go/learn_aemforms_documentation_65_kr)에서 모든 설명서에 액세스합니다.

JEE의 서드파티 참조 플랫폼인 AEM Forms은 JEE의 AEM Forms을 개발 및 릴리스하는 동안 현재 존재하는 서드파티 인프라의 특정 패치 수준과 JEE의 해당 버전의 AEM Forms에서 지원하는 인프라의 최소 패치/서비스 팩 수준을 설명합니다.

Adobe은 타사 공급업체가 JEE의 AEM Forms이 지원하는 버전과의 이전 버전과의 호환성을 보장한다고 가정하고 출시 시 타사 공급업체에서 발급하는 긴급 패치 또는 권장 패치를 지원합니다. Adobe은 AEM Forms on JEE 설명서에 명시된 최소 패치 수준 이후에 릴리스된 패치만 지원합니다.

경우에 따라 Adobe은 주요 기능을 변경하는 서드파티 업데이트를 지원하지 않으므로 전체 이전 버전과의 호환성을 지원하지 않습니다. 지원되는 업데이트에 대한 자세한 내용은 특정 공급업체 제품 및 Adobe에서 지원하는 패치 유형에 대해 [지원되는 패치 정의](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html)를 참조하십시오.

Adobe이 제어할 수 없는 상황에서 이전 버전과의 호환성을 주장하는 타사 패치는 Adobe 제품이나 고객 환경에 부정적인 영향을 미칠 수 있습니다. 이러한 경우 Adobe은 고객이 중요한 시스템에 적용하기 전에 서드파티의 긴급 패치가 미치는 영향을 평가하도록 권장합니다. Adobe은 일반적인 Adobe 지원 프로그램을 통해 또는 제3자가 해당 패치의 문제를 수정하여 이러한 문제를 해결하기 위해 합리적인 비즈니스 노력을 사용하는 제3자와 협력합니다. 이는 Adobe에서 지원할 새로 릴리스된 타사 패치가 공급업체나 JEE의 AEM Forms에서 문서화한 대로 작동함을 보장하지 않습니다.

Adobe은 JEE 릴리스의 AEM Forms에서 지원하는 타사 참조 플랫폼과 해당 시점에 지원되는 패치 정의를 변경할 수 있는 권한을 보유합니다.

타사 패치에 대한 추가 정보는 Adobe 엔터프라이즈 지원 사이트에서 제품과 관련된 기술 문서를 검색하여 찾을 수도 있습니다.

<!--

## Platform updates {#platform-updates}

The following platforms are marked as deprecated with AEM Forms 6.5.18.0 release on August 31, 2023:

- Microsoft&reg; Windows Server 2019 (64-bit)
- Microsoft&reg; Active Directory 2016

The following platforms are marked as deprecated with AEM Forms 6.5.13.0 release on June 2, 2022:
- Microsoft&reg; SharePoint 2016

The following platforms are marked as deprecated with AEM Forms 6.5.10.0 release on September 7, 2021:

- Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/kr/support/programs/eol-matrix.html).
- Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
- Microsoft&reg; Windows Server 2016 (64-bit) 
- Microsoft&reg; Office 2016
- OpenOffice 4.1.2

-->


<!--## Revision History {#revision-history}-->

<!--

- 6.5.18.0 (Aug 31, 2023)
  - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
    - MongoDB Enterprise 4.4
    - Oracle WebLogic Server 14c
    - My SQL JDBC connector 8
    - Active Directory 2022
    - Microsoft&reg; Windows Server 2022 (64-bit)

  - **Removed support**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
    - Windows Server 2016 (64-bit)
    - MongoDB Enterprise 4.0
    - Oracle Database 12c Release 2 (12.2.0.1.0)
    - MySQL 5.7.35
    - Microsoft&reg; SQL Server 2016
    - JBoss&reg; EAP 7.1.4
    - My SQL JDBC connector 5.1.44
    - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
    - Microsoft&reg; SQL Server JDBC driver 6.2.2.0
    - Microsoft&reg; JDBC Driver 8.x for SQL Server

    The release has also removed support for the following platforms for PDF Generator and in-general:
    - Microsoft&reg; Sharepoint 2016
    - Microsoft&reg; Office 2016
    - Microsoft&reg; Office Visio 2016 
    - Microsoft&reg; Publisher 2016
    - Microsoft&reg; Project 2016
    - OpenOffice 4.1.2
    - Acrobat 2017 (Classic track) Version 17.011.30078 or later

  - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:
    - Microsoft&reg; Windows Server 2019 (64-bit)
    - Microsoft&reg; Active Directory 2016
    
- 6.5.13.0 (June 2, 2022)

  The following platforms are deprecated with AEM Forms 6.5.13.0 release on:
 
  - Microsoft&reg; SharePoint 2016

- 6.5.12.0 (March 3, 2022)

    - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
      - IBM&reg; J9 Virtual Machine (build 2.8, JRE 1.8.0)
      - Oracle Database 12c Release 1
      - Oracle Database 18c
      - Oracle Unified Directory (OUD) 11g Release 2
      - IBM&reg; Lotus Domino 9.0
      - IBM&reg; FileNet 5.2
      - Adobe Flash Player

    - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:

      - MongoDB Enterprise 4.0
      - MongoDB Enterprise 4.2
      - IBM&reg; DB2&reg; 11.1
      - Oracle Database 12c Release 2
      - MySQL 5.7.35
      - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
      - JBoss&reg; Enterprise Application Platform (EAP) 7.1.4
      - IBM&reg; Content Manager Server 8.5 Fix pack 2
      - IBM&reg; Content Manager Client 8.5
      - Microsoft&reg; SQL Server 2016

- 6.5.10.0 (Sep 01, 2022)

  - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platform:
  
    - Oracle Java&trade; SE 11 (64 bit) SDK for application server JBoss&reg; EAP 7.4.
  - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:

    - Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/kr/support/programs/eol-matrix.html).
    - Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
    - Microsoft&reg; Windows Server 2016 (64-bit) 
    - Microsoft&reg; Office 2016
    - OpenOffice 4.1.2


-->
<!--
### Release 6.5.19.1 (Dec 15, 2023)

| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 6.0 |MongoDB Enterprise 4.4   |  |
| MongoDB Enterprise 5.0 |  |  |
|  | |  |

### Release 6.5.18.0 (Aug 31, 2023)

| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 4.4 | Windows Server 2016 (64-bit) | Microsoft&reg; Windows Server 2019 (64-bit) |
| Oracle WebLogic Server 14c | MongoDB Enterprise 4.0 | Microsoft&reg; Active Directory 2016 |
| My SQL JDBC connector 8 | Oracle Database 12c Release 2 (12.2.0.1.0) |  |
| Active Directory 2022 | MySQL 5.7.35 |  |
| Microsoft&reg; Windows Server 2022 (64-bit) | Microsoft&reg; SQL Server 2016 |  |
|  | JBoss&reg; EAP 7.1.4 |  |
|  | My SQL JDBC connector 5.1.44 |  |
|  | Microsoft&reg; SQL Server JDBC driver 6.2.1.0 |  |
|  | Microsoft&reg; SQL Server JDBC driver 6.2.2.0 |  |
|  | Microsoft&reg; JDBC Driver 8.x for SQL Server |  |
|  |  |  |
|  | **Removed Support (PDF Generator and In-General):** |  |
|  | Microsoft&reg; Sharepoint 2016 |  |
|  | Microsoft&reg; Office 2016 |  |
|  | Microsoft&reg; Office Visio 2016 |  |
|  | Microsoft&reg; Publisher 2016 |  |
|  | Microsoft&reg; Project 2016 |  |
|  | OpenOffice 4.1.2 |  |
|  | Acrobat 2017 (Classic track) Version 17.011.30078 or later |  |


### Release 6.5.13.0 (June 2, 2022)

| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
|  |  | Microsoft&reg; SharePoint 2016 |


### Release 6.5.12.0 (March 3, 2022)

| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
|  | IBM&reg; J9 Virtual Machine (build 2.8, JRE 1.8.0) | MongoDB Enterprise 4.0 |
|  | Oracle Database 12c Release 1 | MongoDB Enterprise 4.2 |
|  | Oracle Database 18c | IBM&reg; DB2&reg; 11.1 |
|  | Oracle Unified Directory (OUD) 11g Release 2 | Oracle Database 12c Release 2 |
|  | IBM&reg; Lotus Domino 9.0 | MySQL 5.7.35 |
|  | IBM&reg; FileNet 5.2 | Microsoft&reg; SQL Server JDBC driver 6.2.1.0 |
|  | Adobe Flash Player | JBoss&reg; Enterprise Application Platform (EAP) 7.1.4 |
|  | | IBM&reg; Content Manager Server 8.5 Fix pack 2 |
|  | | IBM&reg; Content Manager Client 8.5 |
|  | | Microsoft&reg; SQL Server 2016 |
|  | | Microsoft&reg; Windows Server 2016 |

### Release 6.5.10.0 (September 01, 2022)

| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
| Oracle Java&trade; SE 11 (64 bit) SDK for application server JBoss&reg; EAP 7.4. | | [Adobe Acrobat 2017 - Core support for Adobe Acrobat 2017 ends on June 6, 2022.](https://helpx.adobe.com/kr/support/programs/eol-matrix.html)|
|  | Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)| |
|  | | Microsoft&reg; Windows Server 2016 (64-bit)|
|  | | Microsoft&reg; Office 2016 |
|  | | OpenOffice 4.1.2 |


>[!NOTE]
>
> A deprecated platform continue to receive support until the next full installer release or until third-party vendor support for the platform reaches its end-of-life, whichever is earlier.
-->
<!-- 
- Oct 10, 2021

  - Changed supported version of iOS for AEM Forms App to iOS 15.1. The previous version was iOS 12.

- Sep 07, 2021
  - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
    - [!DNL Adobe Acrobat 2020]
    - [!DNL Ubuntu 20.04]
    - [!DNL Open Office 4.1.10]
    - [!DNL Microsoft&reg;&reg; Office 2016]
    - [!DNL Microsoft&reg;&reg; Windows Server 2016]
    - [!DNL RHEL8]

- Dec 03, 2020
  - Support added with AEM Forms 6.5.7.0 or later for the following platform:
    - [!DNL Microsoft&reg;&reg; SQL Server 2019]

- Sep 09, 2020

    - Changed supported version of iOS for AEM Forms App to iOS 12. The previous version was iOS 11.

-->
