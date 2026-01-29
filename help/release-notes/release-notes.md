---
title: Adobe Experience Manager 6.5 LTS의 최신 릴리스 정보, SP1
description: Adobe Experience Manager 6.5 LTS, 서비스 팩 1에 대한 최신 릴리스 정보를 찾아보십시오.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 6a6a79663579e4d63e68ae6c9a4bec97f24032f9
workflow-type: tm+mt
source-wordcount: '7745'
ht-degree: 93%

---

# Adobe Experience Manager 6.5 LTS의 최신 릴리스 정보, SP1 {#release-notes}

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| 버전 | 서비스 팩 1(SP1), GRANITE-61551에 대한 핫픽스 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2025년 9월 9일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq660%2Fhotfixes%2Fcq-6.5.lts.1-hotfix-GRANITE-61551-1.2.zip) |

<!-- OLD URL TO JAR
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.1.jar) | -->


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

## [!DNL Adobe Experience Manager] 6.5 LTS, SP1 포함 사항 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS, SP1에는 새로운 기능, 고객 요청을 반영한 주요 개선 사항 및 버그 수정이 포함되어 있습니다. 여기에는 2025년 3월 6.5 LTS가 처음 출시된 이후 적용된 성능, 안정성, 보안 개선 사항도 포함됩니다. 6.5 LTS에 [이 서비스 팩을 설치](#install-update)하십시오.

## 주요 기능 및 개선 사항

### 양식

이제 JEE의 AEM 6.5 Forms LTS를 사용할 수 있습니다. 지원되는 환경에 대한 자세한 내용은 [지원되는 플랫폼](/help/forms/using/aem-forms-jee-supported-platforms.md) 조합 문서를 참조하십시오. 설치 관리자 링크는 [AEM Forms 릴리스](https://experienceleague.adobe.com/ko/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) 페이지에서 사용할 수 있습니다.

#### AEM Forms 6.5 LTS SP1에 포함된 제품

**Java 지원 업데이트**

최신 Java 버전에 대한 지원이 도입되었습니다.

* Java™ 17
* Java™ 21

**응용 프로그램 서버 지원 업데이트**

* JBoss EAP 8에 대한 지원이 추가되었습니다.
* 기존 PicketBox 보안 프레임워크가 제거되었습니다.
* 이제 보안 자격 증명 관리를 위해 Elytron 기반 자격 증명 저장소가 지원됩니다.

**구성: 자격 증명 저장소(Elytron 기반)**

JBoss EAP 8의 AEM Forms은 보안 자격 증명을 관리하는 데 Elytron을 사용합니다. 고객은 서버를 성공적으로 시작하고 데이터베이스 인증을 보호하려면 Elytron 기반 Credential Store를 구성해야 합니다.

구성에 대한 자세한 내용은 설치 및 구성 안내서를 참조하십시오.

**플랫폼 및 호환성 변경**

* 서블릿 사양 5+ 지원
* Jakarta EE 9 규정 준수

**네임스페이스 마이그레이션 요구 사항**

* Jakarta EE 9에서는 `javax.*`에서 `jakarta.*`(으)로 네임스페이스가 변경되었습니다.
* 모든 **사용자 지정 DSC**&#x200B;을 `jakarta.*` 네임스페이스로 마이그레이션해야 합니다.
* AEM Forms 6.5 LTS SP1은(는) **Jakarta EE 9+ 기반 응용 프로그램 서버만 지원합니다**

자세한 내용은 **javax에서 jakarta 네임스페이스로 마이그레이션**&#x200B;을 참조하십시오.

#### `javax`에서 `jakarta` 네임스페이스로 마이그레이션

**AEM Forms 6.5 LTS SP1**&#x200B;부터 **Jakarta Servlet API 5/6**&#x200B;을 구현하는 응용 프로그램 서버만 지원됩니다. **Jakarta EE 9 이상**&#x200B;에서 모든 API가 `javax.{}` 네임스페이스에서 `jakarta.`(으)로 전환되었습니다.

따라서 **모든 사용자 지정 DSC는 `jakarta` 네임스페이스를 사용해야 합니다**. `javax.{}` API를 사용하여 빌드된 사용자 지정 구성 요소는 지원되는 응용 프로그램 서버와 **호환되지 않습니다**.

**사용자 지정 DSC에 대한 마이그레이션 옵션**

다음 방법 중 하나를 사용하여 기존 사용자 지정 DSC를 마이그레이션할 수 있습니다.

**옵션 1: Source 코드 마이그레이션(권장)**

* `javax.{}`에서 `jakarta.`(으)로 모든 가져오기 문 업데이트
* 사용자 지정 DSC 프로젝트 다시 빌드 및 다시 컴파일
* 업데이트된 구성 요소를 애플리케이션 서버에 재배포

**이점:**

* Jakarta EE 9+와의 장기적인 호환성 보장
* 활발하게 유지 관리되는 프로젝트에 가장 적합

**옵션 2: Eclipse 변환기를 사용한 이진 마이그레이션**

* **Eclipse 변환기** 도구를 사용하여 컴파일된 이진 파일(`.jar`, `.war`)을 `javax`에서 `jakarta`(으)로 변환합니다
* 소스 코드를 변경하거나 다시 컴파일할 필요가 없습니다.
* 변환된 바이너리를 애플리케이션 서버에 다시 배포

>[!NOTE]
>
> 이진 변환은 **바이트코드 수준**&#x200B;에서 수행됩니다.

다음은 마이그레이션 중에 필요한 네임스페이스 변경 사항에 대한 일반적인 예입니다.

* 이전(javax)    이후(자카르타)
* javax.servlet. **jakarta.servlet**
* javax.servlet.http. **jakarta.servlet.http.**

**샘플 가져오기 매핑**

다음 표에서는 `javax`에서 `jakarta`(으)로 마이그레이션할 때 필요한 일반적인 네임스페이스 변경 사항을 보여 줍니다.

| 다음 이전(`javax`) | 다음 이후(`jakarta`) |
| ---------------------- | ------------------------ |
| `javax.servlet.*` | `jakarta.servlet.*` |
| `javax.servlet.http.*` | `jakarta.servlet.http.*` |

사용자 지정 DSC 소스 코드를 업데이트하거나 변환된 바이너리를 확인할 때 이러한 매핑을 참조로 사용합니다.

<!-- 6.5 LTS REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE EACH RELEASE -->

## 6.5 LTS, 서비스 팩 1에서 해결된 문제 {#fixed-issues}

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-65-LTS-SP1}

#### 접근성 {#sites-accessibility-65-lts-sp1}

