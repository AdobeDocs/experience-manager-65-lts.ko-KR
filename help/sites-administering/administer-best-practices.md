---
title: 관리자가 시작하고 실행하는 데 도움이 되는 모범 사례
description: 관리자가 시작하고 실행하는 데 도움이 되는 Adobe 엔지니어링 및 컨설팅 팀에서 컴파일한 모범 사례를 확인하십시오.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: 933ef22f-d023-44d2-8ec0-4bb47a46bba3
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 9%

---

# 모범 사례{#best-practices}

모범 사례에서는 가능한 가장 효율적이고 효과적인 방법으로 AEM을 개발, 관리 또는 사용하는 방법을 설명합니다. 이렇게 늘어나는 주제 목록에는 AEM의 다양한 영역이 포함되어 있습니다.

다음 영역에는 모범 사례와 관련된 설명서가 있습니다.

* [자산](#assets)
* [Sites](#sites)

작성, 배포, 유지 관리 또는 개발에 대한 우수 사례는 다음 중 하나를 참조하십시오.

* [작성 모범 사례](/help/sites-authoring/best-practices.md)
* [모범 사례 개발](/help/sites-developing/best-practices.md)
* [모범 사례 배포](/help/sites-deploying/best-practices.md)

특정 문서는 다음에 나오는 표에 설명되어 있고 연결됩니다.

## 자산 {#assets}

Dynamic Media 기능 및 Dynamic Media Classic 통합을 포함하여 Assets에 대한 우수 사례는 다음 항목에 설명되어 있습니다.

<table>
 <tbody>
  <tr>
   <td>로드 중 시스템 안정성과 성능을 개선하기 위한 Assets과 관련된 다양한 영역의 모범 사례입니다</td>
   <td><a href="/help/assets/best-practices-for-assets.md">에셋에 대한 우수 사례</a></td>
   <td>Assets과 관련된 다양한 영역의 모범 사례 안내서에 대한 링크를 포함합니다. 이를 검토한 후 엔터프라이즈 자산 관리 시스템을 구축하고 관리할 수 있는 지식과 도구를 갖추게 됩니다.</td>
  </tr>
  <tr>
   <td>콘텐츠 구성 방법(폴더 계층 구조)</td>
   <td><a href="/help/assets/organize-assets.md">파일 관리 우수 사례</a></td>
   <td>대부분의 처리 프로필은 비디오, 메타데이터, 이미지 처리가 항상 폴더에 적용되므로 폴더를 기반으로 합니다. 이 모범 사례 문서에서는 계층 구조가 콘텐츠 처리 방법에 중요한 영향을 미치므로 폴더 계층 구조를 정의하고 설정하는 방법에 대해 설명합니다. </td>
  </tr>
  <tr>
   <td>Scene7 및 AEM 통합</td>
   <td><a href="/help/sites-administering/scene7.md#best-practices-for-integrating-scene-with-aem">Scene7과 AEM 통합에 대한 우수 사례</a></td>
   <td><p>폴링 가져오기를 설정하는 시점, 통합을 테스트하는 방법, 콘텐츠 브라우저를 사용하여 Assets에 직접 업로드하는 시점에 대해 설명합니다.</p> </td>
  </tr>
  <tr>
   <td>이미지 사전 설정 옵션</td>
   <td><a href="/help/assets/managing-image-presets.md#understanding-image-presets">이미지 사전 설정</a> 및 <a href="/help/assets/managing-image-presets.md#image-preset-options">이미지 사전 설정 모범 사례</a> 이해</td>
   <td><a href="/help/assets/managing-image-presets.md">이미지 사전 설정 관리</a>에 대한 설명서의 일부로, 이 항목에서는 이미지 사전 설정이 무엇인지와 이미지 사전 설정 옵션 선택에 대한 모범 사례를 설명합니다.</td>
  </tr>
  <tr>
   <td>Dynamic Media 및 Scene7과의 직접 통합</td>
   <td><a href="/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media">Scene7/AEM 통합과 Dynamic Media</a></td>
   <td>Dynamic Media 솔루션을 사용하는 것이 가장 좋은 경우, S7을 AEM과 통합하는 경우 또는 둘 다 사용하는 경우에 대해 설명합니다.</td>
  </tr>
 </tbody>
</table>

## Sites {#sites}

웹 사이트 컨텐츠 관리 및 작성에는 다음과 같이 요약된 몇 가지 우수 사례가 있습니다.

<table>
 <tbody>
  <tr>
   <td>GDPR 준수</td>
   <td><a href="/help/sites-administering/gdpr-compliance-sites.md">AEM Sites GDPR 규정 준수</a></td>
   <td>데이터 개인정보 보호권에 관한 유럽 연합의 일반 데이터 보호 규정은 2018년 5월부터 시행됩니다. AEM Sites은 GDPR을 준수합니다. 이 페이지에서는 고객에게 AEM Sites에서 GDPR 요청을 처리하는 절차를 안내합니다. 저장된 개인 데이터의 위치와 수동으로 또는 코드로 해당 데이터를 제거하는 방법에 대해서도 설명합니다.</td>
  </tr>
  <tr>
   <td>인스턴스에 대한 기본 UI를 정의합니다.</td>
   <td><p><a href="/help/sites-authoring/select-ui.md#configuring-the-default-ui-for-your-instance">인스턴스에 대한 기본 UI 구성</a></p> </td>
   <td>AEM에는 터치에 적합한 UI와 클래식 UI가 있습니다. 이 섹션에서는 인스턴스에 대한 기본 UI를 정의하는 방법을 자세히 설명합니다.</td>
  </tr>
  <tr>
   <td>다중 사이트 관리</td>
   <td><a href="/help/sites-administering/msm-best-practices.md">MSM 모범 사례</a></td>
   <td>MSM을 사용하여 콘텐츠 배포를 자동화하는 우수 사례입니다. </td>
  </tr>
  <tr>
   <td>콘텐츠 번역</td>
   <td><a href="/help/sites-administering/tc-bp.md">번역 모범 사례</a></td>
   <td>다국어 사이트 계획 및 구현을 위한 모범 사례입니다.</td>
  </tr>
  <tr>
   <td>사용자 관리</td>
   <td><a href="/help/sites-administering/security.md#best-practices">권한 및 권한 모범 사례</a></td>
   <td>권한 및 권한을 사용하여 작업할 때의 모범 사례를 설명합니다 </td>
  </tr>
  <tr>
   <td>워크플로</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md#configuration">워크플로우 모범 사례 - 구성</a></td>
   <td>워크플로를 사용하면 Adobe Experience Manager(AEM) 활동을 자동화할 수 있으며 AEM 환경에서 발생하는 대량의 처리를 나타낼 수 있으므로 워크플로 구현을 신중하게 계획하고 구성하는 것이 좋습니다.</td>
  </tr>
 </tbody>
</table>
