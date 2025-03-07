---
title: Windows Vista에서 SSL 구성
description: Windows Vista에서 SSL을 구성하는 방법에 대해 알아봅니다. Java Keytool 을 사용하고 실행하여 인증에 RSA 키를 사용하여 SSL 인증서를 생성합니다.
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: ee73f6a1-712c-461f-95e8-85f8c5694293
source-git-commit: d0f29cb177e98315cd50c2d7e96c3605eec14885
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Windows Vista에서 SSL 구성 {#configuring-ssl-on-windows-vista}

Windows Vista™에서 SSL을 구성하려면 인증을 위해 RSA 키가 포함된 SSL 인증서가 필요합니다. Java 키 도구를 사용하여 인증서를 생성할 수 있습니다.

>[!NOTE]
>
>Windows Vista는 DSA 키에서 작동하지 않습니다.

인증서 및 키 저장소를 만드는 데 필요한 모든 정보가 포함된 단일 명령을 사용하여 키 도구를 실행할 수 있습니다.

**SSL 인증서 만들기**

1. 명령 프롬프트에서 *`[JAVA HOME]`*/bin으로 이동하고 다음 명령을 입력하여 인증서 및 키 저장소를 만듭니다.

   `keytool -genkey -keyalg RSA -dname "CN=`*호스트 이름* `, OU=`*그룹 이름* `, O=`*회사 이름* `,L=`*도시 이름* `, S=`*상태* `, C=`*국가 코드* `" -alias`*&quot;LC 인증서&quot;* `-keypass` `key`*_* *암호* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >*`[JAVA_HOME]`을(를) JDK가 설치된 디렉터리로 바꾸고 텍스트를 사용자 환경에 해당하는 값으로 기울임꼴로 바꿉니다.*

1. 암호로 `changeit`을(를) 입력하십시오. 이 암호는 Java 설치의 기본값이며 시스템 관리자가 변경했을 수 있습니다.
