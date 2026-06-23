---
title: Adobe Experience Manager 6.5 LTS의 최신 릴리스 정보, SP2
description: Adobe Experience Manager 6.5 LTS, 서비스 팩 2에 대한 최신 릴리스 정보를 찾아보십시오.
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: c532abc558084ee9b58e618b0fc16677f4c5b6a4
workflow-type: tm+mt
source-wordcount: '7743'
ht-degree: 96%

---


# Adobe Experience Manager 6.5 LTS의 최신 릴리스 정보, SP2 {#release-notes}

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 버전 | 서비스 팩 2(SP2) <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2026년 2월 19일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.2.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> **필수 핫픽스** – SP2를 설치할 때 오프라인 압축과 관련된 SNFE(SegmentNotFoundException) 문제를 방지하려면 [알려진 문제 - 온라인 압축 중 저장소 손상](#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146)에 설명된 핫픽스를 설치하십시오.

## [!DNL Adobe Experience Manager] 6.5 LTS, SP2 포함 사항 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS, SP2에는 새로운 기능, 고객 요청을 반영한 주요 개선 사항 및 버그 수정이 포함되어 있습니다. 여기에는 2025년 3월 6.5 LTS가 처음 출시된 이후 적용된 성능, 안정성, 보안 개선 사항도 포함됩니다. 6.5 LTS에 [이 서비스 팩을 설치](#install-update)하십시오.

## 주요 기능 및 개선 사항

**AEM Sites**

이제 AEM 6.5 LTS SP2에 [콘텐츠 조각 및 모델 관리](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/65lts/) 및 [론치](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/launches/)를 위한 OpenAPI가 포함되어 있습니다. 이러한 API는 작성 및 예약을 위한 콘텐츠 조각 및 실행에 대한 액세스를 제공합니다. AEM as a Cloud Service와 동일한 최신 OpenAPI를 사용합니다.

**AEM Forms**

**AEM Forms 6.5 LTS SP2 포함 사항**

* JBoss® EAP 8.0을 사용하는 RDBMK 지원이 추가되었습니다.

* WebSphere® Liberty Profile(WLP)에 대한 지원이 추가되었습니다. WLP는 Oracle 데이터베이스 및 IBM® Sumeru JDK 21에서만 지원됩니다.

* 시각적 규칙 편집기의 사용자 경험이 개선되었습니다. 이번 업데이트에는 다음 사항이 포함됩니다.

   * 저장 후 요약 보기를 자동으로 다시 로드하여 업데이트된 규칙 상태 표시

   * “추가”/“삭제” 버튼을 표시하고 숨기는 대신 토글 허용

   * 규칙 저장 작업이 실패할 때 명확한 피드백 제공(FORMS-21261)

* `Dcom.adobe.fd.forms.export.legacy` 매개변수를 대체하여 AEM Forms에서 이전 확장 가능한 마크업 언어(XML) 내보내기 모드를 전환하기 위한 런타임 애플리케이션 프로그래밍 인터페이스(API)를 추가했습니다. 이 향상된 기능을 통해 사용자는 더 효율적으로 내보내기 모드를 전환하여 워크플로의 유연성이 향상됩니다. (FORMS-23115)

* 적응형 양식의 네임스페이스 태그를 사용하여 JavaScript 오브젝트 표기법(JSON)에 대한 지원이 추가되었습니다. 이 향상된 기능을 통해 사용자는 JSON 데이터 구조를 보다 효과적으로 처리할 수 있으므로 데이터 통합 및 처리 기능이 향상됩니다. (FORMS-22519)

* 규칙 편집기에 기본 제공(OOTB)으로 기록 문서 다운로드(DoR) / 양식 제출 버튼이 추가되었습니다. 이 향상된 기능을 통해 고객은 사용자 정의 코드를 작성하지 않고도 downloadDoR 기능을 사용할 수 있어 유용성과 효율성이 향상됩니다 (FORMS-21263)

* 적응형 양식의 네임스페이스 태그를 사용하여 JavaScript 오브젝트 표기법(JSON)에 대한 지원이 추가되었습니다. 이 향상된 기능을 통해 사용자는 더 정확하고 효율적으로 양식을 미리 작성할 수 있으며, 데이터 통합을 개선하고 수동 입력 오류를 줄입니다. (FORMS-10883)

<!-- UPDATE THE EACH RELEASE -->

## 6.5 LTS, 서비스 팩 2에서 해결된 문제 {#fixed-issues}

### [!DNL Sites]{#sites-65-LTS-SP2}

#### 접근성 {#sites-accessibility-65-lts-sp2}

* 작성자가 편집하는 동안 구성 요소 브라우저의 항목을 가리킬 때 텍스트 구성 요소가 키보드 초점을 잃었습니다. 이로 인해 입력이 중단되고 WCAG 3.2.1에서 액세스 가능성 오류가 트리거되었습니다. 이 수정 사항을 통해 마우스로 가리키면 스타일이 초점을 이동하는 것을 방지하며 구성 요소 브라우저 상호 작용 중에 텍스트 구성 요소에 초점이 맞춰지도록 합니다. (SITES-35370)
* 탭 키로 앞으로의 탐색을 차단하는 설명 서식 있는 텍스트 필드의 초점 관리가 수정되었습니다. 사용자가 비표준 키보드 명령에 의존하여 초점을 전환하면서 예상했던 대화 상자 탐색이 중단되었기 때문에 RTE에 갇히게 되었습니다. 이 변경 사항을 통해 표준 키보드 상호 작용을 강제하고 대화 상자 전체에 논리적인 탭 순서를 유지합니다. (SITES-35228)
* Sites 편집기에서 페이지 작성 중 예상되는 비헤이비어를 중단시키고 일관성 없는 구성 요소 상호 작용을 초래한 문제를 수정했습니다. 작성자가 표준 편집 작업을 방해하고 워크플로 효율성을 저하시키는 신뢰할 수 없는 UI 응답을 경험했습니다. 이 업데이트로 기본 편집기 논리를 개선하고 영향을 받는 구성 요소 간의 안정적이고 예측 가능한 상호 작용을 복원합니다. (SITES-35227)
* 페이지 편집기에서 에셋 선택기를 손상시켜 특정 페이지 편집 시나리오에서 로드되지 않는 회귀. 이제 작성자는 페이지를 편집하면서 에셋을 선택하거나 탐색할 때 에셋 선택기를 정상적으로 열고 사용할 수 있습니다. 이 변경 사항을 통해 로드 실패로 인해 중단된 에셋 선택 워크플로에 대한 일관된 액세스를 복원합니다. (SITES-35226)
* 페이지 상호 작용 중 일관성 없는 비헤이비어를 유발하고 표준 작성 워크플로를 중단시키는 문제를 Sites 편집기에서 제거했습니다. 이 오류로 인해 예상치 못한 UI 응답이 발생하여 구성 요소 구성 및 콘텐츠 업데이트가 방해받았습니다. 이 업데이트로 영향을 받은 기능을 안정화하고 페이지 간 편집 액션의 신뢰할 수 있는 실행을 복원합니다. (SITES-35225)
* 페이지 편집 중 일관성 없는 비헤이비어를 유발하고 정상적인 워크플로를 방해하는 Sites 저작 인터페이스의 결함을 제거했습니다. 작성자가 구성 요소 상호 작용과 콘텐츠 업데이트를 방해하는 예기치 않은 UI 응답을 받았습니다. 이 업데이트로 영향을 받은 기능을 안정화하고 편집 시나리오 전반에 걸쳐 신뢰할 수 있고 예측 가능한 비헤이비어를 복원합니다. (SITES-35224)
* 이제 AEM Sites에는 ADA 및 WCAG 요구 사항을 충족하기 위해 이미지에 `alt` 텍스트 지원이 포함됩니다. 페이지 출력에서 더 이상 `alt` 속성을 생략하지 않으므로 화면 판독기에서 올바른 대체 텍스트를 받습니다. (SITES-27153)
* 추가 버튼이 더 이상 제목과 320px 뷰포트 폭으로 겹치지 않도록 `Note Add` 도구 모음 레이아웃을 수정했습니다. 개선된 작은 화면 리플로우 기능으로 400% 확대/축소 동안에도 제어를 읽을 수 있고 사용할 수 있습니다. (SITES-25376)
* 링크 선택 대화 상자 오류에 대한 화면 판독기 공지가 누락된 문제를 해결했습니다. UI가 이제 상태 메시지 컨테이너를 통해 오류 텍스트를 게시하므로 NVDA는 메시지가 표시되는 즉시 메시지를 읽습니다. (SITES-25368)
* 측면 레일 에셋 목록에서 ARIA 그리드 및 그리드 셀 역할을 제거했습니다. 표준 목록 의미 체계와 키보드 초점 순서를 복원하여 화면 판독기 탐색을 개선하고 추가 탭 정지를 줄였습니다. (SITES-25361)
* 측면 레일 에셋의 초점 순서가 수정되었습니다. 키보드 사용자가 이제 일관된 탭 경로를 통해 편집을 포함한 모든 에셋 액션에 도달합니다. (SITES-25360)
* 320px 뷰포트 폭의 에셋 검색 모달에서 레이아웃 오버플로가 수정되었습니다. 이제 모달 콘텐츠가 리플로우되고 가독성을 유지하므로 제어가 더 이상 대화 상자와 겹치거나 오버런되지 않습니다. (SITES-25330)
* 편집 버튼에 대한 NVDA 출력이 수정되었습니다. NVDA가 이제 “미리보기 버튼을 눌렀음”이 아닌 편집 액션을 발표합니다. (SITES-25320)
* 자동 또는 일반 화면 판독기 출력을 발생시킨 이름 없는 인구 통계 도구 모음 텍스트 입력을 수정했습니다. 이제 각 입력에 명확한 레이블 기반 액세스 가능한 이름이 표시되므로 키보드 및 보조 기술 탐색이 개선됩니다. (SITES-25316)
* 레이아웃 미리보기 탐색 중 인구 통계 도구 모음에 대한 키보드 초점 순서가 수정되었습니다. 탭 탐색이 이제 보조 도구 모음으로 건너뛰지 않고 인구 통계 버튼에서 도구 모음 제어로 바로 이동합니다. (SITES-25305)
* 레이아웃 편집 눈금자에서 “더 작은 화면” 및 “태블릿” 레이블에 대한 잘못된 공지 순서가 수정되었습니다. 이제 화면 판독기에 페이지 레이아웃과 일치하는 올바른 눈금자 표시기에 이러한 레이블이 표시됩니다. (SITES-25291)
* 200% 확대/축소에서 레이아웃 편집 도구 모음 오버플로가 수정되었습니다. 이제 콘텐츠가 뷰포트 내에 있고 스크롤을 통해 연결 가능한 상태로 유지됩니다. (SITES-25288)
* 주석 오버레이의 잘못된 초점 순서가 해결되었습니다. 이제 키보드 탭 기능이 오버레이 제어 및 주석 항목을 순환합니다. 상위 페이지가 더 이상 오버레이 뒤에서 초점을 가져오지 않습니다. (SITES-25282)
* 색상 견본 팝오버 초점 처리가 수정되었습니다. 이제 대화 상자에서 초점을 명확한 제목으로 이동하고 해당 진입점에서 화면 판독기 출력을 시작합니다. NVDA가 더 이상 전체 대화 상자 콘텐츠를 순서대로 읽지 않습니다. (SITES-25275)
* 날짜 선택기를 닫은 후 타임워프 모달 초점 처리가 수정되었습니다. 이제 `Escape`가 날짜 선택기 버튼으로 초점을 반환합니다. 이제 날짜 선택에서 날짜 선택기 제어 옆에 있는 입력 필드에 초점을 두어 초점 손실 및 배경 페이지 액세스를 방지합니다. (SITES-25264)
* 주석 삭제 대화 상자에 대한 키보드 초점 처리가 수정되었습니다. 이제 취소가 16진수 값 확인 제어가 아니라 대화 상자를 연 `Delete` 제어에 초점을 반환합니다. 취소 후 화면 판독기에서 더 이상 관련되지 않은 대화 상자 콘텐츠를 알리지 않습니다. (SITES-25258)
* 주석 모달 대화 상자에 대한 초점 처리가 수정되었습니다. 이제 대화 상자를 열면 대화 상자 제목에 초점이 설정되고 NVDA가 캔버스 콘텐츠 및 관련 없는 대화 상자 텍스트를 읽지 못합니다. 이제 키보드 탐색이 대화 상자를 닫을 때까지 대화 상자 안에 남아 있습니다. (SITES-25257)
* 320px 폭에서 검색 모달 레이아웃 문제가 해결되었습니다. 이제 모달 콘텐츠가 완전히 리플로우되어 트리 디렉터리와 겹치지 않습니다. 사용자가 결과를 보고 숨겨진 제어 없이 디렉터리를 탐색할 수 있습니다. (SITES-25246)
* 텍스트 간격이 늘어나면 검색 모달 텍스트가 더 이상 클립되지 않습니다. 이제 트리 디렉터리 레이아웃이 명확하게 구분되므로 레이블과 항목을 읽을 수 있습니다. 이제 사용자가 중복 또는 잘라낸 텍스트 없이 검색 및 탐색을 완료할 수 있습니다. (SITES-25245)
* 이제 주석을 활성화하면 키보드 초점이 주석 종료 버튼이 아닌 주석 콘텐츠로 이동합니다. 탭 순서는 논리적 시퀀스를 따르며, 역방향 탐색 없이도 관련 제어가 연결 가능하도록 유지합니다. (SITES-25241)
* 날짜 설정 및 종료 타임워프 링크에 키보드 탐색 중 초점 표시기가 표시되지 않았습니다. 이제 UI가 뚜렷하고 대비가 높은 초점 스타일을 렌더링하므로 사용자가 활성 링크를 한 눈에 식별할 수 있습니다. (SITES-25232)
* 티저 모달 헤더가 더 이상 키보드 사용자가 대화 상자를 이동할 수 없도록 차단하지 않습니다. 키보드 제어는 이제 화면 판독기의 유용성과 전반적인 조작성을 향상시키는 픽업, 이동, 드롭 액션을 가능하게 합니다. (SITES-25226)
* 이제 AEM에서 티저 모달 정보 버튼에 의미 있는 액세스 가능한 레이블을 사용합니다. 화면 판독기는 기본 아이콘 대체 텍스트 문자열 대신 명확한 액션 이름을 발표합니다. (SITES-25223)
* 이제 화면 판독기에서 사용자가 편집 버튼을 활성화할 때 올바른 액션을 발표합니다. NVDA가 더 이상 “미리보기 버튼을 눌렀음”을 보고하지 않아 잘못된 피드백과 키보드 탐색 중 혼동을 초래했습니다. (SITES-25208)
* 왼쪽 레일을 확장하면 이제 키보드 초점이 첫 번째 왼쪽 레일 제어로 이동합니다. 탭 시퀀스가 더 이상 보조 도구 모음으로 이동하거나 중간 목록에 도달하지 않으므로 키보드 사용자가 역방향 탐색 없이 왼쪽 레일 콘텐츠에 도달할 수 있습니다. (SITES-24998)
* 이제 디바이스 에뮬레이터 바 콘텐츠가 320px 뷰포트 폭으로 전체 표시됩니다. 도구 모음 텍스트와 제어를 잘라내어 겹침을 줄이고 가독성을 향상시키는 대신 줄바꿈합니다. (SITES-24953)
* 이제 AEM이 에뮬레이터 도구 모음에 전체 iPhone 디바이스 레이블을 표시합니다. 텍스트가 더 이상 기본 폭에서 잘리지 않아 가독성과 디바이스 선택의 명확성이 향상됩니다. (SITES-24952)
* 이제 목록 보기 테이블 헤더가 ARIA를 통해 정렬 상태를 표시합니다. 화면 판독기가 열 정렬 액션 후에 오름차순 또는 내림차순을 알려 줍니다. (SITES-24943)
* 이제 AEM은 텍스트 간격 변경 시 카드 보기에서 자세히 액션 메뉴 레이블 가시성을 유지합니다. 메뉴 옵션이 빠른 게시를 포함한 전체 텍스트를 유지하며, WCAG 텍스트 간격 설정에서도 메뉴를 읽을 수 있습니다. (SITES-24941)
* 이제 카드 액션 메뉴 모음이 카드 보기에 액세스 가능한 이름을 표시합니다. 화면 판독기가 메뉴 모음 목적을 명확히 알려 주고, 음성 제어가 이름별로 컨트롤을 타기팅할 수 있습니다. (SITES-24938)
* 카드 보기가 더 이상 혼란스러운 화면 판독기 비헤이비어를 유발하는 ARIA 그리드 의미 체계를 사용하지 않습니다. UI가 이제 카드 콘텐츠와 카드 액션 바에 의미 있는 역할과 레이블을 제공하여 키보드 사용 중 누락된 컨트롤을 줄여 줍니다. (SITES-24933)
* 이제 사용자가 툴팁 아이콘을 마우스로 가리키면 `Delete Modal` 툴팁이 표시됩니다. 초점 액션이 이제 동일한 툴팁 텍스트를 표시하여 마우스와 키보드 사용자의 반복 액세스를 향상시킵니다. (SITES-24778)
* 왼쪽 레일 탐색이 이제 사용자가 레일을 구성한 후 예상되는 키보드 초점 순서를 따릅니다. 탭 초점이 스위치 디스플레이 대신 선택한 왼쪽 레일 영역에 위치하여 화면 판독기 탐색 선명도를 향상시킵니다. (SITES-24754)
* 사용자 환경 설정 모달에서 색상 견본 탐색 중 잘못된 NVDA 피드백을 수정했습니다. NVDA가 이제 초점을 받는 견본의 레이블을 읽어 잘못된 색상 출력이 제거됩니다. 이제 견본 세트가 일관된 키보드 탐색과 명확한 선택 인식을 지원합니다. (SITES-24739)
* `Spin` 제어에 대한 자세한 NVDA 출력이 감소했습니다. 입력 레이블을 복제한 중복 그룹 레이블을 제거했으므로 NVDA는 제어 이름을 한 번 알립니다. 키보드와 화면 판독기 탐색이 이제 하나의 명확한 알림을 제공합니다. (SITES-24725)
* 이제 슬라이드 대화 상자에 항목 탭 대신 대화 상자 제목에 초점이 배치됩니다. 취소 및 Esc가 대화 상자를 실행한 제어로 초점을 복원하여 장황한 NVDA 출력을 줄입니다. (SITES-24716)
* 이제 링크 선택 대화 상자가 마지막 단계 트리 항목에 대한 프로그램 레이블을 화면 레이블에 맞춥니다. 화살표 키 탐색이 각 항목에 대해 신뢰할 수 있는 화면 판독기 알림을 트리거하고 잘못된 레이블 출력을 제거합니다. (SITES-24710)
* 이제 링크 열기 선택 대화 상자가 320px 뷰포트에서 올바르게 리플로우됩니다. 콘텐츠가 더 이상 모달을 초과하거나 잘리지 않으며, 모달에 더 이상 가로 스크롤바가 표시되지 않습니다. (SITES-24709)
* 링크 열기 선택 대화 상자가 이제 닫기 또는 취소 후 대화 상자 트리거로 키보드 초점을 복원합니다. 초점이 더 이상 링크 입력으로 이동하지 않아 화면 판독기 컨텍스트가 안정적으로 유지되고 추가 탐색이 줄어듭니다. (SITES-24707)
* 이미지 모달 대화 상자가 이제 논리적 초점 시퀀스를 따릅니다. 초점이 더 이상 이전 제어를 건너뛰거나 취소 후 페이지 랜드마크에서 드롭되지 않으며, 종료 후 사용자는 구성 버튼에 다시 초점을 둡니다. (SITES-24693)
* 참조 레일 모달 대화 상자에 키보드 초점이 트래핑됩니다. Tab과 Shift+Tab이 대화 상자 제어 안에 있으며, 초점이 더 이상 페이지 콘텐츠로 이동하지 않습니다. 화면 판독기가 대화 상자 콘텐츠만 알려 줍니다. (SITES-24683)
* 이제 하이퍼링크 경로 선택 모달이 열리면 대화 상자 제목에 초점을 설정합니다. 취소하면 대화 상자가 닫히고 초점을 선택 열기 대화 상자 버튼으로 복원하여 초점 손실과 중복된 화면 판독기 출력을 방지합니다. (SITES-24672)
* 이제 검색 필드에서 플레이스홀더 텍스트 대신 영구 화면 레이블을 사용합니다. 레이블이 입력 중에도 계속 표시되어 키보드, 화면 판독기, 음성 사용자의 명확성을 향상시킵니다. (SITES-24529)
* 이제 티저 모달 대화 상자가 열리면 대화 상자 제목에 초점을 맞춥니다. 대화 상자를 닫으면 초점이 `Configure` 제어로 반환되어 초점이 손실되고 화면 판독기가 과도하게 출력되지 않습니다. (SITES-24522)
* 이제 측면 레일 에셋 패널에 닫기 제어가 포함됩니다. 닫기가 키보드 초점을 측면 레일 전환으로 반환하고 패널 콘텐츠를 억지로 탭하지 못하도록 합니다. (SITES-24489)
* 이제 키보드 탭이 관리자 테이블 내의 버튼과 링크에 도달합니다. 대화형 제어를 찾기 위해 화살표 키 셀 탐색에 더 이상 의존하지 않습니다. (SITES-24285)
* 이미지 구성 요소 대화 상자가 더 이상 이미지로 장식용 도움말 및 전체 화면 아이콘을 표시하지 않습니다. 이제 화면 판독기에서 이러한 아이콘을 건너뛰고 실행 가능한 제어 및 필드 내용에 초점을 둡니다. (SITES-2940)
* 이제 사이트 관리자가 폴더 썸네일 아이콘에서 이미지 역할을 제거합니다. 보조 기술이 이러한 장식 요소를 건너뛰고 폴더 이름과 액션에 초점을 유지합니다. (SITES-2852)
* 이제 콘텐츠 트리가 키보드 초점을 활성 트리 항목 또는 첫 번째 트리 항목으로 라우팅합니다. 트리 컨테이너가 더 이상 빈 탭 중지 역할을 하지 않으므로 Shift+Tab 초점 트랩을 방지합니다. (SITES-1577)

#### 관리자 사용자 인터페이스{#sites-adminui-65-lts-sp2}

Sites 콘솔 목록 보기 설정이 목록 보기에 표시된 열을 반영하지 않았습니다. 체크박스 선택이 취소되고 선택한 열이 올바르지 않은 상태로 대화 상자가 열립니다. 이 수정 사항을 통해 대화 상자가 활성 그리드 열과 상태를 동기화하고 실제 열 가시성과 일치하도록 카운터를 업데이트합니다. (SITES-38576)

#### 클래식 사용자 인터페이스{#sites-classicui-65-lts-sp2}

클래식 UI 텍스트 구성 요소 편집 시 업그레이드 후 서식 있는 텍스트 대신 원시 HTML 태그가 표시되었습니다. 서비스 팩 2가 편집기가 형식이 지정된 콘텐츠를 표시하고 저장된 마크업을 유지할 수 있도록 클래식 UI RTE(서식 있는 텍스트 편집기) 렌더링을 수정합니다. 또한 이 수정 사항을 통해 반복적인 편집 도중 마크업 확장을 중지하고 저장합니다. (SITES-38709)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp2}

