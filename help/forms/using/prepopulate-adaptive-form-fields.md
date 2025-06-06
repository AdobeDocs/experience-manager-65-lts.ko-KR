---
title: 적응형 양식 필드 미리 채우기
description: 기존 데이터를 사용하여 적응형 양식의 필드를 미리 채웁니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms,Foundation Components
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 69734a2b-7f9d-4661-a1e9-3bf6e362c272
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2203'
ht-degree: 3%

---

# 적응형 양식 필드 미리 채우기{#prefill-adaptive-form-fields}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ko)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html?lang=ko) |
| AEM 6.5 | 이 문서 |

## 소개 {#introduction}

기존 데이터를 사용하여 적응형 양식의 필드를 미리 채울 수 있습니다. 사용자가 양식을 열면 해당 필드의 값이 미리 채워집니다. 적응형 양식에 데이터를 미리 채우려면 적응형 양식의 미리 채우기 데이터 구조를 준수하는 형식으로 사용자 데이터를 미리 채우기 XML/JSON으로 사용할 수 있도록 합니다.

## 미리 채우기 데이터 구조 {#the-prefill-structure}

적응형 양식에는 바인딩된 필드와 바인딩되지 않은 필드가 혼합되어 있을 수 있습니다. 바인딩된 필드는 콘텐츠 파인더 탭에서 드래그한 필드이며 필드 편집 대화 상자에 비어 있지 않은 `bindRef` 속성 값을 포함합니다. 바인딩되지 않은 필드는 Sidekick의 구성 요소 브라우저에서 직접 드래그되며 빈 `bindRef` 값을 갖습니다.

적응형 양식의 바인딩된 필드와 바인딩되지 않은 필드를 모두 미리 채울 수 있습니다. 미리 채우기 데이터에는 적응형 양식의 바인딩된 필드와 바인딩되지 않은 필드를 모두 미리 채우는 afBoundData 섹션과 afUnBoundData 섹션이 포함됩니다. `afBoundData` 섹션에는 바인딩된 필드 및 패널에 대한 미리 채우기 데이터가 포함되어 있습니다. 이 데이터는 연결된 양식 모델 스키마와 호환되어야 합니다.

