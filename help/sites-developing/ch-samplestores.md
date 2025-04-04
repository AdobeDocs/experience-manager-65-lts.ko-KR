---
title: 샘플 ContextHub 저장소 후보
description: ContextHub는 솔루션에서 사용할 수 있는 몇 가지 샘플 저장소 후보를 제공합니다
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
exl-id: b49aee0b-292c-4854-83cb-2e70e05b0a17
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---

# 샘플 ContextHub 저장소 후보{#sample-contexthub-store-candidates}

ContextHub는 솔루션에서 사용할 수 있는 몇 가지 샘플 저장소 후보를 제공합니다. 각 샘플에 대해 다음 정보가 제공됩니다.

* 학습 목적으로 열 수 있도록 소스 코드를 찾을 위치.
* 저장소 후보에서 만드는 저장소를 구성하는 방법입니다.
* 액세스할 수 있도록 스토어 데이터를 구성하는 방법입니다.

>[!WARNING]
>
>샘플 저장소 후보는 프로젝트에 대한 자체 전용 구성을 작성하는 데 도움이 되는 참조 구성으로 제공됩니다. 직접 사용하지 마십시오.

## aem.segmentation 샘플 저장소 후보 {#aem-segmentation-sample-store-candidate}

해결되거나 해결되지 않은 ContextHub 세그먼트를 저장합니다. ContextHub SegmentManager에서 세그먼트를 자동으로 검색합니다.

### Source 위치 {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### 기본 구현 {#base-implementation-segmentation}

aem.segmentation 저장소 후보가 [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)을(를) 확장합니다.

### 구성 {#configuration-segmentation}

