---
title: JEE의 AEM Forms에 대한 설치 및 업그레이드 워크플로
description: 관련 PDF 및 그 용도의 통합 목록이 포함된 JBoss(JEE의 AEM Forms 6.5 LTS)용 설치 및 업그레이드 워크플로우입니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms on JEE,AEM Forms Upgrade
exl-id: 6d8c0e24-7f08-4e66-bb12-2cf1cfe1d5d3
source-git-commit: fb9f6ef794da7f3b242e9e81a6c2505692c16cd8
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 2%

---


# JEE의 AEM Forms에 대한 설치 및 업그레이드 워크플로 {#aem-forms-jee-installation-upgrade-documentation}

## 적용 대상 {#applies-to}

이 설명서는 **AEM 6.5 LTS Forms**&#x200B;에 적용됩니다.

다음 워크플로우 및 표를 사용하여 시나리오에 적합한 안내서를 선택하십시오. 일부 문서는 PDF로 게시됩니다. 시간이 지남에 따라 사용 가능한 문서가 추가될 수 있습니다.

## 설치 및 업그레이드 워크플로 {#installation-upgrade-workflow}

1. [JEE에서 AEM Forms에 대해 지원되는 플랫폼](/help/forms/using/aem-forms-jee-supported-platforms.md)을 검토하고 시스템이 필요한 소프트웨어/하드웨어 조합을 충족하는지 확인하십시오.
2. **새로 설치**&#x200B;를 수행할지 **업그레이드**&#x200B;를 수행할지 결정하십시오.
3. 선택한 경로에 대해 아래에 설명된 시퀀스를 수행합니다. 일부 시나리오에서는 두 개 이상의 안내서가 필요합니다.

## 사전 설치 및 사전 업그레이드 단계 {#start-here}

| 안내서 | 설명 |
| --- | --- |
| [JEE에서 AEM Forms에 지원되는 플랫폼](/help/forms/using/aem-forms-jee-supported-platforms.md) | JEE의 AEM Forms에 대해 지원되는 소프트웨어 및 하드웨어 조합을 나열합니다. 설치 또는 업그레이드를 시작하기 전에 필수 구성 요소의 유효성을 검사하려면 이 옵션을 사용하십시오. |
| [AEM Forms의 아키텍처 및 배포 토폴로지](/help/forms/using/aem-forms-architecture-deployment.md) | 권장 아키텍처 및 배포 토폴로지에 대해 설명하므로 사용자 환경(예: 단일 서버와 클러스터)에 적합한 접근 방식을 선택할 수 있습니다. |
| [AEM Forms 설치를 위한 지속성 유형 선택](/help/forms/using/choosing-persistence-type-for-aem-forms.md) | 시작하기 전에 설치 토폴로지에 적합한 지속성 유형을 선택하는 데 도움이 됩니다. |

## JBoss의 JEE에 Adobe Experience Manager Forms(AEM Forms)를 설치하려면 어떻게 합니까? {#installing-aem-forms-jee-jboss}

### 턴키 {#install-jee-jboss-turnkey}

| 안내서 | 설명 |
| --- | --- |
| [JBoss 턴키(PDF)를 사용하여 JEE에 AEM Forms 6.5 LTS 설치 및 배포](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-turnkey.pdf) | JBoss에서 **새 턴키 설치**&#x200B;에 사용합니다. 이 문서에서는 JBoss 턴키 배포를 사용하여 JEE에 AEM Forms을 설치하고 배포하는 방법에 대한 지침을 제공합니다. |

### 단일 서버(턴키 아님) {#install-jee-jboss-single-server}

| 안내서 | 설명 |
| --- | --- |
| [AEM Forms(단일 서버)(PDF) 설치 준비 중](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-install-single-server.pdf) | **이전**&#x200B;에 **새 단일 서버(턴키가 아닌 서버) 설치**&#x200B;를 사용합니다. 이 문서에서는 단일 서버 토폴로지에 AEM Forms on JEE를 설치하기 위한 사전 요구 사항 및 환경 준비 단계를 나열합니다. |
| [JBoss(PDF)용 JEE에 AEM Forms 설치 및 배포](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-jboss.pdf) | JBoss에서 JEE의 AEM Forms **단계별 설치 및 배포**(**턴키가 아님**)에 사용합니다. 단일 서버 설치의 경우 **AEM Forms(단일 서버) 설치 준비**&#x200B;를 완료한 후&#x200B;*이 안내서를 따르십시오.* |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **fresh cluster installation**. Describes prerequisites and environment preparation steps for installing AEM Forms on JEE in a server cluster topology. *(Link will be added once the PDF is available.)* |
| [Configuring AEM Forms on JEE on JBoss Cluster (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/cluster-jboss.pdf) | Use when setting up and configuring a **JBoss cluster topology** for AEM Forms on JEE. |
-->

## JBoss의 JEE에서 Adobe Experience Manager Forms(AEM Forms)를 업그레이드하려면 어떻게 합니까? {#upgrading-aem-forms-jee-jboss}

### 턴키 {#upgrade-jee-jboss-turnkey}

| 안내서 | 설명 |
| --- | --- |
| [JBoss 턴키용 JEE의 AEM Forms 6.5 LTS로 업그레이드(PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-turnkey.pdf) | **턴키 업그레이드**&#x200B;에 사용합니다. 이 문서에서는 JEE JBoss 턴키 설치의 기존 AEM Forms을 업그레이드하는 방법에 대한 지침을 제공합니다. |

### 단일 서버 {#upgrade-jee-jboss-single-server}

| 안내서 | 설명 |
| --- | --- |
| [AEM Forms(PDF) 업그레이드 준비 중](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-upgrade.pdf) | **이전**&#x200B;에 **단일 서버 업그레이드**&#x200B;를 사용합니다. AEM 6.5 LTS Forms으로 업그레이드하기 전에 환경을 준비하는 방법에 대해 설명합니다. 단일 서버 설치 모드에서 JEE의 AEM Forms을 실행하는 환경에 적용됩니다. |
| [JBoss(PDF)용 JEE의 AEM Forms으로 업그레이드](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-jboss.pdf) | **단일 서버** 설치 모드에서 JBoss의 **단계별 업그레이드 프로시저**&#x200B;에 사용합니다. **AEM Forms 업그레이드 준비**&#x200B;를 완료하는 *후*&#x200B;에 이 안내서를 따르십시오. |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **cluster upgrade**. Describes how to prepare the environment for a server cluster before upgrading to AEM 6.5 LTS Forms. It applies to environments running AEM Forms on JEE in a server cluster installation mode. *(Link will be added once the PDF is available.)* |
| Upgrading to AEM Forms on JEE for JBoss (Cluster) (PDF) (**TBD**) | Use for the **step-by-step upgrade procedure** on JBoss in a **clustered** installation mode. Follow this guide **after** completing *Preparing to Install AEM Forms (Server Cluster)*. *(Link will be added once the PDF is available.)* | -->