* [XFA 양식 템플릿](../../forms/using/prepopulate-adaptive-form-fields.md)을(를) 사용하는 적응형 양식의 경우 XFA 템플릿의 데이터 스키마와 호환되는 미리 채우기 XML을 사용하십시오.
* [XML 스키마](#xml-schema-af)을(를) 사용하는 적응형 양식의 경우 XML 스키마 구조와 호환되는 미리 채우기 XML을 사용하십시오.
* [JSON 스키마](#json-schema-based-adaptive-forms)를 사용하는 적응형 양식의 경우 JSON 스키마와 호환되는 미리 채우기 JSON을 사용하십시오.
* FDM 스키마를 사용하는 적응형 양식의 경우, FDM 스키마와 호환되는 JSON 미리 채우기를 사용하십시오.
* [양식 모델이 없는](#adaptive-form-with-no-form-model)적응형 양식의 경우 바인딩된 데이터가 없습니다. 모든 필드는 바인딩되지 않은 필드이며 바인딩되지 않은 XML을 사용하여 미리 채워집니다.

### 샘플 미리 채우기 XML 구조 {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         . 
         .              
    </data>
  </afUnboundData>
</afData>
```

### 샘플 미리 채우기 JSON 구조 {#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

동일한 bindref를 가진 바인딩된 필드 또는 이름이 같은 바인딩되지 않은 필드의 경우 XML 태그 또는 JSON 개체에 지정된 데이터가 모든 필드에 채워집니다. 예를 들어 양식의 두 필드는 미리 채우기 데이터의 이름 `textbox`에 매핑됩니다. 런타임 중에 첫 번째 텍스트 상자 필드에 &quot;A&quot;가 포함되어 있으면 두 번째 텍스트 상자에 자동으로 &quot;A&quot;가 채워집니다. 이러한 연결을 적응형 양식 필드의 라이브 연결이라고 합니다.

### XFA 양식 템플릿을 사용한 적응형 양식 {#xfa-based-af}

XFA 기반 적응형 양식을 위한 미리 채우기 XML 및 제출된 XML의 구조는 다음과 같습니다.

* **미리 채우기 XML 구조**: XFA 기반 적응형 양식에 대한 미리 채우기 XML은 XFA 양식 서식 파일의 데이터 스키마와 호환되어야 합니다. 바인딩되지 않은 필드를 미리 채우려면 미리 채우기 XML 구조를 `/afData/afBoundData` 태그로 래핑합니다.

* **제출된 XML 구조**: 미리 채우기 XML을 사용하지 않으면 제출된 XML에 `afData` 래퍼 태그의 바인딩된 필드와 바인딩되지 않은 필드 모두에 대한 데이터가 포함됩니다. 미리 채우기 XML을 사용하는 경우 제출된 XML의 구조는 미리 채우기 XML과 동일합니다. 미리 채우기 XML이 `afData` 루트 태그로 시작하는 경우 출력 XML의 형식도 동일합니다. 미리 채우기 XML에 `afData/afBoundData`래퍼가 없고 대신 `employeeData`과(와) 같은 스키마 루트 태그에서 직접 시작하는 경우 제출된 XML도 `employeeData` 태그로 시작합니다.

Prefill-Submit-Data-ContentPackage.zip

[파일 가져오기](assets/prefill-submit-data-contentpackage.zip)
미리 채우기 데이터 및 제출된 데이터가 포함된 샘플

### XML 스키마 기반 적응형 양식  {#xml-schema-af}

XML 스키마를 기반으로 하는 적응형 양식에 대해 사전 작성된 XML 및 제출된 XML의 구조는 다음과 같습니다.

* **미리 채우기 XML 구조**: 미리 채우기 XML은 연결된 XML 스키마를 준수해야 합니다. 바인딩되지 않은 필드를 미리 채우려면 미리 채우기 XML 구조를 /afData/afBoundData 태그로 래핑합니다.
* **제출된 XML 구조**: 미리 채우기 XML을 사용하지 않으면 제출된 XML에 `afData` 래퍼 태그의 바인딩된 필드와 바인딩되지 않은 필드 모두에 대한 데이터가 포함됩니다. 미리 채우기 XML을 사용하는 경우 제출된 XML의 구조는 미리 채우기 XML과 동일합니다. 미리 채우기 XML이 `afData` 루트 태그로 시작하는 경우 출력 XML의 형식은 동일합니다. 미리 채우기 XML에 `afData/afBoundData` 래퍼가 없고 대신 `employeeData`과(와) 같은 스키마 루트 태그에서 직접 시작하는 경우 제출된 XML도 `employeeData` 태그로 시작합니다.

```xml
<?xml version="1.0" encoding="utf-8" ?> 
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">
 
    <xs:element name="sample" type="SampleType"/>
         
    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

모델이 XML 스키마인 필드의 경우 아래 샘플 XML과 같이 데이터가 `afBoundData` 태그에 미리 채워집니다. 하나 이상의 바인딩되지 않은 텍스트 필드로 적응형 양식을 미리 채우는 데 사용할 수 있습니다.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>바인딩된 패널(Sidekick 또는 데이터 소스 탭에서 구성 요소를 끌어 만든 비어 있지 않은 `bindRef`이(가) 있는 패널)에서 바인딩되지 않은 필드를 사용하지 않는 것이 좋습니다. 이로 인해 바인딩되지 않은 필드의 데이터가 손실될 수 있습니다. 또한 필드 이름은 양식 전체에서 고유하며 특히 바인딩되지 않은 필드에 대해 고유한 것이 좋습니다.

#### afData 및 afBoundData 래퍼가 없는 예 {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### JSON 스키마 기반 적응형 양식 {#json-schema-based-adaptive-forms}

JSON 스키마 기반의 적응형 양식의 경우 사전 채우기 JSON 및 제출된 JSON의 구조가 아래에 설명되어 있습니다. 자세한 내용은 [JSON 스키마를 사용하여 적응형 양식 만들기](../../forms/using/adaptive-form-json-schema-form-model.md)를 참조하십시오.

* **미리 채우기 JSON 구조**: 미리 채우기 JSON은 연결된 JSON 스키마와 호환되어야 합니다. 선택적으로 언바운드 필드도 미리 채우려면 /afData/afBoundData 개체에 래핑할 수 있습니다.
* **제출된 JSON 구조**: 미리 작성된 JSON을 사용하지 않는 경우 제출된 JSON에는 afData 래퍼 태그의 바인딩된 필드와 바인딩되지 않은 필드 모두에 대한 데이터가 포함됩니다. 미리 채우기 JSON을 사용하는 경우 제출된 JSON의 구조가 미리 채우기 JSON과 동일합니다. 미리 채우기 JSON이 afData 루트 개체로 시작하는 경우 출력 JSON의 형식은 동일합니다. 미리 채우기 JSON에 afData/afBoundData 래퍼가 없고 대신 사용자와 같은 스키마 루트 오브젝트에서 직접 시작하는 경우, 제출된 JSON도 사용자 오브젝트로 시작됩니다.

```json
{
    "id": "https://some.site.somewhere/entry-schema#",
    "$schema": "https://json-schema.org/draft-04/schema#",
    "type": "object",
    "properties": {
        "address": {
            "type": "object",
            "properties": { 
    "name": {
     "type": "string"
    },
    "age": {
     "type": "integer"
}}}}}
```

JSON 스키마 모델을 사용하는 필드의 경우, 데이터는 아래 샘플 JSON에 표시된 대로 afBoundData 개체에 미리 채워집니다. 하나 이상의 바인딩되지 않은 텍스트 필드로 적응형 양식을 미리 채우는 데 사용할 수 있습니다. 다음은 `afData/afBoundData` 래퍼가 포함된 데이터의 예입니다.

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

다음은 `afData/afBoundData` 래퍼가 없는 예입니다.

```json
{
 "user": {
  "address": {
   "city": "Noida",
   "country": "India"
}}}
```

>[!NOTE]
>
>바인딩된 패널(Sidekick 또는 데이터 소스 탭에서 구성 요소를 끌어 만든 비어 있지 않은 bindRef가 있는 패널)에서 바인딩되지 않은 필드를 사용하는 것은 바인딩되지 않은 필드의 데이터가 손실될 수 있으므로 **not**&#x200B;입니다. 특히 바인딩되지 않은 필드의 경우 양식에서 고유한 필드 이름을 사용하는 것이 좋습니다.

### 양식 모델이 없는 적응형 양식 {#adaptive-form-with-no-form-model}

양식 모델이 없는 적응형 양식의 경우 모든 필드의 데이터는 `<afUnboundData> tag`의 `<data>` 태그 아래에 있습니다.

또한 다음 사항에 유의하십시오.

다양한 필드에 대해 제출된 사용자 데이터의 XML 태그는 필드의 이름을 사용하여 생성됩니다. 따라서 필드 이름은 고유해야 합니다.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## 구성 관리자를 사용하여 미리 채우기 서비스 구성 {#configuring-prefill-service-using-configuration-manager}

미리 채우기 서비스를 활성화하려면 AEM 웹 콘솔 구성에서 기본 미리 채우기 서비스 구성을 지정합니다. 다음 단계를 사용하여 미리 채우기 서비스를 구성합니다.

>[!NOTE]
>
>미리 채우기 서비스 구성은 적응형 양식, HTML 5 양식 및 HTML 5 양식 세트에 적용할 수 있습니다.

1. 다음 URL을 사용하여 **[!UICONTROL Adobe Experience Manager 웹 콘솔 구성]**&#x200B;을 엽니다.\
   https://&lt;server>:&lt;port>/system/console/configMgr
1. **[!UICONTROL 기본 미리 채우기 서비스 구성]**&#x200B;을 검색하여 엽니다.

   ![미리 채우기 구성](assets/prefill_config_new.png)

1. **데이터 파일 위치**&#x200B;에 대한 데이터 위치 또는 정규 표현식(정규 표현식)을 입력하십시오. 유효한 데이터 파일 위치의 예는 다음과 같습니다.

   * file:///C:/Users/public/Document/Prefill/.&#42;
   * https://localhost:8000/somesamplexmlfile.xml

   >[!NOTE]
   >
   >기본적으로 모든 유형의 적응형 Forms(XSD, XDP, JSON, FDM 및 양식 모델 기반 없음)에 대해 crx 파일을 통해 미리 채우기가 허용됩니다. 미리 채우기는 JSON 및 XML 파일에서만 허용됩니다.

1. 이제 양식에 대해 미리 채우기 서비스가 구성되었습니다.

   >[!NOTE]
   >
   >crx 프로토콜은 미리 채워진 데이터 보안을 처리하므로 기본적으로 허용됩니다. 일반 정규 표현식을 사용하는 다른 프로토콜을 통해 미리 채우면 취약성이 발생할 수 있습니다. 구성에서 데이터를 보호하기 위한 보안 URL 구성을 지정합니다.

## 반복 가능한 패널의 이상한 사례 {#the-curious-case-of-repeatable-panels}

일반적으로 바인딩된(양식 스키마) 필드와 바인딩되지 않은 필드는 동일한 적응형 양식으로 작성되지만, 바인딩이 반복될 수 있는 경우 다음과 같은 몇 가지 예외가 있습니다.

* XFA 양식 템플릿, XSD, JSON 스키마 또는 FDM 스키마를 사용하는 적응형 양식에 대해서는 바인딩되지 않은 반복 가능한 패널이 지원되지 않습니다.
* 바인딩된 반복 가능한 패널에 바인딩되지 않은 필드를 사용하지 마십시오.

>[!NOTE]
>
>일반적으로 바인딩된 필드와 바인딩되지 않은 필드가 바인딩되지 않은 필드에서 최종 사용자가 채운 데이터에 교차되는 경우 혼합하지 마십시오. 가능한 경우 스키마나 XFA 양식 템플릿을 수정하고 바인딩되지 않은 필드에 대한 항목을 추가하여 바인딩된 데이터가 제출된 데이터의 다른 필드와 같이 사용할 수 있도록 해야 합니다.

## 사용자 데이터 미리 채우기에 대해 지원되는 프로토콜 {#supported-protocols-for-prefilling-user-data}

적응형 양식은 유효한 정규 표현식으로 구성된 경우 다음 프로토콜을 통해 미리 채우기 데이터 형식의 사용자 데이터로 미리 채울 수 있습니다.

### crx:// 프로토콜 {#the-crx-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

지정한 노드에 이름이 `jcr:data`인 속성이 있어야 하며 데이터를 보관해야 합니다.

### file:// 프로토콜  {#the-file-protocol-nbsp}

```http
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

참조된 파일은 동일한 서버에 있어야 합니다.

### https:// 프로토콜 {#the-http-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### service:// 프로토콜 {#the-service-protocol}

```http
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME은 OSGI 미리 채우기 서비스의 이름을 나타냅니다. [미리 채우기 서비스 만들기 및 실행](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service)을 참조하세요.
* IDENTIFIER는 미리 채우기 데이터를 가져오기 위해 OSGI 미리 채우기 서비스에 필요한 메타데이터를 나타냅니다. 로그인한 사용자에 대한 식별자는 사용할 수 있는 메타데이터의 예입니다.

>[!NOTE]
>
>인증 매개 변수 전달은 지원되지 않습니다.

### slingRequest에서 데이터 속성 설정 {#setting-data-attribute-in-slingrequest}

`slingRequest`에서 `data` 특성을 설정할 수도 있습니다. 여기서 `data` 특성은 아래 샘플 코드(예: XML용)에 표시된 대로 XML 또는 JSON이 포함된 문자열입니다.

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

모든 데이터가 포함된 간단한 XML 또는 JSON 문자열을 작성하여 slingRequest에서 설정할 수 있습니다. 이 작업은 slingRequest 데이터 속성을 설정할 수 있는 페이지에 포함하려는 모든 구성 요소에 대해 렌더러 JSP에서 쉽게 수행할 수 있습니다.

예를 들어 특정 유형의 헤더가 있는 페이지에 특정 디자인을 사용하려는 경우. 이를 위해 페이지 구성 요소에 포함하고 `data` 특성을 설정할 수 있는 자신의 `header.jsp`을(를) 작성할 수 있습니다.

또 다른 좋은 예는 Facebook, Twitter 또는 LinkedIn과 같은 소셜 계정을 통해 로그인할 때 데이터를 미리 채우는 사용 사례입니다. 이 경우 사용자 계정에서 데이터를 가져오고 데이터 매개 변수를 설정하는 간단한 JSP를 `header.jsp`에 포함할 수 있습니다.

prefill-page component.zip

[파일 가져오기](assets/prefill-page-component.zip)
페이지 구성 요소의 샘플 prefill.jsp

## AEM Forms 사용자 지정 미리 채우기 서비스 {#aem-forms-custom-prefill-service}

사전 정의된 소스에서 데이터를 지속적으로 읽는 시나리오에 대해 사용자 지정 미리 채우기 서비스를 사용할 수 있습니다. 미리 채우기 서비스는 정의된 데이터 소스에서 데이터를 읽고 적응형 양식의 필드를 미리 채우기 데이터 파일의 콘텐츠로 채웁니다. 또한 미리 채워진 데이터를 적응형 양식과 영구적으로 연결할 수 있습니다.

### 미리 채우기 서비스 만들기 및 실행 {#create-and-run-a-prefill-service}

프리필 서비스는 OSGi 서비스이며 OSGi 번들을 통해 패키징된다. OSGi 번들을 만들고 업로드한 다음 AEM Forms 번들에 설치합니다. 번들 만들기를 시작하기 전에 다음을 수행하십시오.

* [AEM Forms 클라이언트 SDK 다운로드](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html)
* 보일러 플레이트 패키지 다운로드

* crx-repository에 데이터(데이터 미리 채우기) 파일을 넣습니다. crx-repository의 \contents 폴더에 있는 임의의 위치에 파일을 배치할 수 있습니다.

[파일 가져오기](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### 미리 채우기 서비스 만들기 {#create-a-prefill-service}

보일러플레이트 패키지(샘플 미리 채우기 서비스 패키지)에는 AEM Forms 미리 채우기 서비스의 샘플 구현이 포함되어 있습니다. 코드 편집기에서 상용구 패키지를 엽니다. 예를 들어 편집할 Eclipse에서 보일러판 프로젝트를 엽니다. 코드 편집기에서 상용구 패키지를 연 후 다음 단계를 수행하여 서비스를 만듭니다.

1. 편집할 src\main\java\com\adobe\test\Prefill.java 파일을 엽니다.
1. 코드에서 다음 값을 설정합니다.

   * `nodePath:` crx-repository 위치를 가리키는 노드 경로 변수에 데이터(미리 채우기) 파일의 경로가 있습니다. 예: /content/prefilldata.xml
   * `label:` label 매개 변수는 서비스의 표시 이름을 지정합니다. 예: 기본 미리 채우기 서비스

1. `Prefill.java` 파일을 저장하고 닫습니다.
1. `AEM Forms Client SDK` 패키지를 상용구 프로젝트의 빌드 경로에 추가합니다.
1. 프로젝트를 컴파일하고 번들에 대한 .jar를 만듭니다.

#### 미리 채우기 서비스 시작 및 사용 {#start-and-use-the-prefill-service}

미리 채우기 서비스를 시작하려면 JAR 파일을 AEM Forms 웹 콘솔에 업로드하고 서비스를 활성화합니다. 이제 서비스가 적응형 양식 편집기에 표시되기 시작합니다. 미리 채우기 서비스를 적응형 양식에 연결하려면 다음 작업을 수행하십시오.

1. Forms 편집기에서 적응형 양식을 열고 양식 컨테이너에 대한 속성 패널을 엽니다.
1. 속성 콘솔에서 AEM Forms 컨테이너 > 기본 > 미리 채우기 서비스로 이동합니다.
1. 기본 미리 채우기 서비스를 선택하고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다. 서비스는 양식에 연결됩니다.

## 클라이언트에서 데이터 미리 채우기 {#prefill-at-client}

적응형 양식을 미리 채우면 AEM Forms 서버가 데이터를 적응형 양식과 병합하고 채워진 양식을 사용자에게 전달합니다. 기본적으로 데이터 병합 작업은 서버에서 수행됩니다.

서버 대신 클라이언트에서 데이터 병합 작업을 수행하도록 AEM Forms 서버를 구성할 수 있습니다. 적응형 양식을 미리 채우고 렌더링하는 데 필요한 시간을 크게 줄입니다. 기본적으로 이 기능은 비활성화되어 있습니다. 구성 관리자 또는 명령줄에서 활성화할 수 있습니다.

* 구성 관리자에서 활성화 또는 비활성화하려면 다음을 수행합니다.
   1. AEM 구성 관리자를 엽니다.
   1. 적응형 양식 및 대화형 통신 웹 채널 구성 찾기 및 열기
   1. Configuration.af.clientside.datamerge.enabled.name 옵션을 활성화합니다
* 명령줄에서 을 활성화하거나 비활성화하려면 다음을 수행합니다.
   * 활성화하려면 다음 cURL 명령을 실행합니다.

     `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   * 비활성화하려면 다음 cURL 명령을 실행합니다.

     `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

  클라이언트에서 데이터 미리 채우기 옵션을 최대한 활용하려면 미리 채우기 서비스를 업데이트하여 [FileAttachmentMap](https://helpx.adobe.com/kr/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) 및 [CustomContext](https://helpx.adobe.com/kr/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)을(를) 반환합니다
