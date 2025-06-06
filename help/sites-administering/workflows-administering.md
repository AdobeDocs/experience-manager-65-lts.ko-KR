---
title: 워크플로 인스턴스 관리
description: 워크플로 콘솔에서 워크플로 인스턴스가 예상대로 실행되도록 관리하기 위한 몇 가지 도구를 제공하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
exl-id: c86f66b3-6471-4fb6-81d6-3c0a4dcbe200
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 66%

---

# 워크플로 인스턴스 관리{#administering-workflow-instances}

워크플로 콘솔은 워크플로 인스턴스가 예상대로 실행되도록 관리하기 위한 몇 가지 도구를 제공합니다.

>[!NOTE]
>
>[JMX 콘솔](/help/sites-administering/jmx-console.md#workflow-maintenance)에서 추가 워크플로우 유지 관리 작업을 제공합니다.

다양한 콘솔을 사용하여 워크플로를 관리할 수 있습니다. [전역 탐색](/help/sites-authoring/basic-handling.md#global-navigation)을 사용하여 **도구** 창을 연 다음 **워크플로**&#x200B;를 선택합니다.

* **모델**: 워크플로 정의 관리
* **인스턴스**: 실행 중인 워크플로 인스턴스 조회 및 관리
* **시작 관리자**: 워크플로 실행 방법 관리
* **보관**: 정상적으로 완료된 워크플로 내역 조회
* **실패**: 오류와 함께 완료된 워크플로 내역 조회
* **자동 할당**: 템플릿에 자동 할당 워크플로 구성

## 워크플로 인스턴스 상태 모니터링 {#monitoring-the-status-of-workflow-instances}

1. 탐색을 사용하여 **도구**&#x200B;를 선택한 다음 **워크플로**&#x200B;를 선택합니다.
1. 현재 진행 중인 워크플로 인스턴스 목록을 표시하려면 **인스턴스**&#x200B;를 선택하십시오.

   ![wf-96](assets/wf-96.png)

<!--
## Search Workflow Instances {#search-workflow-instances}

1. Using Navigation select **Tools**, then **Workflow**.
1. Select **Instances** to display the list of workflow instances currently in progress. On the top rail, in the left corner, select **Filters**. Alternatively, you can use the keystrokes alt+1. The following dialog is displayed:

   ![wf-99-1](assets/wf-99-1.png)

1. In the Filter dialog, select the workflow search criteria. You can search based on these inputs:

   * Payload path: Select a specific path
   * Workflow model: Select a workflow model
   * Assignee: Select a workflow Assignee
   * Type: Task, Workflow item, or Workflow Failure
   * Task Status: Active, Complete, or Terminated
   * Where I Am: Owner AND Assignee, Owner only, Assignee only
   * Start Date: Start date before or after a specified date
   * End Date: End date before or after a specified date
   * Due Date: Due date before or after a specified date
   * Updated Date: Updated date before or after a specified date
-->

## 워크플로 인스턴스 일시 중단, 재시작 및 종료 {#suspending-resuming-and-terminating-a-workflow-instance}

1. 탐색을 사용하여 **도구**&#x200B;를 선택한 다음 **워크플로**&#x200B;를 선택합니다.
1. 현재 진행 중인 워크플로 인스턴스 목록을 표시하려면 **인스턴스**&#x200B;를 선택하십시오.

   ![wf-96-1](assets/wf-96-1.png)

1. 특정 항목을 선택한 다음 **종료**, **일시 중단** 또는 **재시작**&#x200B;을 적절히 사용합니다. 확인 및/또는 세부 정보가 필요합니다.

   ![wf-97-1](assets/wf-97-1.png)

## 보관된 워크플로 보기 {#viewing-archived-workflows}

1. 탐색을 사용하여 **도구**&#x200B;를 선택한 다음 **워크플로**&#x200B;를 선택합니다.
1. **보관**&#x200B;을(를) 선택하여 정상적으로 완료된 워크플로 인스턴스 목록을 표시합니다.

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >중단 상태는 다음과 같은 사용자 작업의 결과로 발생하므로 성공적인 종료로 간주됩니다.
   >
   >* **종료** 작업 사용
   >* 워크플로의 대상이 되는 페이지가 (강제로) 삭제되면 워크플로가 종료됩니다

1. 특정 항목을 선택한 다음 **내역 열기**&#x200B;를 선택하여 세부 정보를 표시합니다.

   ![wf-99](assets/wf-99.png)

## 워크플로 인스턴스 실패 해결 {#fixing-workflow-instance-failures}

워크플로우가 실패하면 AEM에서는 원래 원인을 처리하고 나면 조사하고 적절한 조치를 취할 수 있는 **실패** 콘솔을 제공합니다.

* **실패 세부 정보**
**실패 메시지**, **단계** 및 **실패 스택**&#x200B;을 표시하는 창을 엽니다.

* **내역 열기** - 워크플로 내역의 세부 정보를 표시합니다.

* **단계 다시 시도** - 스크립트 단계 구성 요소 인스턴스를 다시 실행합니다. 원래 오류의 원인을 해결한 다음 단계 다시 시도 명령을 사용합니다. 예를 들어 프로세스 단계에서 실행되는 스크립트에서 버그를 수정하고 단계를 다시 시도할 수 있습니다.
* **종료** - 오류로 인해 워크플로에 해결할 수 없는 상황이 발생한 경우 워크플로를 종료합니다. 예를 들어 워크플로는 워크플로 인스턴스에 대해 더 이상 유효하지 않은 저장소의 정보와 같은 환경 조건에 의존할 수 있습니다.
* **종료 후 다시 시도** - **종료**&#x200B;와(과) 유사하지만 원래 페이로드, 제목, 설명을 사용하여 새 워크플로 인스턴스를 시작합니다.

실패를 조사한 다음 그 직후에 워크플로를 다시 시작하거나 종료하려면 다음 단계를 사용하십시오.

1. 탐색을 사용하여 **도구**&#x200B;를 선택한 다음 **워크플로**&#x200B;를 선택합니다.
1. 완료되지 않은 워크플로 인스턴스 목록을 표시하려면 **실패**&#x200B;를 선택하십시오.
1. 특정 항목을 선택한 다음 적절한 작업을 선택합니다.

   ![wf-47](assets/wf-47.png)

## 정기적인 워크플로 인스턴스 제거 {#regular-purging-of-workflow-instances}

워크플로 인스턴스 수를 최소화하면 워크플로 엔진의 성능이 향상되므로 완료되었거나 실행 중인 워크플로 인스턴스를 저장소에서 정기적으로 제거할 수 있습니다.

수명 및 상태에 따라 워크플로 인스턴스를 제거하도록 **Adobe Granite 워크플로 제거 구성**&#x200B;을 구성합니다. 또한 모든 모델 또는 특정 모델의 워크플로 인스턴스를 제거할 수 있습니다.

여러 서비스 구성을 생성하여 서로 다른 기준을 충족하는 워크플로 인스턴스를 제거할 수도 있습니다. 예를 들어 특정 워크플로 모델의 인스턴스가 예상 시간보다 오래 실행될 때 해당 인스턴스를 제거하는 구성을 생성할 수 있습니다. 저장소 크기를 최소화하기 위해 특정 일수가 지난 후 완료된 모든 워크플로를 제거하는 다른 구성을 생성할 수도 있습니다.

서비스를 구성하려면 [웹 콘솔](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 또는 [저장소에 OSGi 구성을 추가](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)할 수 있습니다. 다음 테이블에서는 두 가지 방법에 필요한 속성을 설명합니다.

>[!NOTE]
>
>저장소에 구성을 추가하는 경우 서비스 PID는 다음과 같습니다.
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>이 서비스는 공장 서비스이므로 `sling:OsgiConfig` 노드의 이름에는 다음과 같은 식별자 접미사가 필요합니다.
>
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>속성 이름 (웹 콘솔)</th>
   <th>OSGi 속성 이름</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>작업 이름</td>
   <td>scheduledpurge.name</td>
   <td>예약된 제거의 설명적인 이름입니다.</td>
  </tr>
  <tr>
   <td>워크플로 상태</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>제거할 워크플로 인스턴스의 상태입니다. 다음은 유효한 값입니다.</p>
    <ul>
     <li>완료됨: 완료된 워크플로 인스턴스가 제거됩니다.</li>
     <li>실행 중: 실행 중인 워크플로 인스턴스가 제거됩니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>제거 모델</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>제거할 워크플로 모델의 ID입니다. ID는 모델 노드로의 경로입니다(예: <br /> /var/workflow/models/dam/update_asset<br />). </p> <p>여러 모델을 지정하려면 웹 콘솔에서 “+” 버튼을 클릭하십시오. </p> <p>모든 워크플로우 모델의 인스턴스를 제거할 값을 지정하지 마십시오.</p> </td>
  </tr>
  <tr>
   <td>워크플로 수명</td>
   <td>scheduledpurge.daysold</td>
   <td>제거할 워크플로 인스턴스의 수명(일)입니다.</td>
  </tr>
 </tbody>
</table>

## 받은 편지함의 최대 크기 설정 {#setting-the-maximum-size-of-the-inbox}

[웹 콘솔](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 또는 [저장소에 OSGi 구성을 추가](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)하여 **Adobe Granite Workflow Service**&#x200B;을(를) 구성하여 받은 편지함의 최대 크기를 설정할 수 있습니다. 다음 표에서는 두 메서드에 대해 구성하는 속성을 설명합니다.

>[!NOTE]
>
>저장소에 구성을 추가하는 경우 서비스 PID는 다음과 같습니다.
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`

| 속성 이름 (웹 콘솔) | OSGi 속성 이름 |
|---|---|
| 최대 받은 편지함 쿼리 크기 | granite.workflow.inboxQuerySize |

## 고객 소유 데이터 스토어에 워크플로 변수 사용 {#using-workflow-variables-customer-datastore}

워크플로에서 처리된 데이터는 Adobe 제공 스토리지(JCR)에 저장됩니다. 이 데이터는 기본적으로 중요할 수 있습니다. 모든 사용자 정의 메타데이터/데이터를 Adobe 제공 스토리지가 아닌 자체 관리 스토리지에 저장할 수 있습니다. 이 섹션에서는 이러한 변수를 외부 스토리지로 설정하는 방법에 대해 설명합니다.

### 메타데이터의 외부 스토리지를 사용하도록 모델 설정 {#set-model-for-external-storage}

워크플로 모델 수준에서는 모델(및 런타임 인스턴스)에 메타데이터의 외부 스토리지가 있음을 나타내는 플래그가 제공됩니다. 워크플로 변수는 외부 스토리지로 표시된 모델의 워크플로 인스턴스에 대해 JCR에서 유지되지 않습니다.

*userMetadataPersistenceEnabled* 속성은 워크플로 모델의 *jcr:content 노드*&#x200B;에 저장됩니다. 이 플래그는 워크플로 메타데이터에서 *cq:userMetaDataCustomPersistenceEnabled*&#x200B;로 유지됩니다.

아래 일러스트레이션에서는 워크플로에 플래그를 설정하는 방법을 보여 줍니다.

![workflow-externalize-config](assets/workflow-externalize-config.png)

### 외부 스토리지의 메타데이터를 위한 API {#apis-for-metadata-external-storage}

변수를 외부에 저장하려면 워크플로에서 표시하는 API를 구현합니다.

UserMetaDataPersistenceContext

다음 샘플은 API 사용 방법을 보여 줍니다.

```
@ProviderType
public interface UserMetaDataPersistenceContext {
 
    /**
     * Gets the workflow for persistence
     * @return workflow
     */
    Workflow getWorkflow();
 
    /**
     * Gets the workflow id for persistence
     * @return workflowId
     */
    String getWorkflowId();
 
    /**
     * Gets the user metadata persistence id
     * @return userDataId
     */
    String getUserDataId();
}
```

UserMetaDataPersistenceProvider

```
/**
 * This provider can be implemented to store the user defined workflow-data metadata in a custom storage location
 */
@ConsumerType
public interface UserMetaDataPersistenceProvider {
 
   /**
    * Retrieves the metadata using a unique identifier
    * @param userMetaDataPersistenceContext
    * @param metaDataMap of user defined workflow data metaData
    * @throws WorkflowException
    */
   void get(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
   /**
    * Stores the given metadata to the custom storage location
    * @param userMetaDataPersistenceContext
    * @param metaDataMap metadata map
    * @return the unique identifier that can be used to retrieve metadata. If null is returned, then workflowId is used.
    * @throws WorkflowException
    */
   String put(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
} 
```
