---
title: 부재 설정 구성
description: 부재 중 기능을 사용하면 사용자가 부재 중일 때 AEM 양식에서 할당한 작업을 완료할 수 없는 시점을 지정할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: bf4fa6e4-25c7-46a8-9bae-4af7bfc14426
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# 부재 설정 구성 {#configuring-out-of-office-settings}

부재 중 기능을 사용하면 사용자나 관리자가 사용자가 부재 중일 때 AEM 양식에서 할당한 작업을 완료할 수 없는 시점을 지정할 수 있습니다. 사용자가 부재 중으로 설정되어 있는 동안 해당 작업은 하나 이상의 지정된 사용자에게 할당됩니다. 사용자는 Workspace에서 부재 중 설정을 변경하거나 관리자는 Forms Workflow에서 사용자를 대신하여 설정을 변경할 수 있습니다.

프로세스를 만들 때 Workbench 사용자는 부재 설정으로 인해 작업을 리디렉션할 수 있는지 여부를 지정할 수 있습니다.

## 사용자의 부재 중 정보 보기 {#view-a-user-s-out-of-office-information}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

1. 관리 콘솔에서 서비스 > 양식 워크플로우 > 부재 를 클릭합니다.
1. 부재 중 페이지 상단 근처에 있는 상자에서 다음 중 하나를 수행할 수 있습니다.

   **이름으로 검색**

   이름으로 검색 옵션을 선택합니다. 사용자 이름의 전체 또는 일부를 입력하고 찾기를 누릅니다. 필드를 비워 두면 Forms 워크플로우는 모든 사용자 목록을 반환합니다.

   **날짜 범위별로 검색**

   날짜 범위별 검색 옵션을 선택합니다. 원하는 타임스탬프와 함께 시작 및 종료 날짜를 지정하여 검색 결과의 범위를 좁힐 수 있습니다. 찾기를 누릅니다.

1. 사용자 이름을 클릭하여 사용자 목록 아래에 사용자의 부재 중 정보를 표시합니다.

## 사용자의 부재 중 상태 변경 {#change-a-user-s-out-of-office-status}

1. [사용자의 부재 중 정보 보기](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)에 설명된 대로 사용자를 찾습니다.
1. 변경할 사용자의 이름을 클릭합니다.
1. *사용자 이름*&#x200B;이(가) 현재 목록에서 Office에서 또는 Out of Office를 선택합니다.
1. 저장을 클릭합니다.

## 사용자에 대한 부재 중 날짜 범위 추가 {#add-an-out-of-office-date-range-for-a-user}

1. [사용자의 부재 중 정보 보기](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)에 설명된 대로 사용자를 찾습니다.
1. 변경할 사용자의 이름을 클릭합니다.
1. 날짜 범위 추가를 클릭합니다.
1. 시작 시간 및 종료 시간을 입력합니다. 달력 아이콘을 클릭하여 날짜를 선택할 수 있습니다. 종료 시간을 지정하지 않으면 사용자가 무기한 부재 중으로 설정됩니다.
1. 저장을 클릭합니다.

## 부재 중 작업에 대한 사용자 할당 {#assign-a-user-for-out-of-office-tasks}

사용자가 부재 중인 동안 사용자를 한 명 이상 할당하여 해당 사용자에 대한 새 작업을 수행할 수 있습니다. 다음 구성을 설정할 수 있습니다.

* 모든 새 작업을 지정된 기본 사용자에게 할당합니다.
* 작업을 재할당하지 마십시오. 부재 중인 사용자에게는 새 작업이 계속 할당됩니다.
* 대부분의 사용자 작업을 수신할 기본 사용자를 할당하지만 특정 프로세스의 작업이 다른 사용자에게 재할당되거나 부재 중인 사용자에게 계속 할당되도록 지정합니다.
* 기본 사용자를 할당하지 않고 특정 프로세스의 특정 작업을 특정 사용자에게 할당합니다.

   1. [사용자의 부재 중 정보 보기](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)에 설명된 대로 사용자를 찾습니다.
   1. 변경할 사용자의 이름을 클릭합니다.
   1. 부재 중 작업에 대한 기본 사용자 목록의 목록에서 사용자를 선택합니다. 재지정된 품목을 받을 기본 사용자를 지정하지 않으려면 지정 안함을 선택합니다.

      목록에 해당 사용자 이름이 나타나지 않으면 사용자 찾기를 누르고 사용자 찾기 대화 상자를 사용하여 사용자를 검색합니다. 목록에서 해당 사용자를 선택하고 사용자 선택 을 클릭합니다. 사용자 찾기 대화 상자에서 사용자 일정 보기 를 클릭하여 선택한 사용자의 부재 중 일정을 확인할 수도 있습니다.

   1. 기본 사용자에게 보내지 말아야 할 프로세스가 있는 경우 예외 추가를 클릭한 다음 프로세스를 선택하고 목록에서 다른 사용자를 선택합니다. 할당 안 함 을 선택하여 부재 중인 사용자에게 작업을 계속 할당할 수도 있습니다.
   1. 저장을 클릭합니다.
