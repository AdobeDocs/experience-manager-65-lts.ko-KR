---
title: 에셋 테스트를 위한 이름 지정 규칙
description: 저장소의 노드는 Java Content Repository의 이름 지정 규칙에 따릅니다. 하지만 Adobe Experience Manager은 에셋 노드의 이름에 대한 추가 규칙을 지정합니다.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 37de1a8b-b7db-469e-98a7-20ddb6218510
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 1%

---

# 에셋 테스트를 위한 이름 지정 규칙{#naming-conventions-for-assets-testing}

저장소의 노드는 [Java 콘텐츠 저장소](/help/sites-developing/the-basics.md#java-content-repository)의 이름 지정 규칙을 따릅니다. 하지만 Adobe Experience Manager은 에셋 노드의 이름에 대한 추가 규칙을 지정합니다.

## 클래식 UI {#classic-ui}

클래식 UI는 더 엄격한 제한을 적용합니다.

* 명시적 노드 이름이 다음 중 하나에 해당할 경우 자산 이름을 확인합니다.

   * 노드 이름으로 변환하기 위한 자산 제목이 제공됩니다.
   * 명시적인 노드 이름이 입력되었습니다.

* 유효한 문자(이 문자만 클래식 UI 내에서 에셋을 만드는 경우 실제로 유효함):

   * &#39;a&#39;에서 &#39;z&#39;로
   * &#39;A&#39;에서 &#39;Z&#39;로
   * &#39;0&#39;에서 &#39;9&#39;
   * _(밑줄)
   * `-`(대시/빼기)
