---
title: 정적 개체의 만료
description: 정적 개체가 적절한 기간 동안 만료되지 않도록 Adobe Experience Manager을 구성하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: a279ebed-a116-4719-989e-1b2f79f6caa4
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# 정적 개체의 만료{#expiration-of-static-objects}

정적 객체(예: 아이콘)는 변경되지 않습니다. 따라서 시스템이 (적절한 기간 동안) 만료되지 않고 불필요한 트래픽을 줄이도록 구성되어야 합니다.

이는 다음과 같은 영향을 줍니다.

* 서버 인프라의 요청을 오프로드합니다.
* 브라우저가 브라우저 캐시의 오브젝트를 캐시하므로 페이지 로드 성능이 향상됩니다.

만료는 파일의 &quot;만료&quot;와 관련하여 HTTP 표준에 의해 지정됩니다(예: [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot; Hypertext Transfer Protocol — HTTP 1.1&quot;의 14.21장 참조). 이 표준에서는 헤더를 사용하여 클라이언트가 오래된 것으로 간주될 때까지 객체를 캐시할 수 있습니다. 이러한 객체는 원래 서버에 대한 상태 검사 없이 지정된 시간 동안 캐시됩니다.

>[!NOTE]
>
>이 구성은 Dispatcher과 별도이며 (이 경우 작동하지 않습니다.)
>
>Dispatcher의 목적은 Adobe Experience Manager(AEM) 앞에 데이터를 캐시하는 것입니다.

동적이지 않고 시간이 지나도 변경되지 않는 모든 파일은 캐시할 수 있으며 캐시되어야 합니다. Apache HTTPD 서버에 대한 구성은 환경에 따라 다음 중 하나와 비슷할 수 있습니다.

>[!CAUTION]
>
>개체가 최신 상태로 간주되는 기간을 정의할 때는 주의하십시오. *지정된 기간이 만료될 때까지 확인이 없음*&#x200B;이므로, 클라이언트는 캐시에서 이전 콘텐츠를 표시할 수 있습니다.

1. 작성자 인스턴스의 **경우:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   따라서 중간 캐시(예: 브라우저 캐시)는 만료될 때까지 최대 1개월 동안 CSS, JavaScript, PNG 및 GIF 파일을 저장할 수 있습니다. 즉, AEM 또는 웹 서버에서 요청할 필요는 없지만 브라우저 캐시에 남아 있을 수 있습니다.

   사이트의 다른 섹션은 언제든지 변경될 수 있으므로 작성자 인스턴스에 캐시해서는 안 됩니다.

1. **게시 인스턴스의 경우:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /content>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   <Location /etc/designs>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   ```

   이렇게 하면 중간 캐시(예: 브라우저 캐시)가 최대 하루 동안 CSS, JavaScript, PNG 및 GIF 파일을 클라이언트 캐시에 저장할 수 있습니다. 이 예제는 `/content` 및 `/etc/designs` 아래의 모든 항목에 대한 전역 설정을 보여 주지만 좀 더 세분화해야 합니다.

   사이트가 업데이트되는 빈도에 따라 HTML 페이지를 캐시하는 것도 고려할 수 있습니다. 적절한 기간은 1시간입니다.

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

정적 개체를 구성한 후 이러한 개체가 있는 페이지를 선택하는 동안 `request.log`을(를) 검사하여 정적 개체에 대해 불필요한 요청이 발생하지 않았는지 확인하십시오.
