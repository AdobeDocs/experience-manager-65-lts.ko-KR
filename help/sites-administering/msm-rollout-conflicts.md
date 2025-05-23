---
title: MSM 롤아웃 충돌
description: 다중 사이트 관리자 롤아웃 충돌을 처리하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
feature: Multi Site Manager
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 3c207bfd-5d40-4355-8710-a620f0d66399
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 20%

---

# MSM 롤아웃 충돌{#msm-rollout-conflicts}

블루프린트 분기 및 종속 라이브 카피 분기 모두에서 동일한 페이지 이름의 새 페이지를 만들면 충돌이 발생할 수 있습니다.

이러한 충돌은 롤아웃 시 처리 및 해결해야 합니다.

## 충돌 처리 {#conflict-handling}

블루프린트 및 라이브 카피 분기에 충돌하는 페이지가 있는 경우 MSM을 사용하여 처리 방법(또는 처리 여부)을 정의할 수 있습니다.

롤아웃을 차단하지 않도록 다음과 같은 정의를 사용할 수 있습니다.

* 롤아웃 시 우선 순위가 높은 페이지(블루프린트 또는 라이브 카피)
* 페이지 이름 변경(및 방법),
* 게시된 콘텐츠에 미치는 영향

  Adobe Experience Manager(AEM)의 기본 비헤이비어(기본 제공)는 게시된 콘텐츠에 영향을 미치지 않는다는 것입니다. 따라서 라이브 카피 분기에 수동으로 생성된 페이지가 게시되어 있는 경우 해당 콘텐츠는 충돌 처리 및 롤아웃 이후에도 계속 게시됩니다.

표준 기능 이외에도 맞춤화된 충돌 핸들러를 추가하여 다른 규칙을 구현할 수 있습니다. 또한 개별 프로세스로 게시 작업을 허용할 수도 있습니다.

### 예시 상황 {#example-scenario}

다음 섹션에서는 블루프린트 및 라이브 카피 분기 모두에 수동으로 생성된 새 페이지 `b`의 예를 사용하여 다양한 충돌 해결 방법을 설명해야 합니다.

* 블루프린트: `/b`

  마스터 페이지. 한 개의 하위 페이지가 있는 경우 bp-level-1.

* live copy: `/b`

  Live Copy 분기에 수동으로 생성된 페이지입니다. 하위 페이지 `lc-level-1`이(가) 한 개 있습니다.

   * 게시에서 하위 페이지와 함께 `/b`(으)로 활성화되었습니다.

**롤아웃 전**

<table>
 <tbody>
  <tr>
   <td><strong>롤아웃 이전의 블루프린트</strong></td>
   <td><strong>롤아웃 이전의 live copy</strong></td>
   <td><strong>롤아웃 전 게시</strong></td>
  </tr>
  <tr>
   <td><code>b</code><br /> <br /> (블루프린트 분기에서 만들어짐, 롤아웃 준비 완료)<br /> </td>
   <td><code>b</code><br /> <br /> (라이브 카피 분기에 수동으로 생성됨)<br /> </td>
   <td><code>b</code><br /> <br /> (라이브 카피 분기에 수동으로 생성된 페이지 b의 콘텐츠 포함)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (라이브 카피 분기에 수동으로 생성됨)<br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> (라이브 카피 분기에 수동으로 생성된 <br /> 하위 수준 1의 페이지 콘텐츠 포함)</td>
  </tr>
 </tbody>
</table>

## 롤아웃 관리자 및 충돌 처리 {#rollout-manager-and-conflict-handling}

롤아웃 관리자를 사용하여 충돌 관리를 활성화 또는 비활성화할 수 있습니다.

이 작업은 **일 CQ WCM 롤아웃 관리자**&#x200B;의 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 사용하여 수행됩니다.

* **수동으로 만든 페이지와의 충돌 처리**:

  ( `rolloutmgr.conflicthandling.enabled`)

  롤아웃 관리자가 블루프린트에 존재하는 이름으로 라이브 카피에 생성된 페이지의 충돌을 처리해야 하는 경우 true로 설정합니다.

