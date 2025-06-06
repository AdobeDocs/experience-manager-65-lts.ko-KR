---
title: 다국어화 옵션 설정
description: 양식 렌더링에 사용되는 로케일을 지정하는 방법과 출력 스트림을 인코딩하는 데 사용되는 문자 집합을 지정하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 47a49147-2921-4d28-8d04-2281c0b9a190
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 1%

---

# 다국어화 옵션 설정{#setting-internationalization-options}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

## 양식 렌더링에 사용되는 로케일 지정 {#specify-the-locale-used-to-render-forms}

PDF 양식을 렌더링할 때 사용되는 로케일을 지정할 수 있습니다. PDF 양식의 필드는 지정된 로케일을 사용하여 데이터를 표시합니다. 예를들어 로케일이 독일어로 설정되어 있으면 폼은 숫자 값에 독일어 소수 구분 기호를 사용합니다. 로케일은 HTML 변환의 일부로서 웹 브라우저와 같은 클라이언트 디바이스에 유효성 검사 메시지를 전송하는 데에도 사용됩니다.

1. 관리 콘솔에서 서비스 > Forms을 클릭합니다.
1. 국제화 아래의 언어 목록에서 양식을 렌더링하는 데 사용되는 로케일을 선택합니다. 기본값은 영어(미국)입니다.
1. 저장을 클릭합니다.

## 출력 스트림을 인코딩하는 데 사용되는 문자 집합을 지정합니다. {#specify-the-character-set-used-to-encode-the-output-stream}

1. 국제화 아래의 문자 집합 목록에서 문자 집합을 선택합니다. 이 설정은 사용된 API(renderHTMLForm 또는 renderPDFForm)에 따라 다릅니다. 나열된 문자 세트 이외의 문자 세트를 지정하려면 사용자 정의를 선택하고 표시되는 상자에서 인코딩 값을 지정합니다.

   HTML 변환의 경우 AEM forms에서 `java.nio.charset` 패키지로 정의된 문자 인코딩 값을 지원합니다. sFormPreference가 PDFForm이면 특정 문자 집합만 지원됩니다. 문자 집합은 유효한 정식 이름이어야 합니다. 기본값은 ISO-8859-1입니다.

1. 저장을 클릭합니다.
