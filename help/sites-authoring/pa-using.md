---
title: 페이지 분석 데이터를 보고 페이지 콘텐츠의 효과를 측정합니다
description: 페이지 분석 데이터를 사용하여 페이지 콘텐츠의 효과를 측정합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Integration
role: User,Admin,Architect,Developer
exl-id: debcc73f-c2bb-4e3a-8ebf-c7590264d289
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 4%

---

# 페이지 분석 데이터 보기{#seeing-page-analytics-data}

페이지 분석 데이터를 사용하여 페이지 콘텐츠의 효과를 측정합니다.

## 콘솔에서 볼 수 있는 분석 {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

페이지 분석 데이터가 사이트 콘솔의 [목록 보기](/help/sites-authoring/basic-handling.md#list-view)에 표시됩니다. 페이지가 목록 형식으로 표시되면 기본적으로 다음 열을 사용할 수 있습니다.

* 페이지 조회수
* 고유 방문자
* 페이지 시간

각 열에는 현재 보고 기간에 대한 값이 표시되며, 이전 보고 기간 이후 값이 증가했는지 또는 감소했는지도 표시됩니다. 표시되는 데이터는 12시간마다 업데이트됩니다.

>[!NOTE]
>
>업데이트 기간을 변경하려면 [가져오기 간격을 구성하십시오](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. **사이트** 콘솔을 엽니다(예: [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. 도구 모음의 맨 오른쪽(오른쪽 상단)에서 아이콘을 클릭하여 **목록 보기**&#x200B;를 선택합니다. 표시되는 아이콘은 [현재 보기](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)에 따라 다릅니다.

1. 도구 모음의 맨 오른쪽(오른쪽 상단)에서 아이콘을 클릭한 다음 **설정 보기**&#x200B;를 선택합니다. **열 구성** 대화 상자가 열립니다. 필요한 변경 내용을 적용하고 **업데이트**&#x200B;를 통해 확인하세요.

   ![aa-04](assets/aa-04.png)

### 보고 기간 선택 {#selecting-the-reporting-period}

Analytics 데이터가 사이트 콘솔에 표시되는 보고 기간을 선택하십시오.

* 최근 30일 데이터
* 최근 90일 데이터
* 올해의 데이터

현재 보고 기간은 사이트 콘솔의 도구 모음(상단 도구 모음 오른쪽)에 표시됩니다. 드롭다운을 사용하여 필요한 보고 기간을 선택합니다.
![aa-05](assets/aa-05.png)

### 사용 가능한 데이터 열 구성 {#configuring-available-data-columns}

Analytics-Administrators 사용자 그룹의 구성원은 작성자가 추가 Analytics 열을 볼 수 있도록 Sites 콘솔을 구성할 수 있습니다.

>[!NOTE]
>
>페이지 트리에 다른 Adobe Analytics 클라우드 구성과 연결된 하위 항목이 포함되어 있는 경우 페이지에 사용할 수 있는 데이터 열을 구성할 수 없습니다.

1. 목록 보기에서 보기 선택기(도구 모음 오른쪽)를 사용하고 **보기 설정**&#x200B;을 선택한 다음 **사용자 지정 분석 데이터 추가**&#x200B;를 선택합니다.

   ![aa-15](assets/aa-15.png)

1. 사이트 콘솔에서 작성자에게 표시할 지표를 선택한 다음 **추가**&#x200B;를 클릭합니다.

   표시되는 열은 Adobe Analytics에서 검색됩니다.

   ![aa-16](assets/aa-16.png)

### 사이트에서 컨텐츠 인사이트 열기 {#opening-content-insights-from-sites}

사이트 콘솔에서 [콘텐츠 인사이트](/help/sites-authoring/content-insights.md)를 열어 페이지 효율성을 자세히 조사하십시오.

1. 사이트 콘솔에서 컨텐츠 인사이트를 보려는 페이지를 선택합니다.
1. 도구 모음에서 Analytics 및 권장 사항 아이콘을 클릭합니다.

   ![분석 및 권장 사항 아이콘](do-not-localize/chlimage_1-16a.png)

## 페이지 편집기에 표시되는 분석(Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>웹 사이트에 대해 [Activity Map이 구성](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map)된 경우 표시됩니다.

>[!NOTE]
>
>Activity Map에 대한 데이터는 Adobe Analytics에서 가져옵니다.

웹 사이트가 Adobe Analytics에 대해 [구성](/help/sites-administering/adobeanalytics-connect.md)되면 [모드 Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes)을 사용하여 관련 데이터를 볼 수 있습니다. 예:

![aa-07](assets/aa-07.png)

### Activity Map 액세스 {#accessing-the-activity-map}

[Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) 모드를 선택하면 Adobe Analytics 자격 증명을 입력해야 합니다.

![aa-03](assets/aa-03.png)

**Analytics** 부동 도구 모음이 표시됩니다. 여기에서 다음 작업을 수행할 수 있습니다.

* 이중 화살표(**>>**)를 사용하여 도구 모음 형식 변경
* 페이지 세부 정보 전환(눈 모양 아이콘)
* Activity Map 설정 구성( cog 아이콘)
* 표시할 분석을 선택합니다(다양한 드롭다운 선택기).
* Activity Map을 종료하고 도구 모음(x)을 닫습니다.

![aa-09](assets/aa-09.png)

### 표시할 분석 선택 {#selecting-the-analytics-to-show}

다양한 기준을 사용하여 표시할 분석 데이터와 표시 방법을 선택할 수 있습니다.

* **표준**/**라이브**

* 이벤트 유형
* 사용자 그룹
* **버블**/**그라데이션**/**승자 및 패자**/**해제**

* 표시할 기간

![aa-13](assets/aa-13.png)

### Activity Map 구성 {#configuring-the-activity-map}

**설정 표시** 아이콘을 사용하여 **Activity Map 설정** 대화 상자를 엽니다.

![aa-04-1](assets/aa-04-1.png)

**Activity Map 설정** 대화 상자는 다음 세 가지 탭에서 다양한 옵션을 제공합니다.

![aa-06](assets/aa-06.png)

* 일반

   * 보고서 세트
   * 페이지 이름
   * 언어
   * 레이블 오버레이 방법
   * 레이블 글꼴 크기
   * 그라데이션 색상
   * 거품 색상
   * 색상 그라데이션 기준
   * 그라데이션 투명도

* 표준

   * 표시(링크 유형 및 수)
   * 조회 수가 없는 링크에 대한 오버레이 숨기기

* 라이브

   * 상위 표시(승자 또는 패자)
   * 하위 % 제외
   * 자동 업데이트(데이터 및 기간)
