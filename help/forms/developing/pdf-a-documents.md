---
title: PDF/A 문서 작업
description: DocConverter 서비스를 사용하여 PDF 문서가 PDF/A 문서인지 확인하고 PDF 문서를 PDF/A 문서로 변환합니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Document Services, APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 387f917c-eae3-4326-88f4-3b77cb9e4d46
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 1%

---

# PDF/A 문서 작업 {#working-with-pdf-a-documents}

**DocConverter 서비스 정보**

DocConverter 서비스는 PDF 문서를 PDA/A 문서로 변환할 수 있습니다. 이 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* PDF 문서를 PDF/A 문서로 변환합니다. ([문서를 PDF/A 문서로 변환](pdf-a-documents.md#converting-documents-to-pdf-a-documents)을 참조하십시오.)
* PDF 문서가 PDF/A 문서인지 확인합니다. ([프로그래밍 방식으로 PDF/A 규정 준수 확인](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)을 참조하십시오.)

>[!NOTE]
>
>DocConverter 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## 문서를 PDF/A 문서로 변환 {#converting-documents-to-pdf-a-documents}

DocConverter 서비스를 사용하여 PDF 문서를 PDF/A 문서로 변환할 수 있습니다. PDF/A는 문서 내용을 장기간 보존하기 위한 보관 형식이므로 모든 글꼴이 임베드되고 파일이 압축 해제됩니다. 따라서 PDF/A 문서는 일반적으로 표준 PDF 문서보다 큽니다. 또한 PDF/A 문서에는 오디오 및 비디오 콘텐츠가 포함되어 있지 않습니다. PDF 문서를 PDF/A 문서로 변환하려면 먼저 PDF 문서가 PDF/A 문서가 아닌지 확인합니다.

PDF/A-1 사양은 두 가지 적합성 수준, 즉 A와 B로 구성됩니다. 두 요소의 주요 차이점은 적합성 수준 B에 필요하지 않은 논리 구조(접근성) 지원에 대한 것입니다. 적합성 수준에 관계없이 PDF/A-1은 모든 글꼴이 생성된 PDF/A 문서 내에 임베드되도록 지시합니다. 현재 유효성 검사(및 전환)에서는 PDF/A-1b만 지원됩니다.

PDF/A는 PDF 문서를 보관하는 표준이지만 표준 PDF 문서가 회사의 요구 사항을 충족하는 경우 PDF/A를 보관에 사용해야 하는 것은 아닙니다. PDF/A 표준의 목적은 장기적인 보관 및 문서 보존 요구 사항을 위한 PDF 파일을 설정하는 것입니다.

>[!NOTE]
>
>DocConverter 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary-of-steps}

PDF 문서를 PDF/A 문서로 변환하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. DocConvert 클라이언트 만들기
1. PDF 문서를 참조하여 PDF/A 문서로 변환합니다.
1. 추적 정보를 설정합니다.
1. 문서를 변환합니다.
1. PDF/A 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**DocConvert 클라이언트 만들기**

DocConverter 작업을 프로그래밍 방식으로 수행하려면 먼저 DocConverter 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `DocConverterServiceClient` 개체를 만듭니다. DocConverter 웹 서비스 API를 사용하는 경우 `DocConverterServiceService` 개체를 만듭니다.

**PDF/A 문서로 변환하려면 PDF 문서를 참조하십시오**

PDF 문서를 검색하여 PDF/A 문서로 변환합니다. Acrobat 양식과 같은 PDF 문서를 PDF/A 문서로 변환하려고 하면 예외가 발생합니다.

**추적 정보 설정**

변환 프로세스 중에 추적되는 정보의 양을 결정하는 런타임 옵션을 설정할 수 있습니다. 즉, PDF 문서를 PDF/A 문서로 변환할 때 DocConverter 서비스가 추적하는 정보의 양을 지정하는 9개의 서로 다른 수준을 설정할 수 있습니다.

**문서 변환**

DocConverter 서비스 클라이언트를 만든 후 변환할 PDF 문서를 참조하고 추적되는 정보의 양을 지정하는 런타임 옵션을 설정하면 PDF 문서를 PDF/A 문서로 변환할 수 있습니다.

**PDF/A 문서 저장**

PDF/A 문서를 PDF 파일로 저장할 수 있습니다.

**추가 참조**

[Java API를 사용하여 문서를 PDF/A 문서로 변환](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[웹 서비스 API를 사용하여 문서를 PDF/A 문서로 변환](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF/A 준수 여부 확인](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Java API를 사용하여 문서를 PDF/A 문서로 변환 {#convert-documents-to-pdf-a-documents-using-the-java-api}

Java API를 사용하여 PDF 문서를 PDF/A 문서로 변환합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-docconverter-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. DocConvert 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `DocConverterServiceClient` 개체를 만듭니다.

1. PDF 문서를 참조하여 PDF/A 문서로 변환

   * 생성자를 사용하고 PDF 파일의 위치를 지정하는 문자열 값을 전달하여 변환할 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 추적 정보 설정

   * 해당 생성자를 사용하여 `PDFAConversionOptionSpec` 개체를 만듭니다.
   * `PDFAConversionOptionSpec` 개체의 `setLogLevel` 메서드를 호출하고 추적 수준을 지정하는 문자열 값을 전달하여 정보 추적 수준을 설정하십시오. 예를 들어 값 `FINE`을(를) 전달합니다. 다른 값에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)에서 `setLogLevel` 메서드를 참조하십시오.

1. 문서 변환

   `DocConverterServiceClient` 개체의 `toPDFA` 메서드를 호출하고 다음 값을 전달하여 PDF 문서를 PDF/A 문서로 변환합니다.

   * 변환할 PDF 문서가 포함된 `com.adobe.idp.Document` 개체
   * 추적 정보를 지정하는 `PDFAConversionOptionSpec` 개체

   `toPDFA` 메서드가 PDF/A 문서를 포함하는 `PDFAConversionResult` 개체를 반환합니다.

1. PDF/A 문서 저장

   * `PDFAConversionResult` 개체의 `getPDFA` 메서드를 호출하여 PDF/A 문서를 검색합니다. 이 메서드는 PDF/A 문서를 나타내는 `com.adobe.idp.Document` 개체를 반환합니다.
   * PDF/A 파일을 나타내는 `java.io.File` 개체를 만듭니다. 파일 이름 확장명이 .pdf인지 확인합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하고 `java.io.File` 개체를 전달하여 파일을 PDF/A 데이터로 채웁니다.

**추가 참조**

[PDF/A 문서 작업](pdf-a-documents.md#working-with-pdf-a-documents)

[빠른 시작(SOAP 모드): Java API를 사용하여 문서를 PDF/A 문서로 변환](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 문서를 PDF/A 문서로 변환 {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

DocConverter API(웹 서비스)를 사용하여 PDF 문서를 PDF/A 문서로 변환합니다.

1. 프로젝트 파일 포함

   * DocConverter WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. DocConvert 클라이언트 만들기

   * Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `DocConverterServiceService` 개체를 만듭니다.
   * `DocConverterServiceService` 개체의 `Credentials` 데이터 구성원을 사용자 이름과 암호 값을 지정하는 `System.Net.NetworkCredential` 값으로 설정하십시오.

1. PDF 문서를 참조하여 PDF/A 문서로 변환

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 PDF/A 문서로 변환된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `binaryData` 속성을 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. 추적 정보 설정

   * 해당 생성자를 사용하여 `PDFAConversionOptionSpec` 개체를 만듭니다.
   * 추적 수준을 지정하는 값을 `PDFAConversionOptionSpec` 개체의 `logLevel` 데이터 멤버에 할당하여 정보 추적 수준을 설정합니다. 예를 들어 이 데이터 멤버에 값 `FINE`을(를) 할당합니다.

1. 문서 변환

   `DocConverterServiceService` 개체의 `toPDFA` 메서드를 호출하고 다음 값을 전달하여 PDF 문서를 PDF/A 문서로 변환합니다.

   * 변환할 PDF 문서가 포함된 `BLOB` 개체
   * 추적 정보를 지정하는 `PDFAConversionOptionSpec` 개체

   `toPDFA` 메서드가 PDF/A 문서를 포함하는 `PDFAConversionResult` 개체를 반환합니다.

1. PDF/A 문서 저장

   * `PDFAConversionResult` 개체의 `PDFADocument` 데이터 멤버 값을 가져와서 PDF/A 문서를 저장하는 `BLOB` 개체를 만듭니다.
   * `PDFAConversionResult` 개체를 사용하여 반환된 `BLOB` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `binaryData` 데이터 멤버의 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 PDF/A 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

**추가 참조**

[PDF/A 문서 작업](pdf-a-documents.md#working-with-pdf-a-documents)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 프로그래밍 방식으로 PDF/A 준수 여부 확인 {#programmatically-determining-pdf-a-compliancy}

DocConverter 서비스를 사용하여 PDF 문서가 PDF/A를 준수하는지 여부를 확인할 수 있습니다. PDF/A 문서와 PDF 문서를 PDF/A 문서로 변환하는 방법에 대한 자세한 내용은 [문서를 PDF/A 문서로 변환](pdf-a-documents.md#converting-documents-to-pdf-a-documents)을 참조하십시오.

>[!NOTE]
>
>DocConverter 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-1}

PDF/A 준수 여부를 확인하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. DocConvert 클라이언트 만들기
1. PDF/A 준수 여부를 확인하는 데 사용되는 PDF 문서를 참조하십시오.
1. 런타임 옵션을 설정합니다.
1. PDF 문서에 대한 정보를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**DocConvert 클라이언트 만들기**

DocConverter 작업을 프로그래밍 방식으로 수행하려면 먼저 DocConverter 클라이언트를 만들어야 합니다. Java API를 사용하는 경우 `DocConverterServiceClient` 개체를 만듭니다. DocConverter 웹 서비스 API를 사용하는 경우 `DocConverterServiceService` 개체를 만듭니다.

**PDF/A 준수 여부를 확인하는 데 사용되는 PDF 문서를 참조하십시오**

PDF 문서를 참조하고 DocConverter 서비스에 전달하여 PDF 문서가 PDF/A와 호환되는지 여부를 확인해야 합니다.

**런타임 옵션 설정**

변환 프로세스 중에 추적되는 정보의 양을 결정하는 런타임 옵션을 설정할 수 있습니다. 즉, PDF 문서를 PDF/A 문서로 변환할 때 DocConverter 서비스가 추적하는 정보의 양을 지정하는 9개의 서로 다른 수준을 설정할 수 있습니다.

**PDF 문서에 대한 정보를 검색합니다**

DocConverter 서비스 클라이언트를 만들고 PDF 문서를 참조하며 런타임 옵션을 설정한 후 PDF 문서가 PDF/A 호환 문서인지 여부를 결정할 수 있습니다.

**추가 참조**

[Java API를 사용하여 PDF/A 준수 여부 확인](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[웹 서비스 API를 사용하여 PDF/A 준수 여부 확인](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 PDF/A 준수 여부 확인 {#determine-pdf-a-compliancy-using-the-java-api}

Java API를 사용하여 PDF/A 준수 여부를 확인합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-docconverter-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. DocConvert 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `DocConverterServiceClient` 개체를 만듭니다.

1. PDF/A 준수 여부를 확인하는 데 사용되는 PDF 문서 참조

   * 생성자를 사용하고 PDF 파일의 위치를 지정하는 문자열 값을 전달하여 변환할 PDF 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 런타임 옵션 설정

   * 해당 생성자를 사용하여 `PDFAValidationOptionSpec` 개체를 만듭니다.
   * `PDFAValidationOptionSpec` 개체의 `setCompliance` 메서드를 호출하고 `PDFAValidationOptionSpec.Compliance.PDFA_1B`을(를) 전달하여 준수 수준을 설정하십시오.
   * `PDFAValidationOptionSpec` 개체의 `setLogLevel` 메서드를 호출하고 추적 수준을 지정하는 문자열 값을 전달하여 정보 추적 수준을 설정하십시오. 예를 들어 값 `FINE`을(를) 전달합니다. 다른 값에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)에서 `setLogLevel` 메서드를 참조하십시오.

1. PDF 문서에 대한 정보 검색

   `DocConverterServiceClient` 개체의 `isPDFA` 메서드를 호출하고 다음 값을 전달하여 PDF/A 호환성을 확인합니다.

   * PDF 문서가 포함된 `com.adobe.idp.Document` 개체입니다.
   * 런타임 옵션을 지정하는 `PDFAValidationOptionSpec` 개체입니다.

   `isPDFA` 메서드가 이 작업의 결과를 포함하는 `PDFAValidationResult` 개체를 반환합니다.

**추가 참조**

[PDF/A 문서 작업](pdf-a-documents.md#working-with-pdf-a-documents)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF/A 준수 여부 확인](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 PDF/A 준수 여부 확인 {#determine-pdf-a-compliancy-using-the-web-service-api}

웹 서비스 API를 사용하여 PDF/A 준수 여부를 확인합니다.

1. 프로젝트 파일 포함

   * DocConverter WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. DocConvert 클라이언트 만들기

   * Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `DocConverterServiceService` 개체를 만듭니다.
   * `DocConverterServiceService` 개체의 `Credentials` 데이터 구성원을 사용자 이름과 암호 값을 지정하는 `System.Net.NetworkCredential` 값으로 설정하십시오.

1. PDF/A 준수 여부를 확인하는 데 사용되는 PDF 문서 참조

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 PDF/A 문서로 변환된 PDF 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `binaryData` 속성을 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. 런타임 옵션 설정

   * 해당 생성자를 사용하여 `PDFAValidationOptionSpec` 개체를 만듭니다.
   * 값이 `PDFAConversionOptionSpec_Compliance.PDFA_1B`인 `PDFAValidationOptionSpec` 개체의 `compliance` 데이터 구성원을 할당하여 준수 수준을 설정하십시오.
   * 값이 `PDFAValidationOptionSpec_ResultLevel.DETAILED`인 `PDFAValidationOptionSpec` 개체의 `resultLevel` 데이터 구성원을 할당하여 정보 추적 수준을 설정합니다.

1. PDF 문서에 대한 정보 검색

   `DocConverterServiceService` 개체의 `isPDFA` 메서드를 호출하고 다음 값을 전달하여 PDF/A 호환성을 확인합니다.

   * PDF 문서가 포함된 `BLOB` 개체입니다.
   * 런타임 옵션이 포함된 `PDFAValidationOptionSpec` 개체입니다.

   `isPDFA` 메서드가 이 작업의 결과를 포함하는 `PDFAValidationResult` 개체를 반환합니다.

**추가 참조**

[PDF/A 문서 작업](pdf-a-documents.md#working-with-pdf-a-documents)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
