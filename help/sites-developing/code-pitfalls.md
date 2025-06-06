---
title: 코드 함정
description: AEM용으로 개발할 때 피해야 할 일반적인 코딩 위험
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 95656312-2648-455e-80fb-3e03bf1cd633
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# 코드 함정{#code-pitfalls}

## Java 코드에서 Sling 바인딩 방지 {#avoid-sling-bindings-in-java-code}

슬링 바인딩은 90%의 경우 서비스에 액세스할 수 있는 부적절한 방법입니다. 대신 *@Reference* 또는 *@Inject* 주석을 사용해야 합니다.

## Java 코드에서 Thread.interrupt 방지 {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt*&#x200B;은(는) 잘못된 시간에 호출될 때 Lucene 파일 및 영구 캐시 파일을 포함한 파일을 닫을 수 있으므로 위험합니다.

## Java 동기화와 ReadWriteLocks 혼용 방지 {#avoid-mixing-java-synchronization-with-readwritelocks}

이로 인해 코드가 결국 교착 상태에 빠질 수 있는 경합 조건이 발생할 수 있습니다.
