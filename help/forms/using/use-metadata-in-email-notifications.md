---
title: 이메일 알림에서 메타데이터 사용
description: 메타데이터를 사용하여 양식 워크플로우 이메일 알림의 정보 채우기
topic-tags: publish
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
exl-id: 64d4ef01-ee33-4c8b-977f-0c9b31755820
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 1%

---

# 이메일 알림에서 메타데이터 사용 {#use-metadata-in-an-email-notification}

작업 할당 단계를 사용하여 작업을 만들고 사용자 또는 그룹에 할당할 수 있습니다. 작업이 사용자 또는 그룹에 할당되면 정의된 사용자 또는 정의된 그룹의 각 구성원에게 이메일 알림이 전송됩니다. 일반적인 [전자 메일 알림](../../forms/using/use-custom-email-template-assign-task-step.md)에는 할당된 작업의 링크와 작업과 관련된 정보가 포함되어 있습니다.

이메일 템플릿에 있는 메타데이터를 사용하여 이메일 알림의 정보를 동적으로 채울 수 있습니다. 예를 들어 다음 이메일 알림의 제목, 설명, 기한, 우선 순위, 워크플로우 및 마지막 날짜 값은 런타임 시(이메일 알림이 생성될 때) 동적으로 선택됩니다.

![기본 전자 메일 서식 파일](assets/default_email_template_metadata_new.png)

메타데이터는 키-값 쌍으로 저장됩니다. 전자 메일 템플릿에 키를 지정할 수 있으며 키는 런타임 시(전자 메일 알림이 생성될 때) 값으로 대체됩니다. 예를 들어 아래 코드 샘플에서는 &quot;$ {workitem_title}&quot;이(가) 키입니다. 이 값은 런타임 시 &quot;Loan-Request&quot; 값으로 대체됩니다.

```html
subject=Task Assigned - ${workitem_title}

message=<html><body>\n\
 <table style="width: 480px; font-family: Helvetica, Arial, sans-serif; border: 0; padding: 0; vertical-align: top; text-align: left; word-wrap: break-word; margin: 16px auto; color:#323232; background-color:#FFFCF9; border-collapse: collapse;">\n\
  <tbody>\n\
   <tr>\n\
    <td style="height: 100px; width: 480px; background-color: #FFE0CB; border-top: 5pt solid black; font-family: Helvetica, Arial, sans-serif; font-weight: bold; font-size: 15px; line-height: 20px; padding: 12px; color: #707070;">\n\
      Sample Company\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="font-family: Helvetica, Arial, sans-serif; height: auto; background-color: #FFFCF9; padding: 32px 16px 20px 16px; ">\n\
     <pre style="font-size: 13px; font-family: Helvetica, Arial, sans-serif;  font-weight: normal; color: #323232;"> Hello ${workitem_assignee},\n\
 The following task has been assigned to you:</pre>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="width: 480px;">\n\
     <table style="height: auto; width: 480px; background-color:#FFFBF9; font-family: Helvetica, Arial, sans-serif; border-collapse: collapse;">\n\
      <tbody>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> TITLE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_title}</p>\n\
        </td>\n\
       </tr>\n\
                            <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DESCRIPTION</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_description}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DUE DATE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_due_date}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> PRIORITY</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_priority}</p>\n\
        </td>\n\
       </tr>\n\
       <tr>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> WORKFLOW</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_workflow}</p>\n\
        </td>\n\
       </tr>\n\
      </tbody>\n\
     </table>\n\
    </td>\n\
   </tr>\n\
   <tr style = "text-align: center; vertical-align: middle;">\n\
    <td style="padding:48px 0 72px 0;"> \n\
     <a href="${workitem_url}" target="_blank" style="background-color: #1EBBBB; font-size: 18px; line-height: 25px; font-weight: bold; color: #FFFFFF; text-decoration: none; padding: 15px 15px 15px 15px;">Open Task</a>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="border-top: solid 1px #EDEAE7; padding: 16px;">\n\
     <p><span style="font-size: 12px; font-weight: normal; font-style: italic; color: #919191;">This is an automatically generated email. Do not reply to this email.</code></p>\n\
    </td>\n\
   </tr>\n\
  </tbody>\n\
 </table>\n\
</body>\n\
</html>\n\
```

## 이메일 알림에서 시스템 생성 메타데이터 사용 {#using-system-generated-metadata-in-an-email-notification}

