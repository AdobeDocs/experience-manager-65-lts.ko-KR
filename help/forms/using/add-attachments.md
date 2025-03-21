---
title: 첨부 파일 추가
description: AEM Forms 앱에서 사진과 스크리블 메모를 작업에 주석으로 추가합니다
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: ef0917ec-bae2-4a5c-b3ca-5b6e57f8bc93
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# 첨부 파일 추가{#adding-attachments}

## AEM Forms 워크플로 서버(JEE의 AEM Forms)와 동기화된 양식에서 첨부 파일 추가 {#adding-annotations}

AEM Forms 앱을 사용하면 AEM Forms JEE 서버와 동기화된 양식에 이미지, 스크리블 메모, 텍스트 메모를 첨부할 수 있습니다. 양식이 AEM Forms Workflow 서버에서 로드되면 첨부 파일이 양식에 추가됩니다. 첨부 파일 버튼 ![attachments-app](assets/attachments-app.png)을(를) 선택하여 양식의 모든 첨부 파일을 함께 볼 수 있습니다. 빨간색 알림은 양식의 첨부 파일 수를 지정합니다. 양식에 첨부 파일이 없으면 빨간색 알림 버튼이 표시되지 않습니다. 양식에 첨부 파일이 없는 경우 첨부 단추 ![첨부](assets/attch.png)를 선택하면 사진이나 낙서를 첨부할 수 있는 옵션이 제공됩니다.

옵션은 다음과 같습니다.

* **갤러리**: 장치에 저장된 사진에서 사진을 추가할 수 있습니다.

* **카메라**: 사진을 찍어 양식에 추가할 수 있습니다.

* **메모**: 낙서 또는 텍스트 메모를 추가할 수 있습니다. 낙서를 추가하려면 ![낙서](assets/scribble.png)를 사용하고, 텍스트 메모를 추가하려면 ![키보드](assets/keyboard.png)를 사용하십시오.

>[!NOTE]
>
>한 사용자가 추가한 첨부 파일은 다른 AEM Forms 앱 사용자에게 표시됩니다. 다른 사용자는 사용자가 추가한 첨부 파일을 삭제할 수 없습니다.
>

### 첨부 파일 화면 {#the-attachments-screen}

한 위치에 있는 모든 첨부 파일을 보려면 ![첨부 파일-앱](assets/attachments-app.png)을 선택하세요. 여기에서 첨부 파일을 추가, 이름 변경 및 삭제할 수 있습니다.

![한 곳에 있는 모든 첨부 파일](assets/attachments-screen.png)

첨부 파일 화면의 **+** 단추를 사용하여 다른 그림, 낙서 또는 텍스트를 첨부할 수 있습니다.

### 사진 추가 {#adding-a-photograph}

모바일 장치의 카메라나 장치에 저장된 사진을 사용하여 양식에 사진을 첨부할 수 있습니다.

1. 창 맨 아래에 있는 첨부 파일 단추 ![attch](assets/attch.png)을(를) 선택합니다.
1. 표시되는 팝업에서 **갤러리** 또는 **카메라**&#x200B;를 선택합니다.
1. 선택한 옵션에 따라 다음을 수행합니다.

   1. **카메라**&#x200B;를 선택하는 경우.

      사진 찍어요 **사용** ![사용-사진](assets/use-pic.png) 단추를 선택합니다.

      또는 **사진을 다시 찍기** ![다시 찍기](assets/retake.png) 단추를 선택하여 사진을 다시 찍으십시오.

   1. **갤러리**&#x200B;를 선택하는 경우.

      장치의 이미지 브라우저 팝업이 표시됩니다. 장치의 그림 브라우저에서 첨부할 그림을 선택합니다.

### 메모 추가 {#adding-a-note}

**메모** 옵션을 사용하면 양식에 자유 형식 낙서와 텍스트 첨부 파일을 추가할 수 있습니다.

1. 창 맨 아래에 있는 첨부 파일 단추 ![attch](assets/attch.png)을(를) 선택합니다.
1. 표시되는 팝업에서 **메모**&#x200B;을(를) 선택합니다.
1. 실행된 Notes 사용자 인터페이스에서 자유 형식의 스크리블 을 캡처합니다.

   ![스크리블 인터페이스](assets/scribble-ui.png)

   낙서

   스크리블 인터페이스에서 다음 옵션을 사용할 수 있습니다.

   * **지우기**: 화면을 지웁니다.
   * **완료 단추**: 현재 스크리블을 첨부합니다.
   * **취소 단추**: 현재 스크리블을 삭제하고 스크리블 사용자 인터페이스를 종료합니다.
   * ![키보드](assets/keyboard.png): 낙서를 지우고 텍스트 메모를 추가할 수 있습니다.

   ![AEM Forms 앱 스크리블 키보드](assets/keyboard-inapp.png)

## AEM Forms 워크플로우 없이 AEM Forms 서버와 동기화된 양식의 첨부 파일(OSGi의 AEM Forms) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

AEM Forms OSGi 서버와 동기화된 모바일 양식의 첨부 파일은 AEM Forms JEE 서버와 유사하게 작동합니다.

AEM Forms OSGi 서버에서 앱에 로드된 적응형 양식에 대해서는 양식 수준 첨부 파일이 지원되지 않습니다. 이미지 또는 텍스트 메모를 첨부하려면 작성할 때 양식의 필드 수준 첨부 파일을 활성화합니다. 필드의 구성 요소 브라우저에서 첨부 파일 구성 요소를 드래그 앤 드롭합니다.

적응형 양식이 있는 경우 기록 문서(DoR)에서 첨부 파일을 볼 수 있습니다. [XFA 이외의 적응형 양식에 대한 기록 문서 생성](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)을 참조하세요.
