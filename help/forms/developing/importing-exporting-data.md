---
title: 데이터 가져오기 및 내보내기
description: 양식 데이터 통합 서비스를 사용하여 데이터를 PDF 양식으로 가져오고 Java API 및 웹 서비스 API를 사용하여 PDF 양식에서 데이터를 내보냅니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 2e8b73eb-7070-4b7b-b14b-bfcca6175afb
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2754'
ht-degree: 0%

---

# 데이터 가져오기 및 내보내기 {#importing-and-exporting-data}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

## 양식 데이터 통합 서비스 정보 {#about-the-form-data-integration-service}

양식 데이터 통합 서비스는 데이터를 PDF 양식으로 가져오고 PDF 양식에서 데이터를 내보낼 수 있습니다. 가져오기 및 내보내기 작업은 두 가지 유형의 PDF forms을 지원합니다.

* Acrobat 양식(Acrobat에서 작성)은 양식 필드를 포함하는 PDF 문서입니다.
* Adobe XML 양식(Designer에서 작성)은 XML Adobe XML Forms 아키텍처(XFA)를 준수하는 PDF 문서입니다.

양식 데이터는 PDF 양식의 유형에 따라 다음 형식 중 하나로 존재할 수 있습니다.

* Acrobat 양식 데이터 형식의 XML 버전인 XFDF 파일입니다.
* 양식 필드 정의가 포함된 XML 파일인 XDP 파일입니다. 양식 필드 데이터와 포함된 PDF 파일도 포함될 수 있습니다. Designer에서 생성한 XDP 파일은 포함된 base 64로 인코딩된 PDF 문서를 포함하는 경우에만 사용할 수 있습니다.

