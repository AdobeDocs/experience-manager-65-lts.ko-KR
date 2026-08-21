---
title: Adobe Experience Manager 6.5 LTS, SP3의 최신 릴리스 노트
description: Adobe Experience Manager 6.5 LTS, 서비스 팩 3의 최신 릴리스 정보를 확인하십시오.
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 79f3d3211a79ce62242273df0cdecd24cd8900cf
workflow-type: tm+mt
source-wordcount: '6705'
ht-degree: 26%

---


# Adobe Experience Manager 6.5 LTS, SP3의 최신 릴리스 노트 {#release-notes}

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 버전 | 서비스 팩 3(SP3) <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2026년 8월 20일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.3.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

<!-- **Mandatory Hotfix** – To avoid SNFE (SegmentNotFoundException) issues with offline compaction when installing SP2, install the hotfix described in [Known issues – Repository corruption during online compaction](#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146). -->

## [!DNL Adobe Experience Manager] 6.5 LTS, SP3에 포함된 항목 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS, SP3에는 새로운 기능, 고객이 요청한 주요 개선 사항 및 버그 수정이 포함되어 있습니다. 2025년 3월에 6.5 LTS가 처음 출시된 이후 플랫폼 전반에서 성능, 보안 및 현지화 기능이 향상되었습니다. 6.5 LTS에 [이 서비스 팩을 설치](#install-update)하십시오.

### 해결된 문제 개요 {#fixed-issues-overview}

[!DNL Adobe Experience Manager] 6.5 LTS, SP3이(가) [!DNL Sites] 및 [!DNL Experience Manager Foundation]에서 문제를 해결합니다. 이 수정 사항은 접근성, 작성 안정성, Headless 콘텐츠 전달, 다중 사이트 관리 및 플랫폼 안정성을 개선합니다. 다음에 나오는 섹션은 참조 번호와 함께 각 수정 사항을 나열합니다.

대부분의 변경 내용이 [!DNL Sites]에 적용됩니다.

* 가장 큰 그룹에서 액세스 가능성이 개선되었습니다. 이 업데이트는 페이지 편집기, Assets 측 레일, 필터 및 관련 작성 인터페이스 전반에서 키보드 탐색, 화면 판독기 피드백, 포커스 관리, 시맨틱 마크업, 텍스트 대비 및 터치 타겟 크기 조정을 강화합니다.
* [!DNL Content Fragments]의 수정 사항은 조각 편집기, 모델 편집기, REST API 및 GraphQL API에 적용됩니다. 업데이트는 현지화, 필드 유효성 검사, 편집 동작 및 응답 처리를 수정합니다.
* MSM 라이브 카피 수정 사항을 통해 작성자는 블루프린트 페이지에서 변경 사항을 안정적으로 롤아웃하고 기존 롤아웃 구성을 유지할 수 있습니다.
* 필요한 번들, 시스템 사용자 및 구성을 포함하여 Adobe Managed Services에서 횡단보도 지원을 사용할 수 있습니다.
* 관리 및 클래식 인터페이스, 핵심 구성 요소, 구성 요소 콘솔, Campaign 통합, 경험 조각 및 론치를 해결하는 추가 수정 사항이 있습니다.

나머지 변경 사항은 [!DNL Experience Manager Foundation]에 적용됩니다.

* 현지화 업데이트는 상태 보고서, 작업 콘솔 및 여러 작성 인터페이스에서 이전의 영어 전용 텍스트를 번역합니다.
* 안정성 수정 사항은 상태 모니터링 엔드포인트를 복원하고, 간헐적인 구성 오류 후 메일 서비스를 계속 실행하며, 워크플로우 변수 및 워크플로우 패키지 편집을 수정합니다.
* 또한 이 릴리스에서는 AEM 컨텍스트 서비스 지원이 추가되고 보안, 번역 및 사용자 인터페이스 문제가 해결되었습니다.

전체 목록에 대해서는 [6.5 LTS, 서비스 팩 3의 해결된 문제](#fixed-issues)를 참조하십시오.


<!-- ## Key features and enhancements -->



<!-- UPDATE THE EACH RELEASE -->

## 6.5 LTS, 서비스 팩 3의 문제가 해결되었습니다. {#fixed-issues}

### [!DNL Sites]{#sites-65-LTS-SP3}

* AEM 6.5 LTS, 서비스 팩 3에는 횡단보도 번들, 콘텐츠 패키지, 시스템 사용자, 서비스 사용자 매핑, 기능 전환 및 필수 OSGi 구성이 포함됩니다. 새로 설치하면 횡단보도 사전 요구 사항이 자동으로 제공되며 고객별 런타임 구성만 필요합니다. (SITES-41596)
* AEM 6.5 LTS, 서비스 팩 3은(는) Adobe Managed Services에서 횡단보도를 지원하도록 `cq-wcm-core`을(를) 업데이트합니다. 업데이트는 오래된 사용자 지정 코드 및 기능 전환을 제거하면서 템플릿 만들기 및 유니버설 편집기 액세스를 추가합니다. (SITES-37657)


#### 접근성 {#sites-accessibility-65-lts-sp3}

* 페이지 편집기 캔버스는 이제 키보드 전용 구성 요소 관리를 지원합니다. 작성자는 구성 요소 삽입, 잘라내기, 붙여넣기 및 삭제 를 사용하여 구성 요소를 추가, 순서 변경 및 제거할 수 있습니다. (SITES-25359) 중요
* 이제 키보드 사용자는 드래그 앤 드롭 제스처를 사용하지 않고 사이트 목록 보기에서 표 행을 재정렬할 수 있습니다. 키보드 컨트롤을 사용하면 사용자가 행을 선택하고 다른 위치로 이동한 다음 배치를 완료할 수 있습니다. (SITES-24946) 중요

* 이제 사용자 지정 속성 편집기에서 서식 지정 컨트롤과 키보드 상호 작용을 지원합니다. 작성자는 도구 모음 옵션 간에 포커스를 이동하고, 텍스트 스타일을 선택하고, 키보드만 사용하여 속성 값의 서식을 지정할 수 있습니다. (SITES-40333) 메이저

* 이제 키보드 포커스는 사용 가능한 상호 작용에 끌어서 놓기가 필요할 때 사이드 패널 구성 요소 목록을 건너뜁니다. 이 변경 사항으로 인해 키보드 사용자는 사용할 수 없는 구성 요소 선택 워크플로우에 들어갈 수 없습니다. (SITES-40752)
* 이제 오버레이를 닫으면 포커스가 트리거 제어로 복원됩니다. 키보드 및 화면 판독기 사용자는 더 이상 오버레이로 돌아가거나 인터페이스에서 위치를 잃지 않습니다. (SITES-40819)
* 키보드 탐색은 더 이상 포커스를 숨겨진 페이지 콘텐츠로 이동하지 않습니다. 이러한 변경은 예측 가능한 포커스 시퀀스를 유지하고 내비게이션 중단을 방지한다. (SITES-41430)
* 이제 잠금 버튼을 사용하여 제목을 기반으로 정확한 화면 판독기 피드백을 제공할 수 있습니다. 사용자가 긴 설명 대신 명확한 작업 레이블을 듣습니다. (SITES-41431)
* 이제 시각적 표시기가 파일 또는 폴더 변경 목록 상자에서 선택한 옵션을 식별합니다. 표시기는 사용자가 이동 경로 경로를 이해하고 현재 폴더를 인식하는 데 도움이 됩니다. (SITES-25532)
* 이제 화면 판독기에 오름차순 또는 내림차순 정렬 방향이 한 번 표시됩니다. 설명 레이블은 버튼 작업을 명확하게 식별하고 중복 피드백을 제거합니다. (SITES-25534)
* 이제 AEM Sites은 일반적인 작성 워크플로 전반에서 더 광범위한 접근성 지원을 제공합니다. 업데이트는 키보드 상호 작용, 인터페이스 레이블, 포커스 관리 및 보조 기술 피드백을 개선합니다. (SITES-38239)
* 이제 도구 모음 항목이 키보드 포커스를 받을 때 표시되는 레이블을 표시합니다. 키보드 사용자는 각 컨트롤을 활성화하기 전에 식별할 수 있습니다. (SITES-40751)
* 키보드 및 화면 판독기 사용자는 이제 받은 편지함 메뉴를 열어 두지 않고 그대로 둘 수 있습니다. 메뉴가 자동으로 닫히고 명확한 탐색 경로를 유지합니다. (SITES-25518)
* 이제 색상 견본에 충분한 대비가 있는 선택된 상태 아이콘이 표시됩니다. 더 선명한 표시기는 사용자가 다양한 배경색에서 활성 견본을 인식하는 데 도움이 됩니다. (SITES-25523)
* 이제 레이아웃 편집 도구 모음에서 현재 장치를 보조 기술에 정확하게 보고합니다. 장치 버튼은 사용자가 각 버튼을 켜거나 끌 수 있음을 더 이상 제안하지 않습니다. (SITES-25524)
* 이제 검색 모달에 텍스트 대비가 충분한 **정렬 기준** 레이블이 표시됩니다. 업데이트된 스타일링은 시력이 낮은 사용자의 가독성을 향상시킵니다. (SITES-25531)
* 이제 사이트 목록 보기 정렬 버튼이 최소 대비 요구 사항을 충족합니다. 사용자는 표 배경에서 각 정렬 컨트롤 및 해당 상태를 보다 쉽게 식별할 수 있습니다. (SITES-25372)
* 필터 필드가 키보드 포커스를 받을 때 사이드 레일 Assets 목록이 더 이상 다시 로드되지 않습니다. 사용자는 예기치 않은 콘텐츠 이동 또는 반복적인 화면 판독기 로드 알림 없이 필드에 입력할 수 있습니다. (SITES-25377)
* 이제 콘텐츠 조각 사이드바 탭에서 액세스 가능한 일관된 레이블을 제공합니다. NVDA는 선택한 하위 탐색 항목을 알리는 대신 탭 이름을 알립니다. (SITES-25509)
* 키보드 또는 화면 판독기 포커스가 도움말 메뉴 밖으로 이동하면 도움말 메뉴가 닫힙니다. 사용자는 메뉴를 열어 두지 않고 머리글 컨트롤 또는 페이지 콘텐츠를 계속 탐색할 수 있습니다. (SITES-25517)
* 인구 통계 도구 모음 필드에 입력한 텍스트가 이제 최소 대비 요구 사항을 충족합니다. 사용자는 텍스트 필드 배경에 대해 프로필 값을 보다 명확하게 읽을 수 있습니다. (SITES-25318)
* 이제 페이지 정보 메뉴에 텍스트 대비가 충분한 포커스가 있는 옵션이 표시됩니다. 더 명확한 스타일을 통해 사용자가 메뉴 전체에서 키보드 포커스를 추적할 수 있습니다. (SITES-25321)
* 이제 티저, 이미지 및 회전판 대화 상자의 확인란에 관련 지침이 화면 판독기에 표시됩니다. 키보드 포커스가 각 확인란에 도달하면 지원 설명이 표시됩니다. (SITES-25364)
* 이제 텍스트 편집기 컨트롤은 현재 상태를 보조 기술에 전달합니다. 화면 판독기는 활성 단락 형식과 선택한 하이퍼링크 대상 옵션을 식별합니다. (SITES-25367)
* 이제 화면 판독기에 **장치 회전** 단추와 현재 장치 방향이 명확하게 표시됩니다. 컨트롤을 활성화하면 반대 작업을 설명하는 레이블을 사용하지 않고 새 방향이 보고됩니다. (SITES-25292)
* 이제 키보드 탐색은 축소된 인구 통계 도구 모음 내에 숨겨진 컨트롤을 건너뜁니다. 사용자는 사용할 수 없는 도구 모음 옵션을 발견하지 않고도 레이아웃 미리 보기를 통해 이동할 수 있습니다. (SITES-25304)
* 이제 [인구 분포] 도구 모음의 텍스트 레이블이 [레이아웃 미리 보기] 동안 최소 대비 요구 사항을 충족합니다. 사용자는 도구 모음 배경에 대해 권장 과 같은 레이블을 보다 명확하게 읽을 수 있습니다. (SITES-25307)
* 이제 인구 통계 도구 모음에 충분한 대비가 있는 단추 포커스 표시기가 표시됩니다. 사용자는 키보드 탐색 중에 활성 Commerce, 사용자 또는 장치 제어를 식별할 수 있습니다. (SITES-25308)
* 레이아웃 편집 도구 모음에서는 장치 선택기에 대해 그룹화된 포커스 표시기를 사용합니다. 윤곽선에는 관련 **장치 선택** 및 **장치 회전** 컨트롤이 의도한 도구 모음 동작의 일부로 포함되어 있습니다. (SITES-25283)
* 사용자가 다른 장치를 선택할 때 레이아웃 편집 도구 모음이 더 이상 **iPhone 8 Plus** 레이블을 자르지 않습니다. 전체 장치 이름은 모든 버튼 상태에서 계속 표시됩니다. (SITES-25284)
* 이제 레이아웃 편집 눈금자가 화면 판독기에 측정 컨텍스트를 제공합니다. 사용자는 설명되지 않은 일련의 숫자 대신 설명 레이블과 측정 형식을 듣습니다. (SITES-25287)
* 데스크톱 보기가 활성 상태일 때 레이아웃 편집 도구 모음이 **데스크톱** 단추를 강조 표시합니다. 시각적 표시기가 현재 장치 선택을 명확하게 합니다. (SITES-25290)
* 이제 키보드 포커스가 사용 가능한 모든 색상의 견본 단추에 계속 표시됩니다. 추가된 간격은 포커스 표시기가 선택한 견본에 혼합되지 않도록 합니다. (SITES-25253)
* 이제 화면 판독기에서 타임워프 날짜 필드를 올바르게 식별합니다. 필드는 더 이상 대화 상자를 여는 것처럼 오해의 소지가 있는 피드백을 제공하지 않습니다. (SITES-25263)
* 이제 주석 단추 레이블이 기본 및 마우스 오버 상태에서 최소 대비 요구 사항을 충족합니다. 사용자는 버튼 배경에 라벨을 명확하게 읽을 수 있습니다. (SITES-25267)
* 이제 화면 판독기에 주석 대화 상자의 컨트롤에 대해 의미 있는 레이블이 표시됩니다. 각 버튼은 불필요한 주석 접두사 없이 해당 작업을 전달합니다. (SITES-25277)
* 이제 Assets 측 레일 편집 버튼에 더 큰 터치 대상이 제공됩니다. 사용자는 가까운 요소를 선택하지 않고서도 보다 확실하게 제어를 활성화할 수 있다. (SITES-25221)
* 이제 페이지 편집기에서 논리 제목 계층 구조를 사용합니다. 화면 판독기는 페이지 제목을 기본 제목으로, 측면 레일 제목을 하위 제목으로 식별합니다. (SITES-25222)
* 이제 주석 대화 상자에 해당 제목이 의미 체계 머리글로 표시됩니다. 화면 판독기 사용자는 제목 명령을 통해 제목을 식별하고 대화 상자 구조를 탐색할 수 있습니다. (SITES-25248)
* 이제 화면 판독기 사용자가 새 구성 요소 삽입 목록을 필터링할 때 피드백을 받습니다. 검색 필드는 필터링 동작에 대해 설명하고 상태 메시지는 결과 수를 보고합니다. (SITES-25251)
* 이제 사이드 레일 구성 요소 패널에서 의미 목록 마크업을 사용합니다. 화면 판독기는 항목 수를 알려주고 효율적인 목록 탐색을 지원할 수 있습니다. (SITES-25214)
* 이제 [구성 요소] 패널에서 정보 버튼에 더 큰 아이콘이 사용됩니다. 사용자는 각 컨트롤을 보다 쉽게 찾아 인식할 수 있습니다. (SITES-25217)
* 이제 사용자가 텍스트 간격을 늘리면 구성 요소 제목이 계속 표시됩니다. 긴 제목은 근처 콘텐츠를 자르거나 겹치는 대신 래핑됩니다. (SITES-25219)
* 이제 Assets 쪽 레일 **편집** 단추가 새 브라우저 탭을 열었음을 나타냅니다. 시각적 및 화면 판독기 큐는 탐색 전에 사용자를 준비시킵니다. (SITES-25220)
* 이제 주석 모드에서는 도구 모음이 열릴 때 주석 도구 모음에 키보드 포커스가 배치됩니다. 키보드 및 화면 판독기 사용자는 **닫기** 단추에서 뒤로 이동하지 않고 컨트롤을 논리적 순서로 이동할 수 있습니다. (SITES-24996)
* 경로 및 태그 필드에 대한 선택 단추는 더 이상 확인란 아이콘을 사용하지 않습니다. 업데이트된 아이콘은 컨트롤에서 선택된 상태를 변경하는 대신 선택 대화 상자가 열린다는 것을 보여 줍니다. (SITES-25210)
* 이제 측면 레일 구성 요소 패널의 필터 필드에 유효한 액세스 가능한 레이블이 있습니다. 화면 판독기는 아이콘이나 자리 표시자 텍스트에 의존하는 대신 필드 용도를 알려줍니다. (SITES-25212)
* 이제 Assets 사이드 레일은 화면 판독기에서 장식 썸네일을 숨깁니다. 사용자가 자산 그리드를 탐색할 때 더 이상 자산 이름을 두 번 듣지 않습니다. (SITES-25213)
* 이제 필터 레일의 아코디언 단추에 충분한 대비로 포커스 표시기가 표시됩니다. 키보드 사용자는 필터 범주를 탐색하는 동안 포커스를 추적할 수 있습니다. (SITES-24986)
* 이제 필터 레일에 라디오 버튼 주위에 키보드 포커스가 지워져 표시됩니다. 증가된 대비는 사용자가 필터 옵션에서 위치를 추적하는 데 도움이 됩니다. (SITES-24987)
* 이제 필터 페이지에서 상태 메시지를 로드하면 최소 텍스트 대비 요구 사항이 충족됩니다. 사용자가 카드 보기와 목록 보기 간을 전환하는 동안 진행률 피드백을 읽을 수 있습니다. (SITES-24991)
* 이제 편집기 캔버스의 페이지 제목에서는 의미 체계 제목 마크업을 사용합니다. 보조 기술은 제목을 알리고 제목 탐색에 포함할 수 있습니다. (SITES-24993)
* 이제 에뮬레이터 메뉴를 확장하면 키보드 포커스가 첫 번째 메뉴 항목으로 이동합니다. 메뉴를 축소하면 포커스가 논리적 보조 도구 모음 시퀀스 내에 유지됩니다. (SITES-24954)
* 이제 라이브 뷰 테이블의 텍스트가 최소 대비 요구 사항을 충족합니다. 사용자는 일반 및 마우스로 가리키면 라이브 카피 세부 사항을 명확하게 읽을 수 있습니다. (SITES-24956)
* 이제 참조 레일에서 제목에 의미 체계 제목 마크업을 사용합니다. 화면 판독기는 초기 로드 중 및 사용자가 폴더를 탐색하는 동안 머리글을 알려줍니다. (SITES-24967)
* 이제 카드 링크가 대상을 명확하게 설명합니다. 화면 판독기 사용자는 카드의 전체 메타데이터를 듣지 않고도 각 링크를 식별할 수 있습니다. (SITES-24975)
* 머리글 메뉴 단추는 더 이상 화면 판독기에 대화 상자를 열었다는 것을 알리지 않습니다. 대신 화면 판독기는 각 단추의 확장 또는 축소 상태를 알려주므로 메뉴 동작을 정확하게 설명합니다. (SITES-24742)
* 이제 삭제 단추의 텍스트가 빨간색 배경에 대해 충분한 대비를 제공합니다. 사용자는 삭제를 확인하기 전에 작업을 보다 쉽게 식별할 수 있습니다. (SITES-24772)
* 캔버스 카드는 더 이상 동일한 대상으로 이어지는 별도의 이미지 및 제목 링크를 노출하지 않습니다. 단일 링크를 사용하면 중복 키보드 중지 및 반복적인 화면 판독기 알림이 줄어듭니다. (SITES-24947)
* 이제 목록 보기에 시각적 효과가 더 뛰어난 드래그 앤 드롭 버튼이 표시됩니다. 업데이트된 아이콘 크기, 두께 및 대비를 통해 컨트롤을 쉽게 찾고 사용할 수 있습니다. (SITES-24951)
* 이제 헤더 단추에 검색, 앱, 도움말, 받은 편지함 및 사용자와 같은 간결한 액세스 가능한 이름이 제공됩니다. 화면 판독기에 키보드 탐색 중에 &quot;클릭 가능&quot; 또는 &quot;그래픽&quot;과 같은 중복 용어가 더 이상 표시되지 않습니다. (SITES-24715)
* 이제 앱 탐색의 링크에 더 강한 시각적 강조가 표시됩니다. 텍스트 크기 및 무게가 증가하면 시력이 낮거나 색각 차이가 있는 사용자의 가독성이 향상됩니다. (SITES-24723)
* 이제 받은 편지함 링크에서 의미 목록 마크업을 사용합니다. 화면 판독기는 링크를 관련 그룹으로 식별하고 항목 수를 알려주며 보다 효율적인 탐색을 지원할 수 있습니다. (SITES-24730)
* 이제 사용자 환경 설정 대화 상자의 도구 설명 컨트롤에 설명적인 액세스 가능한 이름이 표시됩니다. 화면 판독기는 도구 설명 내용을 읽기 전에 &quot;공백&quot;이라고 하지 않고 각 컨트롤의 목적을 알려줍니다. (SITES-24732)
* 이제 각 필터 레일 랜드마크에는 액세스 가능한 고유한 레이블이 포함됩니다. 화면 판독기는 필터 레일을 다른 페이지 영역과 구별하고 탐색 중에 식별할 수 있습니다. (SITES-24686)
* 이제 편집기 대화 상자에서 도움말 및 전체 화면 전환 버튼을 제목 요소에서 분리합니다. 화면 판독기는 이러한 대화형 컨트롤을 정확하게 식별하므로 더 이상 제목으로 알려주지 않습니다. (SITES-24696)
* 이제 CSV 보고서 버튼은 새 브라우저 탭을 열기 전에 사용자에게 경고합니다. 이 레이블은 활성화하기 전에 화면 판독기 및 키보드 사용자에게 동작을 전달합니다. (SITES-24704)
* 이제 필터 레일이 저장된 검색 및 검색 디렉토리 선택을 위한 레이블을 일관되게 로드합니다. 필터 버튼은 포커스, 키보드 또는 마우스 상호 작용 중에 더 이상 레이블 요소를 삽입하지 않습니다. (SITES-24706)
* 이제 [닫기] 및 [위치 제거] 단추를 사용하여 더 큰 터치 대상을 제공합니다. 사용자는 인접한 요소를 선택하지 않고도 두 제어 중 하나를 보다 안정적으로 활성화할 수 있습니다. (SITES-24530)
* 위치 제거 버튼과 포커스 표시기가 이제 최소 대비 요구 사항을 충족합니다. 보다 강력한 대비는 사용자가 컨트롤을 식별하고 키보드 포커스를 추적하는 데 도움이 됩니다. (SITES-24531)
* 이제 편집기 iframe에는 캔버스, 사이드 레일, 구성 요소 대화 상자 및 레이아웃 미리 보기에 대한 설명 제목이 포함됩니다. 화면 판독기는 포커스가 들어갈 때 각 프레임을 식별할 수 있습니다. (SITES-24650)
* 텍스트 대비가 개선되어 참조 레일 메시지를 보다 쉽게 읽을 수 있습니다. 이 변경 사항은 선택을 요청하거나 사용할 수 없는 참조를 보고하는 프롬프트를 명확히 합니다. (SITES-24666)
* 구성 요소 패널은 각 정보 아이콘에 액세스 가능한 의미 있는 레이블을 제공합니다. 화면 판독기는 구성 요소 설명을 표시하는 컨트롤을 일관되게 식별합니다. (SITES-24500)
* 이제 키보드 포커스가 Byline의 설명 표시 단추 전체를 둘러싸고 있습니다. 표시되는 윤곽선은 사용자가 위치를 추적하고 다른 컨트롤을 활성화하지 않도록 도와줍니다. (SITES-24503)
* 티저 구성 요소 대화 상자는 도움말 및 전환 전체 화면 단추를 더 이상 제목으로 노출하지 않습니다. 화면 판독기는 두 컨트롤을 단추로 표시하고 올바른 제목 구조를 유지합니다. (SITES-24525)
* Adobe Experience Manager 헤더 컨트롤은 확장되거나 축소된 상태를 올바르게 보고합니다. 컨트롤은 탐색 콘텐츠를 열고 닫으므로 화면 판독기에서 유효한 상태 정보를 받습니다. (SITES-24528)
* 필터 결과 지구본 아이콘을 장식용으로 표시하고 액세스 가능한 이름을 제거합니다. 화면 판독기는 오해의 소지가 있는 설명을 알리는 대신 아이콘을 무시합니다. (SITES-3057)
* [시간 비틀기] 대화 상자에서 이제 시간 입력 오류를 해당 시간 또는 분 필드와 연결합니다. 화면 판독기는 유효성 검사 메시지와 함께 영향을 받는 필드를 알려줍니다. (SITES-10980)
* 선택한 콘텐츠 트리 항목이 더 이상 변경 파일 또는 폴더 제어 레이블의 일부가 아닙니다. 화면 판독기에서 추가 상태 텍스트 없이 명확한 제어 이름을 들을 수 있습니다. (SITES-24496)
* 이제 Assets 측면 레일의 지역 랜드마크는 액세스 가능한 고유한 이름을 노출합니다. 화면 판독기 사용자는 각 영역을 모호하지 않고 식별하고 탐색할 수 있습니다. (SITES-24497)
* 이제 화면 판독기에서 슬라이드 대화 상자의 장식용 도움말 및 전체 화면 아이콘을 무시합니다. 키보드 탐색이 더 이상 불필요한 아이콘 알림을 트리거하지 않습니다. (SITES-2912)
* 이제 화면 판독기에서 티저 대화 상자의 장식 도구 모음 아이콘을 건너뜁니다. 도움말, 전체 화면, 서식 지정 및 링크 컨트롤은 더 이상 중복 알림을 생성하지 않습니다. (SITES-2934)


#### 관리자 사용자 인터페이스{#sites-adminui-65-lts-sp3}

* 이제 AEM을 사용하여 관리 그룹의 구성원이 페이지의 잠금을 해제하고 사용자를 가장할 수 있습니다. 그룹 구성원은 기존 액세스를 통해 두 관리 작업을 모두 완료할 수 있습니다. (SITES-14732)
* 이제 작성자가 타임라인에서 **이 버전으로 되돌리기**&#x200B;를 선택하면 Assets 관리 보기에서 에셋 카드를 업데이트합니다. 썸네일에 복원된 버전이 즉시 표시되고 더 이상 오래된 미리보기 콘텐츠가 표시되지 않습니다. (SITES-46590)


#### 클래식 사용자 인터페이스{#sites-classicui-65-lts-sp3}

인도네시아어 언어 복사 속성에 올바른 ID 언어 코드가 표시됩니다. 작성자가 인도네시아어 사본을 만들거나 검토할 때 참조 레일이 더 이상 IN을 대체하지 않습니다. (SITES-44918)


#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp3}

이제 사용자가 검색 필터를 적용할 때 Assets 콘솔이 응답합니다. 콘텐츠 조각 모델 필터를 변경하면 현재 에셋 목록을 변경하지 않고 결과가 새로 고쳐집니다. (SITES-38686) 메이저


#### [!DNL Content Fragments] - 관리자{#sites-admin-65-lts-sp3}

* 이제 Assets 페이지에서 잠긴 콘텐츠 조각에 대한 도구 설명을 현지화합니다. 사용자가 잠금 표시기를 마우스로 가리키면 번역된 **체크아웃한 사람** 레이블이 표시됩니다. (SITES-42531) 메이저

* AEM은 콘텐츠 조각을 만드는 동안 잘못된 이름 제공 유효성 검사 메시지를 현지화합니다. 지원되지 않는 제목 문자는 더 이상 영어가 아닌 인터페이스에서 영어 텍스트를 트리거하지 않습니다. (SITES-19796)
* AEM은 콘텐츠 조각을 만드는 동안 콘텐츠 조각 모델 문자열을 번역합니다. Assets 인터페이스에서는 현지화된 환경에서 해당 레이블에 대한 영어 텍스트가 더 이상 표시되지 않습니다. (SITES-22336)
* 콘텐츠 조각 서비스가 더 이상 사용되지 않는 기능 전환 논리에 의존하지 않습니다. 간소화된 구현은 전환 종속 분기를 제거하고 서비스 팩 동작을 일관되게 유지합니다. (SITES-38688)
* AEM은 예약된 콘텐츠 조각을 게시하는 동안 나중에 옵션을 번역합니다. 게시 작업 과정은 활성 인터페이스 언어와 일치합니다. (SITES-42532)
* AEM은 콘텐츠 조각 다운로드 대화 상자에서 기본 문자열을 번역합니다. 요소 섹션은 활성 인터페이스 언어와 일치합니다. (SITES-42534)


#### [!DNL Content Fragments] - 조각 편집기{#sites-fragments-editor-65-lts-sp3}

* 이제 콘텐츠 조각 편집기에서 리치 텍스트 편집기 드롭다운 메뉴를 올바르게 배치합니다. 각 메뉴는 도구 모음 컨트롤과 정렬된 상태를 유지하고 주변 서식 컨트롤을 표시합니다. (SITES-44005) 중요

* 이제 콘텐츠 조각 편집 버튼이 나타나고 참조 다중 필드 항목에 대해 즉시 작동합니다. 작성자는 임베드된 조각을 편집하기 전에 상위 콘텐츠 조각을 더 이상 저장하고, 닫고, 다시 열 필요가 없습니다. (SITES-43733) 메이저

* 작성자가 여러 줄 텍스트 필드를 선택하면 콘텐츠 조각 편집기에 하나의 포커스 개요가 표시됩니다. 윤곽선이 더 이상 주변 컨트롤과 중복되거나 겹치지 않습니다. (SITES-39253)
* 콘텐츠 조각 생성은 기울임꼴 스타일을 지정하지 않고 CJK 자리 표시자 텍스트를 표시합니다. 일본어, 한국어, 중국어 간체, 중국어 번체 문자는 의도한 모양을 유지하고 있습니다. (SITES-43548)
* 콘텐츠 조각 편집기는 작성자가 조각을 저장하거나 게시한 후 상태 배너를 새로 고칩니다. 작성자는 브라우저 탭을 다시 로드하지 않고 수정됨, 저장됨 또는 게시됨 상태를 확인할 수 있습니다. (SITES-45897)
* 콘텐츠 조각 편집기는 Granite UI가 변경된 후에도 필드를 일관되게 확인합니다. 업데이트된 클라이언트 라이브러리는 예상 유효성 검사 동작을 복원합니다. (SITES-46650)


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp3}

* 이제 DAM 파일 이름에 공백 또는 비 ASCII 문자가 포함된 경우 GraphQL JSON 응답에 포함된 이미지 참조가 포함됩니다. 클라이언트 애플리케이션은 에셋의 이름을 변경하지 않고 이러한 이미지를 검색하고 렌더링할 수 있습니다. (SITES-42191) 메이저
* 이제 콘텐츠 조각 GraphQL API에 여러 쿼리 처리 및 응답 처리 업데이트가 포함됩니다. 변경 사항은 중복 캐시 헤더 및 값을 방지하고, 인코딩을 개선하고, 지속 쿼리 상태 정보를 유지하며, 빈 헤더를 처리하고, 적절한 끝점 오류를 반환합니다. (SITES-40159) 메이저
* 이제 PersistedQueryServlet은 false 오류나 경고를 기록하지 않고 유효한 GraphQL 지속 쿼리에서 인코딩된 변수를 처리합니다. 쿼리는 로그가 실제 실행 상태를 반영하는 동안 성공적인 응답을 계속 반환합니다. (SITES-39354) 메이저

* GraphQL 엔드포인트 페이지를 다시 로드하면 현지화된 빈 상태 메시지가 유지됩니다. 끝점이 존재하지 않으면 페이지는 더 이상 영어로 되돌아가지 않습니다. (SITES-43586)


<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp3}-->


