---
title: 적응형 양식에서 SOM 표현식 사용
description: 적응형 양식 패널의 SOM 표현식을 추출하는 방법을 알아봅니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms,Foundation Components
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: a2a2a6f3-409e-44a2-a85b-9f0bc40cc800
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 적응형 양식에서 SOM 표현식 사용{#using-som-expressions-in-adaptive-forms}

적응형 양식은 AEM 저장소에서 JCR 콘텐츠 구조로 표시되는 AEM 페이지로 모델링됩니다. 콘텐츠 구조의 주요 요소는 guideContainer 노드입니다. guideContainer 아래에는 중첩된 패널과 필드를 포함할 수 있는 rootPanel이 있습니다.

SOM(스크립팅 개체 모델)을 사용하여 특정 DOM(문서 개체 모델) 내의 값, 속성 및 메서드를 참조할 수 있습니다. DOM은 메모리 개체와 속성을 트리 계층 구조로 구성합니다. SOM 표현식은 필드/그리기 요소 및 패널을 참조합니다.

다음 이미지는 양식에 구성 요소를 추가할 때 적응형 양식이 로 변환되는 노드 구조를 보여 줍니다. 예를 들어, 런타임 시 DOM으로 변환되는 패널과 패널의 라디오 단추에 루트 패널에 패널을 추가할 수 있습니다. 적응형 양식의 라디오 단추 필드에 대한 SOM 식이 `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`(으)로 지정되었습니다.

![DOM 트리](assets/hierarchy.png)

DOM 트리

적응형 양식의 모든 요소에 대한 SOM 식 앞에 `guide[0].guide1[0]`이(가) 있습니다. 노드 구조 계층 구조에서 구성 요소의 위치는 해당 SOM 표현식을 파생하는 데 사용됩니다.

![라디오 단추가 두 개인 DOM 트리](assets/hierarchy_radio_button.png)

라디오 버튼이 두 개인 DOM 트리

적응형 양식에서 라디오 단추의 위치를 변경하면 SOM 표현식이 변경됩니다. 작성 모드에서 SOM 표현식 보기 옵션을 사용하여 AEM Forms 내의 필드 또는 요소에 대한 SOM 표현식을 볼 수 있습니다. 옵션은 필드 또는 요소를 마우스 오른쪽 버튼으로 클릭하면 패널에 표시됩니다.

![적응형 양식에서 SOM 표현식 추출](assets/som-expressions.png)

적응형 양식에서 SOM 표현식 추출

패널 내의 패널 도구 모음에서 기능에 액세스할 수 있습니다. 이 기능을 사용하면 적응형 양식 작성자가 쉽게 스크립팅할 수 있습니다.

![패널 도구 모음을 사용하여 SOM 표현식 추출](assets/som-expression.png)

패널 도구 모음을 사용하여 SOM 표현식 추출

[GuideBridge](https://helpx.adobe.com/kr/aem-forms/6/javascript-api/GuideBridge.html)에 나열된 일부 API는 요소의 SOM 식을 사용합니다. 예를 들어 적응형 양식의 특정 필드에 초점을 맞추려면 해당 SOM 식을 `guideBridge`의 `getFocus`API에 전달하십시오.
