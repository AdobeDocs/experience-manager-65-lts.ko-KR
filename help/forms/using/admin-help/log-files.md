---
title: 로그 파일
description: 런타임 오류나 시작 오류와 같은 이벤트는 애플리케이션 서버 로그 파일에 기록되며, 이 로그 파일은 모든 텍스트 편집기를 사용하여 열 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: ff4dce07-725e-4750-9e95-4261b50580bd
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 97%

---

# 로그 파일 {#log-files}

런타임 오류나 시작 오류와 같은 이벤트는 애플리케이션 서버 로그 파일에 기록됩니다. 애플리케이션 서버에 배포하는 데 문제가 있는 경우 로그 파일을 사용하여 문제를 찾을 수 있습니다. 모든 텍스트 편집기를 사용하여 로그 파일을 열 수 있습니다.

(JBoss) 다음과 같은 로그 파일은 `[appserver root]/server/'server'/log` 디렉터리에 있습니다.

* boot.log
* server.log.*[yyyy-mm-dd]*
* server.log

(WebLogic) 도메인 로그 파일은 `[appserverdomain]` 디렉터리에 있고 서버 로그 파일은 `[appserverdomain]/servers/[appserver name]/logs` 디렉터리에 있습니다.

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) 다음과 같은 로그 파일은 `[appserver root]/profiles/default/logs/[appserver name]` 디렉터리에 있습니다.

* SystemErr.log
* SystemOut.log
* StartServer.log