* 콘텐츠 조각의 텍스트 편집기 요소가 기본적으로 잘리는 문제를 해결했습니다. 이제 텍스트 편집기에서 잘림 없이 전체 내용이 표시됩니다. (SITES-33005)
* URL 경로를 클릭하면 올바른 대상 URL 대신 Indigo의 홈 페이지가 열리는 문제를 해결했습니다. (SITES-33004)
* 자동 테스트 중 ADA 규정 준수 실패를 유발하는 사용자 정의 AEM 구성 요소의 접근성 문제를 해결했습니다. (SITES-30660)
* 밝은 배경에서 텍스트가 검은색으로 표시되고 WCAG 2.0 대비 요구 사항을 충족하도록 하여 알림 대화 상자와 워크플로 메시지상의 ADA 규정 준수 문제를 해결했습니다. (SITES-30138)
* AEM Sites 편집기의 &#39;카테고리&#39; 버튼에 특정 레이블이 없어서 JAWS에서 설명 레이블을 제공하는 대신 &#39;이미지 버튼 메뉴&#39;로 알리는 접근성 문제를 해결했습니다. (SITES-27497)
* 유효 권한 화면의 체크 표시 아이콘에 대체 텍스트가 없어 JAWS에서 해당 의미를 읽고 전달하지 못하는 접근성 문제를 해결했습니다. (SITES-27272)
* 사용자 또는 그룹 권한을 제거할 때 JAWS에서 명확한 안내를 제공하지 않아 화면 판독기 사용자에게 혼란을 야기하는 접근성 문제를 해결했습니다. (SITES-27238)
* 오류 메시지가 설명 텍스트 없이 아이콘으로만 표시되어 JAWS에서 오류 발생 시 이를 알리지 못하는 접근성 문제를 해결했습니다. (SITES-27155)
* 모듈 섹션의 제목 수준 2 텍스트 누락을 비롯하여 JAWS가 AEM 온프레미스 환경에서 잘못되고 불분명한 버튼 설명을 읽는 접근성 문제를 해결했습니다. (SITES-27152)
* AEM Assets 탭에서 값을 필터링한 후 JAWS가 결과 수를 알리지 않는 접근성 문제를 해결했습니다. (SITES-27150)
* 폴더를 만들 때 확인 메시지가 표시되지 않고 JAWS가 자산 UI에서 이를 알리지 않는 접근성 문제를 해결했습니다. (SITES-27141)
* AEM Sites의 접근성 문제를 해결했습니다. JAWS는 양식 오류를 알리지 않았고, 포커스는 비대화형 오류 요소로 이동했으며, 필수 필드 오류는 탭 아웃 시 표시되지 않았습니다. (SITES-27138)
* 타임라인 버튼 메뉴에 특정 레이블이 없어서 JAWS에서 명확한 설명 없이 &#39;활동 버튼 메뉴&#39;만 읽어 오는 접근성 문제를 해결했습니다. (SITES-27134)
* JAWS가 컨테이너 항목에 대한 작업이나 역할을 알리지 않으며 설명 레이블 대신 &#39;이동 경로 v1&#39; 및 &#39;버튼 v2&#39;만 읽는 접근성 문제를 해결했습니다. (SITES-27131)
* 빠른 게시 팝업에서 적절한 성공 메시지가 제공되지 않아 화면 판독기가 완료 피드백을 알리지 못하는 접근성 문제를 해결했습니다. (SITES-26912)
* ARIA 역할이 있고 하위 역할이 필요한 요소가 해당 역할을 포함하지 않아 접근성 표준을 준수하지 않는 coral-column 보기의 접근성 문제를 해결했습니다. (SITES-26898)
* 생성 페이지의 상단 탐색에 있는 &#39;템플릿&#39; 및 &#39;속성&#39; 텍스트가 리플로우 모드에서 보이지 않아 키보드 및 화면 판독기 사용자가 액세스할 수 없는 접근성 문제가 해결되었습니다. (SITES-26895)
* 상단 탐색의 &#39;검색&#39;, &#39;솔루션&#39;, &#39;도움말&#39;, &#39;받은 편지함&#39; 및 &#39;사용자&#39; 아이콘에 대한 툴팁에 키보드 탐색을 사용하여 접근할 수 없었던 접근성 문제를 해결했습니다. (SITES-26889)
* 필수 입력 필드가 비어 있을 경우 기본 탭 양식 필드에서 오류 제안 사항이 제공되지 않아 사용자가 안내를 받을 수 없었던 접근성 문제가 해결되었습니다. (SITES-26885)
* NVDA 및 내레이터 화면 판독기가 만들기 페이지에서 템플릿 파일 세부 정보를 안내하지 않아 사용자가 프로그래밍 방식으로 전체 정보를 받지 못하는 접근성 문제가 해결되었습니다. (SITES-26884)
* 기본 탭의 &#39;페이지 제목 텍스트 상자&#39;에 잘못된 이름을 사용하여 화면 판독기가 사용자에게 정확한 정보를 제공하지 못하는 접근성 문제를 해결했습니다. (SITES-26879)
* WCAG 2.2 AA 최소 대비율 요구 사항을 충족하도록 버튼 전경색 및 배경색을 업데이트하여 모든 사용자의 가독성과 접근성을 개선했습니다. (SITES-26877)
* 시력이 약한 사용자의 가시성과 접근성을 보장하기 위해 생성 페이지의 상단 탐색에 있는 &#39;템플릿&#39; 및 &#39;속성&#39; 텍스트가 크기 조정 후 사라지는 문제를 해결했습니다. (SITES-26872)
* 리플로우를 적용한 후 메인 페이지에 여러 개의 수평 스크롤 막대가 나타나는 문제를 해결하여 단일 스크롤 막대가 표시되도록 함으로써 적절한 접근성 및 콘텐츠 가시성을 확보했습니다. (SITES-26800)
* AEM 페이지 편집기에서 페르소나, 장바구니, 포기 등의 버튼을 활성화한 후 키보드 포커스가 예기치 않게 인구 통계 도구 모음의 시작 부분으로 재설정되는 접근성 문제를 해결했습니다. 일관된 키보드 탐색과 화면 판독기 워크플로를 지원하기 위해 이제 활성화된 버튼에 포커스가 유지됩니다. (SITES-25306)
* 페이지 제목 및 태그 필드에 대한 접근성 레이블 연결 문제를 해결했습니다. 이제 AEM 인터페이스는 JAWS와 같은 화면 판독기를 사용할 때 접근성 레이블을 &#39;제목&#39; 및 &#39;페이지 제목&#39; 필드에 올바르게 연결합니다. 이 수정 사항을 통해 적절한 레이블 판독이 보장되고 페이지 생성, 속성 및 이동 워크플로 전반에서 ADA 규정 준수가 개선됩니다. (SITES-27149)
* 타임라인의 댓글 입력 필드에 시각적 레이블이 누락된 문제를 해결했습니다. 접근성을 개선하기 위해 타임라인 섹션의 &#39;댓글&#39; 입력 필드에 시각적 레이블이 누락된 문제를 수정했습니다. 이 업데이트 덕분에 화면 판독기가 필드 레이블을 정확하게 읽을 수 있습니다. 이러한 경험은 특히 보조 기술에 의존하는 개인을 비롯하여 모든 사용자에 대한 양식 탐색 및 제출 기능을 향상합니다. (SITES-26903)
* 타임라인 댓글의 줄임표 버튼에 대한 키보드 접근성을 개선했습니다. 타임라인 섹션의 댓글 옆에 있는 줄임표(점 세 개) 버튼에 대한 키보드 탐색을 활성화했습니다. 이제 사용자는 탭 키를 사용하여 버튼에 접근하고 상호 작용할 수 있기 때문에 키보드만으로 탐색하던 기존 대비 사용자의 접근성이 향상되었습니다. (SITES-26891)
* 선택 대화 상자에서 검색 결과에 대한 NVDA/내레이터 안내를 개선했습니다. NVDA 또는 내레이터와 같은 화면 판독기를 사용할 때 검색 결과가 있는지 여부를 알려 주는 선택 항목 열기 대화 상자를 업데이트했습니다. 이러한 개선 사항은 보조 기술을 사용하는 사용자가 시각적 확인 없이도 검색 작업의 결과를 이해하는 데 도움이 됩니다. (SITES-26883)
* 댓글 입력 필드 옆에 있는 줄임표 아이콘에 대한 ARIA 역할을 수정했습니다. 화면 판독기의 정확한 요소 판별을 지원하기 위해 댓글 입력 필드 옆에 있는 줄임표(점 세 개) 아이콘을 올바른 ARIA 역할을 사용하도록 업데이트했습니다. 이러한 개선을 통해 접근성 규정 준수가 강화되고 보조 기술을 사용하는 사용자의 경험이 향상됩니다. (SITES-26881)
* Coral UI 구성 요소의 잘못된 ARIA 속성을 수정했습니다. 모든 ARIA 속성이 유효한 값을 사용하도록 Coral UI 구성 요소를 업데이트하여 접근성 규정 준수를 향상했습니다. 특히, `aria-modal="dialog"`와 같이 잘못된 값이 잘못 할당되는 문제가 해결되었습니다. 이 개선 사항은 화면 판독기가 대화 상자 요소를 올바르게 해석하도록 지원하여 보조 기술을 사용하는 사용자의 접근성을 향상합니다. (SITES-26873)
* 리플로우 시나리오에서 아이콘의 가시성과 툴팁을 개선했습니다. **다운로드**, **자산 재처리** 및 **체크아웃** 아이콘에 대한 툴팁이 올바르게 표시되도록 리플로우 동작을 향상했습니다. 뷰포트 크기가 조정되거나 브라우저 확대/축소 설정이 변경되면 아이콘과 레이블이 보이지 않는 접근성 문제에 중점을 두었습니다. 이 수정 사항은 리플로우 중에 가시성을 유지하고 적절한 아이콘 설명을 제공함으로써 시력이 약한 사용자를 지원합니다. (SITES-26871)


#### 관리자 사용자 인터페이스{#sites-adminui-65-lts-sp1}

