---
title: JEE의 AEM Forms 프로세스에 데이터를 제출하도록 AEM Forms 구성
description: 양식 데이터 처리를 위해 JEE 프로세스의 AEM Forms과 적응형 양식을 통합합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: c888da5d-6a98-4139-9656-a187177efcb0
hide: true
hidefromtoc: true
source-git-commit: 1336ccddcc73459f933e5e4b00a3a22605cdb9a1
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# JEE 프로세스에서 AEM 양식에 양식 데이터를 제출하도록 AEM Forms 구성{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

적응형 양식은 추가 처리를 위해 JEE의 AEM Forms 프로세스에 데이터 제출을 지원합니다. 제출된 양식에서 사용할 수 있는 데이터로 JEE의 AEM Forms 프로세스를 트리거할 수 있습니다. AEM Forms 인스턴스를 활성화하여 적응형 양식을 JEE의 AEM Forms 프로세스에 제출할 수 있도록 다음 단계를 수행하십시오.

## AEM Forms 서버 구성 {#configure-your-aem-forms-server}

AEM Forms 서버가 JEE 서버의 AEM Forms에 데이터를 제출할 수 있도록 다음 단계를 수행하십시오.

1. https://[*host*]:[*port*]/system/console/configMgr에서 AEM 웹 구성 콘솔로 이동합니다.

1. **Adobe LiveCycle Client SDK 구성** 구성 요소를 찾아 클릭합니다.
1. 를 클릭하여 JEE 서버의 AEM Forms에 대한 구성 서버 URL, 사용자 이름 및 암호를 편집합니다.
1. 설정을 검토하고 **저장**&#x200B;을 클릭하세요.

![Adobe LiveCycle Client SDK 구성](assets/clientsdkconfiguration.jpg)

## 프로세스 필드를 사용하여 데이터 매핑 {#map-data-with-process-fields}

AEM Forms을 구성한 후 제출된 양식의 데이터 XML 및 첨부 파일을 JEE의 AEM Forms 프로세스에 있는 필드에 매핑합니다. 다음 작업을 수행합니다.

1. AEM 웹 구성 콘솔에서 을 클릭하여 **Guide LiveCycle Process Locator 및 Invoker** 구성을 편집합니다.
1. 다음 매개 변수를 지정합니다.

   * **데이터 xml 매개 변수의 이름**(필수): 제출된 데이터를 처리해야 하는 JEE의 AEM Forms 프로세스에 대한 XML 속성 파일을 지정합니다. 기본값은 **dataxml**&#x200B;입니다.

   * **첨부 파일 매개 변수의 이름**(선택 사항): JEE의 AEM Forms 프로세스에서 처리해야 하는 문서 개체의 목록을 지정합니다. 기본값은 **fileAttachmentsList**&#x200B;입니다.

1. 설정을 검토하고 **저장**&#x200B;을 클릭하세요.

![LiveCycle Process Locator 및 Invoker 안내](assets/test3.jpg)

구성된 경우 Forms Workflow에 제출 액션은 지정된 데이터 xml 매개 변수를 포함하는 JEE의 AEM Forms 서버 프로세스를 나열합니다.
