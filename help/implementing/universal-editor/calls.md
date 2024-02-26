---
title: ユニバーサルエディターの呼び出し
description: デバッグ時に役立つユニバーサルエディターによってアプリに対しておこなわれる様々なタイプの呼び出しについて説明します。
exl-id: 00d66e59-e445-4b5c-a5b1-c0a9f032ebd9
source-git-commit: 1fc53e726f3a15c9ac7d772b4c181a7877e417af
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 2%

---


# ユニバーサルエディターの呼び出し {#calls}

デバッグ時に役立つユニバーサルエディターによってアプリに対しておこなわれる様々なタイプの呼び出しについて説明します。

{{universal-editor-status}}

## 概要 {#overview}

ユニバーサルエディターは、定義された一連の呼び出しを通じて、実装されたアプリと通信します。 これはに対して透過的で、エンドユーザーエクスペリエンスには影響しません。

ただし、開発者は、これらの呼び出しについて理解し、ユニバーサルエディターを使用する場合にアプリケーションのデバッグをおこなう際に、それらの呼び出しについて理解すると役に立ちます。 アプリが実装されていて、期待どおりに動作していない場合は、 **ネットワーク** 」タブをクリックし、アプリ内のコンテンツを編集する際に呼び出しを調べます。

![ブラウザーの開発者ツールの「ネットワーク」タブでの詳細呼び出しの例](assets/calls-network-tab.png)

* The **ペイロード** 呼び出しの内容には、更新する内容や更新方法の識別など、エディターによる更新内容の詳細が含まれています。
* The **応答** には、エディターサービスによって正確に更新された内容の詳細が含まれています。 これは、エディターでコンテンツを簡単に更新できるようにするためです。 場合によっては、 `move` を呼び出す場合は、ページ全体を更新する必要があります。

呼び出しが正常に完了すると、リクエストのペイロードと応答のペイロードを含むイベントがトリガーされます。このペイロードは、独自のアプリ用にカスタマイズできます。 ドキュメントを参照してください [ユニバーサルエディターイベント](/help/implementing/universal-editor/events.md) を参照してください。

以下は、ユニバーサルエディターがアプリに対しておこなう呼び出しのタイプと、サンプルのペイロードおよび応答のリストです。

## アップデート {#update}

An `update` 呼び出しは、ユニバーサルエディターを使用してアプリのコンテンツを編集する際に発生します。 The `update` は変更を保持します。

ペイロードには、JCR に書き戻す内容の詳細が含まれます。

* `resource`：更新する JCR パス
* `prop`：更新する JCR プロパティ
* `type`：更新するプロパティの JCR 値タイプ
* `value`：更新されたデータ

>[!BEGINTABS]

>[!TAB サンプルペイロード]

```json
{
  "connections": [
    {
      "name": "aem",
      "protocol": "aem",
      "uri": "https://localhost:8443"
    }
  ],
  "target": {
    "resource": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "type": "text",
    "prop": "jcr:title"
  },
  "value": "Tiny Toon Adventures"
}
```

>[!TAB レスポンスのサンプル]

```json
{
  "updates": [
    {
      "resource": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
      "prop": "jcr:title",
      "type": "text"
    }
  ]
}
```

>[!ENDTABS]

## 詳細 {#details}

A `details` アプリのコンテンツを取得するためにユニバーサルエディターでアプリを読み込む際に、呼び出しが発生します。

ペイロードには、レンダリングされるデータと、データが表す内容（スキーマ）の詳細が含まれており、ユニバーサルエディターでレンダリングできます。

* コンポーネントの場合、ユニバーサルエディターは `data` オブジェクトに含まれる必要はありません。データのスキーマがアプリ内で定義されているからです。
* コンテンツフラグメントの場合、ユニバーサルエディターでも `schema` オブジェクトの内容は、JCR でコンテンツフラグメントモデルが定義されているので、変更できません。

>[!BEGINTABS]

>[!TAB サンプルペイロード]

```json
{
  "connections": [
    {
      "name": "aem",
      "protocol": "aem",
      "uri": "https://localhost:8443"
    }
  ],
  "target": {
    "resource": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "type": "component",
    "prop": ""
  }
}
```

