---
title: 사용자 지정 Adobe Campaign 확장
description: AEM 또는 Adobe Campaign에서 Adobe Campaign으로 AEM에서 사용자 지정 코드를 호출할 수 있습니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 7cdce721-ca00-43ac-a543-85bfad382821
index: false
source-git-commit: 2edf37c2d6bb04b418618f2780f773ab37559114
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 2%

---


# 사용자 지정 Adobe Campaign 확장 {#creating-custom-extensions}

일반적으로 프로젝트를 구현할 때에는 AEM과 Adobe Campaign 모두에 사용자 지정 코드가 있습니다. 기존 API를 사용하면 AEM 또는 AEM에서 Adobe Campaign으로 Adobe Campaign에서 사용자 지정 코드를 호출할 수 있습니다. 이 문서에서는 그 방법에 대해 설명합니다.

## 사전 요구 사항 {#prerequisites}

다음을 설치해야 합니다.

* Adobe Experience Manager
* Adobe Campaign 6.1

자세한 내용은 [AEM과 Adobe Campaign 6.1 통합](/help/sites-administering/campaignonpremise.md)을 참조하십시오.

## 예제 1: AEM to Adobe Campaign {#example-aem-to-adobe-campaign}

AEM과 Campaign 간의 표준 통합은 JSON 및 JSSP(JavaScript 서버 페이지)를 기반으로 합니다. 이러한 JSSP 파일은 Campaign 콘솔에서 찾을 수 있으며 모두 **aec**(Adobe Experience Cloud)로 시작합니다.

![chlimage_1-15](assets/chlimage_1-15a.png)

이 예에서는 새로운 사용자 정의 JSSP 파일이 만들어지고 AEM 측에서 해당 파일을 호출하여 결과를 검색합니다. 예를 들어 Adobe Campaign에서 데이터를 검색하거나 Adobe Campaign에 데이터를 저장하는 데 사용할 수 있습니다.

1. Adobe Campaign에서 JSSP 파일을 만들려면 **새로 만들기** 아이콘을 클릭합니다.

   ![왼쪽 상단 모서리 근처에 별표가 있는 페이지에 표시된 새 아이콘](do-not-localize/chlimage_1-4a.png)

1. 이 JSSP 파일의 이름을 입력합니다. 이 예제에서는 **cus:custom.jssp**&#x200B;를 사용합니다(**cus** 네임스페이스에 있음).

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. jssp 파일 내에 다음 코드를 넣습니다.

   ```
   <%
   var origin = request.getParameter("origin");
   document.write("Hello from Adobe Campaign, origin : " + origin);
   %>
   ```

1. 작업 내용을 저장합니다. 남은 작업은 AEM에 있습니다.
1. 이 JSSP를 호출할 수 있도록 AEM 측에서 간단한 서블릿을 만듭니다. 이 예에서는 다음과 같이 가정할 수 있습니다.

   * AEM과 Campaign 간에 연결이 작동합니다.
   * Campaign 클라우드 서비스가 **/content/geometrixx-outdoors**&#x200B;에 구성되어 있습니다.

   이 예제에서 가장 중요한 개체는 Adobe Campaign 측에서 jssp 파일을 호출(가져오기 및 게시)할 수 있는 **GenericCampaignConnector**&#x200B;입니다.

   다음은 작은 코드 조각입니다.

   ```
   @Reference
   private GenericCampaignConnector campaignConnector;
   ...
   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
   ```

1. 이 예에서는 자격 증명을 호출에 전달해야 합니다. Campaign 클라우드 서비스가 구성된 페이지에서 를 전달하는 getCredentials() 메서드를 통해 가져올 수 있습니다.

   ```xml
   // page containing the cloudservice for Adobe Campaign
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);
   ```

전체 코드는 다음과 같습니다.

```java
import java.io.IOException;
import java.io.PrintWriter;
import java.util.HashMap;
import java.util.Map;

import javax.servlet.ServletException;

import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.sling.SlingServlet;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.mcm.campaign.CallResults;
import com.day.cq.mcm.campaign.CampaignCredentials;
import com.day.cq.mcm.campaign.GenericCampaignConnector;
import com.day.cq.wcm.api.Page;
import com.day.cq.wcm.api.PageManager;
import com.day.cq.wcm.api.PageManagerFactory;
import com.day.cq.wcm.webservicesupport.Configuration;

@SlingServlet(paths="/bin/campaign", methods="GET")
public class CustomServlet extends SlingSafeMethodsServlet {

 private final Logger log = LoggerFactory.getLogger(this.getClass());

 @Reference
 private GenericCampaignConnector campaignConnector;

 @Reference
 private PageManagerFactory pageManagerFactory;

 @Override
 protected void doGet(SlingHttpServletRequest request,
   SlingHttpServletResponse response) throws ServletException,
   IOException {

  PageManager pm = pageManagerFactory.getPageManager(request.getResourceResolver());

  Page page = pm.getPage("/content/geometrixx-outdoors");

  String result = null;
  if ( page != null) {
   result = callCustomFunction(page);
  }
  if ( result != null ) {
   PrintWriter pw = response.getWriter();
   pw.print(result);
  }
 }

 private String callCustomFunction(Page page ) {
  try {
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);

   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
  } catch (Exception e ) {
   log.error("Something went wrong during the connection", e);
  }
  return null;

 }

}
```

## 예제 2: Adobe Campaign to AEM {#example-adobe-campaign-to-aem}

AEM은 siteadmin 탐색기 보기의 어느 위치에서나 사용 가능한 개체를 검색할 수 있는 기본 API를 제공합니다.

![chlimage_1-17](assets/chlimage_1-17a.png)

탐색기의 각 노드에 대해 연결된 API가 있습니다. 예를 들어 노드의 경우:

* [http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommendations](http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends)

API:

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommendations.1.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

URL **.1.json**&#x200B;의 끝은 가져오려는 하위 수준의 수에 따라 **.2.json**, **.3.json**(으)로 바꿀 수 있습니다. 모두 키워드를 얻으려면 **무한**&#x200B;을(를) 사용할 수 있습니다.

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.infinity.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

API를 사용하려면 기본적으로 AEM에서 기본 인증을 사용합니다.

이름이 **amcIntegration.js**&#x200B;인 JS 라이브러리는 여러 다른 라이브러리 간에 해당 논리를 구현하는 6.1.1(빌드 8624 이상)에서 사용할 수 있습니다.

### AEM API 호출 {#aem-api-call}

```java
loadLibrary("nms:amcIntegration.js");

var cmsAccountId = sqlGetInt("select iExtAccountId from NmsExtAccount where sName=$(sz)","aemInstance")
var cmsAccount = nms.extAccount.load(String(cmsAccountId));
var cmsServer = cmsAccount.server;

var request = new HttpClientRequest(cmsServer+"/content/campaigns/geometrixx.infinity.json")
aemAddBasicAuthentication(cmsAccount, request);
request.method = "GET"
request.header["Content-Type"] = "application/json; charset=UTF-8";
request.execute();
var response = request.response;
```
