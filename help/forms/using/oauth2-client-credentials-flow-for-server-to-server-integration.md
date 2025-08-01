---
title: OAuth 2.0 클라이언트 자격 증명 플로우를 사용하여 AEM Forms과 Salesforce 통합
description: OAuth 2.0 클라이언트 자격 증명 플로우를 사용하여 Salesforce과 AEM Forms을 통합하는 단계
solution: Experience Manager, Experience Manager Forms
feature: Form Data Model
role: Admin, User, Developer
exl-id: 56b4a767-1210-47f3-b022-766b0dda9943
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 68%

---

# OAuth 2.0 클라이언트 자격 증명 플로우를 사용한 Salesforce 통합  {#configure-salesforce-with-ouath-2.0-client-credential}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/aem-forms-salesforce-integration) |
| AEM 6.5 | 이 문서 |

OAuth 2.0 클라이언트 자격 증명을 사용하여 AEM Forms를 Salesforce 애플리케이션과 통합할 수 있습니다. OAuth 2.0 클라이언트 자격 증명은 사용자 개입 없는 직접 통신을 위한 표준 보안 방법입니다.

![AEM Forms과 Salesforce 응용 프로그램 간의 통신을 설정하는 동안 워크플로우가 발생했습니다](/help/forms/using/assets/salesforce-workflow.png)

AEM Forms은 액세스 토큰을 얻기 위해 Salesforce 연결된 애플리케이션에 정의된 클라이언트 자격 증명(소비자 키 및 소비자 암호)을 교환합니다.

인증 코드 흐름 인증을 통한 인증에 OAuth 2.0 클라이언트 자격 증명을 사용하면 여러 가지 이점이 있습니다.

* OAuth 2.0 클라이언트 자격 증명 인증은 사용자당 5개가 넘는 연결을 허용합니다.
* AEM 데이터 소스 구성은 AEM 사용자에 대한 비활성화, 액세스 변경, 암호 업데이트 작업을 계속합니다.

## 사전 요구 사항 {#prerequisites}

Salesforce 애플리케이션과 AEM 환경 간의 통신을 설정하기 전에 다음 작업을 수행하십시오.

* [OAuth 2.0 클라이언트 자격 증명 흐름이 있는 Salesforce 연결 앱](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&type=5) 및 조직의 API 전용 사용자를 만들고 앱에 대한 소비자 키 및 소비자 암호를 받습니다.

* Swagger 파일이 조직의 API와 일치하도록 적절하게 구성되었는지 확인합니다. 또는 AEM 환경에서 활용하는 데 맞춤형으로 직접 [Swagger 파일을 만들](https://experienceleague.adobe.com/ko/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api) 수도 있습니다.
>[!NOTE]
>
> AEM 6.5는 Swagger 2.0 파일 사양만 지원합니다.

+++

## 클라이언트 자격 증명 흐름으로 Salesforce을 구성하는 단계 {#steps-to-create-aem-datasource-configuration}

1. 작성자 인스턴스에 로그인합니다.
1. **[!UICONTROL 도구]** > **[!UICONTROL 클라우드 서비스]** > **[!UICONTROL 데이터 소스]**&#x200B;로 이동합니다.
1. 구성 폴더를 선택합니다.
1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 그러면 **[!UICONTROL 데이터 소스 구성 만들기]**&#x200B;가 나타납니다.
1. **[!UICONTROL 제목]**&#x200B;을 지정하고 **[!UICONTROL 서비스 유형]**&#x200B;을 **[!UICONTROL RESTful 서비스]**&#x200B;로 선택합니다.
1. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. **[!UICONTROL Swagger 소스]**&#x200B;를 **[!UICONTROL 파일]로 선택합니다.**
   >[!NOTE]
   >
   > Swagger 파일을 선택하면 스키마, 호스트 이름 및 기본 경로가 자동으로 채워집니다.

1. **[!UICONTROL 찾아보기]**&#x200B;를 클릭하여 로컬 컴퓨터에서 만든 Swagger 파일을 업로드합니다.
1. **[!UICONTROL 인증 유형]**&#x200B;을 **[!UICONTROL OAuth 2.0]**&#x200B;으로 선택합니다. 그러면 **[!UICONTROL 인증 설정]** 패널이 나타납니다.
1. **[!UICONTROL 부여 유형]**&#x200B;을(를) **[!UICONTROL 클라이언트 자격 증명]**(으)로 선택하십시오.
1. Salesforce 연결된 앱에서 받은 **[!UICONTROL 클라이언트 ID]** 및 **[!UICONTROL 클라이언트 보안]**&#x200B;을 지정합니다.
1. **[!UICONTROL 액세스 토큰 URL]**&#x200B;을 다음과 같은 형식으로 지정합니다.
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`

   >[!NOTE]
   >
   > 각 조직에는 고유한 특정 도메인 이름이 있습니다.

1. **[!UICONTROL 연결 테스트]**&#x200B;를 클릭합니다.
1. 연결에 성공하면 **[!UICONTROL 만들기]** 버튼을 클릭합니다.

이제 [양식 데이터 모델을 만들어](/help/forms/using/create-form-data-model.md)적응형 Forms과 구성된 데이터 원본을 통합할 수 있습니다.
