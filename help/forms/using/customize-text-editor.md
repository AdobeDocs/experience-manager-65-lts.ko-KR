---
title: 텍스트 편집기 사용자 지정
description: Adobe Experience Manager Forms 환경에서 텍스트 편집기를 사용자 지정하는 방법을 알아봅니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: fbe61ef4-1045-49f7-8280-4bc74288cbec
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 1%

---

# 텍스트 편집기 사용자 지정{#customize-text-editor}

## 개요 {#overview}

Assets 관리 및 서신 UI 만들기에서 텍스트 편집기를 사용자 지정하여 더 많은 글꼴과 글꼴 크기를 추가할 수 있습니다. 이러한 글꼴에는 영어 및 일본어 글꼴과 같은 비영어가 포함됩니다.

글꼴 설정에서 다음을 변경하도록 사용자 지정할 수 있습니다.

* 글꼴 패밀리 및 크기
* 높이 및 문자 간격 같은 속성
* 글꼴 패밀리 및 크기, 높이, 문자 간격 및 날짜 형식의 기본값
* 글머리 기호 들여쓰기

다음 작업을 수행합니다.

1. [CRX에서 tbxeditor-config.xml 파일을 편집하여 글꼴 사용자 지정](#customizefonts)
1. [클라이언트 컴퓨터에 사용자 정의 글꼴 추가](#addcustomfonts)

## CRX에서 tbxeditor-config.xml 파일을 편집하여 글꼴 사용자 지정 {#customizefonts}

tbxeditor-config.xml 파일을 편집하여 글꼴을 사용자 정의하려면 다음을 수행합니다.

1. `https://'[server]:[port]'/[ContextPath]/crx/de`(으)로 이동하여 관리자로 로그인합니다.
1. 앱 폴더에서 다음 단계를 사용하여 config 폴더(libs/fd/cm/config)와 유사한 경로/구조로 config 라는 폴더를 만듭니다.

   1. 다음 경로에서 항목 폴더를 마우스 오른쪽 단추로 클릭하고 **오버레이 노드**&#x200B;를 선택합니다.

      `/libs/fd/cm/config`

      ![오버레이 노드](assets/1-1.png)

   1. 오버레이 노드 대화 상자에 다음 값이 있는지 확인합니다.

      **경로:** /libs/fd/cm/config

      **위치:** /apps/

      **노드 유형 일치:** 선택됨

      ![오버레이 노드](assets/2.png)

   1. **확인**&#x200B;을 클릭합니다. 폴더 구조는 앱 폴더에 생성됩니다.

   1. **모두 저장**&#x200B;을 클릭합니다.

1. 새로 생성된 구성 폴더에 다음 단계를 사용하여 tbxeditor-config.xml 파일의 복사본을 만듭니다.

   1. libs/fd/cm/config에서 tbxeditor-config.xml 파일을 마우스 오른쪽 단추로 클릭하고 **복사**&#x200B;를 선택합니다.
   1. 다음 폴더를 마우스 오른쪽 단추로 클릭하고 **붙여넣기:**&#x200B;를 선택합니다

      `apps/fd/cm/config`

   1. 붙여넣은 파일의 이름은 기본적으로 `copy of tbxeditor-config.xml.`입니다. 파일 이름을 `tbxeditor-config.xml`(으)로 변경하고 **모두 저장**&#x200B;을 클릭합니다.

1. apps/fd/cm/config에서 tbxeditor-config.xml 파일을 연 다음 필요한 사항을 변경합니다.

   1. apps/fd/cm/config에서 tbxeditor-config.xml 파일을 두 번 클릭합니다. 파일이 열립니다.

      ```xml
      <editorConfig>
         <bulletIndent>0.25in</bulletIndent>
      
         <defaultDateFormat>DD-MM-YYYY</defaultDateFormat>
      
         <fonts>
            <default>Times New Roman</default>
            <font>_sans</font>
            <font>_serif</font>
            <font>_typewriter</font>
            <font>Arial</font>
            <font>Courier</font>
            <font>Courier New</font>
            <font>Geneva</font>
            <font>Georgia</font>
            <font>Helvetica</font>
            <font>Tahoma</font>
            <font>Times New Roman</font>
            <font>Times</font>
            <font>Verdana</font>
         </fonts>
      
         <fontSizes>
            <default>12</default>
            <fontSize>8</fontSize>
            <fontSize>9</fontSize>
            <fontSize>10</fontSize>
            <fontSize>11</fontSize>
            <fontSize>12</fontSize>
            <fontSize>14</fontSize>
            <fontSize>16</fontSize>
            <fontSize>18</fontSize>
            <fontSize>20</fontSize>
            <fontSize>22</fontSize>
            <fontSize>24</fontSize>
            <fontSize>26</fontSize>
            <fontSize>28</fontSize>
            <fontSize>36</fontSize>
            <fontSize>48</fontSize>
            <fontSize>72</fontSize>
         </fontSizes>
      
         <lineHeights>
            <default>2</default>     
            <lineHeight>2</lineHeight>
            <lineHeight>3</lineHeight>
            <lineHeight>4</lineHeight>
            <lineHeight>5</lineHeight>
            <lineHeight>6</lineHeight>
            <lineHeight>7</lineHeight>
            <lineHeight>8</lineHeight>
            <lineHeight>9</lineHeight>
            <lineHeight>10</lineHeight>
            <lineHeight>11</lineHeight>
            <lineHeight>12</lineHeight>
            <lineHeight>13</lineHeight>
            <lineHeight>14</lineHeight>
            <lineHeight>15</lineHeight>
            <lineHeight>16</lineHeight>
         </lineHeights>
      
         <letterSpacings>
            <default>0</default>
            <letterSpacing>0</letterSpacing>
            <letterSpacing>1</letterSpacing>
            <letterSpacing>2</letterSpacing>
            <letterSpacing>3</letterSpacing>
            <letterSpacing>4</letterSpacing>
            <letterSpacing>5</letterSpacing>
            <letterSpacing>6</letterSpacing>
            <letterSpacing>7</letterSpacing>
            <letterSpacing>8</letterSpacing>
            <letterSpacing>9</letterSpacing>
            <letterSpacing>10</letterSpacing>
            <letterSpacing>11</letterSpacing>
            <letterSpacing>12</letterSpacing>
            <letterSpacing>13</letterSpacing>
            <letterSpacing>14</letterSpacing>
            <letterSpacing>15</letterSpacing>
            <letterSpacing>16</letterSpacing>
         </letterSpacings>
      </editorConfig>
      ```

   1. 글꼴 설정에서 다음을 변경할 수 있도록 파일에서 필요한 사항을 변경합니다.

      * 글꼴 모음 및 크기 추가 또는 제거
      * 높이 및 문자 간격 같은 속성
      * 글꼴 패밀리 및 크기, 높이, 문자 간격 및 날짜 형식의 기본값
      * 글머리 기호 들여쓰기

      예를들어 Sazanami Mincho Medium라는 일본어 글꼴을 추가하려면 XML 파일에 다음 항목을 만들어야 합니다. `<font>Sazanami Mincho Medium</font>`. 또한 글꼴 사용자 지정에 액세스하고 작업하는 데 사용되는 클라이언트 시스템에도 이 글꼴이 설치되어 있어야 합니다. 자세한 내용은 [클라이언트 컴퓨터에 사용자 지정 글꼴 추가](#addcustomfonts)를 참조하십시오.

      텍스트의 다양한 측면에 대한 기본값을 변경하고 항목을 제거하여 텍스트 편집기에서 글꼴을 제거할 수도 있습니다.

   1. **모두 저장**&#x200B;을 클릭합니다.

## 클라이언트 컴퓨터에 사용자 정의 글꼴 추가 {#addcustomfonts}

서신 관리 텍스트 편집기에서 글꼴에 액세스할 때 서신 관리에 액세스하는 데 사용하는 클라이언트 시스템에 글꼴이 있어야 합니다. 텍스트 편집기에서 사용자 지정 글꼴을 사용하려면 먼저 클라이언트 컴퓨터에 해당 글꼴을 설치해야 합니다.

글꼴 설치에 대한 자세한 내용은 다음을 참조하십시오.

* [Windows에서 글꼴 설치 또는 제거](https://windows.microsoft.com/en-us/windows-vista/install-or-uninstall-fonts)
* [Mac 기본 사항: 글꼴 책](https://support.apple.com/en-us/HT201749)

## 글꼴 사용자 지정 액세스 {#access-font-customizations}

CRX에서 `tbxeditor-config.xml` 파일의 글꼴을 변경하고 AEM Forms에 액세스하는 데 사용되는 클라이언트 컴퓨터에 필요한 글꼴을 설치한 후 변경 내용이 텍스트 편집기에 나타납니다.

예를 들어, [CRX에서 tbxeditor-config.xml 파일을 편집하여 글꼴 사용자 지정](#customizefonts) 절차에 추가된 Sazanami Mincho Medium 글꼴이 텍스트 편집기 UI에 다음과 같이 표시됩니다.

![sazanamiminchointext](assets/sazanamiminchointext.png)

>[!NOTE]
>
>일본어 텍스트를 보려면 먼저 일본어 문자로 텍스트를 입력해야 합니다. 사용자 정의 일본어 글꼴을 적용하면 특정 방식으로만 텍스트 서식을 지정할 수 있습니다. 사용자 정의 일본어 글꼴을 적용해도 영어나 다른 문자가 일본어 문자로 변경되지 않습니다.
