---
title: 초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플
description: 사용자 지정된 데이터 및 메타데이터 서비스의 구현을 참조하여 초안 및 제출 구성 요소를 데이터베이스와 통합합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
exl-id: b9b989e3-f204-4929-a03a-857cbb786185
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 1%

---

# 초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플 {#sample-for-integrating-drafts-submissions-component-with-database}

## 샘플 개요 {#sample-overview}

AEM Forms 포털 초안 및 제출 구성 요소를 통해 사용자는 양식을 초안으로 저장하고 나중에 모든 장치에서 제출할 수 있습니다. 또한 사용자는 포털에서 제출된 양식을 볼 수 있습니다. 이 기능을 활성화하기 위해 AEM Forms에서는 사용자가 양식에 입력한 데이터와 초안 및 제출된 양식과 관련된 양식 메타데이터를 저장할 수 있는 데이터 및 메타데이터 서비스를 제공합니다. 이 데이터는 기본적으로 CRX 저장소에 저장됩니다. 그러나 일반적으로 엔터프라이즈 방화벽 외부에 있는 AEM 게시 인스턴스를 통해 사용자가 양식과 상호 작용할 때 조직은 보다 안전하고 신뢰할 수 있도록 데이터 저장소를 사용자 정의하고자 할 수 있습니다.

이 문서에서 설명하는 샘플은 초안 및 제출 구성 요소를 데이터베이스와 통합하기 위한 사용자 지정된 데이터 및 메타데이터 서비스의 참조 구현입니다. 샘플 구현에 사용된 데이터베이스는 **MySQL 5.6.24**&#x200B;입니다. 그러나 초안 및 제출 구성 요소를 선택한 데이터베이스와 통합할 수 있습니다.

