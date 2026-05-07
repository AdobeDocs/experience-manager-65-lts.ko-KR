---
title: XCI 구성 옵션 지정
description: XCI 구성 옵션을 지정하는 방법을 알아봅니다. 적응형 양식에 사용자 정의 XCI 파일 값을 지정하여 양식 렌더링 중에 사용할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
exl-id: 198016d7-0fb5-47e6-91ed-f2f0c98b2224
source-git-commit: 26f8a32961cf18c2f1930ab7bc910333b3ccf188
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 90%

---

# XCI 구성 옵션 지정 {#specifying-xci-configuration-options}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

Forms를 사용하면 렌더링에 사용할 수 있는 사용자 정의 XCI 파일을 지정할 수 있습니다. ([Forms 위치 구성](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)을 참조하십시오.) 기본적으로 Forms은 다음을 포함하여 XCI 파일에 지정된 일부 옵션을 재정의합니다.

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

위에 나열된 옵션에 대한 재정의를 취소하는 옵션을 선택할 수 있으며, 이 경우 Forms는 사용자 정의 XCI 파일에 지정된 값을 사용합니다.

1. 관리 콘솔에서 **서비스** > **Forms**&#x200B;를 클릭합니다.
1. 시스템 기본 XCI 옵션 사용 확인란을 선택하거나 선택 취소합니다. 이 옵션을 선택하면 Forms에서 패킷, 만든 사람, 제작자 및 compressObjectStream 설정에 대한 기본값을 사용합니다. 이 옵션을 선택 취소하면 Forms는 사용자 정의 XCI 파일에 지정된 값을 사용합니다.
1. **저장**&#x200B;을 클릭합니다.
