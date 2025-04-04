---
title: Salesforce과 통합
description: Adobe Experience Manager(AEM)와 Salesforce 통합에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: 68003650-76d7-40b3-860b-70454c13211e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 3%

---

# Salesforce과 통합 {#integrating-with-salesforce}

Salesforce과 Adobe Experience Manager(AEM)를 통합하면 리드 관리 기능이 제공되고 Salesforce에서 즉시 제공하는 기존 기능을 사용합니다. Salesforce으로 가는 잠재 고객을 게시하고 Salesforce에서 직접 데이터에 액세스하는 구성 요소를 만들도록 AEM을 구성할 수 있습니다.

AEM과 Salesforce 간의 양방향 확장 가능한 통합을 통해 다음과 같은 이점을 얻을 수 있습니다.

* 조직은 고객 경험을 개선하기 위해 데이터를 완전히 사용하고 수정해야 합니다.
* 마케팅에서 영업 활동까지 참여.
* 조직은 Salesforce 데이터 저장소에서 데이터를 자동으로 전송하고 수신합니다.

이 문서에서는 다음 사항에 대해 설명합니다.

* Salesforce 클라우드 서비스 구성 방법(Salesforce과 통합하도록 AEM 구성).
* Client Context 및 Personalization에서 Salesforce 리드/연락처 정보를 사용하는 방법.
* Salesforce 워크플로 모델을 사용하여 AEM 사용자를 Salesforce의 리드로 게시하는 방법.
* Salesforce의 데이터를 표시하는 구성 요소를 만드는 방법

## Salesforce과 통합하도록 AEM 구성 {#configuring-aem-to-integrate-with-salesforce}

AEM과 Salesforce을 통합하도록 구성하려면 먼저 Salesforce에서 원격 액세스 애플리케이션을 구성합니다. 그런 다음 이 원격 액세스 애플리케이션을 가리키도록 Salesforce 클라우드 서비스를 구성합니다.

>[!NOTE]
>
>Salesforce에서 무료 개발자 계정을 만들 수 있습니다.

Salesforce과 통합하도록 AEM을 구성하려면 다음을 수행합니다.

