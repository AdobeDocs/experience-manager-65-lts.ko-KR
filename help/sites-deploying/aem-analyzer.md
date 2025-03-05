---
title: AEM Analyzer를 사용한 업그레이드 복잡성 평가
description: AEM Analyzer 를 사용하여 업그레이드의 복잡성을 평가하는 방법을 알아봅니다.
topic-tags: upgrading
content-type: reference
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 2645745a83477509bac81cb5e122eabc44db3961
workflow-type: tm+mt
source-wordcount: '2068'
ht-degree: 15%

---


# AEM Analyzer를 사용한 업그레이드 복잡성 평가 {#assessing-the-upgrade-complexity-with-the-aem-analyzer}

## 개요 {#overview}

AEM 6.5 LTS 분석기는 6.5 LTS에 원활한 업그레이드 환경을 제공하기 위해 업데이트가 필요한 영역을 표시하여 현재 AEM 구현에 대한 평가를 제공합니다.

이 도구는 잠재적 리팩터링 영역을 식별하는 보고서를 생성합니다.

## AEM 6.5 LTS Analyzer 보고서 {#aem-65lts-analyzer-report}

AEM 6.5 LTS 분석기 보고서는 일반적인 업그레이드 준비 상태를 세부적으로 파악하는 데 사용됩니다. 이 보고서는 AEM 6.5 LTS로의 성공적인 업그레이드를 위해 해결해야 하는 문제 카테고리 내의 검색 결과로 구성됩니다.

AEM 6.5 LTS Analyzer 보고서에는 다음 카테고리가 포함됩니다.

* 리팩터링해야 하는 애플리케이션 기능
* 지원되는 위치로 이동해야 하는 저장소 항목
* 구성 문제
* 새로운 기능으로 제거되었거나 현재 AEM 6.5 LTS에서 지원되지 않는 AEM 6.5 기능
* Java 및 Guava API 사용 제거

카테고리 및 이러한 카테고리와 관련된 가능한 의미 및 솔루션에 대한 추가 정보는 AEM 6.5 LTS 분석기 보고서 내에서 링크를 통해 제공됩니다.

## 사용 가능 {#analyzer-availability}

[소프트웨어 배포 포털](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)에서 AEM 분석기를 zip 파일로 다운로드할 수 있습니다. 원본 AEM 인스턴스에서 [패키지 관리자](/help/sites-administering/package-manager.md)를 통해 패키지를 설치할 수 있습니다.

## AEM Analyzer 사용에 대한 중요 고려 사항 {#important-considerations-for-using-aem-analyzer}

AEM Analyzer 실행을 위한 중요한 고려 사항을 이해하려면 아래 섹션을 따르십시오.

* 분석기 보고서는 AEM [패턴 탐지기](/help/sites-deploying/pattern-detector.md)의 출력을 사용하여 작성됩니다. Analyzer에서 사용하는 패턴 탐지기 버전은 AEM Analyzer 설치 패키지에 포함되어 있습니다
* AEM 분석기는 **관리자** 사용자 또는 **관리자** 그룹의 사용자만 실행할 수 있습니다.
* Analyzer 는 버전 6.5 이상의 AEM 인스턴스에서 지원됩니다.

>[!NOTE]
>
>비즈니스 크리티컬 인스턴스에 영향을 주지 않도록 사용자 지정, 구성, 컨텐츠 및 사용자 애플리케이션 영역의 프로덕션 환경에 최대한 가까운 스테이징 환경에서 AEM Analyzer를 실행하는 것이 좋습니다. 또는 프로덕션 작성 환경의 복제본에서 실행할 수 있습니다.

* AEM Analyzer 보고서 컨텐츠를 생성하는 데 몇 분에서 몇 시간까지 상당한 시간이 걸릴 수 있습니다. 필요한 시간은 AEM 저장소 컨텐츠, AEM 버전 및 기타 요소에 따라 크게 달라집니다
* 보고서 컨텐츠를 생성하는 데 필요한 상당한 시간으로 인해 백그라운드 프로세스에 의해 생성되고 캐시에 보관됩니다. 보고서가 만료되거나 보고서가 명시적으로 새로 고쳐질 때까지 컨텐츠 캐시를 활용하므로 보고서를 보고 다운로드하는 작업이 상대적으로 빨라야 합니다. 보고서 컨텐츠를 생성하는 동안 브라우저 탭을 닫고 나중에 돌아와서 컨텐츠가 캐시에서 사용 가능하게 되면 보고서를 볼 수 있습니다.

## AEM 분석기 보고서 보기 {#viewing-the-aem-analyzer-report}

AEM Analyzer 보고서를 보려면 아래 단계를 따르십시오.

1. Adobe Experience Manager을 선택하고 **도구 - 작업 - 6.5 LTS 현대화 도구**&#x200B;로 이동합니다.

   ![분석기 보고서 보기 1](/help/sites-deploying/assets/view-analyzer-report-1.png)

