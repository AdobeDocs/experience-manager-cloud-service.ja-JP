---
title: ユニバーサルエディター呼び出し
description: デバッグ時に役立つユニバーサルエディターによってアプリに対しておこなわれる様々なタイプの呼び出しについて説明します。
source-git-commit: 16f2922a3745f9eb72f7070c30134e5149eb78ce
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---


# ユニバーサルエディター呼び出し {#calls}

デバッグ時に役立つユニバーサルエディターによってアプリに対しておこなわれる様々なタイプの呼び出しについて説明します。

{{universal-editor-status}}

## 概要 {#overview}

ユニバーサルエディターは、定義された一連の呼び出しを通じて、実装されたアプリと通信します。 これはに対して透過的で、エンドユーザーエクスペリエンスには影響しません。

ただし、開発者は、これらの呼び出しについて理解し、ユニバーサルエディターを使用する場合にアプリケーションのデバッグをおこなう際に、それらの呼び出しについて理解すると役に立ちます。 アプリが実装されていて、期待どおりに動作していない場合は、 **ネットワーク** 」タブをクリックし、アプリ内のコンテンツを編集する際に呼び出しを調べます。

![ブラウザーの開発者ツールの「ネットワーク」タブでの詳細呼び出しの例](assets/calls-network-tab.png)

* The **ペイロード** 呼び出しの内容には、更新する内容や更新方法の識別など、エディターによる更新内容の詳細が含まれています。
* The **応答** には、エディターサービスによって正確に更新された内容の詳細が含まれています。 これは、エディターでコンテンツを簡単に更新できるようにするためです。 場合によっては、 `move` を呼び出す場合は、ページ全体を更新する必要があります。

以下は、ユニバーサルエディターがアプリに対しておこなう呼び出しのタイプと、サンプルのペイロードおよび応答のリストです。

## アップデート {#update}

An `update` 呼び出しは、ユニバーサルエディターを使用してアプリのコンテンツを編集する際に発生します。 The `update` は変更を保持します。

ペイロードには、JCR に書き戻す内容の詳細が含まれます。

* `itemid`：更新する JCR パス
* `itemprop`：更新する JCR プロパティ
* `itemtype`：更新するプロパティの JCR 値タイプ
* `value`：更新されたデータ

### サンプルペイロード {#update-payload}

```json
{
  "op": "patch",
  "connections": {
    "aem": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "path": {
    "itemid": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "itemtype": "text",
    "itemprop": "jcr:title"
  },
  "value": "Tiny Toon Adventures"
}
```

### レスポンスのサンプル {#update-response}

```json
{
  "updates": [
    {
      "itemid": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
      "itemprop": "jcr:title",
      "itemtype": "text"
    }
  ]
}
```

## 詳細 {#details}

A `details` アプリのコンテンツを取得するためにユニバーサルエディターでアプリを読み込む際に、呼び出しが発生します。

ペイロードには、レンダリングされるデータと、データが表す内容（スキーマ）の詳細が含まれており、ユニバーサルエディターでレンダリングできます。

* コンポーネントの場合、ユニバーサルエディターは `data` オブジェクトに含まれる必要はありません。データのスキーマがアプリ内で定義されているからです。
* コンテンツフラグメントの場合、ユニバーサルエディターでも `schema` オブジェクトの内容は、JCR でコンテンツフラグメントモデルが定義されているので、変更できません。

### サンプルペイロード {#details-payload}

```json
{
  "op": "patch",
  "connections": {
    "aem": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "path": {
    "itemid": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "itemtype": "component",
    "itemprop": ""
  }
}
```

### レスポンスのサンプル {#details-response}

```json
{
  "data": {
    "jcr:primaryType": "nt:unstructured",
    "jcr:title": "Tiny Toon Adventures!",
    "fileReference": "/content/dam/wknd-shared/en/adventures/riverside-camping-australia/adobestock-216674449.jpeg",
    "cq:panelTitle": "WKND Adventures",
    "actionsEnabled": "true",
    "jcr:lastModifiedBy": "admin",
    "titleFromPage": "false",
    "jcr:description": "<p>With WKND Adventures, you don't just see the world you experinece it.</p>",
    "jcr:lastModified": "Wed Jan 03 2024 09:06:05 GMT+0100",
    "descriptionFromPage": "true",
    "sling:resourceType": "wknd/components/teaser",
    "textIsRich": "true",
    "cq:styleIds": [
      "1555543212672"
    ],
    "actions": {
      "jcr:primaryType": "nt:unstructured",
      "item0": {
        "jcr:primaryType": "nt:unstructured",
        "link": "/content/wknd/language-masters/en/adventures",
        "text": "View Trips"
      }
    }
  }
}
```

## add {#add}

An `add` 呼び出しは、ユニバーサルエディターを使用してアプリに新しいコンポーネントを配置すると発生します。

ペイロードには、 `path` コンテンツを追加する場所を含むオブジェクト。

また、 `content` 保存するコンテンツのエンドポイント固有の詳細用の追加オブジェクトを含むオブジェクト [プラグインごとに](/help/implementing/universal-editor/architecture.md) 例えば、アプリがAEMとMagentoのコンテンツに基づいている場合、ペイロードには各システムのデータオブジェクトが含まれます。

### サンプルペイロード {#add-payload}

```json
{
  "op": "patch",
  "connections": {
    "aemconnection": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "path": {
    "container": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemtype": "container",
      "itemprop": ""
    }
  },
  "content": {
    "name": "text",
    "aem": {
      "page": {
        "resourceType": "wknd/components/text",
        "template": {
          "text": "Default Text"
        }
      }
    }
  }
}
```

### レスポンスのサンプル {#add-response}