aem.segmentation 스토어를 만들 때 세부 구성을 제공할 필요가 없습니다. 기본 구성은 ContextHub 세그먼트 정의의 위치를 지정합니다.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation 샘플 저장소 후보 {#contexthub-geolocation-sample-store-candidate}

contexthub.geolocation 샘플 저장소 후보는 Google 맵을 사용하여 클라이언트 위치에 대한 정보를 가져오고 저장합니다.

### Source 위치 {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### 기본 구현 {#base-implementation-geolocation}

contexthub.geolocation 저장소 후보가 [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)을(를) 확장합니다.

### 구성 {#configuration-geolocation}

기본 구성은 Google 서비스와 초기 위도 및 경도 좌표에 대한 정보를 지정합니다.

```xml
{
        "service": {
            "jsonp": false,
            "timeout": 1000,
            "ttl": 1800000,
            "secure": false,
            "host": "maps.googleapis.com",
            "port": 80,
            "path": "/maps/api/geocode/json"
        },

        "eventDeferring": 16,

        "html5coordinatesDiscoveryAPI": {
            "timeout": 30000,
            "ttl": 900000,
            "highAccuracy": false
        },

        "initialValues": {
            "latitude": 37.331375,
            "longitude": -121.893992
        }
    }
```

### 데이터 항목 {#data-items-geolocation}

저장소는 다음 예제와 유사한 데이터 트리를 사용합니다.

```xml
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Chrome 50.x에 도입된 보안 정책을 사용하려면 모든 지리적 위치 관련 호출이 보안 연결을 통해 수행되어야 합니다. 따라서 AEM은 AEM이 https에서도 실행 중인 경우 지리적 위치 API 호출에 https 사용을 강제합니다. 그렇지 않으면 동일한 출처의 정책을 준수하는 데 http가 사용됩니다. Chrome 변경에 대한 자세한 내용은 [이 Google 블로그 게시물](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only)을 참조하십시오.

## contexthub.surferinfo 샘플 저장소 후보 {#contexthub-surferinfo-sample-store-candidate}

장치, 창, 브라우저, 날짜 및 시간 등 현재 클라이언트 환경에 대한 정보를 저장합니다.

### Source 위치 {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### 기본 구현 {#base-implementation-surferinfo}

contexthub.datetime 저장소 후보가 [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)을(를) 확장합니다.

### 구성 {#configuration-surferinfo}

기본 구성은 `ContextHub.Store.PersistedStore`에서 상속됩니다.

### 데이터 항목 {#data-items-surferinfo}

이 저장소 후보를 사용하는 저장소에는 다음 예제와 유사한 데이터 트리가 있습니다.

```xml
{
   "display":{
      "resolution":{
         "width":1440,
         "height":900
      },
      "devicePixelRatio":1,
      "colorDepth":24,
      "nrOfColors":16777216,
      "pixelsPerInch":96,
      "orientation":{
         "mode":"landscape",
         "direction":"normal"
      }
   },
   "window":{
      "dimension":{
         "width":1395,
         "height":652
      },
      "percentageUsage":0.7
   },
   "browser":{
      "version":"39.0",
      "family":"Firefox",
      "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:39.0) Gecko/20100101 Firefox/39.0"
   },
   "device":{
      "category":"Desktop",
      "type":"Desktop",
      "model":"PC",
      "version":""
   },
   "isMobile":true,
   "os":{
      "name":"Mac OS X",
      "version":"10"
   },
   "year":2015,
   "month":7,
   "day":22,
   "hour":14,
   "minutes":1
}
```

## granite.emulators 샘플 저장소 후보 {#granite-emulators-sample-store-candidate}

granite.emulators 샘플 저장소 후보는 클라이언트 장치에 대한 정보를 저장합니다.

### Source 위치 {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### 기본 구현 {#base-implementation-emulators}

contexthub.geolocation 저장소 후보가 [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)을(를) 확장합니다.

### 구성 {#configuration-emulators}

기본 구성에는 서로 다른 장치에 대한 정보가 포함된 `defaultEmulators`(이)라는 배열이 포함되어 있습니다. 저장소를 만들 때 다음 예제에 나와 있는 형식을 사용하여 필요에 따라 세부 구성 속성에 다른 장치 프로필을 제공합니다.

```xml
{
   "defaultEmulators":[
        {
            "id": "iphone-6",
            "title": "iPhone 6",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 750,
            "height": 1334,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 2
        },
        {
            "id": "iphone-6-plus",
            "title": "iPhone 6 Plus",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        },
        {
            "id": "galaxy-s4",
            "title": "Samsung Galaxy S4",
            "type": "mobile",
            "platform": "Android",
            "platformVersion": "4.4.2 KitKat",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        }
    ]
}
```

### 데이터 항목 {#data-items-emulators}

저장소 데이터 트리는 다음 예와 유사합니다.

```xml
{
   "devices":[
      {"id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
      },
      {"id":"ipad-3",
      "title":"iPad 3 / 4 / Air",
      "type":"tablet",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":1536,
      "height":2048,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"iphone-6",
      "title":"iPhone 6",
      "type":"mobile",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":750,
      "height":1334,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"galaxy-s4",
      "title":"Samsung Galaxy S4",
      "type":"mobile",
      "platform":"Android",
      "platformVersion":"4.4.2 KitKat",
      "width":1080,
      "height":1920,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":3
      }
   ],
   "currentDeviceId":"native",
   "orientations":[
      {"id":"landscape",
      "title":"Landscape"
      },
      {"id":"portrait",
       "title":"Portrait"
      }
   ],
   "currentDevice":{
      "id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
   }
}
```

## granite.profile 샘플 저장소 후보 {#granite-profile-sample-store-candidate}

현재 사용자에 대한 정보를 저장합니다.

### Source 위치 {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### 기본 구현 {#base-implementation-profile}

contexthub.datetime 저장소 후보가 [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)을(를) 확장합니다.

### 구성 {#configuration-profile}

다음 기본 구성이 사용됩니다. 이 구성을 변경해서는 안 됩니다.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"${contexthub:/store/profile/path}.infinity.json"
   },
   "initialValues":{"path":"/home/users/a/anonymous"}
}
```

### 데이터 항목 {#data-items-profile}

이 저장소 후보를 사용하는 저장소에는 다음 예제와 유사한 데이터 트리가 있습니다.

```xml
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