6.5 LTS의 콘텐츠 조각 및 모델에 대한 필수 OSGi 이벤트는 헤드리스 이벤트 지원에 없었습니다. 이 업데이트에는 이벤트 번들과 필요한 종속성이 추가되며 6.5 LTS 빌드가 포함됩니다. 이제 콘텐츠 조각 및 모델 이벤트가 올바로 실행되며 론치 API 워크플로를 지원합니다. (SITES-35329)

#### [!DNL Content Fragments] - 관리자{#sites-admin-65-lts-sp2}

* 페이지 업데이트 중 불규칙한 비헤이비어를 중단하도록 Sites 저작 인터페이스에서 구성 요소 처리를 조정했습니다. 이 결함으로 인해 일상적인 콘텐츠 수정을 방해하고 워크플로 효율성을 떨어뜨리는 예측 불가의 편집기 응답이 발생했습니다. 이 업데이트로 예상되는 상호 작용 패턴에 따라 편집기 논리를 정렬하고 작성 활동 중에 신뢰할 수 있는 성능을 제공합니다. (SITES-35078) 중요

* 회귀로 인해 콘텐츠 조각에 대한 Assets 콘솔 목록 보기가 깨지고 목록 렌더링 중에 오류가 트리거되었습니다. 이 업데이트로 미리보기-정보 제거 후 목록-보기 논리를 수정하고 안정적인 목록 출력을 복원합니다. 이제 콘솔에 콘텐츠 조각이 오류 없이 표시되고 목록 상호 작용을 사용할 수 있도록 유지합니다. (SITES-38683)
* 이제 콘텐츠 조각 편집기에서 태그 레이블을 현지화합니다. 또한 편집기가 컬렉션 레이블을 현지화하므로 UI 텍스트가 선택한 로케일과 일치합니다. (SITES-977)