* JAWS가 사이트 생성 대화 상자에서 목록 역할을 알리지 않거나 탐색 및 활성화 지침을 제공하지 않는 접근성 문제를 해결했습니다. (SITES-30661)
* 사이트 필터 보기에서 상태 메시지에 대한 화면 판독기 지원이 예상대로 작동하여 사용자가 보기 간에 전환할 때 명확하고 시기적절한 피드백을 받을 수 있습니다. (SITES-24992)
* 필터 레일의 날짜 선택기가 컨테이너 내에 완전히 표시되어 적절한 터치 대상 크기를 제공하고 클리핑 문제를 제거합니다. (SITES-24988)
* 선택된 필터 태그는 이제 시각적 표현과 일치하는 의미론적 HTML과 aria-labels를 사용하여 보조 기술에 대한 정확한 역할 지원과 명확한 작업을 보장합니다. (SITES-24980)
* 화면 판독기 사용자에게 고유하고 설명적인 레이블을 제공하고 페이지 전체에서 일관된 랜드마크 식별을 보장하기 위해 참조 레일 영역에 aria-label 속성을 추가했습니다. (SITES-24973)
* 참조 레일을 업데이트하여 크기 조정 및 위치 지정에 상대적 단위를 사용함으로써 1280x1024 뷰포트에서 400% 확대/축소 시에도 콘텐츠의 크기를 조절하고 모든 기능을 유지할 수 있게 되었습니다. (SITES-24972)
* 사이트 홈 페이지 목록 보기의 테이블 요소에 적절한 열 머리글 역할이 포함되어 있어 화면 판독기가 각 데이터 셀의 머리글을 알릴 수 있도록 했습니다. (SITES-24942)
* NVDA가 이제 트리 디렉터리에 수정 날짜를 알려 화면 판독기 사용자가 완전한 자산 세부 정보를 받을 수 있도록 했습니다. (SITES-24782)
* AEM Sites의 트리 디렉터리 구성 요소에 있는 항목에 대해 NVDA 화면 판독기가 불완전한 텍스트를 알리는 문제를 해결했습니다. NVDA가 이제 각 항목의 전체 텍스트를 읽어 접근성과 규정 준수를 개선합니다. (SITES-24780)
* 트리 디렉터리 내 Window Splitter의 키보드 접근성을 향상하여 사용자가 키보드만 사용하여 왼쪽 사이드바의 크기를 조정할 수 있도록 했습니다. (SITES-24779)
* 목록 항목에 대한 올바른 ARIA 역할을 포함하도록 도움말 메뉴 검색 결과를 업데이트하여 화면 판독기가 링크를 적절하게 알리도록 함으로써 접근성을 개선했습니다. (SITES-24729)
* 화면 판독기가 &#39;결과 Y개 중 X개&#39; 상태 메시지를 알리지 않는 문제를 해결했습니다. 또는 사이트 필터 패널에서 필터를 적용한 후 &#39;검색 결과가 없습니다&#39;라는 메시지를 표시하여 사용자가 결과에 대한 적절한 확인을 받을 수 있도록 했습니다. (SITES-24720)
* 앱 탐색에서 탐색 링크에 대한 역할 할당이 누락된 문제를 수정했습니다. 화면 판독기가 탐색 요소를 올바르게 식별하고 알릴 수 있도록 적절한 ARIA 역할을 추가했습니다. (SITES-24719)
* 선택한 필터 태그에 대한 잘못된 그리드 역할 마크업을 버튼 요소로 바꾸고, 액세스 가능한 이름을 추가하여 화면 판독기가 태그를 올바르게 알리고 식별할 수 있도록 했습니다. (SITES-24717)
* 여러 항목을 선택할 때 참조 레일 상태 메시지에 대한 화면 판독기 안내를 추가하여 사용자가 변경 사항에 대한 확인을 받을 수 있도록 했습니다. (SITES-24678)
* 첫 번째 결과가 자동으로 발표되지 않도록 검색 필드 동작을 수정했습니다. 이제 화면 판독기가 찾은 결과의 개수를 안내하므로 사용자가 잘못된 포커스 알림 없이 목록을 탐색할 수 있습니다. (SITES-24658)
* 화면 판독기가 오해의 소지가 있거나 관련성 없는 정보를 알리는 것을 방지하기 위해 목록 보기 내 비대화형 정적 요소에서 잘못된 `aria-label` 속성을 제거했습니다. (SITES-24515)
* 목록 보기의 첫 번째 열에 있는 확인란을 업데이트하여 액세스 가능한 이름으로 제목 열 텍스트를 사용하도록 했습니다. 이를 통해 화면 판독기가 양식 필드의 목적을 정확하게 전달할 수 있습니다. (SITES-24514)
* 콘텐츠를 탐색할 때 화면 판독기 사용자에게 로딩 상태 메시지를 알리기 위해 적절한 ARIA 속성과 라이브 지역 지원이 추가되었습니다. (SITES-24481)
* 뷰포트 폭이 1280×1024인 상태에서 콘텐츠를 400%로 확대할 때 수평 스크롤을 없애기 위해 반응형 디자인을 업데이트하여 측면 스크롤 없이도 전체 가시성을 제공합니다. (SITES-24308)
* 사이트 관리자 UI에서 올바른 포커스 탐색을 통해 논리적 순서를 따르도록 수정했습니다. 따라서 Esc 키를 누르면 포커스가 &#39;모두 선택&#39; 버튼으로 돌아가고, Tab 키를 누르면 포커스가 다음 대화형 요소로 이동합니다. (SITES-24307)
* 사이트 관리자 UI에서 포커스 순서를 업데이트하여 키보드 탐색 중에 `<betty-titlebar-title>` 요소의 이동 경로 버튼이 올바른 순서로 포커스를 받도록 했습니다. (SITES-24305)
* 키보드 포커스를 주요 콘텐츠 영역으로 이동하여 키보드 사용자가 머릿글 요소를 우회하고 효율적으로 콘텐츠에 액세스할 수 있도록 검증된 건너뛰기 링크 기능을 제공합니다. (SITES-24061)


#### 클래식 사용자 인터페이스{#sites-classicui-65-lts-sp1}

날짜 검색 및 비표준 인터페이스를 포함한 여러 UI 요소에서 체크박스 레이블이 누락되고 HTML이 인코딩된 텍스트로 표시되는 클래식 UI 문제를 해결했습니다. (SITES-31822)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp1}

이제 AEM이 이미지 자산의 잘못된 XMP 메타데이터로 인해 발생하는 성능 저하를 방지합니다. 숫자 세그먼트나 정규화되지 않은 구조 등 유효하지 않거나 규정을 준수하지 않는 XMP 속성 이름이 포함된 자산은 처리 중에 더 이상 반복적인 경고 로그를 트리거하지 않습니다. 이 시스템은 문제가 있는 메타데이터를 필터링하여 자산 수집 및 검증이 오류 없이 완료되도록 보장합니다. (SITES-30683)

<!--
#### [!DNL Content Fragments] - Admin{#sites-admin-65-lts-sp1} -->

#### [!DNL Content Fragments] - 조각 편집기{#sites-fragments-editor-65-lts-sp1}

작성자가 콘텐츠 조각을 체크아웃한 경우에도 다른 작성자가 여전히 콘텐츠 조각을 게시할 수 있다면 체크아웃 기능의 의도된 동작에 반하게 됩니다. 이번 수정 사항은 콘텐츠 조각이 체크아웃될 때 다른 사용자가 작성 인터페이스에서 게시 버튼을 보거나 사용할 수 없도록 합니다. (SITES-30578)

<!--
#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp1}

#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp1}

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp1} -->

#### 구성 요소 콘솔{#sites-component-console-65-lts-sp1}

제품 목록 구성 요소에서 &#39;모두 선택&#39; 체크박스를 사용하면 검색 결과에 모든 SKU가 추가되는 대신, 초기 페이지의 처음 20개 SKU만 추가되는 문제를 해결했습니다. (SITES-29191)

#### 핵심 백엔드{#sites-core-backend-65-lts-sp1}

XMP 메타데이터가 잘못 포맷되어 `ValidationDataServlet`에서 이미지 자산을 처리하는 동안 오류가 발생하는 문제가 있었습니다. 이번 수정 사항은 규정을 준수하는 메타데이터의 처리를 보장하고 잘못된 속성의 중복 구문 분석을 방지합니다. (SITE-30683)

<!--
#### Core Components{#sites-core-components-65-lts-sp1}

#### Campaign integration{#sites-campaign-integration-65-lts-sp1}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp1}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp1}

#### Launches{#sites-launches-65-lts-sp1}

#### Link Checker{#sites-link-checker-65-lts-sp1} -->

#### MSM - Live Copy{#sites-msm-live-copies-65-lts-sp1}

* AEM 6.5 온프레미스에서 고스트 구성 요소 상속을 다시 활성화할 때 발생하는 JavaScript 오류 `ns.ui.alert is not a function`를 수정했습니다. (SITES-31993)
* AEM 6.5에서 “나중에” 롤아웃 옵션을 사용하면 날짜를 선택하지 않고도 계속 진행할 수 있는 문제가 해결되었습니다. (SITES-31374)

#### 페이지 편집기{#sites-pageeditor-65-lts-sp1}

