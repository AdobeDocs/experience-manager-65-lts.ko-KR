---
title: 자산 사용 및 공유에 대한 보고서
description: 디지털 자산의 사용, 활동 및 공유를 이해하는 데 도움이 되는  [!DNL Adobe Experience Manager Assets] 의 자산에 대한 보고서입니다.
contentOwner: AG
role: User, Admin
feature: Asset Reports,Asset Management
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 434a081a-f9e4-4a0d-8468-55b4ab5a6287
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 8%

---

# 자산 보고서 {#asset-reports}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/asset-reports.html?lang=ko) |
| AEM 6.5 | 이 문서 |

자산 보고를 통해 [!DNL Adobe Experience Manager Assets] 배포의 유틸리티를 평가할 수 있습니다. [!DNL Assets]을(를) 사용하면 디지털 자산에 대한 다양한 보고서를 생성할 수 있습니다. 보고서는 시스템의 사용, 사용자가 에셋과 상호 작용하는 방법, 다운로드 및 공유되는 에셋에 대한 유용한 정보를 제공합니다.

보고서의 정보를 사용하여 기업 내 및 고객에 의한 [!DNL Assets]의 채택률을 측정하기 위한 주요 성공 지표를 도출할 수 있습니다.

[!DNL Assets] 보고 프레임워크는 [!DNL Sling] 작업을 사용하여 순서대로 보고서 요청을 비동기적으로 처리합니다. 대형 저장소에 대해 확장 가능합니다. 비동기 보고서 처리를 통해 보고서가 생성되는 효율성과 속도가 향상됩니다.

보고서 관리 인터페이스는 직관적이고, 보관된 보고서에 액세스하고 보고서 실행 상태(성공, 실패 및 대기 중)를 보기 위한 세분화된 옵션 및 제어를 포함합니다.

보고서가 생성되면 전자 메일(선택 사항) 및 받은 편지함 알림을 통해 사용자에게 알립니다. 이전에 생성된 모든 보고서가 표시되는 보고서 목록 페이지에서 보고서를 보거나 다운로드하거나 삭제할 수 있습니다.

## 전제 조건 {#prerequisite-for-reporting}

보고서를 생성하려면 다음을 수행합니다.

* **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;에서 [!UICONTROL 일 CQ DAM 이벤트 레코더] 서비스를 사용하도록 설정하십시오.
* 보고할 활동 또는 이벤트를 선택합니다. 예를 들어 다운로드한 자산에 대한 보고서를 생성하려면 [!UICONTROL 다운로드한 자산(다운로드한 자산)]을 선택합니다.

![웹 콘솔에서 자산 보고 사용](assets/reports-config-day-cq-dam-event-recorder.png)

## 보고서 생성 {#generate-reports}

[!DNL Experience Manager Assets]은(는) 다음 표준 보고서를 생성합니다.

* 업로드
* 다운로드
* 만료
* 수정
* 게시
* [!DNL Brand Portal] 게시
* 디스크 사용량
* 파일
* 공유 링크

[!DNL Adobe Experience Manager] 관리자는 사용자의 구현을 위해 이러한 보고서를 쉽게 생성하고 사용자 지정할 수 있습니다. 관리자는 다음 단계에 따라 보고서를 생성할 수 있습니다.

1. [!DNL Experience Manager] 인터페이스에서 **[!UICONTROL 도구]** > **[!UICONTROL Assets]** > **[!UICONTROL 보고서]**&#x200B;를 클릭합니다.

   자산 보고서를 탐색할 ![도구 페이지](assets/AssetsReportNavigation.png)