#### [!DNL Content Fragments] - 조각 편집기{#sites-fragments-editor-65-lts-sp2}

* 리팩터링 후 기능 토글이 비활성화된 상태로 유지되면 콘텐츠 조각 베리에이션 태그가 사라졌습니다. 이 수정 사항을 통해 토글이 꺼진 상태에서도 베리에이션 태그 지원을 복원합니다. 작성자가 콘텐츠 조각 편집기에서 베리에이션 태그를 다시 추가하고 볼 수 있습니다. (SITES-38682) 중요
* 작성자가 콘텐츠 조각 편집기에서 다시 탐색한 후 편집된 콘텐츠 조각이 Assets 콘솔 목록에서 사라졌습니다. 브라우저 캐싱이 documents 목록을 반환하고 수동으로 새로 고칠 때까지 업데이트된 조각을 숨겼습니다. 이 수정 사항을 통해 편집기 반환 경로에 대한 캐시 제어 처리를 추가하므로 목록이 올바르게 다시 로드되고 편집된 조각이 계속 표시되도록 합니다. (SITES-35374) 중요

* 콘텐츠 조각 RTE가 최근 UI 스타일 변경 후 레이아웃 및 시각적 문제를 표시했습니다. 서비스 팩 2는 도구 모음 및 편집 가능한 영역이 올바르게 렌더링되고 읽을 수 있도록 RTE 스타일을 구체화합니다. 이제 콘텐츠 조각 편집기가 페이지 편집기 모양과 비헤이비어에 맞게 조정됩니다. (SITES-38684)
* Polaris Asset Selector에서 IMS 범위를 제거하면 게재 엔드포인트와의 콘텐츠 조각 통합이 끊어졌습니다. 작성자가 원격 에셋 선택기를 열고 에셋을 선택할 때 오류가 발생합니다. 이 업데이트로 필요한 IMS 범위를 다시 추가하고 안정적인 게재 계층 액세스를 복원합니다. (SITES-35837)
* 연결된 컨텐츠 패널에서 더 이상 하드코딩된 &quot;정의되지 않은&quot; 자리 표시자가 렌더링되지 않습니다. 콘텐츠 조각 편집기는 이제 현지화 리소스를 통해 해당 텍스트를 확인하므로 편집자는 번역된 UI 텍스트를 확인합니다. (SITES-33675)
  <!-- REMOVED FROM BUG LIST FEBRUARY 13, 2026 * Preview error messaging now uses localized strings instead of raw `Cannot print fragment's Json` text. The Content Fragment Editor now shows translated output across locales during GraphQL endpoint resolution failures. (SITES-33666)-->
