---
title: 기술 관련 자주 묻는 질문 (FAQ)
description: AEM 6.5 LTS에 대해 자주 묻는 기술적 질문
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
source-git-commit: 89016492c069d61c18f9bf83bfb896cd78fb20fd
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 75%

---

# AEM 6.5 LTS 기술 FAQ {#technical-faq}

이 페이지에서는 AEM 6.5 LTS에 대해 자주 묻는 몇 가지 기술적인 질문에 답변합니다.

## 기술 관련 FAQ

### `/systemalive` 엔드포인트는 AEM 6.5 LTS에서 더 이상 사용할 수 없습니다.

`/systemalive` 엔드포인트를 제공하도록 구성된 Felix System Ready 번들은 더 이상 사용되지 않으며 Apache Felix Health Checks로 대체되었습니다. 이 번들은 AEM 6.5 LTS에 더 이상 포함되지 않습니다.

새로운 상태 검사 엔드포인트는 `/system/health`에서 사용할 수 있으며 Apache Felix Health Checks를 사용하여 구현됩니다.

Felix Health Check 프레임워크에 대한 자세한 내용은 [felix 설명서](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md)를 참조하십시오.

### AEM Groovy 콘솔 지원

AEM 6.5에서 사용 중이던 AEM Groovy Console 버전은 Guava 종속성 누락으로 인해 AEM 6.5 LTS에서 작동하지 않을 수 있습니다. 새로 지원되는 AEM Groovy Console 버전은 [19.0.8](https://github.com/orbinson/aem-groovy-console/releases/download/19.0.8/aem-groovy-console-all-19.0.8.zip)입니다.

#### AEM Groovy Console에 필요한 추가 구성

AEM Groovy Console을 사용하는 경우 `com.adobe.granite.apicontroller.FilterResolverHookFactory`에 대해 다음 OSGi 구성을 명시적으로 추가해야 합니다. `org.apache.sling.distribution.api` 키의 허용된 번들 목록에 `aem-groovy-console-bundle`을(를) 추가하여 플랫폼 기본값을 확장합니다.

```
"org.apache.sling.distribution.api": "com.adobe.*,com.day.*,org.apache.sling.*,aem-groovy-console-bundle"
```

### AEM 6.5 LTS가 사용자 동기화를 지원합니까?

예. AEM 6.5 LTS는 사용자 동기화를 지원합니다. AEM 6.5와 6.5 LTS 간에 사용자 동기화의 기능에 변경 사항은 없습니다.

### Maven Central의 Uber JAR가 손상된 것 같습니다. 문제가 무엇입니까?

`apis` 분류자를 사용하여 Uber JAR를 사용하고 있는지 확인합니다. AEM 6.5 LTS에서 Uber JAR의 패키징 구조가 변경되었습니다. 자세한 내용은 [AEM Uber Jar 버전 업데이트](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)를 참조하십시오.

## 추가 도움말 보기

여기에 포함되지 않은 문제가 발생하는 경우 다음 작업을 수행해 보십시오.
* 알려진 문제에 대한 [릴리스 정보](/help/release-notes/release-notes.md)를 검토합니다.
* 도움이 필요하면 Adobe 지원 팀에 문의하십시오.
