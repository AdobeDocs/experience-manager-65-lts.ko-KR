---
title: Acrobat Reader DC Extensions에서 사용할 시간 초과 값 설정
description: Acrobat Reader DC Extensions에서 사용할 시간 초과 값을 설정하는 방법에 대해 알아봅니다.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: c2f96686-15e3-4d92-acfe-f971c5849de4
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Acrobat Reader DC Extensions에서 사용할 시간 초과 값 설정  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

Acrobat Reader DC Extensions에서 많은 PDF 파일에서 작업할 때 작업이 시간 초과되어 실패하지 않도록 다음 시간 초과 값이 적절히 설정되어 있는지 확인하십시오.

**문서 처리 시간 초과**

이 값은 관리 콘솔에서 설정할 수 있습니다. 설정 > 핵심 시스템 설정 > 구성 을 클릭하고 기본 문서 폐기 시간 초과 값을 지정합니다.

**사용자 관리자 AEM 양식 시간 초과:** config.xml 파일을 편집하여 이 값을 설정할 수 있습니다. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기 를 클릭한 다음 내보내기 를 클릭합니다. 내보낸 config.xml 파일을 열고 다음 줄을 편집합니다.

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

저장한 다음 config.xml 파일을 다시 관리 콘솔로 가져옵니다.

**응용 프로그램 서버 세션 시간 제한:** 이 값은 응용 프로그램 서버에 설정할 수 있습니다. 자세한 내용은 애플리케이션 서버와 함께 제공되는 설명서를 참조하십시오.
