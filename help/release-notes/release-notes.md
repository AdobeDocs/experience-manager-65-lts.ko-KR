---
title: Adobe Experience Manager 6.5 LTS, SP1의 최신 릴리스 노트
description: Adobe Experience Manager 6.5 LTS, 서비스 팩 1의 최신 릴리스 정보를 확인하십시오.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 8c726951cbd99660d2cfd23abef8857a6f4fcf36
workflow-type: tm+mt
source-wordcount: '4939'
ht-degree: 14%

---

# Adobe Experience Manager 6.5 LTS, SP1의 최신 릴리스 노트 {#release-notes}

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 버전 | 서비스 팩 1(SP1) <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2025년 8월 21일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://artifactory.corp.adobe.com/artifactory/maven-aem-release-local/com/adobe/aem/cq-quickstart/6.6.1/cq-quickstart-6.6.1.jar) |

<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

## [!DNL Adobe Experience Manager] 6.5 LTS, SP1에 포함된 항목 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS, SP1에는 새로운 기능, 고객이 요청한 주요 개선 사항 및 버그 수정이 포함되어 있습니다. 또한 2025년 3월 6.5 LTS의 최초 출시 이후 발표된 성능, 안정성 및 보안 개선 사항이 포함되어 있습니다. 6.5 LTS에 [이 서비스 팩을 설치](#install-update)합니다.

## 주요 기능 및 개선 사항

<!-- 6.5 LTS REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE EACH RELEASE -->

## 6.5 LTS, 서비스 팩 1의 문제가 해결되었습니다. {#fixed-issues}

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-65-LTS-SP1}

#### 접근성 {#sites-accessibility-65-lts-sp1}

