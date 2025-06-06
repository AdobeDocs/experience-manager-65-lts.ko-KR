---
title: Forms 서비스
description: 이 문서에서는 Forms 서비스 및 Forms 서비스를 사용하여 수행할 수 있는 양식 관련 작업에 대해 설명합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services,Forms Service,PDF Generator
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 1e7aa0fa-4440-42fb-8e0b-3c757568b78f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Forms 서비스 {#forms-service}

## 개요 {#overview}

Forms 서비스를 사용하면 일반적으로 Designer에서 생성되는 양식을 확인, 처리, 변환 및 제공하는 대화형 데이터 캡처 클라이언트 애플리케이션을 만들 수 있습니다. Forms 서비스는 사용자가 개발하는 모든 양식 디자인을 PDF 문서로 렌더링합니다.

또한 Forms service를 통해 조직은 전자 양식을 Adobe PDF로 배포하여 지능형 데이터 캡처 프로세스를 확장할 수 있습니다. 또한 이 서비스를 사용하여 기존 PDF forms으로 데이터를 가져오거나 기존 에서 데이터를 내보낼 수도 있습니다.

Forms 서비스를 사용하여 다음을 수행합니다.

* 템플릿 및 XML 데이터를 기반으로 PDF forms을 렌더링합니다.
* 양식 데이터 통합을 활성화하여 PDF forms으로 데이터를 가져오고 데이터를 추출합니다.
* 조각을 기반으로 양식 렌더링

## PDF forms 만들기  {#creating-pdf-forms-nbsp}

양식 서비스를 사용하여 데이터 캡처를 위한 PDF forms을 만듭니다. 일반적으로 AEM Forms Designer 템플릿으로 시작합니다. Forms 서비스의 `renderPDFForm`(Javadoc에 대한 링크) 작업을 사용하여 이 템플릿을 PDF 양식으로 변환합니다.

`renderPDFForm` 작업의 첫 번째 매개 변수는 템플릿 파일의 이름입니다(예: `ExpenseClaim.xdp`). 템플릿 파일을 로컬 파일 시스템, CRX 저장소 또는 HTTP 또는 FTP 위치에 저장할 수 있습니다. `renderPDFForm` 작업의 `PDFFormRenderOptions` 매개 변수에서 콘텐츠 루트를 설정하여 템플릿 파일의 위치를 지정할 수 있습니다. `PDFFormRenderOptions` 매개 변수에 대해 지정할 수 있는 기타 옵션에 대한 자세한 내용은 Javadoc을 참조하십시오.

`renderPDFForm` 작업에서도 XML 데이터를 사용할 수 있습니다. 생성된 PDF 양식에 지정된 데이터가 포함되도록 PDF 양식을 만들 때 XML 데이터가 템플릿과 병합됩니다. `renderPDFForm` 작업의 두 번째 매개 변수는 XML 데이터가 포함된 문서(Javadoc) 개체를 사용할 수 있습니다.

## PDF forms에서 데이터 추출  {#extracting-data-from-pdf-forms-nbsp}

Forms 서비스의 `exportData`(Javadoc) 작업을 사용하여 PDF 양식에서 데이터 XML을 추출합니다. 이 작업은 문서를 첫 번째 매개 변수로 허용합니다. 데이터를 XDP 문서 또는 XML 파일로 내보낼 수 있습니다. 데이터를 XML 파일로 내보내면 내보낸 데이터는 XDP 포락선을 제거하고 일반 XML 파일을 반환합니다. 두 번째 매개 변수를 사용하여 이 배열을 지정할 수 있습니다.

## PDF forms으로 데이터 가져오기 {#importing-data-into-pdf-forms}

또한 Forms 서비스를 사용하면 AEM Forms Designer 또는 `renderPDFForm` 작업을 사용하여 만든 PDF 양식을 XML 데이터와 병합할 수 있습니다. Forms 서비스의 `importData`(Javadoc) 작업은 PDF 양식과 XML 데이터를 수락하고 데이터 XML이 있는 PDF 양식을 반환합니다.

## 조각을 기반으로 한 양식 렌더링 {#rendering-forms-based-on-fragments}

Forms 서비스는 AEM Forms Designer을 사용하여 만든 조각을 기반으로 양식을 렌더링할 수 있습니다. 조각은 양식의 재사용 가능한 부분입니다. 여러 양식 디자인에 삽입할 수 있는 별도의 XDP 파일로 저장됩니다. 예를 들어 조각에는 주소 블록이나 법적 텍스트가 포함될 수 있습니다.

조각을 사용하면 많은 수의 양식을 간편하게 만들고 유지 관리할 수 있습니다. 양식을 작성할 때 조각이 양식에 표시되는 데 필요한 조각에 대한 참조를 삽입합니다. 조각 참조에는 실제 XDP 파일을 가리키는 하위 양식이 포함되어 있습니다.

다음은 조각을 사용할 때의 장점입니다.

* **콘텐츠 재사용**: 여러 양식 디자인에서 콘텐츠를 재사용할 수 있습니다. 동일한 콘텐츠의 일부를 여러 양식으로 신속하게 재사용하려면 조각을 만듭니다. 콘텐츠를 복사하거나 다시 만드는 데 시간이 더 오래 걸립니다. 또한 조각을 사용하면 양식 디자인에서 자주 사용되는 부분이 참조하는 모든 양식에서 일관된 내용과 모양을 갖게 됩니다.
* **전역 업데이트**: 파일에서 한 번만 여러 양식을 전체적으로 변경할 수 있습니다. 조각의 콘텐츠, 스크립트 개체, 데이터 바인딩, 레이아웃 또는 스타일을 변경할 수 있습니다. 조각을 참조하는 모든 XDP 양식은 변경 사항을 반영합니다.
* **공유 양식 만들기**: 여러 리소스 간에 양식 만들기를 공유할 수 있습니다. 스크립팅 또는 AEM Forms Designer의 기타 고급 기능에 대한 전문 지식을 갖춘 양식 개발자는 스크립팅 및 동적 속성을 사용하는 조각을 개발하고 공유할 수 있습니다. 양식 디자이너는 조각을 사용하여 양식을 디자인할 수 있습니다. 또한 조각을 사용하여 양식의 모든 부분이 여러 양식에서 일관된 모양과 기능을 가지도록 할 수 있습니다.
