---
title: ' [!DNL Adobe Workfront]과(와) [!DNL Experience Manager Assets] 통합'
description: ' [!DNL Assets] 과(와) [!DNL Workfront] 간의 통합 소개'
role: Admin,Leader,Architect
feature: Workfront Integrations and Apps
hide: true
solution: Experience Manager, Workfront
exl-id: 5181d278-2e6e-41f7-891e-1067a03de016
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 9%

---

# [!DNL Adobe Workfront]과(와) [!DNL Adobe Experience Manager Assets] 통합 {#assets-integration-overview}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=ko) |
| AEM 6.5 | 이 문서 |

[!DNL Adobe Workfront]은(는) 업무의 전체 라이프사이클을 한 곳에서 관리할 수 있도록 도와주는 작업 관리 애플리케이션입니다. [!DNL Workfront]과(와) [!DNL Adobe Experience Manager Assets] 간의 통합을 통해 조직은 작업과 디지털 에셋 관리를 본질적으로 연결하여 콘텐츠 속도와 마켓 출시 속도를 개선할 수 있습니다. Workfront에서 작업을 관리하는 맥락에서 사용자는 필요한 문서 및 이미지에 액세스할 수 있습니다.

[!DNL Workfront for Experience Manager enhanced connector]은(는) 통합 워크플로우를 통해 향상된 비즈니스 프로세스를 가능하게 하고 개인화된 통합 클라이언트 환경과 중앙 저장소를 제공합니다. Adobe은 표준 커넥터와 두 솔루션을 통합할 수 있는 향상된 커넥터를 제공합니다. 비교하려면 아래의 지원되는 기능을 확인하고 [새로운 기능 [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)을 확인하세요.

[!DNL Workfront for Experience Manage enhanced connector]을(를) 통해 조직은 다음을 수행할 수 있습니다.

* Workfront에서 연결된 Experience Manager 폴더를 자동으로 만들고 Workfront 포트폴리오, 프로그램 및 프로젝트를 기반으로 폴더를 구성합니다.
* Workfront 프로젝트 메타데이터를 연결된 Experience Manager 폴더와 동기화합니다.
* Experience Manager 메타데이터가 새 버전으로 업데이트됩니다.
* Experience Manager 워크플로우를 사용하여 구성 가능한 조건에 따라 Workfront 개체 상태를 설정합니다.
* Experience Manager 게시 환경 또는 Brand Portal에 자산을 게시합니다.

플랫폼 지원 및 향상된 커넥터에 대한 [필수 구성 요소](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)를 참조하세요.

>[!IMPORTANT]
>
>* Adobe에서는 인증된 파트너 또는 [!DNL Adobe Professional Services]을(를) 통해서만 [!DNL Adobe Workfront for Experience Manager enhanced connector]을(를) 배포하고 구성해야 합니다. 인증 파트너 또는 [!DNL Adobe Professional Services] 없이 배포 및 구성된 경우 Adobe에서 지원하지 않습니다.
>
>* Adobe은 이 커넥터를 중복 커넥터로 만드는 [!DNL Adobe Workfront] 및 [!DNL Adobe Experience Manager]에 대한 업데이트를 릴리스할 수 있습니다. 이러한 경우 고객은 이 커넥터를 사용하지 않도록 전환해야 할 수 있습니다.
>
>* Adobe은 향상된 커넥터 버전 1.7.4 이상을 지원합니다. 이전 프리릴리스 및 사용자 지정 버전은 지원되지 않습니다. 향상된 커넥터 버전을 확인하려면 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65-lts/administering/contentmanagement/package-manager.html?lang=en)의 왼쪽 창에서 사용할 수 있는 `digital.hoodoo` 그룹으로 이동하십시오.
>
>* [Workfront for Experience Manager Assets 강화 커넥터에 대한 파트너 인증 시험](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)을 참조하세요. 시험에 대한 자세한 내용은 [시험 가이드](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)를 참조하세요.

## [!DNL Assets]과(와) [!DNL Workfront] 간의 다른 통합 비교 {#feature-parity-matrix}

다음은 [!DNL Assets]과(와) [!DNL Workfront] 간의 다양한 통합 유형을 통해 사용할 수 있는 기능에 대한 세부 정보입니다.