* 티저 모달에서 유효한 데이터 입력 및 오류 해결 후에도 링크 및 작업 탭에 오류 스타일, 아이콘 및 aria-invalid 속성이 계속 표시되는 문제가 해결되었습니다. (SITES-25527)
* 정확한 aria 확장 속성 업데이트를 보장하기 위해 티저 모달 텍스트 편집기에서 목록 및 문단 버튼이 확장 또는 축소된 상태를 화면 판독기에 전달하지 않는 문제를 해결했습니다. (SITES-25365)
* 인구 통계 도구 모음에서 키보드 입력으로 장바구니 슬라이더를 조정하면 슬라이더에 포커스가 유지되지 않고 장바구니 버튼으로 포커스가 이동하는 문제를 해결하여 키보드 사용자의 탐색 효율성을 향상했습니다. (SITES-25324)
* 인구 통계 도구 모음의 장바구니 슬라이더에 액세스 가능한 이름을 추가하려면 연관된 `<label>` 요소에 값을 할당해야 하는 문제가 있었습니다. 이번 수정 사항은 보조 기술과의 호환성을 개선하고 화면 판독기 사용자의 사용성을 향상했습니다. (SITES-25322)
* 인구 통계 도구 모음 드롭다운 내부의 버튼에 ARIA 역할과 액세스 가능한 이름을 추가했습니다. 이번 수정 사항은 보조 기술을 통한 적절한 식별을 지원하고 키보드와 화면 판독기 사용자의 탐색 기능을 향상했습니다. (SITES-25315)
* 브라우저 확대/축소율이 200%일 때 뷰포트 이상으로 콘텐츠가 표시되지 않도록 인구 통계 도구 모음 레이아웃을 조정하여 수평 스크롤 없이도 모든 제어에 접근할 수 있도록 했습니다. (SITES-25309)
* 인구 통계 도구 모음의 포커스 관리를 수정하여 포커스를 도구 모음의 시작 위치로 재설정하는 것이 아니라 활성화된 버튼에 키보드 포커스를 유지하도록 했습니다. (SITES-25306)
* 버튼 레이블 중첩 기능은 화면 폭이 유사한 모드가 활성화되면 툴팁을 사용하여 레이블을 표시하도록 설계된 대로 작동합니다. (SITES-25285)
* 주석 모달에 눈에 보이는 제출 버튼이 포함하여 사용자가 Esc 키를 누르거나 모달 외부를 클릭하지 않고도 주석을 제출할 수 있습니다. (SITES-25281)
* 주석 모달에 사용자가 주석을 제출할 수 있는 펜 아이콘 버튼을 포함하여 명확하고 접근하기 쉬운 제출 방법을 제공합니다. (SITES-25269)
* 관련성이 없거나 혼란스러운 정보를 제거하고 정확하고 관련성 있는 피드백을 제공하기 위해 주석 및 주석 닫기 버튼에 대한 화면 판독기 안내를 수정했습니다. (SITES-25268)
* AEM 편집기 페이지의 캔버스 섹션에서 이제 전체 키보드 접근성이 지원됩니다. 사용자는 마우스 호버에 의존하지 않고 키보드만 사용하여 섹션 제목과 편집 버튼을 활성화할 수 있습니다. 이 업데이트는 WCAG 2.1.1을 준수하고 티저, 이미지, 슬라이드, 레이아웃, 타임워프, 주석 모달 등 구성 요소 전반의 사용성을 개선합니다. (SITES-25256)
* 모든 콘텐츠가 좌우 탐색 없이 뷰포트 내에 표시되도록 하기 위해 폭이 320px인 슬라이드 모달에서 불필요한 수평 스크롤을 제거했습니다. (SITES-25254)
* 모든 콘텐츠가 좌우 탐색 없이 뷰포트 내에 표시되도록 하기 위해 폭이 320px인 이미지 모달에서 불필요한 수평 스크롤을 제거했습니다. (SITES-25244)
* 모든 콘텐츠가 좌우 탐색 없이 뷰포트 내에 표시되도록 하기 위해 폭이 320px인 티저 모달에서 불필요한 수평 스크롤을 제거했습니다. (SITES-25242)
* 티저 모달의 `List` 및 `Paragraph Format` 팝업 메뉴 모두에서 키보드 탐색을 활성화했습니다. 이 수정 사항은 사용자가 화살표 키를 사용하여 해당 메뉴에 접근하고 탐색할 수 있도록 지원합니다. (SITES-25235)
* 연관된 작업에 맞춰 정확하고 관련성 있는 피드백을 제공하기 위해 주석 및 주석 닫기 버튼에 대한 화면 판독기 안내를 수정했습니다. (SITES-25234)
* 모든 사용자, 특히 보조 기술 사용자에게 도움말 버튼의 목적을 명확하게 설명하고 의미 있는 컨텍스트를 제공하기 위해 티저 모달의 도움말 버튼 레이블을 개선했습니다. (SITES-25224)
* 각 디바이스에 눈금자 측정값을 연결하여 화면 판독기 사용자를 위한 에뮬레이터 눈금자를 개선했습니다. 또한 툴팁을 aria-describedby 요소로 대체했습니다. (SITES-24955)
* 편집 버튼은 의도한 대로 작동하며, 작업을 수행하는 것이 아니라 정보 관련 컨텍스트를 제공하기 때문에 수정 사항이 구현되지 않았습니다. (SITES-24950)
* 사용자가 예기치 않게 건너뛰거나 되돌아가는 일 없이 모든 대화형 요소를 탐색할 수 있도록 편집기 페이지에서 포커스 순서가 논리적 순서를 따르게 했습니다. (SITES-24937)
* 사용자가 사용자 정의 텍스트 간격 설정을 적용하면 미리보기 모드 캔버스가 텍스트 간격을 올바르게 업데이트하도록 하여 모든 콘텐츠 영역에서 일관된 서식을 보장합니다. (SITES-24936)
* 검증된 미리보기 버튼은 더 이상 포커스의 컨텍스트나 상태 변경을 트리거하지 않으므로, 페이지 보기가 업데이트되기 전에 사용자가 의도적으로 버튼을 활성화할 수 있습니다. (SITES-24784)
* 앱 탐색 링크에 올바른 ARIA 역할 할당을 추가하여 화면 판독기가 탐색 항목을 정확하게 식별하고 알리도록 함으로써 접근성을 개선했습니다. (SITES-24718)
* 확장 및 축소된 상태를 화면 판독기에 알리기 위해 필터 변경 버튼을 업데이트하고, 중복된 ARIA 속성을 제거하고, 명확하고 중복되지 않는 설명을 제공하기 위해 레이블을 조정했습니다. (SITES-24713)
* 결과가 로드되거나 일치하는 항목이 없는 경우 사용자에게 확인을 제공하도록 보장하기 위해 링크 선택 대화 상자에서 검색 결과 상태 메시지에 대한 화면 판독기 알림을 추가했습니다. (SITES-24700)
* 모달이 로드되고 상호 작용할 준비가 되면 사용자가 피드백을 받을 수 있도록 이미지 모달의 로딩 상태에 대한 화면 판독기 안내를 추가했습니다. (SITES-24697)
* 200% 및 400% 확대 시 스티키 머리말이 티저 모달 콘텐츠를 가리는 접근성 문제를 해결하여 페이지 확대 기능을 사용할 때 완벽한 가시성과 사용성을 확보했습니다. (SITES-24523)
* 검색/필터 필드에 검색 결과의 개수를 알려 주는 상태 메시지를 추가하여 화면 판독기가 사용자에게 결과를 알릴 수 있도록 했습니다. (SITES-24506)
* 검색/필터 필드에 검색 결과 수에 대한 화면 판독기 안내를 추가하여 결과가 로드될 때 사용자가 즉각적인 피드백을 받을 수 있도록 했습니다. (SITES-24505)
* 화면 판독기가 WAI-ARIA 가이드라인을 준수하여 해당 목적을 알릴 수 있도록 사이드 레일 패널의 탭 목록에 액세스 가능한 이름을 추가했습니다. (SITES-24492)
* 모호한 편집기 아이콘에 설명 레이블을 추가하여 모든 사용자가 각 버튼의 기능을 명확하게 이해할 수 있도록 했습니다. (SITES-24480)
* 캔버스 보기에서 섹션 제목과 작업 버튼에 대한 전체 키보드 접근성을 활성화하여 마우스와 키보드 사용자가 일관된 작업을 수행할 수 있도록 했습니다. (SITES-24479)

<!--
#### Replication{#sites-replication-65-lts-sp1}

#### Rich Text Editor{#sites-rte-65-lts-sp1} -->

#### 범용 편집기 {#sites-universal-editor-65-lts-sp1}

* 로그인 토큰 서비스가 결과를 반환하기 전에 쿼리 매개변수가 있는 여러 요청이 트리거되는 경우 잘못된 로그인을 유발하는 QueryTokenService의 경합 조건을 수정했습니다. (SITES-30659)
* Felix ConfigMgr에서 매핑된 경로 배열을 저장하면 첫 번째 항목만 유지되는 UniversalEditorURLService의 문제를 해결했습니다. (SITES-30292)

### [!DNL Assets]{#assets-65-lts-sp1}

원격 DAM에서 Sites 로컬 AEM으로 자산을 동기화할 때 자산에서 게시된 상태 및 복제 관련 속성이 제거되는 문제를 해결했습니다. (Assets-48958)

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

HTL 스크립트 엔진 팩토리의 기능을 차단하는 OSGi 종속성 주기를 해결하여 적절한 서비스 확인 및 스크립트 실행을 보장했습니다. (Granite-58275)

#### 통합{#foundation-integrations-65-lts-sp1}