#### [!DNL Content Fragments] - 모델 편집기{#sites-model-editor-65-lts-sp3}

* 이제 콘텐츠 조각 모델 콘솔에는 이름에 현지화된 문자가 포함된 구성에 대해 업로드된 썸네일이 표시됩니다. 구성 이름이 영어가 아닌 텍스트를 사용하는 경우 작성자가 더 이상 축소판 미리 보기를 손실하지 않습니다. (SITES-39242) 메이저

* 콘텐츠 조각 모델 편집기는 작성자가 구성 요소를 캔버스에 추가하는 즉시 현지화된 **필드 레이블** 텍스트를 표시합니다. 작성자는 더 이상 번역을 보기 위해 모델을 저장하고 다시 열 필요가 없습니다. (SITES-45383)
* 콘텐츠 조각 모델 편집기 는 작성자가 복합 구성 요소에 대해 잘못된 모델 유형을 선택할 때 표시되는 유효성 검사 메시지를 현지화합니다. 이제 메시지가 영어로만 표시되지 않고 활성 로케일과 일치합니다. (SITES-41117)
* 콘텐츠 조각 모델 편집기는 모델이 잠겨 있음 대화 상자의 모든 텍스트를 현지화합니다. 이 대화 상자에서는 영어 단추 레이블 및 지침을 번역된 인터페이스 텍스트와 더 이상 혼합하지 않습니다. (SITES-28592)



