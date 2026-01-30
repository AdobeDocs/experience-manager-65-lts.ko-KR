---
title: We.Retail 참조 구현
description: We.Retail은 AEM을 사용하여 온라인 상태를 설정하는 권장 방법을 보여 주는 참조 구현의 기술 미리 보기입니다
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 71a49353-5273-46ee-a1ff-5bbfe5b6b0b4
source-git-commit: c0bf6864bb344e582c4f88371c892d401ce2827c
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 9%

---

# `We.Retail` 참조 구현{#we-retail-reference-implementation}

## 소개 {#introduction}

`We.Retail` 페이지는 Adobe Experience Manager을 사용하여 온라인 상태를 설정하는 권장 방법을 보여 주는 참조 구현 및 샘플 콘텐츠입니다.

`We.Retail` 사이트는 HTL, 응답형 레이아웃, 편집 가능한 템플릿, 핵심 구성 요소 등과 같은 최신 Adobe Experience Manager(AEM) 기술을 사용합니다.

이 안내서는 소매 카테고리를 보여 주지만 사이트 설정 방법은 모든 카테고리에 적용할 수 있으며 제품 카탈로그와 장바구니 기능만 소매에 따라 다릅니다.

## 기능 {#features}

AEM의 표준 참조 구현으로 `We.Retail`은(는) AEM의 가장 강력한 기능 중 일부를 보여 줍니다.