* `com.adobe.cq.cq-analytics-integration` 번들에서 commons-httpclient 3.x 사용을 제거하고 최신 AEM 6.5 LTS 표준에 맞추기 위해 `org.apache.httpcomponents.httpclient` 4.5.13.B0001로 대체했습니다. (CQ-4360586)
* 사용되지 않는 구성 요소를 제거하고 유지 관리 오버헤드를 줄이기 위해 AEM에서 더 이상 사용되지 않는 Search&amp;Promote 통합 번들을 제거했습니다. (CQ-4358030)
* 분석 유효성 검사를 개선하고 보다 포괄적인 적용 범위를 보장하기 위해 SiteCatalyst 통합에 대한 새로운 백엔드 테스트 사례를 추가했습니다. (CQ-4359991)
* Launch Config의 속성 섹션에서 회사 및 속성 드롭다운이 나타나지 않는 문제를 해결했습니다. 또한 모든 필수 필드가 채워졌음에도 불구하고 저장 및 닫기에서 발생하는 오류와 제목 필드만 비어 있을 때 회사 및 부동산에 대한 잘못된 오류 메시지가 표시되는 문제를 해결했습니다. (CQ-4359853)
* Search&amp;Promote 번들 제거에 맞춰 버전 6.6에서 `searchpromote` 서블릿 경로 항목을 제거했습니다. (CQ-4359523)
* 정확한 유효성 검사 및 테스트 안정성 향상을 보장하기 위해 대상 저장소에 대한 HTTP 테스트 케이스를 수정했습니다. (CQ-4359022)
* Guava 라이브러리 종속성을 제거하기 위해 integration-adobeims-console 모듈에서 Guava 캐싱 사용을 제거했습니다. (CQ-4358710)
* AEM 6.5에서 적절한 작동을 보장하기 위해 AEM 6.6에서 DTM 통합 워크플로, 받은 편지함 작업 및 프로젝트 기능을 검증했습니다. (CQ-4358151)
* AEM 6.5 내 호환성 및 적절한 작동을 보장하기 위해 AEM 6.6에서 Content Insight 기능을 검증했습니다. (CQ-4357774)
* AEM 6.5 내 호환성 및 적절한 작동을 보장하기 위해 AEM 6.6의 클라우드 서비스 기능을 검증했습니다. (CQ-4357773)
* AEM 6.5 내 호환성 및 적절한 작동을 보장하기 위해 AEM 6.6에서 Adobe IMS 콘솔 통합을 검증했습니다. (CQ-4357772)
* Java 17에서 실행되도록 Test&amp;Target 통합을 위한 Jenkins 파이프라인을 업데이트하고, 실패한 Selenium 테스트를 해결하고, 일부 테스트를 Playwright로 옮기고, 모든 단위 테스트를 통과하도록 했습니다. (CQ-4357770)
* 빌드 및 테스트 파이프라인을 업데이트하여 DX 통합, 워크플로, 받은 편지함 및 프로젝트를 6.6.0 분기에 맞게 조정했습니다. 또한 업그레이드 호환성 문제를 해결하고, 영향을 받는 모든 서비스의 안정성과 기능을 검증했습니다. (CQ-4357767)

<!--
#### Jetty{#foundation-jetty-65-lts-sp1} -->

#### 현지화{#foundation-localization-65-lts-sp1}

* &#39;권한&#39; 목록에서 &#39;액세스 제어 제거&#39; 대화 상자의 문자열을 현지화하여 올바른 번역을 표시했습니다. (GRANITE-59427)
* 모델 편집기의 &#39;OR 분할 속성&#39; 규칙 추가 대화 상자에서 연산자와 필드 레이블을 포함한 여러 UI 문자열이 현지화되지 않은 상태로 표시되는 문제를 해결했습니다. 모든 문자열이 이제 올바르게 현지화되어 표시됩니다. (CQ-4354014)
* 워크플로 모델 편집 대화 상자에서 &#39;설명 표시&#39; 툴팁에 대해 누락된 번역을 추가했습니다. (CQ-4347996)

#### Oak {#foundation-oak-65-lts-sp1}

업그레이드 중에 AEM이 `/apps/system/config`에서 기존 구성 파일을 다시 만들거나 이름을 바꾸고, `.cfg.json` 파일을 `.config` 파일로 대체하는 문제를 해결했습니다. (GRANITE-58899)

#### Omnisearch{#foundation-omnisearch-65-lts-sp1}

입력 필드의 레이블로 플레이스홀더가 잘못 표시되는 접근성 문제를 해결했습니다. 이러한 문제는 검색, AEM 경험 조각, 콘텐츠 조각 및 콘텐츠 조각 모델에서 필드 레이블 누락을 야기합니다. (Granite-61791)

<!--
#### Platform{#foundation-platform-65-lts-sp1} -->

#### 프로젝트{#foundation-projects-65-lts-sp1}

* 프로젝트가 성공적으로 삭제되었음에도 불구하고 캘린더 보기에서 프로젝트를 삭제할 때 잘못된 오류 팝업이 표시되는 문제를 해결했습니다. (CQ-4358890)
* Firefox에서 프로젝트 보기의 &#39;자산 컬렉션&#39; 카드 바닥글이 카드 테두리와 겹치는 문제를 해결했습니다. 이제 바닥글이 겹치지 않고 올바르게 정렬됩니다. (CQ-4353317)

#### Quickstart{#foundation-quickstart-65-lts-sp1}

* 패키지 관리자를 통해 Guava 번들을 설치할 때 차단 목록에 추가되는 것을 방지하기 위해 제거 스크립트를 업데이트하여 Guava 번들의 버전 범위를 조정했습니다. (GRANITE-59559)
* 인터페이스에서 클래식 체크박스 처리를 수정하여 복제 에이전트를 편집할 때 오류(`#1660`)가 표시되는 복제 UI의 문제를 해결했습니다. (GRANITE-58302)
* 누락된 서비스 권한을 해결하고, 구성 처리를 업데이트하고, 필수 서비스가 올바르게 초기화되도록 함으로써 JDK 21과 함께 AEM 6.5 LTS를 실행할 때 발생하는 S3 데이터 저장소의 여러 시작 오류를 해결했습니다. (GRANITE-57082)
* AEM 6.5의 유지 관리 및 지속 가능성 전략을 정의했습니다. 이 수정 사항에는 다음이 포함되었습니다.
   * 서비스 팩 주기
   * 핫픽스 주기
   * AEM 6.6과의 병렬 지원
   * 지원 매트릭스 업데이트
   * 추가 기능 소유권 책임 (GRANITE-50459)

<!--
#### Security{#foundation-security-65-lts-sp1} -->

#### Sling{#foundation-sling-65-lts-sp1}

* 여러 `ResourceAccessGate` 참조가 `ResourceAccessSecurityImpl`을 초기화할 때 발생하는 `ClassCastException` 문제를 해결하기 위해 Sling ResourceAccessSecurity를 버전 1.1.2로 업데이트했습니다. (NPR-42750)
* Adobe Stock 통합에서 라이선스 대화 상자가 회색으로 표시되는 문제를 해결했습니다. 이 문제는 `sunt:initList` 함수에서 필수 입력 필드가 제거되어 발생했습니다. 해당 함수는 Coral Foundation 클라이언트 라이브러리에서 발견되었습니다. 필수 필드를 유지하고 적절한 라이선스 대화 상자 기능을 활성화하기 위해 클라이언트 라이브러리를 업데이트했습니다. (NPR-42748)
* `org.apache.sling.scripting.jsp 2.6.0`으로 인해 예기치 않은 JSP 컴파일 오류가 수정되었습니다. (NPR-42640)

<!--
* Backported the fix for Sling Scripting issue that caused `DataTimeParseException` and `String.length()` null pointer exceptions during package installation. Updated Sling Scripting to version 2.8.3-1.0.10.6 to reduce installation errors and improve stability. (NPR-42640) -->

<!--

#### Translation{#foundation-translation-65-lts-sp1} -->

#### 사용자 인터페이스{#foundation-ui-65-lts-sp1}

* AEM 작성자 UI에서 사용자 그룹 표시를 41개로 제한하는 문제를 해결했습니다. 이 문제는 Granite UI 그룹 선택기 구성 요소의 기본 배치 제한으로 인해 발생했습니다. 모든 그룹을 잘림 없이 표시하도록 구성 요소를 업데이트했습니다. (NPR-42749)
* 온프레미스 페이지 생성 마법사에서 페이지 속성을 편집할 때 다중 필드 구성 요소의 필수 필드가 다시 검증되지 않는 문제를 해결했습니다. 이 문제로 인해 작성자는 검증 과정을 건너뛰고 불완전한 데이터로 작업을 계속 진행할 수 있었습니다. (GRANITE-58826)
* AEM의 도움말 버튼에 대한 ARIA 속성을 수정하여 JAWS 화면 판독기가 번역되지 않은 아이콘과 텍스트 메타데이터를 표시하는 대신 명확하고 사용자 친화적인 레이블을 알릴 수 있도록 했습니다. (GRANITE-55360)

#### WCM{#foundation-wcm-65-lts-sp1}

* 번역 번들을 업데이트하고, Java 패키지 호환성을 검증하고, 사용되지 않는 종속성을 제거하고, 포괄적인 테스트를 통해 모든 기능을 보장하여 AEM 번역에 대한 Java 17 지원을 추가했습니다. (CQ-4357525)
* 자동화된 테스트 중에 거짓 실패가 발생하지 않도록 불안정한 Evergreen 테스트 `com.adobe.cq.platform.it.http.workflow.inbox.InboxOnOffTimeIT.testActivateLater`를 제거했습니다. (CQ-4298376)

#### 워크플로{#foundation-workflow-65-lts-sp1}