#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp3}

Headless 콘텐츠 조각 REST API 번들은 사용되지 않는 기능 전환 및 관련 조건부 코드를 제거합니다. 지원되는 API 동작은 변경되지 않지만 번들은 활성 기능에 필요한 전환만 유지합니다. (SITES-39113)



#### 구성 요소 콘솔{#sites-component-console-65-lts-sp3}

이제 컨텐츠 파인더에 실패하거나 예외를 생성하지 않고, 이름에 인코딩할 수 없는 문자가 포함된 자산이 나열됩니다. 또한 구성 요소 라이브 사용량 페이지는 스크롤하는 동안 빈 행을 표시하지 않고 큰 결과 세트를 연속적으로 로드합니다. (SITES-44672) 메이저

<!--
#### Content API{#sites-content-api-65-lts-sp3}

#### Core backend{#sites-core-backend-65-lts-sp3}
-->

#### 핵심 구성 요소{#sites-core-components-65-lts-sp3}

* 이제 다중 필드 구성 요소는 각 항목에 대해 별도의 원격 자산 선택을 저장합니다. 작성자는 모든 다중 필드 항목에 하나의 이미지를 복제하지 않고 원격 이미지를 선택, 변경 및 저장할 수 있습니다. (SITES-42376) 메이저
* 이제 ThumbnailServlet이 누락된 리소스에 대한 요청을 리디렉션한 후 처리를 중지합니다. 이 변경 사항은 DAM 및 콘솔 검색 중에 반복되는 null 포인터 예외와 과도한 오류 로깅을 방지합니다. (SITES-41238) 메이저