양식 데이터 통합 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* PDF forms으로 데이터를 가져옵니다. 자세한 내용은 [양식 데이터 가져오기](importing-exporting-data.md#importing-form-data)를 참조하십시오.
* PDF forms에서 데이터를 내보냅니다. 자세한 내용은 [양식 데이터 내보내기](importing-exporting-data.md#exporting-form-data)를 참조하십시오.

>[!NOTE]
>
>양식 데이터 통합 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## 양식 데이터 가져오기 {#importing-form-data}

양식 데이터 통합 서비스를 사용하여 양식 데이터를 대화형 PDF forms으로 가져올 수 있습니다. 대화형 PDF 양식은 사용자로부터 정보를 수집하거나 사용자 정의 정보를 표시하기 위한 하나 이상의 필드가 포함된 PDF 문서입니다. 양식 데이터 통합 서비스는 양식 계산, 유효성 검사 또는 스크립팅을 지원하지 않습니다.

Designer에서 만든 양식으로 데이터를 가져오려면 유효한 XDP XML 데이터 소스를 참조해야 합니다. 다음 예제 모기지 신청 양식을 고려하십시오.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

데이터 값을 이 양식으로 가져오려면 양식에 해당하는 유효한 XDP XML 데이터 소스가 있어야 합니다. 임의의 XML 데이터 소스를 사용하여 양식 데이터 통합 서비스를 사용하여 데이터를 양식으로 가져올 수 없습니다. 임의의 XML 데이터 소스와 XDP XML 데이터 소스의 차이점은 XDP 데이터 소스가 XFA(XML Forms Architecture)를 준수한다는 것입니다. 다음 XML은 예제 담보 대출 신청 양식에 해당하는 XDP XML 데이터 소스를 나타냅니다.

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

>[!NOTE]
>
>양식 데이터 통합 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary-of-steps}

양식 데이터를 PDF 양식으로 가져오려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.
1. PDF 양식을 참조하십시오.
1. XML 데이터 소스를 참조합니다.
1. PDF 양식으로 데이터를 가져옵니다.
1. PDF 양식을 PDF 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar (AEM Forms이 JBoss에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**양식 데이터 통합 서비스 클라이언트 만들기**

프로그래밍 방식으로 PDF form 클라이언트 API로 데이터를 가져오려면 먼저 데이터 통합 서비스 클라이언트를 만들어야 합니다. 서비스 클라이언트를 만들 때 서비스를 호출하는 데 필요한 연결 설정을 정의합니다. 자세한 내용은 [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.

**PDF 양식 참조**

데이터를 PDF 양식으로 가져오려면 Designer에서 만든 XML 양식 또는 Acrobat에서 만든 Acrobat 양식을 참조해야 합니다.

**XML 데이터 원본 참조**

양식 데이터를 가져오려면 유효한 데이터 소스를 참조해야 합니다. Designer에서 만든 XFA XML 양식으로 데이터를 가져오려면 XDP XML 데이터 소스를 사용해야 합니다. Acrobat 양식을 참조하는 경우 XFDF 데이터 소스를 사용해야 합니다. 데이터를 가져올 각 필드에 값을 지정해야 합니다. XML 데이터 소스의 요소가 양식의 필드에 해당하지 않으면 요소가 무시됩니다.

**PDF 양식으로 데이터 가져오기**

PDF 양식 및 유효한 XML 데이터 소스를 참조한 후 데이터를 PDF 양식으로 가져올 수 있습니다.

**PDF 양식을 PDF 파일로 저장**

데이터를 양식으로 가져온 후 양식을 PDF 파일로 저장할 수 있습니다. PDF 파일로 저장되면 사용자는 Adobe Reader 또는 Acrobat에서 양식을 열고 가져온 데이터가 있는 양식을 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 양식 데이터 가져오기](importing-exporting-data.md#import-form-data-using-the-java-api)

[웹 서비스 API를 사용하여 양식 데이터 가져오기](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[양식 데이터 통합 서비스 API 빠른 시작](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[양식 데이터 내보내기](importing-exporting-data.md#exporting-form-data)

### Java API를 사용하여 양식 데이터 가져오기 {#import-form-data-using-the-java-api}

양식 데이터 통합 API(Java)를 사용하여 양식 데이터 가져오기:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-formdataintegration-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `FormDataIntegrationClient` 개체를 만듭니다.

1. PDF 양식을 참조하십시오.

   * 해당 생성자를 사용하여 `java.io.FileInputStream` 개체를 만듭니다. PDF 양식의 위치를 지정하는 문자열 값을 전달합니다.
   * `com.adobe.idp.Document` 생성자를 사용하여 PDF 양식을 저장하는 `com.adobe.idp.Document` 개체를 만듭니다. PDF 폼이 포함된 `java.io.FileInputStream` 개체를 생성자에 전달합니다.

1. XML 데이터 소스를 참조합니다.

   * 해당 생성자를 사용하여 `java.io.FileInputStream` 개체를 만들고 가져올 데이터가 포함된 XML 파일의 위치를 지정하는 문자열 값을 양식으로 전달합니다.
   * `com.adobe.idp.Document` 생성자를 사용하여 양식 데이터를 저장하는 `com.adobe.idp.Document` 개체를 만듭니다. 양식 데이터가 포함된 `java.io.FileInputStream` 개체를 생성자에 전달합니다.

1. PDF 양식으로 데이터를 가져옵니다.

   `FormDataIntegrationClient` 개체의 `importData` 메서드를 호출하고 다음 값을 전달하여 PDF 양식으로 데이터를 가져옵니다.

   * PDF 양식을 저장하는 `com.adobe.idp.Document` 개체입니다.
   * 양식 데이터를 저장하는 `com.adobe.idp.Document` 개체입니다.

   `importData` 메서드는 XML 데이터 원본의 데이터가 포함된 PDF 양식을 저장하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. PDF 양식을 PDF 파일로 저장합니다.

   * `java.io.File` 개체를 만들고 파일 확장명이 &quot;.PDF&quot;인지 확인하십시오.
   * `Document` 개체의 `copyToFile` 메서드를 호출하여 `Document` 개체의 내용을 파일에 복사합니다(`importData` 메서드에서 반환된 `Document` 개체를 사용하는지 확인).

**추가 참조**

[단계 요약](importing-exporting-data.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 양식 데이터 가져오기](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 양식 데이터 가져오기 {#import-form-data-using-the-web-service-api}

양식 데이터 통합 API(웹 서비스)를 사용하여 양식 데이터 가져오기:

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `FormDataIntegrationClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `FormDataIntegrationClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 MTOM을 사용하려면 `?blob=mtom`을(를) 지정하십시오.
   * `FormDataIntegrationClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `FormDataIntegrationClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `FormDataIntegrationClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. PDF 양식을 참조하십시오.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 PDF 양식을 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. PDF 양식의 위치와 파일을 열 모드를 지정하는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. XML 데이터 소스를 참조합니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 양식으로 가져온 데이터를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. 가져올 데이터가 포함된 XML 파일의 위치와 파일을 열 모드를 지정하는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. PDF 양식으로 데이터를 가져옵니다.

   `FormDataIntegrationClient` 개체의 `importData` 메서드를 호출하고 다음 값을 전달하여 PDF 양식으로 데이터를 가져옵니다.

   * PDF 양식을 저장하는 `BLOB` 개체입니다.
   * 양식 데이터를 저장하는 `BLOB` 개체입니다.

   `importData` 메서드는 XML 데이터 원본의 데이터가 포함된 PDF 양식을 저장하는 `BLOB` 개체를 반환합니다.

1. PDF 양식을 PDF 파일로 저장합니다.

   * 해당 생성자를 호출하고 PDF 파일의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `importData` 메서드에서 반환된 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 필드 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

**추가 참조**

[단계 요약](importing-exporting-data.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 양식 데이터 내보내기 {#exporting-form-data}

양식 데이터 통합 서비스를 사용하여 대화형 PDF 양식에서 양식 데이터를 내보낼 수 있습니다. 내보내는 데이터의 형식은 양식 유형에 따라 다릅니다. 양식 유형이 Acrobat에서 생성된 Acrobat 양식인 경우 내보낸 데이터는 XFDF입니다. 양식 유형이 Designer에서 생성된 XML 양식인 경우 내보낸 데이터는 XDP입니다.

>[!NOTE]
>
>양식 데이터 통합 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### 단계 요약 {#summary_of_steps-1}

PDF 양식에서 양식 데이터를 내보내려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.
1. PDF 양식을 참조하십시오.
1. PDF 양식에서 데이터를 내보냅니다.
1. 내보낸 데이터를 XML 파일로 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar (AEM Forms이 JBoss에 배포된 경우 필수)

**양식 데이터 통합 서비스 클라이언트 만들기**

프로그래밍 방식으로 PDF formClient API로 데이터를 가져오려면 먼저 데이터 통합 서비스 클라이언트를 만들어야 합니다. 서비스 클라이언트를 만들 때 서비스를 호출하는 데 필요한 연결 설정을 정의합니다. 자세한 내용은 [연결 속성을 설정하는 중](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)입니다.

**PDF 양식 참조**

PDF 양식에서 데이터를 내보내려면 Designer 또는 Acrobat에서 만들어지고 양식 데이터를 포함하는 PDF 양식을 참조해야 합니다. 빈 PDF 양식에서 데이터를 내보내려고 하면 빈 XML 스키마가 만들어집니다.

**PDF 양식에서 데이터 내보내기**

양식 데이터가 포함된 PDF 양식을 참조한 후 양식에서 데이터를 내보낼 수 있습니다. 데이터는 양식을 기반으로 하는 XML 스키마 내에서 내보내집니다.

**양식 데이터를 XML 파일로 저장**

양식 데이터를 내보낸 후 데이터를 XML 파일로 저장할 수 있습니다. XML 파일로 저장되면 XML 뷰어에서 XML 파일을 열어 양식 데이터를 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 양식 데이터 내보내기](importing-exporting-data.md#export-form-data-using-the-java-api)

[웹 서비스 API를 사용하여 양식 데이터 내보내기](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[양식 데이터 통합 서비스 API 빠른 시작](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[양식 데이터 가져오기](importing-exporting-data.md#importing-form-data)

### Java API를 사용하여 양식 데이터 내보내기 {#export-form-data-using-the-java-api}

양식 데이터 통합 API(Java)를 사용하여 양식 데이터 내보내기:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-formdataintegration-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `FormDataIntegrationClient` 개체를 만듭니다.

1. PDF 양식을 참조하십시오.

   * 생성자를 사용하여 `java.io.FileInputStream` 개체를 만들고 내보낼 데이터가 포함된 PDF 폼의 위치를 지정하는 문자열 값을 전달합니다.
   * `com.adobe.idp.Document` 생성자를 사용하여 PDF 양식을 저장하는 `com.adobe.idp.Document` 개체를 만듭니다. PDF 폼이 포함된 `java.io.FileInputStream` 개체를 생성자에 전달합니다.

1. PDF 양식에서 데이터를 내보냅니다.

   `FormDataIntegrationClient` 개체의 `exportData` 메서드를 호출하여 양식 데이터를 내보내고 PDF 양식을 저장하는 `com.adobe.idp.Document` 개체를 전달합니다. 이 메서드는 양식 데이터를 XML 스키마로 저장하는 `com.adobe.idp.Document` 개체를 반환합니다.

1. PDF 양식을 PDF 파일로 저장합니다.

   * `java.io.File` 개체를 만들고 파일 확장명이 XML인지 확인하십시오.
   * `Document` 개체의 `copyToFile` 메서드를 호출하여 `Document` 개체의 내용을 파일에 복사합니다(`exportData` 메서드에서 반환된 `Document` 개체를 사용하는지 확인).

**추가 참조**

[단계 요약](importing-exporting-data.md#summary-of-steps)

[빠른 시작(SOAP 모드): Java API를 사용하여 양식 데이터 내보내기](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 양식 데이터 내보내기 {#export-form-data-using-the-web-service-api}

양식 데이터 통합 API(웹 서비스)를 사용하여 양식 데이터 내보내기:

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   * `localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

1. 양식 데이터 통합 서비스 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `FormDataIntegrationClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `FormDataIntegrationClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 MTOM을 사용하려면 `?blob=mtom`을(를) 지정하십시오.
   * `FormDataIntegrationClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `FormDataIntegrationClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `FormDataIntegrationClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. PDF 양식을 참조하십시오.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 데이터를 내보내는 PDF 양식을 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하여 `System.IO.FileStream` 개체를 만듭니다. PDF 양식의 위치와 파일을 열 모드를 지정하는 문자열 값을 전달합니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. PDF 양식에서 데이터를 내보냅니다.

   `FormDataIntegrationClient` 개체의 `exportData` 메서드를 호출하여 데이터를 PDF 양식으로 가져온 다음 PDF 양식을 저장하는 `BLOB` 개체를 전달하십시오. 이 메서드는 양식 데이터를 XML 스키마로 저장하는 `BLOB` 개체를 반환합니다.

1. PDF 양식을 PDF 파일로 저장합니다.

   * 해당 생성자를 호출하고 XML 파일의 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `exportData` 메서드에서 반환된 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 필드 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 XML 파일에 씁니다.

**추가 참조**

[단계 요약](importing-exporting-data.md#summary-of-steps)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
