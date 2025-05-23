---
title: 다국어 자산
description: 바이너리, 메타데이터 및 태그를 비롯한 에셋을 여러 언어로 번역하기 위한 워크플로를 자동화하는 방법에 대해 알아봅니다.
contentOwner: AG
feature: Asset Management
role: Admin
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 512bd351-2e6b-47a2-85c6-a23ea2c7102f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---

# 다국어 자산 {#multilingual-assets}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=ko) |
| AEM 6.5 | 이 문서 |

[!DNL Adobe Experience Manager Assets]을(를) 사용하면 이진, 메타데이터 및 태그를 포함하여 에셋의 번역 워크플로를 자동화하여 다국어 프로젝트에서 사용할 다른 언어의 에셋을 생성할 수 있습니다.

번역 워크플로를 자동화하려면 번역 서비스 공급업체를 [!DNL Experience Manager]과(와) 통합하고 에셋을 다국어로 번역하는 프로젝트를 만듭니다. [!DNL Experience Manager]은(는) 사람 번역 및 기계 번역 워크플로를 지원합니다.

사람 번역: 번역된 자산을 반환하여 [!DNL Experience Manager]&#x200B;(으)로 가져옵니다. 번역 공급업체를 [!DNL Experience Manager]과(와) 통합하면 에셋이 [!DNL Experience Manager]과(와) 번역 공급업체 간에 자동으로 전송됩니다.

기계 번역: 기계 번역 서비스는 에셋의 메타데이터와 태그를 즉시 번역합니다.

에셋 번역에는 다음이 포함됩니다.

1. [Experience Manager과 번역 서비스 공급업체 연결](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [번역 통합 프레임워크 구성 만들기](/help/sites-administering/tc-tic.md)
1. [번역을 위한 자산 준비](preparing-assets-for-translation.md)
1. [폴더에 번역 클라우드 서비스 적용](transition-cloud-services.md)
1. [번역 프로젝트 만들기](translation-projects.md)

번역 서비스 공급자가 [!DNL Experience Manager]과(와) 통합할 커넥터를 제공하지 않는 경우 [대체 프로세스](/help/sites-administering/tc-manage.md#exporting-a-translation-job)를 사용하십시오.

[콘텐츠 조각에 대한 번역 프로젝트 만들기](creating-translation-projects-for-content-fragments.md)도 참조하세요.