AEM Forms 애플리케이션은 즉시 사용할 수 있는 여러 메타데이터 변수(키-값 쌍)를 제공합니다. 전자 메일 템플릿에서 이러한 변수를 사용할 수 있습니다. 변수의 값은 연결된 양식 애플리케이션을 기반으로 합니다. 다음 표에는 즉시 사용할 수 있는 모든 메타데이터 변수가 나열되어 있습니다.

<table>
 <tbody> 
  <tr> 
   <td>키</td> 
   <td>설명</td> 
  </tr> 
  <tr> 
   <td>workitem_title</td> 
   <td>연결된 양식 애플리케이션 제목입니다.</td> 
  </tr> 
  <tr> 
   <td>workitem_url</td> 
   <td>연결된 양식 애플리케이션에 액세스하기 위한 URL.</td> 
  </tr> 
  <tr> 
   <td>workitem_description</td> 
   <td>연결된 양식 응용 프로그램에 대한 설명입니다.</td> 
  </tr> 
  <tr> 
   <td>workitem_priority</td> 
   <td>연결된 양식 응용 프로그램에 대해 지정된 우선 순위입니다.</td> 
  </tr> 
  <tr> 
   <td>workitem_due_date</td> 
   <td>연결된 양식 응용 프로그램에 대한 마지막 작업일.</td> 
  </tr> 
  <tr> 
   <td>workitem_workflow</td> 
   <td>양식 응용 프로그램과 연결된 워크플로의 이름입니다.</td> 
  </tr> 
  <tr> 
   <td>작업 항목 할당 타임스탬프</td> 
   <td>워크플로 항목이 현재 할당자에게 할당된 날짜 및 시간입니다.</td> 
  </tr> 
  <tr> 
   <td>workitem_assinee</td> 
   <td>현재 피할당자의 이름입니다.</td> 
  </tr> 
  <tr> 
   <td>host_prefix</td> 
   <td>작성자 서버의 URL. 예: https://10.41.42.66:4502<br /> </td> 
  </tr> 
  <tr> 
   <td>publish_prefix</td> 
   <td>게시 서버의 URL. 예: https://10.41.42.66:4503</td> 
  </tr> 
 </tbody> 
</table>

## 이메일 알림에서 사용자 지정 메타데이터 사용 {#using-custom-metadata-in-an-email-notification}

이메일 알림에서 사용자 지정 메타데이터를 사용할 수도 있습니다. 사용자 지정 메타데이터에는 시스템에서 생성한 메타데이터 외에 다른 정보가 포함됩니다. 예를 들어, 데이터베이스에서 검색한 정책 세부 정보. ECMAScript 또는 OSGi 번들을 사용하여 crx-repository에 사용자 지정 메타데이터를 추가할 수 있습니다.

### ECMAScript를 사용하여 사용자 지정 메타데이터 추가  {#use-ecmascript-to-add-custom-metadata}

[ECMAScript](https://en.wikipedia.org/wiki/ECMAScript)은 스크립팅 언어입니다. 클라이언트측 스크립팅 및 서버 애플리케이션에 사용됩니다. ECMAScript를 사용하여 전자 메일 템플릿에 대한 사용자 지정 메타데이터를 추가하려면 다음 단계를 수행하십시오.

1. 관리 계정으로 CRX DE에 로그인합니다. URL은 https://&#39;[서버]:[포트]&#39;/crx/de/index.jsp입니다.

1. /apps/fd/dashboard/scripts/metadataScripts로 이동합니다. 확장명이 .ecma인 파일을 만듭니다. 예: usermetadata.ecma

   위에서 언급한 경로가 존재하지 않는 경우 경로를 만듭니다.

1. 키-값 쌍에서 사용자 지정 메타데이터를 생성하는 논리가 있는 .ecma 파일에 코드를 추가합니다. 예를 들어 다음 ECMAScript 코드는 보험 증서에 대한 사용자 지정 메타데이터를 생성합니다.

   ```javascript
   function getUserMetaData()  {
       //Commented lines below provide an overview on how to set user metadata in map and return it.
       var HashMap = Packages.java.util.HashMap;
       var valuesMap = new HashMap();
       valuesMap.put("policyNumber", "2017568972695");
       valuesMap.put("policyHolder", "Adobe Systems");
   
       return valuesMap;
   }
   ```

1. 모두 저장을 클릭합니다. 이제 AEM 워크플로우 모델에서 스크립트를 선택할 수 있습니다.

   ![assigntask-metadata](assets/assigntask-metadata.png)

1. (선택 사항) 스크립트 제목을 지정합니다.

   제목을 지정하지 않으면 사용자 지정 메타데이터 필드에 ECMAScript 파일의 전체 경로가 표시됩니다. 다음 단계를 수행하여 스크립트에 의미 있는 제목을 지정합니다.

   1. 스크립트 노드를 확장하고 **[!UICONTROL jcr:content]** 노드를 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL Mixins]**&#x200B;을 클릭합니다.
   1. 믹스인 편집 대화 상자에서 mix:title을 입력하고 **+**&#x200B;을(를) 클릭합니다.
   1. 다음 값이 있는 속성을 추가합니다.

      | 이름 | jcr:title |
      |---|---|
      | 유형 | 문자열 |
      | 값 | 스크립트 제목을 지정합니다. (예: 정책 소유자에 대한 사용자 지정 메타데이터) 지정된 값이 작업 할당 단계에 표시됩니다. |

