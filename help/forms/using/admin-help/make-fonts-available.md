---
title: 글꼴을 사용 가능하도록 제공
description: 양식 내에 사용된 글꼴이 AEM 양식을 호스팅하는 J2EE 애플리케이션 서버에서 사용할 수 있는지 확인합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 2861bde5-b373-4ab2-9808-7d32ef1dc925
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 2%

---

# 글꼴을 사용 가능하도록 제공 {#make-fonts-available}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

양식 내에 사용된 글꼴이 AEM 양식을 호스팅하는 J2EE 애플리케이션 서버에서 사용할 수 있는지 확인합니다. 예를 들어 다음 시나리오를 고려하십시오. 양식 디자이너는 Designer이 사용하는 글꼴 디렉터리에 글꼴을 추가하고 별도의 컴퓨터에서 해당 글꼴을 사용하는 양식을 만듭니다. 출력 서비스에서 글꼴을 사용하려면 Customer fonts 디렉토리에 넣습니다. Customer fonts 디렉토리가 없는 경우 AEM Forms를 호스팅하는 J2EE 응용 프로그램 서버에 디렉토리를 만듭니다.

추가 글꼴 설정에 대한 자세한 내용은 [일반 AEM 양식 설정 구성](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)을 참조하십시오.

**고객 글꼴 디렉터리 위치 지정**

1. 관리 콘솔에서 설정 > 핵심 시스템 설정 > 구성 을 클릭합니다.
1. 시스템 글꼴 디렉토리 위치 상자에 고객 글꼴 디렉토리 경로를 입력합니다. 여러 디렉터리를 세미콜론 **;**(으)로 구분하여 추가할 수 있습니다.
1. 확인을 클릭합니다.
1. AEM Forms가 설치된 시스템을 다시 시작합니다.

>[!NOTE]
>
>Windows 시스템 글꼴 캐시에서 글꼴을 선택하고 캐시를 업데이트하려면 시스템을 다시 시작해야 합니다. Customer 글꼴 디렉터리를 지정한 후 AEM Forms가 설치된 시스템을 다시 시작해야 합니다.
