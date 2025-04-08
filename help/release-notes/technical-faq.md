---
title: 기술 자주 묻는 질문(FAQ)
description: AEM 6.5 LTS에 대한 기술 관련 FAQ.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 2352420843c613884ad3cae487ed048bd775e294
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# AEM 6.5 LTS 기술 FAQ {#technical-faq}

이 페이지는 AEM 6.5 LTS에 대한 몇 가지 FAQ에 답변하기 위한 것입니다.

## 기술 FAQ

### `/systemalive` 끝점은 AEM 6.5 LTS에서 더 이상 사용할 수 없습니다.

`/systemalive` 끝점을 제공하도록 구성된 Felix System Ready 번들은 더 이상 사용되지 않으며 Apache Felix 상태 검사로 대체되었습니다. 이 번들은 더 이상 AEM 6.5 LTS에 포함되지 않습니다.

새 상태 검사 끝점은 `/system/health`에서 사용할 수 있으며 Apache Felix 상태 검사를 사용하여 구현됩니다.

Felix 상태 검사 프레임워크에 대한 자세한 내용은 [felix 설명서](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md)를 참조하십시오.

### AEM Groovy 콘솔 지원

AEM 6.5에서 사용 중이던 AEM Groovy 콘솔 버전이 guava 종속성 누락으로 인해 AEM 6.5 LTS에서 작동하지 않을 수 있습니다. 새로 지원되는 AEM Groovy 콘솔 버전은 [19.0.8](https://mvnrepository.com/artifact/be.orbinson.aem/aem-groovy-console/19.0.8)입니다.

## 추가 도움말 보기

여기에서 다루지 않은 문제가 발생하는 경우:
* 알려진 문제에 대해서는 [릴리스 정보](/help/release-notes/release-notes.md)를 검토하십시오.
* 도움이 필요하면 Adobe 지원 팀에 문의하십시오.