### OSGi 번들 및 Java 인터페이스를 사용하여 사용자 지정 메타데이터 추가 {#use-an-osgi-bundle-and-java-interface-to-add-custom-metadata}

WorkitemUserMetadataService Java 인터페이스를 사용하여 이메일 템플릿에 대한 사용자 지정 메타데이터를 추가할 수 있습니다. WorkitemUserMetadataService Java 인터페이스를 사용하는 OSGi 번들을 만들고 AEM Forms 서버에 배포할 수 있습니다. 이 옵션을 사용하면 작업 할당 단계에서 메타데이터를 선택할 수 있습니다.

Java 인터페이스를 사용하여 OSGi 번들을 만들려면 [AEM Forms 클라이언트 SDK](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) jar 및 [granite jar](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) 파일을 OSGi 번들 프로젝트에 외부 종속성으로 추가합니다. 모든 Java IDE를 사용하여 OSGi 번들을 만들 수 있습니다. 다음 절차에서는 Eclipse를 사용하여 OSGi 번들을 만드는 단계를 제공합니다.

1. Eclipse IDE를 엽니다. 파일 > 새 프로젝트로 이동합니다.

1. 마법사 선택 화면에서 Maven 프로젝트를 선택하고 다음을 클릭합니다.

1. 새 Maven 프로젝트에서 기본값을 유지하고 다음을 누릅니다. Archetype을 선택하고 다음 을 클릭합니다. 예: maven-archetype-quickstart. 프로젝트의 그룹 ID, 아티팩트 ID, 버전 및 패키지를 지정하고 마침을 클릭합니다. 프로젝트가 생성됩니다.

1. 편집할 pom.xml 파일을 열고 파일의 모든 내용을 다음과 같이 바꿉니다.

1. WorkitemUserMetadataService Java 인터페이스를 사용하여 이메일 템플릿에 대한 사용자 지정 메타데이터를 추가하는 소스 코드를 추가합니다. 샘플 코드가 아래에 나와 있습니다.

   ```java
   package com.aem.impl;
   
   import com.adobe.fd.workspace.service.external.WorkitemUserMetadataService;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Properties;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.osgi.framework.Constants;
   
   import java.util.HashMap;
   import java.util.Map;
   
   @Component
   @Service
   @Properties({
           @Property(name = Constants.SERVICE_DESCRIPTION, value = "A sample implementation of a user metadata service."),
           @Property(name = WorkitemUserMetadataService.SERVICE_PROPERTY_LABEL, value = "Default User Metadata Service")})
   
   public class WorkitemUserMetadataServiceImpl
     implements WorkitemUserMetadataService
   {
     public WorkitemUserMetadataServiceImpl() {}
   
     public Map<String, String> getUserMetadataMap()
     {
       HashMap<String, String> metadataMap = null;
       metadataMap = new HashMap();
       metadataMap.put("test_metadata", "tested-interface implementation");
       return metadataMap;
     }
   }
   ```

1. 명령 프롬프트를 열고 OSGi 번들 프로젝트가 포함된 디렉터리로 이동합니다. 다음 명령을 사용하여 OSGi 번들을 생성합니다.

   `mvn clean install`

1. AEM Forms 서버에 번들을 업로드합니다. AEM 패키지 관리자를 사용하여 번들을 AEM Forms 서버로 가져올 수 있습니다.

번들을 가져온 후에는 작업 할당 단계에서 메타데이터를 선택하고 이메일 템플릿으로 사용할 수 있습니다.
