---
title: AEM Forms 프로세스 이해
description: AEM Forms 프로세스가 양식 작성, 제출, 데이터 처리, 유효성 검사, 통합, 워크플로우 자동화 및 출력 관리를 포함하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: 228185f0-deef-4d49-a5b9-0c19411e30c2
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---

# AEM Forms 프로세스 이해 {#understanding-aem-forms-processes}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

일반적인 사용 사례는 한 세트의 AEM Forms 서비스가 하나의 문서에서 작동하는 것입니다. Workbench를 사용하여 프로세스를 생성하여 서비스 컨테이너에 요청을 보낼 수 있습니다. 프로세스는 자동화하는 비즈니스 프로세스를 나타냅니다. 프로세스 만들기에 대한 자세한 내용은 [워크벤치 사용](https://www.adobe.com/go/learn_aemforms_workbench_63)을 참조하십시오.

프로세스가 활성화되면 서비스가 되고 다른 서비스처럼 호출될 수 있습니다. 암호화 서비스와 같은 표준 서비스와 프로세스에서 비롯된 서비스의 한 가지 차이점은, 후자는 많은 동작을 수행하는 하나의 동작을 가진다는 것이다. 반면에 표준 서비스에는 많은 작업이 있습니다. 각 작업은 일반적으로 문서에 정책을 적용하거나 문서를 암호화하는 등의 한 가지 작업을 수행합니다.

프로세스는 단기간 또는 장기간일 수 있습니다. 단기 수행 프로세스는 해당 프로세스가 호출된 실행 스레드와 동기적으로 수행되는 작업입니다. 단기 작업은 클라이언트 응용 프로그램에서 메서드를 호출하고 반환 값을 기다리는 대부분의 프로그래밍 언어에서 제공하는 표준 동작과 비슷합니다.

그러나 다음과 같은 요인으로 인해 프로세스를 동기적으로 완료할 수 없는 경우가 있습니다.

* 프로세스는 상당한 시간에 걸쳐 있을 수 있습니다.
* 프로세스는 조직의 경계를 포괄할 수 있습니다.
* 프로세스를 완료하려면 외부 입력이 필요합니다. 예를 들어 부재 중인 관리자에게 양식을 전송하는 상황을 생각해 보겠습니다. 이 경우 관리자가 돌아와서 양식을 작성할 때까지 프로세스가 완료되지 않습니다.

  이러한 유형의 과정은 장수명 과정으로 알려져 있다. 장기 프로세스는 비동기적으로 수행되므로 리소스가 허용하는 대로 시스템이 상호 작용하고 작업의 추적 및 모니터링이 가능합니다. 장기 프로세스가 호출되면 AEM Forms은 장기 프로세스 상태를 추적하는 레코드의 일부로 호출 식별자 값을 만듭니다. 레코드는 AEM Forms 데이터베이스에 저장됩니다. 더 이상 필요하지 않은 장기 프로세스 레코드를 제거할 수 있습니다.

>[!NOTE]
>
>AEM Forms은 단기 프로세스가 호출될 때 레코드를 만들지 않습니다.

호출 식별자 값을 사용하여 장기 프로세스 상태를 추적할 수 있습니다. 예를 들어 프로세스 호출 식별자 값을 사용하여 실행 중인 프로세스 인스턴스 종료와 같은 Process Manager 작업을 수행할 수 있습니다.

**단기 프로세스 예**

다음 그림은 *MyApplication/EncryptDocument*&#x200B;라는 단기 프로세스의 예입니다.

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 이 프로세스를 호출하는 방법을 설명하는 코드 예제와 함께 수행하려면 Workbench를 사용하여 이름이 `MyApplication/EncryptDocument`인 프로세스를 만듭니다. [워크벤치 사용](https://www.adobe.com/go/learn_aemforms_workbench_63)을 참조하세요.

이 단기 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달되는 보안되지 않은 PDF 문서를 입력 값으로 가져옵니다.
1. 암호로 PDF 문서를 암호화합니다. 이 프로세스에 대한 입력 매개 변수의 이름은 `inDoc`이고 데이터 형식은 document입니다.
1. 암호로 암호화된 PDF 문서를 로컬 파일 시스템에 PDF 파일로 저장합니다. 이 프로세스는 암호화된 PDF 문서를 출력 값으로 반환합니다. 이 프로세스에 대한 출력 매개 변수의 이름은 `outDoc`이고 데이터 형식은 document입니다.

   이 프로세스는 이 프로세스를 호출한 실행 스레드와 동기적으로 완료됩니다. 이 단기 프로세스의 이름은 `MyApplication/EncryptDocument`이고 해당 작업은 `invoke`입니다.

   >[!NOTE]
   >
   >일반적으로 단기 프로세스는 세 가지 이상의 작업으로 구성됩니다. 워크벤치를 사용하여 프로세스를 생성합니다. [워크벤치 사용](https://www.adobe.com/go/learn_aemforms_workbench_63)을 참조하세요.

   *AEM 양식을 사용한 프로그래밍*&#x200B;에서는 이 단기 프로세스를 프로그래밍 방식으로 호출할 수 있는 다음과 같은 방법에 대해 설명합니다.

   * [AEM Forms Remoting을 사용하여 안전하지 않은 문서를 전달하여 단기 프로세스 호출](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)(Flex 응용 프로그램 사용)
   * [Invocation API를 사용하여 단기 프로세스 호출](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api)(Java™ Invocation API)
   * [Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)(웹 서비스 예)
   * [MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)(웹 서비스 예)
   * [SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)(웹 서비스 예)
   * [HTTP를 통해 BLOB 데이터를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http)(웹 서비스 예)
   * [DIME을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime)(웹 서비스 예)
   * [REST를 사용하여 MyApplication/EncryptDocument 프로세스 호출](/help/forms/developing/invoking-aem-forms-using-rest.md)

**오래 지속된 프로세스 예**

다음 그림은 오래 지속된 프로세스의 예입니다.

이 프로세스는 지원자가 대출 양식을 제출할 때 호출됩니다. 대출 담당자가 대출 요청을 승인 또는 거절할 때까지 절차가 완료되지 않습니다. 이 장기 프로세스의 이름은 *FirstAppSolution/PreLoanProcess*&#x200B;이고 해당 작업은 `invoke_Async`입니다. 이 프로세스는 비동기적으로 호출해야 합니다. 프로그래밍 방식으로 이 오래 지속되는 프로세스를 호출하는 방법에 대한 자세한 내용은 [사람 중심의 오래 지속되는 프로세스 호출](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)을 참조하십시오.

>[!NOTE]
>
>이 프로세스는 [첫 번째 AEM Forms 애플리케이션 만들기](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)에 지정된 자습서를 따라 만들 수 있습니다.