* 이제 콘텐츠 조각 편집기에 로케일 간에 번역된 일반 탭 레이블이 표시됩니다. 편집기가 현지화되지 않은 탭 텍스트를 바꾸고 탭 제목에서 내부 ID를 제거합니다. (SITES-30715)
* 이제 콘텐츠 조각 편집기에 허용된 에셋 유형에 대해 번역된 이름이 표시됩니다. 작성자가 콘텐츠 참조 제한 사항을 구성할 때 선택기 목록이 더 이상 내부 문자열과 영어 전용 레이블을 혼합하지 않습니다. (SITES-29699)

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp2}

* 필터 실행 오류로 인한 배포 실패를 중지하기 위해 GraphQL 쿼리 유효성 검사 처리를 개선했습니다. 이 결함이 애플리케이션 시작 중에 예외를 발생시켰으며 영향을 받는 환경에서 정상적인 롤아웃을 차단했습니다. 이 개정을 통해 일관된 유효성 검사 비헤이비어를 보장하며 런타임 쿼리 유효성 검사를 중단하지 않고 원활하게 배포할 수 있습니다. (SITES-34301) 중요

* 이제 GraphQL 엔드포인트 편집 대화 상자에 현지화된 UI 문자열이 표시됩니다. 대화 상자에 더 이상 “GraphQL 스키마는 구성에서 가져온 것입니다.”와 같은 영어 전용 텍스트가 표시되지 않고, 관련 레이블이 로케일에서 올바르게 렌더링됩니다. (SITES-34018)

#### [!DNL Content Fragments] - GraphQL 쿼리 편집기{#sites-graphql-query-editor-65-lts-sp2}

* 필터 실행 오류로 인한 배포 실패를 중지하기 위해 GraphQL 쿼리 유효성 검사 처리를 개선했습니다. 이 결함이 애플리케이션 시작 중에 예외를 발생시켰으며 영향을 받는 환경에서 정상적인 롤아웃을 차단했습니다. 이 개정을 통해 일관된 유효성 검사 비헤이비어를 보장하며 런타임 쿼리 유효성 검사를 중단하지 않고 원활하게 배포할 수 있습니다. (SITES-35529)
* 구성 브라우저 이름에 CJK 문자가 포함되어 있으면 더 이상 GraphQL 탐색기가 실패하지 않습니다. 엔드포인트 생성 및 저장된 쿼리 액세스가 정상적으로 작동하고 GraphQL 쿼리 편집기 페이지는 오류 없이 유지됩니다. (SITES-31616)

#### [!DNL Content Fragments] - 모델 편집기{#sites-model-editor-65-lts-sp2}

* 리팩터링이 기능을 비활성화된 토글에 연결하면 중첩된 콘텐츠 조각 모델이 작동하지 않습니다. 이 수정 사항을 통해 토글 변경 없이 중첩 모델 지원을 복원합니다. 작성자가 모델 편집기에서 중첩 모델을 다시 만들고 사용할 수 있습니다. (SITES-38681) 중요

* 콘텐츠 조각 모델 필터 패널이 더 이상 현지화되지 않은 문자열을 표시하지 않습니다. 이제 AEM에 모든 로케일에 걸쳐 현지화된 필터 레이블 및 현지화된 상태 값이 표시됩니다. (SITES-30863)
* 이제 콘텐츠 조각 모델 편집기에서 잠금 경고 대화 상자의 지역화된 문자열을 렌더링합니다. UI이 현지화되지 않은 영어 메시지를 지원되는 언어에 대한 로케일 리소스로 대체합니다. (SITES-28592)

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp2}

AEM Headless가 메인라인 빌드와의 종속성 및 번들 버전 충돌을 방지하기 위해 전용 릴리스 분기가 필요했습니다. 이 업데이트로 `release/6.5lts` 헤드리스 분기를 추가하고 종속성 집합 및 번들 버전을 정렬합니다. 이제 Jenkins가 버전 충돌 없이 헤드리스 코드 베이스를 깔끔하게 빌드합니다. (SITES-36585)

<!-- #### Component console{#sites-component-console-65-lts-sp2} -->

#### 콘텐츠 API{#sites-content-api-65-lts-sp2}

기능-토글 결함으로 페이지 관리 API 상태를 잘못 보고했습니다. 이 업데이트로 전용 활성화 플래그를 추가하고 기존 토글과 함께 평가합니다. 이제 페이지 관리 API에 안정적인 상태가 표시됩니다. 사이트 관리 API가 실험적으로 유지됩니다. (SITES-39284)

#### 핵심 백엔드{#sites-core-backend-65-lts-sp2}

* 표준 페이지 편집 워크플로를 방해하는 일관되지 않은 비헤이비어를 해결하기 위해 Sites 저작 경험이 변경되었습니다. 작성자가 구성 요소 상호 작용 중에 예기치 않은 결과가 발생하여 콘텐츠 업데이트가 방해되고 신뢰성이 저하되었습니다. 이 변경 사항을 통해 안정적인 편집기 비헤이비어를 복원하고 영향을 받는 시나리오 간에 작성 액션을 일관되게 실행합니다. (SITES-35162) 중요

* 구성 요소 상호 작용 중 페이지 편집을 방해하고 일관되지 않은 결과를 초래한 문제를 해결하기 위해 Sites 작성 비헤이비어를 개선했습니다. 작성자가 콘텐츠 업데이트를 방해하고 워크플로 안정성을 감소시키는 예기치 않은 UI 응답을 경험했습니다. 이 변경 사항을 통해 안정적인 편집기 상태 관리를 복원하고 영향을 받는 시나리오 간에 작성 액션을 예측 가능하게 실행합니다. (SITES-34499)

<!--
#### Core Components{#sites-core-components-65-lts-sp2}

#### Campaign integration{#sites-campaign-integration-65-lts-sp2}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp2}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp2}
-->

#### 론치{#sites-launches-65-lts-sp2}

