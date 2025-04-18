---
title: 편집기
description: 클래식 UI 편집기로 다시 전환하는 방법에 대해 알아봅니다.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 54a97ac0-db9e-4903-b395-b1af87cfd151
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---

# 편집기{#editor}

편집기에서 클래식 UI로 전환하는 기능이 기본적으로 비활성화되었습니다.

**페이지 정보** 메뉴에서 **클래식 UI에서 열기** 옵션을 다시 사용하려면 다음 단계를 따르십시오.

1. CRXDE Lite을 사용하여 다음 노드를 찾습니다.

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   예

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. **오버레이 노드** 옵션을 사용하여 오버레이를 만듭니다. 예:

   * **경로**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **오버레이 위치**: `/apps/`
   * **노드 유형 일치**: 활성(확인란 선택)

1. 중첩된 노드에 다음 다중 값 텍스트 속성을 추가합니다.

   `sling:hideProperties = ["granite:hidden"]`

1. 페이지를 편집할 때 **페이지 정보** 메뉴에서 **클래식 UI에서 열기** 옵션을 다시 사용할 수 있습니다.

   ![페이지 정보에서 클래식 UI로 열기 옵션](assets/syui-03-2019-02-27-15-19-48.png)
