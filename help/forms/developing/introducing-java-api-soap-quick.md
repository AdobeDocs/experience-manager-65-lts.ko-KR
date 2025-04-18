---
title: Java 소개&trade; API QuickStart
description: SOAP 연결에 활성화된 AEM Forms Java&trade; 강력한 형식의 API를 사용하여 AEM Forms 작업을 수행하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: a5ae164d-d0c0-40d0-baeb-0e646fc71f55
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Java™ API 빠른 시작 소개 {#introducing-java-api-quickstart}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

Adobe AEM Forms API 빠른 시작을 사용하면 AEM Forms 서비스와 상호 작용하는 프로그램 개발을 위한 노력을 가속화할 수 있습니다. *빠른 시작*&#x200B;은(는) 자체 프로젝트에 복사하여 붙여 넣고 시작점으로 사용할 수 있는 완전한 프로그램입니다. 빠른 시작을 실행하여 작동 방식을 확인하고 필요에 따라 수정할 수 있습니다.

AEM Forms 작업은 AEM Forms 강력한 형식의 API를 사용하여 수행할 수 있으며 연결 모드를 SOAP으로 설정해야 합니다.

Java™ 강력한 형식의 API 빠른 시작은 Java™ 애플리케이션을 실행하는 데 필요한 JAR 파일 목록을 제공합니다. 대부분의 Java™ 빠른 시작은 `main` 내에서 실행되는 콘솔 응용 프로그램입니다. 그러나 Forms Java™ 강력한 형식의 API 빠른 시작은 웹 애플리케이션 내에서 실행되는 Java™ 서블릿으로 구현됩니다.

JAR 파일 목록은 빠른 시작 부분의 주석 섹션에 있습니다. 예를 들어 다음 설명은 출력 빠른 시작에 있으며 각 Java™ 빠른 시작에 있는 일반적인 JAR 파일 목록입니다.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
```

## 다중 서비스 빠른 시작 {#multiple-services-quick-start}

*JEE의 AEM Forms으로 프로그래밍*&#x200B;에서 가장 빠른 시작은 특정 서비스를 호출하여 작업을 수행합니다. 그러나 일부 빠른 시작은 여러 AEM Forms 서비스를 호출하여 주어진 워크플로우를 수행합니다. 다음 목록은 두 개 이상의 AEM Forms 서비스를 호출하는 Java™ 빠른 시작을 제공합니다.

[빠른 시작(SOAP 모드): Java™ API를 사용하여 AEM Forms 저장소의 문서를 출력 서비스에 전달](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)(저장소 및 출력 서비스 호출)

[빠른 시작(SOAP 모드): Java™ API를 사용하여 조각을 기반으로 PDF 문서 만들기](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)(어셈블러 및 출력 서비스 호출)

[빠른 시작(SOAP 모드): Java™ API를 사용하여 제출된 XML 데이터로 PDF 문서 만들기](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api)(Forms, 출력 및 문서 관리 서비스 호출)

[빠른 시작(SOAP 모드): Java™ API를 사용하여 Forms 서비스에 문서 전달](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)(Forms 및 문서 관리 서비스 호출)

[빠른 시작(SOAP 모드): Java™ API를 사용하여 XFA 기반 양식에 디지털 서명합니다](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api)(Forms 및 서명 서비스 호출)

[빠른 시작(SOAP 모드): Java™ API를 사용하여 역할 및 권한 관리](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)(DirectoryManager 및 AuthorizationManager 서비스 호출)

[빠른 시작(SOAP 모드): Java™ API를 사용하여 출력 서비스에 문서 전달](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)(출력 및 문서 관리 서비스 호출)

>[!NOTE]
>
>AEM Forms을 사용한 프로그래밍의 빠른 시작은 JBoss® Application Server 및 Microsoft® Windows® 운영 체제에 배포되는 AEM Forms을 기반으로 합니다. 그러나 UNIX®와 같은 다른 운영 체제를 사용하는 경우에는 Windows 특정 경로를 해당 운영 체제에서 지원하는 경로로 바꿉니다. 마찬가지로 다른 J2EE 응용 프로그램 서버를 사용하는 경우 유효한 연결 속성을 지정해야 합니다. ([연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하세요.)

>[!NOTE]
>
>대부분의 웹 서비스 빠른 시작은 C#으로 작성되며 .NET Framework를 사용합니다. 그러나 SOAP 표준을 지원하는 모든 개발 환경에서 AEM Forms 서비스를 호출할 수 있는 클라이언트 응용 프로그램 논리를 만들 수 있습니다. [웹 서비스를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)을 참조하십시오.
