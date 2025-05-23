---
title: 정책 생성 및 관리
description: 정책은 정책이 적용되는 문서에 액세스할 수 있는 기밀 유지 설정 및 사용자 세트입니다. AEM Forms를 사용하여 다양한 유형의 정책을 만들고 관리할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: e8faf76e-5287-4b0c-b440-f348443287f3
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '4725'
ht-degree: 0%

---

# 정책 생성 및 관리 {#creating-and-managing-policies}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

*정책*&#x200B;은(는) 정책이 적용되는 문서에 액세스할 수 있는 기밀 유지 설정 집합 및 사용자를 정의합니다. *정책 집합*&#x200B;은(는) 일반적인 비즈니스 목적을 가진 정책 집합을 그룹화하는 데 사용됩니다. 그런 다음 시스템의 사용자 하위 집합에서 이러한 정책 집합을 사용할 수 있습니다. 정책에 대한 자세한 내용은 [정책 및 정책으로 보호된 문서](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents)를 참조하십시오.

## 정책 유형 {#types-of-policies}

Document Security는 다음과 같은 유형의 정책을 제공합니다.

**개인 정책**

사용자는 특정 상황에 적합한 설정을 사용하여 정책을 생성, 편집, 복사, 삭제 및 적용할 수 있습니다. 정책을 작성한 사람과 관리자만 해당 개인 정책에 액세스할 수 있습니다. 개인 정책은 정책 페이지의 내 정책 탭에 나타납니다.

관리자가 이 기능을 사용하도록 설정한 경우 초대된 사용자는 개인 정책을 만들고, 편집하고, 복사하고, 삭제할 수도 있습니다.

**공유 정책**

관리자 및 정책 세트 코디네이터는 조직이 다양한 유형의 문서 및 사용자에 대해 식별하는 기밀 유지 요구 사항을 기반으로 공유 정책을 생성합니다. 공유 정책은 정책 세트 내에 포함되어 있으며 특정 정책 세트에 대해 권한이 부여된 모든 사용자(문서 게시자, 정책 세트 조정자 및 문서 수신자)가 사용할 수 있습니다. 관리자 및 정책 세트 코디네이터는 공유 정책을 활성화 및 비활성화할 수 있습니다. 공유 정책은 정책 페이지의 정책 세트 탭에 있는 정책 세트에 나타납니다.

문서 보안을 처음 설치하면 *모든 보안 주체로 제한*&#x200B;이라는 공유 정책이 포함됩니다. 이 정책이 문서에 적용되면 문서 보안에 로그인할 수 있는 모든 사용자가 문서에 액세스할 수 있습니다. 이 정책은 이름이 *전역 정책 집합*&#x200B;인 정책 집합에 있습니다. 기본적으로 이 정책은 활성화되어 있지 않습니다. 조직의 요구 사항에 맞는 경우 활성화할 수 있습니다.

**Microsoft® Outlook 자동 생성 정책**

