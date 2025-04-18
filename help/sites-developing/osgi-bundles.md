---
title: OSGi 번들
description: Adobe Experience Manager에서 OSGi 번들을 관리하기 위한 몇 가지 팁을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 1688ac19-b7fb-4c52-b04f-9126a3f72ac7
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# OSGi 번들{#osgi-bundles}

## 시맨틱 버전 관리 사용 {#use-semantic-versioning}

의미 체계 버전 번호 매기기에 대해 합의된 모범 사례는 [https://semver.org/](https://semver.org/)에서 찾을 수 있습니다.

## OSGi 번들에 반드시 필요한 것보다 더 많은 클래스와 jar를 포함하지 마십시오 {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

일반 라이브러리는 별도의 번들로 팩터링해야 합니다. 이렇게 하면 번들 전체에서 재사용할 수 있습니다. OSGi 번들로 *JAR*&#x200B;을(를) 래핑할 때 온라인 소스를 확인하여 이전에 이미 이 작업을 수행했는지 확인하십시오. 기존 번들 래퍼를 찾는 일반적인 위치는 Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse 번들 레서피 및 SpringSource Enterprise 번들 저장소입니다.

## 가장 필요한 번들 버전에 따라 다름 {#depend-on-the-lowest-needed-bundle-versions}

POM 파일의 컴파일 시간 종속성의 경우 필요한 API를 표시하는 필요한 가장 낮은 버전에 항상 의존합니다. 이렇게 하면 이전 버전과의 호환성이 향상되고 이전 릴리스에 대한 지원 수정 사항이 더 쉬워집니다.

## OSGi 번들에서 최소 패키지 세트 내보내기 {#export-a-minimal-set-of-packages-from-osgi-bundles}

패키지를 내보내면 다른 사용자가 사용할 수 있는 API가 만들어집니다. 가능한 한 적게 내보내고 내보낼 항목이 API인지 확인하십시오. 기존에 수출하던 것을 가져와서 비공개로 하는 것보다 개인 방식/클래스를 가져와서 공개로 하는 것이 훨씬 쉽다.

항상 별도의 *impl* 패키지에 구현을 배치하십시오. 기본적으로 *maven-bundle-plugin*&#x200B;은(는) 이름에 *impl*&#x200B;이(가) 없는 프로젝트의 모든 항목을 내보냅니다.

## 내보낸 각 패키지에 대해 항상 의미 체계 버전을 명시적으로 정의 {#always-explicitly-define-a-semantic-version-for-each-package-exported}

이를 통해 API 소비자가 귀하와 함께 발전할 수 있습니다. 그렇게 할 때는 항상 시맨틱 버전 관리 모범 사례를 따르십시오. 이를 통해 API 소비자는 새 버전에서 예상할 변경 유형을 알 수 있습니다.

## 노출된 위치에 메타타입 정보 포함 {#include-metatype-information-where-exposed}

의미 있는 메타 유형 정보를 지정하면 Felix 콘솔에서 서비스 및 구성 요소를 더 쉽게 이해할 수 있습니다. SCR 주석 및 특성 목록은 [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html)에서 찾을 수 있습니다.