>[!NOTE]
>
>* 이 문서에서 설명하는 예와 구성은 MySQL 5.6.24에 따라 다르며 데이터베이스 시스템에 맞게 적절하게 대체해야 합니다.
>* 최신 버전의 AEM Forms 추가 기능 패키지를 설치했는지 확인하십시오. 사용 가능한 패키지 목록은 [AEM Forms 릴리스](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 문서를 참조하십시오.
>* 샘플 패키지는 적응형 Forms 제출 작업에만 작동합니다.

## 샘플 설정 및 구성 {#set-up-and-configure-the-sample}

모든 작성자 및 게시 인스턴스에서 다음 단계를 수행하여 샘플을 설치하고 구성합니다.

1. 다음 **aem-fp-db-integration-sample-pkg-6.1.2.zip** 패키지를 파일 시스템에 다운로드합니다.

   데이터베이스 통합을 위한 샘플 패키지

[파일 가져오기](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. https://[*host*]:[*port*]/crx/packmgr/에서 AEM 패키지 관리자로 이동합니다.
1. **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭합니다.

1. **aem-fp-db-integration-sample-pkg-6.1.2.zip** 패키지를 찾아 선택한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
1. 패키지를 설치하려면 패키지 옆에 있는 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.
1. **[!UICONTROL AEM 웹 콘솔 구성]**(으)로 이동
https://[*host*]:[*port*]/system/console/configMgr에서 페이지를 만듭니다.
1. 편집 모드에서 **[!UICONTROL Forms 포털 초안 및 제출 구성]**&#x200B;을 열려면 클릭하세요.

1. 다음 표에 설명된 대로 등록 정보 값을 지정합니다.

   | **속성** | **설명** | **값** |
   |---|---|---|
   | Forms 포털 초안 데이터 서비스 | 초안 데이터 서비스 식별자 | formsportal.sampledataservice |
   | Forms 포털 초안 메타데이터 서비스 | 초안 메타데이터 서비스용 식별자 | formsportal.samplemetadataservice |
   | Forms 포털 데이터 서비스 제출 | 데이터 전송 서비스에 대한 식별자 | formsportal.sampledataservice |
   | Forms 포털 제출 메타데이터 서비스 | 메타데이터 서비스 제출용 식별자 | formsportal.samplemetadataservice |
   | Forms 포털 대기 중 서명 데이터 서비스 | 대기 중 서명 데이터 서비스 식별자 | formsportal.sampledataservice |
   | Forms 포털 대기 중 서명 메타데이터 서비스 | 대기 중 서명 메타데이터 서비스 식별자 | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >서비스는 다음과 같이 `aem.formsportal.impl.prop` 키의 값으로 언급된 이름으로 확인됩니다.

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   데이터 및 메타데이터 테이블의 이름을 변경할 수 있습니다.

   메타데이터 테이블에 다른 이름을 제공하려면 다음을 수행합니다.

   * 웹 콘솔 구성에서 Forms 포털 메타데이터 서비스 샘플 구현을 찾아 클릭합니다. 데이터 소스, 메타데이터/추가 메타데이터 테이블 이름의 값을 변경할 수 있습니다.

   데이터 테이블에 다른 이름을 제공하려면 다음을 수행합니다.

   * 웹 콘솔 구성에서 Forms 포털 데이터 서비스 샘플 구현을 찾아 클릭합니다. 데이터 소스 및 데이터 테이블 이름의 값을 변경할 수 있습니다.

   >[!NOTE]
   >
   >테이블 이름을 변경하는 경우 양식 포털 구성에서 이름을 제공하십시오.

1. 다른 구성은 그대로 두고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

1. 데이터베이스 연결은 Apache Sling 연결의 풀링된 데이터 Source을 통해 수행할 수 있습니다.
1. Apache Sling 연결의 경우 찾아 클릭하여 웹 콘솔 구성의 편집 모드에서 **[!UICONTROL Apache Sling 연결의 풀링된 데이터 소스]**&#x200B;를 엽니다. 다음 표에 설명된 대로 등록 정보 값을 지정합니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>값</strong></td>
  </tr>
  <tr>
   <td>데이터 소스 이름</td>
   <td><p>데이터 소스 풀에서 드라이버를 필터링하기 위한 데이터 소스 이름</p> <p><strong>참고: </strong><em>샘플 구현에서는 FormsPortal을 데이터 원본 이름으로 사용합니다.</em></p> </td>
  </tr>
  <tr>
   <td>JDBC 드라이버 클래스</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>JDBC 연결 URI<br /> </td>
   <td>jdbc:mysql://[<em>host</em>]:[<em>port</em>]/[<em>schema_name</em>]</td>
  </tr>
  <tr>
   <td>사용자 이름</td>
   <td>데이터베이스 테이블에 대해 인증하고 작업을 수행할 사용자 이름</td>
  </tr>
  <tr>
   <td>암호</td>
   <td>사용자 이름과 연계된 암호</td>
  </tr>
  <tr>
   <td>트랜잭션 격리</td>
   <td>READ_COMMIT</td>
  </tr>
  <tr>
   <td>최대 활성 연결</td>
   <td>1000년</td>
  </tr>
  <tr>
   <td>최대 유휴 연결</td>
   <td>100</td>
  </tr>
  <tr>
   <td>최소 유휴 연결</td>
   <td>10</td>
  </tr>
  <tr>
   <td>초기 크기</td>
   <td>10</td>
  </tr>
  <tr>
   <td>최대 대기</td>
   <td>100000</td>
  </tr>
  <tr>
   <td>차입 시 테스트</td>
   <td>선택됨</td>
  </tr>
  <tr>
   <td>유휴 상태 테스트</td>
   <td>선택됨</td>
  </tr>
  <tr>
   <td>유효성 검사 쿼리</td>
   <td>값의 예로는 SELECT 1(mysql), select 1 from dual(oracle), SELECT 1(MS Sql Server)(validationQuery)이 있습니다.</td>
  </tr>
  <tr>
   <td>유효성 검사 쿼리 시간 초과</td>
   <td>10000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* MySQL용 JDBC 드라이버는 샘플에서 제공되지 않습니다. JDBC 연결 풀을 구성하는 데 필요한 정보를 제공하고 프로비저닝되었는지 확인합니다.
>* 작성자 및 게시 인스턴스가 동일한 데이터베이스를 사용하도록 지정합니다. JDBC 연결 URI 필드의 값은 모든 작성자 및 게시 인스턴스에 대해 동일해야 합니다.

1. 다른 구성은 그대로 두고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

1. 데이터베이스 스키마에 테이블이 이미 있는 경우 다음 단계로 건너뜁니다.

   그렇지 않으면 데이터베이스 스키마에 테이블이 없는 경우 다음 SQL 문을 실행하여 데이터베이스 스키마에 데이터, 메타데이터 및 추가 메타데이터에 대해 별도의 테이블을 생성합니다.

   >[!NOTE]
   >
   >작성자 및 게시 인스턴스에 서로 다른 데이터베이스가 필요하지 않습니다. 모든 작성자 및 게시 인스턴스에서 동일한 데이터베이스를 사용합니다.

   데이터 테이블에 대한 **SQL 문**

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   메타데이터 테이블에 대한 **SQL 문**

   ```sql
   CREATE TABLE `metadata` (
   `formPath` varchar(1000) DEFAULT NULL,
   `formType` varchar(100) DEFAULT NULL,
   `description` text,
   `formName` varchar(255) DEFAULT NULL,
   `owner` varchar(255) DEFAULT NULL,
   `enableAnonymousSave` varchar(45) DEFAULT NULL,
   `renderPath` varchar(1000) DEFAULT NULL,
   `nodeType` varchar(45) DEFAULT NULL,
   `charset` varchar(45) DEFAULT NULL,
   `userdataID` varchar(45) DEFAULT NULL,
   `status` varchar(45) DEFAULT NULL,
   `formmodel` varchar(45) DEFAULT NULL,
   `markedForDeletion` varchar(45) DEFAULT NULL,
   `showDorClass` varchar(255) DEFAULT NULL,
   `sling:resourceType` varchar(1000) DEFAULT NULL,
   `attachmentList` longtext,
   `draftID` varchar(45) DEFAULT NULL,
   `submitID` varchar(45) DEFAULT NULL,
   `id` varchar(60) NOT NULL,
   `profile` varchar(255) DEFAULT NULL,
   `submitUrl` varchar(1000) DEFAULT NULL,
   `xdpRef` varchar(1000) DEFAULT NULL,
   `agreementId` varchar(255) DEFAULT NULL,
   `nextSigners` varchar(255) DEFAULT NULL,
   `eSignStatus` varchar(45) DEFAULT NULL,
   `pendingSignID` varchar(45) DEFAULT NULL,
   `agreementDataId` varchar(255) DEFAULT NULL,
   `enablePortalSubmit` varchar(45) DEFAULT NULL,
   `submitType` varchar(45) DEFAULT NULL,
   `dataType` varchar(45) DEFAULT NULL,
   `jcr:lastModified` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`id`),
   UNIQUE KEY `ID_UNIQUE` (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   additionalmetadatable에 대한 **SQL 문**

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT 'additionalmetadatatable_fk' FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   주석 테이블에 대한 **SQL 문**

   ```sql
   CREATE TABLE `commenttable` (
   `commentId` varchar(255) DEFAULT NULL,
   `comment` text DEFAULT NULL,
   `ID` varchar(255) DEFAULT NULL,
   `commentowner` varchar(255) DEFAULT NULL,
   `time` varchar(255) DEFAULT NULL);
   ```

1. 데이터베이스 스키마에 이미 테이블(data, metadata 및 additionalmetadatable)이 있는 경우 다음 alter table 쿼리를 실행합니다.

   데이터 테이블 변경을 위한 **SQL 문**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   메타데이터 테이블을 변경하기 위한 **SQL 문**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >이미 ALTER TABLE 메타데이터 추가 쿼리를 실행하고 markedforDeletion 열이 테이블에 있는 경우 쿼리가 실패합니다.

   ```sql
   ALTER TABLE metadata add agreementId varchar(255) DEFAULT NULL,
   add nextSigners varchar(255) DEFAULT NULL,
   add eSignStatus varchar(45) DEFAULT NULL,
   add pendingSignID varchar(45) DEFAULT NULL,
   add agreementDataId varchar(255) DEFAULT NULL,
   add enablePortalSubmit varchar(45) DEFAULT NULL,
   add submitType varchar(45) DEFAULT NULL,
   add dataType varchar(45) DEFAULT NULL;
   ```

   ```sql
   ALTER TABLE `metadata` CHANGE `formPath` `formPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formType` `formType` VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `description` `description` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formName` `formName` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `renderPath` `renderPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `showDorClass` `showDorClass` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `sling:resourceType` `sling:resourceType` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `profile` `profile` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `submitUrl` `submitUrl` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `xdpRef` `xdpRef` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   additionalmetadatable 테이블을 변경하기 위한 **SQL 문**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

이제 샘플 구현이 구성되었으며, 이를 사용하여 데이터베이스에 모든 데이터 및 메타데이터를 저장하는 동안 초안 및 제출을 나열할 수 있습니다. 이제 데이터 및 메타데이터 서비스가 샘플에서 어떻게 구성되는지 살펴보겠습니다.

## mysql-connector-java-5.1.39-bin.jar 파일 설치 {#install-mysql-connector-java-bin-jar-file}

모든 작성자 및 게시 인스턴스에서 다음 단계를 수행하여 mysql-connector-java-5.1.39-bin.jar 파일을 설치합니다.

1. `https://'[server]:[port]'/system/console/depfinder`(으)로 이동하여 com.mysql.jdbc 패키지를 검색합니다.
1. 내보낸 사람 열에서 패키지를 번들로 내보내는지 확인합니다.

   번들로 패키지를 내보내지 않는 경우 계속 진행합니다.

1. `https://'[server]:[port]'/system/console/bundles`(으)로 이동하여 **[!UICONTROL 설치/업데이트]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 파일 선택]**&#x200B;을 클릭하고 mysql-connector-java-5.1.39-bin.jar 파일을 찾아 선택합니다. **[!UICONTROL 번들 시작]** 및 **[!UICONTROL 패키지 새로 고침]** 확인란도 선택하십시오.
1. **[!UICONTROL 설치 또는 업데이트]**&#x200B;를 클릭합니다. 완료되면 서버를 다시 시작합니다.
1. (*Windows 전용*) 운영 체제에 대한 시스템 방화벽을 끕니다.

>[!NOTE]
>
> SDK을 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK을 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.

## Forms 포털 데이터 및 메타데이터 서비스용 샘플 코드 {#sample-code-for-forms-portal-data-and-metadata-service}

다음 zip에는 데이터 및 메타데이터 서비스 인터페이스에 대한 `FormsPortalSampleDataServiceImpl` 및 `FormsPortalSampleMetadataServiceImpl`(구현 클래스)이 포함되어 있습니다. 또한 위에 언급된 구현 클래스를 컴파일하는 데 필요한 모든 클래스를 포함합니다.

[파일 가져오기](assets/sample_package.zip)

## 파일 이름의 길이 확인  {#verify-length-of-the-file-name}

Forms 포털의 데이터베이스 구현에서는 추가 메타데이터 테이블을 사용합니다. 테이블에는 테이블의 키 및 ID 열을 기반으로 하는 복합 기본 키가 있습니다. MySQL에서는 기본 키를 최대 255자까지 사용할 수 있습니다. 다음 클라이언트측 유효성 검사 스크립트를 사용하여 파일 위젯에 첨부된 파일 이름의 길이를 확인할 수 있습니다. 파일이 첨부되면 유효성 검사가 실행됩니다. 파일 이름이 150(확장명 포함)보다 큰 경우 다음 절차에 제공된 스크립트는 메시지를 표시합니다. 스크립트를 수정하여 다른 문자 수가 있는지 확인할 수 있습니다.

[클라이언트 라이브러리](/help/sites-developing/clientlibs.md)를 만들고 스크립트를 사용하려면 다음 단계를 수행하십시오.

1. CRXDE에 로그인하고 /etc/clientlibs/ 로 이동합니다.
1. **cq:ClientLibraryFolder** 유형의 노드를 만들고 노드의 이름을 제공합니다. 예: `validation`

   **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

1. 노드를 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL 새 파일 만들기]**&#x200B;를 클릭한 다음 확장명이 .txt인 파일을 만듭니다. 예를들어, `js.txt`새로 만든 .txt 파일에 다음 코드를 추가하고 **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   ```javascript
   #base=util
    util.js
   ```

   위의 코드에서 `util`은(는) 폴더 이름이며 `util` 폴더에 있는 파일의 `util.js` 이름입니다. `util` 폴더 및 `util.js` 파일이 이어지는 단계에서 만들어집니다.

1. 2단계에서 만든 `cq:ClientLibraryFolder` 노드를 마우스 오른쪽 단추로 클릭하고 만들기 > 폴더 만들기를 선택합니다. `util` 폴더를 만듭니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다. `util` 폴더를 마우스 오른쪽 단추로 클릭하고 만들기 > 파일 만들기를 선택합니다. 이름이 `util.js`인 파일을 만듭니다. **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

1. util.js 파일에 다음 코드를 추가하고 **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다. 파일 이름의 코드 유효성 검사 길이입니다.

   ```javascript
   /*
    * ADOBE CONFIDENTIAL
    * ___________________
    *
    * Copyright 2016 Adobe Systems Incorporated
    * All Rights Reserved.
    *
    * NOTICE:  All information contained herein is, and remains
    * the property of Adobe Systems Incorporated and its suppliers,
    * if any.  The intellectual and technical concepts contained
    * herein are proprietary to Adobe Systems Incorporated and its
    * suppliers and may be covered by U.S. and Foreign Patents,
    * patents in process, and are protected by trade secret or copyright law.
    * Dissemination of this information or reproduction of this material
    * is strictly forbidden unless prior written permission is obtained
    * from Adobe Systems Incorporated.
    *
    */
   (function () {
       var connectWithGuideBridge = function (gb) {
           gb.connect(function () {
               //For first time load
               window.guideBridge.on("elementValueChanged" , function(event, payload) {
           var component = payload.target; // Field whose value has changed
                   if(component.name == 'fileAttachment' && component.parent) {
                       var fileItems = $('#'+payload.target.parent.id).find(".guide-fu-fileItem");
                       for (i = 0;i<fileItems.length;i++) {
                           var filename = $(fileItems[i]).find(".guide-fu-fileName").text();
                           //check whether it is previously attached file or a newly  attached one
                           if(filename.length > 150 && filename.indexOf("fp.attach.jsp") < 0) {
                               window.alert("filename is larger than 150 : "+filename);
                                $(fileItems[i]).find(".guide-fu-fileClose.close").click();
                           }
                       }
                   }
   
      });
           });
       };
   
       if (window.guideBridge) {
           connectWithGuideBridge(window.guideBridge);
       } else {
           window.addEventListener("bridgeInitializeStart", function (event) {
               connectWithGuideBridge(event.detail.guideBridge);
           });
       }
   })();
   ```

   >[!NOTE]
   >
   >스크립트는 기본 첨부 파일 위젯 구성 요소에 사용됩니다. 기본 첨부 파일 위젯을 사용자 정의한 경우 위의 스크립트를 변경하여 각각의 변경 사항을 통합합니다.

1. 2단계에서 만든 폴더에 다음 속성을 추가하고 **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.

   * **[!UICONTROL 이름:]** 범주

   * **[!UICONTROL 유형:]** 문자열

   * **[!UICONTROL 값:]** fp.validation

   * **[!UICONTROL 다중 옵션:]** 사용

1. `/libs/fd/af/runtime/clientlibs/guideRuntime`(으)로 이동하여 `fp.validation` 값을 포함 속성에 추가합니다.

1. /libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA로 이동하여 `fp.validation` 값을 embed 속성에 추가합니다.

   >[!NOTE]
   >
   >guideRuntime 및 guideRuntimeWithXfa 클라이언트 라이브러리 대신 사용자 지정 클라이언트 라이브러리를 사용하는 경우 카테고리 이름을 사용하여 이 절차에서 만든 클라이언트 라이브러리를 런타임 시 로드되는 사용자 지정 라이브러리에 포함합니다.

1. **[!UICONTROL 모두 저장 을 클릭합니다.]** 이제 파일 이름이 150자(확장명 포함)보다 크면 메시지가 표시됩니다.
