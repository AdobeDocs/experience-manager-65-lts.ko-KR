---
title: '자습서: 적응형 양식 만들기'
description: 적응형 양식을 만들고, 레이아웃하고, 미리 보는 방법에 대해 알아봅니다. 또한 제출 액션을 구성하는 방법도 알아보십시오.
feature: Adaptive Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 87e03ff2-1324-42bd-b4da-54a0c17ce98e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 9%

---

# 자습서: 적응형 양식 만들기 {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

이 자습서는 [첫 번째 적응형 양식을 만들기](/help/forms/using/create-your-first-adaptive-form.md) 시리즈의 단계입니다. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하려면 연대순으로 시리즈를 따르는 것이 좋습니다.

## 튜토리얼 기본 정보 {#about-the-tutorial}

적응형 양식은 동적이고 반응형 차세대 양식입니다. 적응형 양식을 사용하여 개인화된 경험을 전달할 수 있습니다. 사용량 통계를 위해 [!DNL Adobe Analytics] 및 캠페인 관리를 위해 [!DNL Adobe Campaign]과(와) 적응형 양식을 통합할 수도 있습니다. 적응형 양식 기능에 대한 자세한 내용은 [적응형 양식 작성 소개](/help/forms/using/introduction-forms-authoring.md)를 참조하십시오.

적절한 프로세스를 따라야 양식을 더 쉽게 만들고 관리할 수 있습니다. 이 문서에서는 다음 방법을 알아봅니다.

