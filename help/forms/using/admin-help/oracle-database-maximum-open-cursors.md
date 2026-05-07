---
title: Oracle 데이터베이스 최대 열린 커서 임계값
description: Oracle에서 열린 커서의 최대값을 구성하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
exl-id: 98663f16-6c05-4485-9bf2-a2de9d1975c8
source-git-commit: 26f8a32961cf18c2f1930ab7bc910333b3ccf188
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 100%

---

# Oracle 데이터베이스 최대 열린 커서 임계값 {#oracle-database-maximum-open-cursors-threshold}

Oracle에서 열린 커서의 최대값을 구성하려면 이 값을 애플리케이션에 적합한 숫자로 조정해야 할 수도 있습니다. 적당한 부하에서는 평균 열린 커서 수가 2,700개였던 것으로 확인됩니다. 처음에는 상한선을 3,000개로 시작하는 것이 좋습니다. 자세한 내용은 [https://www.orafaq.com/node/758](https://www.orafaq.com/node/758)에서 확인하십시오.
