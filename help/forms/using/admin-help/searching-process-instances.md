---
title: 프로세스 인스턴스 검색
description: '[프로세스 검색] 페이지에서는 프로세스 인스턴스를 찾기 위한 검색 조건을 입력할 수 있습니다.'
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
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# 프로세스 인스턴스 검색{#searching-for-process-instances}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

[프로세스 검색] 페이지에서는 프로세스 인스턴스를 찾기 위한 검색 조건을 입력할 수 있습니다. Forms Workflow 페이지에서 또는 프로세스 인스턴스 페이지에서 검색을 눌러 프로세스 검색 페이지에 액세스할 수 있습니다.

일반 검색을 수행할 기본 기준, 세부 검색을 수행할 특정 속성 또는 기본 기준과 특정 속성의 조합을 입력하여 결합된 검색을 수행할 수 있습니다.

## 일반 검색 수행 {#perform-a-general-search}

일반적인 프로세스 검색은 프로세스 인스턴스의 프로세스 ID를 알고 있거나, 관련 프로세스 인스턴스 그룹을 찾고 있거나, 일부 프로세스 인스턴스만 실행 중인 경우에 가장 적합합니다.

일반 검색을 수행하려면 기본 기준을 입력합니다. 여러 기준을 입력하면 내포된 AND 조건으로 검색이 수행됩니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로 > 프로세스 검색 을 클릭합니다.
1. 프로세스 검색 페이지의 일반 검색에서 다음 기준을 제공합니다.

   * **프로세스 ID:** 각 고유한 프로세스 인스턴스를 식별하는 양의 정수입니다.
   * **프로세스 상태:** 목록에서 상태를 선택합니다.
   * **응용 프로그램:** 목록에서 응용 프로그램을 선택합니다. 배포된 응용 프로그램만 표시됩니다.
   * **프로세스 이름 - 버전:** 메뉴에서 프로세스 이름을 선택합니다. 배포된 프로세스만 표시됩니다.

1. 검색을 클릭합니다. 검색된 인스턴스를 나열하는 [프로세스 인스턴스] 페이지가 나타납니다.

## 프로세스에 대한 세부 검색 수행 {#perform-a-detailed-search-for-a-process}

특정 속성을 입력하여 세부 검색을 수행할 수 있습니다. 실행 중인 프로세스 인스턴스가 많고 특정 기준에 따라 가능한 검색 범위를 좁혀야 하는 경우에는 세부 검색이 가장 적합합니다.

1. 관리 콘솔에서 서비스 > Forms 워크플로 > 프로세스 검색 을 클릭합니다.
1. 프로세스 검색 페이지의 상세 검색에서 첫 번째 기준 세트를 지정합니다.

   * 속성 목록에서 속성을 선택합니다.
   * 필터 목록에서 연산자를 선택합니다.
   * 값(Value) 상자에 선택한 속성에 적합한 값을 입력합니다.

1. 다른 행을 추가하려면 [추가 필터]를 선택합니다. 다른 속성, 필터 및 값 목록 세트와 조건 목록이 나타납니다.
1. Condition에서 AND 또는 OR를 선택합니다. 필요에 따라 1~3단계를 반복하여 검색 범위를 더 좁힙니다.
1. 행을 추가하거나 제거하려면 [추가 필터] 또는 [더 적은 필터]를 클릭합니다. 1행에서 4행까지 가질 수 있습니다.
1. 검색을 클릭합니다. 검색된 인스턴스를 나열하는 [프로세스 인스턴스] 페이지가 나타납니다.

[프로세스 인스턴스 상태 정보](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## 프로세스에 대한 통합 검색 수행 {#perform-a-combined-search-for-a-process}

영역 사이에 AND가 암시되어 있는 일반 검색 및 세부 검색을 모두 기반으로 검색을 생성하려면 프로세스 검색 페이지의 일반 검색 및 세부 검색 영역 모두에 검색 기준을 입력합니다.

검색 범위가 너무 좁으면 인스턴스를 찾을 수 없습니다.