* Java 21과 함께 AEM 6.5 LTS를 사용할 때 URL에 정의되지 않은 값이 나타나는 것을 방지하기 위해 받은 편지함 항목에 누락된 `data-detailsurl` 속성을 추가했습니다. (GRANITE-60158)
* Java 21과 함께 AEM 6.5 LTS를 실행할 때 `WorkflowToPublishEventService` 번들의 `deactivate` 메서드에서 발생하는 NullPointerException을 수정하여 오류 없이 워크플로 서비스가 적절하게 종료되도록 했습니다. (GRANITE-58151)
* 공유, 사무실 외부 사용자 정의, 타임라인 쿼리 문제 해결을 지원하기 위해 워크플로 인덱스를 업데이트했습니다. (GRANITE-52640)
* 공유, 사무실 외부 사용자 정의 기능, 타임라인 쿼리 문제 해결을 지원하기 위해 워크플로 인덱스를 업데이트했습니다. (GRANITE-52294)
* AEM 릴리스 10912로 프로그램을 업그레이드할 때 로그 비교 검증 중에 오류 로그 오류가 증가하는 문제를 해결하여 안정적인 워크플로 실행을 보장했습니다. (GRANITE-44268)
* `url.searchParams`를 `url.search`로 대체하여 취약한 URL에 대한 XSS 보호를 강화하기 위해 워크플로 저장소의 URL 정리 방법을 업데이트했습니다. (CQ-4359585)
* 적절한 작동과 통합을 보장하기 위해 AEM 6.6 Forms의 워크플로, 받은 편지함 및 프로젝트 기능을 검증했습니다. (CQ-4358777)
* AEM 6.5에서 간소화되고 일관된 배포 프로세스를 지원하기 위해 Jenkins를 통해 Workflow-Content 아티팩트를 릴리스하는 자동화를 구현했습니다. (CQ-4358472)
* 작업이 이미 생성 중임에도 불구하고 제출을 클릭한 후 &#39;작업 추가&#39; 대화 상자가 JavaScript 구문 오류로 인해 닫히지 않는 문제가 발생하는 받은 편지함 작업 생성 워크플로의 문제를 해결했습니다. (CQ-4355336)
* `isEndUserConfigurationEnabled`에 대한 속성 정의가 누락되어 받은 편지함 보기 구성을 저장할 수 없었던 문제를 해결했습니다. (CQ-4287757)

## Forms

### Forms Designer

* 사용자가 exportDataAPI를 사용하여 XFA 기반 PDF에 대한 데이터를 내보낼 때 결과 XML이 Acrobat Reader를 사용하여 수동으로 내보낸 XML 데이터와 불일치합니다. Acrobat Reader에서 생성된 출력과 비교했을 때 일부 필드의 값이 출력에 누락되었습니다. (LC-3922791)
* Workbench의 출력 서비스를 사용하여 태그가 지정된 PDF를 생성하면 목차 항목의 참조 태그 아래에 예기치 않은 레이블 태그가 추가됩니다. (LC-3922756)
* 출력 서비스를 사용하여 동적이고 입력 가능한 PDF를 PDF/A 형식으로 평면화할 때 동적 상태가 보존되지 않습니다. 이 문제는 특히 태그 지정이 활성화된 경우 데이터 손실과 잠재적인 규정 준수 문제가 발생됩니다. (LC-3922708)
* 사용자가 AEM Forms Designer에서 필드 캡션을 하단 또는 오른쪽 정렬로 배치하면 태그 트리에 해당 값이 없는 캡션만 포함되어 접근성 태그 지정이 불완전해집니다. (LC-3922619)
* 생성된 PDF의 QR 코드를 읽을 수 없게 됩니다. QR 코드에 대한 대체 텍스트도 접근성 테스트에 실패하여 화면 판독기 호환성에 영향을 미칩니다. (LC-3922551)
* 사용자가 에이전트 UI에서 문자를 렌더링하면 FormService render() API로 인해 콘텐츠가 올바르게 표시되지 않습니다. (LC-3922461)
* 사용자가 AEM Forms에서 Sunken Square 스타일이 있는 XDP에서 PDF/A 파일을 생성하려고 하면 테두리 렌더링 문제가 발생합니다. (LC-3922180)
* XSD 스키마에 바인딩된 동적 양식을 병합하면 일부 바인딩된 양식 데이터가 최종 PDF에 유지되지 않으므로 부분적인 데이터 손실이 발생합니다. (LC-3922008)
* 사용자가 AEM Forms 6.5.13 이상 버전에서 extractData API를 사용하여 대화형 PDF에서 데이터를 내보내려고 하면 수동 내보내기와 비교하여 데이터가 누락됩니다. (LC-3921983)
* AEM Forms Designer 또는 출력 서비스를 사용하여 XDP 양식을 정적 PDF로 변환하면 여러 `Link-OBJR` 태그가 생성됩니다. 이 문제들은 단일 통합 링크 태그가 예상되기 때문에 접근성 준수 문제가 발생합니다. (LC-3921977)

### 적응형 양식