* 콘텐츠 조각의 텍스트 편집기 요소가 기본적으로 잘렸던 문제를 수정했습니다. 이제 텍스트 편집기에 잘리지 않고 전체 콘텐츠가 표시됩니다. (SITES-33005)
* URL 경로를 클릭하면 올바른 대상 URL 대신 Indigo의 홈 페이지가 열리는 문제가 해결되었습니다. (SITES-33004)
* 자동화된 테스트 중 ADA 규정 준수 실패를 초래한 사용자 지정 AEM 구성 요소의 접근성 문제를 수정했습니다. (SITES-30660)
* 배경에 텍스트가 검은색으로 표시되고 WCAG 2.0 대비 요구 사항을 충족하도록 하여 경고 대화 상자 및 워크플로우 메시지의 ADA 규정 준수 문제를 해결했습니다. (SITES-30138)
* AEM Sites 편집기의 &quot;카테고리&quot; 단추에 특정 레이블이 없어 JAWS가 이를 설명 레이블을 제공하는 대신 &quot;이미지 단추 메뉴&quot;로 알리는 접근성 문제를 해결했습니다. (SITES-27497)
* 유효 권한 화면의 체크 표시 아이콘에 대체 텍스트가 부족해서 JAWS가 해당 의미를 읽고 전달하지 못하는 접근성 문제를 해결했습니다. (SITES-27272)
* [권한] 페이지에서 사용자 또는 그룹 권한을 제거하기 위한 명확한 JAWS 공지를 제공하지 않아 화면 판독기 사용자에게 혼란을 초래하는 접근성 문제를 해결했습니다. (SITES-27238)
* 오류 메시지가 설명 텍스트 없이 아이콘으로만 표시되므로 오류가 발생할 때 JAWS에서 이를 알리지 않는 접근성 문제가 해결되었습니다. (SITES-27155)
* 모듈 섹션에 대한 제목 수준 2 텍스트가 누락되는 등, JAWS가 AEM 온-프레미스 환경에서 잘못되고 명확하지 않은 단추 설명을 읽는 접근성 문제를 수정했습니다. (SITES-27152)
* AEM Assets 탭에서 값을 필터링한 후 JAWS가 결과 수를 알리지 않는 접근성 문제를 수정했습니다. (SITES-27150)
* 폴더 만들기에 확인이 표시되지 않고 JAWS에서 Assets UI에 알리지 않는 접근성 문제를 해결했습니다. (SITES-27141)
* AEM Sites의 접근성 문제를 해결했습니다. JAWS에서 양식 오류를 알리지 않았고, 포커스가 비대화형 오류 요소로 이동되었으며, 탭 아웃 시 필수 필드 오류가 표시되지 않았습니다. (SITES-27138)
* 타임라인 버튼 메뉴에 특정 레이블이 없어 JAWS가 명확한 설명을 제공하지 않고 &quot;활동 버튼 메뉴&quot;만 읽던 접근성 문제를 해결했습니다. (SITES-27134)
* JAWS가 컨테이너 항목에 대한 작업이나 역할을 알리지 않고 설명 레이블 대신 &quot;탐색 표시 v1&quot; 및 &quot;버튼 v2&quot;만 읽던 접근성 문제를 해결했습니다. (SITES-27131)
* 빠른 게시 팝업이 적절한 성공 메시지를 제공하지 않아 화면 판독기가 완료 피드백을 발표하지 못했던 접근성 문제를 수정했습니다. (SITES-26912)
* 하위 역할이 필요한 ARIA 역할이 있는 요소에 하위 역할이 포함되지 않아 접근성 표준을 준수하지 못하는 coral-column 보기의 접근성 문제를 해결했습니다. (SITES-26898)
* 만들기 페이지의 위쪽 탐색에 있는 &quot;template&quot; 및 &quot;properties&quot; 텍스트가 리플로우 모드에서 표시되지 않아서 키보드와 화면 판독기 사용자가 액세스할 수 없는 접근성 문제가 수정되었습니다. (SITES-26895)
* 키보드 탐색을 사용하여 상단 탐색의 &quot;검색&quot;, &quot;솔루션&quot;, &quot;도움말&quot;, &quot;받은 편지함&quot; 및 &quot;사용자&quot; 아이콘에 대한 도구 설명에 액세스할 수 없는 접근성 문제를 해결했습니다. (SITES-26889)
* 기본 탭 양식 필드에 오류 제안이 제공되지 않아 필수 입력 필드가 비어 있는 경우 사용자가 안내를 받을 수 없었던 접근성 문제를 수정했습니다. (SITES-26885)
* NVDA 및 내레이터 화면 판독기가 만들기 페이지에서 템플릿 파일 세부 사항을 알리지 않아 사용자가 프로그래밍 방식으로 전체 정보를 수신하지 못하는 접근성 문제를 해결했습니다. (SITES-26884)
* 기본 탭의 &quot;페이지 제목 텍스트 상자&quot;에 잘못된 이름을 사용했기 때문에 화면 판독기가 사용자에게 정확한 정보를 제공하지 못하는 접근성 문제를 해결했습니다. (SITES-26879)
* WCAG 2.2 AA 최소 명암비 요구 사항을 충족하도록 단추 전경색과 배경색을 업데이트하여 모든 사용자의 가독성과 접근성을 개선했습니다. (SITES-26877)
* 크기 조정 후 만들기 페이지의 상단 탐색에 있는 &quot;템플릿&quot; 및 &quot;속성&quot; 텍스트가 사라지게 하여 저시력 사용자가 가시성 및 접근성을 유지할 수 있도록 하는 문제를 해결했습니다. (SITES-26872)
* Reflow를 적용한 후 기본 페이지에 여러 개의 가로 스크롤 막대가 표시되어 적절한 액세스 가능성 및 컨텐츠 가시성을 확보할 수 있는 문제를 해결했습니다. (SITES-26800)
* 페르소나, 장바구니 또는 포기와 같은 단추를 활성화한 후 키보드 포커스가 예기치 않게 인구 통계학적 도구 모음의 시작으로 재설정되는 AEM 페이지 편집기의 접근성 문제를 해결했습니다. 이제 일관된 키보드 탐색 및 화면 판독기 워크플로우를 지원하기 위해 활성화된 단추에 포커스가 유지됩니다. (SITES-25306)
* 페이지 제목 및 태그 필드에 대한 접근성 레이블 연결 문제를 수정했습니다. 이제 AEM 인터페이스는 JAWS와 같은 화면 판독기를 사용할 때 액세스 가능성 레이블을 &quot;제목&quot; 및 &quot;페이지 제목&quot; 필드와 올바르게 연결합니다. 이 수정 사항은 적절한 레이블 읽기를 보장하며 페이지 생성, 속성 및 이동 워크플로우에서 ADA 준수를 향상시킵니다. (SITES-27149)
* 타임라인의 주석 입력 필드에 대한 시각적 레이블이 누락되는 문제를 해결했습니다. 접근성을 개선하기 위해 타임라인 섹션 아래의 &quot;댓글&quot; 입력 필드에 대한 시각적 레이블이 누락되었습니다. 업데이트를 통해 화면 판독기에서 필드 레이블을 정확하게 알릴 수 있습니다. 이 경험은 모든 사용자, 특히 보조 기술에 의존하는 개인을 위해 양식 탐색 및 제출을 향상시킵니다. (SITES-26903)
* 타임라인 주석에서 줄임표 단추에 대한 키보드 접근성을 수정했습니다. 타임라인 섹션의 주석 옆에 있는 생략 부호(세 점) 단추에 대한 키보드 탐색을 활성화했습니다. 이제 사용자는 tab 키를 사용하여 버튼에 액세스하고 버튼과 상호 작용할 수 있으므로 키보드 전용 탐색에 의존하는 사용자의 접근성을 향상시킵니다. (SITES-26891)
* 선택 대화 상자의 검색 결과에 대한 NVDA/내레이터 공지가 개선되었습니다. NVDA 또는 내레이터와 같은 화면 판독기를 사용할 때 검색 결과가 검색되는지 여부를 알리도록 선택 열기 대화 상자를 업데이트했습니다. 이러한 개선된 기능은 보조 기술에 의존하는 사용자가 시각적 확인이 필요 없이 검색 작업의 결과를 이해하는 데 도움이 됩니다. (SITES-26883)
* 댓글 입력 필드 옆에 있는 줄임표 아이콘에 대한 ARIA 역할을 수정했습니다. 올바른 ARIA 역할을 사용하도록 주석 입력 필드 옆에 있는 생략 부호(세 점) 아이콘을 업데이트하여 화면 판독기에서 요소를 정확하게 식별할 수 있도록 했습니다. 이러한 개선 사항은 접근성 규정 준수를 향상시키며 보조 기술에 의존하는 사용자의 경험을 개선합니다. (SITES-26881)
* Coral UI 구성 요소에서 잘못된 ARIA 속성을 수정했습니다. 모든 ARIA 속성이 유효한 값을 사용하도록 Coral UI 구성 요소를 업데이트하여 접근성 준수를 개선했습니다. 특히 `aria-modal="dialog"`과(와) 같은 잘못된 값이 잘못 할당된 경우가 해결되었습니다. 이 향상된 기능을 통해 화면 판독기에서 대화 상자 요소를 올바르게 해석할 수 있으므로 보조 기술에 의존하는 사용자의 접근성을 향상시킬 수 있습니다. (SITES-26873)
* 리플로우 시나리오에서 아이콘에 대한 가시성과 도구 설명이 개선되었습니다. **다운로드**, **에셋 재처리** 및 **체크아웃** 아이콘에 대한 도구 설명이 올바르게 표시되도록 리플로우 동작을 개선했습니다. 뷰포트 크기가 조정되거나 브라우저 확대/축소 설정이 변경될 때 아이콘과 해당 레이블이 보이지 않는 접근성 문제에 초점을 맞췄습니다. 이 수정 사항은 Reflow 동안 가시성을 유지하고 적절한 아이콘 설명을 제공하여 저시력 사용자를 지원합니다. (SITES-26871)


#### 관리 사용자 인터페이스{#sites-adminui-65-lts-sp1}