Acrobat을 사용하면 Microsoft® Outlook에서 전자 메일 첨부 파일로 보내는 문서에 정책을 적용할 수 있습니다. Outlook에서는 기존 정책을 사용하여 문서를 보호할 수 있습니다. 또는 Acrobat이 기본 기밀 유지 설정을 사용하여 생성하고 이메일 메시지에 첨부된 문서에 적용되는 자동 생성 정책을 사용할 수 있습니다. (*[Acrobat 도움말](https://help.adobe.com/en_US/acrobat/pro/using/index.html)*&#x200B;을 참조하세요.)

>[!NOTE]
>
>Outlook에서 사용할 수 있는 정책은 Acrobat에서 즐겨찾기로 설정해야 합니다. 게시자인 정책을 포함하여 다른 모든 정책은 Outlook에 표시되지 않습니다.

## 정책 및 정책 세트를 만들고 관리할 수 있는 사용자 {#who-can-create-and-manage-policies-and-policy-sets}

정책 및 정책 집합과 상호 작용하는 방법은 조직 내의 역할에 따라 다릅니다.

**사용자:** 사용자는 개인 정책을 만들고 편집하고 삭제할 수 있습니다. 관리자가 이 기능을 사용하도록 설정한 경우 초대된 사용자는 개인 정책을 만들 수도 있습니다.

**정책 집합 코디네이터:** 정책 집합 코디네이터는 코디네이터로 지정된 정책 집합에서 공유 정책을 만들고 관리할 수 있습니다. 정책 세트 코디네이터는 일반적으로 특정 정책 세트의 정책을 가장 잘 작성할 수 있는 조직의 전문가입니다.

**관리자:** 관리자는 사용자의 개인 정책을 편집할 수 있습니다. 공유 정책을 만들 수 있습니다. 정책 세트를 생성, 편집 및 삭제하고 정책 세트 코디네이터를 지정할 수도 있습니다.

다양한 문서 보안 역할에 대한 자세한 내용은 [문서 보안 사용자 정보](/help/forms/using/admin-help/document-security.md#about-document-security-users)를 참조하십시오.

## 정책 만들기 및 편집 {#creating-and-editing-policies}

사용자는 자신의 사용을 위해 개인 정책을 만들거나 편집할 수 있습니다. 관리자 및 정책 세트 코디네이터는 조직에 대한 공유 정책을 만들거나 편집할 수 있습니다.

### 정책 편집 시 고려 사항 {#considerations-for-editing-policies}

정책을 편집할 때 변경 사항은 정책이 현재 보호하는 문서와 그 이후에 정책이 보호하는 문서에 영향을 줍니다. 예를 들어 문서에 적용된 정책에서 수신자를 제거하면 수신자는 더 이상 문서를 열 수 없습니다.

문서의 상태는 변경 사항의 적용 시기를 결정합니다.

* 문서가 온라인 상태이면 사용자가 문서를 열지 않은 한 변경 사항이 즉시 적용됩니다. 이 경우 변경 사항을 적용하려면 사용자가 문서를 닫아야 합니다.
* 받는 사람이 문서를 오프라인으로(예: 랩톱 컴퓨터에서) 사용하는 경우 다음에 받는 사람이 문서를 온라인으로 가져올 때 변경 사항이 적용됩니다. 그런 다음 정책으로 보호된 문서를 열어 문서 보안과 동기화합니다.

>[!NOTE]
>
>Acrobat에서 Microsoft의 이메일 메시지에 첨부된 문서 수신자를 위해 자동으로 생성하는 정책은 정책 목록에 표시되지 않습니다® 연관된 문서에 대한 문서 세부 정보 페이지를 열어야 이러한 정책을 볼 수 있습니다.

정책을 편집할 때 다음 제한 사항이 적용됩니다.

* 초대된 사용자는 관리자가 이 기능을 활성화한 경우에만 정책을 편집할 수 있습니다. 정책을 편집할 수 없는 경우 편집 옵션을 사용할 수 없습니다.
* 정책 세트 코디네이터는 올바른 권한이 있는 경우에만 정책 세트 내에서 정책을 편집할 수 있습니다. 수퍼 유저 또는 정책 세트 관리자는 문서 보안 관리자 인터페이스에서 이러한 권한을 설정합니다.
* 정책이 생성된 이후 관리자가 삭제하도록 구성된 워터마크가 정책에 있는 경우 정책을 편집하고 저장하면 이 워터마크가 문서에 더 이상 적용되지 않습니다. 삭제된 워터마크는 정책을 편집하지 않는 한 기존 정책에만 적용됩니다. 정책을 편집하는 경우 삭제된 워터마크를 대체할 다른 워터마크를 선택해야 합니다.
* 적용되는 정책을 편집하여 문서에 대한 익명 액세스 권한을 부여할 수 없습니다. 정책을 편집하는 경우에도 사용자가 문서에 액세스하려면 로그인해야 합니다. 이 문서에 익명 액세스를 적용하려면 먼저 클라이언트 응용 프로그램에서 정책을 제거한 다음 익명 액세스를 허용하는 다른 정책을 적용합니다.
* Acrobat Outlook에서 전자 메일 메시지에 첨부된 문서의 수신자를 위해 Microsoft에서 자동으로 생성하는 정책은 정책 목록에 표시되지 않습니다. 이 정책에 액세스하려면 문서 페이지에서 문서를 찾은 다음 문서 세부 정보 페이지를 열고 문서 세부 정보 목록에서 정책 이름을 클릭합니다.

**정책 만들기 또는 편집**

1. 문서 보안 페이지에서 정책 을 클릭하고 다음 탭 중 하나를 클릭합니다.

   * 개인 정책을 만들거나 편집하려면 내 정책 탭을 클릭합니다.
   * 공유 정책을 만들거나 편집하려면 권한이 있는 경우 정책 세트 탭을 클릭하고 적절한 정책 세트 이름을 클릭한 다음 정책 탭을 클릭합니다.

1. 새로 만들기 를 클릭하거나 목록에서 편집할 정책을 선택합니다.
1. 이름 상자에 정책을 고유하게 식별하는 이름을 입력합니다. 설명 상자에서 정책의 역할과 사용 시기를 설명합니다. 정책이 정책 집합 내에 있는 경우 지정된 모든 사용자의 정책 목록에 이름과 설명이 나타납니다. 개인 정책은 사용자와 관리자만 사용할 수 있습니다.

   이름이나 설명에 다음 문자를 사용할 수 없습니다.

   * 부등호(&lt;)
   * 보다 큼 기호(>)
   * 앰퍼샌드(&amp;)
   * 작은따옴표(&#39;)
   * 큰따옴표(&quot;)
   * 백슬래시(\)
   * 슬래시(/)

   이름이나 설명에 다음 문자를 사용한 경우 공백으로 변환됩니다.

   * 캐리지 리턴(ASCII 문자 13)
   * 새 줄(ASCII 문자 10).

   >[!NOTE]
   >
   >확장 문자가 포함된 정책 이름을 만들 수 있지만, 두 문자열 간에 비교되면 &quot;e&quot; 및 &quot;é&quot;와 같이 악센트가 적용된 문자와 악센트가 적용되지 않은 문자가 동일한 것으로 간주됩니다. 누군가 정책을 만들 때, 비교가 이루어져서 같은 이름의 정책이 있는지 확인합니다. 비교 시 악센트가 있는 문자를 제외하고 동일한 이름을 구별할 수 없습니다. 정책이 이미 데이터베이스에 추가되었고 새 정책이 추가되지 않았다고 가정합니다.

1. 정책에 사용자 및 그룹을 추가하고 적절한 권한을 설정합니다. [사용자 및 그룹](creating-policies.md#users-and-groups)을 참조하세요.
1. 일반 설정에서 적절한 옵션을 선택합니다. ([일반 설정](creating-policies.md#general-settings)을 참조하세요.)
1. (선택 사항) 해당되는 경우 외부 인증 공급자를 선택하고 해당 속성을 지정합니다. 외부 인증 공급자를 사용하지 않으려면 기본 공급자 제거를 클릭합니다.

   외부 인증 공급자는 정책 내에서 속성을 설정하는 데 사용되며, 이 옵션을 선택하면 외부 인증 공급자는 이 정보를 사용하여 정책을 평가합니다. 사용 가능한 속성은 관리자 및 소프트웨어를 설치하는 사용자가 구성합니다.

1. 고급 설정에서 적절한 옵션을 선택합니다. ([고급 설정](creating-policies.md#advanced-settings)을 참조하세요.)
1. 변경할 수 없는 고급 설정에서 해당 옵션을 선택합니다. [변경할 수 없는 고급 설정](creating-policies.md#unchangeable-advanced-settings)을 참조하십시오.
1. 저장을 클릭합니다. 정책이 정책 목록에 나타납니다. 새 정책 옆에 빨간색 원이 있는 아이콘이 표시되어 여전히 비활성화되어 있음을 나타냅니다.

   사용자가 정책을 사용할 수 있도록 하려면 활성화하십시오. [공유 정책 사용 또는 사용 안 함](creating-policies.md#enable-or-disable-shared-policies)을 참조하세요.

### 사용자 및 그룹 {#users-and-groups}

사용자 및 그룹 영역에서 정책으로 보호된 문서에 액세스할 수 있는 사용자를 지정합니다. 지정한 각 사용자 또는 그룹에 대해 문서 사용 권한도 설정합니다.

>[!NOTE]
>
>문서 게시자는 정책으로 문서를 보호하는 사용자입니다. 이 사용자는 해지 및 정책 전환 기능을 포함한 전체 액세스 권한이 있는 정책에 기본적으로 항상 포함됩니다. 그러나 관리자는 공유 정책에 대한 문서 게시자의 액세스 권한을 변경할 수 있습니다. 예를 들어 관리자가 문서 게시자가 문서 액세스를 취소하거나 정책을 전환하지 못하도록 제한할 수 있습니다.

**사용자 또는 그룹 추가:** 사용자 또는 사용자 그룹을 추가하려면 [사용자 또는 그룹 추가]를 클릭한 다음 [고급 검색]을 클릭하여 사용자 또는 그룹을 찾습니다. 사용자에는 조직의 내부 사용자와 문서 보안에 등록한 초대된 사용자가 포함됩니다. 이 옵션을 선택하면 [사용자 또는 그룹 추가] 페이지가 나타납니다.

* 찾기 상자에 사용자 또는 그룹 이름이나 이메일 주소를 입력합니다.
* 사용 목록에서 이름 또는 이메일을 선택합니다.
* 유형 목록에서 사용자 또는 그룹을 선택합니다.
* 위치 목록에서 검색할 도메인을 선택하고 찾기를 누릅니다.
* 결과가 반환되면 추가할 사용자 또는 그룹을 선택하고 추가 를 클릭합니다.

>[!NOTE]
>
>올바른 초대된 사용자 이름 또는 이메일 주소를 입력하고 결과가 반환되지 않으면 사용자가 아직 등록하지 않았거나 계정이 삭제될 수 있습니다. 사용자를 초대된 사용자 유형으로 추가하거나 관리자에게 문의할 수 있습니다.

**새 사용자 초대:** 초대된 사용자를 추가하려면 [새 사용자 초대]를 클릭하고 표시되는 상자에 사용자 전자 메일 주소를 입력한 다음 [초대]를 클릭합니다. 이 옵션은 관리자가 활성화한 경우에만 사용할 수 있습니다. 새 초대된 사용자를 정책에 추가할 때 Document Security는 사용자가 아직 등록하도록 초대되지 않은 경우 등록 초대 이메일을 보냅니다. 사용자는 이메일의 링크를 사용하여 계정을 만든 다음 계정을 활성화해야 합니다.

등록 후 초대된 사용자는 권한이 있는 정책으로 보호된 문서를 사용할 수 있습니다. 관리자가 활성화하는 기능에 따라 외부 사용자는 문서에 정책을 적용하고, 정책을 생성, 편집 및 삭제하며, 다른 외부 사용자를 정책에 추가할 수 있는 권한을 가질 수 있습니다.

**익명 사용자 추가:** 익명 사용자 액세스를 허용하려면 [익명 사용자 추가]를 클릭하십시오. 이 옵션은 관리자가 문서 보안을 위해 익명 사용자 액세스를 활성화한 경우에만 사용할 수 있습니다. 자세한 내용은 document security 서버 구성 을 참조하십시오. 이 옵션을 사용하면 문서 보안 계정이 있는지 여부에 관계없이 모든 사용자에게 이 정책으로 보호된 문서에 대한 액세스 권한을 부여합니다. 이 옵션을 선택하면 다른 유형의 사용자를 정책에 추가할 수 없습니다.

>[!NOTE]
>
>현재 이 문서가 없는 정책으로 보호된 문서에 대한 익명 액세스를 허용하려면 기존 정책을 제거한 다음 익명 액세스를 허용하는 정책을 적용합니다. 기존 정책을 전환하거나 변경할 경우 사용자가 계속 로그인하여 문서에 액세스해야 합니다.

#### 사용자 및 그룹에 대한 문서 권한 지정 {#specify-the-document-permissions-for-users-and-groups}

한 번에 한 사용자나 그룹에 대한 문서 권한을 지정하거나 목록에서 여러 사용자와 그룹을 선택하고 열 머리글 영역의 옵션을 사용하여 해당 권한을 변경할 수 있습니다.

기본적으로 모든 정책으로 보호된 문서에는 사용자가 온라인 상태에서 열 수 있는 권한이 있습니다.

문서 보안에 권한 및 옵션 탭이 표시됩니다.

이러한 문서 권한은 권한 탭에서 사용할 수 있습니다. 이러한 권한을 PDF, PTC Pro/E 및 Microsoft Office 파일에 적용할 수 있습니다.

**인쇄:** 사용자가 이 정책으로 보호되는 문서를 인쇄할 수 있도록 허용합니다. Office 및 Pro/E 파일의 경우 인쇄 확인란을 선택하여 인쇄를 허용하거나 선택을 취소하여 인쇄를 금지할 수 있습니다. PDF에 대한 사용자 지정 권한 표시 확인란을 선택하는 경우 다음 옵션 중에서 선택할 수 있습니다.

**허용되지 않음:** 사용자는 PDF을 인쇄할 수 없습니다.

**허용:** 사용자는 PDF을 인쇄할 수 있습니다.

**낮은 해상도.** 사용자만 낮은 해상도로 PDF을 인쇄할 수 있습니다.

**수정:** 사용자가 이 정책으로 보호되는 문서를 수정할 수 있도록 허용합니다. Office 및 Pro/E 파일의 경우 수정 확인란을 선택하여 수정할 수 있도록 하거나, 확인란을 선택 취소하여 수정할 수 없도록 할 수 있습니다. PDF에 대한 사용자 지정 권한 표시 확인란을 선택하는 경우 다음 옵션 중에서 선택할 수 있습니다.

**허용되지 않음:** 사용자는 PDF을 수정할 수 없습니다.

**모두:** 사용자는 PDF을 수정할 수 있습니다.

**공동 작업:** 사용자는 Adobe Acrobat의 공동 작업 옵션을 사용하여 다른 사용자와 공동 작업을 할 수 있습니다. 이 권한을 사용하면 정책에 복사 권한이 명시적으로 지정되지 않은 경우에도 사용자가 양식 데이터를 복사할 수 있습니다.

**페이지 변경:** 사용자는 PDF에서 페이지를 추가 및 제거하고 콘텐츠를 편집할 수 있습니다.

**채우기 및 서명:** 사용자는 PDF에서 양식 필드를 채우고 서명할 수 있습니다.

**복사:** 사용자가 이 정책으로 보호된 문서의 텍스트를 복사할 수 있도록 허용합니다.

**화면 Reader:** 이 권한은 PDF에 대한 사용자 지정 권한 표시 확인란을 선택하면 표시됩니다. 이 옵션을 선택하면 Adobe Acrobat은 화면 판독기를 사용하여 가독성을 개선하기 위해 PDF에 임시 태그를 추가할 권한이 있습니다.

이러한 문서 권한은 옵션 탭에서 사용할 수 있습니다. PDF, PTC Pro/E 및 Microsoft Office 파일에 다음 권한을 적용할 수 있습니다.

**오프라인:** 사용자가 이 정책으로 보호되는 문서를 오프라인으로 볼 수 있도록 허용합니다.

**권한 유효 기간:** 권한 선택이 항상 유효하거나 문서 권한 유효 기간을 설정합니다. 유효 기간을 선택하는 경우 달력 아이콘을 눌러 날짜를 선택하고 화살표를 사용하여 시간을 24시간 형식으로 지정합니다.

공유 정책의 경우 관리자는 문서 게시자(문서에 정책을 적용하는 사용자)에 대해 다음 권한을 비활성화할 수 있습니다.

**취소:** 문서 게시자가 문서 액세스 권한을 취소할 수 있도록 허용합니다.

**전환:** 문서 게시자가 정책 권한을 전환할 수 있도록 허용합니다.

### 일반 설정 {#general-settings}

일반 설정 영역에는 다음 설정이 포함됩니다.

**유효 기간:** 승인된 수신자가 정책으로 보호된 문서에 액세스할 수 있는 기간입니다. 다음 유효 기간 옵션 중에서 선택할 수 있습니다.

**다음 날짜 이후에 문서가 유효하지 않습니다.** 문서를 보호한 후 지정한 기간(일 수) 동안 문서에 액세스할 수 있습니다.

**이 날짜 이후에 문서가 유효하지 않습니다.** 문서가 유효하려면 정책이 문서에 적용된 날짜부터 지정된 종료 날짜까지 문서가 유효합니다.

**유효 기간, 종료 기간:** 지정한 날짜 동안 문서가 유효합니다. 해당하는 경우 달력 아이콘을 클릭하여 달력을 사용하여 날짜를 선택할 수 있습니다.

**문서가 항상 유효합니다.** 문서 유효 기간이 만료되지 않습니다.

>[!NOTE]
>
>유효 날짜는 로컬 컴퓨터의 표준 시간대가 아니라 문서 보안 시스템의 표준 시간대를 기준으로 합니다.

**감사:** 정책으로 보호된 문서와 연결된 이벤트의 감사를 활성화하거나 비활성화합니다. 예를 들어 문서 보안은 문서 열기 시도와 같은 이벤트를 기록할 수 있습니다. 감사된 이벤트는 [이벤트] 페이지의 목록에 나타납니다. 이 옵션을 선택하지 않으면 Document Security는 정책과 연관된 문서에 대한 이벤트를 기록하지 않습니다.

>[!NOTE]
>
>또한 관리자는 감사 기능이 작동하도록 감사 및 개인 정보 설정 구성 페이지에서 서버 감사를 활성화해야 합니다.

**확장 사용 추적:** 확장 사용 추적을 사용하거나 사용하지 않도록 설정합니다. Document Security는 PDF 파일에서 수행되는 다양한 작업과 관련된 사용자 이벤트 추적을 지원합니다. 문서 보안 개체는 Java Script를 사용하여 액세스할 수 있습니다. 단추 클릭, 재생 중인 멀티미디어 파일 또는 파일 저장은 정책으로 보호된 PDF에서 실행되는 이벤트의 몇 가지 예입니다. 문서 보안 개체를 사용하여 사용자 정보를 검색할 수도 있습니다. 이벤트 추적은 문서 보안 서버에서 전역 수준 또는 정책 수준에서 사용할 수 있습니다.

**자동 오프라인 임대 기간:** 받는 사람이 정책으로 보호된 문서를 오프라인으로 사용할 수 있는 최대 일 수(활성 인터넷 또는 네트워크 연결 없이)입니다. 임대 기간이 만료되면 수신자는 문서를 다시 동기화하여 계속 사용해야 합니다.

### 외부 인증 공급자 {#external-authorization-providers}

이미 구성한 경우 외부 인증 공급자를 선택하십시오. 사용 가능한 공급자가 나열됩니다.

### 인증 설정 {#authentication-settings}

서버에서 구성한 인증 설정을 재정의하고 이 정책과 관련된 인증 옵션을 지정할 수 있습니다. 글로벌 인증 설정 재정의를 선택한 다음 이 정책과 관련된 인증 옵션을 선택합니다. 다음 인증 옵션을 사용할 수 있습니다.

**사용자 이름 암호 인증 허용:** 클라이언트 응용 프로그램에서 서버에 연결할 때 사용자 이름/암호 인증을 사용하도록 설정하려면 이 옵션을 선택하십시오.

**Kerberos 인증 허용:** 서버에 연결할 때 클라이언트 응용 프로그램에서 Kerberos 인증을 사용하도록 설정하려면 이 옵션을 선택하십시오.

**클라이언트 인증서 인증 허용:** 서버에 연결할 때 클라이언트 응용 프로그램에서 인증서 인증을 사용하도록 설정하려면 이 옵션을 선택하십시오.

**확장 인증 허용** 확장 인증을 사용하려면 선택합니다. 이 옵션을 선택하면 클라이언트 응용 프로그램에서 확장 인증을 사용할 수 있습니다. 확장 인증은 Document Security 서버에 구성된 사용자 지정 인증 프로세스 및 다양한 인증 옵션을 제공합니다

전역 인증 설정을 재정의하는 경우 이 정책과 관련된 인증 옵션을 선택할 수 있습니다. 예를 들어 서버에서 세 가지 인증 옵션(사용자 이름과 암호, 클라이언트 인증서 및 확장 인증)을 사용하도록 설정한 경우 해당 전역 설정을 무시하고 이 정책에 대한 확장 인증만 선택할 수 있습니다. 여기서 선택하는 인증 옵션이 서버에 이미 구성되어 있는지 확인하십시오. 이 예제에서는 서버에 구성되지 않았으므로 Kerberos를 인증 옵션으로 선택할 수 없습니다.

>[!NOTE]
>
>확장 인증은 Adobe Acrobat 릴리스 11.0.6 이상의 Apple Mac OS X에서 지원됩니다.

### 고급 설정 {#advanced-settings}

고급 설정 영역에는 다음 설정이 포함됩니다.

**동적 워터마크:** 받는 사람이 문서를 인쇄할 때 문서 페이지에 동적으로 표시할 워터마크를 선택합니다. 동적 워터마크는 문서를 고유하게 식별하므로 문서의 기밀성을 보장하고 저작권 침해를 방지합니다. 예를 들어 관리자는 현재 날짜, 사용자 이름 또는 문서를 사용 중인 사용자의 식별자를 표시하는 동적 워터마크를 구성할 수 있습니다. 또는 문서를 보호하는 데 사용되는 정책의 이름입니다. 워터마크는 구성된 경우 사용자 지정 텍스트 또는 그래픽 요소를 표시할 수도 있습니다. 관리자는 워터마크 옵션을 구성하고 관리자와 사용자는 이를 정책에 적용할 수 있습니다.

[동적 워터마크 구성](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks)을 참조하십시오.

정책을 편집하는 중에 관리자가 이전에 이 정책에 대해 선택한 구성된 워터마크를 삭제한 경우 [정책 편집] 페이지에 메모가 나타납니다. 이 경우 편집된 문서를 저장하는 경우 새 워터마크를 문서에 표시하려면 새 워터마크를 선택합니다.

>[!NOTE]
>
>익명 사용자 액세스를 제공하는 정책의 경우 익명 사용자의 사용자 이름과 식별자는 이 유형의 워터마크를 선택하더라도 워터마크로 표시되지 않습니다.

**PDF에 인증된 Acrobat 플러그인만 사용:** 정책에 대해 이 옵션을 선택하면 정책으로 보호된 문서를 열 때 Acrobat 8.0 이상이 인증된 모드로 실행되도록 지정합니다. Acrobat이 인증 모드에서 실행되면 서드파티 플러그인이 로드되지 않습니다.

문서 수신자가 Acrobat 8.0 이상에서 문서 보호를 피할 수 있는 플러그인을 작성하는 것이 걱정되는 경우 이 옵션을 선택합니다. 문서 수신자가 Acrobat에서 서드 파티 플러그인을 사용하여 문서와 상호 작용해야 하는 경우에는 이 옵션을 선택하지 마십시오.

이 옵션을 사용하면 Acrobat 8.0 이상에서는 인증된 모드만 사용할 수 있습니다. 관리자는 Acrobat 7.0에 대한 액세스를 비활성화해야 합니다.

([문서 보안 서버 구성](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server)을 참조하세요.)

이 옵션은 Adobe Reader에는 적용되지 않습니다.

**액세스 거부 오류 메시지:** 권한이 없는 정책으로 보호된 문서를 열려고 하는 모든 사람에게 표시되는 메시지입니다. 이 메시지는 Acrobat에 표시됩니다. 이 메시지를 표시할 수 없는 클라이언트는 액세스가 거부되었음을 나타내는 기본 메시지를 표시합니다.

### 변경할 수 없는 고급 설정 {#unchangeable-advanced-settings}

변경할 수 없는 고급 설정 영역에는 다음 설정이 포함됩니다. 정책을 저장한 후에는 이러한 설정을 변경할 수 없습니다.

문서를 보호하는 데 사용되는 **암호화 알고리즘 및 키 길이:**. 다음 옵션 중에서 선택할 수 있습니다.

* AES 128비트
* AES 256비트. Acrobat 9.0 이상에서만 이 옵션을 지원합니다. PDF 파일에 AES 256 암호화를 사용하려면 JCE(Java Cryptography Extension) 무제한 강도 관할 정책 파일을 가져와 설치하십시오. 이러한 파일은 [JAVE_HOME]/lib/security 폴더의 local_policy.jar 및 US_export_policy.jar 파일을 대체합니다. 예를 들어 Sun JDK 1.6을 사용하는 경우 다운로드한 파일을 [dep root]/Java/jdk1.6.0_26/lib/security 폴더에 복사합니다. [Java SE 다운로드](https://java.sun.com/javase/downloads/index.jsp)에서 이러한 파일을 다운로드할 수 있습니다.
* 암호화 없음. Acrobat 9.0 이상에서는 현재 이 옵션을 지원합니다. 이 옵션을 선택하면 문서 제한 옵션이 비활성화됩니다. 이 옵션은 문서 감사 또는 버전 제어에 문서 보안을 사용하고 문서를 암호화하지 않으려는 경우에 유용합니다.

**문서 제한:** 암호화할 PDF 문서 구성 요소를 선택합니다. 다른 클라이언트 애플리케이션은 전체 문서를 암호화하지만 링크되거나 임베드된 파일은 암호화하지 않습니다. 다음 옵션 중에서 선택할 수 있습니다.

* 첨부 파일 및 메타데이터를 포함한 전체 문서. *메타데이터*&#x200B;은(는) 문서 속성 대화 상자나 Acrobat 고급 메뉴를 통해 볼 수 있는 문서 및 문서에 대한 정보입니다. Acrobat에서는 다른 유형의 파일(예: 텍스트, 오디오 및 비디오 파일)을 PDF 문서에 첨부할 수 있습니다.
* 문서와 해당 첨부 파일(메타데이터는 아님).
* 문서 첨부 파일만. 문서 내용을 암호화하지 않고도 PDF 파일의 첨부 파일을 암호화할 수 있습니다.

## 공유 정책 활성화 또는 비활성화 {#enable-or-disable-shared-policies}

공유 정책을 사용할 수 있게 하려면 관리자 또는 정책 집합 코디네이터가 이를 활성화해야 합니다. 새 정책 또는 이전에 비활성화한 정책을 활성화할 수 있습니다. 비활성화하는 공유 정책은 해당 정책으로 보호되는 문서에 여전히 적용됩니다.

비활성화된 정책 옆에 빨간색 X가 표시됩니다.

>[!NOTE]
>
>관리자는 개인 정책을 비활성화할 수 없으며 사용자는 자신의 정책을 활성화 및 비활성화할 수 없습니다.

1. 문서 보안 페이지에서 정책을 클릭한 다음 정책 세트 탭을 클릭합니다.
1. 해당 정책 세트 이름을 클릭하고 정책 탭을 클릭합니다.
1. 해당 정책 옆의 확인란을 선택하고 활성화 또는 비활성화를 클릭한 다음 확인을 클릭합니다.

## 정책에 대한 정보 보기 {#view-information-about-a-policy}

내 정책 탭을 사용하여 개인 정책을 검색할 수 있습니다.

관리자가 만드는 정책 세트는 정책 페이지의 정책 세트 탭에 나열됩니다. 여기에는 이름, 생성 및 수정 날짜, 설명 등 정책 세트에 대한 정보가 포함됩니다. 세부 정보를 볼 수 있도록 정책 세트 이름을 클릭합니다. 정책을 관리할 권한이 있는 정책 세트 코디네이터는 특정 정책 세트 내에 공유 정책을 만들 수 있습니다.

정책을 만들거나 편집할 때 정책에 포함할 정책 이름, 권한 수준, 기밀 유지 설정 및 수신자를 구성할 수 있는 페이지가 표시됩니다.

관리자는 정책에 대해 다음 기밀 유지 설정을 구성할 수 있습니다.

* 문서 유효 기간 및 오프라인 임대 기간과 같은 일반 문서 기밀 유지 옵션
* 승인된 사용자, 각 사용자에 대한 문서 제한 및 권한
* 동적 워터마크 및 문서 암호화를 포함한 고급 문서 기밀 유지 옵션

사용자는 자신이 만든 정책 및 액세스 권한이 있는 모든 공유 정책을 볼 수 있습니다. 관리자는 문서 보안에 있는 모든 공유 및 개인 정책을 볼 수 있습니다.

정책에 포함된 사용자 또는 그룹 및 해당 사용자에 대해 지정된 기밀 유지 설정을 포함하여 목록에 나타나는 정책에 대한 자세한 정보를 볼 수 있습니다.

>[!NOTE]
>
>Microsoft Outlook의 이메일 메시지에 첨부된 문서 수신자를 위해 Acrobat에서 자동으로 생성하는 정책은 정책 목록에 표시되지 않습니다. 연관된 문서에 대한 문서 세부 정보 페이지를 열어야 이러한 정책을 볼 수 있습니다.

1. 문서 보안 페이지에서 정책을 클릭한 다음 내 정책 탭을 클릭합니다.
1. 개인 정책을 검색할 수 있도록 검색 정보를 작성합니다.
1. 목록에서 적절한 정책을 선택합니다.
1. 정책 세부 정보 페이지에서 정책에 대한 세부 정보를 보거나 정책을 편집하거나 정책과 관련된 이벤트를 볼 수 있습니다.

## 정책 검색 {#search-for-policies}

관리자는 공유 정책 및 다른 사용자가 만든 개인 정책을 검색할 수 있습니다.

1. 공유 정책을 검색하려면 정책을 클릭한 다음 정책 세트 탭을 클릭합니다. 목록에서 정책 세트를 클릭한 다음 정책 탭을 클릭합니다.

   개인 정책을 검색하려면 문서 보안 페이지에서 정책을 클릭한 다음 내 정책 탭을 클릭합니다.

1. 찾기 목록에서 다음 옵션 중 하나를 선택합니다.

   **정책 ID:** 사용자가 정책을 만들 때 생성되는 정책 ID 번호입니다. 정확한 정책 ID를 입력합니다.

   **정책 이름:** 정책의 이름입니다. 정책 이름의 일부 또는 전체를 검색할 수 있습니다.

1. 텍스트 상자에 해당 값을 입력합니다. 예를 들어 정책 이름을 선택한 경우 검색 중인 정책 이름을 입력합니다.
1. 표시 목록에서 표시할 결과 수를 선택한 다음 찾기를 누릅니다. 검색 결과가 표시됩니다.
1. (선택 사항) 정책 세부 사항을 보려면 정책을 누릅니다.

## 정책 복사 {#copy-a-policy}

기존 정책을 복사하고 새 이름과 설명을 사용하여 저장할 수 있습니다. 정책을 복사하는 것은 기존 설정을 사용하여 정책을 만드는 효율적인 방법입니다.

외부 사용자는 관리자가 이 기능을 사용하도록 설정한 경우에만 정책을 복사할 수 있습니다. 정책을 생성할 수 없는 경우 복사 옵션을 사용할 수 없습니다.

1. 문서 보안 페이지에서 정책을 클릭한 다음 내 정책 탭을 클릭합니다.
1. 목록에서 적절한 정책을 선택합니다.
1. 정책 세부 정보 페이지에서 복사를 클릭합니다.
1. 새 정책 이름 상자에 새 정책 이름을 입력합니다. 원할 경우 새 설명을 입력합니다.

   이름이나 설명에 다음 문자를 사용할 수 없습니다.

   * 부등호(&lt;)
   * 보다 큼 기호(>)
   * 앰퍼샌드(&amp;)
   * 작은따옴표(&#39;)
   * 큰따옴표(&quot;)
   * 백슬래시(\)
   * 슬래시(/)

   이름이나 설명에 다음 문자를 사용한 경우 공백으로 변환됩니다.

   * 캐리지 리턴(ASCII 문자 13)
   * 새 줄(ASCII 문자 10).

   >[!NOTE]
   >
   >확장 문자가 포함된 정책 이름을 만들 수 있지만, 두 문자열 간에 비교되면 &quot;e&quot; 및 &quot;é&quot;와 같이 악센트가 적용된 문자와 악센트가 적용되지 않은 문자가 동일한 것으로 간주됩니다. 누군가 정책을 만들 때, 비교가 이루어져서 같은 이름의 정책이 있는지 확인합니다. 비교 시 악센트가 있는 문자를 제외하고 동일한 이름을 구별할 수 없습니다. 정책이 이미 데이터베이스에 추가되었고 새 정책이 추가되지 않았다고 가정합니다.

1. 확인을 클릭합니다.

## 정책 삭제 {#delete-a-policy}

생성한 정책을 삭제할 수 있습니다. 관리자는 사용자가 만든 정책을 삭제할 수 있습니다. 정책 세트 코디네이터는 정책 세트에서 정책을 삭제할 수 있습니다. 삭제되는 정책은 해당 정책으로 보호되는 문서에 여전히 적용됩니다. 한 번에 두 개 이상의 정책을 삭제할 수 있습니다.

초대된 사용자는 관리자가 이 기능을 사용하도록 설정한 경우에만 정책을 삭제할 수 있습니다. 정책을 삭제할 수 없는 경우 삭제 옵션을 사용할 수 없습니다.

1. 문서 보안 페이지에서 정책을 클릭합니다.
1. 내 정책 탭을 클릭합니다.
1. 공유 정책을 삭제하려면 정책 세트 탭을 클릭하고 적절한 정책 세트 이름을 클릭합니다.
1. 해당 정책 옆의 확인란을 선택하고 삭제를 클릭한 다음 확인을 클릭합니다.

>[!NOTE]
>
>클라이언트 응용 프로그램을 사용하여 문서에서 정책을 제거합니다. (Acrobat 도움말 또는 적절한 Acrobat Reader DC 확장 도움말 참조)

## 정책 목록 정렬 {#sort-the-policy-list}

열 머리글별로 정책 목록을 정렬하여 정책을 보다 쉽게 찾을 수 있습니다. 열 제목 옆에 있는 삼각형 아이콘은 현재 정렬에 사용되는 열을 나타냅니다. 위쪽을 가리키는 삼각형은 오름차순을 나타내고 아래쪽을 가리키는 삼각형은 내림차순을 나타냅니다.

1. 문서 보안 페이지에서 정책을 클릭하고 정책 세트 탭을 클릭합니다.
1. 정책 세트를 선택한 다음 정책 탭을 클릭합니다.
1. 해당 열 머리글을 클릭합니다.
1. 정렬 순서를 변경하려면 열을 다시 클릭합니다.
