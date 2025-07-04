---
title: 개발자 모드
description: 개발자 모드에서는 현재 페이지에 대한 정보를 개발자에게 제공하는 몇 가지 탭이 있는 사이드 패널이 열립니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: b30bb90b-adca-4d3a-ae15-bede70e1c39a
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 3%

---

# 개발자 모드{#developer-mode}

Adobe Experience Manager(AEM)에서 페이지를 편집할 때 개발자 모드를 비롯한 여러 [모드](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui)를 사용할 수 있습니다. 이렇게 하면 개발자에게 현재 페이지에 대한 정보를 제공하는 몇 가지 탭이 있는 사이드 패널이 열립니다. 세 개의 탭은 다음과 같습니다.

* 구조 및 성능 정보를 볼 수 있는 **[구성 요소](#components)**.
* 테스트 실행 및 결과 분석을 위한 **[테스트](#tests)**.
* 발생하는 모든 문제를 보려면 **[오류](#errors)**&#x200B;를 확인하십시오.

이렇게 하면 개발자가 다음과 같은 작업을 수행할 수 있습니다.

* 검색: 어떤 페이지로 구성되어 있는지 알아보십시오.
* 디버그: 언제 어디서 발생하는지 파악하여 문제 해결에 도움이 됩니다.
* 테스트: 애플리케이션이 예상대로 작동합니까?

>[!CAUTION]
>
>개발자 모드:
>
>* 터치 지원 UI에서만 사용할 수 있습니다(페이지를 편집할 때).
>* 공간 제약으로 인해 데스크톱의 작은 창이나 모바일 장치에서는 사용할 수 없습니다.
>
>   * 이 문제는 너비가 1024px 미만일 때 발생합니다.
>* `administrators` 그룹의 멤버인 사용자만 사용할 수 있습니다.

>[!CAUTION]
>
>개발자 모드는 nosamplecontent 실행 모드를 사용하지 않는 표준 작성자 인스턴스에서만 사용할 수 있습니다.
>
>필요한 경우 사용하도록 구성할 수 있습니다.
>
>* nosamplecontent 실행 모드를 사용하는 작성자 인스턴스에서
>* 게시 인스턴스
>
>사용 후 다시 비활성화해야 합니다.

>[!NOTE]
>
>다음을 참조하십시오.
>
>* 기술 자료 문서, [AEM TouchUI 문제 해결](https://experienceleague.adobe.com/ko/docs/experience-cloud-kcs/kbarticles/ka-16935)을 참조하십시오.
>* [AEM 6.0 개발자 모드](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2014/aem-developer-mode.html?lang=ko)에 대한 AEM Gems 세션.
>

## 개발자 모드 열기 {#opening-developer-mode}

개발자 모드는 페이지 편집기의 사이드 패널로 구현됩니다. 패널을 열려면 페이지 편집기의 도구 모음에 있는 모드 선택기에서 **개발자**&#x200B;를 선택합니다.

![chlimage_1-11](assets/chlimage_1-11.png)

패널은 두 개의 탭으로 나뉘어 있습니다.

* **[구성 요소](/help/sites-developing/developer-mode.md#components)** - 작성자의 [콘텐츠 트리](/help/sites-authoring/author-environment-tools.md#content-tree)와(과) 유사한 구성 요소 트리를 표시합니다.

* **[오류](/help/sites-developing/developer-mode.md#errors)** - 문제가 발생하면 각 구성 요소에 대한 세부 정보가 표시됩니다.

### 구성 요소 {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

이 구성 요소 트리는 다음과 같습니다.

* 페이지에 렌더링된 구성 요소 체인 및 템플릿(SLY, JSP 등)에 대해 설명합니다. 트리를 확장하여 계층 내에 컨텍스트를 표시할 수 있습니다.
* 구성 요소를 렌더링할 서버측 계산 시간을 표시합니다.
* 트리를 확장하고 트리 내에서 특정 구성 요소를 선택할 수 있습니다. 선택 항목을 통해 다음과 같은 구성 요소 세부 정보에 액세스할 수 있습니다.

   * 저장소 경로
   * 스크립트 링크(CRXDE Lite에서 액세스)

* 선택한 구성 요소(컨텐츠 플로우에서 파란색 테두리로 표시됨)가 컨텐츠 트리에서 강조 표시됩니다(반대로 표시).

이렇게 하면 다음과 같은 이점이 있습니다.

* 구성 요소당 렌더링 시간을 결정하고 비교합니다.
* 계층 구조를 확인하고 이해합니다.
* 느린 구성 요소를 찾아 페이지 로드 시간을 이해한 다음 개선합니다.

각 구성 요소 항목은 다음을 표시할 수 있습니다(예:).

![chlimage_1-13](assets/chlimage_1-13.png)

* **세부 정보 보기**: 다음을 표시하는 목록에 대한 링크입니다.

   * 구성 요소를 렌더링하는 데 사용되는 모든 구성 요소 스크립트.
   * 특정 구성 요소에 대한 저장소 콘텐츠 경로입니다.

  ![chlimage_1-14](assets/chlimage_1-14.png)

* **스크립트 편집**: 링크:

   * CRXDE Lite에서 구성 요소 스크립트를 엽니다.

* 구성 요소 항목(화살표 헤드)을 확장하면 다음도 표시됩니다.

   * 선택한 구성 요소 내의 계층입니다.
   * 선택한 구성 요소, 그 안에 중첩된 개별 구성 요소 및 결합된 합계의 렌더링 시간.

  ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>일부 링크는 `/libs` 아래의 스크립트를 가리킵니다. 그러나 이러한 변경 내용은 참조용이므로 **은(는) `/libs`에서 어떤 것도 편집할 수 없습니다**. 변경 내용은 손실될 수 있습니다. 이는 이 분기가 핫픽스 또는 기능 팩을 업그레이드하거나 적용할 때마다 변경되기 쉽기 때문입니다. `/apps`에서 필요한 변경 작업을 수행합니다. [오버레이 및 무시](/help/sites-developing/overlays.md)를 참조하십시오.

### 오류수 {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

**오류** 탭이 위와 같이 항상 비어 있기를 바라지만, 문제가 발생하면 각 구성 요소에 대해 다음 세부 정보가 표시됩니다.

* 구성 요소가 오류 로그에 오류의 세부 정보와 함께 항목을 쓰고 CRXDE Lite 내의 적절한 코드로 직접 연결하는 경우의 경고.
* 구성 요소가 관리 세션을 여는 경우 경고 메시지가 표시됩니다.

예를 들어 정의되지 않은 메서드가 호출되는 경우 결과 오류가 **오류** 탭에 표시됩니다.

![chlimage_1-17](assets/chlimage_1-17.png)

오류가 발생하면 구성 요소 탭의 트리에 있는 구성 요소 항목에도 표시기가 표시됩니다.

### 테스트 {#tests}

>[!CAUTION]
>
>AEM 6.2에서는 개발자 모드의 테스트 기능이 독립 실행형 도구 애플리케이션으로 다시 구현되었습니다.
>
>자세한 내용은 [UI 테스트](/help/sites-developing/hobbes.md)를 참조하십시오.
