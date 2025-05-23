---
title: XCI 구성 옵션 지정
description: XCI 구성 옵션을 지정하는 방법을 알아봅니다. 적응형 양식에 대한 사용자 지정 XCI 파일 값을 지정하여 양식 렌더링 중에 사용할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 198016d7-0fb5-47e6-91ed-f2f0c98b2224
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 1%

---

# XCI 구성 옵션 지정 {#specifying-xci-configuration-options}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

Forms을 사용하면 렌더링에 사용할 수 있는 사용자 지정 XCI 파일을 지정할 수 있습니다. ([Forms 위치 구성](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)을 참조하십시오.) 기본적으로 Forms은 다음을 포함하여 XCI 파일에 지정된 일부 옵션을 재정의합니다.

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

위에 나열된 옵션의 재정의를 취소하는 옵션을 선택할 수 있습니다. 이 경우 Forms은 사용자 지정 XCI 파일에 지정된 값을 사용합니다.

1. 관리 콘솔에서 **서비스** > **Forms**&#x200B;을 클릭합니다.
1. 시스템 기본 XCI 옵션 사용 확인란을 선택하거나 선택 취소합니다. 이 옵션을 선택하면 Forms은 패킷, 생성자, 생성자 및 compressObjectStream 설정에 대해 해당 기본값을 사용합니다. 이 옵션을 선택 해제하면 Forms은 사용자 지정 XCI 파일에 지정된 값을 사용합니다.
1. **저장**&#x200B;을 클릭합니다.
