---
title: PaperCapture 서비스가 PDF에서 OCR(Optical Character Recognition) 작업을 수행하지 못할 때 발생하는 문제를 해결하기 위한 문제 해결 문서
description: PaperCapture 서비스가 PDF에서 OCR(Optical Character Recognition) 작업을 수행하지 못하는 문제를 해결하기 위한 단계에 대해 알아봅니다.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: de3cd0ad-0b18-4d9a-8c6b-72cc16149cfc
source-git-commit: eb6f6b994fdd3b2b01e77700d2deb7bd2830ac8f
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 13%

---

# PaperAture 서비스에서 PDF에 대한 OCR 작업을 수행하지 못했습니다.

## 문제

AEM Forms 서비스 팩 6.5.21.0(으)로 업그레이드한 후 `PaperCapture` 서비스가 PDF에서 OCR(광학 문자 인식) 작업을 수행하지 못했습니다. 이 서비스는 PDF 또는 로그 파일 형태의 출력을 생성하지 않습니다.

## 적용 대상

이 솔루션은 다음에 적용됩니다.

* 모든 (JBoss®, WebLogic, WebSphere®) JEE 서버의 AEM Forms
* OSGi 서버의 AEM Forms

## 솔루션

1. 소프트웨어 배포 포털에서 [핫픽스](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0)를 다운로드합니다.
1. 다운로드한 폴더의 컨텐츠를 추출하고 복사합니다.
1. 해당 애플리케이션 서버의 아래 경로로 이동합니다.
   * **JBoss{1®:**
     `..\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\PaperCaptureSvc`
   * **웹 논리**:
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **WebSphere®**:\
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **OSGi 설정**:\
     `..\quickstart\crx-quickstart\bedrock\svcnative\PaperCaptureSvc`
1. AEM 애플리케이션 서버를 중지합니다.
1. `PaperCaptureSvc` 폴더의 기존 콘텐츠를 복사한 콘텐츠로 바꿉니다.
1. AEM 애플리케이션 서버를 다시 시작합니다.

   >[!NOTE]
   >
   >Adobe에서는 `Ctrl + C` 명령을 사용하여 SDK을 다시 시작할 것을 권장합니다. 예를 들어 Java 프로세스를 중지하는 것과 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경에서 불일치가 발생할 수 있습니다.