1. **AEM 6.5 LTS 분석기**&#x200B;를 클릭하여 엽니다.

   ![분석기 보고서 보기 2](/help/sites-deploying/assets/view-analyzer-report-2.png)

1. AEM 분석기를 실행하려면 **보고서 생성**&#x200B;을 클릭하세요.

   ![분석기 보고서 보기 3](/help/sites-deploying/assets/view-analyzer-report-3.png)

1. AEM 분석기가 보고서를 생성하는 동안 도구에서 수행한 진행 상황을 화면에 볼 수 있습니다. 완료율 기준으로 진행률이 표시됩니다. 또한 분석된 항목 수와 검색 결과 수를 표시합니다

   ![분석기 보고서 보기 4](/help/sites-deploying/assets/view-analyzer-report-4.png)

1. 6.5 LTS Analyzer 보고서가 생성되면 요약 및 결과 수가 검색 유형 및 중요도 수준별로 구성된 표 형식으로 표시됩니다. 특정 검색 결과에 대한 자세한 내용을 보려면 테이블에서 검색 유형에 해당하는 숫자를 클릭합니다

   ![분석기 보고서 보기 5](/help/sites-deploying/assets/view-analyzer-report-5.png)

1. **CSV로 내보내기**&#x200B;를 클릭하여 쉼표로 구분된 값(CSV) 형식으로 보고서를 다운로드할 수 있습니다. **보고서 새로 고침**&#x200B;을 클릭하여 분석기가 캐시를 지우고 보고서를 다시 생성하도록 할 수 있습니다. 캐시가 만료되면 보고서를 다시 생성해야 합니다.

## AEM 분석기 보고서 해석 {#interpreting-the-aem-analyzer-report}

AEM 인스턴스에서 6.5 LTS 분석기 도구를 실행하면 보고서가 도구 창의 결과로 표시됩니다.

보고서의 형식은 다음과 같습니다.

* **보고서 개요**: 다음 정보를 포함하는 보고서 자체에 대한 정보:

   * **보고서 시간**: 보고서 내용이 생성되어 처음 사용할 수 있게 된 시기
   * **만료 시간**: 보고서 내용 캐시가 만료되는 시기
   * **생성 기간**: 보고서가 생성된 시간입니다
   * **검색 횟수**: 보고서에 포함된 총 검색 결과 수

* **시스템 개요**: 분석기가 실행된 AEM 시스템에 대한 정보
* **카테고리 찾기**: 각 섹션에서 동일한 카테고리의 하나 이상의 발견을 처리하는 여러 섹션. 각 섹션에는 카테고리 이름, 하위 유형, 검색 횟수 및 중요도, 요약, 카테고리 설명서 링크 및 개별 검색 정보가 포함됩니다.

  ![Analyzer 보고서 요약](/help/sites-deploying/assets/analyzer-report-summary.png)

  작업의 대략적인 우선순위를 나타내기 위해 각 검색 결과에 중요도 수준이 지정됩니다.

>[!NOTE]
>
>각 검색 범주에 대한 자세한 내용은 [패턴 탐지기 범주](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/aso)를 참조하세요.

중요도 수준을 이해하려면 아래 표를 따르십시오.

| 중요 | 설명 |
|---|---|
| 정보 | 이 검색 결과는 정보용으로 제공됩니다. |
| 권고 조치 | 이 검색 결과는 잠재적으로 업그레이드 문제가 될 수 있습니다. 추가 조사가 권장됩니다. |
| 위험 | 이 검색 결과는 기능 또는 성능 손실을 방지하기 위해 해결해야 하는 업그레이드 문제가 될 가능성이 높습니다. |

## AEM 6.5 LTS 분석기 CSV 보고서 해석 {#interpreting-the-aem-65lts-analyzer-report}

AEM 인스턴스에서 **CSV** 옵션을 클릭하면 Analyzer 보고서의 CSV 형식이 컨텐츠 캐시에서 만들어지고 브라우저에 반환됩니다. 브라우저 설정에 따라 이 보고서는 기본 이름이 `report.csv`인 파일로 자동 다운로드됩니다.

캐시가 만료된 경우 CSV 파일을 빌드하고 다운로드하기 전에 보고서가 다시 생성됩니다.

보고서의 CSV 형식에는 패턴 탐지기 출력에서 생성된 정보가 포함되어 있으며 카테고리 유형, 하위 유형 및 중요도 수준별로 정렬 및 구성됩니다. 이 형식은 Microsoft Excel과 같은 애플리케이션에서 보고 편집하는 데 적합합니다. 진행 상황을 측정하기 위해 시간 경과에 따른 보고서를 비교할 때 유용할 수 있는 모든 검색 정보를 반복 가능한 형식으로 제공하기 위한 것입니다.