1. [!UICONTROL 자산 보고서] 페이지의 도구 모음에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 보고서 만들기]** 페이지에서 만들려는 보고서를 선택하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   ![보고서 유형 선택](assets/choose_report.png)

   >[!NOTE]
   >
   >기본적으로 콘텐츠 조각 및 링크 공유는 자산 [!UICONTROL 다운로드] 보고서에 포함됩니다. 적절한 옵션을 선택하여 링크 공유 보고서를 만들거나 다운로드 보고서에서 콘텐츠 조각을 제외합니다.

   >[!NOTE]
   >
   >[!UICONTROL 다운로드] 보고서에는 개별적으로 선택한 후 다운로드하거나 빠른 작업을 사용하여 다운로드한 에셋에 대한 세부 정보만 표시됩니다. 단, 다운로드한 폴더 내에 있는 에셋의 세부 정보는 포함되지 않습니다.

1. 보고서가 저장된 CRX 저장소에서 제목, 설명, 썸네일 및 폴더 경로 등 보고서 세부 정보를 구성합니다. 기본적으로 폴더 경로는 `/content/dam`입니다. 다른 경로를 지정할 수 있습니다.

   ![보고서 세부 정보를 추가할 페이지](assets/report_configuration.png)

   보고서의 날짜 범위를 선택합니다.

   지금 또는 미래 날짜 및 시간에 보고서를 생성하도록 선택할 수 있습니다.

   >[!NOTE]
   >
   >보고서를 나중에 예약하도록 선택하는 경우 날짜 및 시간 필드에 날짜 및 시간을 지정해야 합니다. 값을 지정하지 않으면 보고서 엔진은 값을 즉시 생성할 보고서로 처리합니다.

   구성 필드는 사용자가 만드는 보고서 유형에 따라 다를 수 있습니다. 예를 들어, **[!UICONTROL 디스크 사용]** 보고서는 에셋에서 사용하는 디스크 공간을 계산할 때 에셋 변환을 포함하는 옵션을 제공합니다. 디스크 사용량 계산을 위해 하위 폴더에 자산을 포함하거나 제외하도록 선택할 수 있습니다.

   >[!NOTE]
   >
   >The **[!UICONTROL Disk Usage]** report does not include date range fields because it indicates current disk space usage only.

   ![디스크 사용량 보고서의 세부 정보 페이지](assets/disk_usage_configuration.png)

   **[!UICONTROL 파일]** 보고서를 만들 때 하위 폴더를 포함/제외할 수 있습니다. 그러나 이 보고서에 대한 에셋 렌디션은 포함할 수 없습니다.

   ![파일 보고서의 세부 정보 페이지](assets/files_report.png)

   **[!UICONTROL 링크 공유]** 보고서에 [!DNL Assets] 내에서 외부 사용자와 공유되는 자산의 URL이 표시됩니다. 여기에는 자산을 공유한 사용자의 이메일 ID, 자산을 공유받은 사용자의 이메일 ID, 공유 날짜, 그리고 링크의 만료 날짜가 포함됩니다. The columns are not customizable.

   **[!UICONTROL 링크 공유]** 보고서는 `/var/dam/share` 아래에 표시되는 공유 URL만 게시하므로 하위 폴더 및 변환에 대한 옵션을 포함하지 않습니다.

   ![링크 공유 보고서의 세부 정보 페이지](assets/link_share.png)

1. 도구 모음에서 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 열 구성]** 페이지에서 기본적으로 보고서에 표시할 일부 열이 선택되어 있습니다. 열을 더 선택할 수 있습니다. 보고서에서 제외할 열 선택을 취소합니다.

   ![보고서 열 선택 또는 취소](assets/configure_columns.png)

   사용자 지정 열 이름 또는 속성 경로를 표시하려면 CRX의 `jcr:content` 노드 아래에서 에셋 바이너리에 대한 속성을 구성하십시오. 또는 속성 경로 선택기를 통해 추가합니다.

   ![보고서 열 선택 또는 취소](assets/custom_columns.png)

