---
title: 감시 폴더 엔드포인트 구성
description: 감시 폴더 엔드포인트를 구성하는 방법에 대해 알아봅니다. 문서가 감시 폴더에 배치되면 구성된 서비스 작업이 호출되어 파일을 조작합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: ae001541-ae7f-42ce-8236-5fbb6ddb4c1f
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '7192'
ht-degree: 0%

---

# 감시 폴더 엔드포인트 구성 {#configuring-watched-folder-endpoints}

관리자는 사용자가 감시 폴더에 파일(예: PDF 파일)을 배치할 때 구성된 서비스 작업이 호출되어 파일을 조작할 수 있도록 *감시 폴더*&#x200B;라고 하는 네트워크 폴더를 구성할 수 있습니다. 이 서비스는 지정된 작업을 수행한 후 수정된 파일을 지정된 출력 폴더에 저장합니다.

## 감시 폴더 서비스 구성 {#configuring-the-watched-folder-service}

감시 폴더 엔드포인트를 구성하기 전에 감시 폴더 서비스를 구성하십시오. 감시 폴더 서비스의 구성 매개 변수에는 두 가지 목적이 있습니다.

* 모든 감시 폴더 엔드포인트에 대해 공통되는 속성을 구성하려면
* 모든 감시 폴더 끝점에 기본값을 제공하려면

감시 폴더 서비스를 구성한 후에는 대상 서비스에 대한 감시 폴더 엔드포인트를 추가합니다. 끝점을 추가할 때는 구성된 감시 폴더 서비스의 입력 폴더에 파일이나 폴더가 배치될 때 호출할 서비스 이름 및 작업 이름과 같은 값을 설정합니다. 감시 폴더 서비스 구성에 대한 자세한 내용은 [감시 폴더 서비스 설정](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings)을 참조하세요.

## 감시 폴더 만들기 {#creating-a-watched-folder}

다음 두 가지 방법으로 감시 폴더를 만들 수 있습니다.

* 감시 폴더 끝점에 대한 설정을 구성할 때는 다음 예와 같이 경로 상자에 상위 디렉터리의 전체 경로를 입력하고 만들 감시 폴더의 이름을 추가합니다.
  `  C:\MyPDFs\MyWatchedFolder`MyWatchedFolder 폴더가 아직 없으므로 AEM Forms에서 해당 위치에 폴더를 만들려고 시도합니다.

* 감시 폴더 끝점을 구성하기 전에 파일 시스템에 폴더를 만든 다음 경로 상자에 전체 경로를 입력합니다.

클러스터형 환경에서는 감시 폴더로 사용되는 폴더를 액세스, 쓰기 및 공유할 수 있어야 합니다. 이 시나리오에서는 클러스터의 각 애플리케이션 서버 인스턴스가 동일한 공유 폴더에 액세스할 수 있어야 합니다.

Windows에서 응용 프로그램 서버가 서비스로 실행 중인 경우 다음 방법 중 하나로 공유 폴더에 대한 적절한 액세스 권한으로 시작해야 합니다.

* 응용 프로그램 서버 서비스 **매개 변수로 로그온**&#x200B;을 구성하여 공유 감시 폴더에 적절한 액세스 권한을 가진 특정 사용자로 시작합니다.
* 서비스가 데스크톱과 상호 작용할 수 있도록 응용 프로그램 서버 서비스 로컬 시스템으로 시작 옵션을 구성합니다. 이 옵션을 사용하려면 공유 감시 폴더에 모든 사용자가 액세스하고 쓸 수 있어야 합니다.

## 감시 폴더 함께 체인 {#chaining-together-watched-folders}

감시 폴더는 하나의 감시 폴더의 결과 문서가 다음 감시 폴더의 입력 문서가 되도록 함께 체인화될 수 있습니다. 각 감시 폴더는 다른 서비스를 호출할 수 있습니다. 이러한 방식으로 감시 폴더를 구성함으로써, 복수의 서비스가 호출될 수 있다. 예를 들어 하나의 감시 폴더는 PDF 파일을 Adobe PostScript®로 변환할 수 있고 두 번째 감시 폴더는 PostScript 파일을 PDF/A 형식으로 변환할 수 있습니다. 이렇게 하려면 첫 번째 끝점에서 정의한 감시 폴더의 *result* 폴더를 두 번째 끝점에서 정의한 감시 폴더의 *input* 폴더를 가리키도록 설정하기만 하면 됩니다.

첫 번째 변환의 출력은 \path\result로 이동합니다. 두 번째 변환에 대한 입력은 \path\result이고 두 번째 변환의 출력은 \path\result\result(또는 두 번째 변환에 대해 결과 폴더 상자에 정의한 디렉토리)로 이동합니다.

## 사용자가 감시 폴더와 상호 작용하는 방법 {#how-users-interact-with-watched-folders}

감시 폴더 끝점의 경우 사용자는 데스크탑에서 감시 폴더로 입력 파일 또는 폴더를 복사하거나 드래그하여 를 호출할 수 있습니다. 파일은 도착하는 순서대로 처리됩니다.

감시 폴더 엔드포인트의 경우, 작업에 하나의 입력 파일만 필요한 경우 사용자는 해당 파일을 감시 폴더의 루트에 복사할 수 있습니다.

작업에 두 개 이상의 입력 파일이 포함되어 있는 경우 사용자는 감시 폴더 계층 구조 외부에 모든 필수 파일이 포함된 폴더를 만들어야 합니다. 이 새 폴더에는 입력 파일이 포함되어야 합니다(필요한 경우 프로세스에 DDX 파일 선택 사항). 작업 폴더가 생성되면 사용자는 이를 감시 폴더의 입력 폴더에 복사합니다.

>[!NOTE]
>
>응용 프로그램 서버가 감시 폴더의 파일에 대한 액세스 권한을 삭제했는지 확인합니다. 파일을 스캔한 후 AEM Forms에서 입력 폴더에서 파일을 삭제할 수 없는 경우 관련 프로세스가 무기한 호출됩니다.

## 감시 폴더 출력 {#watched-folder-output}

입력이 폴더이고 출력이 여러 파일로 구성된 경우 AEM Forms는 입력 폴더와 동일한 이름의 출력 폴더를 만들고 출력 파일을 해당 폴더에 복사합니다. 출력이 출력 프로세스의 출력처럼 키-값 쌍을 포함하는 문서 맵으로 구성된 경우 키는 출력 파일 이름으로 사용됩니다.

끝점 프로세스에서 발생한 출력 파일 이름에는 파일 확장명 앞에 문자, 숫자 및 마침표(.) 이외의 문자가 포함될 수 없습니다. AEM forms는 다른 문자를 16진수 값으로 변환합니다.

클라이언트 애플리케이션은 감시 폴더 결과 폴더에서 결과 문서를 선택합니다. 프로세스 오류는 감시 폴더 실패 폴더에 기록됩니다.

## 감시 폴더 작동 방식 {#how-watched-folder-works}

감시 폴더 모듈에는 다음 서비스가 포함됩니다.

* 감시 폴더 서비스
* provider.file_scan_service
* provider.file_write_results_service

