---
title: AEM SDK을 다시 시작하는 방법
description: AEM SDK을 다시 시작하는 우수 사례
role: Admin, Developer, User
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
solution: Experience Manager, Experience Manager Forms
hide: true
hidefromtoc: true
exl-id: 68935045-89b1-4219-b111-88a4600200df
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# AEM SDK 다시 시작

Java™ 프로세스를 중지한 후 AEM SDK을 다시 시작하면 가 AEM 개발 환경에서 일치하지 않아 다음과 같은 오류가 발생할 수 있습니다.

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![다시 시작-aem-sdk-error](/help/forms/using/assets/restart-sdk-error.png)

## 솔루션

AEM SDK을 다시 시작하려면 활성 명령 창으로 이동하여 `Ctrl + C` 명령을 눌러 SDK을 다시 시작합니다.

SDK을 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. 대체 방법(예: Java™ 프로세스 중지)을 사용하여 AEM SDK을 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.