* JAWS가 사이트 생성 대화 상자에서 목록 역할을 알리거나 탐색 및 활성화 지침을 제공하지 않는 접근성 문제를 해결했습니다. (SITES-30661)
* 사이트 필터 보기의 상태 메시지에 대한 화면 판독기 지원은 예상대로 작동하므로 사용자가 보기 사이를 전환할 때 명확하고 시기적절한 피드백을 받을 수 있습니다. (SITES-24992)
* 필터 레일의 날짜 선택기는 컨테이너 내에 완전히 표시되므로 적절한 터치 대상 크기를 제공하고 클리핑 문제를 방지할 수 있습니다. (SITES-24988)
* 이제 선택한 필터 태그는 시각적 표시와 일치하는 시맨틱 HTML 및 Aria 레이블을 사용하므로 보조 기술에 대한 정확한 역할 지원과 명확한 작업이 보장됩니다. (SITES-24980)
* 참조 레일 영역에 Aria 레이블 속성을 추가하여 화면 판독기 사용자에게 고유하고 설명적인 레이블을 제공하고 페이지 전체에서 일관된 랜드마크가 식별되도록 했습니다. (SITES-24973)
* 크기 조정 및 위치를 지정하는 데 상대 단위를 사용하도록 참조 레일을 업데이트했습니다. 이를 통해 1280x1024 뷰포트에서 400%로 확대/축소할 때 콘텐츠의 크기를 조정하고 완전히 기능을 유지할 수 있습니다. (SITES-24972)
* Sites 홈 페이지 목록 보기의 확인된 테이블 요소에는 적절한 열 헤더 역할이 포함되어 있으므로 화면 판독기에서 각 데이터 셀에 대한 헤더를 알릴 수 있습니다. (SITES-24942)
* 이제 NVDA는 트리 디렉터리에서 수정된 날짜를 발표하여 화면 판독기 사용자가 전체 에셋 세부 정보를 받을 수 있도록 합니다. (SITES-24782)
* NVDA 화면 판독기가 AEM Sites의 트리 디렉터리 구성 요소에 있는 항목에 대한 불완전한 텍스트를 알리는 문제를 해결했습니다. 이제 NVDA가 각 항목에 대한 전체 텍스트를 읽어 접근성과 규정 준수를 개선합니다. (SITES-24780)
* 사용자가 키보드만 사용하여 왼쪽 막대의 크기를 조정할 수 있도록 트리 디렉토리의 창 분할기에 키보드 액세스 가능성이 추가되었습니다. (SITES-24779)
* 목록 항목에 대한 올바른 ARIA 역할을 포함하도록 도움말 메뉴 검색 결과를 업데이트하여 화면 판독기가 링크를 제대로 알려 접근성을 개선했습니다. (SITES-24729)
* 화면 판독기에서 &quot;Y개 결과 중 X&quot; 상태 메시지를 알리지 않던 문제를 수정했습니다. 또는 [사이트 필터] 패널에서 필터를 적용한 후 &quot;결과가 없습니다.&quot;라는 메시지가 표시되어 사용자가 제대로 된 결과를 확인할 수 있습니다. (SITES-24720)
* 앱 탐색에서 탐색 링크에 대한 누락된 역할 할당이 수정되었습니다. 화면 판독기가 탐색 요소를 올바르게 식별하고 알려주도록 적절한 ARIA 역할이 추가되었습니다. (SITES-24719)
* 선택한 필터 태그에 대한 잘못된 그리드 역할 마크업을 버튼 요소와 추가된 액세스 가능한 이름으로 대체하여 화면 판독기가 태그를 올바르게 발표하고 식별하도록 했습니다. (SITES-24717)
* 여러 선택을 수행할 때 참조 레일 상태 메시지에 대한 화면 판독기 공지가 추가되어 사용자가 변경 내용을 확인할 수 있습니다. (SITES-24678)
* 첫 번째 결과가 자동으로 발표되지 않도록 검색 필드 동작이 수정되었습니다. 이제 화면 판독기에 발견된 결과 수가 표시되어 사용자가 잘못된 포커스 공지 없이 목록을 탐색할 수 있습니다. (SITES-24658)
* 목록 보기의 비대화형 정적 요소에서 잘못된 `aria-label` 특성을 제거하여 화면 판독기에서 오해의 소지가 있거나 관련성이 없는 정보를 표시하지 않도록 했습니다. (SITES-24515)
* 액세스 가능한 이름에 제목 열 텍스트를 사용하도록 목록 보기의 첫 번째 열에 있는 확인란을 업데이트하여 화면 판독기가 양식 필드의 목적을 정확하게 전달할 수 있도록 했습니다. (SITES-24514)
* 콘텐츠를 탐색할 때 화면 판독기 사용자에게 로드 상태 메시지를 알리기 위한 적절한 ARIA 특성 및 라이브 영역 지원이 추가되었습니다. (SITES-24481)
* 뷰포트 너비가 1280×1024인 상태에서 콘텐츠가 400%로 확대/축소될 때 수평 스크롤을 제거하기 위해 응답형 디자인을 업데이트하여 측면 스크롤 없이 전체 가시성을 보장합니다. (SITES-24308)
* 논리적 순서를 따르도록 사이트 관리 UI에서 포커스 탐색을 수정했습니다. Esc 키를 누른 후 포커스를 &quot;모두 선택&quot; 버튼으로 되돌리고 Tab을 누른 후 포커스를 다음 대화형 요소로 이동했습니다. (SITES-24307)
* 키보드 탐색 중에 `<betty-titlebar-title>` 요소의 탐색 표시 단추가 올바른 순서로 포커스를 받도록 사이트 관리 UI의 포커스 순서가 업데이트되었습니다. (SITES-24305)
* 건너뛰기 링크 기능을 확인하여 키보드 포커스를 기본 컨텐츠 영역으로 이동하여 키보드 사용자가 헤더 요소를 무시하고 컨텐츠에 효율적으로 액세스할 수 있도록 합니다. (SITES-24061)


#### 클래식 UI{#sites-classicui-65-lts-sp1}

확인란 레이블이 누락되고 HTML이 날짜 검색 및 비표준 인터페이스를 포함한 여러 UI 요소에서 인코딩된 텍스트로 표시되는 클래식 UI 문제를 수정했습니다. (SITES-31822)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp1}

이제 AEM은 이미지 에셋에서 잘못된 형식의 XMP 메타데이터로 인한 성능 저하를 방지합니다. 숫자 세그먼트나 정규화되지 않은 구조가 있는 Assets과 같이 잘못되거나 호환되지 않는 XMP 속성 이름이 포함된 는 처리 중에 더 이상 반복된 경고 로그를 트리거하지 않습니다. 시스템은 문제가 있는 메타데이터를 필터링하여 자산 수집 및 유효성 검사가 오류 없이 완료되도록 합니다. (SITES-30683)

<!--
#### [!DNL Content Fragments] - Admin{#sites-admin-65-lts-sp1} -->

#### [!DNL Content Fragments] - 조각 편집기{#sites-fragments-editor-65-lts-sp1}

다른 작성자는 다른 작성자가 체크아웃하더라도 콘텐츠 조각을 게시할 수 있으며, 이는 체크아웃 기능의 의도한 비헤이비어와 상반됩니다. 이 수정 사항으로 인해 콘텐츠 조각을 체크아웃할 때 작성 인터페이스에서 다른 사용자가 게시 버튼을 보거나 사용할 수 없습니다. (SITES-30578)

<!--
#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp1}

#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp1}

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp1} -->

