---
title: SPA 모델 라우팅
description: AEM의 단일 페이지 애플리케이션의 경우 앱이 라우팅을 담당합니다. 이 문서에서는 경로지정 메커니즘, 계약 및 사용 가능한 옵션에 대해 설명합니다.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
exl-id: 4403f563-e9c7-4693-9142-45e0f587a88a
index: false
source-git-commit: f6a3d16c55a6b62aea9a374904339e16d30f0a75
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# SPA 모델 라우팅{#spa-model-routing}

AEM의 단일 페이지 애플리케이션의 경우 앱이 라우팅을 담당합니다. 이 문서에서는 경로지정 메커니즘, 계약 및 사용 가능한 옵션에 대해 설명합니다.

{{ue-over-spa}}

## 프로젝트 라우팅 {#project-routing}

앱은 라우팅을 소유하며 프로젝트 프론트엔드 개발자에 의해 구현됩니다. 이 문서에서는 AEM 서버에서 반환된 모델과 관련된 라우팅에 대해 설명합니다. 페이지 모델 데이터 구조는 기본 리소스의 URL을 노출합니다. 프론트엔드 프로젝트는 라우팅 기능을 제공하는 모든 사용자 지정 또는 서드파티 라이브러리를 사용할 수 있습니다. 경로에 모델 조각이 있으면 `PageModelManager.getData()` 함수를 호출할 수 있습니다. 모델 경로가 변경된 경우 페이지 편집기와 같은 수신 라이브러리를 경고하기 위해 이벤트를 트리거해야 합니다.

## 아키텍처 {#architecture}

자세한 설명은 SPA 블루프린트 문서의 [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 섹션을 참조하십시오.

## 모델 라우터 {#modelrouter}

`ModelRouter` - 활성화된 경우 - HTML5 기록 API 함수 `pushState` 및 `replaceState`을(를) 캡슐화하여 모델의 지정된 조각을 미리 가져오고 액세스할 수 있도록 합니다. 그런 다음 등록된 프런트엔드 구성 요소에 모델이 수정되었음을 알립니다.

## 수동 및 자동 모델 라우팅 {#manual-vs-automatic-model-routing}

`ModelRouter`은(는) 모델 조각의 가져오기를 자동화합니다. 그러나 모든 자동화된 툴은 제한 사항이 있습니다. 필요한 경우 메타 속성을 사용하여 경로를 무시하도록 `ModelRouter`을(를) 비활성화하거나 구성할 수 있습니다([SPA 페이지 구성 요소](/help/sites-developing/spa-page-component.md) 문서의 메타 속성 섹션 참조). 그러면 프론트엔드 개발자는 `getData()` 함수를 사용하여 지정된 모델의 조각을 로드하도록 `PageModelManager`에 요청하여 자체 모델 라우팅 계층을 구현할 수 있습니다.

>[!NOTE]
>
>[We.Retail 저널](https://github.com/adobe/aem-sample-we-retail-journal) 샘플 React 프로젝트는 자동화된 접근 방식을 보여 주고 Angular 프로젝트는 수동 접근 방식을 보여 줍니다. 반자동화된 접근 방식 또한 유효한 사용 사례일 것입니다.

>[!CAUTION]
>
>`ModelRouter`의 현재 버전에서는 Sling 모델 진입점의 실제 리소스 경로를 가리키는 URL만 사용할 수 있습니다. Vanity URL 또는 별칭의 사용을 지원하지 않습니다.

## 라우팅 계약 {#routing-contract}

현재 구현은 SPA 프로젝트가 다른 애플리케이션 페이지로 라우팅하기 위해 HTML5 내역 API를 사용한다는 가정을 기반으로 합니다.

### 구성 {#configuration}

`ModelRouter`은(는) 모델 조각 미리 가져오기에 대한 `pushState` 및 `replaceState` 호출을 수신하므로 모델 라우팅 개념을 지원합니다. 내부적으로 `PageModelManager`을(를) 트리거하여 지정된 URL에 해당하는 모델을 로드하고 다른 모듈이 수신할 수 있는 `cq-pagemodel-route-changed` 이벤트를 실행합니다.

기본적으로 이 동작은 자동으로 활성화됩니다. 비활성화하려면 SPA에서 다음 메타 속성을 렌더링해야 합니다.

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

`PageModelManager`이(가) 경로를 선택하면 해당 페이지 모델을 자동으로 로드하기 때문에 SPA의 모든 경로는 AEM에서 액세스 가능한 리소스(예: &quot; `/content/mysite/mypage"`)에 해당해야 합니다. 그러나 필요한 경우 SPA는 `PageModelManager`에서 무시해야 하는 경로의 &quot;차단 목록&quot;도 정의할 수 있습니다.

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
