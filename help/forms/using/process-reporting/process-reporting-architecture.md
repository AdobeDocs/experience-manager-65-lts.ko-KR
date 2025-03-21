---
title: 프로세스 보고 작동 방식
description: JEE 프로세스 보고에서 AEM Forms을 구성하는 서비스에 대한 설명과 프로세스 보고 UI 소개
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: c59e5a1d-a066-48e7-a57e-c28cbb959719
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 프로세스 보고 작동 방식{#how-process-reporting-works}

프로세스 보고는 JEE의 AEM Forms 보고 모듈입니다.

프로세스 보고를 사용하면 AEM Forms 프로세스 및 작업에 대한 보고서를 실행할 수 있습니다.

프로세스 보고에서는 포함된 프로세스 보고 저장소를 사용하여 Forms 데이터를 게시합니다. 그런 다음 해당 데이터를 사용하여 보고서를 실행합니다.

프로세스 보고는 다음 모듈로 구성됩니다.

* [ProcessDataPublisher 서비스](#processdatapublisher-service-br-p)
* [ProcessDataStorage 서비스](#processdatastorageprovider-service-br-p)
* [OSGI 서비스](#osgi-service-br-p)
* [쿼리 데이터 서블릿](#querydataservlet-service-br-p)
* [프로세스 보고 사용자 인터페이스](#process-reporting-user-interface-br-p)

## 프로세스 보고 아키텍처 {#process-reporting-architecture-br}

![processreportingarchitecture](assets/processreportingarchitecture.png)

## 프로세스 보고 모듈 {#process-reporting-modules}

### ProcessDataPublisher 서비스 {#processdatapublisher-service-br}

ProcessDataPublisher 서버는 AEM Forms 데이터베이스에서 주기적으로 실행되고 마지막 서비스 실행 이후 변경된 데이터를 추출합니다. 그런 다음 데이터를 프로세스 데이터 스토리지 서비스에 게시합니다.

서비스 구성에 대한 자세한 내용은 [ProcessDataPublisher 서비스 구성](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)을 참조하십시오.

### ProcessDataStorageProvider 서비스 {#processdatastorageprovider-service-br}

ProcessDataStorageProvider 서비스는 ProcessDataPublisher 서비스로부터 프로세스 데이터를 수신하여 Process Reporting 저장소에 저장합니다.

서비스 구성에 대한 자세한 내용은 [ProcessDataStorageProvider 서비스 구성](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)을 참조하십시오.

### OSGI 서비스 {#osgi-service-br}

QueryDataServlet은 이 서비스를 사용하여 프로세스 보고 저장소에서 보고 데이터를 가져옵니다.

### QueryDataServlet 서비스 {#querydataservlet-service-br}

QueryDataServlet 서비스는 Process Reporting 사용자 인터페이스에서 쿼리를 수락합니다.

그런 다음 이 서비스는 OSGi 서비스를 사용하여 관련 보고 데이터를 가져오고 데이터를 처리한 다음 사용자 인터페이스로 데이터를 반환합니다.

### 프로세스 보고 사용자 인터페이스 {#process-reporting-user-interface-br}

프로세스 보고 사용자 인터페이스는 웹 브라우저 기반 인터페이스입니다. 이 인터페이스를 사용하여 AEM Forms 데이터베이스에서 게시되는 프로세스 및 작업 정보를 볼 수 있습니다.

Process Reporting 사용자 인터페이스에 대한 소개는 [Process Reporting 사용자 인터페이스](/help/forms/using/process-reporting/introduction-process-reporting.md)를 참조하십시오.

### QueryDataServlet 서비스 {#querydataservlet-service-br-1}

QueryDataServlet 서비스는 Process Reporting 사용자 인터페이스에서 쿼리를 수락합니다.

그런 다음 이 서비스는 OSGi 서비스를 사용하여 관련 보고 데이터를 가져오고 데이터를 처리한 다음 사용자 인터페이스로 데이터를 반환합니다.

### 사용자 정의 보고서 {#custom-reports-br}

고유한 사용자 지정 보고서를 만들고 이러한 보고서를 프로세스 보고 사용자 인터페이스의 사용자 지정 보고서 탭에 표시할 수 있습니다.

사용자 지정 보고서를 만드는 단계는 문서 [보고 중인 사용자 지정 보고서](/help/forms/using/process-reporting/process-reporting-custom-reports.md)에서 사용자 지정 보고서 만들기 를 참조하십시오.
