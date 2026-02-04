---
title: 프로그래밍 방식으로 PreferencesNodes 관리
description: Java(Preferences Manager Service API)를 사용하여 프로그래밍 방식으로 기본 설정 노드를 관리합니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 95a83858-c0b7-4c68-b4a9-d525bfc663c0
source-git-commit: 51342861dd01e659999c19fbe0274e8d3cbcf8c4
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 2%

---

# 프로그래밍 방식으로 환경 설정 노드 관리 {#programmatically-managing-the-preferencesnodes}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

이 항목에서는 기본 설정 관리자 서비스 API(Java)를 사용하여 기본 설정 노드를 프로그래밍 방식으로 관리하는 방법을 설명합니다.

관리자 UI에서 구성 설정을 수동으로 변경할 수 있습니다. 옵션을 변경하려면 `Home>Settings>User Management> Configuration>Manual Configuration`(으)로 이동합니다. 변경 후 `config.xml`을(를) 가져오면 `/Adobe/Adobe Experience Manager Forms/Config/UM persist` 노드에서 변경한 내용을 제외한 모든 변경 내용이 손실됩니다. 사용자 관리 가져오기 및 내보내기 미리 보기는 다른 구성 요소에 대한 구성 설정 변경을 지원하지 않습니다. 이제 `PreferencesManagerServiceClient` API를 사용하여 이러한 변경 작업을 수행할 수 있습니다.

**단계 요약**
기본 설정 노드를 프로그래밍 방식으로 관리하려면 다음을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. `PreferencesManagerService` 클라이언트를 만듭니다.
1. 적절한 역할 또는 권한 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 생성하는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**클라이언트 `PreferencesManagerService`개 만들기**

User Management `PreferencesManagerService` 작업을 프로그래밍 방식으로 수행하려면 먼저 `PreferencesManagerService` 클라이언트를 만들어야 합니다. Java API를 사용하여 `PreferencesManagerServiceClient` 개체를 만듭니다.

**적절한 역할 또는 권한 작업을 호출합니다**

서비스 클라이언트를 만들면 기본 설정 관리자 작업을 호출할 수 있습니다. 서비스 클라이언트를 사용하여 권한을 읽고 설정할 수 있습니다.
