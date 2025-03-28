---
title: 압축된 토큰 지원
description: AEM의 캡슐화된 토큰 지원에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
exl-id: f33950b1-6164-4e02-b666-50af84647852
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---

# 압축된 토큰 지원{#encapsulated-token-support}

## 소개 {#introduction}

기본적으로 AEM은 토큰 인증 핸들러를 사용하여 각 요청을 인증합니다. 그러나 인증 요청을 처리하려면 모든 요청에 대해 토큰 인증 핸들러가 저장소에 액세스해야 합니다. 이 문제는 쿠키가 인증 상태를 유지하는 데 사용되기 때문에 발생합니다. 논리적으로 상태는 저장소에서 지속되어야 후속 요청의 유효성을 검사할 수 있습니다. 사실상, 이것은 인증 메커니즘이 상태 저장(stateful)임을 의미한다.

이는 특히 수평적 확장성에 중요합니다. 아래 표시된 게시 팜과 같은 다중 인스턴스 설정에서 로드 밸런싱을 최적의 방식으로 수행할 수 없습니다. 상태 저장 인증을 사용하면 사용자가 처음 인증되는 인스턴스에서만 지속 인증 상태를 사용할 수 있습니다.

![chlimage_1-33](assets/chlimage_1-33a.png)

예를 들어 다음 시나리오를 생각해 보십시오.

게시 인스턴스 1에서 사용자를 인증할 수 있지만 후속 요청이 게시 인스턴스 2로 이동하면 해당 상태는 게시 인스턴스 1의 저장소에서 지속되었고 게시 인스턴스 2에는 자체 저장소가 있으므로 해당 인스턴스에는 해당 지속된 인증 상태가 없습니다.

이에 대한 솔루션은 로드 밸런서 수준에서 고정 연결을 구성하는 것입니다. 고정 연결을 사용하면 사용자는 항상 동일한 게시 인스턴스로 이동됩니다. 따라서 최적의 로드 밸런싱은 불가능합니다.

게시 인스턴스를 사용할 수 없게 되면 해당 인스턴스에서 인증된 모든 사용자의 세션이 손실됩니다. 인증 쿠키의 유효성을 검사하려면 저장소 액세스가 필요하기 때문입니다.

## 캡슐화된 토큰을 사용한 상태 비저장 인증 {#stateless-authentication-with-the-encapsulated-token}

수평적 확장성을 위한 솔루션은 AEM의 새로운 캡슐화된 토큰(Encapsulated Token) 지원을 사용하는 상태 비저장 인증(Stateless Authentication)입니다.

캡슐화된 토큰은 AEM이 저장소에 액세스하지 않고도 오프라인에서 인증 정보를 안전하게 만들고 확인할 수 있도록 하는 암호화 방법입니다. 이렇게 하면 고정 연결이 필요 없이 모든 게시 인스턴스에서 인증 요청이 발생할 수 있습니다. 또한 모든 인증 요청에 대해 저장소에 액세스할 필요가 없기 때문에 인증 성능이 향상된다는 장점이 있습니다.

아래 MongoMK 작성자 및 TarMK 게시 인스턴스와 함께 지리적으로 분산된 배포에서 이 기능이 어떻게 작동하는지 확인할 수 있습니다.

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>캡슐화된 토큰은 인증에 대한 것입니다. 저장소에 액세스하지 않고도 쿠키의 유효성을 검사할 수 있습니다. 그러나 사용자가 모든 인스턴스에 존재하고 모든 인스턴스에서 해당 사용자 아래에 저장된 정보에 액세스할 수 있어야 합니다.
>
>예를 들어, 캡슐화된 토큰의 작동 방식 때문에 게시 인스턴스 번호 1에 새 사용자가 생성되면 게시 번호 2에서 성공적으로 인증됩니다. 사용자가 두 번째 게시 인스턴스에 없는 경우 요청이 계속 실패하게 됩니다.
>

## 캡슐화된 토큰 구성 {#configuring-the-encapsulated-token}

>[!NOTE]
>사용자를 동기화하고 토큰 인증에 의존하는 모든 인증 핸들러(예: SAML 및 OAuth)는 다음과 같은 경우 캡슐화된 토큰으로만 작동합니다.
>
>* 고정 세션이 활성화되어 있거나
>
>* 동기화가 시작될 때 AEM에서 사용자가 이미 생성되었습니다. 즉, 동기화 프로세스 중에 처리기가 사용자를 **만들기**&#x200B;하는 상황에서는 캡슐화된 토큰이 지원되지 않습니다.

캡슐화된 토큰을 구성할 때 고려해야 할 몇 가지 사항이 있습니다.

1. 관련된 암호화 때문에 모든 인스턴스는 동일한 HMAC 키를 가져야 합니다. AEM 6.3 이후 주요 자료는 더 이상 저장소에 저장되지 않고 실제 파일 시스템에 저장됩니다. 따라서 키를 복제하는 가장 좋은 방법은 소스 인스턴스의 파일 시스템에서 키를 복제할 타겟 인스턴스의 파일 시스템으로 키를 복제하는 것입니다. 자세한 내용은 아래의 &quot;HMAC 키 복제&quot;에서 확인하십시오.
1. 캡슐화된 토큰을 활성화해야 합니다. 이 작업은 웹 콘솔을 통해 수행할 수 있습니다.

### HMAC 키 복제 {#replicating-the-hmac-key}

인스턴스 간에 키를 복제하려면 다음을 수행해야 합니다.

1. 복사할 주요 자료가 포함된 AEM 인스턴스(일반적으로 작성자 인스턴스)에 액세스합니다.
1. 로컬 파일 시스템에서 `com.adobe.granite.crypto.file` 번들을 찾습니다. 예를 들어 이 경로에서 다음을 수행합니다.

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25`

   각 폴더 내의 `bundle.info` 파일은 번들 이름을 식별합니다.

1. 데이터 폴더로 이동합니다. 예:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. HMAC 및 마스터 파일을 복사합니다.
1. 그런 다음 HMAC 키를 복제할 대상 인스턴스로 이동하여 데이터 폴더로 이동합니다. 예:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. 이전에 복사한 두 파일을 붙여넣습니다.

1. 키를 복제할 모든 인스턴스에 대해 위의 단계를 반복합니다.

#### 캡슐화된 토큰 활성화 {#enabling-the-encapsulated-token}

HMAC 키가 복제되면 웹 콘솔을 통해 캡슐화된 토큰을 활성화할 수 있습니다.

1. 브라우저를 `https://serveraddress:port/system/console/configMgr`(으)로 지정
1. **Adobe Granite 토큰 인증 처리기**&#x200B;라는 항목을 찾아 클릭합니다.
1. 다음 창에서 **캡슐화된 토큰 지원을 사용하도록 설정** 상자를 선택하고 **저장**&#x200B;을 누릅니다.