* Sites 타임라인에 론치 프로모션 시 하드코딩된 영어 텍스트 표시: “실행 프로모션 전 버전 ... 생성됨” 이 업데이트로 하드코딩된 문자열을 현지화된 메시지 처리로 대체합니다. 이제 타임라인에 현지화된 텍스트가 표시되고 표준 AEM 현지화 동작에 따라 항목이 정렬됩니다. (SITES-39157)
* 론치 프로모션 범위가 작성자가 현재 페이지 및 하위 페이지 홍보를 프로모션하여 하위 섹션을 프로모션하면 표류했습니다. 또한 AEM이 관련 없는 페이지를 프로모션하여 예기치 않은 라이브-사이트를 수정했습니다. 이 수정 사항을 통해 선택한 하위 트리만 프로모션되도록 론치 범위 계산을 수정합니다. (SITES-38315)
* 론치 내의 콘텐츠 조각이 `damAssetLucene` 색인과 제한된 검색 결과 및 쿼리 효율성에 참여하지 않았습니다. 이 변경 사항을 통해 론치 콘텐츠 조각 경로를 색인 정의에 추가합니다. 이제 검색 및 사용자 정의 쿼리가 `/content/launches`에서 콘텐츠 조각을 찾습니다. (SITES-35634)
* 제품이 Touch UI에 콘텐츠 조각 Launches를 표시하지 않지만 론치 UI에 콘텐츠 조각 실행 제어가 표시됩니다. 이 변경 사항을 통해 cq-launches-content에서 콘텐츠 조각 론치 코드 경로를 제거하고 론치 목록 필터링을 조정합니다. 이제 작성자가 콘텐츠 조각 론치 항목 없이 일관된 페이지 론치 옵션을 볼 수 있습니다. (SITES-35633)
* AEM 6.5 LTS Quickstart에는 필요한 론치 번들 및 사전 요구 사항이 없어서 론치 OpenAPI 활성화가 차단되었습니다. 이 업데이트로 론치 번들 및 필요한 종속성(예: 지표 지원, DAM-cfm 업데이트 및 대기열 구성)이 추가됩니다. 론치 API가 이제 필요한 런타임 구성 요소가 있는 6.5 LTS Quickstart에서 실행됩니다. (SITES-35297)
* CF Launches가 새로운 종속성 버전과 불필요한 GraphQL 라이브러리를 패키지화하여 AEM 6.5 LTS 통합이 복잡했습니다. 이 변경 사항을 통해 종속성 버전을 AEM 6.5 LTS 기준선에 맞추고 사용하지 않는 GraphQL 종속성을 제거합니다. 이제 번들 해상도가 일관되고 CF 론치 시작이 안정적으로 유지됩니다. (SITES-35295)
* 이제 AEM Launches에서 6.5 LTS 분기에 대한 전용 Jenkins 파이프라인을 실행합니다. 이 파이프라인이 매일 밤 빌드를 실행하고 이메일로 오류 알림을 보냅니다. 이 설정으로 테스트 범위를 늘리고 회귀를 조기에 포착합니다. (SITES-35293)
* AEM 6.5 LTS가 이제 정렬된 아티팩트 버전과 함께 업데이트된 론치 API 번들을 제공합니다. 번들이 올바른 6.5 LTS 릴리스 버전을 유지하면서 기본 코드 행을 추적합니다. 이 업데이트로 6.5 LTS 스택에서 론치 API 소비를 안정화합니다. (SITES-35292)
* 이제 AEM 6.5 LTS에 종속성 버전이 정렬된 업데이트된 실행-코어 번들이 포함되어 있습니다. 이 업데이트로 조각 UUID 및 참조 UUID 데이터 유형에 대한 실행-코어 처리를 추가합니다. 이제 론치 처리를 통해 론치 및 콘텐츠 조각 워크플로 전반에서 일관된 비헤이비어가 유지됩니다. (SITES-35290)
* 일반 페이지 작성 워크플로를 중단시킨 일관되지 않은 비헤이비어 해결하기 위해 Sites 편집기를 개선했습니다. 작성자가 예기치 않은 구성 요소 상호 작용을 하여 콘텐츠 업데이트가 방해되고 편집 안정성이 저하되었습니다. 이 변경 사항을 통해 일관된 UI 상태 관리를 복원하고 영향을 받는 시나리오 간에 작성 액션을 예측 가능하게 실행합니다. (SITES-35138)
* 이제 론치 편집에 하드코딩된 `Provided path is not a launch` 문자열 대신 현지화된 오류 텍스트가 표시됩니다. 이제 편집이 잘못된 실행 경로를 수신하면 UI는 번역된 메시지를 언어 간에 렌더링합니다. (SITES-33360)
* 이제 AEM 6.5 LTS에 론치 OpenAPI 사이드 포트 작업이 포함됩니다. 이 업데이트로 론치 API 번들, 콘텐츠 패키지 및 필수 Quickstart 아티팩트를 패리티로 가져오며 안정적인 CI 유효성 검사로 콘텐츠 조각 론치 OpenAPI 시나리오를 활성화합니다. (SITES-32050)
* 론치 UI가 이제 재정의된 템플릿 레이블을 현지화합니다. 이제 템플릿 재정의 세부 정보에 영어 전용 문자열 대신 번역된 텍스트가 표시됩니다. (SITES-29525)
* AEM에서 **Sites** > **Launches** > **편집**&#x200B;에서 누락된 지역화 키를 해결했습니다. 이제 사용자에게 원시 “실행 소스 목록을 업데이트할 수 없음” 문자열 대신 번역된 오류 메시지가 표시됩니다. (SITES-21499)
* 이제 론치 프로모션 UI에 현지화된 상태 레이블 및 액션이 표시됩니다. 미리보기 영역에 원시 영어 문자열이 아닌 **삭제됨**, **새로 만들기** 및 **보기**&#x200B;에 대한 번역된 텍스트가 표시됩니다. (SITES-13540)
* 이제 론치 생성에 현지화된 오류 메시지가 표시됩니다. UI가 더 이상 `Unable to create launch page`, `Source root resource is not a page` 또는 `Mandatory parameter is missing`과 같은 원시 영어 문자열을 표시하지 않습니다. (SITES-13085)


<!-- #### Link Checker{#sites-link-checker-65-lts-sp2} -->


#### MSM - Live Copy{#sites-msm-live-copies-65-lts-sp2}

* 관리자가 콘텐츠 변경 중 MSM 수정되면 푸시 처리에 대한 가시성에 제한을 받았습니다. 이 수정 사항을 통해 MSM 이벤트 수신 및 롤아웃 실행에 대한 자세한 로깅을 추가합니다. 이제 디버그 출력에 실행된 이벤트, 변경된 콘텐츠 경로 및 변경 사항을 트리거한 사용자가 표시됩니다. (SITES-38029)
* AEM에서 블루프린트 롤아웃 날짜 필드의 지역화 레이아웃 문제를 수정했습니다. 이제 날짜 프롬프트가 제어에 적합하고 `fr_FR`를 포함하여 지원되는 언어에서 읽을 수 있습니다. (SITES-14961)

<!-- #### Page editor{#sites-pageeditor-65-lts-sp2} -->

#### 복제{#sites-replication-65-lts-sp2}

이제 페이지 편집기 게시가 선택기 또는 접미사가 포함된 URL을 처리합니다. 게시된 요청이 이제 선택기나 접미사 URL 문자열이 아닌 JCR 페이지 경로를 전송하여 활성화가 완료되고 콘텐츠가 활성화됩니다. 이제 복제가 실패 시 오류 상태를 반환하여 잘못된 “게시 시작됨” 메시지를 방지합니다. (NPR-43288)

<!-- #### Rich Text Editor{#sites-rte-65-lts-sp2} -->

#### 템플릿 편집기{#sites-template-editor-65-lts-sp2}

템플릿 상태 텍스가 일부 로케일의 경우 **도구** > **일반** > **템플릿**&#x200B;에 세로로 표시되었습니다. “오래됨” 레이블이 레이아웃을 깨고 문자 열로 읽혔습니다. 이 수정 사항을 통해 레이블이 단일 가로 행에서 렌더링되도록 템플릿 상태 스타일을 수정합니다. (SITES-36797)

#### 범용 편집기 {#sites-universal-editor-65-lts-sp2}

* OSGi 기본 구성이 `preview=true`로 설정되었으며 범용 편집기가 미리보기 모드에서 시작하도록 강제되었습니다. 이 업데이트로 기본값을 수정하고 표준 프로덕션 입력 비헤이비어를 복원합니다. 이제 관리자가 미리보기 모드를 명시적으로 활성화하지 않는 한 범용 편집기는 프로덕션 모드에서 열립니다. (SITES-37193)
* 이제 범용 편집기 열기 명령은 개발 및 스테이징 환경에서 기본적으로 미리보기 모드로 설정됩니다. 명령이 `preview=true`를 추가하여 작성자 검사를 미리보기 컨텍스트와 정렬하고 실수로 프로덕션이 열리지 않도록 합니다. (SITES-33839)

### [!DNL Assets]{#assets-65-lts-sp2}

이제 Assets 연결이 공백을 포함하는 파일 이름에 대해 작동합니다. 이제 업데이트된 연결 클라이언트 논리가 공간이 포함된 경로를 올바르게 처리하고 관계 선택 중 `undefined` 소스 오류를 방지합니다. 이제 연결 대화 상자가 열리고 UI 중단이나 회전기 없이 관계가 저장됩니다. DAM 사용자가 파일 이름을 변경하지 않고도 에셋의 연결, 도출 및 연결 해제할 수 있습니다. (Assets-56418)

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp2}

* 새로운 Dynamic Media 비디오 플레이어 통합(제한된 롤아웃) - 이제 AEM 6.6 Quickstart에서 새로운 Dynamic Media 비디오 플레이어 경험을 누릴 수 있습니다. 이 개선 사항을 통해 현재 제어된 롤아웃의 일부로서 초기 고객에게만 활성화되어 있습니다. (Assets-60165)
* 비디오 속성 대화 상자의 썸네일 선택 옵션이 에셋 선택기를 열지 않았던 문제를 해결하여 사용자가 비디오 에셋에 대한 사용자 정의 썸네일을 선택할 수 있는 기능이 복원되었습니다. (Assets‑58926)
* Dynamic Media 비디오에서 자막 및 오디오 트랙 언어 드롭다운 목록에서 아랍어를 선택할 수 있는 지원이 추가되어 작성자가 AEM에서 직접 아랍어 자막을 관리할 수 있습니다. (Assets‑61771)

<!-- #### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp2} -->

### [!DNL Forms]{#forms-65-lts-sp2}

