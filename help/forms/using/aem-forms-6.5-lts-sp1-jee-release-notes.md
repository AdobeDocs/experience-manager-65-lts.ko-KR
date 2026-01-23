---
title: ' [!DNL Adobe Experience Manager] 6.5 LTS SP1 릴리스 노트'
description: ' [!DNL Adobe Experience Manager] 6.5 LTS SP1에 대한 릴리스 정보, 새로운 기능, 설치 방법 및 자세한 변경 목록을 확인하십시오.'
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: 27ec3c516b0746fd7e0d82f86750fbb4ef410711
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 3%

---


# JEE의 Adobe Experience Manager (AEM) Forms 6.5 LTS SP1 릴리스 노트

## 릴리스 정보

| **제품** | Adobe Experience Manager Forms |
| -------------------- | ------------------------------------ |
| **버전** | 6.5 LTS SP1 |
| **유형** | JEE(장기 지원 서비스 팩) |
| **릴리스 범주** | 업그레이드 릴리스 |
| **URL 다운로드** | 소프트웨어 배포 |

## [!DNL Experience Manager] 6.5 LTS SP1에 포함된 항목 {#what-is-included-in-aem-65ltssp1}

Adobe Experience Manager(AEM) JEE의 Forms **6.5 LTS SP1**&#x200B;은(는) 새로운 기능, 주요 고객 요청 플랫폼 업데이트 및 일반적인 버그 수정을 제공하며 제품 안정성 및 장기 지원에 중점을 둡니다.

## AEM Forms 6.5 LTS SP1에 포함된 제품

### &#x200B;1. Java 지원 업데이트

최신 Java 버전에 대한 지원이 도입되었습니다.

* **Java™ 17**
* **Java™ 21**

### &#x200B;2. Application Server 지원 업데이트

#### JBoss EAP 8 지원

* **JBoss EAP 8**&#x200B;에 대한 지원이 추가되었습니다.
* 기존 **PicetBox** 보안 프레임워크가 제거되었습니다.
* **Elytron 기반 자격 증명 저장소**&#x200B;가 이제 보안 자격 증명 관리를 위해 지원됩니다.

##### 구성: 자격 증명 저장소(Elytron 기반)

JBoss EAP 8의 AEM Forms은 보안 자격 증명을 관리하는 데 Elytron을 사용합니다. 고객은 서버를 성공적으로 시작하고 데이터베이스 인증을 보호하려면 Elytron 기반 Credential Store를 구성해야 합니다.

구성에 대한 자세한 내용은 설치 및 구성 안내서를 참조하십시오.

### &#x200B;3. 플랫폼 및 호환성 변경 사항

#### 서블릿 사양 지원

* **서블릿 사양 5+** 지원
* **Jakarta EE 9** 준수 기준

#### 네임스페이스 마이그레이션 요구 사항

* Jakarta EE 9에서는 `javax.*`에서 `jakarta.*`(으)로 네임스페이스가 변경되었습니다.
* 모든 **사용자 지정 DSC**&#x200B;을 `jakarta.*` 네임스페이스로 마이그레이션해야 합니다.
* AEM Forms 6.5 LTS SP1은(는) **Jakarta EE 9+ 기반 응용 프로그램 서버만 지원합니다**

자세한 내용은 **javax에서 jakarta 네임스페이스로 마이그레이션**&#x200B;을 참조하십시오.

## 업그레이드

자세한 업그레이드 지침은 [JEE의 AEM Forms 6.5 LTS SP1용 업그레이드 안내서](https://experienceleague.adobe.com/ko/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)를 참조하십시오.

## 설치

설치 단계 및 필수 조건은 **AEM Forms 6.5 LTS SP1(JEE)용 설치 안내서**&#x200B;를 참조하십시오.

## 지원되는 플랫폼

지원되는 플랫폼, 운영 체제, 데이터베이스 및 애플리케이션 서버의 전체 목록은 다음을 참조하십시오.

**지원되는 플랫폼 매트릭스 - AEM Forms 6.5 LTS SP1(JEE)**

## 더 이상 사용되지 않으며 제거된 기능

* CRX 저장소 지속성에 대한 **RDBMK** 지원이 제거되었습니다.
* 클러스터된 환경의 경우 **MongoMK**&#x200B;만 저장소 지속성이 지원됩니다.

## javax에서 jakarta 네임스페이스로 마이그레이션

### `javax`에서 `jakarta` 네임스페이스로 마이그레이션

**AEM Forms 6.5 LTS SP1**&#x200B;부터 **Jakarta Servlet API 5/6**&#x200B;을 구현하는 응용 프로그램 서버만 지원됩니다. **Jakarta EE 9 이상**&#x200B;에서 모든 API가 `javax.{}` 네임스페이스에서 `jakarta.`(으)로 전환되었습니다.

따라서 **모든 사용자 지정 DSC는 `jakarta` 네임스페이스를 사용해야 합니다**. `javax.{}` API를 사용하여 빌드된 사용자 지정 구성 요소는 지원되는 응용 프로그램 서버와 **호환되지 않습니다**.

### 사용자 지정 DSC에 대한 마이그레이션 옵션

다음 방법 중 하나를 사용하여 기존 사용자 지정 DSC를 마이그레이션할 수 있습니다.

#### 옵션 1: Source 코드 마이그레이션(권장)

* `javax.{}`에서 `jakarta.`(으)로 모든 가져오기 문 업데이트
* 사용자 지정 DSC 프로젝트 다시 빌드 및 다시 컴파일
* 업데이트된 구성 요소를 애플리케이션 서버에 재배포

**이점:**

* Jakarta EE 9+와의 장기적인 호환성 보장
* 활발하게 유지 관리되는 프로젝트에 가장 적합

#### 옵션 2: Eclipse 변환기를 사용한 바이너리 마이그레이션

* **Eclipse 변환기** 도구를 사용하여 컴파일된 이진 파일(`.jar`, `.war`)을 `javax`에서 `jakarta`(으)로 변환합니다
* 소스 코드를 변경하거나 다시 컴파일할 필요가 없습니다.
* 변환된 바이너리를 애플리케이션 서버에 다시 배포

>[!NOTE]
>
> 이진 변환은 **바이트코드 수준**&#x200B;에서 수행됩니다.

샘플 가져오기 매핑

다음은 마이그레이션 중에 필요한 네임스페이스 변경 사항에 대한 일반적인 예입니다.

이전(javax)    이후(자카르타)
javax.servlet.*    jakarta.servlet.*
javax.servlet.http.*    jakarta.servlet.http*

### 샘플 가져오기 매핑

다음 표에서는 `javax`에서 `jakarta`(으)로 마이그레이션할 때 필요한 일반적인 네임스페이스 변경 사항을 보여 줍니다.

| 다음 이전(`javax`) | 다음 이후(`jakarta`) |
| ---------------------- | ------------------------ |
| `javax.servlet.*` | `jakarta.servlet.*` |
| `javax.servlet.http.*` | `jakarta.servlet.http.*` |

사용자 지정 DSC 소스 코드를 업데이트하거나 변환된 바이너리를 확인할 때 이러한 매핑을 참조로 사용합니다.