#### 구성 요소 콘솔{#sites-component-console-65-lts-sp1}

제품 목록 구성 요소에서 검색 결과에 있는 모든 SKU 대신 초기 페이지에서 처음 20개의 SKU만 &quot;모두 선택&quot; 확인란이 추가되는 문제가 수정되었습니다. (SITES-29191)

#### 핵심 백엔드{#sites-core-backend-65-lts-sp1}

`ValidationDataServlet`에서 이미지 자산을 처리하는 동안 형식이 잘못된 XMP 메타데이터에서 오류가 발생했습니다. 이 수정 사항은 규정을 준수하는 메타데이터 처리를 보장하며 잘못된 속성의 중복 구문 분석을 방지합니다. (SITE-30683)

<!--
#### Core Components{#sites-core-components-65-lts-sp1}

#### Campaign integration{#sites-campaign-integration-65-lts-sp1}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp1}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp1}

#### Launches{#sites-launches-65-lts-sp1}

#### Link Checker{#sites-link-checker-65-lts-sp1} -->

#### MSM - 라이브 카피{#sites-msm-live-copies-65-lts-sp1}

* AEM 6.5 온프레미에서 유령 구성 요소 상속을 다시 사용하도록 설정할 때 발생하는 JavaScript 오류 `ns.ui.alert is not a function`을(를) 수정했습니다. (SITES-31993)
* AEM 6.5에서 날짜를 선택하지 않고 롤아웃 &quot;나중에&quot; 옵션을 계속 사용할 수 있었던 문제를 해결했습니다. (SITES-31374)

#### 페이지 편집기{#sites-pageeditor-65-lts-sp1}

* 유효한 데이터 입력 및 오류 해결 후 링크 및 작업 탭에 오류 스타일, 아이콘 및 Aria가 유효하지 않은 속성이 계속 표시되는 티저 모달의 문제를 해결했습니다. (SITES-25527)
* 목록 및 단락 단추가 화면 판독기에 확장 또는 축소된 상태를 전달하지 않아 Aria가 확장된 속성을 정확하게 업데이트할 수 없는 티저 양식 텍스트 편집기의 문제를 수정했습니다. (SITES-25365)
* 키보드 입력이 슬라이더에 포커스를 유지하는 대신 장바구니 버튼으로 포커스를 이동한 상태에서 장바구니 슬라이더를 조정하는 인구 통계 도구 모음의 문제를 해결하여 키보드 사용자의 탐색 효율을 개선했습니다. (SITES-25324)
* 연결된 `<label>` 요소에 값을 할당하여 인구 통계 도구 모음의 장바구니 슬라이더에 액세스 가능한 이름을 추가했습니다. 이 수정 사항은 보조 기술과의 호환성을 개선하고 화면 판독기 사용자의 사용성을 개선했습니다. (SITES-25322)
* 인구 통계 도구 모음 드롭다운 내의 단추에 ARIA 역할 및 액세스 가능한 이름이 추가되었습니다. 이 수정 사항으로 보조 기술을 통해 적절한 식별이 가능해졌으며 키보드 및 화면 판독기 사용자의 탐색 기능이 개선되었습니다. (SITES-25315)
* 200% 브라우저 확대/축소에서 뷰포트를 넘어 컨텐츠 오버플로를 방지하기 위해 인구 통계학적 도구 모음 레이아웃을 조정하여 모든 컨트롤에 수평 스크롤 없이 액세스할 수 있도록 했습니다. (SITES-25309)
* 포커스를 도구 모음의 시작 위치로 재설정하는 대신 활성화된 단추에 키보드 포커스를 유지하도록 인구 통계 도구 모음의 포커스 관리를 수정했습니다. (SITES-25306)
* 단추 레이블 겹침은 설계된 대로 작동하며, 비슷한 화면 너비의 모드가 활성화되면 도구 설명을 사용하여 레이블을 표시합니다. (SITES-25285)
* 주석 모달에는 표시되는 제출 버튼이 포함되어 있어 사용자가 Esc 키를 누르거나 모달 바깥쪽을 클릭하지 않고도 주석을 제출할 수 있습니다. (SITES-25281)
* 주석 모달에는 사용자가 주석을 제출할 수 있는 펜 아이콘 버튼이 포함되어 있어 명확하고 액세스 가능한 제출 방법을 제공합니다. (SITES-25269)
* 주석 및 주석 닫기 단추에 대한 화면 판독기 알림을 수정하여 정확하고 관련 있는 피드백을 제공하고 관련되지 않거나 헷갈리는 정보를 제거합니다. (SITES-25268)
* 이제 AEM 편집기 페이지의 캔버스 섹션에서 전체 키보드 접근성을 지원합니다. 사용자는 마우스로 가리키지 않고 키보드만 사용하여 섹션 제목을 활성화하고 버튼을 편집할 수 있습니다. 이 업데이트는 WCAG 2.1.1을 준수하도록 하며 구성 요소(예: 티저, 이미지, 회전 메뉴, 레이아웃, 타임워프 및 주석 양식) 간의 사용성을 개선합니다. (SITES-25256)
* 좌우로 탐색하지 않고도 뷰포트 내에 모든 컨텐츠가 표시되도록 하기 위해 320px 너비의 회전식 모달에서 불필요한 수평 스크롤을 제거했습니다. (SITES-25254)
* 사이드 투 사이드 탐색이 필요 없이 모든 컨텐츠가 뷰포트 내에 표시되도록 320px 너비의 이미지 모달에서 불필요한 수평 스크롤을 제거했습니다. (SITES-25244)
* 320px 너비의 티저 모달에서 불필요한 수평 스크롤링을 제거하여 좌우로 탐색하지 않고도 뷰포트 내에 모든 콘텐츠가 표시되도록 합니다. (SITES-25242)
* 티저 모달에서 `List` 및 `Paragraph Format` 팝업 메뉴에 대한 키보드 탐색을 사용하도록 설정했습니다. 이 수정 사항을 통해 사용자는 화살표 키를 사용하여 이러한 메뉴에 액세스하고 해당 메뉴를 탐색할 수 있습니다. (SITES-25235)
* 주석 및 주석 닫기 단추에 대한 화면 판독기 알림을 수정하여 관련 작업에 맞게 정확하고 적절한 피드백을 제공할 수 있습니다. (SITES-25234)
* 티저 모달의 도움말 버튼 레이블을 개선하여 목적을 명확하게 설명하고 보조 기술 사용자를 포함한 모든 사용자에게 의미 있는 컨텍스트를 제공했습니다. (SITES-25224)
* 눈금자 측정값을 해당 장치와 연결하여 화면 판독기 사용자를 위한 에뮬레이터 눈금자를 개선했습니다. 또한 도구 설명을 아리아 설명 요소로 바꿉니다. (SITES-24955)
* 편집 단추가 의도한 대로 작동하며 작업을 수행하는 대신 정보 컨텍스트를 제공하기 때문에 수정 사항이 구현되지 않았습니다. (SITES-24950)
* 편집기 페이지에서 확인된 포커스 순서는 논리적 시퀀스를 따르며, 사용자가 예기치 않게 건너뛰거나 반복하지 않고 모든 대화형 요소를 탐색할 수 있습니다. (SITES-24937)
* 확인된 미리 보기 모드 캔버스는 사용자가 사용자 지정 텍스트 간격 설정을 적용할 때 텍스트 간격을 올바르게 업데이트하여 모든 컨텐츠 영역에서 일관된 서식을 유지합니다. (SITES-24936)
* 확인된 미리 보기 단추가 포커스의 컨텍스트 또는 상태 변경을 더 이상 트리거하지 않으므로 페이지 보기가 업데이트되기 전에 사용자가 버튼을 의도적으로 활성화하도록 합니다. (SITES-24784)
* 앱 탐색 링크에 올바른 ARIA 역할 할당을 추가하여 화면 판독기가 탐색 항목을 정확하게 식별하고 알려 접근성을 개선했습니다. (SITES-24718)
* 필터 변경 버튼을 업데이트하여 화면 판독기에 확장 및 축소 상태를 알리고, 중복 ARIA 속성을 제거했으며, 레이블 지정을 조정하여 중복되지 않는 명확한 설명을 제공했습니다. (SITES-24713)
* 검색 결과 상태 메시지에 대한 화면 판독기 알림을 링크 선택 대화 상자에 추가하여 결과가 로드되거나 일치하는 항목이 없을 때 사용자에게 확인을 제공합니다. (SITES-24700)
* 이미지 모달의 로드 상태에 대한 화면 판독기 알림을 추가하여 모달이 로드되고 상호 작용할 준비가 되었을 때 사용자가 피드백을 받을 수 있도록 합니다. (SITES-24697)
* 스티커 헤더가 200% 및 400% 확대에서 티저 모달 콘텐츠를 가리켰던 접근성 문제를 해결하여 페이지 확대율을 사용할 때 완전한 가시성과 유용성이 보장되었습니다. (SITES-24523)
* 검색/필터 필드에 검색 결과 수가 포함된 상태 메시지를 추가하여 화면 판독기가 사용자에게 결과를 알릴 수 있습니다. (SITES-24506)
* 검색/필터 필드에 검색 결과 수에 대한 화면 판독기 공지를 추가하여 결과가 로드될 때 사용자가 즉시 피드백을 받을 수 있도록 했습니다. (SITES-24505)
* 사이드 레일 패널의 탭 목록에 액세스 가능한 이름을 추가하여 화면 판독기가 WAI-ARIA 지침을 준수하여 용도를 알릴 수 있습니다. (SITES-24492)
* 모호한 편집기 아이콘에 설명 레이블을 추가하여 모든 사용자가 각 버튼의 기능을 명확하게 이해할 수 있도록 했습니다. (SITES-24480)
* 캔버스 보기의 섹션 제목 및 작업 버튼에 대한 전체 키보드 액세스 권한을 활성화하여 마우스 및 키보드 사용자가 일관되게 작업할 수 있습니다. (SITES-24479)

