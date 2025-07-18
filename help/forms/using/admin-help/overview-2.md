---
title: 인증서 및 자격 증명 관리의 기본 사항
description: 인증서 및 자격 증명 관리의 기본 사항에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 8aeacdb7-68a7-476f-a725-f9ad7406cc9c
source-git-commit: 02b9eb98d1fdf1b090166a6ae7c0a4379487d2e1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 인증서 및 자격 증명 관리의 기본 사항 {#basics-of-managing-certificates-and-credentials}

*자격 증명*&#x200B;에 문서에 서명하거나 문서를 식별하는 데 필요한 개인 키 정보가 포함되어 있습니다. *인증서*&#x200B;는 트러스트에 대해 구성하는 공개 키 정보입니다. AEM forms에서는 여러 가지 용도로 인증서 및 자격 증명을 사용합니다.

* Acrobat Reader DC 확장은 자격 증명을 사용하여 PDF 문서에서 Adobe Reader 사용 권한을 활성화합니다. ([Acrobat Reader DC 확장에 사용할 자격 증명 구성](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)을 참조하십시오.)
* 신뢰할 수 있는 발급자에서만 Acrobat에서 사용할 자격 증명을 표시하도록 Rights Management을 구성할 수 있습니다. [Rights Management 표시 설정 구성](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings)을 참조하십시오. 인증서에 CN(일반 이름)이 있어야 합니다.
* 서명 서비스는 인증서 및 자격 증명에 액세스합니다. 서명 서비스에 대한 자세한 내용은 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_65)를 참조하십시오.

**쌍 키 생성**

AEM forms는 Trust Store를 사용하여 인증서, 자격 증명 및 CRL(인증서 해지 목록)을 저장하고 관리합니다. 또한 독립 하드웨어 보안 모듈(HSM) 장치를 사용하여 개인 키를 저장할 수 있습니다.

AEM forms에서는 키 쌍을 생성하는 옵션을 제공하지 않습니다. 그러나 Java 키 도구와 같은 도구를 사용하여 생성하고 AEM forms Trust Store에서 가져올 수 있습니다. Java 키 도구에 대한 자세한 내용은 다음을 참조하십시오.

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

지원되는 서명 유형은 다음과 같습니다. AEM 양식으로 가져올 수 있습니다.

* XML 서명
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* DSA 서명

**손실되거나 손상된 키 처리**

키가 손실되었거나 손상된 것으로 의심되는 경우 다음 조치를 취하십시오.

1. 인증 기관이 인증서 취소 목록에 손상된 키를 추가하여 키를 취소하도록 인증 기관에 알립니다.
1. 인증 기관에서 새 키와 해당 인증서를 받습니다.
1. 손상된 키를 사용하여 서명한 문서에 새 키를 사용하여 다시 서명합니다.