* AEM Forms에서 루트 패널에 “제목에 리치 텍스트 허용”을 활성화하면 중첩된 패널에서 “기록 문서에서 제목 제외”가 기록 문서에 루트 패널의 제목을 잘못 숨깁니다. 이는 생성된 기록 문서에서 수행됩니다. (FORMS-19696)
* 시스템이 JSON 스키마에서 `aem:afProperties`를 통해 할당된 사용자 정의 `sling:resourceType`을 무시합니다. 렌더링 중에 사용자 정의 리소스 유형이 무시됩니다. (FORMS-19691)
* 사용자가 URI를 사용하여 미리 채워진 첨부 파일로 적응형 양식을 제출하면 바이너리 데이터가 누락되어 NullPointerException으로 인해 양식 제출이 실패합니다. (FORMS-19371) (FORMS-19486)
* 사용자가 &#39;양식 및 문서&#39; 섹션에 PDF를 업로드하면 타임라인 기능이 작동을 멈춥니다. (FORMS-19407)(FORMS-19234)
* 사용자가 AEM Forms의 기본 제공(OOTB) 파일 첨부 구성 요소로 파일을 업로드하면 보안 취약성이 식별됩니다. 이 문제로 인해 승인되지 않은 엔티티에 의한 제출 프로세스의 잠재적인 가로채기로 이어집니다. (FORMS-19271)
* 사용자가 기록 문서(DoR)를 자동으로 생성하도록 AEM Forms의 기본 제공 적응형 양식을 구성하면 Acrobat Reader의 문서 속성에 있는 “제목” 필드에 캡처된 DoR 제목이 표시되지 않습니다. 기본적으로 양식 제목은 파일 이름 대신 나타나지 않습니다. (FORMS-19263)
* 사용자가 에이전트 UI에서 대화형 커뮤니케이션을 열면 미리 채워진 데이터를 완전히 지울 수 없습니다. 제거 시 동일한 데이터로 자동으로 채워집니다. (FORMS-19151)
* 사용자가 에이전트 UI에서 날짜 필드를 미리 볼 때 날짜가 예기치 않게 변경됩니다. 이 문제는 VM의 UTC 설정과 시스템의 날짜 해석 간의 시간대 불일치로 인해 발생합니다. (FORMS-19115)
* 사용자가 양식을 제출하면 파일 첨부 파일이 중복되어 동일한 파일이 여러 번 업로드될 수 있습니다. (FORMS-19045)(FORMS-19051)
* 문서 보안에서 정책 세트에 코디네이터를 추가하는 작업은 프로덕션 및 하위 환경 모두에서 실패합니다. (FORMS-18603, FORMS-18212, FORMS-19697)
* 사용자가 데스크탑 모드에서 빈 필드의 “datepicker-calendar-icon”을 클릭하면 정의되지 않은 _$focusedDate 변수로 인해 오류가 발생하여 관련 사용자 정의 스크립트가 중단됩니다. (FORMS-18483)(FORMS-18268)
* 고객이 문자를 미리 볼 때 &#39;단어 수&#39; 필드에 숫자 값이 표시되지 않거나 잘못 업데이트되어 콘텐츠에 정렬 오류가 발생하고 공백이 누락됩니다. (FORMS-18437, FORMS-17330, FORMS-18209, FORMS-18557, CTG-4150848,FORMS-19614, LC-3922004)
* 고객이 RHEL에서 저장된 문자를 미리 볼 때 콘텐츠가 잘못 정렬되고 공백이 누락되며 &#39;x&#39;와 같은 예기치 않은 문자가 나타납니다. (FORMS-18422)(FORMS-17641)
* 사용자가 AEM Forms의 탭 사이를 이동하면 첫 번째 탭의 구성 요소 선택이 응답하지 않습니다. (FORMS-18345)
* 사용자가 WebToPDF 옵션을 사용하여 HTML 파일을 PDF로 변환하면 출력 PDF에 메타데이터 및 제목 태그를 포함한 헤더 섹션이 누락됩니다. (FORMS-18223, FORMS-17835, FORMS-19642, FORMS-18224)
* AEM JEE Process Manager SDK에서 사용자가 retryAction(long actionOid) 메서드를 호출하면 시스템이 tb_action_instance 테이블에서 발견된 첫 번째 작업을 잘못 재시도합니다. 이 워크플로는 특정 작업 ID가 제공되거나 ID가 null인 경우에도 발생하여 의도하지 않은 비헤이비어가 발생합니다. (FORMS-18187)
* 사용자는 오류 메시지가 표시되지 않고 초안 저장 및 제출 기능이 실패하는 문제에 직면합니다. (FORMS-18069)
* XSD 기반 기초 구성 요소에서 핵심 구성 요소로 전환하면 JSON 스키마에서 교차 파일 참조를 구현할 수 없어 적응형 양식 마이그레이션에 영향을 미칩니다. (FORMS-18065)
* 사용자가 에이전트 UI에서 문자를 미리 볼 때 IC 시간 변환 문제로 인해 날짜 필드에 잘못된 값이 표시됩니다. 이러한 불일치는 VM 환경과 시스템의 시간 해석(UTC 및 현지 시간) 간의 시간대 차이로 인해 발생합니다. (FORMS-17988) (FORMS-17248)
* 사용자가 AEM Forms에서 Notice IC 템플릿을 사용하여 문자를 미리 보면 동일한 서버에서도 PDF 생성 시간이 1.5초에서 10초 이상까지 크게 다릅니다. 이 불일치는 비즈니스에 중요한 워크플로에 영향을 미칩니다. (FORMS-17951)
* 사용자가 &#39;데이터 소스&#39; 옵션을 사용하여 적응형 양식의 스크리블 서명 오브젝트를 XDP에 바인딩하면 변경 사항을 저장할 수 없습니다. 유효한 값을 사용할 때도 종횡비 유효성 검사 오류가 지속적으로 발생하기 때문입니다. (FORMS-17587)
* 사용자가 문서 조각에 숨겨진 필드가 많은 특정 XDP를 사용할 때, AEM은 `cm:optional` 속성이 false로 설정된 CRX 노드를 생성하여 인터랙티브 커뮤니케이션(IC) 제출이 실패하게 됩니다. (FORMS-17538)
* 고객이 문자를 미리 볼 때, 숫자 상자 필드가 Lead 및 Frac에 대한 숫자 제한이 정의된 경우 음수 값을 올바르게 처리하지 못합니다. 이 문제는 빼기 기호를 숫자의 일부로 처리하는 parseFloat를 사용하기 때문에 발생합니다. (FORMS-17451)
* 레터를 미리 볼 때 Adobe.json 파일에서 “*” 와일드카드가 사용되는 것이 발견되어 그 목적 및 잠재적 수정에 대한 우려가 제기됩니다. (FORMS-17317)
* 사용자가 고정 금리 저축 공동 계좌 신청 시 화면 판독기를 사용하면 제목이 클릭 가능한 것으로 잘못 안내되어 접근성 문제가 발생합니다. (FORMS-17038)
* 양식이 임베드되면 생성된 iframe에 제목 속성이 누락되어 접근성 규정 준수 문제가 발생합니다. (FORMS-17010)
* Forms Manager UI를 사용하여 양식을 다운로드하면 테마 및 조각과 같은 관련 종속성이 항상 포함됩니다. (FORMS-15811)
* 사용자가 모바일 디바이스(iOS 및 Android™)에서 양식에 액세스하면 첫 번째 페이지의 &#39;다음&#39; 및 &#39;이전&#39; 버튼이 비활성화됩니다. 그러나 화면 판독기는 비활성화된 것으로 식별하지 않습니다. (FORMS-15773)
* 사용자가 조각 및 지연 로딩이 활성화된 상태에서 큰 양식을 저장하면 초안을 검색하지 못하여 워크플로가 중단됩니다. (FORMS-19890, FORMS-19808)
* 사용자는 핵심 구성 요소를 기반으로 하는 적응형 양식에 대한 양식 속성을 저장하는 데 문제를 겪었습니다. 이 오류는 기초 구성 요소 편집기를 기반으로 하는 적응형 양식의 중복 스크립트가 포함되어 핵심 구성 요소를 기반으로 하는 적응형 양식에서 충돌이 발생했기 때문입니다. 편집기 (FORMS-17474)
* 사용자는 iframe에서 Adobe Sign GovCloud 서명 페이지가 렌더링되지 않는 문제를 경험했습니다. (FORMS-16803)
* 사용자는 핵심 구성 요소 적응형 양식(AF) 조각에 대한 참조를 선택할 때 오류를 경험합니다. “참조를 렌더링할 수 없습니다. 절대 경로가 아닙니다”라는 오류 메시지가 나타나 참조를 제대로 렌더링할 수 없습니다. (FORMS-19678)
* Acrobat DC를 사용한 다중 스레드 변환에 대한 지원이 추가되어 사용자가 Word, Excel 및 PowerPoint 문서를 PDF 문서로 동시에 더 효율적으로 변환할 수 있습니다. (FORMS-21310)
* AEM 서비스 팩 24에 `com.adobe.granite.toggle.impl.dev` 번들을 포함하여 Forms 추가 기능에서 제거하여 더 간소화된 개발 프로세스를 지원합니다. (FORMS-20139)
* forms-foundation에서 FeatureToggleRenderConditionServlet을 제거했고 forms add-on에서 com.adobe.granite.toggle.impl.dev 번들을 제거했습니다. 이 업데이트는 Forms 추가 기능 설치 후 렌더링 조건이 올바르게 해결되도록 하여 고객을 위한 구성 요소 기능을 개선합니다. (FORMS-20138)
* 사용자는 적응형 양식에서 장기 실행 쿼리로 인해 성능이 저하되는 문제를 경험했습니다. 이 업데이트는 효율성을 개선하기 위해 쿼리 변경 사항을 백포트합니다. 이제 고객들은 aemformsAFReferences라는 태그 이름으로 인덱스를 생성할 수 있습니다. (FORMS-21411)
* 사용자는 WebtoPDF를 사용하여 HTML을 PDF(Portable Document Format)로 변환할 때 헤더 위치가 잘못 정렬되는 문제를 경험했습니다. 이 문제는 문서 레이아웃 일관성 및 출력의 가독성에 영향을 미쳤습니다. (FORMS-21502, FORMS-21540)
* 사용자는 PreFlight 확인에 성공했음에도 불구하고 PDF/A-1b 유효성 검사 실패를 경험했습니다. 이 문제는 PDF 유효성 검사 도구를 사용하는 기업 고객의 문서 규정 준수 검사에 영향을 미쳤습니다. (FORMS-20196)
* 사용자는 UI에 번역되지 않은 문자열을 경험하여 인터페이스를 이해하는 데 혼란과 어려움을 겪었습니다. (FORMS-6542)
* 사용자는 이메일 알림 문제를 경험했습니다. 이메일 보내기 워크플로 단계에서 이메일을 보내는 데 실패하여 자동화된 커뮤니케이션 프로세스에 영향을 미쳤습니다. (FORMS-17961)
* 사용자는 양식 워크플로에 대한 테스트 실패를 경험했고, 이로 인해 워크플로 프로세스를 효율적으로 완료하는 기능에 영향을 받았습니다. (FORMS-16231)
* 사용자는 AEM Forms에서 PDF 파일의 타임라인 기능을 사용할 수 없었습니다. 이 문제는 사용자가 문서 변경 사항 및 수정을 효율적으로 추적하는 능력에 영향을 미쳤습니다. AEM Forms 영역의 &#39;양식 및 문서&#39; 섹션에 PDF를 업로드하면 타임라인 보기가 작동을 멈춥니다. (FORMS-19408)
* 사용자는 OData와 상호 작용할 때 null 포인터 예외를 경험합니다. 이로 인해 데이터 검색 프로세스가 중단됩니다. (FORMS-20348)
* 오픈 소스 Java 라이브러리인 Guava가 제거된 후 google.common.collect 라이브러리도 제거되었습니다. 이 업데이트는 적응형 양식을 사용하는 기업 고객을 위한 더 나은 호환성 및 성능을 보장합니다. (FORMS-17031)

### Forms Captcha

* 기초 구성 요소를 기반으로 한 적응형 양식에 대한 `Hcaptcha` 및 `Turnstile` 지원이 추가되었습니다. (FORMS-16562)
* 사용자는 `Create hCaptcha Configuration` 대화 상자에서 아이콘 겹침 문제를 경험했습니다. 필수 필드를 입력할 때 정보 아이콘이 오류 아이콘과 겹쳐 구성 설정 중에 혼란을 야기했습니다. (FORMS-16916)
* 사용자는 기초 구성 요소를 기반으로 하는 적응형 양식에서 reCAPTCHA에 대해 잘못된 구성이 선택되는 문제를 경험했습니다. 양식에 대해 구성 컨테이너가 선택되지 않은 경우 `conf/global` 폴더의 여러 구성으로 인해 문제가 발생했습니다. (FORMS-19237)
* 사용자는 reCAPTCHA가 렌더링되지 않는 문제를 경험했습니다. 이 문제는 기업 고객의 양식 제출 및 보안 유효성 검사에 영향을 미쳤습니다. (FORMS-17136, FORMS-19596)
* 사용자는 reCAPTCHA Enterprise의 크기가 사용자 인터페이스(UI)에 반영되지 않는 문제를 경험합니다. (FORMS-16574)
* 사용자는 `ReCaptchaConfigurationServiceImpl`의 비공개 ResourceResolver로 인해 ReCaptcha 기능에 문제가 발생하여 양식 제출 중에 간헐적인 유효성 검사 실패를 경험했습니다. (FORMS-19241)
* 사용자는 양식이 Sites에서 작성될 때 reCAPTCHA 유효성 검사 문제를 경험했습니다. AEM Forms가 양식 이름을 올바르게 인식하지 못하여 유효성 검사 실패가 발생했습니다. (FORMS-20486)
* 사용자는 기업 reCAPTCHA 점수가 1.0일 때도 양식 제출을 경험했으며, 이는 잠재적인 보안 위험으로 이어졌습니다. (FORMS-16766){{$include }}
* 제출 오류 코드를 400으로 업데이트하여 적응형 양식에서 reCAPTCHA 경고를 개선했습니다. 또한 로그 경고를 개선하여 시간 초과, 만료 및 봇 감지 실패를 구분함으로써 문제 해결 정확도와 시스템 관찰 가능성을 향상했습니다. (FORMS-19240)
* ReCaptchaConfigurationServiceImpl의 닫히지 않은 ResourceResolver 인스턴스를 닫아 AEM Forms에서 reCAPTCHA 통합을 사용할 때 잠재적인 리소스 누수를 방지하고 시스템 안정성을 개선했습니다. (FORMS-19242)
* conf/global 폴더에 여러 항목이 있는 경우 올바른 구성이 각 양식에 바인딩되도록 하여 AEM Forms에 대한 CAPTCHA 구성 처리를 개선했습니다. 구성 컨테이너가 명시적으로 선택되지 않은 경우 잘못된 CAPTCHA 설정이 의도치 않게 사용되는 것을 방지합니다. (FORMS-19239)