1. 도구 모음에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 보고서 생성이 시작되었음을 알리는 메시지가 표시됩니다.
1. [!UICONTROL 자산 보고서] 페이지에서 보고서 생성 상태는 보고서 작업의 현재 상태(예: [!UICONTROL 성공], [!UICONTROL 실패], [!UICONTROL 큐에 있음] 또는 [!UICONTROL 예약됨])를 기반으로 합니다. 받은 편지함에도 동일한 상태가 나타납니다.보고서 페이지를 보려면 보고서 링크를 클릭하십시오. 또는 보고서를 선택하고 도구 모음에서 **[!UICONTROL 보기]**&#x200B;를 클릭합니다.

   <!--![A generated report](assets/report_page.png)-->
   [보고서 상태](assets/report-status.JPG)

   도구 모음에서 **[!UICONTROL 다운로드]**&#x200B;를 클릭하여 보고서를 CSV 형식으로 다운로드합니다.

## 사용자 정의 열 추가 {#add-custom-columns}

다음 보고서에 사용자 정의 열을 추가하여 사용자 정의 요구 사항에 더 많은 데이터를 표시할 수 있습니다.

* 업로드
* 다운로드
* 만료
* 수정
* 게시
* [!DNL Brand Portal] 게시
* 파일

이러한 보고서에 사용자 정의 열을 추가하려면 다음 단계를 수행합니다.

1. [!DNL Manager interface]에서 **[!UICONTROL 도구]** > **[!UICONTROL Assets]** > **[!UICONTROL 보고서]**&#x200B;를 클릭합니다.
1. [!UICONTROL 자산 보고서] 페이지의 도구 모음에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

1. **[!UICONTROL 보고서 만들기]** 페이지에서 만들려는 보고서를 선택하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 제목, 설명, 썸네일, 폴더 경로 및 날짜 범위 등 보고서 세부 사항을 적절히 구성합니다.

1. To display a custom column, specify the name of the column in under **[!UICONTROL Custom Columns]**.

   ![보고서의 사용자 지정 열 이름 지정](assets/custom_columns-1.png)

1. 속성 경로 선택기를 사용하여 CRXDE의 `jcr:content` 노드 아래에 속성 경로를 추가합니다. 또는 속성 경로 필드에 경로를 입력합니다.

   ![jcr:content의 경로에서 속성 경로 매핑](assets/property_picker.png)

   사용자 지정 열을 더 추가하려면 **[!UICONTROL 추가]**&#x200B;를 클릭하고 5단계와 6단계를 반복합니다.

1. 도구 모음에서 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 보고서 생성이 시작되었음을 알리는 메시지가 표시됩니다.

## 제거 서비스 구성 {#configure-purging-service}

더 이상 필요하지 않은 보고서를 제거하려면 웹 콘솔에서 DAM 보고서 제거 서비스를 구성하여 수량 및 기간에 따라 기존 보고서를 제거합니다.

1. `https://[aem_server]:[port]/system/console/configMgr`에서 웹 콘솔(구성 관리자)에 액세스합니다.
1. **[!UICONTROL DAM 보고서 제거 서비스]** 구성을 엽니다.
1. `scheduler.expression.name` 필드에 제거 서비스의 빈도(시간 간격)를 지정합니다. 보고서에 대한 기간 및 수량 임계값을 구성할 수도 있습니다.
1. 변경 사항을 저장합니다.

## 문제 해결 정보, 팁 및 제한 사항 {#best-practices-and-limitations}

* 보고서의 일부 보고서나 숫자를 사용할 수 없거나 예상대로 사용할 수 없는 경우 [!UICONTROL 일 CQ DAM 이벤트 레코더] 서비스가 활성화되어 있는지 확인하십시오.

* 더 이상 필요하지 않은 보고서를 제거합니다. DAM 보고서 제거 서비스의 구성 옵션을 사용하여 보고서 제거 기준을 구성합니다.

* 디스크 사용량 보고서가 생성되지 않고 [!DNL Dynamic Media]을(를) 사용 중인 경우 모든 자산이 올바르게 진행되는지 확인하십시오. 해결하려면 에셋을 재처리한 다음 보고서를 다시 생성합니다.
