---
title: 데이터베이스 증가 최소화 팁
description: 오래 지속되는 프로세스는 AEM 양식 데이터베이스에 프로세스 데이터를 저장합니다. 몇 가지 간단한 프로세스 설계와 제품 구성 전략을 사용하여 AEM 양식 데이터베이스의 증가를 최소화할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: ac3766c5-b741-4e65-8053-0c9cfd66a2f9
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 데이터베이스 증가 최소화 팁 {#tips-for-minimizing-database-growth}

오래 지속되는 프로세스는 AEM 양식 데이터베이스에 프로세스 데이터를 저장합니다. 몇 가지 간단한 프로세스 설계와 제품 구성 전략을 사용하여 AEM 양식 데이터베이스의 증가를 최소화할 수 있습니다.

## 프로세스 디자인 팁 {#process-design-tips}

가능하면 수명이 짧은 프로세스를 사용하십시오. 수명이 짧은 프로세스는 프로세스 데이터를 데이터베이스에 저장하지 않습니다. 단기 공정 사용의 단점은 그 상태와 상태가 관리 콘솔에서 추적되지 않고 공정 내역이 없다는 것이다.

작업 할당 작업(사용자 서비스)과 같은 일부 서비스 작업은 장기 프로세스에서 사용해야 합니다. 이 경우 프로세스를 여러 하위 프로세스로 분할하고 가능한 경우 단기 상태로 만들 수 있습니다. 이 전략을 사용하는 경우 단기 하위 프로세스는 문서 값과 같은 대용량 데이터 항목을 처리해야 합니다.

변수는 제한적으로 사용하십시오. 수명이 긴 프로세스를 사용할 경우 모든 프로세스 인스턴스에 대해 데이터베이스의 각 프로세스 변수에 대한 공간이 할당됩니다. 변수를 전략적으로 사용하면 상당한 양의 공간을 절약할 수 있습니다. 예를 들어 이전 값이 프로세스에 더 이상 필요하지 않은 경우 변수 값을 덮어쓸 수 있습니다. 그리고 만들었으며 사용하지 않는 변수를 모두 삭제합니다. 프로세스의 유효성을 검사하여 사용하지 않는 변수를 찾을 수 있습니다.

간단한 변수 유형(예: string 또는 int)을 사용하고 가능한 경우 복잡한 변수 유형을 사용하지 마십시오. 변수에 값이 포함되지 않은 경우에도 데이터베이스 공간이 할당됩니다. 복잡한 변수는 일반적으로 간단한 변수보다 더 많은 공간을 필요로 합니다.

## 제품 관리 팁 {#product-administration-tips}

GDS(전역 문서 저장소)를 효과적으로 사용합니다. Forms 서버의 GDS 디렉토리는 특히 프로세스에서 AEM 양식의 일부인 서비스에 전달되는 파일을 저장하는 데 사용됩니다. 성능을 향상시키기 위해 대신 작은 문서는 메모리에 저장되고 데이터베이스에 유지됩니다.

관리 콘솔은 메모리에 저장되고 데이터베이스에 지속되는 문서의 최대 크기를 구성하기 위한 기본 문서 최대 인라인 크기 속성을 표시합니다. ([일반 AEM 양식 설정 구성](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)을 참조하십시오.) 이 속성을 낮은 값으로 설정하면 대부분의 문서가 데이터베이스가 아닌 GDS 디렉터리에서 유지됩니다. GDS 디렉토리에 저장되는 경우 더 이상 필요하지 않은 파일을 보다 쉽게 삭제할 수 있다는 이점이 있습니다.
