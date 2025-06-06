---
title: 페이지 편집을 위해 실행 취소 구성
description: AEM에서 페이지 편집에 대한 실행 취소 지원을 구성하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
exl-id: efeda84f-e04f-4cbd-898c-4754dc29e008
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 2%

---

# 페이지 편집을 위해 실행 취소 구성{#configuring-undo-for-page-editing}

[OSGi 서비스](/help/sites-deploying/configuring-osgi.md) **일 CQ WCM 실행 취소 구성**( `com.day.cq.wcm.undo.UndoConfigService`)은(는) 페이지 편집을 위해 실행 취소 및 다시 실행 명령의 동작을 제어하는 여러 속성을 표시합니다.

## 기본 구성 {#default-configuration}

표준 설치에서 기본 설정은 `sling:OsgiConfig`노드의 속성으로 정의됩니다.

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

이 노드에는 `cq.wcm.undo.whitelist` 및 `cq.wcm.undo.blacklist` 속성이 포함되어 있습니다. 다른 속성에는 기본값이 사용됩니다.

>[!CAUTION]
>
>***은(는) `/libs` 경로에서 아무 것도 변경하지 말아야***&#x200B;합니다.
>
>이는 다음에 인스턴스를 업그레이드할 때 `/libs`의 콘텐츠가 덮어쓰기되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수도 있음).

## 실행 취소 및 재실행 구성 {#configuring-undo-and-redo}

사용자 인스턴스에 대해 이러한 OSGi 서비스 속성을 구성할 수 있습니다.

>[!NOTE]
>
>AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리할 수 있는 방법에는 몇 가지가 있습니다. 자세한 내용 및 권장 사례를 확인하려면 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을(를) 참조하십시오.

다음은 웹 콘솔에 표시되는 등록 정보, 해당 OSGi 매개 변수의 이름, 설명 및 기본값(해당되는 경우)을 나열합니다.

* **사용**
( `cq.wcm.undo.enabled`)

   * **설명**: 페이지 작성자가 변경 내용을 실행 취소하거나 다시 실행할 수 있는지 여부를 결정합니다.
   * **기본값**: `Selected`
   * **유형**: `Boolean`

* **경로**
( `cq.wcm.undo.path`)

   * **설명**: 이진 실행 취소 데이터를 유지하기 위한 저장소 경로입니다. 작성자가 이미지와 같은 바이너리 데이터를 변경하면 데이터의 원래 버전이 여기에 유지됩니다. 이진 데이터에 대한 변경 내용을 실행 취소하면 이 이진 실행 취소 데이터가 페이지에 복원됩니다.
   * **기본값**: `/var/undo`
   * **유형**: `String`

  >[!NOTE]
  >
  >기본적으로 관리자만 `/var/undo` 노드에 액세스할 수 있습니다. 작성자는 이진 실행 취소 데이터에 액세스할 수 있는 권한이 부여된 후에만 이진 콘텐츠에 대해 실행 취소 및 재실행 작업을 수행할 수 있습니다.

* **분. 유효성**
( `cq.wcm.undo.validity`)

   * **설명**: 이진 실행 취소 데이터가 저장되는 최소 시간(시간)입니다. 이 기간이 지나면 디스크 공간을 절약하기 위해 이진 데이터를 삭제할 수 있습니다.
   * **기본값**: `10`
   * **유형**: `Integer`

* **단계**
( `cq.wcm.undo.steps`)

   * **설명**: 실행 취소 기록에 저장되는 최대 페이지 작업 수입니다.
   * **기본값**: `20`
   * **유형**: `Integer`

* **지속성**
( `cq.wcm.undo.persistence`)

   * **설명**: 실행 취소 기록을 유지하는 클래스입니다. 두 가지 지속성 클래스가 제공됩니다.

      * `CQ.undo.persistence.WindowNamePersistence`: window.name 속성을 사용하여 기록을 유지합니다.
      * `CQ.undo.persistence.CookiePersistance`: 쿠키를 사용하여 기록을 유지합니다.

   * **기본값**: `CQ.undo.persistence.WindowNamePersistence`
   * **유형**: `String`

