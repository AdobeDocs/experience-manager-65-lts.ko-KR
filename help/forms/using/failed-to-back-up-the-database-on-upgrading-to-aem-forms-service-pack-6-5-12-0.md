---
title: MySQL용 6.5.12.0(으)로 업그레이드하는 동안 데이터베이스를 백업하지 못했습니다.
description: 사용자가 Experience Manager 6.5.12.0(으)로 업그레이드하고 "MySQL 업그레이드"를 클릭하면 구성 관리자가 이전 Experience Manager Forms 데이터베이스를 백업하지 못합니다.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
exl-id: afc09a9f-58ef-4292-a2f2-b62d3246c006
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# MySQL용 6.5.12.0(으)로 업그레이드하는 동안 데이터베이스를 백업하지 못했습니다. {#issue}

사용자가 Experience Manager 6.5.12.0(으)로 업그레이드하고 &quot;MySQL 업그레이드&quot;를 클릭하면 구성 관리자가 이전 Experience Manager Forms 데이터베이스를 백업하지 못하고 다음 오류가 표시됩니다.

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 적용 대상 {#applies-to}

* Experience Manager 6.5 Forms

## 솔루션 {#solution}

이 문제를 해결하려면 데이터베이스의 max_packet_size를 100M로 늘리거나 필요에 따라 {AEM_HOME}/mysql에 있는 my.ini 파일에서 늘리십시오.