>[!TAB レスポンスのサンプル]

```json
{
  "data": {
    "jcr:primaryType": "nt:unstructured",
    "jcr:title": "Tiny Toon Adventures",
    "fileReference": "/content/dam/wknd-shared/en/adventures/riverside-camping-australia/adobestock-216674449.jpeg",
    "cq:panelTitle": "WKND Adventures",
    "actionsEnabled": "true",
    "jcr:lastModifiedBy": "admin",
    "titleFromPage": "false",
    "jcr:description": "<p>With WKND Adventures, you don't just see the world you experinece it.</p>\r\n",
    "jcr:lastModified": "Fri Jan 19 2024 11:05:59 GMT+0100",
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

>[!ENDTABS]

## 追加 {#add}

An `add` 呼び出しは、ユニバーサルエディターを使用してアプリに新しいコンポーネントを配置すると発生します。

ペイロードには、 `path` コンテンツを追加する場所を含むオブジェクト。

また、 `content` 保存するコンテンツのエンドポイント固有の詳細用の追加オブジェクトを含むオブジェクト [プラグインごとに](/help/implementing/universal-editor/architecture.md) 例えば、アプリがAEMとMagentoのコンテンツに基づいている場合、ペイロードには各システムのデータオブジェクトが含まれます。

>[!BEGINTABS]

>[!TAB サンプルペイロード]

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-pXXXX-eYYYYY.adobeaemcloud.com"
    }
  ],
  "target": {
    "container": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container",
      "prop": ""
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

>[!TAB レスポンスのサンプル]

```json
{
  "updates": [
    {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container"
    }
  ],
  "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1138559521"
}
```

>[!ENDTABS]

## 移動 {#move}

A `move` 呼び出しは、ユニバーサルエディターを使用してアプリ内のコンポーネントを移動すると発生します。

ペイロードには、 `from` コンポーネントの場所を定義するオブジェクトと `to` 移動先を定義するオブジェクト。

>[!BEGINTABS]

>[!TAB サンプルペイロード]

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-pXXXX-eYYYYY.adobeaemcloud.com"
    }
  ],
  "from": {
    "container": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container",
      "prop": ""
    },
    "component": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_275525847",
      "type": "media",
      "prop": "fileReference"
    }
  },
  "to": {
    "container": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container",
      "prop": ""
    }
  }
}
```

>[!TAB レスポンスのサンプル]

```json
{
  "updates": [
    {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container"
    }
  ]
}
```

>[!ENDTABS]

## 削除 {#remove}

A `remove` ユニバーサルエディターを使用してアプリ内のコンポーネントを削除すると、呼び出しが発生します。

ペイロードには、削除されたオブジェクトのパスが含まれます。

>[!BEGINTABS]

>[!TAB サンプルペイロード]

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-pXXXX-eYYYYY.adobeaemcloud.com"
    }
  ],
  "target": {
    "component": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_593170193",
      "type": "text",
      "prop": "text"
    },
    "container": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container",
      "prop": ""
    }
  }
}
```

>[!TAB レスポンスのサンプル]

```json
{
  "updates": [
    {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "prop": "",
      "type": "container"
    }
  ]
}
```

>[!ENDTABS]

## 公開 {#publish}

A `publish` クリック時に呼び出しが発生します **公開** 」ボタンをクリックして、編集したコンテンツを公開します。

ユニバーサルエディターはコンテンツを反復し、公開する必要がある参照のリストを生成します。

>[!BEGINTABS]

>[!TAB サンプルペイロード]

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-pXXXX-eYYYYY.adobeaemcloud.com"
    }
  ],
  "references": [
    "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
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
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_229050934",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_2123678383",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1668104604",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1138559521",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_275525847"
  ]
}
```

>[!TAB レスポンスのサンプル]

```json
{
  "publishes": [
    "/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway",
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

>[!ENDTABS]

## その他のリソース {#additional-resources}

* [ユニバーサルエディターイベント](/help/implementing/universal-editor/events.md)