>[!CAUTION]
>
>절차를 계속하기 전에 [Salesforce Force API](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=salesforce*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=2&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcom.adobe.cq.mcm.salesforce.content-1.0.4.zip) 통합 패키지를 설치하십시오. 패키지를 사용하여 작업하는 방법에 대한 자세한 내용은 [패키지를 사용하여 작업하는 방법](/help/sites-administering/package-manager.md#package-share) 페이지를 참조하십시오.

1. AEM에서 **클라우드 서비스**(으)로 이동합니다. 타사 서비스에서 **Salesforce**&#x200B;의 **지금 구성**&#x200B;을 클릭합니다.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. 구성을 만드십시오(예: **개발자**).

   >[!NOTE]
   >
   >새 구성이 새 페이지로 리디렉션됩니다. **http://localhost:4502/etc/cloudservices/salesforce/developer.html**. 이 값은 Salesforce에서 원격 액세스 응용 프로그램을 만드는 동안 콜백 URL에 지정해야 하는 값과 정확히 동일합니다. 이 값은 일치해야 합니다.

1. Salesforce 계정에 로그인합니다(또는 계정이 없는 경우 [https://developer.salesforce.com](https://developer.salesforce.com)에서 만드십시오).
1. Salesforce에서 **만들기** > **앱**(으)로 이동하여 **연결된 앱**(이전 Salesforce 버전에서는 워크플로가 **배포** > **원격 액세스**)입니다.
1. AEM과 Salesforce에 연결할 수 있도록 **새로 만들기**&#x200B;를 클릭합니다.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. **연결된 앱 이름**, **API 이름** 및 **연락처 전자 메일**&#x200B;을 입력하세요. **OAuth 설정 활성화** 확인란을 선택하고 **콜백 URL**&#x200B;을(를) 입력한 다음 OAuth 범위를 추가합니다(예: 전체 액세스). 콜백 URL은 다음과 비슷합니다. `http://localhost:4502/etc/cloudservices/salesforce/developer.html`

   구성과 일치하도록 서버 이름/포트 번호 및 페이지 이름을 변경합니다.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Salesforce 구성을 저장하려면 **저장**&#x200B;을 클릭하세요. Salesforce은 AEM 구성에 필요한 **소비자 키** 및 **소비자 암호**&#x200B;를 만듭니다.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >Salesforce의 원격 액세스 응용 프로그램이 활성화될 때까지 몇 분(최대 15분) 정도 기다립니다.

1. AEM에서 **클라우드 서비스**&#x200B;로 이동하고 이전에 만든 Salesforce 구성으로 이동합니다(예: **개발자**). **편집**&#x200B;을 클릭하고 salesforce.com에서 고객 키와 고객 암호를 입력하십시오.

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | 로그인 URL | Salesforce 인증 엔드포인트입니다. 이 값은 미리 채워져 있으며 대부분의 경우 사용됩니다. |
   |---|---|
   | 고객 키 | salesforce.com의 Remote Access 응용 프로그램 등록 페이지에서 가져온 값을 입력하십시오. |
   | 고객 비밀 | salesforce.com의 Remote Access 응용 프로그램 등록 페이지에서 가져온 값을 입력하십시오. |

1. 연결하려면 **Salesforce에 연결**&#x200B;을 클릭하십시오. Salesforce은 구성이 Salesforce에 연결할 수 있도록 허용합니다.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   AEM에서 성공적으로 연결되었음을 알려주는 확인 대화 상자가 열립니다.

1. 웹 사이트의 루트 페이지로 이동하여 **페이지 속성**&#x200B;을 클릭합니다. 그런 다음 **클라우드 서비스**&#x200B;를 선택하고 **Salesforce**&#x200B;을(를) 추가한 다음 올바른 구성을 선택합니다(예: **개발자**).

   ![chlimage_1-75](assets/chlimage_1-75.png)

   이제 워크플로우 모델을 사용하여 Salesforce으로 가는 리드를 게시하고 Salesforce의 데이터에 액세스하는 구성 요소를 만들 수 있습니다.

## AEM 사용자를 Salesforce 리드로 내보내기 {#exporting-aem-users-as-salesforce-leads}

AEM 사용자를 Salesforce 리드로 내보내려면 Salesforce으로 리드를 게시하도록 워크플로우를 구성합니다.

AEM 사용자를 Salesforce 리드로 내보내려면 다음을 수행하십시오.

1. 워크플로우 **Salesforce.com 내보내기**&#x200B;를 마우스 오른쪽 단추로 클릭하고 **시작**&#x200B;을 클릭하여 `http://localhost:4502/workflow`의 Salesforce 워크플로우로 이동합니다.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. 이 워크플로의 **페이로드**(으)로 잠재 고객으로 만들려는 AEM 사용자를 선택하십시오(홈 > 사용자). **givenName** 및 **familyName**&#x200B;과(와) 같은 정보가 포함되어 있으므로 사용자의 프로필 노드를 선택해야 합니다. 이러한 정보는 Salesforce 잠재 고객의 **FirstName** 및 **LastName** 필드에 매핑됩니다.

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >이 워크플로우를 시작하기 전에 AEM에 게시하기 전에 Salesforce의 리드 노드에 포함해야 하는 특정 필수 필드가 있습니다. **givenName**, **familyName**, **회사** 및 **전자 메일**&#x200B;입니다. AEM 사용자와 Salesforce 리드 간의 전체 매핑 목록을 보려면 [AEM 사용자와 Salesforce 리드 간의 매핑 구성](#mapping-configuration-between-aem-user-and-salesforce-lead)을 참조하십시오.

1. **확인**&#x200B;을 클릭합니다. 사용자 정보는 salesforce.com으로 내보내집니다. salesforce.com에서 확인할 수 있습니다.

   >[!NOTE]
   >
   >오류 로그는 잠재 고객 가져오기 여부를 보여 줍니다. 자세한 내용은 오류 로그를 확인하십시오.

### Salesforce.com 내보내기 워크플로우 구성 {#configuring-the-salesforce-com-export-workflow}

필요한 경우 Salesforce.com 내보내기 워크플로우를 구성하여 올바른 Salesforce.com 구성과 일치시키거나 기타 변경합니다.

Salesforce.com 내보내기 워크플로우를 구성하려면 다음 작업을 수행하십시오.

1. `http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.`(으)로 이동

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. Salesforce.com 내보내기 단계를 열고 **인수** 탭을 선택한 다음 올바른 구성을 선택하고 **확인**&#x200B;을 클릭합니다. 또한 워크플로우가 Salesforce에서 삭제된 리드를 다시 만들도록 하려면 확인란을 선택합니다.

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 변경 내용을 저장하려면 **저장**&#x200B;을 클릭하세요.

   ![chlimage_1-79](assets/chlimage_1-79.png)

### AEM 사용자와 Salesforce 리드 간의 매핑 구성 {#mapping-configuration-between-aem-user-and-salesforce-lead}

AEM 사용자와 Salesforce 잠재 고객 간의 현재 매핑 구성을 보거나 편집하려면 구성 관리자를 열고 `https://<hostname>:<port>/system/console/configMgr`Salesforce 잠재 고객 매핑 구성&#x200B;**을 검색합니다.**

1. **웹 콘솔**&#x200B;을 클릭하거나 `https://<hostname>:<port>/system/console/configMgr.`(으)로 직접 이동하여 구성 관리자를 엽니다.
1. **Salesforce 잠재 고객 매핑 구성**&#x200B;을 검색합니다.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. 필요에 따라 매핑을 변경합니다. 기본 매핑은 **aemUserAttribute=sfLeadAttribute** 패턴을 따릅니다. 변경 내용을 저장하려면 **저장**&#x200B;을 클릭하세요.

## Salesforce Client Context Store 구성 {#configuring-salesforce-client-context-store}

Salesforce Client Context Store에는 AEM 내에서 이미 사용할 수 있는 정보보다 현재 로그인한 사용자에 대한 추가 정보가 표시됩니다. 사용자의 Salesforce 연결에 따라 Salesforce에서 이 추가 정보를 가져옵니다.

이렇게 하려면 다음을 구성합니다.

1. Salesforce Connect 구성 요소를 통해 AEM 사용자를 Salesforce ID에 연결합니다.
1. 보려는 속성을 구성할 수 있도록 Salesforce 프로필 데이터를 클라이언트 컨텍스트 페이지에 추가합니다.
1. (선택 사항) Salesforce Client Context Store의 데이터를 사용하는 세그먼트를 만듭니다.

### AEM 사용자를 Salesforce ID와 연결 {#linking-an-aem-user-with-a-salesforce-id}

AEM 사용자를 클라이언트 컨텍스트에서 로드할 수 있도록 Salesforce ID에 매핑합니다. 실제 시나리오에서는 유효성 검사가 있는 알려진 사용자 데이터를 기반으로 연결합니다. 데모용으로 이 절차에서는 **Salesforce 연결** 구성 요소를 사용합니다.

1. AEM의 웹 사이트로 이동하여 로그인한 다음 사이드 킥에서 **Salesforce Connect** 구성 요소를 끌어서 놓습니다.

   >[!NOTE]
   >
   >**Salesforce Connect** 구성 요소를 사용할 수 없는 경우 **디자인** 보기로 이동한 다음 선택하여 **편집** 보기에서 사용할 수 있도록 합니다.

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   구성 요소를 페이지로 드래그하면 **Salesforce에 대한 링크=해제**&#x200B;가 표시됩니다.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >이 구성 요소는 데모용으로만 사용됩니다. 실제 시나리오의 경우 사용자를 리드와 연결/일치시키는 다른 프로세스가 있을 수 있습니다.

1. 페이지에서 구성 요소를 드래그한 후 구성 요소를 열어 구성합니다. 구성, 연락처 유형, Salesforce 잠재 고객 또는 연락처를 선택하고 **확인**&#x200B;을 클릭합니다.

   ![chlimage_1-82](assets/chlimage_1-82.png)

   AEM은 사용자를 Salesforce 연락처 또는 리드와 연결합니다.

   ![chlimage_1-83](assets/chlimage_1-83.png)

### Client Context에 Salesforce 데이터 추가 {#adding-salesforce-data-to-client-context}

Salesforce의 Client Context에서 사용자 데이터를 로드하여 개인화에 사용할 수 있습니다.

1. 확장하려는 클라이언트 컨텍스트를 열어 탐색합니다(예: `http://localhost:4502/etc/clientcontext/default/content.html.`).

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. **Salesforce 프로필 데이터** 구성 요소를 클라이언트 컨텍스트로 드래그합니다.

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. 구성 요소를 두 번 클릭하여 엽니다. **항목 추가**&#x200B;를 선택하고 드롭다운 목록에서 속성을 선택합니다. 속성을 원하는 만큼 추가하고 **확인**&#x200B;을 선택합니다.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. 이제 Salesforce의 Salesforce 관련 속성이 클라이언트 컨텍스트에 표시됩니다.

   ![chlimage_1-85](assets/chlimage_1-85.png)

### Salesforce Client Context Store의 데이터를 사용하여 세그먼트 작성 {#building-a-segment-using-data-from-salesforce-client-context-store}

Salesforce Client Context Store의 데이터를 사용하는 세그먼트를 작성할 수 있습니다. 이를 위해 진행되는 작업:

1. **도구** > **세그먼테이션** 또는 [http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation)&#x200B;(으)로 이동하여 AEM의 세그먼테이션으로 이동합니다.
1. Salesforce의 데이터를 포함하도록 세그먼트를 만들거나 업데이트합니다. 자세한 내용은 [세그먼테이션](/help/sites-administering/campaign-segmentation.md)을 참조하세요.

## 리드 검색 {#searching-leads}

AEM은 주어진 기준에 따라 Salesforce에서 잠재 고객을 검색하는 샘플 검색 구성 요소와 함께 제공됩니다. 이 구성 요소는 Salesforce REST API를 사용하여 Salesforce 개체를 검색하는 방법을 보여 줍니다. salesforce.com 호출을 트리거하려면 페이지를 Salesforce 구성과 연결합니다.

>[!NOTE]
>
>Salesforce REST API를 사용하여 Salesforce 개체를 쿼리하는 방법을 보여 주는 샘플 구성 요소입니다. 필요에 따라 더 복잡한 구성 요소를 만들려면 예를 들어 사용하십시오.

이 구성 요소를 사용하려면:

1. 이 구성을 사용할 페이지로 이동합니다. 페이지 속성을 열고 **클라우드 서비스를 선택합니다.** **서비스 추가**&#x200B;를 클릭하고 **Salesforce** 및 적절한 구성을 선택한 다음 **확인**&#x200B;을 클릭합니다.

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. Salesforce 검색 구성 요소를 페이지로 드래그합니다(활성화된 경우). 활성화하려면 디자인 모드로 이동하여 해당 영역에 추가합니다.

   ![chlimage_1-21](assets/chlimage_1-21.jpeg)

1. 검색 구성 요소를 열고 검색 매개 변수를 지정하고 **확인**&#x200B;을 클릭합니다.

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. AEM에는 지정된 기준과 일치하는 검색 구성 요소에 지정된 리드가 표시됩니다.

   ![chlimage_1-87](assets/chlimage_1-87.png)
