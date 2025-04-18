---
title: 론치 편집
description: 페이지(또는 페이지 세트)에 대한 론치가 만들어지면 페이지의 론치 카피에서 콘텐츠를 편집할 수 있습니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 9a29bdbf-0f5d-4656-bd65-a63fd804c9e7
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 8%

---

# 론치 편집{#editing-launches}

## 론치 편집 페이지 {#editing-launch-pages}

페이지(또는 페이지 세트)에 대한 론치가 만들어지면 페이지의 론치 카피에서 콘텐츠를 편집할 수 있습니다.

1. 편집할 페이지를 엽니다.
1. Sidekick에서 **버전 관리** 탭을 선택한 다음 **시작** 그룹을 확장합니다. 현재 편집 중인 론치 제목은 굵은 글꼴을 사용합니다.

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. 작업할 시작을 선택한 다음 **전환**&#x200B;을 클릭합니다.
1. 편집을 시작합니다.

   >[!NOTE]
   >
   >사이드 킥의 **페이지** 탭을 사용하여 **하위 페이지 만들기**&#x200B;와 같은 작업을 수행할 수 있습니다.

## 론치 구성 편집 {#editing-a-launch-configuration}

론치를 만든 후 론치 이름과 론치 날짜를 변경할 수 있습니다. 론치와 연결할 이미지를 지정할 수도 있습니다.

1. 실행 관리 페이지([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html))를 엽니다.

1. 필요한 시작을 선택하고 **편집**&#x200B;을 클릭하여 대화 상자를 엽니다.

   * **일반** 탭에서 다음을 편집할 수 있습니다.

      * **제목**
      * **라이브 날짜**: 시작 날짜와 동일합니다
      * **프로덕션 준비**

     이러한 필드의 목적 및 상호 작용에 대한 자세한 내용은 [시작 - 이벤트 순서](/help/sites-authoring/launches.md#launches-the-order-of-events)를 참조하십시오.

   * **이미지** 탭에서 이미지 파일을 업로드할 수 있습니다.

1. **저장**&#x200B;을 클릭합니다.

## 페이지의 론치 상태 찾기 {#discovering-the-launch-status-of-a-page}

페이지 시작을 편집하는 경우 Sidekick의 **버전 관리** 탭 하단에 시작에 대한 정보가 표시됩니다.

* 론치 이름입니다.
* 마지막 변경 이후 시간입니다.
* 마지막 변경을 수행한 사용자입니다.
* **프로덕션 준비** 플래그의 상태(주황색=설정되지 않음, 녹색=설정)입니다.

![chlimage_1-186](assets/chlimage_1-186.png)