| 기능 | 설명 | [!DNL Workfront] 및 [!DNL Assets Essentials] *커넥터 없음(기본 제공)* | [!DNL Workfront for Experience Manager enhanced connector] *커넥터 필요* | Workfront 및 [!DNL Experience Manager as a Cloud Service] *커넥터 없음(기본 제공)* |
|----|----|----|-----|-----|
| 배포 메서드 | 제공 항목 [!DNL Assets]에 적합합니다. | Assets Essentials | Adobe Managed Services, 온-프레미스 | Cloud Service |
| **일반** |
| [!DNL Workfront]에서 [!DNL Assets]&#x200B;(으)로 디지털 파일 보내기 | WF 문서의 최신 버전은 문서의 새 버전으로 연결된 AEM Assets에 업로드할 수 있습니다. | ✓ | ✓ | ✓ |
| AEM 폴더를 Workfront 개체에 수동으로 연결 | 기존 AEM 폴더는 Workfront 폴더로 연결되고 하위 자산은 새 Workfront 문서로 연결됩니다. | ✓ | ✓ | ✓ |
| Workfront 개체에 [!DNL Assets] 연결 | AEM의 기존 에셋을 새 Workfront 문서에 연결하거나 기존 문서의 새 버전으로 연결할 수 있습니다. | ✓ | ✓ | ✓ |
| 연결된 폴더에 추가된 Assets은 자동으로 AEM으로 전송됩니다 | 연결된 폴더에 문서가 추가되면 연결된 에셋이 자동으로 새 에셋으로 AEM Assets에 업로드됩니다. | ✓ | ✓ | ✓ |
| Workfront 내에서 연결된 AEM Assets 다운로드 | 에셋이 Workfront에 연결되면 에셋의 바이트를 다운로드할 수 있습니다. | ✓ | ✓ | ✓ |
| Workfront 내에서 AEM Assets 검색 | Workfront의 AEM Assets 선택기를 사용하여 에셋을 전체 텍스트 검색할 수 있습니다. | ✓ | ✓ | ✓ |
| Workfront 내에서 AEM 폴더 검색 | Workfront의 AEM Assets 선택기를 사용하여 폴더를 전체 텍스트 검색할 수 있습니다. | ✓ | ✓ | ✓ |
| Workfront 내에서 AEM 폴더 계층 구조 보기 및 탐색 | Workfront의 AEM Assets 선택기를 사용하면 로 제한된 AEM Assets 계층 구조를 검색할 수 있습니다.   AEM에 설정된 사용자와 관련된 액세스 제어 및 권한. | ✓ | ✓ | ✓ |
| AEM 타임라인에서 자산 버전 추적 | Workfront과 AEM 간 문서 버전 내역 유지 | ✓ | ✓ | ✓ |
| Workfront의 AEM Assets에서 Assets 연결 해제 | AEM에서 연결된 기존 에셋은 연결된 Workfront 문서에서 연결 해제할 수 있습니다. AEM 내의 원래 자산은 삭제되지 않습니다. | ✓ | ✓ | ✓ |
| Workfront에서 AEM Assets에 새 버전 에셋 추가 | Workfront의 문서에 새로 추가된 버전이 있으면 사용자는 새 버전을 AEM으로 보내 기존 버전을 바꿀 수 있습니다. | ✓ | ✓ | ✓ |
| Assets으로 직접 사용자 클릭 시 WorkfrontAEM 에 연결 | Workfront 내에서 연결된 에셋을 미리 볼 수 있도록 AEM으로 이동합니다. | ✓ | ✓ | 예정 |
| Workfront에서 연결된 AEM 폴더 자동 생성 | 프로젝트 상태를 사용하여 Workfront에서 연결된 AEM 폴더를 자동으로 만듭니다. Workfront 포트폴리오, 프로그램 및 프로젝트를 기반으로 AEM 폴더를 자동으로 구성합니다. | 아니요 | ✓ | 아니요 |
| Workfront에서 AEM 저장소로 직접 이동합니다 | 사용자가 Workfront 내에 구성된 사용 가능한 AEM 저장소로 이동할 수 있도록 허용합니다. | ✓ | 아니요 | ✓ |
| Workfront에서 연결된 AEM 폴더 만들기 | 문서 탭에서 사용할 수 있는 옵션을 사용하여 Workfront에서 연결된 AEM 폴더를 수동으로 만듭니다. | ✓ | 아니요 | ✓ |
| 댓글 동기화 중 | 자산에 대한 댓글을 [!DNL Workfront]에서 [!DNL Assets]&#x200B;(으)로 자동 동기화 | 아니요 | ✓ | 아니요 |
| 여러 Workfront 환경을 단일 AEM 환경에 연결 지원 | 여러 Workfront 환경의 사용자는 단일 AEM 환경에 연결할 수 있습니다. | ✓ | 아니요 | ✓ |
| 여러 AEM 환경을 단일 Workfront 환경에 연결 지원 | 단일 Workfront 환경 내의 사용자는 여러 AEM 환경 간에 에셋을 전송하거나 연결할 수 있습니다. | ✓ | ✓ | ✓ |
| **메타데이터** |
| Workfront 에셋 메타데이터를 AEM Assets에 매핑 | Workfront 오브젝트 및 사용자 정의 양식 속성을 AEM 에셋 메타데이터 속성에 매핑할 수 있습니다. 값은 초기 업로드/링크에서 푸시됩니다. | ✓ | ✓ | ✓ |
| Workfront에서 자동으로 문서 사용자 지정 Forms 만들기 | AEM 워크플로우를 사용하여 Workfront 문서, 작업 및 문제에 사용자 정의 양식을 첨부합니다. | 아니요 | ✓ | 아니요 |
| AEM Assets과 Workfront 간 메타데이터의 양방향 자동 업데이트 | AEM Assets과 Workfront 간에 메타데이터를 자동으로 업데이트합니다. 에셋은 처음에 Workfront에서 AEM으로 푸시해야 하며 양방향 메타데이터 업데이트가 제대로 작동하려면 Workfront 에셋 메타데이터를 AEM 에셋에 매핑해야 합니다. | 아니요 | ✓ | 아니요 |
| AEM에 매핑된 메타데이터에 대한 Workfront의 실시간 보기 | Workfront 문서 세부 정보 및 문서 요약 패널에서 AEM에 대해 업데이트된 매핑된 메타데이터를 봅니다. | ✓ | 아니요 | ✓ |
| 업데이트된 Workfront 메타데이터를 AEM으로 실시간 푸시 | 에셋 또는 에셋의 새 버전을 다시 푸시하지 않고 매핑된 Workfront 메타데이터를 AEM으로 자동으로 업데이트합니다. | ✓ | 아니요 | ✓ |
| Workfront 메타데이터를 AEM Assets 폴더에 매핑 | Workfront 프로젝트 메타데이터를 연결된 AEM 폴더와 동기화합니다. | 아니요 | ✓ | ✓ |
| 새 버전의 AEM 메타데이터 업데이트 | AEM의 구성을 통해 Workfront에서 새로 버전이 지정된 에셋이 해당 메타데이터에 대한 변경 사항을 푸시하는지 여부를 결정할 수 있습니다. | 아니요 | ✓ | 아니요 |
| Workfront에서 사용자 지정 AEM 변경 사항에 대한 Forms 메타데이터 자동 업데이트 | AEM을 사용하면 Workfront의 문서 양식에 대한 업데이트를 구독할 수 있습니다. 따라서 Workfront 문서 사용자 정의 양식 메타데이터에 대한 모든 업데이트는 매핑된 AEM 메타데이터 필드의 값을 편집합니다. | 아니요 | ✓ | 아니요 |
| **워크플로(기본 제공)** |
| 연결된 Assets에 새 증명 버전 만들기 | Workfront에서 자산을 연결할 때 증명을 자동으로 생성할 수 있습니다. | 아니요 | 사용자 정의 | 아니요 |
| Workfront 개체의 상태 설정 | AEM 워크플로를 사용하여 구성 가능한 조건에 따라 Workfront 개체 상태 설정 | 아니요 | ✓ | 예정 |
| Assets을 AEM 게시 환경 또는 Brand Portal에 게시 | Workfront 사용자에게 연결된 자산을 AEM 게시 환경 또는 Brand Portal에 자동으로 게시할 수 있는 옵션을 제공합니다. | 아니요 | ✓ | 예정 |
