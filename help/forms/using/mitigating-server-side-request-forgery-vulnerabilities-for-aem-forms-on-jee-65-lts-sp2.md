---
title: JEE 6.5 LTS SP2에서 AEM Forms의 SSRF(서버측 요청 위조) 취약성 완화
description: JBoss에서 실행되는 JEE 6.5 LTS 서비스 팩 2 배포의 AEM Forms에 대한 SSRF(서버측 요청 위조) 취약성 완화 단계.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
solution: Experience Manager, Experience Manager Forms
feature: Security
role: Admin
exl-id: 7c4a9e12-3b8f-4d6a-9f1e-2a5c8d7e6b04
source-git-commit: 314aafaec6b45d7ea929f32d47e73da293800d4b
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---

# SSRF(서버측 요청 위조) 취약성 완화

## 빠른 참조 {#quick-reference}

| 영향 수준 | 영향을 받는 버전 | 권장 작업 |
| --- | --- | --- |
| 심각 | JEE 6.5 LTS 서비스 팩 2의 AEM Forms(6.5 LTS SP2) | [핫픽스](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear) 수동 설치 |
| 영향을 받지 않음 | AEM Forms on OSGi, Workbench, Cloud Service | 필요한 액션 없음 |

**해결된 취약점:**

* SSRF(서버측 요청 위조) (CWE-918)

## 개요 {#overview}

### 영향을 받는 사항 {#whats-affected}

| 취약성 | 영향 | 영향을 받는 구성 요소 |
| --- | --- | --- |
| SSRF(서버측 요청 위조) (CWE-918) | 공격자는 서버가 내부 또는 외부 리소스에 대해 의도하지 않은 요청을 하도록 유도할 수 있다 | JEE 6.5 LTS SP2의 AEM Forms |

### 영향을 받지 않는 사항 {#whats-not-affected}

* Experience Manager Forms Workbench (모든 버전)
* OSGi의 Experience Manager Forms(모든 버전)
* Experience Manager Forms as a Cloud Service

## 해결 옵션 {#resolution-options}

### 시작하기에 앞서 {#before-you-start}

변경하기 전에 교체하려는 EAR 파일을 백업하십시오.

* 배포 디렉터리에서 `adobe-edcserver-jboss.ear`을(를) 찾습니다.

  ```text
  [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
  ```

* 파일을 배포 디렉터리 외부의 보안 백업 위치에 복사합니다.
* 업데이트를 진행하기 전에 백업이 완료되고 액세스할 수 있는지 확인하십시오.

이 주의 사항을 사용하면 업데이트 프로세스 중에 문제가 발생하는 경우 원래 상태를 복원할 수 있습니다.

### JEE 6.5 LTS SP2(JBoss)의 AEM Forms용 수동 핫픽스 설치

1. [Adobe 소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear)에서 `adobe-edcserver-jboss.ear`을(를) 다운로드합니다.

1. 배포 디렉터리에서 `adobe-edcserver-jboss.ear`을(를) 찾아 다운로드한 파일로 바꿉니다.

   ```text
   [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
   ```

1. AEM Forms 구성 관리자를 시작하여 업데이트된 EAR을 다시 배포하고 핫픽스를 적용합니다.

1. 응용 프로그램 서버를 다시 시작하고 서버 로그에서 배포가 성공했는지 확인합니다.

## 참조 {#references}

* [Adobe Experience Manager Forms 보안 우수 사례](/help/forms/using/hardening-securing-aem-forms-environment.md)