위에 나열된 서비스 외에도 감시 폴더는 작업을 예약하기 위한 스케줄러 서비스 및 대상 서비스의 비동기 호출을 지원하는 작업 관리자 서비스를 포함한 다른 서비스에 종속됩니다.

### 감시 폴더가 호출 요청을 처리하는 방법 {#how-watched-folder-processes-an-invocation-request}

감시 폴더 서비스는 끝점의 생성, 업데이트 및 삭제를 처리합니다. 관리자가 끝점을 만든 후 지정된 반복 간격 또는 cron 표현식을 기반으로 스케줄러 서비스에 의해 트리거되도록 예약됩니다.

이 다이어그램은 감시 폴더가 호출 요청을 처리하는 방법을 보여 줍니다.

![en_watchedfolder](assets/en_watchedfolder.png)

감시 폴더를 사용하여 서비스를 호출하는 프로세스는 다음과 같습니다.

1. 클라이언트 애플리케이션은 감시 폴더 입력 폴더에 파일 또는 폴더를 배치합니다.
1. 작업 스캔 간격이 발생하면 스케줄러 서비스는 provider.file_scan_service 를 호출하여 입력 폴더의 파일 또는 폴더를 처리합니다.
1. provider.file_scan_service는 다음 작업을 수행합니다.


   * 입력 폴더에서 포함 파일 패턴과 일치하는 파일 또는 폴더를 검색하고 지정된 제외 파일 패턴에 대해 파일 또는 폴더를 제외합니다. 가장 오래된 파일이나 폴더를 먼저 선택합니다. 대기 시간보다 오래된 파일과 폴더도 선택됩니다. 한 번의 스캔에서 처리되는 파일 또는 폴더의 수는 배치 크기를 기반으로 합니다. 파일 패턴에 대한 자세한 내용은 [파일 패턴 정보](configuring-watched-folder-endpoints.md#about-file-patterns)를 참조하십시오. 일괄 처리 크기 설정에 대한 자세한 내용은 [감시 폴더 서비스 설정](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings)을 참조하세요.
   * 처리할 파일 또는 폴더를 선택합니다. 파일 또는 폴더가 완전히 다운로드되지 않은 경우 다음 스캔에서 선택됩니다. 폴더가 완전히 다운로드되도록 하려면 관리자는 제외 파일 패턴을 사용하여 이름으로 폴더를 만들어야 합니다. 폴더에 모든 파일이 있으면 포함 파일 패턴에 지정된 패턴으로 이름을 변경해야 합니다. 이 단계에서는 서비스 호출에 필요한 모든 파일이 폴더에 있는지 확인합니다. 폴더가 완전히 다운로드되도록 하는 방법에 대한 자세한 내용은 [감시 폴더에 대한 팁과 요령](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders)을 참조하세요.
   * 처리할 파일 또는 폴더를 선택한 후 스테이지 폴더로 이동합니다.
   * 끝점 입력 매개 변수 매핑을 기반으로 스테이지 폴더의 파일 또는 폴더를 적절한 입력으로 변환합니다. 입력 매개 변수 매핑의 예를 보려면 [감시 폴더에 대한 팁과 트릭](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders)을 참조하십시오.


1. 끝점에 대해 구성된 대상 서비스는 동기적으로 또는 비동기적으로 호출됩니다. 끝점에 대해 구성된 사용자 이름과 암호를 사용하여 대상 서비스가 호출됩니다.

   * 동기 호출은 Target 서비스를 직접 호출하고 응답을 즉시 처리합니다.
   * 비동기 호출의 경우 Job Manager 서비스를 통해 Target 서비스가 호출되며, 이 서비스는 요청을 큐에 배치합니다. Job Manager 서비스는 provider.file_write_results_service 를 호출하여 결과를 처리합니다.

1. provider.file_write_results_service는 대상 서비스 호출의 응답 또는 실패를 처리합니다. 성공하면 끝점 구성에 따라 결과가 결과 폴더에 저장됩니다. 성공적으로 완료되면 끝점이 결과를 유지하도록 구성된 경우 provider.file_write_results_service도 소스를 유지합니다.

   대상 서비스를 호출하여 오류가 발생하면 provider.file_write_results_service는 실패 이유를 failure.log 파일에 기록하고 해당 파일을 failure 폴더에 배치합니다. 실패 폴더는 끝점에 대해 지정된 구성 매개 변수를 기반으로 만들어집니다. 관리자가 엔드포인트 구성에 대해 실패 시 유지 옵션을 설정하면 provider.file_write_results_service도 소스 파일을 실패 폴더에 복사합니다. 실패 폴더에서 파일을 복구하는 방법에 대한 자세한 내용은 [실패 지점 및 복구](configuring-watched-folder-endpoints.md#failure-points-and-recovery)를 참조하십시오.


## 감시 폴더 끝점 설정 {#watched-folder-endpoint-settings}

다음 설정을 사용하여 감시 폴더 엔드포인트를 구성합니다.

**이름:**(필수) 끝점을 식별합니다. Workspace에 표시된 이름이 잘리므로 &lt; 문자를 포함하지 마십시오. 끝점의 이름으로 URL을 입력하는 경우 RFC1738에 지정된 구문 규칙을 준수하는지 확인하십시오.

**설명:** 끝점에 대한 설명입니다. Workspace에 표시된 설명이 잘리므로 &lt; 문자를 포함하지 마십시오.

**경로:**(필수) 감시 폴더 위치를 지정합니다. 클러스터된 환경에서 이 설정은 클러스터의 모든 컴퓨터에서 액세스할 수 있는 공유 네트워크 폴더를 가리켜야 합니다.

**비동기:** 호출 형식을 비동기 또는 동기화로 식별합니다. 기본값은 비동기입니다. 비동기식은 수명이 긴 프로세스에 대해 권장되는 반면, 동기식은 수명이 짧은 프로세스에 대해 권장됩니다.

**크론 식:** 크론 식을 사용하여 감시 폴더를 예약해야 하는 경우 크론 식을 입력하십시오. 이 설정이 구성되면 반복 간격이 무시됩니다.

**반복 간격:** 감시 폴더에서 입력을 검색하는 간격(초)입니다. 스로틀 설정을 사용하지 않으면 반복 간격이 평균 작업을 처리하는 시간보다 길어야 합니다. 그렇지 않으면 시스템이 오버로드될 수 있습니다. 기본값은 5입니다. 자세한 내용은 배치 크기 설명을 참조하십시오.

**반복 횟수:** 감시 폴더가 폴더 또는 디렉터리를 검사한 횟수입니다. -1 값은 무한 스캔을 나타냅니다. 기본값은 -1입니다.

**스로틀:** 이 옵션을 선택하면 AEM에서 지정된 시간에 처리하는 감시 폴더 작업 수가 제한됩니다. 최대 작업 수는 [일괄 처리 크기] 값에 의해 결정됩니다. 제한 정보를 참조하십시오.

**사용자 이름:**(필수) 감시 폴더에서 대상 서비스를 호출할 때 사용되는 사용자 이름입니다. 기본값은 Superadmin입니다.

**도메인 이름:**(필수) 사용자의 도메인입니다. 기본값은 DefaultDom입니다.

**일괄 처리 크기:** 검사당 선택할 파일 또는 폴더 수입니다. 시스템의 오버로드를 방지하기 위해 사용합니다. 한 번에 너무 많은 파일을 스캔하면 충돌이 발생할 수 있습니다. 기본값은 2입니다.

[반복 간격] 및 [배치 크기] 설정은 모든 스캔에서 감시 폴더가 선택하는 파일 수를 결정합니다. 감시 폴더는 석영 스레드 풀을 사용하여 입력 폴더를 스캔합니다. 스레드 풀이 다른 서비스와 공유됩니다. 스캔 간격이 작으면 스레드에서 종종 입력 폴더를 스캔합니다. 감시 폴더에 파일이 자주 드롭되는 경우 스캔 간격을 작게 유지해야 합니다. 파일을 자주 삭제하지 않는 경우 다른 서비스가 스레드를 사용할 수 있도록 스캔 간격을 크게 사용합니다.

삭제할 파일이 많은 경우 배치 크기를 크게 만듭니다. 예를 들어, 감시 폴더 끝점에 의해 호출된 서비스가 분당 700개의 파일을 처리할 수 있고 사용자가 동일한 비율로 입력 폴더에 파일을 놓는 경우 배치 크기를 350으로 설정하고 반복 간격을 30초로 설정하면 감시 폴더를 너무 자주 검색하는 비용을 발생시키지 않고도 감시 폴더 성능에 도움이 됩니다.

파일을 감시 폴더에 놓으면 입력에 있는 파일이 표시되므로 매 초마다 스캔이 발생하는 경우 성능이 저하될 수 있습니다. 스캔 간격을 늘리면 성능이 향상될 수 있습니다. 삭제할 파일의 볼륨이 작은 경우 배치 크기 및 반복 간격을 적절하게 조정합니다. 예를 들어 1초마다 10개의 파일을 삭제하는 경우 [반복 간격]을 1초로 설정하고 [배치 크기]를 10초로 설정해 보십시오.

**대기 시간:** 폴더 또는 파일을 만든 후 스캔하기 전에 대기하는 시간(밀리초)입니다. 예를 들어 대기 시간이 3,600,000밀리초(1시간)이고 1분 전에 파일을 만든 경우 59분 이상 경과하면 이 파일이 선택됩니다. 기본값은 0입니다.

이 설정은 파일이나 폴더가 입력 폴더에 완전히 복사되도록 하는 데 유용합니다. 예를 들어 처리할 대형 파일이 있고 파일을 다운로드하는 데 10분이 걸리는 경우 대기 시간을 10&ast;60 &ast;1000밀리초로 설정합니다. 이렇게 하면 감시 폴더가 10분이 되지 않은 경우 파일을 검색하지 못합니다.

**파일 패턴 제외:** 감시 폴더에서 검색하고 가져올 파일과 폴더를 결정하는 데 사용하는 세미콜론 **;**&#x200B;으로 구분된 패턴 목록입니다. 이 패턴의 파일 또는 폴더는 처리를 위해 검사되지 않습니다.

이 설정은 입력이 여러 파일이 있는 폴더인 경우 유용합니다. 폴더의 콘텐츠를 감시 폴더가 선택할 이름으로 폴더에 복사할 수 있습니다. 이렇게 하면 폴더가 입력 폴더로 완전히 복사되기 전에 감시 폴더가 처리할 폴더를 선택하지 못합니다.

파일 패턴을 사용하여 다음을 제외할 수 있습니다.

* 특정 파일 이름 확장자를 가진 파일(예: &ast;.dat, &ast;.xml, &ast;.pdf)
* 특정 이름을 가진 파일(예: 데이터).&ast;에서는 *data1*, *data2* 등의 파일과 폴더를 제외합니다.
* 다음 예제와 같이 이름과 확장명에 복합 표현식이 있는 파일

   * Data[0-9][0-9][0-9].[d][aA]&#39;포트&#39;
   * &ast;.[d][Aa]&#39;포트&#39;
   * &ast;.[Xx][Mm][Ll]

파일 패턴에 대한 자세한 내용은 [파일 패턴 정보](configuring-watched-folder-endpoints.md#about-file-patterns)를 참조하십시오.

**파일 패턴 포함:**(필수) 세미콜론 **;** 검색 및 가져올 폴더와 파일을 결정하는 데 감시 폴더가 사용하는 패턴의 구분된 목록입니다. 예를 들어, [파일 패턴 포함]이 input&ast;이면 input&ast;와 일치하는 모든 파일과 폴더가 선택됩니다. 여기에는 input1, input2 등으로 명명된 파일 및 폴더가 포함됩니다.

기본값은 &ast;이며 모든 파일과 폴더를 나타냅니다.

파일 패턴을 사용하여 다음을 포함할 수 있습니다.

* 특정 파일 이름 확장자를 가진 파일(예: &ast;.dat, &ast;.xml, &ast;.pdf)
* 특정 이름을 가진 파일(예: 데이터).&ast;에는 *data1*, *data2* 등의 파일 및 폴더가 포함됩니다.
* 다음 예제와 같이 이름과 확장명에 복합 표현식이 있는 파일

   * Data[0-9][0-9][0-9].[d][aA]&#39;포트&#39;
   * &ast;.[d][Aa]&#39;포트&#39;
   * &ast;.[Xx][Mm][Ll]

파일 패턴에 대한 자세한 내용은 [파일 패턴 정보](configuring-watched-folder-endpoints.md#about-file-patterns)를 참조하십시오.


**결과 폴더:** 저장된 결과가 저장된 폴더입니다. 결과가 이 폴더에 표시되지 않으면 실패 폴더를 확인하십시오. 읽기 전용 파일은 처리되지 않으며 실패 폴더에 저장됩니다. 이 값은 다음 파일 패턴을 사용하는 절대 또는 상대 경로일 수 있습니다.

* %F = 파일 이름 접두사
* %E = 파일 이름 확장명
* %Y = 연도(전체)
* %y = 연도(마지막 두 자리)
* %M = 월
* %D = 일
* %d = 일(연 기준)
* %H = 시간(24시간 시계)
* %h = 시간(12시간 시계)
* %m = 분
* %s = 초
* %l = 밀리초
* %R = 난수(0-9 사이)
* %P = 프로세스 또는 작업 ID

예를 들어, 2009년 7월 17일 오후 8시이고 `C:/Test/WF0/failure/%Y/%M/%D/%H/`을(를) 지정한 경우 결과 폴더는 `C:/Test/WF0/failure/2009/07/17/20`입니다.

경로가 절대적이 아니라 상대적이면 감시 폴더 내에 폴더가 생성됩니다. 기본값은 감시 폴더 내의 결과 폴더인 result/%Y/%M/%D/입니다. 파일 패턴에 대한 자세한 내용은 [파일 패턴 정보](configuring-watched-folder-endpoints.md#about-file-patterns)를 참조하십시오.

>[!NOTE]
>
>결과 폴더의 크기가 작을수록 감시 폴더 성능이 향상됩니다. 예를 들어 감시 폴더의 예상 로드가 매시간마다 1,000개의 파일인 경우 매시간마다 새 하위 폴더가 만들어지도록 `result/%Y%M%D%H`과(와) 같은 패턴을 시도하십시오. 부하가 더 작은 경우(예: 하루에 1000개의 파일) `result/%Y%M%D`과 같은 패턴을 사용할 수 있습니다.

**폴더 유지:** 검사 및 픽업 후 파일이 저장되는 위치입니다. 경로는 절대, 상대 또는 null 디렉터리 경로일 수 있습니다. 결과 폴더에 설명된 대로 파일 패턴을 사용할 수 있습니다. 기본값은 preserve/%Y/%M/%D/입니다.

**실패 폴더:** 실패 파일이 저장된 폴더입니다. 이 위치는 항상 감시 폴더를 기준으로 합니다. 결과 폴더에 설명된 대로 파일 패턴을 사용할 수 있습니다.

읽기 전용 파일은 처리되지 않으며 실패 폴더에 저장됩니다.

기본값은 failure/%Y/%M/%D/입니다.

**실패 시 유지:** 서비스에서 작업을 실행하지 못한 경우 입력 파일을 유지합니다. 기본값은 true입니다.

**중복 파일 이름 덮어쓰기:** True로 설정하면 결과 폴더의 파일을 덮어쓰고 폴더를 유지합니다. False로 설정하면 이름에 숫자 인덱스 접미사가 있는 파일과 폴더가 사용됩니다. 기본값은 False입니다.

**제거 기간:**(필수) 결과 폴더의 파일과 폴더가 이 값보다 오래되면 제거됩니다. 이 값은 일 단위로 측정됩니다. 이 설정은 결과 폴더가 꽉 차지 않도록 하는 데 유용합니다.

-1일 값은 결과 폴더를 삭제하지 않음을 나타냅니다. 기본값은 -1입니다.

**작업 이름:**(필수) 감시 폴더 끝점에 할당할 수 있는 작업 목록입니다.

**입력 매개 변수 매핑:** 서비스 및 작업을 처리하는 데 필요한 입력을 구성하는 데 사용됩니다. 사용 가능한 설정은 감시 폴더 끝점을 사용 중인 서비스에 따라 다릅니다. 다음은 두 가지 유형의 입력입니다.

**리터럴:** 감시 폴더는 표시되는 대로 필드에 입력한 값을 사용합니다. 모든 기본 Java 유형이 지원됩니다. 예를 들어 API에서 String, long, int 및 Boolean과 같은 입력을 사용하는 경우 문자열이 적절한 유형으로 변환되고 서비스가 호출됩니다.

**변수:** 입력한 값은 감시 폴더에서 입력을 선택하는 데 사용하는 파일 패턴입니다. 예를 들어 암호 암호화 서비스가 있는 경우, 입력 문서가 PDF 파일이어야 하면 사용자는 &ast;.pdf를 파일 패턴으로 사용할 수 있습니다. 감시 폴더는 이 패턴과 일치하는 감시 폴더의 모든 파일을 선택하고 각 파일에 대한 서비스를 호출합니다. 변수를 사용하면 모든 입력 파일이 문서로 변환됩니다. Document를 입력 유형으로 사용하는 API만 지원됩니다.

**출력 매개 변수 매핑:** 서비스 및 작업의 출력을 구성하는 데 사용됩니다. 사용 가능한 설정은 감시 폴더 끝점을 사용 중인 서비스에 따라 다릅니다.

감시 폴더 출력은 단일 문서, 문서 목록 또는 문서 맵일 수 있습니다. 그런 다음 이러한 출력 문서는 출력 매개 변수 매핑에 지정된 패턴을 사용하여 결과 폴더에 저장됩니다.

>[!NOTE]
>
>고유한 출력 파일 이름을 생성하는 이름을 지정하면 성능이 향상됩니다. 예를 들어 서비스가 하나의 출력 문서를 반환하고 출력 매개 변수 매핑이 이 이 문서를 `%F.%E`(입력 파일의 파일 이름 및 확장명)에 매핑하는 경우를 생각해 보십시오. 이 경우 사용자가 매 분마다 같은 이름의 파일을 삭제하고 결과 폴더가 `result/%Y/%M/%D`(으)로 구성된 경우 [파일 이름 중복 덮어쓰기] 설정이 해제되어 있으면 [감시 폴더]에서 중복 파일 이름을 확인하려고 시도합니다. 중복 파일 이름을 확인하는 프로세스는 성능에 영향을 줄 수 있습니다. 이 경우 출력 매개 변수 매핑을 `%F_%h_%m_%s_%l`(으)로 변경하여 이름에 시간, 분, 초 및 밀리초를 추가하거나 삭제된 파일에 고유한 이름이 있는지 확인하면 성능이 향상될 수 있습니다.

## 파일 패턴 정보 {#about-file-patterns}

관리자는 서비스를 호출할 수 있는 파일 유형을 지정할 수 있습니다. 각 감시 폴더에 대해 여러 파일 패턴을 설정할 수 있습니다. 파일 패턴은 다음 파일 속성 중 하나일 수 있습니다.

* 특정 파일 이름 확장명을 가진 파일. 예: &ast;.dat, &ast;.xml, &ast;.pdf
* 특정 이름을 가진 파일. 예: 데이터.&ast;
* 다음 예제와 같이 이름과 확장명에 복합 표현식이 있는 파일

   * Data[0-9][0-9][0-9].[d][aA]&#39;포트&#39;
   * &ast;.[d][Aa]&#39;포트&#39;
   * &ast;.[Xx][Mm][Ll]

관리자는 결과를 저장할 출력 폴더의 파일 패턴을 정의할 수 있습니다. 출력 폴더(결과, 유지 및 실패)에 대해 관리자는 다음 파일 패턴 중 하나를 지정할 수 있습니다.

* %Y = 연도(전체)
* %y = 연도(마지막 두 자리)
* %M = 월,
* %D = 날짜,
* %d = 일(한 해 기준),
* %h = 시간,
* %m = 분,
* %s = 초,
* %R = 0-9 사이의 난수
* %J = 작업 이름

예를 들어 결과 폴더의 경로는 `C:\Adobe\Adobe_Experience_Manager_forms\BarcodedForms\%y\%m\%d`일 수 있습니다.

출력 매개 변수 매핑은 다음과 같은 추가 패턴을 지정할 수도 있습니다.

* %F = Source 파일 이름
* %E = Source 파일 이름 확장명

출력 매개 변수 매핑 패턴이 &quot;File.separator&quot;(경로 구분 기호)로 끝나면 폴더가 생성되고 콘텐츠가 해당 폴더에 복사됩니다. 패턴이 &quot;File.separator&quot;로 끝나지 않으면 컨텐츠(결과 파일 또는 폴더)가 해당 이름으로 만들어집니다. 출력 매개 변수 매핑에 대한 자세한 내용은 [감시 폴더의 팁 및 요령](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders)을 참조하세요.

## 조절 기본 정보 {#about-throttling}

감시 폴더 끝점에 대해 제한이 활성화되면 지정된 시간에 처리할 수 있는 감시 폴더 작업 수가 제한됩니다. 최대 작업 수는 [배치 크기] 값에 의해 결정되며, [감시 폴더] 엔드포인트에서 구성할 수도 있습니다. 제한 한도에 도달하면 감시 폴더의 입력 디렉터리에 있는 수신 문서가 폴링되지 않습니다. 다른 감시 폴더 작업이 완료되고 다른 폴링 시도가 수행될 때까지 문서가 입력 디렉터리에 유지됩니다. 동기 처리가 있는 경우, 작업이 단일 스레드에서 연속적으로 처리되더라도 단일 폴링에서 처리된 모든 작업은 제한 한도에 포함됩니다.

>[!NOTE]
>
>조절은 클러스터로 조절되지 않습니다. 제한이 활성화된 경우 클러스터는 지정된 시간에 일괄 처리 크기에 지정된 작업 수 이상을 처리하지 않습니다. 이 제한은 클러스터 전체에 적용되며 클러스터의 각 노드에만 국한되지 않습니다. 예를 들어 일괄 처리 크기가 2인 경우, 단일 노드가 두 개의 작업을 처리하면 제한 제한에 도달할 수 있으며, 다른 노드는 작업 중 하나가 완료될 때까지 입력 디렉토리를 폴링하지 않습니다.

### 조절 작동 방식 {#how-throttling-works}

감시 폴더는 각 반복 간격마다 입력 폴더를 스캔하고 배치 크기에 지정된 파일 수를 선택한 다음 각 파일에 대해 대상 서비스를 호출합니다. 예를 들어 일괄 처리 크기가 4인 경우 스캔할 때마다 감시 폴더는 4개의 파일을 선택하고 4개의 호출 요청을 만들고 대상 서비스를 호출합니다. 이러한 요청이 완료되기 전에 감시 폴더가 호출되면 이전 4개의 작업이 완료되었는지 여부에 관계없이 4개의 작업이 다시 시작됩니다.

조절은 이전 작업이 완료되지 않은 경우 감시 폴더가 새 작업을 호출하지 못하도록 합니다. 감시 폴더는 진행 중인 작업을 감지하고 일괄 처리 크기에서 진행 중인 작업을 뺀 새 작업을 처리합니다. 예를 들어 두 번째 호출에서 완료된 작업 수가 3개뿐이고 한 작업이 아직 진행 중인 경우 감시 폴더는 3개의 작업만 더 호출합니다.

* 감시 폴더는 스테이지 폴더에 있는 파일 수에 따라 얼마나 많은 작업이 진행 중인지 확인합니다. 단계 폴더에서 파일이 처리되지 않은 상태로 유지되면 감시 폴더에서 더 이상 작업을 호출하지 않습니다. 예를 들어 일괄 처리 크기가 4이고 세 개의 작업이 정지된 경우 감시 폴더는 후속 호출에서 한 작업만 호출합니다. 스테이지 폴더에서 파일이 처리되지 않은 상태로 유지될 수 있는 시나리오가 여러 가지가 있습니다. 작업이 정지되면 관리자는 Forms Workflow 관리 페이지에서 프로세스를 종료하여 감시 폴더가 파일을 스테이지 폴더 밖으로 이동하도록 할 수 있습니다.
* [감시 폴더]에서 작업을 호출하기 전에 Forms 서버가 다운되면 관리자는 단계 폴더에서 파일을 이동할 수 있습니다. 자세한 내용은 [실패 지점 및 복구](configuring-watched-folder-endpoints.md#failure-points-and-recovery)를 참조하십시오.
* Forms 서버가 실행 중이지만 Job Manager 서비스가 다시 호출될 때 감시 폴더가 실행되지 않는 경우(서비스가 순서가 지정된 시퀀스에서 시작되지 않을 때 발생) 관리자는 스테이지 폴더 밖으로 파일을 이동할 수 있습니다. 자세한 내용은 [실패 지점 및 복구](configuring-watched-folder-endpoints.md#failure-points-and-recovery)를 참조하십시오.


## 성능 및 확장성 {#performance-and-scalability}

감시 폴더는 하나의 노드에서 총 100개의 폴더를 제공할 수 있습니다. 감시 폴더의 성능은 Forms 서버의 성능에 따라 다릅니다. 비동기 호출의 경우 성능은 시스템 로드와 작업 관리자 큐에 있는 작업에 더 의존합니다.

클러스터에 노드를 추가하여 감시 폴더 성능을 향상시킬 수 있습니다. 감시 폴더 작업은 Quartz 스케줄러를 통해 클러스터 노드에 분산되며, 비동기 요청이 있는 경우 Job Manager 서비스를 통해 분산됩니다. 모든 작업은 데이터베이스에서 유지됩니다.

감시 폴더는 스케줄러 서비스에 따라 작업을 예약하고, 예약을 취소하며, 일정을 조정합니다. 예약 서비스 스레드 풀을 공유하는 이벤트 관리 서비스, 사용자 관리자 서비스 및 이메일 공급자 서비스와 같은 다른 서비스를 사용할 수 있습니다. 이는 감시 폴더 성능에 영향을 줄 수 있습니다. 모든 서비스가 스케줄러 서비스 스레드 풀 사용을 시작할 때 스케줄러 서비스 스레드 풀 조정이 필요합니다.

## 클러스터의 감시 폴더 {#watched-folders-in-a-cluster}

클러스터에서 감시 폴더는 Quartz 스케줄러 및 작업 관리자 서비스에 따라 로드 밸런싱 및 장애 조치를 수행합니다. Quartz 클러스터 동작에 대한 자세한 내용은 [Quartz 설명서](https://www.quartz-scheduler.org/documentation)를 참조하십시오.

감시 폴더는 각 폴링에서 다음 세 가지 주요 작업을 수행합니다.

* 폴더 검색
* 대상 서비스 호출
* 결과 처리

로드 밸런싱 및 장애 조치 동작은 감시 폴더가 동기 또는 비동기 호출을 위해 구성되었는지 여부에 따라 변경됩니다.

### 클러스터의 동기 감시 폴더 {#synchronous-watched-folder-in-a-cluster}

동기 호출의 경우 Quartz 로드 밸런서는 폴링 이벤트를 가져올 노드를 결정합니다. 폴링 이벤트를 받는 노드는 모든 작업(폴더 스캔, 대상 서비스 호출 및 결과 처리)을 수행합니다.

![en_synchwatchedfoldercluster](assets/en_synchwatchedfoldercluster.png)

동기 호출의 경우 한 노드가 실패하면 Quartz 스케줄러가 새 폴링 이벤트를 다른 노드로 전송합니다. 실패한 노드에서 시작된 호출이 손실됩니다. 실패한 작업과 관련된 파일을 복구하는 방법에 대한 자세한 내용은 [실패 지점 및 복구](configuring-watched-folder-endpoints.md#failure-points-and-recovery)를 참조하십시오.


### 클러스터의 비동기 감시 폴더 {#asynchronous-watched-folder-in-a-cluster}

비동기 호출의 경우 Quartz 로드 밸런서가 폴링 이벤트를 가져올 노드를 결정합니다. 폴링 이벤트를 받는 노드는 입력 폴더를 스캔하고 Job Manager 서비스 큐에 요청을 배치하여 대상 서비스를 호출합니다. 작업 관리자 서비스 로드 밸런서는 호출 요청을 처리할 노드를 결정합니다. 노드 A가 호출 요청을 만들었지만, 노드 B는 결국 요청을 처리하는 것으로 끝날 가능성이 있다. 또는 호출 요청을 시작한 노드는 또한 요청을 처리하는 것으로 끝날 수 있다.

![en_asynchwatchedfoldercluster](assets/en_asynchwatchedfoldercluster.png)

비동기 호출의 경우 한 노드가 실패하면 Quartz 스케줄러가 새 폴링 이벤트를 다른 노드로 보냅니다. 실패한 노드에서 생성된 호출 요청은 Job Manager 서비스 큐에 있으며 처리를 위해 다른 노드로 전송됩니다. 호출 요청이 만들어지지 않은 파일은 스테이지 폴더에 남아 있습니다. 실패한 작업과 관련된 파일을 복구하는 방법에 대한 자세한 내용은 [실패 지점 및 복구](configuring-watched-folder-endpoints.md#failure-points-and-recovery)를 참조하십시오.


## 장애 지점 및 복구 {#failure-points-and-recovery}

각 폴 이벤트에서 감시 폴더는 입력 폴더를 잠그고 포함 파일 패턴과 일치하는 파일을 스테이지 폴더로 이동한 다음 입력 폴더의 잠금을 해제합니다. 두 스레드가 동일한 파일 세트를 선택하여 두 번 처리하지 않도록 잠가야 합니다. 작은 반복 간격과 큰 배치 크기로 이 문제가 발생할 가능성이 높아집니다. 파일을 스테이지 폴더로 이동한 후 다른 스레드에서 폴더를 검색할 수 있도록 입력 폴더의 잠금이 해제됩니다. 이 단계는 한 스레드가 파일을 처리하는 동안 다른 스레드가 검색할 수 있으므로 처리량이 높습니다.

파일을 스테이지 폴더로 이동한 후 각 파일에 대해 호출 요청이 생성되고 대상 서비스가 호출됩니다. 감시 폴더가 스테이지 폴더의 파일을 복구할 수 없는 경우가 있을 수 있습니다.

* [감시 폴더]에서 호출 요청을 만들기 전에 서버가 다운되는 경우 스테이지 폴더의 파일이 스테이지 폴더에 남아 있으며 복구되지 않습니다.
* 감시 폴더가 스테이지 폴더의 각 파일에 대한 호출 요청을 성공적으로 만들었으며 서버가 충돌하는 경우 호출 유형에 따라 두 가지 동작이 있습니다.

**동기:** 감시 폴더가 서비스를 동기적으로 호출하도록 구성된 경우 단계 폴더의 모든 파일이 단계 폴더에서 처리되지 않은 상태로 유지됩니다.

**비동기:** 이 경우 감시 폴더는 작업 관리자 서비스를 사용합니다. Job Manager 서비스가 감시 폴더를 다시 호출하면 호출 결과에 따라 스테이지 폴더의 파일이 유지 또는 실패 폴더로 이동됩니다. 작업 관리자 서비스가 다시 감시 폴더를 호출하지 않으면 파일이 스테이지 폴더에서 처리되지 않은 상태로 유지됩니다. 이 상황은 작업 관리자가 다시 호출할 때 감시 폴더가 실행되고 있지 않을 때 발생합니다.

### 스테이지 폴더에서 처리되지 않은 소스 파일 복구 {#recovering-unprocessed-source-files-in-the-stage-folder}

감시 폴더가 스테이지 폴더의 소스 파일을 처리할 수 없는 경우 처리되지 않은 파일을 복구할 수 있습니다.

1. 응용 프로그램 서버 또는 노드를 다시 시작합니다.
1. (선택 사항) 감시 폴더에서 새 입력 파일을 처리하지 않습니다. 이 단계를 건너뛸 경우 스테이지 폴더에서 처리되지 않은 파일을 확인하는 것이 훨씬 어렵습니다. 감시 폴더가 새 입력 파일을 처리하지 못하도록 하려면 다음 작업 중 하나를 수행합니다.

   * 응용 프로그램 및 서비스에서 감시 폴더 끝점에 대한 Include File Pattern 매개 변수를 새 입력 파일과 일치하지 않는 매개 변수로 변경합니다(예: `NOMATCH` 입력).
   * 새 입력 파일을 만드는 프로세스를 일시 중단합니다.

   AEM Forms가 모든 파일을 복구하고 처리할 때까지 기다립니다. 대부분의 파일은 복구해야하고 새로운 입력 파일은 올바르게 처리해야합니다. 감시 폴더가 파일을 복구하고 처리할 때까지 기다리는 시간은 호출할 작업의 길이와 복구할 파일의 수에 따라 달라집니다.

1. 처리할 수 없는 파일을 확인합니다. 적절한 시간을 기다린 후 이전 단계를 완료했지만 스테이지 폴더에 처리되지 않은 파일이 남아 있는 경우 다음 단계로 이동합니다.

   >[!NOTE]
   >
   >스테이지 디렉터리에서 파일의 날짜 및 타임스탬프를 확인할 수 있습니다. 파일 수와 일반 처리 시간에 따라 중단 상태로 간주할 만큼 오래된 파일을 확인할 수 있습니다.

1. 처리되지 않은 파일을 스테이지 디렉토리에서 입력 디렉토리로 복사합니다.
1. 2단계에서 감시 폴더가 새 입력 파일을 처리하지 못하게 한 경우 포함 파일 패턴을 이전 값으로 변경하거나 비활성화한 프로세스를 다시 활성화하십시오.

## 감시 폴더의 보안 고려 사항 {#security-considerations-for-watched-folders}

각 감시 폴더는 사용자 이름과 암호로 구성됩니다. 이러한 자격 증명은 서비스를 호출할 때 사용됩니다. 감시 폴더는 감시 폴더의 소유자만 공유 폴더에 액세스할 수 있도록 공유 폴더가 기본 보안 파일 시스템으로 보호된다는 사실에 의존합니다.

## 감시 폴더에 대한 팁 및 요령 {#tips-and-tricks-for-watched-folders}

다음은 감시 폴더 엔드포인트를 구성할 때의 몇 가지 팁과 요령입니다.

* Windows에서 이미지 파일을 처리하는 감시 폴더가 있는 경우 감시 폴더에 의해 Windows 자동 생성된 Thumbs.db 파일이 폴링되지 않도록 하려면 [파일 패턴 포함] 또는 [파일 패턴 제외] 옵션에 대한 값을 지정합니다.
* cron 표현식을 지정하면 반복 간격이 무시됩니다. cron 표현식 사용은 Quartz 오픈 소스 작업 스케줄링 시스템, 버전 1.4.0을 기반으로 합니다.
* 배치 크기는 감시 폴더의 각 스캔에서 선택할 파일 또는 폴더 수입니다. 배치 크기를 2로 설정하고 감시 폴더 입력 폴더에 파일 또는 폴더를 10개 놓으면 각 스캔에서 2개만 선택됩니다. 반복 간격에 지정된 시간 후에 발생하는 다음 스캔에서는 다음 두 파일이 선택됩니다.
* 파일 패턴의 경우 관리자는 와일드카드 패턴을 추가로 지원하는 정규식을 지정하여 파일 패턴을 지정할 수 있습니다. 감시 폴더는 &ast;와 같은 와일드카드 패턴을 지원하도록 정규 표현식을 수정합니다.&ast; 또는 &ast;.pdf 이러한 와일드카드 패턴은 정규 표현식에서 지원되지 않습니다.
* 감시 폴더는 입력 폴더에서 입력을 검색하고 소스 파일 또는 폴더가 입력 폴더로 완전히 복사되었는지 여부를 알지 못한 후에 파일 또는 폴더의 처리를 시작합니다. 파일이나 폴더를 선택하기 전에 소스 파일이나 폴더가 감시 폴더의 입력 폴더로 완전히 복사되도록 하려면 다음 작업을 수행합니다.

   * 대기 시간(밀리초)을 사용합니다. 이 시간은 감시 폴더가 마지막 수정 시간부터 대기하는 시간입니다. 처리할 대형 파일이 있는 경우 이 기능을 사용합니다. 예를 들어 파일을 다운로드하는 데 10분이 걸리는 경우 대기 시간을 10&ast;60 &ast;1000 밀리초로 지정합니다. 이렇게 하면 감시 폴더가 10분까지 오래되지 않은 경우 파일을 선택할 수 없습니다.
   * 파일 패턴 제외 및 파일 패턴 포함 을 사용합니다. 예를 들어 파일 제외 패턴이 `ex*`이고 포함 파일 패턴이 `in*`인 경우 감시 폴더는 &quot;in&quot;으로 시작하는 파일을 선택하고 &quot;ex&quot;로 시작하는 파일은 선택하지 않습니다. 큰 파일이나 폴더를 복사하려면 먼저 이름이 &quot;ex&quot;로 시작하도록 파일이나 폴더의 이름을 변경합니다. 이름이 &quot;ex&quot;인 파일 또는 폴더가 감시 폴더로 완전히 복사되면 이름을 &quot;in&ast;&quot;로 바꿉니다.

* 제거 기간을 사용하여 결과 폴더를 깔끔하게 유지합니다. 감시 폴더는 삭제 지속 시간에 언급된 지속 시간보다 오래된 모든 파일을 지웁니다. 기간은 일 단위입니다.
* 감시 폴더 엔드포인트를 추가할 때 작업 이름을 선택한 후 입력 매개 변수 매핑이 채워집니다. 연산의 각 입력에 대해, 하나의 입력 파라미터 맵핑 필드가 생성된다. 다음은 입력 매개 변수 매핑의 예입니다.

   * `com.adobe.idp.Document` 입력의 경우: 서비스 작업에 `Document` 유형의 입력이 있는 경우 관리자는 매핑 유형을 `Variable`(으)로 지정할 수 있습니다. 감시 폴더는 입력 매개변수에 지정된 파일 패턴을 기반으로 감시 폴더의 입력 폴더에서 입력을 선택합니다. 관리자가 `*.pdf`을(를) 매개 변수로 지정하면 확장명이 .pdf인 각 파일이 선택되어 `com.adobe.idp.Document`(으)로 변환되고 서비스가 호출됩니다.
   * `java.util.Map` 입력의 경우: 서비스 작업에 `Map` 유형의 입력이 있는 경우 관리자는 매핑 유형을 `Variable`(으)로 지정하고 `*.pdf` 같은 패턴의 매핑 값을 입력할 수 있습니다. 예를 들어 서비스에는 입력 폴더에 있는 1.pdf 및 2.pdf와 같은 두 파일을 나타내는 두 개의 `com.adobe.idp.Document` 개체에 대한 맵이 필요합니다. 감시 폴더는 키를 파일 이름으로 사용하고 값을 `com.adobe.idp.Document`(으)로 하는 맵을 만듭니다.
   * `java.util.List` 입력의 경우: 서비스 작업에 List 유형의 입력이 있는 경우 관리자는 매핑 유형을 `Variable`(으)로 지정하고 `*.pdf` 같은 패턴의 매핑 값을 입력할 수 있습니다. PDF 파일을 입력 폴더에 놓으면 감시 폴더가 이러한 파일을 나타내는 `com.adobe.idp.Document` 개체 목록을 만들고 대상 서비스를 호출합니다.
   * `java.lang.String`의 경우: 관리자에게 두 가지 옵션이 있습니다. 먼저 관리자가 매핑 유형을 `Literal`(으)로 지정하고 매핑 값을 문자열로 입력할 수 있습니다. 예를 들어 `hello.` 감시 폴더가 문자열 `hello`로 서비스를 호출합니다. 둘째, 관리자가 매핑 유형을 `Variable`(으)로 지정하고 `*.txt`과(와) 같은 패턴의 매핑 값을 입력할 수 있습니다. 후자의 경우 확장명이 .txt인 파일은 서비스를 호출하는 문자열로 강제 적용된 문서로 읽혀집니다.
   * Java 기본 유형: 관리자는 매핑 유형을 `Literal`(으)로 지정하고 값을 제공할 수 있습니다. 감시 폴더는 지정된 값으로 서비스를 호출합니다.

* 감시 폴더는 문서 작업을 하기 위한 것입니다. 지원되는 출력은 `com.adobe.idp.Document`, `org.w3c.Document`, `org.w3c.Node`이며 이러한 유형의 목록 및 맵입니다. 다른 모든 유형은 실패 폴더에 실패 출력을 생성합니다.
* 결과가 결과 폴더에 없는 경우 실패 폴더를 확인하여 실패가 발생했는지 확인합니다.
* 감시 폴더는 비동기 모드에서 사용되는 경우 가장 잘 작동합니다. 이 모드에서 감시 폴더는 호출 요청을 대기열에 배치하고 다시 호출합니다. 그런 다음 큐가 비동기적으로 처리됩니다. 비동기 옵션이 설정되지 않은 경우 감시 폴더는 대상 서비스를 동기적으로 호출하고 프로세스 엔진은 서비스가 요청으로 완료되고 결과가 생성될 때까지 대기합니다. 대상 서비스가 요청을 처리하는 데 시간이 오래 걸리는 경우 감시 폴더에 시간 초과 오류가 발생할 수 있습니다.
* 가져오기 및 내보내기 작업에 대한 감시 폴더를 만들 때 파일 이름 확장자를 추상화할 수 없습니다. 감시 폴더를 사용하여 양식 데이터 통합 서비스를 호출할 때 출력 파일의 파일 이름 확장자 유형이 문서 개체 유형에 대해 의도한 출력 형식과 일치하지 않을 수 있습니다. 예를 들어 내보내기 작업을 호출하는 감시 폴더에 대한 입력 파일이 데이터가 포함된 XFA 양식인 경우 출력은 XDP 데이터 파일이어야 합니다. 올바른 파일 이름 확장명을 가진 출력 파일을 가져오려면 출력 매개 변수 매핑에서 해당 파일을 지정할 수 있습니다. 이 예제에서는 출력 매개 변수 매핑에 %F.xdp를 사용할 수 있습니다.
* 감시 폴더는 입력 파일이 폴더에 완전히 복사되기 전에 처리할 수 있습니다. Windows에서와 마찬가지로 UNIX에서는 파일 잠금이 필수가 아닙니다. 이러한 이유로 파일을 감시 폴더에 복사할 때 감시 폴더는 파일 복사가 완료될 때까지 기다리지 않고 파일을 스테이징으로 이동할 수 있습니다. 이 동작으로 인해 입력 파일의 일부만 처리됩니다. 현재 두 가지 해결 방법이 있습니다.

   * 해결 방법 1

      1. temp&ast;.ps와 같이 파일 제외 패턴 패턴을 지정합니다.
      1. temp로 시작하는 파일(예: temp1.ps)을 감시 폴더에 복사합니다.
      1. 파일을 감시 폴더에 완전히 복사한 후 파일 패턴 포함에 지정된 패턴과 일치하도록 파일의 이름을 변경합니다. 그런 다음 감시 폴더가 완료된 파일을 스테이지로 이동합니다.

   * 해결 방법 2

     파일을 감시 폴더로 복사하는 데 소요되는 최대 시간을 알고 있는 경우 대기 시간(초)을 지정합니다. 그런 다음 감시 폴더는 파일을 스테이지로 이동하기 전에 지정된 시간을 기다립니다.

     Windows에서는 한 스레드가 쓰기할 때 파일을 잠그므로 Windows의 파일에 대해서는 문제가 되지 않습니다. 그러나 Windows의 폴더에서는 문제가 됩니다. 폴더의 경우 해결 방법 1의 단계를 따라야 합니다.

* 감시 폴더에 대한 폴더 이름 유지 끝점 특성이 null 디렉터리 경로로 설정된 경우, 준비 디렉터리는 원래대로 정리되지 않습니다. 디렉터리에는 처리된 파일과 임시 폴더가 여전히 있습니다.

## 감시 폴더에 대한 서비스별 권장 사항 {#service-specific-recommendations-for-watched-folders}

모든 서비스에 대해 감시 폴더가 새 파일 및 폴더를 선택하여 처리하는 속도가 AEM Forms 서버에서 처리할 수 있는 작업 속도를 초과하지 않도록 감시 폴더의 배치 크기 및 반복 간격을 조정해야 합니다. 사용할 실제 매개 변수는 구성된 감시 폴더 수, 감시 폴더를 사용 중인 서비스 및 프로세서의 작업 집약도에 따라 달라질 수 있습니다.

### PDF 서비스 권장 사항 생성 {#generate-pdf-service-recommendations}

* PDF 생성 서비스는 Microsoft Word, Microsoft Excel, Microsoft PowerPoint, Microsoft Project, AutoCAD, Adobe Photoshop®, Adobe FrameMaker® 및 Adobe PageMaker® 파일 유형에 대해 한 번에 하나의 파일만 변환할 수 있습니다. 장기 실행 작업이므로 배치 크기를 낮은 설정으로 유지해야 합니다. 또한 클러스터에 노드가 더 있는 경우 반복 간격을 늘립니다.
* PostScript(PS), 캡슐화된 PostScript(EPS) 및 이미지 파일 유형의 경우 PDF 생성 서비스에서 여러 파일을 동시에 처리할 수 있습니다. 서버 용량과 클러스터의 노드 수에 따라 세션 Bean 풀 크기(동시에 수행되는 전환 수를 제어함)를 신중하게 조정해야 합니다. 그런 다음 변환하려는 파일 형식의 세션 빈 풀 크기와 같은 숫자로 배치 크기를 늘립니다. 폴링 빈도는 클러스터의 노드 수로 지정해야 합니다. 그러나 PDF 생성 서비스는 이러한 유형의 작업을 매우 빠르게 처리하므로 반복 간격을 5 또는 10과 같은 낮은 값으로 구성할 수 있습니다.
* PDF 생성 서비스는 한 번에 하나의 OpenOffice 파일만 변환할 수 있지만 변환 속도는 매우 빠릅니다. PS, EPS 및 이미지 전환에 대한 위의 논리는 OpenOffice 전환에도 적용됩니다.
* 클러스터에서 균일한 로드 분배를 활성화하려면 배치 크기를 낮게 유지하고 반복 간격을 늘립니다.

### 바코드 양식 서비스 권장 사항 {#barcoded-forms-service-recommendations}

* 바코드 양식(작은 파일)을 처리할 때 최상의 성능을 얻으려면 [일괄 처리 크기]에 `10`을(를) 입력하고 [반복 간격]에 `2`을(를) 입력하십시오.
* 입력 폴더에 많은 파일을 넣으면 *thumbs.db*(이)라는 숨겨진 파일이 있는 오류가 발생할 수 있습니다. 따라서 포함 파일에 대한 포함 파일 패턴을 입력 변수에 대해 지정된 동일한 값(예: `*.tiff`)으로 설정하는 것이 좋습니다. 이렇게 하면 감시 폴더가 DB 파일을 처리하지 못합니다.
* Barcoded Forms 서비스에서 일반적으로 바코드 하나를 처리하는 데 약 0.5초가 소요되므로 일괄 처리 크기 값 `5`과(와) 반복 간격 `2`이면 충분합니다.
* 감시 폴더는 프로세스 엔진이 새 파일이나 폴더를 선택하기 전에 작업을 완료할 때까지 기다리지 않습니다. 계속 감시 폴더를 검색하고 대상 서비스를 호출합니다. 이 동작은 엔진을 오버로드하여 리소스 문제 및 시간 초과를 초래할 수 있습니다. 반복 간격과 배치 크기를 사용하여 감시 폴더 입력을 조절해야 합니다. 더 많은 감시 폴더가 있거나 끝점에 전송률을 활성화하는 경우 반복 간격을 늘리고 배치 크기를 줄일 수 있습니다. 조절에 대한 자세한 내용은 [조절 정보](configuring-watched-folder-endpoints.md#about-throttling)를 참조하십시오.
* 감시 폴더는 사용자 이름 및 도메인 이름에 지정된 사용자를 가장합니다. 감시 폴더는 직접 호출되거나 프로세스가 짧은 경우 이 사용자로서 서비스를 호출합니다. 오래 지속되는 프로세스의 경우 프로세스가 시스템 컨텍스트와 함께 호출됩니다. 관리자는 감시 폴더에 대한 운영 체제 정책을 설정하여 액세스를 허용하거나 거부할 사용자를 결정할 수 있습니다.
* 파일 패턴을 사용하여 결과, 실패 및 폴더를 구성합니다. [파일 패턴 정보](configuring-watched-folder-endpoints.md#about-file-patterns)를 참조하세요.

* 감시 폴더는 Quartz 스케줄러를 사용하여 감시 폴더를 검색합니다. Quartz 스케줄러에는 이 스케줄러를 스캔할 스레드 풀이 있습니다. 감시 폴더의 반복 간격이 매우 낮고(&lt; 5초) 배치 크기가 높으면(> 2) 경합 조건이 발생할 수 있습니다. 이 조건이 발생하면 두 개의 석영 스레드에 의해 한 파일이 선택됩니다.

   * 스레드 중 하나가 파일을 성공적으로 찾고 파일을 사용하여 대상 서비스를 호출합니다.
   * 두 번째 스레드는 파일을 확인하지만 파일이 유효한지(읽기 또는 쓰기 파일) 확인하려고 하면 실패하며, 이로 인해 파일이 읽기 전용이기 때문에 파일을 처리할 수 없다는 잘못된 오류가 발생합니다. 이 문제는 반복 간격이 낮고 배치 크기가 큰 경우에만 발생합니다.
