---
title: Java Content Repository에 있는 노드의 이름 지정 규칙
description: 저장소의 노드는 Java Content Repository의 이름 지정 규칙에 따릅니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 36025dac-890e-45ba-adea-a230a5231a0b
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# 이름 지정 규칙 {#naming-conventions}

저장소의 노드는 [Java 콘텐츠 저장소](/help/sites-developing/the-basics.md#java-content-repository)의 이름 지정 규칙을 따릅니다. 하지만 AEM은 페이지 노드 이름에 대한 추가 규칙을 지정합니다.

## 페이지 이름 지정 규칙 {#naming-conventions-for-pages}

이러한 이름 지정 규칙은 다양한 수준에서 구현됩니다.

* JcrUtil: [JCR 유틸리티](#jcr-utilities)의 AEM 구현입니다.
* PageManager: [페이지 관리자](#page-manager)에서 페이지 수준 작업을 위한 메서드를 제공합니다.
* 사용 중인 UI에 따라:

   * [표준, 터치 지원 UI](#standard-ui)
   * [클래식 UI](#classic-ui)

### JCR 유틸리티 {#jcr-utilities}

[JcrUtil](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html)은(는) JCR 유틸리티의 AEM 구현입니다. 이름 확인에 특히 중요한 것은 이 변수가 제어하는 문자 매핑과 다음 유효성 검사입니다.

* `isValidName`

   * 이름이 비어 있지 않고 유효한 문자만 포함되어 있는지 확인합니다.
   * 제안된 이름이 유효한지 여부를 확인하는 데 사용할 수 있습니다.

* `createValidName`

   * 이렇게 하면 임의의 문자열에서 유효한 레이블이 만들어집니다.
   * 제목에서 이름을 만드는 데 사용할 수 있습니다.

### 페이지 관리자 {#page-manager}

[PageManager](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageManager.html)은(는) [JCRUtil](#jcr-utilities)을(를) 기반으로 페이지 수준 작업에 대한 메서드를 제공합니다.

### 표준 UI {#standard-ui}

터치 사용이 가능한 표준 UI는 다음과 같습니다.

* 다음 경우 PageManager에서 지정한 제한에 따라 이름의 유효성을 검사합니다.

   * 노드 이름으로 변환하기 위한 페이지 제목이 제공됩니다.
   * 명시적인 노드 이름이 입력되었습니다.

### 클래식 UI {#classic-ui}

클래식 UI는 더 엄격한 제한을 적용합니다.

* 명시적인 노드 이름일 때 다음 경우에 이름의 유효성을 검사합니다.

   * 노드 이름으로 변환하기 위한 페이지 제목이 제공됩니다.
   * 명시적인 노드 이름이 입력되었습니다.

* 유효한 문자(이 문자만 클래식 UI에서 페이지를 만들 경우 `PageManagerImpl`에서 추가 문자를 허용하더라도 실제로 유효함):

   * &#39;a&#39;에서 &#39;z&#39;로
   * &#39;A&#39;에서 &#39;Z&#39;로
   * &#39;0&#39;에서 &#39;9&#39;
   * _(밑줄)
   * `-`(대시/빼기)