<!--
#### Replication{#sites-replication-65-lts-sp1}

#### Rich Text Editor{#sites-rte-65-lts-sp1} -->

#### Universal Editor {#sites-universal-editor-65-lts-sp1}

* 로그인 토큰 서비스에서 결과를 반환하기 전에 트리거된 쿼리 매개 변수를 사용하는 여러 요청이 잘못된 로그인을 발생시킨 QueryTokenService의 경합 조건을 수정했습니다. (SITES-30659)
* Felix ConfigMgr에 매핑된 경로의 배열을 저장하면 첫 번째 항목만 유지되는 UniversalEditorURLService의 문제를 해결했습니다. (SITES-30292)

### [!DNL Assets]{#assets-65-lts-sp1}

원격 DAM의 자산을 Sites 로컬 AEM으로 동기화하면 자산에서 게시된 상태 및 복제 관련 속성이 제거되던 문제를 수정했습니다. (Assets-48958)

<!--
#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp1}

#### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp1}



### [!DNL Forms]{#forms-65-lts-sp1}


#### Forms Designer 

#### Forms

#### Forms JEE 
 
#### Forms Captcha {#forms-captcha-65-lts-sp1} 

#### XMLFM {#forms-xmlfm-65-lts-sp1}

#### [!DNL Adaptive Forms] {#adaptive-forms-65-lts-sp1}

#### [!DNL Forms Designer] {#forms-designer-65-lts-sp1} -->



### 기초 {#foundation-65-lts-sp1}

<!--
#### Apache Felix {#foundation-apachefelix-65-lts-sp1}

#### Campaign{#foundation-campaign-65-lts-sp1}

#### Cloud Services{#foundation-cloudservices-65-lts-sp1}



#### Communities {#foundation-communities-65-lts-sp1}

#### Content distribution{#foundation-content-distribution-65-lts-sp1}

#### CRX {#foundation-crx-65-lts-sp1}

#### Granite{#foundation-granite-65-lts-sp1} -->

#### HTL{#foundatoin-htl-5-lts-sp1}

HTL 스크립트 엔진 팩토리가 작동하지 못하게 하는 OSGi 종속성 사이클을 해결하여 적절한 서비스 해결 및 스크립트 실행을 보장했습니다. (Granite-58275)

#### 통합{#foundation-integrations-65-lts-sp1}