#### Campaign 통합{#sites-campaign-integration-65-lts-sp3}

이제 Campaign ContentServlet은 콘텐츠 요청 중에 JSON 응답 콘텐츠 유형을 유지합니다. 이 변경 사항은 AEM 6.5.24에서 업그레이드한 후 발생한 반복된 `WARN` 및 `ERROR` 로그 항목을 중지합니다. (SITES-46902) 메이저


#### 경험 조각{#sites-experiencefragments-65-lts-sp3}

이제 작성자가 경험 조각 변형을 만드는 동안 40개 이상의 템플릿을 검색할 수 있습니다. 각 추가 페이지는 원래 폴더 필터를 유지하고 일치하는 다음 템플릿을 표시합니다. (SITES-41531) 메이저


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp3} -->


#### 론치{#sites-launches-65-lts-sp3}

이제 Launch 홍보 기록에 Sites 타임라인에 현지화된 텍스트가 표시됩니다. 타임라인은 지원되는 로케일에서 &quot;의 버전 생성됨&quot; 및 &quot;출시 홍보 전&quot;이라는 메시지를 번역합니다. (SITES-13389)


<!-- #### Link Checker{#sites-link-checker-65-lts-sp3} -->



#### MSM - Live Copy{#sites-msm-live-copies-65-lts-sp3}

