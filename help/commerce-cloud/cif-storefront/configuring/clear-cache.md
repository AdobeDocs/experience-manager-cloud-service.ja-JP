---
title: コンポーネントと GraphQL のキャッシュのクリア
description: AEM CIF でキャッシュ消去機能を有効にし、検証する方法について説明します。
feature: Commerce Integration Framework
role: Admin
exl-id: f89c07c7-631f-41a4-b5b9-0f629ffc36f0
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 84%

---


# コンポーネントと GraphQL のキャッシュのクリア {#clear-cache}

このドキュメントでは、AEM CIF のキャッシュ消去機能を有効にし、検証するための包括的なガイドを提供します。

>[!NOTE]
>
> この機能は実験段階です。

## CIF 設定でのキャッシュ消去機能の有効化 {#enable-clear-cache}

デフォルトでは、CIF 設定でキャッシュ消去機能は無効になっています。有効にするには、対応するプロジェクトに以下を追加する必要があります。

* サーブレットの `/bin/cif/invalidate-cache` を有効にします。これにより、以下に示すように、プロジェクトに `com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json` 設定を追加して、対応するリクエストで clear-cache API をトリガーできます [&#x200B; こちら &#x200B;](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config.author/com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json)。

  >[!NOTE]
  >
  > 設定は、オーサーインスタンスに対してのみ有効にする必要があります。

* 次に示すように、リスナーを有効にして、プロジェクトに `com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json` 設定を追加することにより、AEM（公開およびオーサー）の各インスタンスからキャッシュをクリアします [&#128279;](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json)。
   * 設定は、オーサーインスタンスとパブリッシュインスタンスの両方で有効にする必要があります。
   * Dispatcher のキャッシュを有効にする（オプション）：上記の設定で `enableDispatcherCacheInvalidation` プロパティを true に設定することで、Dispatcher のキャッシュの消去設定を有効にできます。これにより、Dispatcher からキャッシュを消去する機能が提供されます。

     >[!NOTE]
     >
     > これは、パブリッシュインスタンスでのみ機能します。

   * また、製品、カテゴリ、CMS ページに適したパターンを上記の設定ファイルに追加して、Dispatcher キャッシュから削除する必要があります。

* 製品およびカテゴリに関連する対応するページを見つけるための SQL クエリのパフォーマンスを向上させるには、プロジェクトに対応するインデックスを追加します（推奨）。詳しくは、[cifCacheInvalidationSupport](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.apps/src/main/content/jcr_root/_oak_index/cifCacheInvalidationSupport/.content.xml) を参照してください。

## キャッシュ消去機能の確認 {#verify-clear-cache}

すべてが正しく設定されていることを確認するには、以下を行います。

* 対応するサーブレットをオーサーインスタンスのAEMにトリガーします（例：[http://localhost:4502/bin/cif/invalidate-cache](http://localhost:4502/bin/cif/invalidate-cache)。200 HTTP 応答が返されます。
* ノードがオーサーインスタンスの次のパス `/var/cif/cacheinvalidation` に作成されていることを確認します。ノード名は、パターン「`cmd_{{timestamp}}`」に従います。
* 各パブリッシュインスタンスで同じノードが作成されていることを確認します。

次に、キャッシュが正しく消去されているかどうかを確認します。

1. 対応する PLP および PDP ページに移動します。
2. コマースエンジンの製品名またはカテゴリ名を更新します。変更内容は、キャッシュの設定に基づいて AEM にすぐに反映されるわけではありません。
3. 次に示すように、サーブレット API をトリガーします。

   ```
   curl --location '{Author AEM Instance Url}/bin/cif/invalidate-cache' \
   --header 'Content-Type: application/json' \
   --header 'Authorization: ******' \ // Mandatory
   --header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
   --data '{
       "productSkus": ["Sku1", "Sku2"], // Optional: Pass the corresponding sku which got updated.
       "categoryUids":["CategoryUid"], // Optional : Pass the corresponding category-uid which got updated.
       "storePath": "/content/venia/us/en", // Mandatory : Needs to be given to know for which site we are removing the clear cache.
   }'
   ```

すべてが正常に動作すると、新しい変更がすべてのインスタンスに反映されます。パブリッシュインスタンスで変更が表示されない場合は、プライベート／匿名ブラウザーウィンドウで関連する PLP および PDP ページにアクセスしてみてください。

>[!NOTE]
>
> パブリッシュインスタンスには、複数レベルのキャッシュレイヤーを含めることができます。この機能は、AEM の内部メモリと Dispatcher からキャッシュを消去する場合にのみ使用されます。

## キャッシュ無効化 API の消去 {#clear-cache-api}

これは、AEM からコマース関連データのキャッシュを消去する必要がある場合にトリガーする必要がある API です。

リクエストタイプ：`POST`

### ヘッダー {#headers}

| パラメーター | 値 | 必須 | コメント |
|------------------------------|-------------------|---|---|
| `Content-Type` | `application/json` | 必須 |  |
| `Authorization` | 対応するオーサーのユーザー資格情報（認証タイプ：基本認証） | 必須 | 対応するユーザー名とパスワードを追加します。 |


### ペイロード {#payload}

次の表に、この機能が標準で提供する既存の属性を示します。これらの `InvalidateType` プロパティは、必須属性（`storePath` など）と組み合わせて指定する必要があります。

| `invalidateType` | 値 | タイプ（配列／文字列／ブーリアン） | これにより、Dispatcher のキャッシュは消去されますか？ | コメント |
|------------------------------|-------------------|---|---|---|
| `productSkus` | 製品の SKU - キャッシュから無効にする必要があります。 | 配列 | はい | 次のパターン <br>```"\"sku\":\\s*\""```<br>Dispatcher<br> を使用して、内部メモリからキャッシュを消去します<ul><li>対応する SKU の PDP ページキャッシュを消去します</li><li>対応するカテゴリページのキャッシュを消去します（コマースからの GraphQL 応答に基づく）</li><li>次のクエリに基づいてキャッシュを消去します。</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content, '{storePath}')<br>AND ( (content.[product] IN ('sku1','sku2') AND content.[productType] = 'combinedSku')<br> OR (content.[selection] IN ('sku1','sku2') AND content.[selectionType] IN ('combinedSku', 'sku')))``` |
| `categoryUids` | カテゴリの UID - キャッシュから無効にする必要があります。 | 配列 | はい | 次のパターン <br>```"\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\""```<br>Dispatcher<br> を使用して、内部メモリからキャッシュを消去します<ul><li>対応するデータ（その子カテゴリページを含む）のカテゴリページのキャッシュを消去します</li><li>対応するカテゴリを持つすべての PDP ページを消去します</li><li>次のクエリに基づいてキャッシュを消去します。</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content,'{storePath}')<br>AND ((content.[categoryId] in ('category1','category2')<br>AND content.[categoryIdType] in ('uid'))<br>OR (content.[category] in ('category1','category2') AND content.[categoryType] in ('uid')))``` |
| `regexPatterns` | 正規表現パターンに基づいて GraphQL 応答データを消去する必要がある場合は、これを使用します。 | 配列 | いいえ | |
| `cacheNames` | この値は、対応するCIF GraphQL Client Configuration Factory/対応する StorePath GraphQL設定/GraphQL キャッシュ設定で定義されます。 | 配列 | いいえ | |
| `invalidateAll` | true または false | ブーリアン | はい | |

この表は、すべての API 呼び出しで渡す必要がある必須プロパティを示しています。

| プロパティ | 値 | タイプ（配列／文字列／ブーリアン） | これにより、Dispatcher のキャッシュは消去されますか？ | コメント |
|------------------------------|-------------------|---|---|---|
| `storePath` | キャッシュの削除元となるサイトパスの対応する値（例：venia プロジェクトとの参照としての `/content/venia/us/en`）。 | 文字列 | はい | これは、`invalidateType.` の組み合わせで指定する必要があります |

### API リクエストのサンプル {#sample-request}

```text
curl --location 'https://author-p10603-e145552-cmstg.adobeaemcloud.com/bin/cif/invalidate-cache' \
--header 'Content-Type: application/json' \
--header 'Authorization: ******' \
--header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
--data '{
"productSkus": ["VP01", "VT10"], // This will clear cache for the corresponding pages related with mentioned skus.
"categoryUids":["Mjk="], // This will clear cache for the corresponding pages related with mentioned categories.
"regexPatterns":["\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\"(Mjk=)\"", "\"sku\":\\s*\"(VP02|VP03)\""],
"cacheNames": ["venia/components/commerce/product"], // If this been added then it will clear respective caches for the corresponding storepath
"storePath": "/content/venia/us/en"
}'
```

## 拡張機能 {#clear-cache-extensibility}

この機能は、そのコア機能を提供するだけでなく、拡張性も提供するので、開発者は必要に応じて構築し、さらにカスタマイズできます。

### 既存の属性の拡張 {#existing-attribute}

既存の属性ベースの機能（`categoryUids` など）で現在対応していないキャッシュを消去する必要がある場合は、[この参照ファイル](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/ExtendedCategoryUidInvalidation.java)を参照して、新しいパターンを追加し、現在の実装で処理できる範囲を超えてキャッシュから消去する必要がある追加の `invalidatePaths` を定義できます。

### 新しいカスタム属性の追加 {#new-custom-attribute}

例えば、既存の属性をキャッシュの消去に使用しない場合は、独自の属性を柔軟に作成し、対応する機能を定義できます。

* AEMの内部メモリ（graphql レスポンス）からキャッシュをクリアするだけの場合は、[&#x200B; このリファレンス &#x200B;](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomInvalidation.java) に従う必要があります。
* 内部メモリと Dispatcher キャッシュからキャッシュをクリアする必要がある場合は、[&#x200B; このリファレンス &#x200B;](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomDispatcherInvalidation.java) に従ってください。

  >[!NOTE]
  >
  > `getPatterns()` メソッドに対して `null` を返すことで、内部消去キャッシュを無視できます。
