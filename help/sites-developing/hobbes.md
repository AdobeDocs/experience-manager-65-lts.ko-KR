---
title: UI 테스트
description: AEM은 AEM UI에 대한 테스트 자동화를 위한 프레임워크를 제공합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 8f00a86f-0fd0-480d-84a9-89a948840a0b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 3%

---

# UI 테스트{#testing-your-ui}

>[!NOTE]
>
>AEM 6.5 이상에서는 hobbes.js UI 테스트 프레임워크가 더 이상 사용되지 않습니다. Adobe은 추가 개선 사항을 계획하고 있지 않으며 고객에게 Selenium 자동화를 사용할 것을 권장합니다.
>

AEM은 AEM UI에 대한 테스트를 자동화하는 프레임워크를 제공합니다. 프레임워크를 사용하여 웹 브라우저에서 직접 UI 테스트를 작성하고 실행합니다. 프레임워크는 테스트 생성을 위한 JavaScript API를 제공합니다.

AEM 테스트 프레임워크는 JavaScript에서 작성된 테스트 라이브러리인 Hobbes.js를 사용합니다. Hobbes.js 프레임워크는 개발 프로세스의 일부로 AEM을 테스트하기 위해 개발되었습니다. 이제 프레임워크를 AEM 애플리케이션 테스트에 공개적으로 사용할 수 있습니다.

>[!NOTE]
>
>API에 대한 자세한 내용은 Hobbes.js [설명서](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html)를 참조하십시오.

## 테스트 구조 {#structure-of-tests}

AEM 내에서 자동화된 테스트를 사용할 때 다음 용어를 이해하는 것이 중요합니다.

| 작업 | **작업**&#x200B;은(는) 링크 또는 단추를 클릭하는 것과 같은 웹 페이지의 특정 활동입니다. |
|---|---|
| 테스트 사례 | **테스트 사례**&#x200B;은(는) 하나 이상의 **작업**(으)로 구성할 수 있는 특정 상황입니다. |
| 테스트 세트 | **테스트 도구 모음**&#x200B;은(는) 특정 사용 사례를 함께 테스트하는 관련 **테스트 사례** 그룹입니다. |

## 테스트 실행 {#executing-tests}

### 테스트 세트 보기 {#viewing-test-suites}

테스트 콘솔을 열어 등록된 테스트 세트를 확인합니다. 테스트 패널에는 테스트 세트와 테스트 사례 목록이 포함되어 있습니다.

**전역 탐색 > 도구 > 작업 > 테스트**&#x200B;를 통해 도구 콘솔로 이동합니다.

![chlimage_1-63](assets/chlimage_1-63.png)

콘솔을 열면 테스트 세트 가 왼쪽의 목록과 함께 모든 테스트 세트를 순서대로 실행합니다. 체크무늬 배경과 함께 표시되는 오른쪽의 공간은 테스트가 실행될 때 페이지 콘텐츠를 표시하기 위한 자리 표시자입니다.

![chlimage_1-64](assets/chlimage_1-64.png)

### 단일 테스트 세트 실행 {#running-a-single-test-suite}

테스트 세트는 개별적으로 실행할 수 있습니다. 테스트 세트를 실행하면 테스트 사례 및 해당 작업이 실행되고 테스트 완료 후 결과가 표시되면서 페이지가 변경됩니다. 아이콘은 결과를 나타냅니다.

확인 표시 아이콘은 합격한 테스트를 나타냅니다.

![확인 표시 아이콘](do-not-localize/chlimage_1-2.png)

&quot;X&quot; 아이콘은 실패한 테스트를 나타냅니다.

![원형 안에 X로 표시된 테스트 아이콘이 실패했습니다.](do-not-localize/chlimage_1-3.png)

테스트 세트를 실행하려면:

1. [테스트] 패널에서 실행할 테스트 사례의 이름을 클릭하여 작업의 세부 정보를 확장합니다.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. **테스트 실행**&#x200B;을 클릭합니다.

   ![테스트 실행 단추의 이미지로, 원 안에 있는 오른쪽 포인터가 표시됩니다.](do-not-localize/chlimage_1-4.png)