* [고객이 배송 주소를 추가할 수 있도록 하는 적응형 양식을 만듭니다](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [고객의 정보를 표시하고 수락할 적응형 양식의 레이아웃 필드](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [제출 액션을 만들어 양식 콘텐츠가 포함된 이메일을 보냅니다.](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [적응형 양식 미리 보기 및 제출](/help/forms/using/create-adaptive-form.md)

문서의 끝 부분에 다음과 유사한 양식이 표시됩니다.\
[![모바일에서 양식 미리 보기](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## 1단계: 적응형 양식 만들기 {#step-create-the-adaptive-form}

1. AEM 작성자 인스턴스에 로그인하고 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;로 이동합니다. 기본 URL은 [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)입니다.
1. **[!UICONTROL 만들기]**&#x200B;를 선택하고 **[!UICONTROL 적응형 양식]**&#x200B;을 선택하세요. 템플릿을 선택하는 옵션이 나타납니다. **[!UICONTROL Blank]** 템플릿을 선택하여 선택하고 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

1. **[!UICONTROL 속성 추가]** 옵션이 나타납니다. **[!UICONTROL 제목]** 및 **[!UICONTROL 이름]** 필드는 필수입니다.

   * **제목:** **[!UICONTROL 제목]** 필드에 `Add new or update shipping address`을(를) 지정합니다. 제목 필드는 양식의 표시 이름을 지정합니다. 제목을 통해 AEM [!DNL Forms] 사용자 인터페이스에서 양식을 식별할 수 있습니다.
   * **이름:** **[!UICONTROL 이름]** 필드에 `shipping-address-add-update-form`을(를) 지정합니다. 이름 필드는 양식 이름을 지정합니다. 이름이 지정된 노드가 저장소에서 만들어집니다. 제목 입력이 시작되면 이름 필드 값이 자동으로 생성됩니다. 제안 값을 변경할 수 있습니다. 이름 필드에는 영숫자 문자, 하이픈 및 밑줄만 포함될 수 있습니다. 잘못된 모든 입력은 하이픈으로 대체됩니다.

1. **[!UICONTROL 만들기]**&#x200B;를 선택합니다. 적응형 양식이 만들어지고 편집할 양식을 여는 대화 상자가 나타납니다. **[!UICONTROL 열기]**&#x200B;를 선택하여 새로 만든 양식을 새 탭에서 엽니다. 편집할 양식이 열립니다. 또한 요구 사항에 따라 새로 만든 양식을 사용자 정의할 수 있는 사이드바가 표시됩니다.

   적응형 양식 작성 인터페이스 및 사용 가능한 구성 요소에 대한 자세한 내용은 [적응형 양식 작성 소개](/help/forms/using/creating-adaptive-form.md)를 참조하십시오.

   ![새로 만든 적응형 양식입니다.](assets/newly-created-adaptive-form.png)

## 2단계: 머리글 및 바닥글 추가 {#step-add-header-and-footer}

AEM [!DNL Forms]은(는) 적응형 양식에 대한 정보를 표시하는 다양한 구성 요소를 제공합니다. 머리글 및 바닥글 구성 요소를 사용하면 폼에 일관된 모양과 느낌을 제공할 수 있습니다. 머리글에는 일반적으로 법인의 로고, 양식의 제목 및 요약이 포함됩니다. 바닥글에는 일반적으로 저작권 정보와 다른 페이지에 대한 링크가 포함되어 있습니다.

1. ![사이드 패널 전환](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png)을 선택합니다. 구성 요소 브라우저가 열립니다. 구성 요소 브라우저의 **[!UICONTROL Header]** 구성 요소를 적응형 양식으로 끌어 옵니다.
1. **[!UICONTROL 로고]**&#x200B;를 선택하십시오. 도구 모음이 나타납니다. 도구 모음에서 ![aem_6_3_edit](assets/aem_6_3_edit.png)을(를) 선택하고 **We.Retail**&#x200B;을(를) 입력한 다음 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)을(를) 선택합니다.

1. 이미지를 선택합니다. 도구 모음이 나타납니다. ![cmpr](assets/cmppr.png)을(를) 선택합니다. 화면 왼쪽에 속성 브라우저가 열립니다. **[!UICONTROL 찾아보기]**&#x200B;하고 로고 이미지를 업로드하십시오. ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 선택합니다. 이미지가 헤더에 나타납니다.

   파일 가져오기를 선택하여 이 문서에 사용된 로고가 없는 경우 해당 로고를 다운로드할 수 있습니다.

[파일 가져오기](assets/logo.png)

1. ![treeexpandall](assets/treeexpandall.png)에서 **[!UICONTROL 바닥글]** 구성 요소를 적응형 양식으로 드래그하십시오. 이 단계에서 양식은 다음과 같습니다.

   ![머리글 및 바닥글이 있는 적응형 양식](assets/adaptive-form-with-headers-and-footers.png)

## 3단계: 정보를 캡처하고 표시할 구성 요소 추가 {#step-add-components-to-capture-and-display-information}

구성 요소는 적응형 양식의 기본 구성단위입니다. AEM [!DNL Forms]은(는) 적응형 양식에서 정보를 캡처하고 표시할 수 있는 많은 구성 요소를 제공합니다. ![treeexpandall](assets/treeexpandall.png)의 구성 요소를 양식으로 드래그할 수 있습니다. 사용 가능한 구성 요소 및 해당 기능에 대해 알아보려면 [적응형 양식 작성 소개](/help/forms/using/introduction-forms-authoring.md)를 참조하세요.

1. **[!UICONTROL Numeric Box 구성 요소]**&#x200B;를 적응형 양식으로 끌어 놓으십시오. 바닥글 구성 요소 앞에 놓습니다. 구성 요소의 속성을 열고 구성 요소의 **[!UICONTROL Title]**&#x200B;을(를) **`Customer ID`**(으)로 변경하고, **[!UICONTROL 요소 이름]**&#x200B;을(를) **`customer_ID`**(으)로 변경하고, **[!UICONTROL 필수 필드]** 옵션을 활성화하고, **[!UICONTROL HTML5 숫자 입력 유형 사용]** 옵션을 활성화하고, ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)을(를) 선택합니다.
1. 세 개의 텍스트 상자 구성 요소를 적응형 양식으로 드래그합니다. 바닥글 구성 요소 앞에 배치합니다. 이러한 텍스트 상자에 대해 다음 속성을 설정합니다.:

   <table> 
    <tbody> 
     <tr> 
      <td><b>속성</b></td> 
      <td><b>텍스트 상자 1<br/></b></td> 
      <td><b>텍스트 상자 2<br/></b></td> 
      <td><b>텍스트 상자 3</b></td> 
     </tr> 
     <tr> 
      <td>제목</td> 
      <td>이름<br /> </td> 
      <td>배송 주소</td> 
      <td>상태</td> 
     </tr> 
     <tr> 
      <td>요소 이름</td> 
      <td>customer_Name<br /> </td> 
      <td>customer_Shipping_Address</td> 
      <td>customer_State</td> 
     </tr> 
     <tr> 
      <td>필수 필드</td> 
      <td>활성화됨</td> 
      <td>활성화됨</td> 
      <td>활성화됨</td> 
     </tr> 
     <tr> 
      <td>여러 줄 허용<br /> </td> 
      <td>비활성화됨</td> 
      <td>활성화됨</td> 
      <td>비활성화됨</td> 
     </tr> 
    </tbody> 
   </table>

1. **[!UICONTROL 숫자 상자]** 구성 요소를 바닥글 구성 요소 앞으로 끌어 옵니다. 구성 요소의 속성을 열고 아래 표에 나열된 값을 설정한 다음 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 선택합니다.

   | 속성 | 값 |
   |---|---|
   | 제목 | 우편 번호 |
   | 요소 이름 | customer_ZIPCode |
   | 최대 자릿수 | 6 |
   | 필수 필드 | 활성화됨 |
   | 패턴 유형 표시 | 패턴 없음 |

1. **[!UICONTROL 전자 메일]** 구성 요소를 바닥글 구성 요소 앞으로 끌어 놓으십시오. 구성 요소의 속성을 열고 아래 표에 나열된 값을 설정한 다음 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)을(를) 선택합니다.

   | 속성 | 값 |
   |---|---|
   | 제목 | 이메일 |
   | 요소 이름 | customer_Email |
   | 필수 필드 | 활성화됨 |

1. **[!UICONTROL 첨부 파일]** 구성 요소를 바닥글 구성 요소 앞으로 끌어 놓으십시오. 구성 요소의 속성을 열고 아래 표에 나열된 값을 설정한 다음 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)을(를) 선택합니다.

   <table> 
    <tbody> 
     <tr> 
      <td><b>속성</b></td> 
      <td><b>값</b></td> 
     </tr> 
     <tr> 
      <td>제목</td> 
      <td>정부가 주소 증명 <br />을(를) 승인했습니다. </td> 
     </tr> 
     <tr> 
      <td>요소 이름</td> 
      <td>customer_Address_증명</td> 
     </tr> 
     <tr> 
      <td>필수 필드</td> 
      <td>활성화됨</td> 
     </tr> 
    </tbody> 
   </table>

1. **[!UICONTROL 전송 단추]** 구성 요소를 적응형 양식으로 드래그하십시오. 바닥글 구성 요소 앞에 놓습니다. 구성 요소의 속성을 열고 요소 이름을 `address_addition_update_submit`(으)로 변경하고 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 선택합니다. 양식의 레이아웃은 완전하며 양식은 다음과 같습니다.

   ![모든 구성 요소가 포함된 적응형 양식](assets/adaptive-form-with-all-the-components.png)

## 4단계: 적응형 양식에 대한 제출 액션 구성 {#step-configure-submit-action-for-the-adaptive-form}

제출 액션은 사용자가 적응형 양식에서 제출 단추를 탭할 때 트리거됩니다. 제출 액션을 사용하여 양식 데이터를 로컬 리포지토리에 저장하고, 양식 데이터를 REST 엔드포인트로 보내고, 양식 데이터를 이메일로 보내는 등의 작업을 수행할 수 있습니다. 적응형 양식은 몇 가지 기본 제출 액션을 제공합니다. 자세한 내용은 [제출 동작 구성](/help/forms/using/configuring-submit-actions.md)을 참조하세요.

다음 단계를 사용하여 양식의 이메일 제출 액션 및 데모 제출 액션을 구성할 수 있습니다.

1. 이메일 서버를 구성합니다. 자세한 내용은 [전자 메일 알림 구성](/help/sites-administering/notification.md)을 참조하세요.


1. 콘텐츠 브라우저에서 **[!UICONTROL 양식 컨테이너]**&#x200B;를 선택하고 ![cmppr](assets/cmppr.png)을(를) 선택합니다. 속성 브라우저가 왼쪽에서 열립니다.
1. **[!UICONTROL 제출]** > **[!UICONTROL 제출 액션]**(으)로 이동합니다. **[!UICONTROL 전자 메일 보내기]**&#x200B;를 선택합니다. 다음 값을 지정하고 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 선택합니다.

   | 속성 | 값 |
   |--- |--- |
   | 출처 | `donotreply@weretail.com` |
   | 끝 | `${customer_Email}` |
   | 제목 | 승인: We.Retail 웹 사이트에 배송 주소를 추가했습니다. |
   | 전자 메일 템플릿 | 안녕하세요, `${customer_Name}` 님, 다음 주소가 계정의 배송 주소로 추가되었습니다. <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`, `${customer_ZIPCode}`<br> 감사합니다. We.Retail |
   | 첨부 파일 포함 | 활성화됨 |

   양식이 준비되었습니다. 이제 양식을 미리 보고 기능을 테스트할 수 있습니다. 자습서에서 언급된 이름을 사용하고 AEM [!DNL Forms] 서버를 실행하는 컴퓨터에서 양식에 액세스한 경우 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)에서 양식을 사용할 수 있습니다.

## 5단계: 적응형 양식 미리 보기 및 제출 {#step-preview-and-submit-the-adaptive-form}

**[!UICONTROL 미리 보기 옵션]**&#x200B;을 사용하여 폼의 모양과 동작을 평가할 수 있습니다. 미리 보기 모드에서 양식을 제출하고 양식에 적용된 유효성 검사도 확인할 수 있습니다. 예를 들어 필수 필드를 비워 둘 때 오류가 표시되는 경우입니다.

적응형 양식은 또한 다양한 디바이스를 위한 양식 경험을 에뮬레이션하는 옵션을 제공합니다. 예를 들어 iPhone, iPad 및 데스크톱이 있습니다. **[!UICONTROL 미리 보기]** 및 **[!UICONTROL 에뮬레이터]** ![눈금자](assets/ruler.png) 옵션을 함께 사용하여 화면 크기가 다른 장치의 양식을 미리 볼 수 있습니다.

1. 양식 편집기의 오른쪽에 있는 **[!UICONTROL 미리 보기]** 옵션을 선택합니다. 양식이 미리보기 모드에서 열립니다. 자습서에서 언급된 이름을 사용한 경우 양식의 미리 보기 URL은 [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)입니다.
1. ![눈금자](assets/ruler.png)를 사용하여 다양한 장치에서 양식이 어떻게 표시되는지 확인하십시오.
1. 양식의 필드를 작성하고 **[!UICONTROL 제출]**&#x200B;을 선택합니다. 양식이 제출되고 기본 **감사합니다** 페이지로 리디렉션됩니다. 사용자 정의 감사 페이지를 지정할 수도 있습니다. 자세한 내용은 [리디렉션 페이지 구성](/help/forms/using/configuring-redirect-page.md)을 참조하십시오.

주소를 추가할 적응형 양식이 준비되었습니다. 자습서에 언급된 이름을 사용하고 AEM Forms 서버를 실행하는 컴퓨터에서 양식에 액세스한 경우 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)에서 양식을 사용할 수 있습니다.
