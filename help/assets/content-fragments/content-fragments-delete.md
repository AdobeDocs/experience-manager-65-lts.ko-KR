---
title: 콘텐츠 조각 - 삭제 고려 사항
description: AEM에서 콘텐츠 조각 삭제 정책을 정의하기 전에 이러한 중요한 고려 사항을 검토하십시오. 콘텐츠 조각은 Headless 콘텐츠를 제공하기 위한 강력한 도구이며 콘텐츠 조각 삭제가 가져오는 영향을 신중하게 고려해야 합니다.
feature: Content Fragments
role: User
solution: Experience Manager, Experience Manager Assets
exl-id: 1460872b-415f-4392-a480-c442790fd0d9
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 100%

---

# 콘텐츠 조각 - 삭제 고려 사항 {#content-fragments-delete-considerations}

AEM에서 콘텐츠 조각 삭제 정책을 정의하기 전에 이러한 중요한 고려 사항을 검토하십시오. 콘텐츠 조각은 Headless 콘텐츠를 제공하기 위한 강력한 도구이며 콘텐츠 조각 삭제가 가져오는 영향을 신중하게 고려해야 합니다.

## 권한 - 삭제 또는 삭제 안 함 {#permissions-delete-or-not-delete}

콘텐츠 삭제 기능은 강력하지만, 이러한 권한이 배포되는 방식을 제한하고 제어해야 하는 많은 업계에서는 민감할 수 있습니다.

권한 삭제 시 콘텐츠 조각을 두 가지 수준으로 고려해야 합니다.

1. **단일 엔티티로서의 콘텐츠 조각.**

   * **사용 사례**: 컨텐츠 조각을 편집/업데이트하며 **전체 조각을 삭제**&#x200B;해야 하는 사용자.
   * **권한**: [삭제](/help/sites-administering/security.md#actions) 권한은 [사용자 및/또는 그룹 관리를 통해 삭제 권한을 지정](/help/sites-administering/security.md#managing-permissions)할 수 있습니다.

2. **변형이나 하위 노드와 같이 컨텐츠 조각을 구성하는 여러 하위 엔티티.**

   콘텐츠 조각 편집기의 기본 작업을 수행하려면 이러한 임시 하위 요소를 삭제할 수 있어야 합니다. 예를 들어 변형을 조작할 때 또는 메타데이터를 편집하거나 관련 콘텐츠를 관리할 때도 마찬가지입니다.

   * **사용 사례**: 콘텐츠 조각을 편집/업데이트해야 하지만, **전체 조각 삭제는 허용되지 않는** 사용자.
   * **권한**: [편집기 기능에만 필요한 권한](#permissions-required-for-editor-functionality-only)을 참조하십시오.

>[!NOTE]
>
>사용자에게 [삭제](/help/sites-administering/security.md#actions) 권한이 없는 경우 컨텐츠 조각 편집기는 *읽기 전용* 모드로 작동합니다.

>[!NOTE]
>
>[AEM에서 사용자 관리 작업을 감사하는 방법](/help/sites-administering/audit-user-management-operations.md)을 참조하십시오.

## 편집기 기능에만 필요한 권한 {#permissions-required-for-editor-functionality-only}

콘텐츠 조각을 편집/업데이트해야 하는데 **전체 조각 삭제가 허용되지 않는** 사용자의 경우 콘텐츠 조각 편집기의 기본 작업을 수행하려면 임시 하위 요소를 삭제할 수 있어야 하므로 특정 권한을 지정해야 합니다.

예를 들어 변형을 조작할 때 또는 메타데이터를 편집하거나 관련 컨텐츠를 관리할 때도 마찬가지입니다.

>[!NOTE]
>
>컨텐츠 조각을 편집/업데이트하는 데 필요한 삭제 권한은 [사용자 및/또는 그룹 관리를 통해 지정된](/help/sites-administering/security.md#managing-permissions) 삭제 권한에 포함되어 있습니다.

조각을 편집/업데이트하는 데 필요한 권한은 컨텐츠 조각을 포함하는 노드나 적절한 상위 노드(`/content/dam` 하의 어떤 하위 수준이든)에 적용되어야 합니다. 권한은 이러한 상위 노드에 지정되면 해당 분기 내의 모든 노드에 적용됩니다.

예를 들어 다음과 같은 모든 콘텐츠 조각을 포함하는 폴더:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>모든 콘텐츠 조각이 `/content/dam`에 저장되므로 여기에 대한 권한을 설정할 수도 있습니다.
>
>하지만 이 작업을 수행하면 다른 *모든* 자산 유형에도 동일한 삭제 권한이 적용됩니다.

특정 사용자 및/또는 그룹이 콘텐츠 조각을 편집/업데이트할 수 있도록 허용하기 위한 권한 전제 조건은 다음과 같습니다.

>[!NOTE]
>
>이 목록에는 삭제 권한뿐만 아니라 필요한 모든 권한이 표시됩니다.

* 콘텐츠 조각 노드 또는 폴더의 경우:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* 모든 콘텐츠 조각의 `jcr:content`노드의 경우:

   * `jcr:addChildNodes`, `jcr:modifyProperties` 및 `jcr:removeChildNodes`

* 모든 콘텐츠 조각의 `jcr:content` 아래에 있는 모든 노드의 경우:

   * `jcr:addChildNodes`, `jcr:modifyProperties` 및 `jcr:removeChildNodes`, `jcr:removeNode`

이러한 `remove` 권한은 [CRXDE Lite 내에서 액세스 제어 목록을 사용하여 관리](/help/sites-administering/user-group-ac-admin.md#access-right-management)해야 합니다.

`add` 및 `modify` 권한은 CRXDE Lite에서 또는 사용자 관리 콘솔을 사용하여 관리할 수도 있습니다.

예: `content-authors-no-delete` 그룹에 대한 `remove` 권한의 정의:

![cf-delete-03](assets/cf-delete-03.png)