* 작성자가 변경되지 않은 속성을 저장하면 콘텐츠 조각 Live Copy 폴더는 이제 cq:rolloutConfigs을(를) 유지합니다. 작성자는 나중에 기존 구성을 손실하지 않고 롤아웃 설정을 업데이트할 수 있습니다. (SITES-43729) 중요

* 작성자는 이제 블루프린트 페이지의 편집 가능한 도구 모음에서 구성 요소 변경 사항을 롤아웃할 수 있습니다. 롤아웃은 JavaScript 오류 없이 완료되고 변경 사항을 라이브 카피로 전파합니다. (SITES-46052) 메이저
* 이제 작성자는 업그레이드 후 블루프린트 페이지에서 MSM 롤아웃을 완료할 수 있습니다. 롤아웃 대화 상자는 사용 가능한 라이브 카피를 로드하며 지속적인 로드 상태를 유지하는 대신 해당 롤아웃 컨트롤을 활성화합니다. (SITES-43116) 메이저

* 이제 Live Copy 개요가 관계 상태 전체에 현지화된 날짜 형식을 적용합니다. **Live Copy Source 마지막 수정 날짜**, **Live Copy 마지막 수정 날짜** 및 **마지막 롤아웃** 필드가 사용자의 로케일과 일치합니다. (SITES-40756)
* 한 요청에서 블루프린트 상위 및 하위 페이지를 비활성화하면 이제 경로당 하나의 롤아웃 이벤트가 생성됩니다. 롤아웃 관리자는 더 이상 동일한 하위 페이지에 대해 중복 작업을 실행하지 않습니다. (SITES-44987)


#### 페이지 편집기{#sites-pageeditor-65-lts-sp3}

* 이제 작성자는 하나의 페이지 속성을 저장하는 동안 대문자 또는 공백이 포함된 태그를 만들어 적용할 수 있습니다. AEM은 표준화된 태그 값을 즉시 저장하고 페이지 할당을 유지합니다. (SITES-42550) 중요

* 스타일 메뉴를 스크롤해도 선택한 스타일에서 더 이상 강조 표시가 제거되지 않습니다. 작성자는 사용 가능한 다른 옵션을 검토하면서 현재 선택한 항목을 확인할 수 있습니다. (SITES-30874) 메이저

* 이제 작성자가 HTTP를 통해 AEM에 액세스하면 리치 텍스트 편집기 링크 버튼이 열립니다. 링크 만들기가 더 이상 `crypto.randomUUID` 오류를 트리거하지 않습니다. (SITES-39467)
* 이제 작성자는 구성된 콘텐츠 조각 구성 요소를 복사하여 빈 레이아웃 컨테이너에 붙여넣을 수 있습니다. 붙여넣은 구성 요소는 원래 콘텐츠 조각 참조를 유지하고 더 이상 *경험 변형 선택* 오류를 표시하지 않습니다. (SITES-41586)
* 이제 이미지 편집기에서 하이브리드 인라인 편집 중 사용자 지정 자르기 비율을 적용합니다. 각 이미지 드롭 대상은 자체 구성을 사용하므로 전체 화면 모드 외부에서 올바른 방식으로 자르기 선택이 적용됩니다. (SITES-45771)

<!--
#### Replication{#sites-replication-65-lts-sp3}

#### Rich Text Editor{#sites-rte-65-lts-sp3}

#### Template Editor{#sites-template-editor-65-lts-sp3}

#### Universal editor {#sites-universal-editor-65-lts-sp3}

### [!DNL Assets]{#assets-65-lts-sp3}

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp3}

#### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp3}
-->



<!--
### [!DNL Forms]{#forms-65-lts-sp3}
-->



### 기초 {#foundation-65-lts-sp3}

#### AEM 컨텍스트 서비스 {#foundation-aem-context-service-65-lts-sp3}

AEM 6.5 LTS는 AEM 컨텍스트 서비스 지원을 도입했습니다. 롤아웃은 서비스 API, 에이전트 통합, AMS 프로비저닝, Experience Cloud 통합, 프로덕션 모니터링, 운영 Runbook 및 사용 보고를 추가합니다. (GRANITE-65148)

#### Apache Felix {#foundation-apachefelix-65-lts-sp3}

이제 간헐적인 구성 오류가 발생하면 AEM 메일 서비스에서 이메일을 계속 보냅니다. 관리자는 더 이상 이메일 게재를 복원하기 위해 Day Communique 5 Mailer 번들을 다시 시작할 필요가 없습니다. (GRANITE-66817) 메이저

<!--
#### Campaign{#foundation-campaign-65-lts-sp3}

#### Cloud Services{#foundation-cloudservices-65-lts-sp3}

#### Communities {#foundation-communities-65-lts-sp3}

#### Content distribution{#foundation-content-distribution-65-lts-sp3}

#### CRX {#foundation-crx-65-lts-sp3}

#### Granite{#foundation-granite-65-lts-sp3}

#### HTL{#foundation-htl-5-lts-sp3}

#### Integrations{#foundation-integrations-65-lts-sp3}

#### Jetty{#foundation-jetty-65-lts-sp3}
-->

#### 현지화{#foundation-localization-65-lts-sp3}

* 이제 작업 콘솔은 상태 보고서 간에 이전에 번역되지 않은 텍스트를 현지화합니다. 사용자는 번역된 상태 메시지, 경고, 유지 관리 결과 및 성능 정보를 볼 수 있습니다. (NPR-44280) 메이저

* 이제 감사 로그 유지 관리 작업에 현지화된 면책조항이 표시됩니다. 관리자는 자동화된 감사 로그 삭제를 구성하기 전에 선택한 언어로 규정 준수 및 법률 지침을 확인합니다. (NPR-44188)
* 이제 사용자가 수정된 프로필을 재정렬할 때 사용자 편집 페이지에 현지화된 오류가 표시됩니다. 이 메시지는 사용자가 변경 사항을 저장할 때까지 변경된 프로필을 이동할 수 없음을 명확하게 설명합니다. (NPR-44282)
* 이제 AEM은 콘텐츠 조각 목록 속성 전체에서 도구 설명을 현지화합니다. 번역된 안내서에서는 모델 선택, 태그 필터링, 콘텐츠 경로, 항목 제한 및 정렬 설정에 대해 설명합니다. (SITES-14969)
* 이제 템플릿 편집기의 구성 요소 도움말 링크에 현지화된 설명서가 열립니다. 작성자는 영어 전용 구성 요소 페이지 대신 선택한 언어와 일치하는 지침에 도달합니다. (SITES-15058)
* 이제 구성 요소 정책 편집기는 수정할 수 없는 리소스 또는 노드 생성 실패를 보고하는 오류를 현지화합니다. 템플릿 작성자는 선택한 언어로 이러한 메시지를 수신합니다. (SITES-17475)