* `com.adobe.cq.cq-analytics-integration` 번들에서 commons-httpclient 3.x의 사용을 제거하고 최신 AEM 6.5 LTS 표준에 맞게 `org.apache.httpcomponents.httpclient` 4.5.13.B0001로 대체했습니다. (CQ-4360586)
* 사용되지 않는 Search&amp;Promote 통합 번들을 AEM에서 제거하여 사용되지 않는 구성 요소를 제거하고 유지 관리 오버헤드를 줄였습니다. (CQ-4358030)
* SiteCatalyst 통합에 대한 새로운 백엔드 테스트 사례를 추가하여 분석 유효성 검사를 개선하고 보다 포괄적인 적용 범위를 확보했습니다. (CQ-4359991)
* Launch 구성의 속성 섹션에서 회사 및 속성 드롭다운이 표시되지 않는 문제를 해결했습니다. 또한 저장 및 닫기 는 모든 필수 필드가 채워지더라도 오류가 발생하며 제목 필드만 비어 있는 경우 회사 및 속성에 대해 잘못된 오류 메시지가 표시됩니다. (CQ-4359853)
* Search&amp;Promote 번들 제거에 맞추기 위해 버전 6.6에서 `searchpromote` 서블릿 경로 항목을 제거했습니다. (CQ-4359523)
* 정확한 유효성 검사와 향상된 테스트 신뢰성을 보장하기 위해 Target 저장소에 대한 HTTP 테스트 사례를 수정했습니다. (CQ-4359022)
* Guava 라이브러리 종속성을 제거하기 위해 integration-adobeims-console 모듈에서 Guava 캐싱 사용을 제거했습니다. (CQ-4358710)
* AEM 6.5에서 제대로 작동하도록 AEM 6.6에서 DTM 통합 워크플로우, 받은 편지함 작업 및 프로젝트 기능을 확인했습니다. (CQ-4358151)
* AEM 6.5에서 호환성과 적절한 작업을 보장하기 위해 AEM 6.6에서 컨텐츠 Insight 기능의 유효성을 검사했습니다. (CQ-4357774)
* AEM 6.5에서 호환성과 적절한 작업을 보장하기 위해 AEM 6.6에서 클라우드 서비스 기능의 유효성을 검사했습니다. (CQ-4357773)
* AEM 6.5에서 호환성과 적절한 작업을 보장하기 위해 AEM 6.6에서 Adobe IMS 콘솔 통합의 유효성을 검사했습니다. (CQ-4357772)
* Java 17에서 실행하고, 실패한 Selenium 테스트를 해결하고, 선택 테스트를 플레이라이트로 이동하고, 모든 단위 테스트가 통과되도록 Test&amp;Target 통합에 대한 Jenkins 파이프라인을 업데이트했습니다. (CQ-4357770)
* 빌드 및 테스트 파이프라인을 업데이트하여 DX 통합, 워크플로우, 받은 편지함 및 프로젝트를 6.6.0 분기와 연계합니다. 또한 업그레이드 호환성 문제를 해결하고 안정성과 기능에 대해 영향을 받는 모든 서비스의 유효성을 확인합니다. (CQ-4357767)

<!--
#### Jetty{#foundation-jetty-65-lts-sp1} -->

#### 현지화{#foundation-localization-65-lts-sp1}

* 올바른 번역을 표시하기 위해 &quot;권한&quot; 목록에서 &quot;액세스 제어 제거&quot; 대화 상자의 문자열을 지역화했습니다. (GRANITE-59427)
* 모델 편집기의 &quot;Or Split Properties&quot; 규칙 추가 대화 상자에서 연산자 및 필드 레이블을 포함한 여러 UI 문자열이 현지화되지 않은 것으로 표시되는 문제를 해결했습니다. 이제 모든 문자열이 올바른 현지화로 표시됩니다. (CQ-4354014)
* 워크플로우 모델 편집 대화 상자에서 &quot;설명 표시 대상&quot; 도구 설명에 대해 누락된 번역을 추가했습니다. (CQ-4347996)

#### Oak {#foundation-oak-65-lts-sp1}

업그레이드 중에 AEM이 `/apps/system/config`에서 기존 구성 파일을 다시 만들거나 이름을 변경하여 `.cfg.json`개 파일을 `.config`개 파일로 바꾸는 문제를 해결했습니다. (GRANITE-58899)

#### Omnisearch{#foundation-omnisearch-65-lts-sp1}

자리 표시자가 입력 필드의 레이블로 잘못 표시되던 접근성 문제를 수정했습니다. 이 문제로 인해 검색, AEM 경험 조각, 콘텐츠 조각 및 콘텐츠 조각 모델에서 필드 레이블이 누락됩니다. (Granite-61791)

<!--
#### Platform{#foundation-platform-65-lts-sp1} -->

#### 프로젝트{#foundation-projects-65-lts-sp1}

* 프로젝트 삭제가 완료되었음에도 불구하고 캘린더 보기에서 프로젝트를 삭제할 때 잘못된 오류 팝업이 표시되는 문제를 해결했습니다. (CQ-4358890)
* Firefox에서 프로젝트 보기의 &quot;자산 컬렉션&quot; 카드 바닥글이 카드 테두리에 겹치는 문제를 해결했습니다. 이제 바닥글이 겹치지 않고 올바르게 정렬됩니다. (CQ-4353317)

#### Quickstart{#foundation-quickstart-65-lts-sp1}

* 패키지 관리자를 통해 설치할 때 차단 목록에 추가된으로 표시되지 않도록 Guava 번들의 버전 범위를 조정하도록 제거 스크립트를 업데이트했습니다. (GRANITE-59559)
* 구문 분석 오류를 트리거하지 않고 대용량 패키지 설치를 지원하도록 서버 구성을 업데이트하여 JDK 17을 사용하여 Tomcat 11에서 AEMFD 패키지를 업로드하는 동안 발생하는 다중 부분 구성 오류를 해결했습니다. (GRANITE-58327)
* 인터페이스에서 클래식 확인란의 처리를 수정하여 복제 에이전트를 편집할 때 오류(`#1660`)가 표시되는 복제 UI 문제를 해결했습니다. (GRANITE-58302)
* 누락된 서비스 권한을 해결하고, 구성 처리를 업데이트하고, 필요한 서비스를 올바르게 초기화하도록 하여 JDK 21로 AEM 6.5 LTS를 실행할 때 S3 데이터 저장소에 대한 여러 시작 오류를 해결했습니다. (GRANITE-57082)
* AEM 6.5의 유지 관리 및 유지 관리 전략을 정의했습니다. 이 수정 사항에는 다음 사항이 포함되어 있습니다.
   * 서비스 팩 케이던스.
   * 핫픽스 케이던스.
   * AEM 6.6을 통한 병렬 지원
   * 지원 매트릭스가 업데이트되었습니다.
   * 추가 소유권 책임. (GRANITE-50459)

<!--
#### Security{#foundation-security-65-lts-sp1} -->

#### Sling{#foundation-sling-65-lts-sp1}

