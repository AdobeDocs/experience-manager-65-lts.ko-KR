---
title: Forms 렌더링
description: Forms 서비스를 사용하여 일반적으로 Designer에서 만든 양식을 확인, 처리, 변환 및 제공하는 대화형 데이터 캡처 클라이언트 애플리케이션을 만듭니다. 양식 작성자는 다양한 브라우저 환경에서 Forms 서비스가 PDF, SWF 또는 HTML에서 렌더링하는 단일 양식 디자인을 개발할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 3f1f9ecb-be62-4428-8db8-23c57081b0f7
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Forms 렌더링 {#rendering-forms}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

**Forms 서비스 정보**

Forms 서비스를 사용하면 일반적으로 Designer에서 만든 양식을 확인, 처리, 변환 및 제공하는 대화형 데이터 캡처 클라이언트 애플리케이션을 만들 수 있습니다. 양식 작성자는 다양한 브라우저 환경에서 Forms 서비스가 PDF, SWF 또는 HTML에서 렌더링하는 단일 양식 디자인을 개발할 수 있습니다.

최종 사용자가 양식을 요청하면 클라이언트 애플리케이션이 Forms 서비스로 요청을 보내고, 이 서비스에서 적절한 형식으로 양식을 반환합니다. Forms 서비스는 요청을 받는 즉시 데이터를 양식 디자인과 병합한 다음 원하는 형식으로 양식을 전달합니다. 양식 서비스 출력은 대화형 양식(일반적으로 PDF 문서)입니다. 대화형 양식을 사용하면 사용자가 양식에 있는 필드를 채울 수 있습니다.

클라이언트 애플리케이션 유형에 따라 클라이언트 웹 브라우저에 양식을 작성하거나 양식을 PDF 파일로 저장할 수 있습니다. 웹 기반 응용 프로그램은 웹 브라우저에 양식을 작성할 수 있습니다. 데스크탑 애플리케이션은 양식을 PDF 파일로 저장할 수 있습니다. 웹 브라우저 및 PDF 파일에 쓰는 방법을 보여 주기 위해 *Forms 렌더링* 섹션의 빠른 시작은 다음과 같은 방법으로 구성됩니다.

* 강력한 형식의 Java API(SOAP 모드) 예는 Java 서블릿입니다.
* 웹 서비스(Java Base64) 예는 Java 서블릿입니다.
* 웹 서비스(MTOM) 예는 콘솔 애플리케이션입니다(일부 빠른 시작에 MTOM 예제가 있는 것은 아님).

>[!NOTE]
>
>Java 서블릿을 사용하여 Forms 서비스를 호출하는 웹 응용 프로그램을 만드는 방법에 대한 자세한 내용은 [Forms을 렌더링하는 웹 응용 프로그램 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)를 참조하십시오.

다음 두 가지 방법 중 하나를 사용하여 양식 디자인(XDP 파일) 또는 PDF 문서를 Forms 서비스에 전달할 수 있습니다.

* URL 값을 사용하여 양식 디자인을 참조할 수 있습니다. 이 방법에는 `URLSpec` 개체가 포함됩니다. `URLSpec` 개체의 `setContentRootURI` 메서드를 사용하여 콘텐츠 루트가 Forms 서비스에 전달됩니다. 양식 디자인 이름(`formQuery`)이 별도의 매개 변수로 전달됩니다. 두 값을 연결하여 양식 디자인에 대한 절대 참조를 가져옵니다. *Forms 렌더링* 섹션의 빠른 시작은 대부분 이 방법을 사용합니다.
* 양식 디자인이 포함된 `com.adobe.idp.Document`을(를) Forms 서비스에 전달할 수 있습니다. `renderPDFForm2` 및 `renderHTMLForm2`(이)라는 두 개의 새 메서드가 양식 디자인을 포함하는 `com.adobe.idp.Document` 개체를 수락합니다. ([Forms 서비스에 문서 전달](/help/forms/developing/passing-documents-forms-service.md) 참조)

Forms 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* 대화형 PDF forms 렌더링. ([대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)을 참조하십시오.)
* 클라이언트에서 양식을 렌더링합니다. [클라이언트에서 Forms 렌더링](/help/forms/developing/rendering-forms-client.md)을 참조하십시오.
* 조각을 기반으로 양식 렌더링 [조각을 기반으로 Forms 렌더링](/help/forms/developing/rendering-forms-based-fragments.md)을 참조하십시오.
* 렌더링 권한이 활성화된 양식입니다. [권한이 활성화된 Forms 렌더링](/help/forms/developing/rendering-rights-enabled-forms.md)을 참조하십시오.
* 양식을 HTML으로 렌더링합니다. ([Forms을 HTML으로 렌더링](/help/forms/developing/rendering-forms-html.md)을 참조하십시오.)
* 사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링([사용자 지정 CSS 파일을 사용하여 HTML Forms 렌더링](/help/forms/developing/rendering-html-forms-using-custom.md))
* 제출된 양식을 처리합니다. ([제출된 Forms 처리](/help/forms/developing/handling-submitted-forms.md)를 참조하십시오.)
* 제출된 XML 데이터를 사용하여 PDF 문서 생성. [제출된 XML 데이터를 사용하여 PDF 문서 만들기](/help/forms/developing/creating-pdf-documents-submitted-xml.md)를 참조하십시오.
* 양식을 미리 채웁니다. [유동성 레이아웃으로 Forms 미리 채우기](/help/forms/developing/prepopulating-forms-flowable-layouts.md)를 참조하십시오.
* 문서 전달. ([Forms 서비스에 문서 전달](/help/forms/developing/passing-documents-forms-service.md) 참조)
* 양식 데이터를 계산합니다. ([양식 데이터 계산](/help/forms/developing/calculating-form-data.md)을 참조하십시오.)
* 응용 프로그램을 최적화합니다. ([Forms 서비스 성능 최적화](/help/forms/developing/optimizing-performance-forms-service.md)를 참조하십시오.)
