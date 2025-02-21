---
product: adobe experience manager
description: Adobe Experience Manager 6.6 설명서.
git-repo: https://github.com/AdobeDocs/experience-manager-65-lts.ko-KR
index: y
type: Documentation
solution: Experience Manager
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: fd332664a30756feca9bb282ba334bd7e497e1d9
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 53%

---


# 내부 사용을 위한 메타데이터

GitHub 제작 시스템의 메타데이터는 계층적이며 다음과 같이 증가하는 선례 수준으로 정의됩니다.

1. metadata.md
1. ToC
1. 문서

metadata.md 파일에 정의된 메타데이터는 전체 리포지토리에 적용되지만 ToC 및 문서 수준에서 재정의될 수 있습니다. 메타데이터 재정의는 가능한 한 낮은 수준에서 수행해야 합니다.

experience-manager-cloud-service.en 리포지토리의 메타데이터는 필요한 최소값입니다.

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

ToCs

* `sub-product`
* `user-guide-title`

문서

* `title`
* `description`
* `contentOwner`(`/help/assets` 아래의 핵심 자산 콘텐츠에서만)