* **지속성 모드**
( `cq.wcm.undo.persistence.mode`)

   * **설명**: 실행 취소 기록이 지속되는 시기를 결정합니다. 각 페이지를 편집한 후 실행 취소 기록을 유지하려면 이 옵션을 선택하십시오. 페이지가 다시 로드되는 경우(예: 사용자가 다른 페이지로 이동)에만 유지하려면 이 옵션의 선택을 취소합니다.

     실행 취소 기록을 유지하면 웹 브라우저 리소스가 사용됩니다. 사용자의 브라우저가 페이지 편집에 느리게 반응하는 경우 페이지 다시 로드 시 실행 취소 기록을 유지해 보십시오.

   * **기본값**: `Selected`
   * **유형**: `Boolean`

* **표식 모드**
( `cq.wcm.undo.markermode`)

   * **설명**: 실행 취소나 다시 실행이 발생할 때 영향을 받는 단락을 나타내는 데 사용할 시각적 큐를 지정합니다. 다음은 유효한 값입니다.

      * flash: 단락의 선택 표시기가 일시적으로 깜박입니다.
      * 선택: 단락이 선택됩니다.

   * **기본값**: `flash`
   * **유형**: `String`

* **좋은 구성 요소**
( `cq.wcm.undo.whitelist`)

   * **설명**: 실행 취소 및 다시 실행 명령의 영향을 받을 구성 요소 목록입니다. 구성 요소 경로가 실행 취소/다시 실행에서 올바르게 작동하는 경우 이 목록에 추가합니다. 별표(&ast;)를 추가하여 구성 요소 그룹을 지정합니다.

      * 다음 값은 기초 텍스트 구성 요소를 지정합니다.

        `foundation/components/text`

      * 다음 값은 모든 기초 구성 요소를 지정합니다.

        `foundation/components/*`

   * 이 목록에 없는 구성 요소에 대해 실행 취소 또는 재실행을 실행하면 명령을 신뢰할 수 없다는 메시지가 나타납니다.

   * **기본값**: 속성이 AEM에서 제공하는 많은 구성 요소로 채워집니다.
   * **유형**: `String[]`

* **잘못된 구성 요소**
( `cq.wcm.undo.blacklist`)

   * **설명**: 실행 취소 명령의 영향을 받지 않으려는 구성 요소 및/또는 구성 요소 작업의 목록입니다. 실행 취소 명령으로 올바르게 작동하지 않는 구성 요소 및 구성 요소 작업을 추가합니다.

      * 실행 취소 기록에서 구성 요소의 작업을 모두 사용하지 않으려면 구성 요소 경로를 추가하십시오. 예: `collab/forum/components/post`
      * 실행 취소 기록에서 특정 작업을 생략하려면 경로에 콜론(:) 및 작업을 추가하십시오(다른 작업이 올바르게 작동함). 예: `collab/forum/components/post:insertParagraph.`

  >[!NOTE]
  >
  >작업이 이 목록에 있는 경우에도 실행 취소 기록에 추가됩니다. 사용자가 실행 취소 내역에서 **잘못된 구성 요소** 작업 이전에 존재하는 작업을 실행 취소할 수 없습니다.

   * 일반적인 작업 이름은 다음과 같습니다.

      * `insertParagraph`: 구성 요소가 페이지에 추가됩니다.
      * `removeParagraph`: 구성 요소가 삭제되었습니다.
      * `moveParagraph`: 단락이 다른 위치로 이동되었습니다.
      * `updateParagraph`: 단락 속성이 변경되었습니다.

   * **기본값**: 속성이 여러 구성 요소 작업으로 채워집니다.
   * **유형**: `String[]`