* 사용자에게 양식 데이터 모델(FDM) 편집기 `Data Source / Enter Keyword` 기능에 문제가 발생했습니다. 이 문제가 데이터 소스 검색 및 선택 기능에 영향을 주었습니다. (FORMS-23971)
* 모바일 디바이스에서 적응형 양식의 테이블 구성 요소가 맨 위에 숨겨진 헤더를 렌더링하여 화면 판독기에서 콘텐츠를 잘못 알렸습니다. 이로 인해 화면 판독기에 의존하여 탐색하는 사용자가 영향을 받았습니다. (FORMS-23754)
* 사용자에게 granite:InternalArea로 플래그가 지정된 리소스 유형을 참조하는 적응형 양식 기반의 핵심 구성 요소와 관련된 문제가 발생했습니다. 이로 인해 온프레미스 Forms 추가 기능에 있는 여러 granite 구성 요소의 기능에 영향을 받았습니다. (FORMS-23632)
* AEM 6.5 LTS SP1로 업그레이드한 후 양식을 제출하지 못했습니다. 사용자에게 com.adobe.cq.social.commons.CollabUtil 이 누락되어 JSP 컴파일 오류가 발생하고 이메일 액션이 실패했습니다. (FORMS-23457)
* 사용자가 적응형 양식 기반의 기초 구성 요소에서 hCaptcha가 올바르게 번역되지 않는 문제를 겪었습니다. 이로 인해 비영어권 사용자가 양식을 정확하게 완성할 수 있는 기능이 영향을 받았습니다. (FORMS-23426)
* 사용자가 SAXParseException으로 인해 양식 제출 오류를 경험했습니다. “콘텐츠가 프롤로그에서 허용되지 않습니다.”(HTTP 500). 이 문제가 미리 채우기 데이터 XML의 null 값으로 인해 발생하여 서버측 XML 구문 분석이 실패했습니다. (FORMS-22633)
* 사용자가 WCAG(웹 콘텐츠 접근성 지침) 감사에서 적응형 양식 실패를 경험했습니다. 그 이유는 양식의 탭 탐색 마크업이 잘못되었기 때문입니다. 즉, 목록 요소가 아닌 요소는 목록의 직접 하위로 렌더링되며, 여기서 목록 항목만 허용됩니다. 이 문제로 인해 양식에서 접근성 유효성 검사기를 전달할 수 없었고 법적 또는 내부 규정 준수 요구 사항을 충족해야 하는 조직도 영향을 받았습니다. (FORMS-22101)
* 사용자에게 기록 문서(DoR) / 제출 PDF에서 빈 양식 필드에 양식 요소로 태그가 지정되지 않은 접근성 문제가 발생했습니다. 이로 인해 화면 판독기에 문제가 발생하여 장애가 있는 사용자가 양식을 효과적으로 탐색하고 완료할 수 있는 기능이 영향을 받았습니다. (FORMS-21989)
* 사용자에게 양식 로드 중에 하위 패널 내의 구성 요소에 대한 각주가 표시되지 않는 문제가 발생했습니다. 이 문제는 각주가 있는 항목이 페이지의 마지막 구성 요소일 때 발생했습니다. (FORMS-21925)
* 사용자가 AEM Forms 편집기에서 구성 요소를 선택할 때 문제가 발생했습니다. 탭 사이를 이동하고 첫 번째 탭으로 돌아갈 때 일부 컨테이너는 선택할 수 없게 되어 쉽게 식별하고 상호 작용하지 못하게 되었습니다. (FORMS-21814)
* 사용자가 적응형 양식 대시보드에서 보안 취약성을 경험했습니다. 특히 startpointcontrol.js 파일에서 XSS(크로스 사이트 스크립팅) 문제가 확인되었으며, 이로 인해 악의적인 스크립트가 실행될 수 있습니다. (FORMS-20679)
* JBoss® EAP 8에 대한 AEM Forms 6.5 LTS 클러스터 배포에서 `domain/configuration/domain_oracle.xml`, `domain_mysql.xml` 및 `domain_mssql.xml` 파일에 잘못된 XML을 야기하고 도메인 컨트롤러를 시작하지 못하게 하는 중복 `<security>` 태그가 더 이상 포함되지 않습니다. (FORMS-24687)
* 이제 턴키 모드에서 새로 설치 및 업그레이드하는 동안 데이터베이스 포트 업데이트가 올바르게 적용됩니다. 사용자가 새로 설치 모드에서 사용 가능한 모든 포트 중 선택할 수 있으며, 업그레이드 모드에서 lc_turnkey.xml의 업데이트된 데이터베이스 포트가 업그레이드 프로세스 중에서 올바르게 참조됩니다. (FORMS-24689)
* Linux®에서 JBoss® EAP 8.0을 설정할 때 Windows에서 수정된 셸 스크립트가 더 이상 CRLF 줄 끝으로 인해 `/bin/sh^M: bad interpreter or $'\r': command not found` 오류가 발생하지 않습니다. (FORMS-24688)
* JBoss® EAP 8에서 실행 중인 Forms JEE LTS 배포에서 Reader 확장 UI가 내부 서버 오류로 실패할 수 있습니다. (FORMS-24894)
* Linux®에서 Forms JEE LTS 구성 관리자가 `configurationManager/config/solcomp/LFS_Foundation.properties`에서 설정이 해제되었거나 잘못된 `OSFileSetIntendedFor` 값으로 실행될 때 사용자들이 런타임 또는 배포 문제를 겪었으며, 이로 인해 Linux®에 맞게 구성을 올바르게 조정할 수 없었습니다. 설치 후 구성 관리자를 실행하기 전에 해당 파일에서 `OSFileSetIntendedFor=Linux`를 설정합니다. (FORMS-24741)

<!--
#### Forms JEE 

#### Forms Captcha {#forms-captcha-65-lts-sp2}

#### XMLFM {#forms-xmlfm-65-lts-sp2}

#### [!DNL Adaptive Forms] {#adaptive-forms-65-lts-sp2}

#### [!DNL Forms Designer] {#forms-designer-65-lts-sp2}

#### Forms Designer

#### AdaptIve Forms

#### Forms Captcha

#### Forms Management UI
-->


### 기초 {#foundation-65-lts-sp2}

#### Apache Felix {#foundation-apachefelix-65-lts-sp2}

* 이제 Sling 리소스 액세스 보안이 버전 1.1.2에서 실행됩니다. 여러 ResourceAccessGateHandler 서비스를 등록할 때 ResourceAccessSecurityImpl에서 초기화 중에 더 이상 ClassCastException이 발생하지 않습니다. 초기화가 안정적으로 완료되어 여러 핸들러가 있는 환경에서 시작 오류가 발생하지 않습니다. (NPR-42750)
* 이제 JMX 콘솔 및 웹 콘솔에서 콘솔 CSS 리소스에 대한 `Content-Type: text/css header`를 보냅니다. 엄격한 MIME 검사를 통해 스타일 시트 로드가 더 이상 차단되지 않으므로 `/system/console/jmx` UI가 일반적인 스타일로 렌더링됩니다. (GRANITE-63677)
* 이제 AEM에서 생성된 `WEB-INF/resources/provisioning/model.txt`의 `contributor` 그룹에 대해 중복 ACL 항목을 방지합니다. 이제 WAR 출력에 하나의 일관된 ACL 블록이 포함되어 있으므로 검토 중에 혼동을 주는 권한 차이를 방지할 수 있습니다. (GRANITE-63269)
* AEM에서 번들 새로 고침 작업 중에 더 이상 Deserialization Firewall 차단 목록 및 허용 목록 설정을 지우지 않습니다. 업데이트된 필터 등록 논리가 활성 방화벽 인스턴스를 저장된 구성과 정렬하므로 다시 시작하지 않고도 보호가 활성화된 상태를 유지합니다. (GRANITE-61382)
* Felix 웹 콘솔이 `/system/console` 액세스 중에 더 이상 간헐적인 `NullPointerException` 오류를 발생시키지 않습니다. 업데이트된 ServiceTracker 처리로 인해 null 추적기 상태가 방지됩니다. 콘솔 로그인 및 탐색이 반복된 요청 및 자동화된 유효성 검사 동안 안정적으로 유지됩니다. (GRANITE-61042)

<!--
#### Campaign{#foundation-campaign-65-lts-sp2}

#### Cloud Services{#foundation-cloudservices-65-lts-sp2}

#### Communities {#foundation-communities-65-lts-sp2}

#### Content distribution{#foundation-content-distribution-65-lts-sp2}
-->

#### CRX {#foundation-crx-65-lts-sp2}

서비스 팩 업그레이드 후 JSP 파일을 열 때 CRXDE Lite에 더 이상 빈 탭이 표시되지 않습니다. AEM이 이제 일치하는 CodeMirror 코어 및 추가 기능 코드를 제공하므로 치명적인 브라우저 오류를 방지하고 편집기를 계속 사용할 수 있습니다. (GRANITE-64333)

#### Granite{#foundation-granite-65-lts-sp2}

이제 Expression Security 유효성 검사기가 비어 있거나 null인 OSGi 구성 값을 처리합니다. 안전한 기본값을 적용하고, 빈 배열을 무시하며, 명확한 로그를 보고하여 NullPointerException 및 예측 불가능한 유효성 검사 결과를 방지합니다. (NPR-43163)

<!-- #### HTL{#foundatoin-htl-5-lts-sp2} -->

