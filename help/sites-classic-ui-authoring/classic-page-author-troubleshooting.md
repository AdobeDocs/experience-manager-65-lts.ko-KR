---
title: 작성 시의 AEM 문제 해결
description: 다음 섹션에서는 AEM 사용 시 발생할 수 있는 문제들과 이러한 문제의 해결 방법에 대한 제안 사항을 다룹니다.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: be4397d1-0680-4b44-bdd2-825b521a44d6
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 34%

---

# 작성 시의 AEM 문제 해결{#troubleshooting-aem-when-authoring}

다음 섹션에서는 AEM 사용 시 발생할 수 있는 문제들과 이러한 문제의 해결 방법에 대한 제안 사항을 다룹니다.

>[!NOTE]
>
>문제가 발생하면 인스턴스(릴리스 및 서비스 팩)에 대한 [알려진 문제](/help/release-notes/release-notes.md) 목록을 확인하는 것도 좋습니다.

>[!NOTE]
>
>관리자 권한이 있고 AEM 문제를 해결하려는 사용자는 [AEM 문제 해결(관리자용)](/help/sites-administering/troubleshoot.md)에 설명된 문제 해결 방법을 사용할 수 있습니다. 충분한 권한이 없는 경우 시스템 관리자에게 AEM 문제 해결에 대해 문의하십시오.

## 게시된 사이트에 이전 페이지 버전이 여전히 있음 {#old-page-version-still-on-published-site}

* **문제**:

   * 페이지를 변경하고 페이지를 게시 사이트에 복제했지만, 페이지의 *이전* 버전이 여전히 게시 사이트에 표시되고 있습니다.

* **이유**:

   * 이는 때로 복제 큐 문제일 수 있지만 몇 가지 원인이 있을 수 있고 대개는 캐시 문제일 수 있습니다(로컬 브라우저나 디스패처 중 하나).

* **솔루션**:

   * 여기에는 다양한 가능성이 있습니다.
   * 페이지가 올바르게 복제되었는지 확인합니다. 페이지 상태를 확인하고 필요한 경우 복제 큐의 상태를 확인합니다.
   * 로컬 브라우저의 캐시를 지우고 다시 페이지에 액세스합니다.
   * 페이지 URL의 끝에 `?`를 추가합니다. 예:

     `http://localhost:4502/sites.html/content?`

     이렇게 하면 페이지가 AEM에서 바로 요청되고 디스패처가 무시됩니다. 업데이트된 페이지가 표시되면 이는 디스패처 캐시를 지우라는 의미입니다.

   * 복제 큐 문제가 있을 경우 시스템 관리자에게 문의하십시오.

## Sidekick이 표시되지 않음 {#sidekick-not-visible}

* **문제**:

   * 작성 환경에서 컨텐츠 페이지를 편집할 때 Sidekick이 표시되지 않습니다.

* **이유**:

   * 드물게 현재 창의 범위 밖에 사이드 킥의 헤더를 배치했을 수 있습니다. 다시 위치를 변경할 수 없음을 의미합니다.

* **솔루션**:

   * 현재 세션에서 로그아웃하고 다시 로그인합니다. Sidekick이 기본 위치로 돌아갑니다.

## 찾기 및 바꾸기 - 일부 인스턴스는 바뀌지 않음 {#find-replace-not-all-instances-are-replaced}

* **문제:**

   * **찾기 및 바꾸기** 옵션을 사용하면 `find` 용어의 일부 인스턴스가 페이지에서 바뀌지 않을 수 있습니다.

* **이유**:

   * **찾기 및 바꾸기**&#x200B;의 기능은 콘텐츠 저장 방법과 검색 가능 여부에 따라 달라집니다. 예를 들어 블로그 텍스트는 검색이 구성되지 않은 `jcr:text` 속성에 저장됩니다. 찾기 및 바꾸기 서블릿의 기본 범위는 다음 속성을 포함합니다.

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **솔루션**:

   * 이러한 정의는 **웹 콘솔**&#x200B;을 사용하여 **일 CQ WCM 찾기 대체 서블릿**&#x200B;에 대한 구성으로 변경할 수 있습니다. 예:

     `http://localhost:4502/system/console/configMgr`
