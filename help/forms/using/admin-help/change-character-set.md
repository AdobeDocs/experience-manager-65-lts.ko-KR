---
title: 문자 집합 변경
description: 출력 스트림을 인코딩하는 데 사용되는 문자 집합을 지정할 수 있습니다. 문자 집합을 변경하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 1d614736-5897-4fd3-9ca4-94b115139ba3
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 1%

---

# 문자 집합 변경 {#change-the-character-set}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

출력 스트림을 인코딩하는 데 사용되는 문자 집합을 지정할 수 있습니다.

1. 관리 콘솔에서 **[!UICONTROL 서비스 > 출력]**&#x200B;을 클릭합니다.
1. 국제화 아래의 문자 집합 목록에서 문자 집합을 선택합니다. 이 설정은 API를 통해 지정된 `TransformationFormat` 및 `PrintFormat`에 따라 다릅니다. 나열된 문자 세트 이외의 문자 세트를 지정하려면 사용자 정의를 선택하고 표시되는 상자에서 인코딩 값을 지정합니다.

   `TransformationFormat`이(가) PDF 및 PDF/A이거나 `PrintFormat`이(가) PCL, PostScript, Zebra 레이블, IPL, DPL, TPCL, GenericColorPCL 또는 GenericPSLevel3인 경우 특정 문자 집합만 지원됩니다.

   문자 집합은 유효한 정식 이름이어야 합니다. 기본값은 ISO-8859-1입니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
