---
title: '서신 관리: 문제 해결'
description: AEM Forms 환경에서 편지를 저장하는 프로세스 중에 발생하는 오류를 처리하는 방법에 대해 알아봅니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 57794b13-471b-4aae-aa57-ddfc2dfc58c9
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 1%

---

# 서신 관리: 문제 해결 {#correspondence-management-troubleshooting}

## 편지 저장 시 오류 발생 {#errors-when-saving-a-letter}

### 문제 {#issue}

편지를 저장할 때 다음 오류 중 하나가 표시됩니다.

* 텍스트 모듈에 대한 데이터 바인딩이 없습니다.
* 다음에 필요한 속성 정보 제공

### 이유 {#reason}

이러한 오류는 다음 중 하나로 인해 발생할 수 있습니다.

* 데이터 사전이 편지에 바인딩되어 있지만 서버에 없습니다.
* 데이터 사전은 편지에 바인딩되어 있지만 이름에 밑줄(_)이 있습니다.

### 해결 방법 {#workaround}

편지에서 사용 중인 데이터 사전이 서버에 있고 이름에 밑줄(_)이 없는지 확인합니다.

## 편지 미리 보기 시 오류 발생 {#error-when-previewing-a-letter}

### 문제 {#issue-1}

문자를 미리 보는 동안 편지에서 이전에 게시되지 않은 텍스트 자산이 게시되는 경우에도 &quot;편지 로드 오류: XML 입력에서 자산을 가져올 수 없습니다&quot; 오류가 표시됩니다.

### 해결 방법 {#workaround-1}

다음 단계를 사용하여 게시 인스턴스에서 편지 캐시를 재설정한 다음 편지 보기를 다시 시도하십시오.

1. **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`**(으)로 이동한 다음 관리자로 로그인합니다.
1. **서신 관리 구성**&#x200B;을 선택하십시오.
1. **서신 관리 구성**&#x200B;에서 **편지 캐시 사용**&#x200B;을 비활성화한 다음 **저장을 클릭하세요.**
1. **편지 캐시 사용**&#x200B;을 선택한 다음 **저장**&#x200B;을 클릭합니다.
1. 편지 보기를 다시 시도하십시오.
