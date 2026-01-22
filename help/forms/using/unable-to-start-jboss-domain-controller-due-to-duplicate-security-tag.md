---
title: JBoss 도메인 컨트롤러를 시작할 수 없음
description: JBoss EAP 8을 사용한 AEM Forms 6.5.1 LTS 클러스터 배포에서 구성 파일에는 중복 태그가 포함될 수 있습니다.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: 5d020671efaa4527a5f6dbb4b779c7a3351888a4
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---


# JBoss 도메인 컨트롤러를 시작할 수 없음

## 문제

**JBoss EAP 8**&#x200B;을(를) 사용한 **AEM Forms 6.5.1 LTS** 클러스터 배포에서 구성 파일
`<JBOSS_HOME>/domain/configuration/domain_oracle.xml`(및 데이터베이스별 변형)에는 **중복된 열기 `<security>` 태그**&#x200B;가 포함될 수 있습니다.

이로 인해 **잘못된 XML 구성**&#x200B;이 발생하여 **JBoss 도메인 컨트롤러 시작 실패**&#x200B;가 발생하고 클러스터 초기화가 제대로 수행되지 않습니다.

## 적용 대상

* **제품:** AEM Forms 6.5.1 LTS
* **배포 유형:** 클러스터
* **응용 프로그램 서버:** JBoss EAP 8.x
* **구성 파일:**

   * `<JBOSS_HOME>/domain/configuration/domain_oracle.xml`
   * `<JBOSS_HOME>/domain/configuration/domain_mysql.xml`
   * `<JBOSS_HOME>/domain/configuration/domain_mssql.xml`

## 문제 해결 단계

1. 도메인 컨트롤러를 시작하는 동안 다음과 같은 오류가 발생할 수 있습니다.

   * `WFLYCTL0198: Unexpected element 'security'`
   * `IJ010061: Unexpected element: security`

2. 관련 구성 파일을 엽니다.

   ```
   <JBOSS_HOME>/domain/configuration/domain_oracle.xml
   (or domain_mysql.xml / domain_mssql.xml)
   ```

3. 중복된 `<security>` 여는 태그를 찾습니다.

   **잘못된 구성:**

   ```xml
   <security>
       <security>
           <user-name>adobe</user-name>
           <credential-reference store="db-creds" alias="EncryptDBPassword"/>
       </security>
   ```

4. 추가 여는 `<security>` 태그를 제거하여 아래와 같이 구성을 수정합니다.

   **올바른 구성:**

   ```xml
   <security>
       <user-name>adobe</user-name>
       <credential-reference store="db-creds" alias="EncryptDBPassword"/>
   </security>
   ```

5. 파일을 저장하고 JBoss 도메인 컨트롤러를 시작합니다.

6. 모든 클러스터 노드에 걸쳐 동일한 검증된 구성이 일관되게 적용되는지 확인합니다.
