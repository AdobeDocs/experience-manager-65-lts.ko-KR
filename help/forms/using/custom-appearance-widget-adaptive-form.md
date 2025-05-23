---
title: 적응형 양식 필드에 대한 사용자 정의 표시 만들기
description: 적응형 Forms에서 즉시 사용 가능한 구성 요소의 모양을 사용자 지정합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
exl-id: c8745d19-139a-4cea-982a-537bc1dd207d
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1702'
ht-degree: 0%

---

# 적응형 양식 필드에 대한 사용자 정의 표시 만들기{#create-custom-appearances-for-adaptive-form-fields}

## 소개 {#introduction}

적응형 양식은 [모양 프레임워크](/help/forms/using/introduction-widgets.md)를 사용하여 적응형 양식 필드에 대한 사용자 지정 모양을 만들고 다른 사용자 경험을 제공할 수 있습니다. 예를 들어, 라디오 단추 및 확인란을 토글 단추로 바꾸거나 사용자 지정 jQuery 플러그인을 사용하여 전화번호 또는 이메일 ID와 같은 필드에서 사용자 입력을 제한합니다.

이 문서에서는 jQuery 플러그인을 사용하여 적응형 양식 필드에 대한 이러한 대체 경험을 만드는 방법을 설명합니다. 또한 숫자 필드 구성 요소가 숫자 스텝퍼 또는 슬라이더로 표시되도록 하기 위한 사용자 지정 모양을 만드는 예를 보여 줍니다.

이 글에서 사용되는 주요 용어와 개념에 대해 먼저 살펴보자.

**모양**&#x200B;은(는) 적응형 양식 필드의 스타일, 모양 및 느낌, 다양한 요소 구성을 나타냅니다. 일반적으로 레이블, 입력을 제공하는 대화형 영역, 도움말 아이콘, 필드에 대한 짧고 긴 설명이 포함됩니다. 이 문서에서 설명하는 외관의 사용자 지정은 필드의 입력 영역의 외관에 적용할 수 있습니다.

**jQuery 플러그인** jQuery 위젯 프레임워크를 기반으로 대체 모양을 구현하는 표준 메커니즘을 제공합니다.

**ClientLib** 복잡한 JavaScript 및 CSS 코드로 구동되는 AEM 클라이언트측 처리에 있는 클라이언트측 라이브러리 시스템입니다. 자세한 내용은 클라이언트측 라이브러리 사용을 참조하십시오.

**Archetype** Maven 프로젝트의 원래 패턴 또는 모델로 정의된 Maven 프로젝트 템플릿 도구 키트 자세한 내용은 Archetype 소개를 참조하십시오.

**사용자 정의 컨트롤**&#x200B;은(는) 필드의 값을 포함하는 위젯의 기본 요소를 참조하며, 사용자 정의 위젯 UI를 적응형 양식 모델과 바인딩하기 위해 모양 프레임워크에서 사용됩니다.

## 사용자 정의 모양을 만드는 단계 {#steps-to-create-a-custom-appearance}

높은 수준에서 사용자 정의 모양을 만드는 단계는 다음과 같습니다.

1. **프로젝트 만들기**: AEM에 배포할 콘텐츠 패키지를 생성하는 Maven 프로젝트를 만듭니다.
1. **기존 위젯 클래스 확장**: 기존 위젯 클래스를 확장하고 필요한 클래스를 재정의합니다.
1. **클라이언트 라이브러리 만들기**: `clientLib: af.customwidget` 라이브러리를 만들고 필요한 JavaScript 및 CSS 파일을 추가합니다.

1. **프로젝트 빌드 및 설치**: Maven 프로젝트를 빌드하고 AEM에 생성된 콘텐츠 패키지를 설치합니다.
1. **적응형 양식을 업데이트하십시오**: 사용자 지정 모양을 사용하려면 적응형 양식 필드 속성을 업데이트하십시오.

### 프로젝트 만들기 {#create-a-project}

Maven Archetype은 사용자 정의 모양을 만드는 시작점입니다. 사용할 Archetype의 세부 내용은 다음과 같습니다.

* **저장소**: https://repo1.maven.org/maven2/com/adobe/
* **아티팩트 ID**: custom-appearance-archetype
* **그룹 ID**: com.adobe.aemforms
* **버전**: 1.0.4

다음 명령을 실행하여 Archetype을 기반으로 로컬 프로젝트를 생성합니다.

`mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

이 명령은 저장소에서 Maven 플러그인 및 Archetype 정보를 다운로드하고 다음 정보를 기반으로 프로젝트를 생성합니다.

* **groupId**: 생성된 Maven 프로젝트에서 사용되는 그룹 ID
* **artifactId**: 생성된 Maven 프로젝트에서 사용되는 아티팩트 ID입니다.
* **버전**: 생성된 Maven 프로젝트의 버전입니다.
* **package**: 파일 구조에 사용되는 패키지입니다.
* **artifactName**: 생성된 AEM 패키지의 아티팩트 이름입니다.
* **packageGroup**: 생성된 AEM 패키지의 패키지 그룹입니다.
* **widgetName**: 참조에 사용되는 모양 이름입니다.

생성된 프로젝트의 구조는 다음과 같습니다.

```java
─<artifactId>

 └───src

     └───main

         └───content

             └───jcr_root

                 └───etc

                     └───clientlibs

                         └───custom

                             └───<widgetName>

                                 ├───common [client library - af.customwidgets which encapsulates below clientLibs]

                                 ├───integration [client library - af.customwidgets.<widgetName>_widget which contains template files for integrating a third-party plugin with Adaptive Forms]

                                 │   ├───css

                                 │   └───javascript

                                 └───jqueryplugin [client library - af.customwidgets.<widgetName>_plugin which holds the third-party plugins and related dependencies]

                                     ├───css

                                     └───javascript