1. 자리 표시자는 테스트가 실행될 때 페이지 콘텐츠로 대체됩니다.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 설명을 탭하거나 클릭하여 **결과** 패널을 열어 테스트 사례의 결과를 검토하십시오. **결과** 패널에서 테스트 사례 이름을 탭하거나 클릭하면 모든 세부 정보가 표시됩니다.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 여러 테스트 실행 {#running-multiple-tests}

테스트 세트는 콘솔에 표시되는 순서로 순차적으로 실행됩니다. 테스트로 드릴다운하여 자세한 결과를 확인할 수 있습니다.

![chlimage_1-68](assets/chlimage_1-68.png)

1. 테스트 패널에서 실행할 테스트 세트의 제목 아래에 있는 **모든 테스트 실행** 단추 또는 **테스트 실행** 단추를 클릭합니다.

   ![원 안에 있는 오른쪽 포인터로 표시된 모든 테스트 실행 단추와 테스트 실행 단추의 이미지입니다.](do-not-localize/chlimage_1-5.png)

1. 각 테스트 사례의 결과를 보려면 테스트 사례의 제목을 클릭합니다. **결과** 패널에서 테스트 이름을 클릭하면 모든 세부 정보가 표시됩니다.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 간단한 테스트 세트 만들기 및 사용 {#creating-and-using-a-simple-test-suite}

다음 절차에서는 [We.Retail 콘텐츠](/help/sites-developing/we-retail.md)를 사용하여 테스트 도구 모음을 만들고 실행하는 과정을 단계별로 안내하지만, 다른 웹 페이지를 사용하도록 테스트를 쉽게 수정할 수 있습니다.

고유한 테스트 세트 만들기에 대한 자세한 내용은 [Hobbes.js API 설명서](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html)를 참조하십시오.

1. CRXDE Lite을 엽니다. ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. `/etc/clientlibs` 폴더를 마우스 오른쪽 단추로 클릭하고 **만들기 > 폴더 만들기**&#x200B;를 클릭합니다. `myTests` 이름을 입력하고 **확인**&#x200B;을 클릭합니다.
1. `/etc/clientlibs/myTests` 폴더를 마우스 오른쪽 단추로 클릭하고 **만들기 > 노드 만들기**&#x200B;를 클릭합니다. 다음 속성 값을 사용한 다음 **확인**&#x200B;을 클릭합니다.

   * 이름: `myFirstTest`
   * 유형: `cq:ClientLibraryFolder`

1. myFirstTest 노드에 다음 속성을 추가합니다.

   | 이름 | 유형 | 값 |
   |---|---|---|
   | `categories` | 문자열[] | `granite.testing.hobbes.tests` |
   | `dependencies` | 문자열[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**AEM Forms 전용**
   >
   >
   >적응형 양식을 테스트하려면 범주 및 종속 항목에 다음 값을 추가하십시오. 예:
   >
   >
   >**범주**: `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**종속성**: `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. **모두 저장**&#x200B;을 클릭합니다.
1. `myFirstTest` 노드를 마우스 오른쪽 단추로 클릭하고 **만들기 > 파일 만들기**&#x200B;를 클릭합니다. 파일 이름을 `js.txt`로 지정하고 **확인**&#x200B;을 클릭합니다.
1. `js.txt` 파일에 다음 텍스트를 입력하십시오.

   ```
   #base=.
   myTestSuite.js
   ```

1. **모두 저장**&#x200B;을 클릭한 다음 `js.txt` 파일을 닫습니다.
1. `myFirstTest` 노드를 마우스 오른쪽 단추로 클릭하고 **만들기 > 파일 만들기**&#x200B;를 클릭합니다. 파일 이름을 `myTestSuite.js`로 지정하고 **확인**&#x200B;을 클릭합니다.
1. 다음 코드를 `myTestSuite.js` 파일에 복사한 다음 파일을 저장합니다.

   ```
   new hobs.TestSuite("Experience Content Test Suite", {path:"/etc/clientlibs/myTests/myFirstTest/myTestSuite.js"})
      .addTestCase(new hobs.TestCase("Navigate to Experience Content")
         .navigateTo("/content/we-retail/us/en/experience/arctic-surfing-in-lofoten.html")
      )
      .addTestCase(new hobs.TestCase("Hover Over Topnav")
         .mouseover("li.visible-xs")
      )
      .addTestCase(new hobs.TestCase("Click Topnav Link")
         .click("li.active a")
   );
   ```

1. 테스트 도구 모음을 사용하려면 **테스트** 콘솔로 이동하십시오.