### Forms 관리 UI

* 사용자는 `Forms` > `Create Watchfolder` >` Watchfolder` 생성 과정에서 현지화되지 않은 문자열을 경험했습니다. 감시 폴더를 만들 때 `Watchfolder creation` 및 `Watchfolder created successfully`와 같은 문자열이 발견되지 않아 사용자 인터페이스 경험에 영향을 미쳤습니다. (FORMS-15234)

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
* 자세한 업그레이드 지침은 [JEE의 AEM Forms 6.5 LTS SP1용 업그레이드 안내서](https://experienceleague.adobe.com/ko/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)를 참조하십시오.

#### AEM 6.5 LTS 서비스 팩 업그레이드에 대한 모범 사례

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

**환경**
적용 대상: 서비스 팩 1(SP1)을 설치하는 AEM 6.5 LTS (On-Premise) 고객 SP1은 Quickstart JAR로 제공됩니다.

**이것이 중요한 이유**
AEM 6.5 LTS용 SP1은 패키지 관리자를 통해 설치하기 위해 ZIP이 아닌 Quickstart JAR로 제공됩니다. On-prem 고객은 Quickstart JAR을 대체하고 압축을 푼 다음 다시 시작하여 업그레이드합니다. 이 방법은 Adobe의 즉석 업그레이드 절차와 일치합니다.

**권장 업그레이드 흐름 (작성자 또는 게시)**

1. AEM 6.5 LTS 인스턴스가 정상적이고 액세스할 수 있는지 확인합니다.
1. 소프트웨어 배포에서 SP1 Quickstart JAR(예: `cq-quickstart-6.6.x.jar`)을 다운로드합니다.
1. 실행 중인 인스턴스를 중단합니다.
1. AEM 설치 디렉터리(`crx-quickstart/` 외부)에서 이전 Quickstart JAR을 SP1 JAR로 대체합니다.
1. JAR 압축을 풉니다.

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   (필요에 따라 힙 플래그를 조정합니다.)

1. 역할 및 포트와 일치하도록 압축 해제된 JAR의 이름을 변경합니다(예: `cq-author-4502.jar` 또는 `cq-publish-4503.jar`).
1. AEM을 시작하고 UI(도움말 > 정보) 및 로그에서 업그레이드를 확인합니다.

**위생 관리**

* 프로덕션 전에 하위/테스트 환경에서 업그레이드를 실행합니다.
* 시작하기 전에 복원 가능한 전체 백업(저장소와 모든 외부 데이터 저장소)을 수행합니다.
* Adobe의 즉석 업그레이드 지침 및 기술 요구 사항(LTS에 대해 Java 17/21 권장)을 검토합니다.

>[!NOTE]
>
>위에 표시된 파일 이름(예: `cq-quickstart-6.6.x.jar`)은 이 LTS 릴리스에서 관찰된 SP1 Quickstart 아티팩트 이름을 반영하므로 항상 소프트웨어 배포에서 다운로드한 정확한 파일 이름을 사용하십시오.

## 설치 및 업데이트 {#install-update}

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

Adobe은 기존 기능을 현대화하거나 대체하여 더 큰 고객 가치를 제공하기 위해 제품 기능을 지속적으로 검토하고 발전시킵니다. 이러한 변경 사항은 이전 버전과의 호환성을 신중하게 고려하여 구현됩니다.

Adobe은 투명성을 보장하고 적절한 계획을 수립할 수 있도록 Adobe Experience Manager(AEM)에 대한 이 사용 중단 프로세스를 따릅니다.

* 사용 중단이 먼저 발표됩니다. 사용 중단되는 기능은 계속 사용할 수 있지만 더 이상 개선되지 않습니다.

* 제거는 다음 주요 릴리스 이후에 수행됩니다. 계획된 제거 타임라인은 별도로 통신됩니다.

* 기능이 제거되기 전에 고객이 지원되는 대체 요소로 전환할 수 있도록 최소 하나의 릴리스 주기가 제공됩니다.

### 더 이상 사용되지 않는 기능 {#deprecated-features}

이 섹션에는 Adobe가 AEM 6.5 LTS에서 더 이상 사용되지 않는 기능이 나열됩니다. 일반적으로 Adobe는 향후 릴리스에서 해당 기능을 제거하기 전에 해당 기능을 더 이상 사용하지 않도록 설정하고 사용할 수 있는 대안을 제공합니다.


현재 배포에서 해당 기능을 사용 중인지 검토하고 이들 구현을 변경하여 제공되는 대체 기능을 사용하도록 계획을 세우는 것이 좋습니다.

| 영역 | 기능 | 대체 | 버전 (SP) |
| --- | --- | --- | --- |
| Sites | [SPA 편집기](/help/sites-developing/spa-overview.md) | AEM에서 Headless 콘텐츠를 관리하기 위한 권장 편집기:<br>- 시각적 편집을 위한 [범용 편집기](/help/sites-developing/universal-editor/introduction.md)<br>- 양식 기반 편집을 위한 [콘텐츠 조각 편집기](/help/assets/content-fragments/content-fragments-managing.md) | 6.5 LTS GA |

### 제거된 기능 {#removed-features}

이 섹션에는 AEM 6.5 LTS에서 제거된 기능이 나열됩니다. 이전 릴리스에서는 이러한 기능이 더 이상 사용되지 않는다고 표시되었습니다.

* CRX 저장소 지속성을 위한 RDBMK 지원이 제거되었습니다.

* 클러스터된 환경에서 MongoMK는 이제 저장소 지속성에 대한 유일한 지원 옵션입니다.

| 영역 | 기능 | 대체 | 버전 (SP) |
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

<!-- DO THESE KNOWN ISSUES CARRY OVER EACH RELEASE? THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

<!-- REMOVED THIS SECTION AS PER CQDOC-23046
### Issue with JSP scripting bundle in AEM 6.5.21-6.5.23 and AEM 6.5 LTS GA

AEM 6.5.21, 6.5.22, 6.5.23, and AEM 6.5 LTS GA ship with the `org.apache.sling.scripting.jsp:2.6.0` bundle, which contains a known issue. The issue typically occurs under high load when the AEM instance handles many concurrent requests.

When this issue occurs, one of the following exceptions may appear in the error logs alongside references to `org.apache.sling.scripting.jsp:2.6.0`:

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

A hotfix [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip) is available to resolve this problem. -->

### SSL 전용 기능을 사용한 Dispatcher 연결 실패 (AEM 6.5 LTS SP1 이상에서 수정됨){#ssl-only-feature}

>[!NOTE]
>
> 이 문제는 AEM 6.5 LTS GA 릴리스에서만 발생합니다.

AEM 배포에서 SSL 전용 기능을 활성화하면 Dispatcher와 AEM 인스턴스 간의 연결에 영향을 미치는 알려진 문제가 있습니다. 이 기능을 활성화한 후에는 상태 검사가 실패할 수 있으며 Dispatcher와 AEM 인스턴스 간의 통신이 중단될 수 있습니다. 이 문제는 고객이 Dispatcher에서 AEM 인스턴스로 `https + IP`를 통해 연결을 시도할 때 발생합니다. 이는 SNI(서버 이름 표시) 유효성 검사 문제와 관련이 있습니다.

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

## OSGi 번들 및 콘텐츠 패키지 포함됨{#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 이 [!DNL Experience Manager] 6.5 LTS, 서비스 팩 1 릴리스에 포함된 OSGi 번들과 콘텐츠 패키지가 나열되어 있습니다.

* [Experience Manager 6.5 LTS, 서비스 팩 1에 포함된 OSGi 번들 목록](/help/release-notes/assets/65lts_sp1_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5 LTS, 서비스 팩 1에 포함된 콘텐츠 패키지 목록](/help/release-notes/assets/65lts_sp1_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 제한된 웹 사이트{#restricted-sites}

이들 웹 사이트는 고객만 사용할 수 있습니다. 고객이시며 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 센터](https://experienceleague.adobe.com/ko/docs/customer-one/using/home)에 문의하십시오.

