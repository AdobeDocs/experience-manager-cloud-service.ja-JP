---
title: ContextHub ストア候補のサンプル
description: ContextHub には、ソリューションで利用できるサンプルストア候補がいくつか用意されています
translation-type: tm+mt
source-git-commit: c3f69e4b03819fea9a1842a87cad38bd1e485d83
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 100%

---


# ContextHub ストア候補のサンプル {#sample-contexthub-store-candidates}

ContextHub には、ソリューションで利用できるサンプルストア候補がいくつか用意されています。各サンプルでは次の情報が提供されます。

* 学習用に参照できるソースコードの場所。
* ストア候補から作成するストアの設定方法。
* アクセスするためのストアデータの構造。

>[!WARNING]
>
>サンプルストア候補は、プロジェクト専用の設定を構築する際に役立つリファレンス設定として提供されているので、直接使用しないでください。

## aem.segmentation サンプルストア候補 {#aem-segmentation-sample-store-candidate}

解決済みおよび未解決の ContextHub セグメント用のストア。ContextHub SegmentManager からセグメントを自動的に取得します.

### ソースの場所 {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### ベースとなる実装 {#base-implementation-segmentation}

aem.segmentation ストア候補は、[`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore) を拡張したものです。

### 設定 {#configuration-segmentation}

`aem.segmentation` ストアを作成する場合、詳細な設定をする必要はありません。デフォルトの設定によって、ContextHub セグメント定義の場所が指定されます。

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation サンプルストア候補 {#contexthub-geolocation-sample-store-candidate}

`contexthub.geolocation` サンプルストア候補は、Google マップを使用して、クライアントの位置に関する情報を取得し、格納します。

### ソースの場所 {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### ベースとなる実装 {#base-implementation-geolocation}

`contexthub.geolocation` ストア候補は、[`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore) を拡張したものです。

### 設定 {#configuration-geolocation}

デフォルトの設定で、Google サービスに関する情報および緯度と経度の初期座標を指定します。

```javascript
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

### データ項目 {#data-items-geolocation}

このストアは、次の例のようなデータツリーを使用します。

```javascript
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Chrome 50.x で導入されたセキュリティポリシーでは、すべてのジオロケーション関連呼び出しは、安全な接続を使用しておこなう必要があります。そのため、AEM では、AEM が https 経由で実行されていても、ジオロケーション API 呼び出しに https の使用を強制します。その他の場合は、同一オリジンポリシーに準拠するために、http が使用されます。
>
>Chrome での変更について詳しくは、[Google のこのブログ投稿](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only)を参照してください。

## contexthub.surferinfo サンプルストア候補 {#contexthub-surferinfo-sample-store-candidate}

デバイス、ウィンドウ、ブラウザー、日付時刻など、現在のクライアント環境に関する情報を格納します。

### ソースの場所 {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### ベースとなる実装 {#base-implementation-surferinfo}

`contexthub.surferinfo` ストア候補は、[`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore) を拡張したものです。

### 設定 {#configuration-surferinfo}

デフォルトの設定は、`ContextHub.Store.PersistedStore` から継承されます。

### データ項目 {#data-items-surferinfo}

このストア候補を使用するストアのデータツリーは次の例のようになります。

```javascript
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

## granite.emulators サンプルストア候補 {#granite-emulators-sample-store-candidate}

`granite.emulators` サンプルストア候補は、クライアントデバイスに関する情報を格納します。

### ソースの場所 {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### ベースとなる実装 {#base-implementation-emulators}

`granite.emulators` ストア候補は、[`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore) を拡張したものです。

### 設定 {#configuration-emulators}

デフォルトの設定には、様々なデバイスに関する情報を格納する、`defaultEmulators` という配列が含まれます。ストアを作成する場合、次の例で説明する形式を使用して、必要に応じて詳細設定プロパティで様々なデバイスプロファイルを指定します。

```javascript
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

### データ項目 {#data-items-emulators}

このストアのデータツリーは、次の例のようになります。

```javascript
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

## granite.profile サンプルストア候補 {#granite-profile-sample-store-candidate}

現在のユーザーに関する情報を格納します。

### ソースの場所 {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### ベースとなる実装 {#base-implementation-profile}

`granite.profile` ストア候補は、[`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore) を拡張したものです。

### 設定 {#configuration-profile}

次のデフォルトの設定を使用します。この設定は変更しないでください。

```javascript
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"${contexthub:/store/profile/path}.infinity.json"
   },
   "initialValues":{"path":"/home/users/a/anonymous"}
}
```

### データ項目 {#data-items-profile}

このストア候補を使用するストアのデータツリーは次の例のようになります。

```javascript
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
