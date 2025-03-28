---
title: 작업 관리자 끝점 구성
description: 서비스를 호출하기 위해 작업 관리자 끝점을 구성하는 방법에 대해 알아봅니다. 작업 관리자 끝점을 구성하려면 다른 설정이 필요합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 57fd8b5d-6347-4b83-9489-e8ee59ee39a5
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 작업 관리자 끝점 구성 {#configuring-task-manager-endpoints}

작업 관리자 엔드포인트를 사용하면 Workspace 사용자가 서비스를 호출할 수 있습니다.

**작업 관리자 끝점 설정**

다음 설정을 사용하여 Task Manager 끝점을 구성합니다.

**이름:**(필수) 끝점을 식별합니다. Workspace의 카드 보기에 이름이 표시됩니다. Workspace에 표시된 이름이 잘리므로 &lt; 문자를 포함하지 마십시오. 끝점의 이름으로 URL을 입력하는 경우 RFC1738에 지정된 구문 규칙을 준수하는지 확인하십시오.

**설명:** 끝점에 대한 설명입니다. Workspace에 표시된 설명이 잘리므로 &lt; 문자를 포함하지 마십시오.

**작업 지침:** 이 워크플로를 시작하는 사용자를 위한 지침입니다.

**프로세스 소유자:** 프로세스를 담당하는 사람의 이름입니다.

**사용자가 작업을 전달할 수 있음:** 사용자가 초기 작업을 전달할 수 있도록 허용합니다.

**첨부 파일 창 표시:** 사용자가 첨부 파일 창을 볼 수 있도록 허용합니다.

**첨부 파일 추가 허용:** 사용자가 첨부 파일 및 메모를 추가할 수 있도록 허용합니다.

**처음 잠긴 작업:** 초기 작업을 잠급니다.

**공유 대기열에 대한 ACL 추가:** 초기 작업은 공유 대기열 사용자에 대한 ACL로 만들어집니다.

**범주화:**(필수) 사용자가 Workspace에서 양식을 볼 수 있는 범주입니다. 목록에서 범주를 선택하거나 새 범주 를 선택하여 범주를 추가합니다.

**작업 이름:**(필수) 끝점에 할당할 수 있는 작업 목록입니다.