| **기능** | **설명** | **관심 항목** |
|---|---|---|
| [전역 사이트 구조](/help/sites-administering/tc-bp.md) | `We.Retail`에는 국가별 사이트로 실시간 복사되는 기본 언어 페이지가 포함되어 있습니다. | [사용해 보세요!](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [응답형 레이아웃](/help/sites-authoring/responsive-layout.md) | 모든 페이지에는 화면 및 장치 크기에 맞게 동적으로 조정되는 반응형 레이아웃이 있습니다. | [사용해 보세요!](/help/sites-developing/we-retail-responsive-layout.md) |
| [편집 가능한 템플릿](/help/sites-developing/page-templates-editable.md) | 모든 페이지는 편집 가능한 템플릿을 기반으로 하므로 개발자가 아닌 사용자도 템플릿을 조정하고 맞춤화할 수 있습니다. | [사용해 보세요!](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML Template Language](https://experienceleague.adobe.com/ko/docs/experience-manager-htl/content/overview) | 모든 구성 요소는 HTL을 기반으로 합니다. |  |
| [핵심 구성 요소](https://experienceleague.adobe.com/ko/docs/experience-manager-core-components/using/introduction) | 모든 구성 요소는 새로운 핵심 구성 요소를 기반으로 하며, 보다 유용하고 즉시 구성 가능한 구성 요소입니다 | [사용해 보세요!](/help/sites-developing/we-retail-core-components.md) |
| [콘텐츠 조각](/help/assets/content-fragments/content-fragments.md) | `We.Retail` 경험 섹션은 콘텐츠 조각을 통해 콘텐츠를 재사용하는 기능을 보여 줍니다. | [사용해 보세요!](/help/sites-developing/we-retail-content-fragments.md) |
| [경험 조각](/help/sites-authoring/experience-fragments.md) | 경험 조각 은 페이지 내에서 참조할 수 있는 컨텐츠 및 레이아웃을 포함한 하나 이상의 구성 요소 그룹입니다. | [사용해 보세요!](/help/sites-developing/we-retail-experience-fragments.md) |

## 시작하기 {#getting-started}

`We.Retail` 사이트는 AEM의 샘플 콘텐츠로 제공됩니다. 사용하려면 [일반적인 방법으로 AEM을 시작](/help/sites-deploying/deploy.md#getting-started)하여 샘플 콘텐츠가 비활성화되지 않았는지 확인하세요.

>[!CAUTION]
>
>프로덕션 인스턴스에 `We.Retail`을(를) 설치하지 마십시오. 프로덕션 인스턴스는 `nosamplecontent` [실행 모드](/help/sites-deploying/configure-runmodes.md)에서 시작해야 합니다.

>[!CAUTION]
>
>`We.Retail` 사이트는 최신 AEM 기술을 기반으로 하므로 [클래식 UI 작성](/help/sites-classic-ui-authoring/classic-page-author-first-steps.md)을 지원하지 않습니다.

### 최신 버전 {#latest-version}

`We.Retail`이(가) AEM 릴리스와 함께 배포되었지만 릴리스 이후에 콘텐츠 및 해당 기능에 대한 업데이트가 수행될 수 있습니다. 따라서 GitHub에서 최신 릴리스를 [다운로드](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)한 다음 AEM 인스턴스에서 패키지로 [업로드](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) 및 [설치](/help/sites-administering/package-manager.md#installing-packages)할 수 있습니다.

### 첫 단계 {#first-steps}

1. AEM이 시작되거나 `We.Retail`이(가) 설치되면 **`We.Retail`**&#x200B;사이트 콘솔[에서 &#x200B;](/help/sites-authoring/basic-handling.md#global-navigation) 사이트를 사용할 수 있습니다.
1. 예를 들어 다음 페이지를 열 수 있으며 아래 [부록](#appendix)에 표시된 것과 같이 표시되어야 합니다.

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## `We.Retail` 및 Geometrixx {#we-retail-geometrixx}

Geometrixx 및 그 많은 화신들은 이전 버전의 AEM에서 샘플 콘텐츠로 제공되었습니다. 버전 6.3 이후 `We.Retail`은(는) AEM과 함께 제공되는 샘플 콘텐츠였으며 새로운 표준 참조 구현의 역할을 합니다.

`We.Retail` 사이트는 기술적으로 더 강력하며 최신 AEM 기술을 활용하여 보다 유연하고 확장 가능한 동시에 제품의 최신 기능을 시연합니다.

### 기능 비교 {#feature-comparison}

다음 표는 Geometrixx과 비교하여 `We.Retail`에서 사용할 수 있는 주요 기능에 대한 개요를 제공합니다.

* **사용 가능**&#x200B;은(는) 기능의 예가 샘플 콘텐츠에서 발견되었음을 의미합니다.
* **사용할 수 없음**&#x200B;은(는) 샘플 콘텐츠에 기능 예가 없음을 의미하지만 기능을 계속 사용할 수 있습니다.


| **기능** | **`We.Retail`** | **Geometrixx** |
|---|---|---|
| 세계화된 부위 구조 | 기본 언어 페이지는 국가별 사이트에 라이브 복사됩니다 | 사용할 수 없음 |
| 콘텐츠 조각 | 사용 가능 | 사용할 수 없음 |
| 경험 조각 | 사용 가능 | 사용할 수 없음 |
| 반응형 레이아웃 | 모든 페이지의 경우 | Geometrixx Media만 |
| 편집 가능한 템플릿 | 모든 페이지의 경우 | 사용할 수 없음 |
| HTL | 모든 구성 요소 | 제한적 |
| 타기팅 | 모든 페이지의 경우 | Geometrixx Outdoors만 |
| 원고 | 사용할 수 없음 | 사용 가능 |
| 슬라이드 뷰어, 다운로드 및 차트 구성 요소 | 사용할 수 없음 | 사용 가능 |
| 열 컨트롤 | 레이아웃 컨테이너로 대체됨 | 사용 가능 |
| 양식 | 사용할 수 없음 | 사용 가능 |
| 캠페인 | 이메일 샘플 없음 | 사용 가능 |

>[!NOTE]
>
>이 목록은 완전하기 위해 노력하지만, 완전한 것으로 간주되어서는 안 됩니다.

## 참여 {#contribute}

`We.Retail` 사이트는 오픈 소스 프로젝트로 릴리스되고 GitHub에서 최신 버전의 소스 코드를 다운로드할 수 있습니다.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 확인할 수 있습니다.

* [GitHub에서 aem-sample-we-retail 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* 프로젝트를 [ZIP 파일](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/zip/refs/heads/master)&#x200B;(으)로 다운로드

최신 릴리스는 설치 가능한 패키지로 [직접 다운로드](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/tag/we.retail.reactor-4.0.0)할 수도 있습니다.

문제가 발생하면 [GitHub 문제](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues)를 제출하세요.

포크하거나 [가져오기 요청](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls)에 참여하세요.

## 미리보기 {#preview}

`We.Retail` 시작 페이지 미리 보기:

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
