---
title: 콘텐츠 조각 액세스 및 게재 Headless 빠른 시작 안내서
description: AEM의 Assets REST API를 사용하여 콘텐츠 조각을 관리하고, 콘텐츠 조각 콘텐츠의 Headless 전달을 위한 GraphQL API를 사용하는 방법에 대해 알아봅니다.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
exl-id: a5f7f0b9-7779-49c3-b79f-3dd3762c746a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 43%

---

# 콘텐츠 조각 액세스 및 게재 Headless 빠른 시작 안내서 {#accessing-delivering-content-fragments}

AEM Assets REST API를 사용하여 콘텐츠 조각을 관리하고, 콘텐츠 조각 콘텐츠의 Headless 전달을 위한 GraphQL API를 사용하는 방법에 대해 알아봅니다.

## GraphQL 및 Assets REST API란 무엇입니까? {#what-are-the-apis}

[일부 콘텐츠 조각을 만들었으므로](create-content-fragment.md) 이제 AEM의 API를 사용하여 Headless 방식으로 전달할 수 있습니다.

* [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)를 사용하여 콘텐츠 조각에 액세스하고 전달하기 위한 요청을 만들 수 있습니다.
   * 이 기능을 사용하려면 [끝점을 AEM에서 정의하고 활성화해야 합니다](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint). 필요한 경우 [GraphiQL 인터페이스가 설치되어야 합니다](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#installing-graphiql-interface).
* [Assets REST API](/help/assets/assets-api-content-fragments.md)를 사용하면 콘텐츠 조각(및 기타 자산)을 만들고 수정할 수 있습니다.

이 안내서의 나머지 부분에서는 GraphQL 액세스 및 콘텐츠 조각 게재에 중점을 둡니다.

## GraphQL을 사용하여 컨텐츠 조각을 전달하는 방법 {#how-to-deliver-a-content-fragment}

정보 설계자는 콘텐츠를 전달할 채널 끝점에 대한 쿼리를 설계해야 합니다. 이러한 쿼리는 엔드포인트, 모델당 한 번만 고려하십시오. 이 시작 안내서에서는 하나만 만듭니다.

1. AEM에 로그인하고 [GraphiQL 인터페이스](/help/sites-developing/headless/graphql-api/graphiql-ide.md)에 액세스합니다.
   * 예: `http://<host>:<port>/aem/graphiql.html`.

1. GraphiQL은 GraphQL용 브라우저 내 쿼리 편집기입니다. 이를 사용하여 콘텐츠 조각을 검색하여 JSON으로 원활하게 전달하는 쿼리를 작성할 수 있습니다.
   * 왼쪽 패널을 사용하여 쿼리를 작성할 수 있습니다.
   * 오른쪽 패널에 결과가 표시됩니다.
   * 쿼리 편집기는 쿼리를 쉽게 실행할 수 있는 코드 완성 기능과 단축키를 제공합니다.

     ![GraphiQL 편집기](assets/graphiql.png)

1. 만든 모델이 `firstName`, `lastName`, `position` 필드가 있는 `person`이라고 가정하면 콘텐츠 조각의 콘텐츠를 검색하는 간단한 쿼리를 작성할 수 있습니다.

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. 쿼리를 왼쪽 패널에 입력합니다.
<!--
   ![GraphiQL query](assets/graphiql-query.png)
-->

1. **쿼리 실행**(오른쪽 화살표) 아이콘을 클릭하거나 `Ctrl-Enter` 핫키를 사용하면 결과가 오른쪽 패널에 JSON으로 표시됩니다.
   ![GraphiQL 결과](assets/graphiql-results.png)

1. 클릭:
   * 페이지 오른쪽 상단의 **설명서**&#x200B;를 통해 상황에 맞는 설명서를 표시하여 자신의 모델에 맞는 쿼리를 만드는 데 도움이 됩니다.
   * 이전 쿼리를 표시하기 위해 맨 위 도구 모음의 **기록**
   * 쿼리를 저장하려면 **다른 이름으로 저장** 및 **저장**&#x200B;을 하세요. 그 후에는 **지속 쿼리** 패널 및 **게시**&#x200B;에서 쿼리를 나열하고 검색할 수 있습니다.

     ![GraphiQL 설명서](assets/graphiql-documentation.png)

GraphQL은 특정 데이터 세트 또는 개별 데이터 오브젝트를 대상으로 할 수 있을 뿐만 아니라 오브젝트의 특정 요소 및 중첩된 결과를 전달할 수 있는 구조화된 쿼리를 가능하게 하고, 쿼리 변수 등에 대한 지원을 제공합니다.

GraphQL은 반복적인 API 요청 및 초과 전달을 방지할 수 있습니다. 대신 단일 API 쿼리에 대한 응답으로 렌더링에 필요한 것을 정확히 대량으로 전달할 수 있도록 합니다. 결과 JSON은 데이터를 다른 사이트나 앱으로 전달하는 데 사용할 수 있습니다.

## 다음 단계 {#next-steps}

이번 단계가 끝났습니다! 이제 AEM의 Headless 콘텐츠 관리에 대한 기본 사항을 이해했습니다. 사용 가능한 기능을 포괄적으로 이해하기 위해 더 자세히 알아볼 수 있는 더 많은 리소스가 있습니다.

* **[구성 브라우저](create-configuration.md)** - AEM 구성 브라우저에 대한 자세한 내용
* **[콘텐츠 조각](/help/assets/content-fragments/content-fragments.md)** - 콘텐츠 조각 생성 및 관리에 대한 자세한 내용
* GraphiQL IDE 사용에 대한 자세한 내용은 **[GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md)**&#x200B;을 참조하십시오.
* 지속 쿼리에 대한 자세한 내용은 **[지속 쿼리](/help/sites-developing/headless/graphql-api/persisted-queries.md)**&#x200B;를 참조하세요.
* **[AEM Assets HTTP API의 콘텐츠 조각 지원](/help/assets/assets-api-content-fragments.md)** - CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 통해 HTTP API로 직접 AEM 콘텐츠에 액세스하는 방법에 대한 자세한 내용
* **[GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)** - 콘텐츠 조각을 Headless 방식으로 전달하는 방법에 대한 자세한 내용
