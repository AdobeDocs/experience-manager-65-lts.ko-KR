---
title: 구성 요소에 대해 JSON 내보내기 활성화
description: 구성 요소는 모델러 프레임워크를 기반으로 콘텐츠의 JSON 내보내기를 생성하도록 조정할 수 있습니다.
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: aeb8e954-dd6c-4e18-bb78-6eaac86fa4b9
source-git-commit: cc96a14ebaf9f895a798b5f4904f5b4769b990bb
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 4%

---

# 구성 요소에 대해 JSON 내보내기 활성화{#enabling-json-export-for-a-component}

구성 요소는 모델러 프레임워크를 기반으로 콘텐츠의 JSON 내보내기를 생성하도록 조정할 수 있습니다.

## 개요 {#overview}

JSON 내보내기는 [Sling 모델](https://sling.apache.org/documentation/bundles/models.html) 및 [Sling 모델 내보내기](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 프레임워크([Jackson 주석](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)에 의존)를 기반으로 합니다.

이 접근 방식은 구성 요소에 JSON을 내보내야 하는 경우 슬링 모델이 있어야 함을 의미합니다. 따라서 구성 요소에서 JSON 내보내기를 활성화하려면 다음 두 단계를 따르십시오.

* [구성 요소의 슬링 모델 정의](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Sling 모델 인터페이스에 주석 달기](#annotate-the-sling-model-interface)

## 구성 요소의 슬링 모델 정의 {#define-a-sling-model-for-the-component}

먼저 구성 요소에 대해 슬링 모델 을 정의해야 합니다.

>[!NOTE]
>
>Sling 모델을 사용하는 예는 [AEM에서 Sling 모델 내보내기 개발](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter)을 참조하십시오.

Sling 모델 구현 클래스에는 다음 주석이 포함되어야 합니다.

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

이렇게 하면 `.model` 선택기와 `.json` 확장을 사용하여 구성 요소를 직접 내보낼 수 있습니다.

또한 Sling Model 클래스를 `ComponentExporter` 인터페이스에 적용할 수 있도록 지정합니다.

>[!NOTE]
>
>Jackson 주석은 슬링 모델 클래스 수준에서 지정되지 않고 모델 인터페이스 수준에서 지정됩니다. 이 접근 방식은 JSON 내보내기가 구성 요소 API의 일부로 간주되도록 하기 위한 것입니다.

>[!NOTE]
>
>`ExporterConstants` 및 `ComponentExporter` 클래스는 `com.adobe.cq.export.json` 번들에서 가져옵니다.

### 여러 선택기 사용 {#multiple-selectors}

표준 사용 사례는 아니지만 `model` 선택기 외에 여러 선택기를 구성할 수 있습니다.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

그러나 이 경우 `model` 선택기는 첫 번째 선택기여야 하며 확장은 `.json`이어야 합니다.

## Sling 모델 인터페이스에 주석 달기 {#annotate-the-sling-model-interface}

JSON 내보내기 프레임워크에서 이를 처리하려면 모델 인터페이스가 `ComponentExporter` 인터페이스(또는 컨테이너 구성 요소의 경우 `ContainerExporter`)를 구현해야 합니다.

그런 다음 해당 Sling 모델 인터페이스(`MyComponent`)에 [Jackson 주석](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)을 사용하여 주석을 달아 내보내는(직렬화하는) 방법을 정의합니다.

serialize되는 메서드를 정의하려면 모델 인터페이스에 적절한 주석을 추가해야 합니다. 기본적으로 getter에 대한 일반적인 명명 규칙을 준수하는 모든 메서드는 serialize되며 getter 이름에서 자연스럽게 JSON 속성 이름을 파생합니다. 이 접근 방식은 `@JsonIgnore` 또는 `@JsonProperty`을(를) 사용하여 JSON 속성의 이름을 바꾸는 것을 방지하거나 재정의할 수 있습니다.

## 예 {#example}

핵심 구성 요소는 핵심 구성 요소[의 릴리스 ](https://experienceleague.adobe.com/ko/docs/experience-manager-core-components/using/introduction)1.1.0 이후 JSON 내보내기를 지원했으며 참조로 사용할 수 있습니다.

예를 들어 이미지 핵심 구성 요소의 슬링 모델 구현 및 주석이 달린 인터페이스를 참조하십시오.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 확인할 수 있습니다

* [GitHub에서 aem-core-wcm-components 프로젝트 열기](https://github.com/adobe/aem-core-wcm-components)
* 프로젝트를 [ZIP 파일](https://codeload.github.com/adobe/aem-core-wcm-components/zip/main)&#x200B;(으)로 다운로드


## 관련 설명서 {#related-documentation}

* Assets 사용 안내서의 [콘텐츠 조각 항목](https://experienceleague.adobe.com/en/docs/experience-manager-64/assets/home#)
* [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)
* [컨텐츠 조각으로 작성](/help/sites-authoring/content-fragments.md)
* [콘텐츠 서비스를 위한 JSON 내보내기 도구](/help/sites-developing/json-exporter.md)
* [핵심 구성 요소](https://experienceleague.adobe.com/ko/docs/experience-manager-core-components/using/introduction) 및 [콘텐츠 조각 구성 요소](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/content-fragment-component)
