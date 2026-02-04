---
title: 프로세스 인스턴스 검색
description: 프로세스 검색 페이지에서 프로세스 인스턴스를 찾기 위한 검색 기준을 입력합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: e358ee51-c23f-4737-9dcf-3193ed541bbb
source-git-commit: 51342861dd01e659999c19fbe0274e8d3cbcf8c4
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 65%

---

# 프로세스 인스턴스 검색{#searching-for-process-instances}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

프로세스 검색 페이지에서 프로세스 인스턴스를 찾기 위한 검색 기준을 입력합니다. Forms Workflow 페이지에서 프로세스 검색 페이지에 액세스할 수 있습니다. 또는 프로세스 인스턴스 페이지에서 **검색**&#x200B;을 클릭할 수 있습니다.

기본 기준을 입력하면 일반 검색을 수행하고, 특정 속성을 입력하면 상세 검색을 수행하며, 기본 기준과 특정 속성을 함께 입력하면 결합 검색을 수행할 수 있습니다.

## 일반 검색 수행 {#perform-a-general-search}

프로세스 인스턴스의 프로세스 ID를 알고 있는 경우 프로세스에 대한 일반 검색이 가장 적합합니다. 또는 관련 프로세스 인스턴스 그룹을 찾거나 소수의 프로세스 인스턴스만 실행 중인 경우

일반 검색을 수행할 기본 기준을 입력합니다. 여러 기준을 입력하는 경우 암시적 AND 조건으로 검색이 수행됩니다.

1. 관리 콘솔에서 서비스 > Forms Workflow > 프로세스 검색 을 클릭합니다.
1. 프로세스 검색 페이지의 일반 검색에서 다음 기준을 제공합니다.

   * **프로세스 ID:** 각 고유 프로세스 인스턴스를 식별하는 양의 정수입니다.
   * **프로세스 상태:** 목록에서 상태를 선택합니다.
   * **애플리케이션:** 목록에서 애플리케이션을 선택합니다. 배포된 애플리케이션만 표시됩니다.
   * **프로세스 이름 - 버전:** 메뉴에서 프로세스 이름을 선택합니다. 배포된 프로세스만 표시됩니다.

1. **검색**&#x200B;을 클릭합니다. 발견된 인스턴스가 나열된 프로세스 인스턴스 페이지가 나타납니다.

## 프로세스에 대한 상세 검색 수행 {#perform-a-detailed-search-for-a-process}

특정 속성을 입력하여 상세 검색을 수행할 수 있습니다. 많은 프로세스 인스턴스가 실행 중이고 특정 기준에 따라 가능한 검색 범위를 좁혀야 하는 경우에는 상세 검색이 가장 적합합니다.

1. 관리 콘솔에서 서비스 > Forms Workflow > 프로세스 검색 을 클릭합니다.
1. 프로세스 검색 페이지의 상세 검색에서 첫 번째 기준 세트를 지정합니다.

   * 속성 목록에서 속성을 선택합니다.
   * 필터 목록에서 연산자를 선택합니다.
   * 값 상자에 선택한 속성에 적합한 값을 입력합니다.

1. 다른 행을 추가하려면 필터 더 보기를 선택합니다. 그러면 또 다른 속성, 필터, 값 집합 목록과 조건 목록이 나타납니다.
1. 조건에서 AND 또는 OR를 선택합니다. 검색 범위를 더욱 좁히려면 필요에 따라 1~3단계를 반복합니다.
1. 행을 추가하거나 제거하려면 필터 더 보기 또는 필터 줄이기를 클릭합니다. 1~4행까지 지정할 수 있습니다.
1. **검색**&#x200B;을 클릭합니다. 발견된 인스턴스가 나열된 프로세스 인스턴스 페이지가 나타납니다.

[프로세스 인스턴스 상태 정보](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)도 참조하세요.

## 프로세스에 대한 결합 검색 수행 {#perform-a-combined-search-for-a-process}

일반 기준과 세부 기준을 모두 사용하는 검색을 생성하려면 프로세스 검색 페이지의 두 영역에 값을 입력합니다. 시스템은 두 영역 사이에 암시된 `AND`을(를) 적용합니다.

검색 범위가 너무 좁으면 인스턴스를 찾을 수 없습니다.
