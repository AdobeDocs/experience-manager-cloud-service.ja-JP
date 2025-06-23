---
title: アセットセレクターと Dynamic Media Open API の統合
description: アセットセレクターを様々なアドビ、アドビ以外、サードパーティのアプリケーションと統合します。
role: Admin, User
exl-id: b01097f3-982f-4b2d-85e5-92efabe7094d
source-git-commit: 48a456039986abf07617d0828fbf95bf7661f6d6
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 98%

---

# OpenAPI 機能を備えた Dynamic Media の統合 {#integrate-asset-selector-dynamic-media-open-apis}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime と Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets と Edge Delivery Services の統合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Dynamic Media Prime と Ultimate の有効化</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

アセットセレクターを使用すると、様々なアドビアプリケーションを統合して、シームレスに連携できます。


## 前提条件 {#prereqs-polaris}

アセットセレクターと、OpenAPI 機能を備えた Dynamic Media の統合には、次の前提条件を使用します。

* [通信方法](/help/assets/overview-asset-selector.md#prereqs)
* OpenAPI 機能を備えた Dynamic Media にアクセスするには、次のライセンスが必要です。
   * アセットリポジトリ（例：Experience Manager Assets as a Cloud Service）。
   * AEM Dynamic Media。
* ブランドの一貫性を確保するために、[承認済みアセット](/help/assets/approve-assets.md)のみを使用できます。

## OpenAPI 機能を備えた Dynamic Media の統合 {#adobe-app-integration-polaris}

アセットセレクターと Dynamic Media OpenAPI プロセスの統合には、カスタマイズされた Dynamic Media URL の作成や、Dynamic Media URL を選択する準備など、様々な手順が含まれます。

### OpenAPI 機能を備えた Dynamic Media とのアセットセレクターの統合 {#integrate-dynamic-media}

OpenAPI 機能を備えた Dynamic Media では、`rootPath` プロパティと `path` プロパティを使用しないでください。代わりに、`aemTierType` プロパティを設定できます。設定の構文を以下に示します。

```
aemTierType:[1: "delivery"]
```

この設定により、すべての承認済みアセットをフォルダーなしで表示したり、フラットな構造として表示したりできます。詳しくは、[アセットセレクターのプロパティ](/help/assets/asset-selector-properties.md)の `aemTierType` プロパティを参照してください。


### 承認済みアセットからの動的配信 URL の作成 {#create-dynamic-media-url}

アセットセレクターを設定すると、オブジェクトのスキーマを使用して、選択したアセットから動的配信 URL が作成されます。
例えば、アセットの選択時に受信されるオブジェクトの配列からの 1 つのオブジェクトのスキーマは次のようになります。

```
{
"dc:format": "image/jpeg",
"repo:assetId": "urn:aaid:aem:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"repo:name": "image-7.jpg",
"repo:repositoryId": "delivery-pxxxx-exxxxxx.adobe.com",
...
}
```

すべての選択済みアセットは、JSON オブジェクトとして機能する `handleSelection` 関数によって実行されます。例えば、`JsonObj` のようになります。動的配信 URL は、以下のキャリアを組み合わせて作成されます。

| オブジェクト | JSON |
|---|---|
| ホスト | `assetJsonObj["repo:repositoryId"]` |
| API ルート | `/adobe/dynamicmedia/deliver` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"].split(".").slice(0,-1).join(".")` |
| format | `.jpg` |

#### 承認済みアセット配信 API 仕様 {#approved-assets-delivery-api-specification}

URL 形式：
`https://<delivery-api-host>/adobe/dynamicmedia/deliver/<asset-id>/<seo-name>.<format>?<image-modification-query-parameters>`

ここで、

* ホストは `https://delivery-pxxxxx-exxxxxx.adobe.com` です
* API ルートは `"/adobe/dynamicmedia/deliver"` です
* `<asset-id>` はアセット識別子です
* `<seo-name>` はアセットの名前です
* `<format>` は出力形式です
* `<image modification query parameters>` は、承認済みアセットの配信 API 仕様でサポートされています

#### 承認済みアセット配信 API {#approved-assets-delivery-api}

動的配信 URL の構文は次のとおりです。
`https://<delivery-api-host>/adobe/assets/deliver/<asset-id>/<seo-name>`、ここで、

* ホストは `https://delivery-pxxxxx-exxxxxx.adobe.com` です
* 元のレンディション配信の API ルートは `"/adobe/assets/deliver"` です。
* `<asset-id>` はアセット識別子です
* `<seo-name>` は、拡張子がある場合とない場合があるアセットの名前です。

### 動的配信 URL を選択する準備の完了 {#ready-to-pick-dynamic-delivery-url}

すべての選択済みアセットは、JSON オブジェクトとして機能する `handleSelection` 関数によって実行されます。例えば、`JsonObj` のようになります。動的配信 URL は、以下のキャリアを組み合わせて作成されます。

| オブジェクト | JSON |
|---|---|
| ホスト | `assetJsonObj["repo:repositoryId"]` |
| API ルート | `/adobe/assets/deliver` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"]` |

JSON オブジェクトをトラバースする 2 つの方法を以下に示します。

![動的配信 URL](assets/dynamic-delivery-url.png)

* **サムネール：**&#x200B;サムネールは画像にすることができ、アセットは PDF、ビデオ、画像などです。ただし、アセットのサムネールの高さと幅の属性を動的配信レンディションとして使用できます。
PDF タイプのアセットには、次のレンディションセットを使用できます。
サイドキックで PDF を選択すると、選択コンテキストに以下の情報が表示されます。JSON オブジェクトをトラバースする方法を以下に示します。

  <!--![Thumbnail dynamic delivery url](image-1.png)-->

  上記のスクリーンショットから、レンディションリンクの配列については `selection[0].....selection[4]` を参照できます。例えば、サムネールレンディションの 1 つに含まれる主要なプロパティは次のとおりです。

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/as/algorithm design.jpg?accept-experimental=1&width=319&height=319&preferwebp=true", 
      "type": "image/webp" 
  } 
  ```

上記のスクリーンショットでは、PDF が必要でサムネールは不要な場合は、PDF の元のレンディションの配信 URL をターゲットエクスペリエンスに組み込む必要があります。例えば、`https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/original/as/algorithm design.pdf?accept-experimental=1` のように指定します。

* **ビデオ：**&#x200B;埋め込み iFrame を使用するビデオタイプのアセットには、ビデオプレーヤーの URL を使用できます。ターゲットエクスペリエンスでは、次の配列レンディションを使用できます。
  <!--![Video dynamic delivery url](image.png)-->

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/as/asDragDrop.2.jpg?accept-experimental=1&width=319&height=319&preferwebp=true", 
      "type": "image/webp" 
  } 
  ```

  上記のスクリーンショットから、レンディションリンクの配列については `selection[0].....selection[4]` を参照できます。例えば、サムネールレンディションの 1 つに含まれる主要なプロパティは次のとおりです。

  上記のスクリーンショットのコードスニペットは、ビデオアセットの例です。これには、レンディションリンク配列が含まれます。抜粋の `selection[5]` は、ターゲットエクスペリエンス内のビデオサムネールのプレースホルダーとして使用できる画像サムネールの例です。レンディション配列の `selection[5]` は、ビデオプレーヤー用です。これは、HTML を提供し、iframe の `src` として設定できます。ビデオの web に最適化された配信であるアダプティブビットレートストリーミングをサポートします。

  上記の例では、ビデオ プレーヤーの URL は、`https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/play?accept-experimental=1` です。