#### 통합{#foundation-integrations-65-lts-sp2}

이제 AEM이 시작 및 종료 일자가 있는 경우에도 Adobe Target 활동을 동기화합니다. 이제 Target 페이로드가 활동 날짜를 초, 밀리초 및 시간대를 포함한 전체 ISO 8601 타임스탬프로 지정합니다. Target이 더 이상 `InvalidJson.Json`으로 요청을 거부하지 않습니다. 이제 예약된 활동이 동기화되지 않은 상태로 유지되는 대신 동기화된 상태로 이동합니다. (CQ-4360733)

<!--
#### Jetty{#foundation-jetty-65-lts-sp2}

#### Localization{#foundation-localization-65-lts-sp2} 

#### Omnisearch{#foundation-omnisearch-65-lts-sp2}

#### Platform{#foundation-platform-65-lts-sp2}

#### Projects{#foundation-projects-65-lts-sp2}
-->

#### Oak {#foundation-oak-65-lts-sp2}

AEM 6.5 LTS 서비스 팩 2에는 S3 Connector 1.60.10 이상이 필요합니다. 이제 S3 데이터 저장소 구성에 `crossRegionAccess` 및 `mode`가 포함되어 있으므로 관리자는 필요한 경우 교차 영역 버킷 액세스를 활성화하고 스토리지를 GCP로 전환할 수 있습니다. 이제 `s3EndPoint`가 `s3Region`에 정렬된 영역이 필요하거나, 드라이버가 엔드포인트를 생성하도록 영역이 비어 있습니다. (GRANITE-64873)


#### Quickstart{#foundation-quickstart-65-lts-sp2}

* Sling이 포괄적인 용어와 새로운 구성 PID를 사용하도록 관리 로그인 허용 목록을 업데이트합니다. 이 변경 사항을 통해 Sling JCR Base 3.2.0에 맞게 조정됩니다. (GRANITE-63756)

  **영향**

   * Sling이 이러한 PID를 더 이상 사용하지 않으므로 구성에서 제거해야 합니다.
      * 팩토리 PID: `org.apache.sling.jcr.base.internal.LoginAdminWhitelist.fragment`
      * 글로벌 PID: `org.apache.sling.jcr.base.internal.LoginAdminWhitelist`
이러한 이전 구성은 `whitelist.name` 및 `whitelist.bundles`와 같은 속성을 사용합니다.

   * Sling이 더 이상 사용되지 않는 PID에 대해 부분 이전 버전과의 호환성을 제공하지만 새 구성에 대해서는 사용하지 않습니다. 대신 최신 `LoginAdminAllowList.*` PID를 사용하십시오.
   * 더 이상 사용되지 않는 구성과 새로운 허용 목록을 동시에 실행하지 마십시오. 혼합 구성이 모호성을 만들고 의도하지 않은 비헤이비어를 생성할 수 있습니다. AEM 6.5 LTS SP2로 마이그레이션하는 경우 더 이상 사용되지 않는 PID를 완전히 제거하십시오.

  **해야 할 일**

   1. `LoginAdminWhitelist*` PID를 사용하는 허용 목록 구성을 찾습니다.
   1. 적절한 새 PID로 바꿉니다.

      * 팩토리 PID: `org.apache.sling.jcr.base.LoginAdminAllowList.fragment`
      * 글로벌 PID: `org.apache.sling.jcr.base.LoginAdminAllowList`

      자세한 내용은 [관리자 로그인을 위해 더 이상 사용되지 않는 허용 목록 번들 접근](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecated-approach-to-allowlist-bundles-for-administrative-login)을 참조하십시오.

* AEM 6.5 LTS SP2가 Sling, Oak 및 Felix용 기초 레이어 번들 세트를 업데이트합니다. 이러한 업그레이드로 핵심 런타임 안정성을 강화하고 플랫폼 간에 종속성 버전을 조정합니다. (GRANITE-61874)

<!--
#### Security{#foundation-security-65-lts-sp2}

AEM now prevents NullPointerException errors when a logged-in user lacks read access for some groups and opens the Groups tab. The tab now hides groups without access and renders group membership details without a blank or unresponsive UI. (NPR-43311)
-->

#### Sling{#foundation-sling-65-lts-sp2}

이제 AEM에 Sling 엔진 2.16.6이 포함됩니다. 이 변경 사항을 통해 보안 도구로 플래그가 지정된 XSS 위반을 제거하고 핵심 렌더링 안전성과 안정성을 개선합니다. (NPR-43105)

<!--
#### Translation{#foundation-translation-65-lts-sp2}

#### User interface{#foundation-ui-65-lts-sp2}
-->

#### WCM{#foundation-wcm-65-lts-sp2}

XLIFF 포맷 문제로 인해 AEM 번역이 Java 17 또는 Java 21에서 더 이상 실패하지 않습니다. 내보내기 파이프라인이 이제 번역 공급자가 수락하는 표준 호환 XLIFF를 생성합니다. 이 변경 사항을 통해 번역 작업 중단을 제거하고 AEM과 번역 서비스 간에 예측 가능한 전환을 복원합니다. 이제 번역 워크플로가 지원되는 Java 런타임 동안 안정적으로 유지됩니다. (CQ-4360217)

#### 워크플로{#foundation-workflow-65-lts-sp2}

워크플로 알림을 처리하는 동안 EmailNotificationService-Processor에서 더 이상 반복적인 “세그먼트를 찾을 수 없음” 오류가 트리거되지 않습니다. 업데이트된 예외 처리가 SegmentNotFoundException을 탐지하고 잘못된 읽기를 계속하는 대신 처리 루프를 중지합니다. 워크플로 실행이 받은 편지함 및 작업 항목 액세스 중에 안정적으로 유지되며 로그 노이즈 감소가 발생합니다. (GRANITE-62635)




## [!DNL Experience Manager Foundation] 정보 {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS의 플랫폼은 OSGi 기반 프레임워크(Apache Sling 및 Apache Felix)와 Java™ 콘텐츠 저장소인 Apache Jackrabbit Oak 1.68.x의 업데이트된 버전을 기반으로 빌드되었습니다.

Eclipse Jetty 11.0.x는 Quickstart의 서블릿 엔진으로 사용됩니다.

### Java™ 지원  {#java-support}

* Java™ 17 및 Java™ 21이 지원됩니다.
* 최적의 성능을 위해 기본 GC 값을 다른 값으로 재정의합니다. 자세한 내용은 [설치 및 업데이트](/help/sites-deploying/custom-standalone-install.md) 섹션을 참조하십시오.
* Adobe는 Oracle에서 공개적으로 제공되지 않는 경우 AEM 관련 프로젝트에서 고객이 사용할 수 있도록 Java™ 17 및 Java™ 21 유지 관리 업데이트를 배포합니다.

### Uberjar 패키징 {#uber-jar-packaging}

AEM 6.5 LTS SP2용 UberJar가 AEM 6.5 LTS UberJar 버전 6.6.2를 사용합니다. Maven 중앙 저장소에서 해당 UberJar 아티팩트를 검색할 수 있습니다. AEM 6.5와 달리 AEM 6.5 LTS는 공개 API와 더 이상 사용되지 않는 API를 두 개의 서로 다른 아티팩트로 구분합니다.

공개 API에 대해 컴파일하려면 다음을 사용하십시오.

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.2</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

코드도 더 이상 사용되지 않는 API에 따라 달라지는 경우 다음을 추가하십시오.

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.2</version>
    <classifier>deprecated-apis</classifier>
    <scope>provided</scope>