* 여러 `ClassCastException`에서 `ResourceAccessGate`을(를) 초기화할 때 발생한 `ResourceAccessSecurityImpl`을(를) 해결하기 위해 Sling ResourceAccessSecurity를 버전 1.1.2로 업데이트했습니다. (NPR-42750)
* Adobe Stock 통합에서 라이선스 대화 상자가 회색으로 표시되는 문제가 해결되었습니다. 이 문제는 `sunt:initList` 함수에 의해 필수 입력 필드가 제거되었기 때문입니다. 함수는 Coral Foundation 클라이언트 라이브러리에서 발견되었습니다. 클라이언트 라이브러리가 필요한 필드를 유지하도록 업데이트하여 적절한 라이센스 대화 상자 기능을 활성화합니다. (NPR-42748)
* 패키지 설치 중에 `DataTimeParseException` 및 `String.length()` null 포인터 예외가 발생한 Sling 스크립팅 문제에 대한 수정 사항을 백포트했습니다. 설치 오류를 줄이고 안정성을 개선하기 위해 Sling 스크립팅을 버전 2.8.3-1.0.10.6으로 업데이트했습니다. (NPR-42640)

<!--
#### Translation{#foundation-translation-65-lts-sp1} -->

#### 사용자 인터페이스{#foundation-ui-65-lts-sp1}

* 사용자 그룹 표시를 41개로 제한한 AEM 작성자 UI의 문제가 해결되었습니다. 이 문제는 Granite UI 그룹 선택 구성 요소의 기본 배치 제한으로 인해 발생했습니다. 잘리지 않고 모든 그룹을 표시하도록 구성 요소를 업데이트했습니다. (NPR-42749)
* 페이지 속성을 편집할 때 다중 필드 구성 요소의 필수 필드가 다시 확인되지 않던 온-프레미스 페이지 생성 마법사의 문제를 해결했습니다. 이 문제는 결과적으로 작성자가 유효성 검사를 무시하고 불완전한 데이터를 진행할 수 있도록 허용했습니다. (GRANITE-58826)
* 번역되지 않은 아이콘 및 텍스트 메타데이터를 표시하는 대신, JAWS 화면 판독기에서 명확하고 사용자 친화적인 레이블을 발표하도록 AEM의 도움말 버튼에 대한 ARIA 속성을 수정했습니다. (GRANITE-55360)

#### WCM{#foundation-wcm-65-lts-sp1}

* 번역 번들 업데이트, Java 패키지 호환성 확인, 더 이상 사용되지 않는 종속성 제거, 포괄적인 테스트를 통한 전체 기능 보장을 통해 AEM 번역에 대한 Java 17 지원을 추가했습니다. (CQ-4357525)
* 자동화된 테스트 중 잘못된 오류를 방지하기 위해 불안정한 Evergreen 테스트 `com.adobe.cq.platform.it.http.workflow.inbox.InboxOnOffTimeIT.testActivateLater`을(를) 제거했습니다. (CQ-4298376)

#### 워크플로{#foundation-workflow-65-lts-sp1}

* AEM 6.5 LTS를 Java 21과 함께 사용할 때 정의되지 않은 값이 URL에 표시되지 않도록 하기 위해 받은 편지함 항목에 누락된 `data-detailsurl` 특성이 추가되었습니다. (GRANITE-60158)
* AEM 6.5 LTS를 Java 21로 실행할 때 `deactivate` 번들의 `WorkflowToPublishEventService` 메서드에서 NullPointerException을 해결하여 오류 없이 적절한 워크플로우 서비스를 종료했습니다. (GRANITE-58151)
* 공유, 부재 중 사용자 지정 및 타임라인 쿼리 문제 해결을 지원하도록 워크플로우 인덱스를 업데이트했습니다. (GRANITE-52640)
* 공유, 부재 중 사용자 지정 기능 및 타임라인 쿼리 문제 해결을 지원하도록 워크플로우 인덱스를 업데이트했습니다. (GRANITE-52294)
* AEM 릴리스 10912으로 프로그램 업그레이드에 대한 로그 비교 유효성 검사 중에 증가된 오류 로그 오류를 해결하여 안정적인 워크플로우 실행을 보장합니다. (GRANITE-44268)
* `url.searchParams`을(를) `url.search`(으)로 바꾸도록 워크플로우 보고서의 URL 정리 방법을 업데이트하여 취약한 URL에 대한 XSS 보호를 개선했습니다. (CQ-4359585)
* 적절한 운영과 통합을 위해 AEM 6.6 Forms에서 워크플로우, 받은 편지함 및 프로젝트 기능의 유효성을 검사했습니다. (CQ-4358777)
* Jenkins를 통해 워크플로 컨텐츠 아티팩트를 릴리스하기 위한 자동화를 구현하여 AEM 6.5에서 효율적이고 일관성 있는 배포 프로세스를 가능하게 했습니다. (CQ-4358472)
* 작업이 생성되었는데도 JavaScript 구문 오류로 인해 제출을 클릭한 후 &quot;작업 추가&quot; 대화 상자가 닫히지 않던 받은 편지함 작업 만들기 워크플로우의 문제를 수정했습니다. (CQ-4355336)
* `isEndUserConfigurationEnabled`에 대한 속성 정의가 누락되어 받은 편지함 보기 구성을 저장할 수 없는 문제를 해결했습니다. (CQ-4287757)




## [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS의 플랫폼은 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix)와 Java™ 콘텐츠 저장소인 Apache Jackrabbit Oak 1.68.x의 업데이트된 버전을 기반으로 빌드되었습니다.

Eclipse Jetty 11.0.x는 Quickstart의 서블릿 엔진으로 사용됩니다.

### Java™ 지원  {#java-support}

* Java™ 17 및 Java™ 21이 지원됩니다.
* 최적의 성능을 위해 기본 GC 값을 다른 값으로 재정의합니다. 자세한 내용은 [설치 및 업데이트](/help/sites-deploying/custom-standalone-install.md) 섹션을 참조하십시오.
* Adobe는 Oracle에서 공개적으로 제공되지 않는 경우 AEM 관련 프로젝트에서 고객이 사용할 수 있도록 Java™ 17 및 Java™ 21 유지 관리 업데이트를 배포합니다.

### Uberjar 패키징 {#uber-jar-packaging}

* AEM 6.5 LTS의 Uberjar 패키징에 약간의 차이가 있습니다. 자세한 내용은 [AEM Uber Jar 버전 업데이트](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)를 참조하십시오.

### 업그레이드 {#upgrade}