### カスタムフィルターの設定 {#configure-custom-filters-dynamic-media-open-api}

OpenAPI 機能を備えた Dynamic Media のアセットセレクターを使用すると、カスタムプロパティとそれに基づくフィルターを設定できます。このようなプロパティを設定するには、`filterSchema` プロパティを使用します。カスタマイズは、`metadata.<metadata bucket>.<property name>.` として公開され、それに対してフィルターを設定できます。ここで、

* `metadata` はアセットの情報です
* `embedded` は、設定に使用される静的パラメーターです
* `<propertyname>` は、設定しているフィルター名です

設定では、`jcr:content/metadata/` レベルで定義されているプロパティが、設定するフィルターの `metadata.<metadata bucket>.<property name>.` として公開されます。

例えば、OpenAPI 機能を備えた Dynamic Media のアセットセレクターでは、フィルター設定のために `asset jcr:content/metadata/client_name:market` のプロパティが `metadata.embedded.client_name:market` に変換されます。

名前を取得するには、1 回限りのアクティビティを実行する必要があります。アセットの検索 API 呼び出しを行って、プロパティ名（基本的にはバケット）を取得します。

### OpenAPI 機能を備えた Dynamic Media のアセットセレクターのユーザーインターフェイス {#interface-dynamic-media-open-api}

アドビのマイクロフロントエンドアセットセレクターと統合すると、Experience Manager アセットリポジトリで使用可能なすべての承認済みアセットの、アセットのみの構造を表示できます。

![OpenAPI 機能を備えた Dynamic Media の UI](assets/polaris-ui.png)

* **A**：[パネルの非表示／表示](#hide-show-panel)
* **B**：[アセット](#repository)
* **C**：[並べ替え](#sorting)
* **D**：[フィルター](#filters)
* **E**：[検索バー](#search-bar)
* **F**：[昇順または降順での並べ替え](#sorting)
* **G**：選択をキャンセル
* **H**：1 つまたは複数のアセットを選択

>[!NOTE]
>
>フォルダーは、オーサーリポジトリに接続する場合にのみサポートされ、OpenAPI リポジトリを使用した Dynamic Media ではサポートされません。

>[!MORELIKETHIS]
>
>* [アセットセレクターと様々なアプリケーションの統合](/help/assets/integrate-asset-selector.md)
>* [アセットセレクターのプロパティ](/help/assets/asset-selector-properties.md)
>* [アセットセレクターのカスタマイズ](/help/assets/asset-selector-customization.md)