CSV 형식 보고서의 열은 다음과 같습니다.

* **코드**: 카테고리 코드
* **유형**: 카테고리 이름
* **하위 유형**: 카테고리 하위 유형
* **중요도**: 중요 수준
* **식별자**: 검색 결과의 기본 식별자
* **메시지**: 검색 결과에 대해 제공된 메시지
* **컨텍스트**: 데이터를 찾기 위한 JSON 문자열

개별 검색 열에 있는 &quot;`\N`&quot; 값은 제공된 데이터가 없음을 나타냅니다.

## HTTP 인터페이스 {#http-interface}

6.5 LTS 분석기는 AEM 내의 사용자 인터페이스 대신 사용할 수 있는 HTTP 인터페이스를 제공합니다. 인터페이스는 `HEAD` 및 `GET` 명령을 모두 지원합니다. Analyzer 보고서를 생성하고 JSON, CSV 및 탭으로 구분된 값(TSV)의 세 형식 중 하나로 반환하는 데 사용할 수 있습니다.

다음 URL을 HTTP 액세스에 사용할 수 있습니다. 여기서 `<host>`은(는) 필요한 경우 Analyzer가 설치된 서버의 포트와 함께 호스트 이름입니다.

* JSON 형식용 `http://<host>/apps/aem66-analyzer/analysis/report.json`
* CSV 형식용 `http://<host>/apps/aem66-analyzer/analysis/report.csv`
* TSV 형식용 `http://<host>/apps/aem66-analyzer/analysis/report.tsv`

### HTTP 요청 실행 {#executing-an-http-request}

HTTP 요청을 실행하는 간단한 방법 중 하나는 관리자로 AEM에 이미 로그인한 동일한 브라우저에서 탭을 여는 것입니다. 브라우저 탭에 URL을 입력하고 결과를 브라우저가 표시하거나 다운로드하도록 할 수 있습니다.

`curl` 또는 `wget`과(와) 같은 명령줄 도구와 HTTP 클라이언트 응용 프로그램을 사용할 수도 있습니다. 인증된 세션에서 브라우저 탭을 사용하지 않는 경우 주석의 일부로 관리 사용자 이름과 암호를 제공해야 합니다.

다음은 이 작업을 수행하는 방법의 예입니다.

```shell
curl -u admin:admin 'http://localhost:4502/apps/aem66-analyzer/analysis/report.csv' > report.csv.
```

## 캐시 수명 조정 {#adjusting-the-cache-lifetime}

기본 AEM 6.5 LTS 분석기 캐시 수명은 24시간입니다. 보고서를 새로 고치고 캐시를 다시 생성하는 옵션과 함께 AEM 인스턴스와 HTTP 인터페이스 모두에서 이 기본값은 AEM 6.5 LTS 분석기의 대부분의 사용에 적절할 수 있습니다. 보고서 생성 시간이 AEM 인스턴스에 대해 특히 긴 경우 보고서 재생성을 최소화하기 위해 캐시 수명을 조정할 수 있습니다.

캐시 수명 값은 다음 저장소 노드의 `maxCacheAge` 속성으로 저장됩니다.

```
/apps/aem66-analyzer/content/modernizer/analyzer/jcr:content
```

이 속성의 값은 캐시 수명(초)입니다. 관리자는 CRX/DE Lite를 사용하여 캐시 수명을 조정할 수 있습니다.

## 컨텐츠 변환기 사용 {#using-content-transformer}

### 사용 가능 {#content-transformer-availability}

컨텐츠 변환기는 AEM 6.5 LTS Analyzer 와 번들로 제공되며 소프트웨어 배포 포털에서 zip 파일로 다운로드할 수 있습니다.

### 콘텐츠 변환기 사용에 대한 중요한 고려 사항 {#important-considerations-for-using-content-transformer}

콘텐츠 변환기(CT) 사용에 대한 중요한 고려 사항을 이해하려면 아래 섹션을 참조하십시오.

* 콘텐츠 변환기를 사용하려면 먼저 AEM 환경에서 AEM 분석기를 실행해야 합니다
* 프로덕션 환경에서 콘텐츠 변환기를 실행할 수 있지만 프로덕션 환경의 복제본에서 콘텐츠 변환기를 실행하는 것이 좋습니다. 더 중요한 것은 AEM 분석기와 CT가 동일한 환경에서 실행되는지 확인해야 한다는 것입니다
* 콘텐츠 변환기를 실행할 환경의 관리자여야 합니다
* 소스 콘텐츠를 변경할 수 있는 제거 작업은 기본적으로 변환 전에 `/etc/packages/modernizer-content-transformation` 아래에 소스 경로의 백업 패키지를 만듭니다. [제거 작업] 대화 상자에는 백업 패키지 생성을 비활성화/활성화하는 옵션이 있지만, 항상 패키지 생성 활성화를 선택하는 것이 좋습니다
* 콘텐츠 변환기의 각 페이지는 최대 50개의 검색 결과를 나열하도록 구성됩니다. 따라서 한 번에 최대 50개의 결과를 변환할 수 있습니다. 이 작업은 UI에서 적시에 응답을 제공하기 위해 수행됩니다.