```

### 기존 위젯 클래스 확장 {#extend-an-existing-widget-class}

프로젝트 템플릿이 생성되면 필요에 따라 다음 사항을 변경합니다.

1. 프로젝트에 서드파티 플러그인 종속성을 포함합니다.

   1. 타사 또는 사용자 지정 jQuery 플러그인을 `jqueryplugin/javascript` 폴더에 배치하고 관련 CSS 파일을 `jqueryplugin/css` 폴더에 배치합니다. 자세한 내용은 `jqueryplugin/javascript and jqueryplugin/css` 폴더 아래의 JS 및 CSS 파일을 참조하십시오.

   1. jQuery 플러그인의 추가 JavaScript 및 CSS 파일을 포함하도록 `js.txt` 및 `css.txt` 파일을 수정하십시오.

1. 서드파티 플러그인을 프레임워크와 통합하여 사용자 지정 모양 프레임워크와 jQuery 플러그인 간의 상호 작용을 가능하게 합니다. 새 위젯은 다음 기능을 확장하거나 재정의한 후에만 작동합니다.

<table>
 <tbody>
  <tr>
   <td><strong>함수</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>렌더링 함수는 위젯의 기본 HTML 요소에 대한 jQuery 개체를 반환합니다. 기본 HTML 요소는 집중 가능한 유형이어야 합니다. 예: <code>&lt;a&gt;</code>, <code>&lt;input&gt;</code> 및 <code>&lt;li&gt;</code>. 반환된 요소가 <code>$userControl</code>(으)로 사용됩니다. <code>$userControl</code>이(가) 위의 제약 조건을 지정하면 <code>AbstractWidget</code> 클래스의 함수가 예상대로 작동하고, 그렇지 않으면 일부 공통 API(포커스, 클릭)를 변경해야 합니다. </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>HTML 이벤트를 XFA 이벤트로 변환하는 맵을 반환합니다. <br /> <code class="code">&lbrace;
      blur: XFA_EXIT_EVENT,
      &rbrace;</code><br /> 이 예제는 <code>blur</code>이(가) HTML 이벤트이고 <code>XFA_EXIT_EVENT</code>이(가) 해당 XFA 이벤트임을 보여 줍니다. </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>옵션 변경 시 수행할 작업에 대한 세부 정보를 제공하는 맵을 반환합니다. 키는 위젯에 제공되는 옵션이며 값은 옵션의 변경이 감지될 때마다 호출되는 함수입니다. 위젯은 모든 일반 옵션(<code>value</code> 및 <code>displayValue</code> 제외)에 대한 처리기를 제공합니다.</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>jQuery 위젯 프레임워크는 jQuery 위젯의 값이 XFA 모델에 저장될 때마다(예: 텍스트 필드의 종료 이벤트에서) 함수를 로드합니다. 구현은 위젯에 저장된 값을 반환해야 합니다. 핸들러에 옵션에 대한 새 값이 제공됩니다.</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>기본적으로 XFA on Enter 이벤트에서 필드의 <code>rawValue</code>이(가) 표시됩니다. 이 함수는 사용자에게 <code>rawValue</code>을(를) 표시하기 위해 호출됩니다. </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>기본적으로 종료 시 XFA에서는 필드의 <code>formattedValue</code>이(가) 표시됩니다. 이 함수는 사용자에게 <code>formattedValue</code>을(를) 표시하기 위해 호출됩니다. </td>
  </tr>
 </tbody>
</table>

1. 필요에 따라 `integration/javascript` 폴더에서 JavaScript 파일을 업데이트합니다.

   * `__widgetName__` 텍스트를 실제 위젯 이름으로 바꾸십시오.
   * 적절한 기본 위젯 클래스에서 위젯을 확장합니다. 대개의 경우 기존 위젯이 대체되는 것에 해당하는 위젯 클래스이다. 부모 클래스 이름이 여러 위치에서 사용되므로 파일에서 문자열 `xfaWidget.textField`의 모든 인스턴스를 검색하고 사용된 실제 부모 클래스로 바꾸는 것이 좋습니다.
   * `render` 메서드를 확장하여 대체 UI를 제공하십시오. UI 또는 상호 작용 동작을 업데이트하기 위해 jQuery 플러그인을 호출하는 위치입니다. `render` 메서드는 사용자 제어 요소를 반환해야 합니다.

   * `getOptionsMap` 메서드를 확장하여 위젯의 변경으로 인해 영향을 받는 모든 옵션 설정을 재정의합니다. 함수는 옵션 변경 시 수행할 작업에 대한 세부 정보를 제공하는 매핑을 반환합니다. 키는 위젯에 제공되는 옵션이며 값은 옵션의 변경이 감지될 때마다 호출되는 함수입니다.
   * `getEventMap` 메서드는 위젯에 의해 트리거된 이벤트를 적응형 양식 모델에 필요한 이벤트와 매핑합니다. 기본값은 기본 위젯에 대한 표준 HTML 이벤트를 매핑하며 대체 이벤트가 트리거되는 경우 업데이트해야 합니다.
   * `showDisplayValue` 및 `showValue`은(는) 표시 및 편집 그림 절을 적용하고 대체 동작을 갖도록 재정의할 수 있습니다.

   * `commit` 이벤트가 발생할 때 적응형 양식 프레임워크에서 `getCommitValue` 메서드를 호출합니다. 일반적으로 종료 이벤트입니다. 단, 드롭다운, 라디오 단추 및 변경 시 발생하는 확인란 요소는 예외입니다. 자세한 내용은 [적응형 Forms 표현식](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p)을 참조하십시오.

   * 템플릿 파일은 다양한 방법에 대한 샘플 구현을 제공합니다. 확장하지 않을 메서드를 제거합니다.

### 클라이언트 라이브러리 만들기 {#create-a-client-library}

Maven Archetype에서 생성된 샘플 프로젝트는 필요한 클라이언트 라이브러리를 자동으로 만들고 범주 `af.customwidgets`을(를) 가진 클라이언트 라이브러리로 래핑합니다. `af.customwidgets`에서 사용할 수 있는 JavaScript 및 CSS 파일은 런타임에 자동으로 포함됩니다.

### 빌드 및 설치 {#build-and-install}

프로젝트를 빌드하려면 셸에서 다음 명령을 실행하여 AEM 서버에 설치해야 하는 CRX 패키지를 생성합니다.

`mvn clean install`

>[!NOTE]
>
>Maven 프로젝트는 POM 파일 내의 원격 저장소를 나타냅니다. 이는 참조용으로만 사용되며 Maven 표준에 따라 저장소 정보가 `settings.xml` 파일에 캡처됩니다.

### 적응형 양식 업데이트 {#update-the-adaptive-form}

적응형 양식 필드에 사용자 정의 모양을 적용하려면 다음을 수행합니다.

1. 편집 모드에서 적응형 양식을 엽니다.
1. 사용자 지정 모양을 적용할 필드의 **속성** 대화 상자를 엽니다.
1. **스타일** 탭에서 `CSS class` 속성을 업데이트하여 `widget_<widgetName>` 형식의 모양 이름을 추가합니다. 예: **widget_numericstepper**

## 샘플: 사용자 정의 모양 만들기   {#sample-create-a-custom-appearance-nbsp}

이제 숫자 필드가 숫자 스텝퍼 또는 슬라이더로 표시되도록 하는 사용자 지정 모양을 만드는 예를 살펴보겠습니다. 다음 단계를 수행하십시오.

1. 다음 명령을 실행하여 Maven Archetype을 기반으로 로컬 프로젝트를 생성합니다.

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   다음 매개변수에 대한 값을 지정하라는 메시지가 표시됩니다.
   *이 샘플에서 사용된 값은 굵게 강조 표시되어 있습니다*.

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. `customWidgets`(`artifactID` 속성에 대해 지정된 값) 디렉터리로 이동하고 다음 명령을 실행하여 Eclipse 프로젝트를 생성합니다.

   `mvn eclipse:eclipse`

1. Eclipse 도구를 열고 다음을 수행하여 Eclipse 프로젝트를 가져옵니다.

   1. **[!UICONTROL 파일 > 가져오기 > Workspace으로 기존 프로젝트]**&#x200B;를 선택합니다.

   1. `archetype:generate` 명령을 실행한 폴더를 찾아 선택합니다.

   1. **[!UICONTROL 마침]**&#x200B;을 클릭합니다.

      ![eclipse-screenshot](assets/eclipse-screenshot.png)

1. 사용자 정의 모양새에 사용할 위젯을 선택합니다. 이 샘플은 다음 숫자 스텝퍼 위젯을 사용합니다.

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   Eclipse 프로젝트에서 `plugin.js` 파일의 플러그인 코드를 검토하여 모양 요구 사항과 일치하는지 확인하십시오. 이 샘플에서는 모양이 다음 요구 사항을 충족합니다.

   * 숫자 스텝퍼는 `- $.xfaWidget.numericInput`부터 확장되어야 합니다.
   * 위젯의 `set value` 메서드는 필드에 포커스가 있는 후에 값을 설정합니다. 적응형 양식 위젯에 대한 필수 요구 사항입니다.
   * `bootstrapNumber` 메서드를 호출하려면 `render` 메서드를 재정의해야 합니다.

   * 플러그인의 기본 소스 코드 외에는 플러그인에 대한 추가 종속성이 없습니다.
   * 샘플은 스테퍼에서 스타일링을 수행하지 않으므로 추가 CSS가 필요하지 않습니다.
   * `$userControl` 개체는 `render` 메서드에서 사용할 수 있어야 합니다. 플러그 인 코드로 복제된 `text` 형식의 필드입니다.

   * 필드가 비활성화되어 있으면 **+** 및 **-** 단추를 비활성화해야 합니다.

1. `bootstrap-number-input.js`(jQuery 플러그인)의 내용을 `numericStepper-plugin.js` 파일의 내용으로 바꿉니다.
1. `numericStepper-widget.js` 파일에서 다음 코드를 추가하여 렌더링 메서드를 재정의하여 플러그인을 호출하고 `$userControl` 개체를 반환합니다.

   ```javascript
   render : function() {
        var control = $.xfaWidget.numericInput.prototype.render.apply(this, arguments);
        var $control = $(control);
        var controlObject;
        try{
            if($control){
            $control.bootstrapNumber();
            var id = $control.attr("id");
            controlObject = $("#"+id);
            }
        }catch (exc){
             console.log(exc);
        }
        return controlObject;
   }
   ```

1. `numericStepper-widget.js` 파일에서 `getOptionsMap` 속성을 재정의하여 액세스 옵션을 재정의하고 비활성화 모드에서 + 및 - 단추를 숨깁니다.

   ```javascript
   getOptionsMap: function(){
       var parentOptionsMap = $.xfaWidget.numericInput.prototype.getOptionsMap.apply(this,arguments),
   
       newMap = $.extend({},parentOptionsMap,
   
        {
   
              "access": function(val) {
              switch(val) {
                 case "open" :
                   this.$userControl.removeAttr("readOnly");
                   this.$userControl.removeAttr("aria-readonly");
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
                 case "nonInteractive" :
                 case "protected" :
                   this.$userControl.attr("disabled", "disabled");
                   this.$userControl.attr("aria-disabled", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
                case "readOnly" :
                   this.$userControl.attr("readOnly", "readOnly");
                   this.$userControl.attr("aria-readonly", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
               default :
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
             }
          },
      });
      return newMap;
    }
   ```

1. 변경 내용을 저장하고 `pom.xml` 파일이 포함된 폴더로 이동한 다음, 다음 Maven 명령을 실행하여 프로젝트를 빌드합니다.

   `mvn clean install`

1. AEM 패키지 관리자를 사용하여 패키지를 설치합니다.

1. 사용자 정의 모양을 적용할 편집 모드로 적응형 양식을 열고 다음을 수행합니다.

   1. 모양을 적용할 필드를 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL 편집]**&#x200B;을 클릭하여 구성 요소 편집 대화 상자를 엽니다.

   1. 스타일 탭에서 **[!UICONTROL CSS 클래스]** 속성을 업데이트하여 `widget_numericStepper`을(를) 추가합니다.

새로 만든 모양새를 사용할 수 있습니다.