AEM에는 충돌 관리가 비활성화되었을 때 [미리 정의된 동작이 있습니다](#behavior-when-conflict-handling-deactivated).

## 충돌 핸들러 {#conflict-handlers}

AEM은 충돌 처리기를 사용하여 블루프린트에서 라이브 카피로 콘텐츠를 롤아웃할 때 발생하는 페이지 충돌을 해결합니다. 페이지 이름을 바꾸는 것은 이러한 충돌을 해결하는 일반적인 방법 중 하나입니다. 하나 이상의 충돌 핸들러를 작동하여 다양한 비헤이비어를 실행할 수 있습니다.

AEM은 다음을 제공합니다.

* [기본 충돌 핸들러](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* [사용자 지정된 처리기](#customized-handlers)를 구현할 수 있습니다.
* 각 개별 처리기의 우선 순위를 설정할 수 있는 서비스 순위 메커니즘. 순위가 가장 높은 서비스가 사용됩니다.

### 기본 충돌 핸들러 {#default-conflict-handler}

기본 충돌 처리기는

* `ResourceNameRolloutConflictHandler`(으)로 호출됨

* 이 핸들러를 사용하면 블루프린트 페이지가 우선 순위를 갖습니다.
* 이 처리기의 서비스 순위는 낮게 설정되어 있습니다(즉, `service.ranking` 속성의 기본값보다 낮음). 맞춤화된 처리기에 더 높은 순위가 필요하다고 가정하기 때문입니다. 그러나 순위는 유연성을 보장하기 위한 절대적인 최소 조건이 아닙니다.

이 충돌 핸들러를 사용하면 블루프린트가 우선 순위를 갖습니다. Live Copy 페이지 `/b`이(가) Live Copy 분기 내에서 `/b_msm_moved`(으)로 이동되었습니다.

* live copy: `/b`

  Live Copy 내에서 `/b_msm_moved`(으)로 이동됩니다. 이는 백업 역할을 하며 콘텐츠가 손실되지 않도록 합니다.

   * `lc-level-1`은 이동하지 않습니다.

* 블루프린트: `/b`

  Live Copy 페이지 `/b`(으)로 롤아웃되었습니다.

   * `bp-level-1`이(가) Live Copy로 롤아웃되었습니다.

**롤아웃 이후**

<table>
 <tbody>
  <tr>
   <td><strong>롤아웃 이후의 블루프린트</strong></td>
   <td><strong>롤아웃 이후의 라이브 카피</strong><br /> </td>
   <td></td>
   <td><strong>롤아웃 이후의 Live Copy</strong><br /> <br /> <br /> </td>
   <td><strong>롤아웃 후 게시</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> (롤아웃된 블루프린트 페이지 b의 콘텐츠가 있음)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code><br /> <br /> (라이브 카피 분기에 수동으로 생성된 페이지 b의 콘텐츠가 있음)</td>
   <td><code>b</code><br /> <br /> (변경 내용 없음, 라이브 카피 분기에 수동으로 생성된 원본 페이지 b의 콘텐츠(이제 b_msm_moved라고 함)를 포함합니다.)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (변경 내용 없음)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code><br /> <br /> (변경 내용 없음)</td>
  </tr>
 </tbody>
</table>

### 맞춤화된 핸들러 {#customized-handlers}

맞춤화된 충돌 처리기를 사용하면 고유한 규칙을 구현할 수 있습니다. 서비스 순위 메커니즘을 사용하여 이들 핸들러가 다른 핸들러와 상호 작용하는 방법을 지정할 수도 있습니다.

맞춤화된 충돌 처리기에는 다음이 있을 수 있습니다.

* 요구 사항에 따라 이름이 지정됩니다.
* 요구 사항에 따라 개발/구성됩니다. 예를 들어 라이브 카피 페이지가 우선 순위를 갖도록 핸들러를 개발할 수 있습니다.
* [OSGi 구성](/help/sites-deploying/configuring-osgi.md)을 사용하여 구성되도록 설계되었습니다. 특히

   * **서비스 순위**:

     다른 충돌 처리기(`service.ranking`)와 관련된 순서를 정의합니다.

     기본값은 0입니다.

### 충돌 처리가 비활성화되었을 때 실행되는 비헤이비어 {#behavior-when-conflict-handling-deactivated}

수동으로 [충돌 처리를 비활성화](#rollout-manager-and-conflict-handling)하면 AEM은 충돌이 발생한 페이지에 어떤 조치도 취하지 않습니다(충돌이 발생하지 않은 페이지는 예상대로 롤아웃됨).

>[!CAUTION]
>
>AEM은 이 동작을 명시적으로 구성해야 하므로 충돌이 무시되고 있음을 나타내지 않으므로 필수 동작으로 간주합니다.

이 경우 라이브 카피가 사실상 우선됩니다. 블루프린트 페이지 `/b`은(는) 복사되지 않으며 Live Copy 페이지 `/b`은(는) 그대로 유지됩니다.

* 블루프린트: `/b`

  복사되지 않지만 무시됩니다.

* live copy: `/b`

  똑같군

<table>
 <caption>
   롤아웃 이후
 </caption>
 <tbody>
  <tr>
   <td><strong>롤아웃 이후의 블루프린트</strong></td>
   <td><strong>롤아웃 이후의 Live Copy</strong><br /> <br /> <br /> </td>
   <td><strong>롤아웃 후 게시</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> (변경 내용 없음, 라이브 카피 분기에 수동으로 생성된 페이지 b의 콘텐츠가 있음)</td>
   <td><code>b</code><br /> <br /> (변경 내용 없음, 라이브 카피 분기에 수동으로 생성된 페이지 b의 콘텐츠 포함)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code><br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> (변경 내용 없음)</td>
   <td><code> /lc-level-1</code><br /> <br /> (변경 내용 없음)</td>
  </tr>
 </tbody>
</table>

### 서비스 순위 {#service-rankings}

[OSGi](https://www.osgi.org/) 서비스 순위를 사용하여 개별 충돌 핸들러의 우선 순위를 정의할 수 있습니다.