<!-- #### Omnisearch{#foundation-omnisearch-65-lts-sp3} -->

#### 작업 대시보드{#foundation-operations-dashboard-65-lts-sp3}

이제 고객이 AEM LTS를 업그레이드한 후에도 `/system/health/systemalive.json` 끝점을 사용할 수 있습니다. 수정된 서블릿 컨텍스트 구성은 HTTP 404 응답을 방지하고 끝점에 의존하는 상태 모니터링 시스템을 지원합니다. (GRANITE-69457) 심각

#### Platform{#foundation-platform-65-lts-sp3}

이제 기본 HTL 표현식-옵션 허용 목록에서 `decorationTagName` 및 `cssClassName`을(를) 인식합니다. 표준 반응형 그리드를 렌더링하는 경우 더 이상 알 수 없는 옵션 경고가 반복되어 `error.log`을(를) 채우지 않습니다. (GRANITE-67152)

<!--
#### Projects{#foundation-projects-65-lts-sp3}

#### Oak {#foundation-oak-65-lts-sp3}

#### Quickstart{#foundation-quickstart-65-lts-sp3} 
-->


#### 보안{#foundation-security-65-lts-sp3}

**그룹 복사** 작업에서 빈 페이지를 표시하는 대신 필요한 양식이 열립니다. 관리자는 새 그룹 ID와 설명을 입력한 다음 기존 보안 그룹을 복제할 수 있습니다. (NPR-44302) 메이저


<!-- #### Sling{#foundation-sling-65-lts-sp3} -->


#### 번역{#foundation-translation-65-lts-sp3}

이제 번역 프로젝트는 워크플로 진행에 따라 정확한 상태 수를 유지합니다. 시작 만들기 및 상태 전파는 예상 워크플로 동작을 따르므로 일관되지 않은 프로젝트 메타데이터가 제거됩니다. (NPR-43420)


#### 사용자 인터페이스{#foundation-ui-65-lts-sp3}

* 이제 국가/지역 레이블이 선택한 인터페이스 언어로 표시됩니다. 지역화된 인터페이스에 더 이상 영어 레이블이 표시되지 않습니다. (NPR-43883)
* 형제 페이지를 선택하면 복합 다중 필드 경로 선택기에서 **선택**&#x200B;이(가) 활성화됩니다. 작성자는 브라우저 창을 확대하거나 선택 내용을 반복하지 않고 새 경로를 확인할 수 있습니다. (GRANITE-69323)


<!-- #### WCM{#foundation-wcm-65-lts-sp3} -->


#### 워크플로{#foundation-workflow-65-lts-sp3}

* 이제 워크플로우 패키지 페이지에서 Touch UI 페이지 편집기에서 콘텐츠 트리 및 편집 가능한 리소스 정의 구성 요소를 지원합니다. 작성자는 클래식 UI를 사용하지 않고 패키지 콘텐츠를 탐색하고 해당 구성 요소를 검사하거나 업데이트할 수 있습니다. (GRANITE-67348) 메이저
* 이제 Touch UI 페이지 편집기에서 워크플로 패키지 페이지의 콘텐츠 트리를 렌더링합니다. 작성자는 동일한 편집기를 통해 패키지 구조를 검사하고 리소스 정의 구성 요소를 편집할 수 있습니다. (GRANITE-67186) 메이저

* 이제 워크플로우 변수 대화 상자에 양식 데이터 모델, JSON, XML 및 문서 변수에 대한 올바른 컨트롤이 표시됩니다. 작성자가 이러한 비원시 변수를 만들 때 원시 HTML 마크업을 더 이상 보지 않습니다. (GRANITE-67915)



## [!DNL Experience Manager Foundation] 정보 {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS의 플랫폼은 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix)와 Java™ 콘텐츠 저장소인 Apache Jackrabbit Oak 1.68.x의 업데이트된 버전을 기반으로 빌드되었습니다.

Eclipse Jetty 11.0.x는 Quickstart의 서블릿 엔진으로 사용됩니다.

### Java™ 지원  {#java-support}

* Java™ 17 및 Java™ 21이 지원됩니다.
* 최적의 성능을 위해 기본 GC 값을 다른 값으로 재정의합니다. 자세한 내용은 [설치 및 업데이트](/help/sites-deploying/custom-standalone-install.md) 섹션을 참조하십시오.
* Adobe는 Oracle에서 공개적으로 제공되지 않는 경우 AEM 관련 프로젝트에서 고객이 사용할 수 있도록 Java™ 17 및 Java™ 21 유지 관리 업데이트를 배포합니다.

### Uberjar 패키징 {#uber-jar-packaging}

AEM 6.5 LTS SP3용 UberJar는 AEM 6.5 LTS UberJar 버전 6.6.3을 사용합니다. Maven 중앙 저장소에서 해당 UberJar 아티팩트를 검색할 수 있습니다. AEM 6.5와 달리 AEM 6.5 LTS는 공개 API와 더 이상 사용되지 않는 API를 두 개의 서로 다른 아티팩트로 구분합니다.

공개 API에 대해 컴파일하려면 다음을 사용하십시오.

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.3</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

코드도 더 이상 사용되지 않는 API에 따라 달라지는 경우 다음을 추가하십시오.

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.3</version>
    <classifier>deprecated-apis</classifier>
    <scope>provided</scope>