```json
{
  "updates": [
    {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemtype": "container"
    }
  ]
}
```

## 移動 {#move}

A `move` 呼び出しは、ユニバーサルエディターを使用してアプリ内のコンポーネントを移動すると発生します。

ペイロードには、 `from` コンポーネントの場所を定義するオブジェクトと `to` 移動先を定義するオブジェクト。

### サンプルペイロード {#move-payload}

```json
{
  "op": "patch",
  "connections": {
    "aemconnection": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "from": {
    "container": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemtype": "container",
      "itemprop": ""
    },
    "component": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1068508321",
      "itemtype": "text",
      "itemprop": "text"
    }
  },
  "to": {
    "container": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemtype": "container",
      "itemprop": ""
    },
    "before": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_2063168902",
      "itemtype": "text",
      "itemprop": "text"
    }
  }
}
```

### レスポンスのサンプル {#move-response}

```json
{
  "updates": [
    {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemtype": "container"
    }
  ]
}
```

## 削除 {#remove}

A `remove` ユニバーサルエディターを使用してアプリ内のコンポーネントを削除すると、呼び出しが発生します。

ペイロードには、削除されたオブジェクトのパスが含まれます。

### サンプルペイロード {#remove-payload}

```json
{
  "op": "patch",
  "connections": {
    "aemconnection": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "path": {
    "component": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1068508321",
      "itemtype": "text",
      "itemprop": "text"
    },
    "container": {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemtype": "container",
      "itemprop": ""
    }
  }
}
```

### レスポンスのサンプル {#remove-response}

```json
{
  "updates": [
    {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "itemprop": "",
      "itemtype": "container"
    }
  ]
}
```

## パッチ {#patch}

A `patch` アプリ内のダイアログでコンテンツを更新すると、が呼び出されます。 これにより、アプリのページ内のコンテンツが JSON パッチとして既存のコンテンツに更新されます。

ペイロードには、ページ上のコンテンツのパスと、行われる変更の JSON パッチが含まれます。

### サンプルペイロード {#patch-payload}

```json
{
  "op": "patch",
  "connections": {
    "aemconnection": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "path": {
    "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1540979193",
    "itemtype": "text",
    "itemprop": "text"
  },
  "patch": [
    {
      "op": "replace",
      "path": "/text",
      "value": "Still More WKND Adventures"
    }
  ]
}
```

### レスポンスのサンプル {#patch-response}

```json
{
  "updates": [
    {
      "itemid": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1540979193"
    }
  ]
}
```

## 公開 {#publish}

A `publish` クリック時に呼び出しが発生します **公開** 」ボタンをクリックして、編集したコンテンツを公開します。

ユニバーサルエディターはコンテンツを反復し、公開する必要がある参照のリストを生成します。

### サンプルペイロード {#publish-payload}

```json
{
  "op": "patch",
  "connections": {
    "aemconnection": "aem:https://author-pXXXX-eYYYYY.adobeaemcloud.com"
  },
  "references": [
    "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
    "urn:aemconnection:/content/wknd/us/en/adventures/jcr:content/root/container/container/title",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/bali-surf-camp/bali-surf-camp/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/climbing-new-zealand/climbing-new-zealand/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/cycling-southern-utah/cycling-southern-utah/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/cycling-tuscany/cycling-tuscany/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/downhill-skiing-wyoming/downhill-skiing-wyoming/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/napa-wine-tasting/napa-wine-tasting/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/riverside-camping-australia/riverside-camping-australia/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/ski-touring-mont-blanc/ski-touring-mont-blanc/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/surf-camp-in-costa-rica/surf-camp-costa-rica/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/tahoe-skiing/tahoe-skiing/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/west-coast-cycling/west-coast-cycling/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/yosemite-backpacking/yosemite-backpacking/jcr:content/data/master",
    "urn:aemconnection:/content/wknd/us/en/newsletter/jcr:content/root/container/title",
    "urn:aemconnection:/content/wknd/us/en/newsletter/jcr:content/root/container/text",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/title",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_2123678383",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1668104604",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_229050934",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_275525847",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_358189229",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_2063168902",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1540979193"
  ]
}
```

### レスポンスのサンプル {#publish-response}

```json
{
  "publishes": [
    "/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway",
    "/content/wknd/us/en/adventures",
    "/content/dam/wknd-shared/en/adventures/bali-surf-camp/bali-surf-camp",
    "/content/dam/wknd-shared/en/adventures/climbing-new-zealand/climbing-new-zealand",
    "/content/dam/wknd-shared/en/adventures/cycling-southern-utah/cycling-southern-utah",
    "/content/dam/wknd-shared/en/adventures/cycling-tuscany/cycling-tuscany",
    "/content/dam/wknd-shared/en/adventures/downhill-skiing-wyoming/downhill-skiing-wyoming",
    "/content/dam/wknd-shared/en/adventures/napa-wine-tasting/napa-wine-tasting",
    "/content/dam/wknd-shared/en/adventures/riverside-camping-australia/riverside-camping-australia",
    "/content/dam/wknd-shared/en/adventures/ski-touring-mont-blanc/ski-touring-mont-blanc",
    "/content/dam/wknd-shared/en/adventures/surf-camp-in-costa-rica/surf-camp-costa-rica",
    "/content/dam/wknd-shared/en/adventures/tahoe-skiing/tahoe-skiing",
    "/content/dam/wknd-shared/en/adventures/west-coast-cycling/west-coast-cycling",
    "/content/dam/wknd-shared/en/adventures/yosemite-backpacking/yosemite-backpacking",
    "/content/wknd/us/en/newsletter",
    "/content/wknd/language-masters/en/universal-editor-container"
  ]
}
```