</dependency>
```

또한 [AEM Uber Jar 버전 업데이트](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)를 참조하십시오.

### 업그레이드 {#upgrade}

* 업그레이드 절차에 대한 자세한 내용은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.
* 자세한 업그레이드 지침은 [JEE의 AEM Forms 6.5 LTS SP1 업그레이드 안내서](https://experienceleague.adobe.com/ko/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade) 참조

#### AEM 6.5 LTS 서비스 팩 업그레이드에 대한 모범 사례

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

**환경**
적용 대상: 서비스 팩 2(SP2)을 설치하는 AEM 6.5 LTS(On-Premise) 고객 SP2가 Quickstart JAR로 제공됩니다.

**이러한 업그레이드 사례가 중요한 이유**
AEM 6.5 LTS용 SP2가 패키지 관리자를 통해 설치하기 위해 ZIP이 아닌 Quickstart JAR로 제공됩니다. On-prem 고객은 Quickstart JAR를 대체하고 압축을 푼 다음 다시 시작하여 업그레이드합니다. 이 방법은 Adobe의 즉석 업그레이드 절차와 일치합니다.

**권장 업그레이드 흐름(작성자 또는 게시)**

1. AEM 6.5 LTS 인스턴스가 정상적이고 액세스할 수 있는지 확인합니다.
1. 소프트웨어 배포에서 Quickstart JAR(예: `cq-quickstart-6.6.x.jar`)을 다운로드합니다.
1. 실행 중인 인스턴스를 중단합니다.
1. AEM 설치 디렉터리(`crx-quickstart/` 외부)에서 이전 Quickstart JAR를 SP2 JAR로 대체합니다.
1. JAR 압축을 풉니다.

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   (필요에 따라 힙 플래그를 조정합니다.)

1. 역할 및 포트와 일치하도록 압축 해제된 JAR의 이름을 변경합니다(예: `cq-author-4502.jar` 또는 `cq-publish-4503.jar`).
1. AEM을 시작하고 UI(도움말 > 정보) 및 로그에서 업그레이드를 확인합니다.

**위생 관리**

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


세부 지침은 [업그레이드 설명서](/help/sites-deploying/upgrade.md)를 참조하십시오.

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

고객은 현재 배포에서 이 기능을 사용하는지 검토하는 것이 좋습니다. 제공된 대체 요소를 사용하도록 구현을 변경할 계획을 세웁니다.

| 영역 | 기능 | 대체 | 버전(SP) |
| --- | --- | --- | --- |
| Quickstart | Mongo API | Mongo API는 이제 더 이상 사용되지 않으며 향후 릴리스에서 제거될 예정입니다. | 6.5 TS SP2 |
| Sites | AEM Assets REST API의 콘텐츠 조각 지원 | AEM 6.5 LTS SP2가 콘텐츠 조각 및 모델 관리를 위한 최신 OpenAPI를 제공하므로 AEM Assets REST API의 이전 콘텐츠 조각 지원 엔드포인트는 이제 더 이상 사용되지 않습니다.<br>Adobe는 서비스 종료 공지가 있을 때까지 이러한 이전 엔드포인트를 사용할 수 있도록 유지합니다. Adobe에서는 더 이상 사용되지 않는 엔드포인트에 대한 추가 개선 사항을 계획하지 않습니다. | 6.5 LTS SP2 |
| Sites | [SPA 편집기](/help/sites-developing/spa-overview.md) | AEM에서 헤드리스 콘텐츠 관리에 권장되는 편집기는 <br>- [범용 편집기](/help/sites-developing/universal-editor/introduction.md)(시각적 편집용) <br>- [콘텐츠 조각 편집기](/help/assets/content-fragments/content-fragments-managing.md)(양식 기반 편집용)입니다. | 6.5 LTS GA |
| [!DNL Foundation] | com.adobe.granite.oauth.server 지원 | Adobe IMS 통합 |  |

### 제거된 기능 {#removed-features}

이 섹션에는 AEM 6.5 LTS에서 제거된 기능이 나열됩니다. 이전 릴리스에서는 이러한 기능이 더 이상 사용되지 않는다고 표시되었습니다.

* CRX 저장소 지속성을 위한 RDBMK 지원이 제거되었습니다.
* 클러스터된 환경에서는 이제 MongoMK가 저장소 지속성에 대한 유일한 지원 옵션입니다.

| 영역 | 기능 | 대체 | 버전(SP) |
| --- | --- | --- | --- |
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

* 구성 관리자에서 모듈을 선택하지 않았거나 제한된 구성 요소만 선택한 경우 AEM Forms 6.5 LTS JEE 턴키 사용자 정의 모드의 Bootstrap 중에 데이터베이스 초기화가 실패합니다. 이 실패는 종속성(xalan-2.7.2.jar)이 누락되어 오류가 발생했기 때문입니다. adobe-livecycle-jboss.ear\lib에 JAR 파일을 추가하면 문제가 해결됩니다. (FORMS-24690)
* WebSphere® Liberty Profile에서 실행 중인 Forms JEE LTS 서비스 팩 2 배포에서 이메일 기능이 실패할 수 있습니다. 전자 메일 기능을 사용하려고 할 때 서버에서 오류 `Could not convert socket to TLS`을(를) 기록합니다. (FORMS-24692)
* JBoss®에서 실행 중인 Forms JEE LTS에서 이메일 관련 기능이 실패할 수 있습니다. 전자 메일 기능을 사용하려고 할 때 서버에서 오류 `Error IMAPProvider not a subtype`을(를) 기록합니다. 이 문제를 해결하려면 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-core-jboss.ear)에서 핫픽스를 설치하십시오. (FORMS-24892)

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
> 핫픽스를 설치한 후 설치된 모든 번들의 번들 상태를 확인하여 `com.adobe.granite.apicontroller`의 기본 구성에 기존 사용자 지정 구현에 영향을 줄 수 있는 의도하지 않은 해결 제한 사항이 적용되지 않았는지 확인하십시오.

### JSON 댓글은 최초 콘텐츠 슬링(SP2)에서 더 이상 지원되지 않음 {#json-comments-no-longer-supported-in-sling-initial-content}

이 문제는 JSON 파일과 함께 `Sling-Initial-Content`를 사용하는 번들을 배포하는 OSGi 번들 개발자 및 관리자에게 영향을 줍니다.

AEM 6.5 LTS SP2부터 `Sling-Initial-Content` 번들에 사용된 JSON 파일에 더 이상 댓글(`//` 또는 `/* */`)이 허용되지 않습니다. 이전 AEM 릴리스에서는 `javax.json` 제공자가 이 문제에 대해 엄격하지 않아 댓글이 허용되었습니다. AEM 6.5 LTS SP2는 `org.apache.sling.jcr.contentloader`를 2.6.0 버전으로 업그레이드했으며 이로 인해 JSON 파서가 `jakarta.json`으로 전환되었습니다. [JSON 사양(RFC 8259)](https://datatracker.ietf.org/doc/html/rfc8259)에서 댓글에 대한 구문을 정의하지는 않지만 이전 AEM 릴리스에서는 `javax.json` 제공자 이 문제에 대해 엄격하지 않아 이를 허용했습니다. `jakarta.json` 제공자가 이 확장 기능을 제공하지 않습니다.

알림 없이 오류 발생: 설치 관리자에 오류가 표시되지 않고 번들 활성화 시 콘텐츠 노드 로드에 실패합니다. SP2로 업그레이드한 후 예기치 않게 콘텐츠가 누락된 경우 OSGi 설치 관리자 로그에서 JSON 구문 분석 오류를 확인하십시오. 영향을 받는 번들을 식별하려면 `Sling-Initial-Content` 매니페스트 헤더 아래에 나열된 JSON 파일 내에서 `//` 또는 `/* */`를 찾습니다.

>[!CAUTION]
>
> AEM 6.5 LTS SP2로 업그레이드한 후의 콘텐츠 로드 실패를 방지하려면 `Sling-Initial-Content` 번들에서 JSON 파일의 모든 댓글을 제거하십시오.

### Sites Headless API에 필요한 Oak 인덱스 설치{#site-headless-api}

Sites Headless로 이동한 일부 API의 경우 전체 기능을 위해 추가 Oak 인덱스가 필요합니다.

다음 기능을 사용하려면 `cq-dam-cfm-indices` 패키지를 설치하십시오.

* 콘텐츠 조각 모델 목록
* 콘텐츠 조각 목록
* API 검색
* 워크플로

Adobe 소프트웨어 배포 포털에서 인덱스 패키지 [cq-dam-cfm-indexes](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-dam-cfm-indices-1.1.2.zip)를 다운로드합니다.

### SSL 전용 기능을 사용한 Dispatcher 연결 실패(AEM 6.5 LTS SP1 이상에서 수정됨){#ssl-only-feature}

>[!NOTE]
>
> 이 문제는 AEM 6.5 LTS GA 릴리스에서만 발생합니다.

AEM 배포에서 SSL 전용 기능을 활성화하면 Dispatcher와 AEM 인스턴스 간의 연결에 영향을 미치는 알려진 문제가 있습니다. 이 기능을 활성화한 후에는 상태 검사가 실패할 수 있으며 Dispatcher와 AEM 인스턴스 간의 통신이 중단될 수 있습니다. 이 문제는 고객이 Dispatcher에서 AEM 인스턴스로 `https + IP`를 통해 연결을 시도할 때 발생합니다. 이는 SNI(서버 이름 표시) 유효성 검사 문제와 관련이 있습니다.

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

이 문제가 발생하면 Adobe 고객 지원 센터에 문의하십시오. 이 문제를 해결하기 위해 핫픽스 [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip)이 제공됩니다. 필요한 핫픽스를 적용하기 전에는 SSL 전용 기능을 활성화하지 마십시오.

## OSGi 번들 및 콘텐츠 패키지 포함됨{#osgi-bundles-and-content-packages-included}

다음 zip 파일에는 이 Experience Manager 6.5 LTS 서비스 팩 릴리스에 포함된 OSGi 번들 및 콘텐츠 패키지를 나열하는 텍스트 문서가 포함되어 있습니다.

* [OSGi 번들](/help/release-notes/assets/65lts_sp2_bundles.zip)
* [컨텐츠 패키지](/help/release-notes/assets/65lts_sp2_packages.zip)

## 제한된 웹 사이트{#restricted-sites}

이들 웹 사이트는 고객만 사용할 수 있습니다. 고객이시며 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 센터](https://experienceleague.adobe.com/ko/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience)에 문의하십시오.