</dependency>
```

또한 [AEM Uber Jar 버전 업데이트](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)를 참조하십시오.

### 업그레이드 {#upgrade}

* 업그레이드 절차에 대한 자세한 내용은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.
* 자세한 업그레이드 지침은 [JEE의 AEM Forms 6.5 LTS SP1 업그레이드 안내서](https://experienceleague.adobe.com/ko/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade) 참조

## AEM 6.5 LTS 서비스 팩 업그레이드에 대한 모범 사례

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

적용 대상: AEM 6.5 LTS(온-프레미스) 고객이 서비스 팩 3(SP3)을 설치하는 경우 SP3는 Quickstart JAR로 제공됩니다.

**이러한 업그레이드 사례가 중요한 이유**
AEM 6.5 LTS용 SP2가 패키지 관리자를 통해 설치하기 위해 ZIP이 아닌 Quickstart JAR로 제공됩니다. On-Premise 고객은 Quickstart JAR를 교체하고 압축을 푼 다음 다시 시작하여 업그레이드합니다. 이 방법은 Adobe의 표준 업그레이드 절차와 일치합니다.


**권장 업그레이드 흐름(작성자 또는 게시)**

1. AEM 6.5 LTS 인스턴스가 정상적이고 액세스할 수 있는지 확인합니다.
1. 소프트웨어 배포에서 Quickstart JAR(예: `cq-quickstart-6.6.x.jar`)을 다운로드합니다.
1. 실행 중인 인스턴스를 중단합니다.
1. `crx-quickstart/` 외부 AEM 설치 디렉터리에서 이전 Quickstart JAR를 SP3 JAR로 바꿉니다.
1. JAR 압축을 풉니다.

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   (필요에 따라 힙 플래그를 조정합니다.)

1. 역할 및 포트와 일치하도록 압축 해제된 JAR의 이름을 변경합니다(예: `cq-author-4502.jar` 또는 `cq-publish-4503.jar`).
1. AEM을 시작하고 UI(도움말 > 정보) 및 로그에서 업그레이드를 확인합니다.

**모범 사례**

* 프로덕션 전에 하위 / 테스트 환경에서 업그레이드를 실행합니다.
* 시작하기 전에 복원 가능한 전체 백업(저장소와 모든 외부 데이터 저장소)을 수행합니다.
* Adobe의 즉석 업그레이드 지침 및 기술 요구 사항(LTS에 대해 Java 17/21 권장)을 검토합니다.

>[!NOTE]
>
>위에 표시된 파일 이름(예: `cq-quickstart-6.6.x.jar`)은 이 LTS 릴리스에서 관찰된 Quickstart 아티팩트 이름을 반영하므로 항상 소프트웨어 배포에서 다운로드한 정확한 파일 이름을 사용하십시오.

## 설치 및 업데이트{#install-update}

설정 요구 사항에 대한 자세한 내용은 [설치 지침](/help/sites-deploying/custom-standalone-install.md)을 참조하십시오.

>[!NOTE]
>
> 이전 6.5 SP에서 LTS SP1로 직접 업그레이드하는 경우 6.5에서 6.5 LTS GA [업그레이드](/help/sites-deploying/upgrade.md)하는 데 제공된 지침을 따르십시오.


자세한 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하세요. 동일한 설명서는 LTS 서비스 팩 업데이트에 적용됩니다.

>[!NOTE]
>
> 새 AEM 6.5 LTS 설치의 경우 인덱스 정의를 별도로 설치해야 합니다. 더 자세한 내용은 [이 문서](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)를 참조하십시오.

## AEM Forms 추가 기능 설치 및 업데이트 {#install-update-aem-forms-add-on}

자세한 지침은 [인플레이스 업그레이드 수행](https://experienceleague.adobe.com/ko/docs/experience-manager-65/content/release-notes/aem-forms-current-service-pack-installation-instructions)을 참조하십시오.


## 지원되는 플랫폼 {#supported-platforms}

[AEM 6.5 LTS 기술 요구 사항](/help/sites-deploying/technical-requirements.md)에서 지원 수준을 포함한 전체 지원 플랫폼 매트릭스를 찾을 수 있습니다.

>[!NOTE]
>
>Java™ 17/Java™ 21은 AEM 6.5 LTS와 함께 사용하는 것이 권장되는 버전입니다.


## 더 이상 사용되지 않는 기능과 제거된 기능 {#deprecated-and-removed-features}

<!-- CARRY OVER EACH RELEASE -->

Adobe는 이전 기능을 현대화하거나 대체하여 더 큰 고객 가치를 제공하기 위해 제품 기능을 지속적으로 검토하고 발전시킵니다. 이러한 변경 사항을 통해 이전 버전과의 호환성을 신중하게 고려하여 구현됩니다.

Adobe는 투명성을 보장하고 적절한 계획을 수립할 수 있도록 Adobe Experience Manager(AEM)에 대한 이 사용 중단 프로세스를 따릅니다.

* 사용 중단이 먼저 발표됩니다. 더 이상 사용되지 않는 기능은 계속 사용할 수 있지만 추가로 개선되지 않습니다.
* 제거는 다음 주요 릴리스 이후에 수행됩니다. 계획된 제거 타임라인은 별도로 전달됩니다.
* 기능이 제거되기 전에 고객이 지원되는 대체 요소로 전환할 수 있도록 최소 하나의 릴리스 주기가 제공됩니다.

### 더 이상 사용되지 않는 기능 {#deprecated-features}

이 섹션에는 Adobe가 AEM 6.5 LTS에서 더 이상 사용되지 않는 기능이 나열됩니다. 일반적으로 Adobe는 향후 릴리스에서 해당 기능을 제거하기 전에 해당 기능을 더 이상 사용하지 않도록 설정하고 사용할 수 있는 대안을 제공합니다.

고객은 현재 배포에서 이 기능/기능을 사용할지 여부를 검토하는 것이 좋습니다. 제공된 대체 요소를 사용하도록 구현을 변경할 계획을 세우십시오.

| 영역 | 기능 | 대체 | 버전(SP) |
| --- | --- | --- | --- |
| Quickstart | Mongo API | Mongo API는 이제 더 이상 사용되지 않으며 향후 릴리스에서 제거될 예정입니다. | 6.5 TS SP2 |
| Sites | AEM Assets REST API의 콘텐츠 조각 지원 | AEM 6.5 LTS SP2가 콘텐츠 조각 및 모델 관리를 위한 최신 OpenAPI를 제공하므로 AEM Assets REST API의 이전 콘텐츠 조각 지원 엔드포인트는 이제 더 이상 사용되지 않습니다.<br>Adobe는 서비스 종료 공지가 있을 때까지 이러한 이전 엔드포인트를 사용할 수 있도록 유지합니다. Adobe에서는 더 이상 사용되지 않는 엔드포인트에 대한 추가 개선 사항을 계획하지 않습니다. | 6.5 LTS SP2 |
| Sites | [SPA 편집기](/help/sites-developing/spa-overview.md) | AEM에서 헤드리스 콘텐츠 관리에 권장되는 편집기는 <br>- [범용 편집기](/help/sites-developing/universal-editor/introduction.md)(시각적 편집용) <br>- [콘텐츠 조각 편집기](/help/assets/content-fragments/content-fragments-managing.md)(양식 기반 편집용)입니다. | 6.5 LTS GA |
| [!DNL Foundation] | com.adobe.granite.oauth.server 지원 | Adobe IMS 통합 | |

### 제거된 기능 {#removed-features}

이 섹션에는 AEM 6.5 LTS에서 제거된 기능이 나열됩니다. 이전 릴리스에서는 이러한 기능이 더 이상 사용되지 않는다고 표시되었습니다.

* Adobe CRX 저장소 지속성을 위한 RDBMK 지원이 제거되었습니다.
* 클러스터된 환경에서는 이제 MongoMK가 저장소 지속성에 대한 유일한 지원 옵션입니다.

| 영역 | 기능 | 대체 | 버전(SP) |
| --- | --- | --- | --- |
| Sites | 콘텐츠 조각 텍스트 요약 | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS SP3 |
| Commerce | AEM CIF Classic은 지원되지 않습니다. | [AEM CIF](/help/commerce/cif/migration.md)로 마이그레이션합니다. | 6.5 LTS GA |
| 솔루션 | 소셜/커뮤니티는 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| Screens | Screens는 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| 자산 | 번들이 소셜에 종속되므로 `dam-pim` 및 `dam-rating`은 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| 자산 | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()`는 제거되었습니다. | 추가된 대체 API `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()` 를 사용하십시오. | 6.5 LTS GA |
| 포털 | AEM Portal Director는 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| Granite | 번들 `com.adobe.granite.socketio` 는 제거되었습니다 | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| Granite | `com.adobe.granite.crx-explorer`는 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| Granite | `crx2oak`는 지원되지 않습니다. | [Oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade)의 관련 버전을 선택합니다. | 6.5 LTS GA |
| Adobe | `com.adobe.cq.cq-searchpromote-integration`는 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| Guava | 이제 AEM에서 모든 Guava 종속성이 제거되었으므로 `com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` 번들은 AEM의 일부가 아닙니다. | 고객은 Guava에 종속된 경우 직접 추가하거나, 가능한 경우 Guava 코드를 Java 컬렉션 또는 다른 대체 기능으로 바꿀 수 있습니다. | 6.5 LTS GA |
| `We.Retail` | `We-retail` 샘플 사이트는 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| 공개 소스 | `oak-solr-osgi` 번들은 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| 공개 소스 | `org.apache.servicemix.bundles.abdera-parser`, `org.apache.servicemix.bundles.jdom` 및 `org.apache.sling.atom.taglib`은 지원되지 않습니다. | 사용 가능한 대체 기능이 없습니다. | 6.5 LTS GA |
| 공개 소스 | `org.apache.commons.io` 패키지는 이제 `org.apache.commons.commons-io`에서 내보내집니다. | 변경 작업을 수행할 필요가 없습니다. | 6.5 LTS GA |
| 공개 소스 | `javax.mail` 패키지는 이제 `com.sun.javax.mail` 번들에서 내보내집니다. | 변경 작업을 수행할 필요가 없습니다. | 6.5 LTS GA |
| 공개 소스 | `org.apache.jackrabbit.api` 패키지는 이제 `org.apache.jackrabbit.oak-jackrabbit-api` 번들에서 내보내집니다. | 변경 작업을 수행할 필요가 없습니다. | 6.5 LTS GA |
| 공개 소스 | `com.github.jknack.handlebars`는 지원되지 않음 | 관련 [버전](https://mvnrepository.com/artifact/com.github.jknack/handlebars)을 선택합니다. | 6.5 LTS GA |

## 알려진 문제 {#known-issues}

### AEM Forms

* 구성 관리자에서 모듈을 선택하지 않았거나 제한된 구성 요소만 선택한 경우 AEM Forms 6.5 LTS JEE 턴키 사용자 정의 모드의 Bootstrap 중에 데이터베이스 초기화가 실패합니다. 이 실패는 종속성(xalan-2.7.2.jar)이 누락되어 오류가 발생했기 때문입니다. Adobe-livecycle-jboss.ear\lib에 JAR 파일을 추가하면 문제가 해결됩니다. (FORMS-24690)
* WebSphere® Liberty Profile에서 실행되는 Forms JEE LTS 서비스 팩 2 배포에서 이메일 기능이 작동하지 않습니다. 전자 메일 기능을 사용하려고 할 때 서버에서 오류 `Could not convert socket to TLS`을(를) 기록합니다. (FORMS-24692)
* JBoss®에서 실행 중인 Forms JEE LTS에서 이메일 관련 기능이 실패합니다. 전자 메일 기능을 사용하려고 할 때 서버에서 오류 `Error IMAPProvider not a subtype`을(를) 기록합니다. 이 문제를 해결하려면 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-core-jboss.ear)에서 핫픽스를 설치하십시오. (FORMS-24892)

