---
title: ユニバーサルエディターの呼び出し
description: デバッグ時に役立つユニバーサルエディターによってアプリに対して行われる様々なタイプの呼び出しについて説明します。
exl-id: 00d66e59-e445-4b5c-a5b1-c0a9f032ebd9
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 93%

---


# ユニバーサルエディターの呼び出し {#calls}

デバッグ時に役立つユニバーサルエディターによってアプリに対して行われる様々なタイプの呼び出しについて説明します。

## 概要 {#overview}

ユニバーサルエディターは、一連の定義された呼び出しを通じて実装されたアプリと通信します。エンドユーザーエクスペリエンスに対しては、透過的で、影響はありません。

ただし、開発者にとって、これらの呼び出しとその動作を理解することは、ユニバーサルエディターを使用してアプリケーションをデバッグする際に役立ちます。アプリを実装したにもかかわらず、期待どおりに動作しない場合は、ブラウザーで開発者ツールの「**ネットワーク**」タブを開いて、アプリのコンテンツを編集する場合に呼び出しを検査すると役立つ場合があります。

![ブラウザーの開発者ツールの「ネットワーク」タブでの詳細呼び出しの例](assets/calls-network-tab.png)

* 呼び出しの&#x200B;**ペイロード**&#x200B;には、更新する内容と更新方法の識別など、エディターによって更新される内容の詳細が含まれます。
* **応答**&#x200B;には、エディターサービスによって更新された内容の正確な詳細が含まれます。これは、エディターでコンテンツを簡単に更新できるようにするためです。`move` 呼び出しなどの特定の場合には、ページ全体を更新する必要があります。

呼び出しが正常に完了すると、リクエストと応答のペイロードを含むイベントがトリガーされます。これは、独自のアプリ用にカスタマイズできます。詳しくは、[ユニバーサルエディターイベント](/help/implementing/universal-editor/events.md)ドキュメントを参照してください。

ユニバーサルエディターがアプリに対して行う呼び出しのタイプのリストと、サンプルのペイロードおよび応答を次に示します。

## アップデート {#update}

ユニバーサルエディターを使用してアプリ内のコンテンツを編集すると、`update` 呼び出しが発生します。`update` により変更が保持されます。

ペイロードには、JCR に書き戻す内容の詳細が含まれます。

* `resource`：更新する JCR パス
* `prop`：更新する JCR プロパティ
* `type`：更新するプロパティの JCR 値タイプ
* `value`：更新するデータ

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

>[!TAB サンプル応答]

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

ユニバーサルエディターでアプリを読み込み、アプリのコンテンツを取得すると、`details` 呼び出しが発生します。

ペイロードには、レンダリングされるデータと、ユニバーサルエディターでレンダリングできるようにデータが表す内容（スキーマ）の詳細が含まれます。

* コンポーネントの場合、データのスキーマはアプリで定義されているので、ユニバーサルエディターは `data` オブジェクトのみを取得します。
* コンテンツフラグメントの場合、コンテンツフラグメントモデルは JCR で定義されているので、ユニバーサルエディターは `schema` オブジェクトも取得します。

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

>[!TAB サンプル応答]

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

ユニバーサルエディターを使用してアプリに新しいコンポーネントを配置すると、`add` 呼び出しが発生します。

ペイロードには、コンテンツを追加する場所を含む `path` オブジェクトが含まれます。

また、保存するコンテンツのエンドポイント固有の詳細 [ プラグインごとに ](/help/implementing/universal-editor/architecture.md) を表す追加のオブジェクトを持つ `content` オブジェクトも含まれます。 例えば、アプリがAEMとMagentoのコンテンツに基づいている場合、ペイロードには各システムのデータオブジェクトが含まれます。

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

>[!TAB サンプル応答]

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

ユニバーサルエディターを使用してアプリ内でコンポーネントを移動すると、`move` 呼び出しが発生します。

ペイロードには、コンポーネントの場所を定義する `from` オブジェクトと、コンポーネントの移動場所を定義する `to` オブジェクトが含まれます。

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

>[!TAB サンプル応答]

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

ユニバーサルエディターを使用してアプリ内のコンポーネントを削除すると、`remove` 呼び出しが発生します。

ペイロードには、削除されるオブジェクトのパスが含まれます。

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

>[!TAB サンプル応答]

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

ユニバーサルエディターの「**公開**」ボタンをクリックして、編集したコンテンツを公開すると、`publish` 呼び出しが発生します。

ユニバーサルエディターはコンテンツを反復して、公開する必要がある参照のリストを生成します。

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

>[!TAB サンプル応答]

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

