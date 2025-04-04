---
title: 자산 번역 우수 사례
description: 다양한 번역된 버전을 동기화하고 번역 워크플로를 간소화하기 위한 에셋의 효율적인 관리를 위한 모범 사례입니다.
contentOwner: AG
role: Admin
feature: Asset Management
solution: Experience Manager, Experience Manager Assets
exl-id: 21771c11-ecce-4eff-be5b-f55835a5644e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# 자산 번역 우수 사례 {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets]은(는) 디지털 에셋의 바이너리, 메타데이터 및 태그를 여러 로케일로 번역하고 번역된 에셋을 관리하기 위한 다국어 워크플로우를 지원합니다. 자세한 내용은 [다국어 Assets](multilingual-assets.md)을 참조하세요.

다양한 번역된 버전이 계속 동기화되도록 에셋을 효율적으로 관리하려면 번역 워크플로를 실행하기 전에 에셋의 [언어 사본](preparing-assets-for-translation.md)을 만드십시오.

에셋 또는 에셋 그룹의 언어 사본은 유사한 콘텐츠 계층 구조를 갖는 언어 형제(또는 동급 언어의 에셋 버전)입니다.

각 언어 사본은 독립 자산입니다. 따라서 에셋을 여러 로케일로 변환하면 CRX 저장소의 크기가 크게 늘어날 수 있습니다. 예를 들어, 결합된 크기가 10GB인 에셋을 두 개의 언어로 번역하면 저장소 크기가 약 20GB(각 언어의 경우 10GB)까지 늘어날 수 있습니다.

에셋 바이너리는 메타데이터 및 태그에 비해 훨씬 더 큰 저장 공간을 차지합니다. 따라서 메타데이터와 태그를 번역하는 것이 목적만 제공하는 경우 을 생략하여 바이너리를 번역하십시오. 다른 로케일로 번역된 메타데이터 및 태그와 연결하기 위해 저장소의 바이너리 원본 복사본을 유지할 수 있습니다. 여러 번역된 버전이 아닌 단일 바이너리 사본을 유지 관리하여 저장소 크기에 대한 영향을 최소화합니다.

파일 데이터 저장소 및 Amazon S3 데이터 저장소는 이러한 시나리오에 가장 적합한 스토리지 인프라를 제공합니다. 이러한 저장소 저장소는 여러 로케일의 메타데이터 및 태그에 의해 공유할 수 있는 단일 자산 바이너리(렌디션 포함)를 저장합니다. 따라서 에셋 언어 사본을 만들고 메타데이터 및 태그를 번역하는 것은 저장소 크기에 영향을 주지 않습니다.

몇 가지 워크플로우 및 번역 통합 프레임워크에 대한 몇 가지 구성을 변경하여 프로세스를 더욱 간소화할 수도 있습니다.

1. 다음 중 하나를 수행하십시오.

   * [파일 데이터 저장소 설정](/help/sites-deploying/data-store-config.md)
   * [Amazon S3 데이터 저장소 설정](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. [!UICONTROL 마지막으로 수정한 날짜 설정] 워크플로우를 사용하도록 설정합니다.

   [!UICONTROL DAM 메타데이터 원본에 쓰기] 워크플로는 자산에 대해 마지막으로 수정된 날짜를 구성합니다. 2단계에서 이 워크플로를 사용하지 않도록 설정했으므로 [!DNL Assets]은(는) 마지막으로 수정한 에셋 날짜를 더 이상 최신 상태로 유지할 수 없습니다. 따라서 *마지막으로 수정한 날짜 설정* 워크플로우를 사용하여 마지막으로 수정한 자산이 최신 날짜인지 확인합니다. 오래된 마지막 수정 날짜가 있는 Assets으로 인해 오류가 발생할 수 있습니다.

1. 자산 바이너리 번역을 중지하려면 [번역 통합 프레임워크를 구성하십시오](/help/sites-administering/tc-tic.md). 에셋 바이너리 번역을 중지하려면 [!UICONTROL Assets] 탭에서 **[!UICONTROL Assets 번역]** 옵션을 선택 취소하십시오.
1. [다국어 자산 워크플로우](multilingual-assets.md)를 사용하여 자산 메타데이터/태그를 번역합니다.
