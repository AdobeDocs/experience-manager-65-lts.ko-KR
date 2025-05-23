---
title: 모범 사례 배포
description: 가능한 가장 효율적이고 효과적인 방법으로 Adobe Experience Manager(AEM)를 배포하고 유지 관리하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 4f830ee9-e0e3-48df-b67d-709258cb1991
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 5%

---

# 모범 사례 배포{#deploying-best-practices}

배포 모범 사례에서는 가능한 가장 효율적이고 효과적인 방법으로 Adobe Experience Manager(AEM)를 배포하거나 유지 관리하는 방법을 설명합니다. 이렇게 점점 커지는 주제의 목록은 AEM의 다양한 영역을 포함합니다.

다음 영역에는 모범 사례 및 권장 사항의 배포 및 유지에 대한 설명서가 제공됩니다.

* [Oak](#oak)
* [UI](#ui)
* [성능](#performance)

관리, 개발 또는 작성에 대한 우수 사례는 다음 중 하나를 참조하십시오.

* [모범 사례 관리](/help/sites-administering/administer-best-practices.md)
* [모범 사례 개발](/help/sites-developing/best-practices.md)
* [작성 모범 사례](/help/sites-authoring/best-practices.md)

특정 문서는 다음에 나오는 표에 설명되어 있고 연결됩니다.

## Oak {#oak}

[Oak](/help/sites-deploying/platform.md)은(는) AEM의 기반이 되는 확장 가능하고 성능이 뛰어난 계층적 콘텐츠 저장소입니다.

<table>
 <tbody>
  <tr>
   <td><p>확장성, 성능 및 재해 복구</p> </td>
   <td><a href="/help/sites-deploying/performance.md">성능 및 확장성</a></td>
   <td>기술 민첩성, 고성능 및 건전한 재해 복구 기능에 대해 설명하는 백서를 제공합니다.</td>
  </tr>
  <tr>
   <td>권장 Oak 배포</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">권장 배포</a></td>
   <td>배포 시나리오에 대해 설명합니다</td>
  </tr>
  <tr>
   <td>Mongo 토폴로지</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Mongo 토폴로지 모범 사례</a></td>
   <td>mongo 토폴로지 - 사용할 토폴로지를 설명합니다.</td>
  </tr>
  <tr>
   <td>데이터 저장소 옵션</td>
   <td><a href="/help/sites-deploying/data-store-config.md">노드 및 데이터 저장소 구성</a></td>
   <td>이 문서에서는 이진 데이터 및 콘텐츠 노드 저장과 관련된 모범 사례에 대해 설명합니다. Amazon S3 데이터 저장소 사용에 대한 정보를 포함합니다.</td>
  </tr>
  <tr>
   <td>Oak에서 검색</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">쿼리 및 색인화 모범 사례</a><br /> </td>
   <td>콘텐츠를 색인화하는 방법에 대한 모범 사례를 설명합니다.</td>
  </tr>
 </tbody>
</table>

## UI {#ui}

AEM에는 현재 동일한 릴리스에 클래식 및 터치에 적합한 UI의 두 가지 UI가 있습니다. 따라서 고객은 프로젝트 구현 중에 사용할 항목을 결정해야 합니다. 이 문서는 올바른 선택을 찾는 데 도움을 주기 위한 것입니다.

## 성능 {#performance}

성능에 대한 우수 사례는 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td>품질 Assurance 우수 사례</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">품질 Assurance 우수 사례</a></td>
   <td><em>게시</em> 환경의 성능 테스트를 위해 테스트 개념을 정의하는 것과 관련된 문제에 대한 표준화된 개요입니다. 이는 주로 QA 엔지니어, 프로젝트 관리자 및 시스템 관리자가 관심을 가질 사항입니다.</td>
  </tr>
  <tr>
   <td>콘텐츠 전송 네트워크에 Dispatcher 사용</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ko#using-dispatcher-with-a-cdn">콘텐츠 전송 네트워크에 Dispatcher 사용</a></td>
   <td>Akamai Edge Delivery 또는 Amazon Cloud Front와 같은 CDN(컨텐츠 전달 네트워크)은 최종 사용자에게 가까운 위치에서 컨텐츠를 전달합니다.</td>
  </tr>
  <tr>
   <td>성능 최적화</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">성능 최적화</a></td>
   <td>핵심 문제는 웹 사이트가 방문자 요청에 응답하는 데 걸리는 시간입니다.</td>
  </tr>
  <tr>
   <td>성능 테스트</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">성능 테스트 우수 사례</a></td>
   <td>AEM 배포에서 성능 테스트를 실행하기 위한 모범 사례를 설명합니다.<br /> </td>
  </tr>
 </tbody>
</table>