### 콘텐츠 변환기 열기 {#opening-the-content-transformer}

1. 소스 AEM 인스턴스에 관리자로 로그인하고 *https://host:port/aem/start.htm*&#x200B;의 시작 페이지로 이동합니다.
1. **도구 - 작업 - 6.5 LTS 현대화 도구**(으)로 이동

   ![콘텐츠 변환기 열기](/help/sites-deploying/assets/opening-content-transformer-1.png)

1. **6.5 LTS 분석기 보고서에 대한 콘텐츠 변환기** 카드를 클릭합니다.

   ![콘텐츠 변환기 열기 2](/help/sites-deploying/assets/opening-content-transformer-2.png)

1. 분석기 보고서가 생성되지 않으면 **콘텐츠 변환** 페이지에 **보고서 없음**&#x200B;이 표시됩니다. 모든 콘텐츠 관련 결과를 제거한 경우에도 동일한 **보고서 없음** 메시지가 나타납니다

   ![콘텐츠 변환기 열기 3](/help/sites-deploying/assets/opening-content-transformer-3.png)

1. 다음은 AEM Analyzer 보고서 작성이 성공하고 콘텐츠 관련 문제가 발견된 경우 콘텐츠 변환기 개요 페이지가 어떻게 표시되는지에 대한 예입니다.

AEM Analyzer 보고서에 대한 만료 시간이 측면 레일에 표시됩니다. 콘텐츠 관련 결과가 누락되지 않도록 최신 AEM Analyzer 보고서로 콘텐츠 변환기 를 실행하는 것이 좋습니다

![콘텐츠 변환기 열기 4](/help/sites-deploying/assets/opening-content-transformer-4.png)

1. 패턴 코드, 하위 유형, 중요도 및 Source을 기반으로 문제를 필터링할 수 있습니다

   ![콘텐츠 변환기 열기 5](/help/sites-deploying/assets/opening-content-transformer-5.png)

### 경로 제거 {#removing-paths}

1. 모든 또는 특정 문제를 선택하고 **제거**&#x200B;를 선택하여 해결할 수 있습니다.

   ![경로 제거](/help/sites-deploying/assets/removing-paths-1.png)

   >[!NOTE]
   >제거 작업을 수행하면 기본적으로 변환 전에 `/etc/packages/modernizer-content-transformation` 아래에 원본 경로의 백업 패키지가 만들어집니다. [제거 작업] 대화 상자에는 백업 패키지 생성을 비활성화/활성화하는 옵션이 있지만, 항상 패키지 생성 활성화를 선택하는 것이 좋습니다.

   ![경로 제거](/help/sites-deploying/assets/removing-paths-2.png)

1. 경로의 제거 작업을 위해 만든 백업 패키지의 예가 아래에 나와 있습니다. **설치**&#x200B;를 클릭하여 원본 경로를 다시 가져올 수 있습니다.

   ![경로 제거](/help/sites-deploying/assets/removing-paths-3.png)

   >[!CAUTION]
   >
   >`/etc/packages/modernizer-content-transformation`은(는) 백업 패키지가 있는 위치이므로 삭제하지 마십시오. 더 이상 이러한 패키지가 필요하지 않은 경우에만 이 위치를 삭제하여 저장소 크기를 줄일 수 있습니다.

1. 선택적으로, 나중에 사용하기 위해 선택한 컨텐츠 검색 결과를 패키징할 수 있습니다. 이렇게 하려면 포함할 결과를 선택한 다음 왼쪽 상단에서 **패키지**&#x200B;를 클릭합니다. 패키지 이름을 입력하고 패키지 경로를 선택한 다음 **패키지** 단추를 클릭하여 프로세스를 완료합니다.

   ![경로 제거](/help/sites-deploying/assets/removing-paths-4.png)

### 알려진 문제 {#known-issues}

* 경우에 따라 제거 작업에서 알림이 표시될 수 있습니다. *&quot;일부 경로가 정상적으로 제거되지 않았습니다. 로그를 확인하고 다시 시도하십시오.*&quot;. 그러나 실제로 경로가 제거된 경우에는 이 메시지를 무시해도 됩니다
* 마찬가지로 원하는 작업을 수행하는 동안 오류 *(으)로 인해 패키지 작업이 실패할 수 있습니다. 로그를 확인하고 다시 시도하십시오.*&quot;. 세션 만료 때문일 수 있습니다. 이러한 경우 작업을 다시 시도하면 문제가 해결됩니다.





