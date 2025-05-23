---
title: 포함할 글꼴 지정
description: 적응형 양식에 포함할 글꼴을 지정하는 방법을 알아봅니다. Forms 서비스에서 생성하는 양식에 포함할 글꼴과 포함하지 않을 글꼴을 지정할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: c73dced8-7242-465c-85bc-9315a9a08605
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# 포함할 글꼴 지정 {#specifying-fonts-to-embed}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

Forms 서비스에서 생성하는 양식에 항상 포함할 글꼴과 포함하지 않을 글꼴을 지정할 수 있습니다. 글꼴을 포함하면 양식의 파일 크기가 증가합니다. 사용자가 시스템에 거의 가지고 있지 않은 특이한 글꼴을 임베드합니다. 일반적으로 설치된 일반 글꼴은 포함하지 마십시오.

>[!NOTE]
>
>Forms에 대한 사용자 지정 XCI 파일을 지정한 경우 XCI 파일의 포함 글꼴 옵션이 이러한 설정을 무시합니다. [Forms 위치 구성](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)을 참조하세요.

1. 관리 콘솔에서 **[!UICONTROL 서비스 > Forms]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL 글꼴 포함 설정]**&#x200B;의 **[!UICONTROL 항상 글꼴 포함]** 상자에서 양식에 포함할 글꼴 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴은 폼에서 사용되는 경우에만 생성된 폼에 포함됩니다. 서비스로 전달된 XCI 파일에서 글꼴 포함 옵션이 켜진 경우 PDF에 사용된 모든 글꼴이 항상 포함되므로 이 설정은 무시됩니다.
1. **[!UICONTROL 글꼴 임베드 안 함]** 상자에 양식에 임베드하지 않을 글꼴의 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴은 생성된 PDF에서 사용되더라도 PDF에 포함되지 않습니다. 서비스로 전달된 XCI 파일에서 글꼴 포함 옵션이 꺼진 경우 PDF에 사용된 글꼴이 하나도 포함되어 있지 않으므로 이 설정은 무시됩니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
