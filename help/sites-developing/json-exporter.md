---
title: 콘텐츠 서비스를 위한 JSON 내보내기 도구
description: AEM Content Services는 웹 페이지에 초점을 두지 않고 AEM에서 컨텐츠 설명 및 게재를 일반화하기 위해 디자인되었습니다. 모든 클라이언트가 사용할 수 있는 표준화된 방법을 사용하여 기존 AEM 웹 페이지가 아닌 채널에 콘텐츠를 게재할 수 있습니다.
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 8c66b978-872e-4f5e-8f64-1e2dfb7d7dde
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 24%

---

# 콘텐츠 서비스를 위한 JSON 내보내기 도구{#json-exporter-for-content-services}

AEM Content Services는 웹 페이지에 초점을 두지 않고 AEM에서 콘텐츠 설명 및 게재를 일반화하기 위해 디자인되었습니다.

모든 클라이언트가 사용할 수 있는 표준화된 방법을 사용하여 기존 AEM 웹 페이지가 아닌 채널에 콘텐츠를 게재할 수 있습니다. 이러한 채널에는 다음과 같은 것들이 포함될 수 있습니다.

* [SPA (Single Page Applications)](spa-walkthrough.md)
* 기본 모바일 애플리케이션
* AEM 외부에 있는 기타 채널 및 터치포인트

구조화된 콘텐츠를 사용하는 콘텐츠 조각을 사용하면 JSON 익스포터를 사용하여 AEM 페이지의 콘텐츠를 JSON 데이터 모델 형식으로 전달하여 콘텐츠 서비스를 제공할 수 있습니다. 그런 다음 자체 애플리케이션에서 이 메서드를 사용할 수 있습니다.

>[!NOTE]
>
>여기에 설명된 기능은 [핵심 구성 요소 릴리스 1.1.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ko) 이후 모든 핵심 구성 요소에 사용할 수 있습니다.

## 콘텐츠 조각 핵심 구성 요소가 있는 JSON 내보내기 {#json-exporter-with-content-fragment-core-components}

AEM JSON Exporter를 사용하여 모든 AEM 페이지의 콘텐츠를 JSON 데이터 모델 형식으로 제공할 수 있습니다. 그런 다음 자체 애플리케이션에서 이 메서드를 사용할 수 있습니다.

AEM 내에서 선택기 `model` 및 `.json` 확장을 사용하여 게재를 수행합니다.

`.model.json`

1. 예를 들어 다음과 같은 URL:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. 다음과 같은 콘텐츠 제공:

   ![chlimage_1-192](assets/chlimage_1-192.png)

또는 구조화된 컨텐츠 조각의 컨텐츠를 구체적으로 타겟팅하여 전달할 수 있습니다.

조각에 대한 전체 경로(`jcr:content`에서 사용)를 사용하십시오(예: 접미사 포함).

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

페이지에는 단일 콘텐츠 조각 또는 다양한 유형의 여러 구성 요소가 포함될 수 있습니다. 목록 구성 요소와 같은 메커니즘을 사용하여 관련 콘텐츠를 자동으로 검색할 수도 있습니다.

* 예를 들어 다음과 같은 URL:

  ```shell
  http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
  ```

* 다음과 같은 콘텐츠 제공:

  ![chlimage_1-193](assets/chlimage_1-193.png)

  >[!NOTE]
  >
  >이 데이터에 액세스하고 사용하도록 [자체 구성 요소를 조정](/help/sites-developing/json-exporter-components.md)할 수 있습니다.

  >[!NOTE]
  >
  >표준 구현은 아니지만 [여러 선택기가 지원됩니다.](json-exporter-components.md#multiple-selectors) 그러나 `model`은(는) 첫 번째 선택기여야 합니다.

### 추가 정보 {#further-information}

추가 참조:

* Assets HTTP API

   * [Assets HTTP API](/help/assets/mac-api-assets.md)

* Sling 모델:

   * [Sling 모델 - 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130) 이후 모델 클래스를 리소스 유형과 연결

* JSON이 있는 AEM:

   * [JSON 형식으로 페이지 정보 가져오기](/help/sites-developing/pageinfo.md)

## 관련 설명서 {#related-documentation}

자세한 내용은 다음을 참조하십시오.

* Assets 사용 안내서의 [콘텐츠 조각 항목](/help/assets/content-fragments/content-fragments.md)

* [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)
* [컨텐츠 조각으로 작성](/help/sites-authoring/content-fragments.md)
* [구성 요소에 대해 JSON 내보내기 활성화](/help/sites-developing/json-exporter-components.md)

* [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ko) 및 [콘텐츠 조각 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=ko)