### 오프라인 압축 후 온라인 압축 중 저장소 손상(GRANITE-65146) {#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146}

이전에 JCR 저장소에서 오프라인 압축을 실행한 경우 온라인 압축 중에 저장소 손상이 발생할 수 있습니다. 이 시나리오에서는 `SegmentNotFoundException`(SNFE)이 발생할 수 있으며 이로 인해 저장소가 손상될 수 있습니다.

이 문제를 해결하려면 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-65388-1.0.zip)에서 핫픽스를 설치합니다. 핫픽스에 낮은 수준의 `oak-segment-tar` 번들이 포함되어 있으므로 설치 후 인스턴스가 다시 시작됩니다.

인스턴스 적용 시 다운타임에 대한 계획을 수립합니다. 오프라인 압축을 위해 소프트웨어 배포에서도 사용할 수 있는 해당 [`oak-run` jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar)를 사용합니다.

>[!NOTE]
>
> * `oak-run` 작업의 경우 [`oak-run` 1.88.1-B006 jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar)를 사용합니다.
>
> * 시스템 속성 `oak.compaction.legacy=true`를 설정하여 AEM을 시작합니다.

### AEM 6.5 LTS SP2에 `com.adobe.granite.apicontroller` 번들이 없습니다(GRANITE-67640). {#missing-apicontroller-bundle-granite-67640}

AEM 6.5 LTS SP2에 `com.adobe.granite.apicontroller` 번들이 없습니다. 이 번들은 OSGi 번들이 확인되는 방법을 제어하며 번들이 다른 번들로 확인되지 않도록 할 수 있습니다. 이는 노출된 API를 제한하는 데 유용합니다.

이 기능을 사용하려면 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-67640-1.0.zip)에서 핫픽스를 설치하십시오.

>[!NOTE]
>
> `com.adobe.granite.apicontroller`의 기본 구성에 기존 사용자 지정 구현에 영향을 주는 의도하지 않은 해결 방법 제한이 없는지 확인하려면 핫픽스를 설치한 후 설치된 모든 번들의 번들 상태를 확인하십시오.

### JSON 댓글은 최초 콘텐츠 슬링(SP2)에서 더 이상 지원되지 않음 {#json-comments-no-longer-supported-in-sling-initial-content}

이 문제는 JSON 파일과 함께 `Sling-Initial-Content`를 사용하는 번들을 배포하는 OSGi 번들 개발자 및 관리자에게 영향을 줍니다.

AEM 6.5 LTS SP2부터 `Sling-Initial-Content` 번들에 사용된 JSON 파일에 더 이상 댓글(`//` 또는 `/* */`)이 허용되지 않습니다. 이전 AEM 릴리스에서는 `javax.json` 제공자가 이 문제에 대해 엄격하지 않아 댓글이 허용되었습니다. AEM 6.5 LTS SP2는 `org.apache.sling.jcr.contentloader`를 2.6.0 버전으로 업그레이드했으며 이로 인해 JSON 파서가 `jakarta.json`으로 전환되었습니다. [JSON 사양(RFC 8259)](https://datatracker.ietf.org/doc/html/rfc8259)에서 댓글에 대한 구문을 정의하지는 않지만 이전 AEM 릴리스에서는 `javax.json` 제공자 이 문제에 대해 엄격하지 않아 이를 허용했습니다. `jakarta.json` 제공자가 이 확장 기능을 제공하지 않습니다.

알림 없이 오류 발생: 설치 관리자에 오류가 표시되지 않고 번들 활성화 시 콘텐츠 노드 로드에 실패합니다. SP2로 업그레이드한 후 예기치 않게 콘텐츠가 누락된 경우 OSGi 설치 관리자 로그에서 JSON 구문 분석 오류를 확인하십시오. 영향을 받는 번들을 식별하려면 `Sling-Initial-Content` 매니페스트 헤더 아래에 나열된 JSON 파일 내에서 `//` 또는 `/* */`를 찾습니다.

>[!CAUTION]
>
> AEM 6.5 LTS SP2로 업그레이드한 후 콘텐츠 로드 실패를 방지하려면 `Sling-Initial-Content` 번들의 JSON 파일에서 모든 주석을 제거하십시오.

### Jackson 번들 업그레이드는 GlobalLink 커넥터에 영향을 줍니다. {#jackson-upgrade-globallink-connector}

AEM 6.5 LTS SP3에서 `jackson` 번들을 업그레이드합니다. 이 변경 사항은 GlobalLink 번역 커넥터를 사용하는 배포에 영향을 줍니다.

3.4.0 이전 버전에서 `gs4tr-globallink-adaptors-aem.core` 번들을 사용하는 경우 해당 번들을 호환되는 버전으로 업그레이드하십시오. 버전 3.4.0 이상은 SP3에서 업그레이드된 `jackson` 번들과 함께 작동합니다.

>[!NOTE]
>
> GlobalLink 커넥터와의 호환성 문제를 방지하려면 SP3 업데이트 전이나 업데이트 중에 `gs4tr-globallink-adaptors-aem.core` 번들을 3.4.0 이상으로 업그레이드하십시오.


### Sites Headless API에 필요한 Oak 인덱스 설치{#site-headless-api}

Sites Headless로 이동한 일부 API의 경우 전체 기능을 위해 추가 Oak 인덱스가 필요합니다.

다음 기능을 사용하려면 `cq-dam-cfm-indices` 패키지를 설치하십시오.

* 콘텐츠 조각 모델 목록
* 콘텐츠 조각 목록
* API 검색
* 워크플로

Adobe 소프트웨어 배포 포털에서 인덱스 패키지 [cq-dam-cfm-indexes](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fcq-dam-cfm-indices-1.1.5.zip)를 다운로드합니다.

### SSL 전용 기능을 사용한 Dispatcher 연결 실패(AEM 6.5 LTS SP1 이상에서 수정됨){#ssl-only-feature}

>[!NOTE]
>
> 이 문제는 AEM 6.5 LTS GA 릴리스에서만 발생합니다.

AEM 배포에서 SSL 전용 기능을 활성화하면 Dispatcher와 AEM 인스턴스 간의 연결에 영향을 미치는 알려진 문제가 있습니다. 이 기능을 활성화하면 상태 검사가 실패하고 Dispatcher과 AEM 인스턴스 간의 통신이 중단됩니다. 이 문제는 고객이 Dispatcher에서 AEM 인스턴스로 `https + IP`를 통해 연결을 시도할 때 발생합니다. 이는 SNI(서버 이름 표시) 유효성 검사 문제와 관련이 있습니다.

**영향**

* HTTP 400 응답 코드로 인한 상태 검사 실패.
* Dispatcher와 AEM 인스턴스 간의 손상된 트래픽.
* Dispatcher를 통해 콘텐츠를 제대로 제공할 수 없음.
* Dispatcher 구성에서 IP 주소로 HTTPS를 사용할 때 연결 실패.
* HTTPS + IP를 통해 연결할 때 HTTP 400 “잘못된 SNI” 오류.

**영향을 받는 환경**

* Dispatcher 구성을 사용한 AEM 배포.
* SSL 전용 기능이 활성화된 시스템.
* AEM 인스턴스에 대한 `https + IP` 연결 방법을 사용하는 Dispatcher 구성.

**솔루션**

이 문제가 발생하는 경우 Adobe 고객 지원 센터에 문의하십시오. 이 문제를 해결하기 위해 핫픽스 [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip)이 제공됩니다. 필요한 핫픽스를 적용하기 전에는 SSL 전용 기능을 활성화하지 마십시오.

## OSGi 번들 및 콘텐츠 패키지 포함됨{#osgi-bundles-and-content-packages-included}

다음 zip 파일에는 이 Experience Manager 6.5 LTS 서비스 팩 릴리스에 포함된 OSGi 번들 및 콘텐츠 패키지를 나열하는 텍스트 문서가 포함되어 있습니다.

* [OSGi 번들](/help/release-notes/assets/65lts_sp3_bundles.zip)
* [컨텐츠 패키지](/help/release-notes/assets/65lts_sp3_packages.zip)

## 제한된 웹 사이트{#restricted-sites}

이들 웹 사이트는 고객만 사용할 수 있습니다. 고객이시며 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 센터](https://experienceleague.adobe.com/ko/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience)에 문의하십시오.

