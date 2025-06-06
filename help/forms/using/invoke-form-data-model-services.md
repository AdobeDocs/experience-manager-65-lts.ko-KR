---
title: 적응형 양식에서 양식 데이터 모델 서비스를 호출하기 위한 API
description: 적응형 양식 필드 내에서 WSDL로 작성된 웹 서비스를 호출하는 데 사용할 수 있는 invokeWebServices API에 대해 설명합니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: e36be2da-af72-485f-87a6-cef6172037c6
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 10%

---

# 적응형 양식에서 양식 데이터 모델 서비스를 호출하기 위한 API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ko)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

## 개요 {#overview}

AEM Forms을 사용하면 양식 작성자가 적응형 양식 필드 내에서 양식 데이터 모델에 구성된 서비스를 호출하여 양식 채우기 경험을 보다 단순화하고 향상시킬 수 있습니다. 데이터 모델 서비스를 호출하려면 시각적 편집기에서 규칙을 만들거나 [규칙 편집기](/help/forms/using/rule-editor.md)의 코드 편집기에서 `guidelib.dataIntegrationUtils.executeOperation` API를 사용하여 JavaScript을 지정할 수 있습니다.

이 문서는 `guidelib.dataIntegrationUtils.executeOperation` API를 사용하여 서비스를 호출하는 JavaScript 작성에 중점을 둡니다.

## API 사용 {#using-the-api}

`guidelib.dataIntegrationUtils.executeOperation` API는 적응형 양식 필드 내에서 서비스를 호출합니다. API 구문은 다음과 같습니다.

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

`guidelib.dataIntegrationUtils.executeOperation` API 구조에서 서비스 작업에 대한 세부 정보를 지정합니다. 구조의 구문은 다음과 같습니다.

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

API 구조는 서비스 작업에 대해 다음 세부 사항을 지정합니다.

<table>
 <tbody>
  <tr>
   <th>매개변수</th>
   <th>설명</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>양식 데이터 모델 식별자, 작업 제목 및 작업 이름을 지정하는 구조</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>양식 데이터 모델의 이름을 포함하는 저장소 경로를 지정합니다.</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>실행할 서비스 작업의 이름을 지정합니다.</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>하나 이상의 양식 개체를 서비스 작업의 입력 인수에 매핑합니다.</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>하나 이상의 양식 개체를 서비스 작업의 출력 값에 매핑하여 양식 필드 <br />을(를) 채웁니다. </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>서비스 작업의 입력 인수를 기준으로 값을 반환합니다. 콜백 함수로 사용되는 선택적 매개 변수입니다.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>성공 콜백 함수가 입력 인수를 기반으로 출력 값을 표시하지 못하는 경우 오류 메시지를 표시합니다. 콜백 함수로 사용되는 선택적 매개 변수입니다.<br /> </td>
  </tr>
 </tbody>
</table>

## 서비스를 호출하는 샘플 스크립트 {#sample-script-to-invoke-a-service}

다음 샘플 스크립트는 `guidelib.dataIntegrationUtils.executeOperation` API를 사용하여 `employeeAccount` 양식 데이터 모델에 구성된 `getAccountById` 서비스 작업을 호출합니다.

`getAccountById` 작업은 `employeeID` 양식 필드의 값을 `empId` 인수에 대한 입력으로 취하여 해당 직원의 직원 이름, 계정 번호 및 계정 잔액을 반환합니다. 출력 값은 지정된 양식 필드에 채워집니다. 예를 들어 `name` 인수의 값은 `fullName` 양식 요소에서 채워지고 `account` 양식 요소에서 `accountNumber` 인수의 값이 채워집니다.

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## 콜백 함수와 함께 API 사용 {#using-the-api-callback}

콜백 함수와 함께 `guidelib.dataIntegrationUtils.executeOperation` API를 사용하여 양식 데이터 모델 서비스를 호출할 수도 있습니다. API 구문은 다음과 같습니다.

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

콜백 함수에는 `success` 및 `failure` 콜백 함수가 있을 수 있습니다.

### 성공 및 실패 콜백 함수가 있는 샘플 스크립트 {#callback-function-success-failure}

다음 샘플 스크립트는 `guidelib.dataIntegrationUtils.executeOperation` API를 사용하여 `employeeOrder` 양식 데이터 모델에 구성된 `GETOrder` 서비스 작업을 호출합니다.

`GETOrder` 작업은 `Order ID` 양식 필드의 값을 `orderId` 인수에 대한 입력으로 사용하고 `success` 콜백 함수에서 주문 수량 값을 반환합니다.  `success` 콜백 함수가 주문 수량을 반환하지 않으면 `failure` 콜백 함수에서 `Error occured` 메시지를 표시합니다.

>[!NOTE]
>
>`success` 콜백 함수를 사용하는 경우 출력 값이 지정된 양식 필드에 채워지지 않습니다.

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