* 업그레이드 절차에 대한 자세한 내용은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.

## 설치 및 업데이트 {#install-update}

설정 요구 사항에 대한 자세한 내용은 [설치 지침](/help/sites-deploying/custom-standalone-install.md)을 참조하십시오.

세부 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.

>[!NOTE]
>
> 새 AEM 6.5 LTS 설치의 경우 인덱스 정의를 별도로 설치해야 합니다. 자세한 내용은 [이 문서](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)를 참조하세요.

## 지원되는 플랫폼 {#supported-platforms}

[AEM 6.5 LTS 기술 요구 사항](/help/sites-deploying/technical-requirements.md)에서 지원 수준을 포함한 전체 지원 플랫폼 매트릭스를 찾을 수 있습니다.

>[!NOTE]
>
>Java™ 17/Java™ 21은 AEM 6.5 LTS와 함께 사용하는 것이 권장되는 버전입니다.

## 이제 사용되지 않는 기능과 제거된 기능 {#deprecated-and-removed-features}

<!-- CARRY OVER EACH RELEASE -->

Adobe는 기존 기능을 현대화하거나 대체하여 고객 가치를 개선하기 위해 제품 기능을 지속적으로 검토합니다. 이러한 변경 사항은 이전 버전과의 호환성을 신중하게 고려하여 적용됩니다.

Adobe Experience Manager(AEM) 기능의 제거 또는 대체 예정 사실을 알리기 위해 다음 규칙이 적용됩니다.

1. 사용 중지 공지가 먼저 표시됩니다. 사용 중지 중에도 기능이 계속 지원되지만 더 이상 개선되지는 않습니다.
1. 더 이상 사용되지 않는 기능은 이른 시일 내에 후속 주 릴리스에서 제거됩니다. 제거할 실제 목표 날짜는 추후 발표됩니다.

이 프로세스에서 고객에게 하나 이상의 릴리스 주기를 제공하여, 실제 제거 전에 더 이상 사용되지 않는 기능의 새 버전이나 후속 버전에 대한 구현을 채택할 수 있도록 합니다.


### 이제 사용되지 않는 기능 {#deprecated-features}

이 섹션에는 Adobe가 AEM 6.5 LTS에서 더 이상 사용되지 않는 기능이 나열됩니다. 일반적으로 Adobe는 향후 릴리스에서 해당 기능을 제거하기 전에 해당 기능을 더 이상 사용하지 않도록 설정하고 사용할 수 있는 대안을 제공합니다.


현재 배포에서 해당 기능을 사용 중인지 검토하고 이들 구현을 변경하여 제공되는 대체 기능을 사용하도록 계획을 세우는 것이 좋습니다.

| 영역 | 기능 | 대체 | 버전(SP) |
|---|---|---|---|


### 제거된 기능 {#removed-features}

이 섹션에는 AEM 6.5 LTS에서 제거된 기능이 나열됩니다. 이전 릴리스에서는 이러한 기능이 더 이상 사용되지 않는다고 표시되었습니다.

| 영역 | 기능 | 대체 | 버전(SP) |
|--- |--- |--- |--- |



## 알려진 문제 {#known-issues}

<!-- DO THESE KNOWN ISSUES CARRY OVER EACH RELEASE? THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

### AEM 6.5.21-6.5.23 및 AEM 6.5 LTS GA의 JSP 스크립팅 번들 문제

AEM 6.5.21, 6.5.22, 6.5.23 및 AEM 6.5 LTS GA는 알려진 문제가 포함된 `org.apache.sling.scripting.jsp:2.6.0` 번들과 함께 제공됩니다. 이 문제는 AEM 인스턴스가 많은 동시 요청을 처리할 때 높은 부하 상태에서 일반적으로 발생합니다.

이 문제가 발생하면 `org.apache.sling.scripting.jsp:2.6.0`에 대한 참조와 함께 오류 로그에 다음 예외 중 하나가 나타날 수 있습니다.

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

이 문제를 해결하기 위해 핫픽스 [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip)이 제공됩니다.

### SSL 전용 기능을 사용한 Dispatcher 연결 실패 {#ssl-only-feature}

AEM 배포에서 SSL 전용 기능을 활성화하면 Dispatcher와 AEM 인스턴스 간의 연결에 영향을 미치는 알려진 문제가 있습니다. 이 기능을 활성화한 후에는 상태 검사가 실패할 수 있으며 Dispatcher와 AEM 인스턴스 간의 통신이 중단될 수 있습니다. 이 문제는 특히 고객이 `https + IP`을(를) 통해 Dispatcher 인스턴스에서 AEM 인스턴스로 연결하려고 할 때 발생합니다. SNI(Server Name Indication) 유효성 검사 문제와 관련되어 있습니다.

**영향:**

* HTTP 400 응답 코드로 인한 상태 검사 실패
* Dispatcher와 AEM 인스턴스 간의 손상된 트래픽
* Dispatcher를 통해 콘텐츠를 제대로 제공할 수 없음
* Dispatcher 구성에서 IP 주소로 HTTPS를 사용할 때 연결 실패
* HTTPS + IP를 통해 연결할 때 HTTP 400 “잘못된 SNI” 오류

**영향을 받는 환경:**

* Dispatcher 구성을 사용한 AEM 배포
* SSL 전용 기능이 활성화된 시스템
* AEM 인스턴스에 대한 `https + IP` 연결 방법을 사용하는 Dispatcher 구성

**솔루션:**
이 문제가 발생하면 Adobe 고객 지원 센터에 문의하십시오. 이 문제를 해결하기 위해 핫픽스 [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip)이 제공됩니다. 필요한 핫픽스를 적용하기 전에는 SSL 전용 기능을 활성화하지 마십시오.

## OSGi 번들 및 콘텐츠 패키지가 포함됨{#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 이 [!DNL Experience Manager] 6.5 LTS, 서비스 팩 1 릴리스에 포함된 OSGi 번들 및 컨텐츠 패키지 목록이 나와 있습니다.

* [Experience Manager 6.5 LTS, 서비스 팩에 포함된 OSGi 번들 목록](/help/release-notes/assets/65lts_sp1_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5 LTS, 서비스 팩에 포함된 콘텐츠 패키지 목록](/help/release-notes/assets/65lts_sp1_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 제한된 웹 사이트{#restricted-sites}

이들 웹 사이트는 고객만 사용할 수 있습니다. 고객이시며 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 센터](https://experienceleague.adobe.com/ko/docs/customer-one/using/home)에 문의하십시오.

