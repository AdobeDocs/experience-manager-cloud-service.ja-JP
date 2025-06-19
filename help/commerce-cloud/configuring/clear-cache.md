---
title: コンポーネントとGraphQLのキャッシュのクリア
description: AEM CIFでキャッシュ消去機能を有効にし検証する方法について説明します。
feature: Commerce Integration Framework
role: Admin
exl-id: f89c07c7-631f-41a4-b5b9-0f629ffc36f0
source-git-commit: fb8b2645c0401d1358c7751db03a138dc2de2664
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 2%

---

# コンポーネントとGraphQLのキャッシュのクリア {#clear-cache}

このドキュメントでは、AEM CIFのクリアキャッシュ機能を有効にし検証するための包括的なガイドを提供します。

>[!NOTE]
>
> この機能は実験的なものです。

## CIF設定でのキャッシュ消去機能の有効化 {#enable-clear-cache}

デフォルトでは、CIF設定でキャッシュ消去機能は無効になっています。 有効にするには、対応するプロジェクトに以下を追加する必要があります。

* サーブレット `/bin/cif/invalidate-cache` を有効にします。これにより、（こちら [ に示すようにプロジェクトに `com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json` 設定を追加することで、clear-cache API とそれに対応するリクエストをトリガーすることができ ](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config.author/com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json) す。
  >[!NOTE]
  >
  > 設定は、オーサーインスタンスに対してのみ有効にする必要があります。

* 次に示すように、リスナーを有効にして、プロジェクトに `com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json` 設定を追加することで、AEM（公開およびオーサー）の各インスタンスからキャッシュをクリアします [ こちら ](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json)。
   * 設定は、オーサーインスタンスとパブリッシュインスタンスの両方で有効にする必要があります。
   * Dispatcherのキャッシュを有効にする（オプション）：上記の設定で `enableDispatcherCacheInvalidation` プロパティを true に設定することで、Dispatcher のキャッシュの消去設定を有効にできます。 これにより、Dispatcher からキャッシュをクリアする機能が提供されます。

     >[!NOTE]
     >
     > これは、パブリッシュインスタンスでのみ機能します。

   * また、上記の設定ファイルに商品、カテゴリ、CMSページに適したパターンを追加して、Dispatcher のキャッシュから削除する必要があります。

* 製品およびカテゴリに関連する対応するページを見つけるために SQL クエリのパフォーマンスを向上させるには、プロジェクトに対応するインデックスを追加します（推奨）。 詳しくは、[cifCacheInvalidationSupport](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.apps/src/main/content/jcr_root/_oak_index/cifCacheInvalidationSupport/.content.xml) を参照してください。

## キャッシュ消去機能の確認 {#verify-clear-cache}

すべてが正しく設定されていることを確認するには：

* 対応するサーブレットをオーサーインスタンスのAEMにトリガーします（例：[http://localhost:4502/bin/cif/invalidate-cache](http://localhost:4502/bin/cif/invalidate-cache)。200 HTTP 応答が返されます。
* ノードがオーサーインスタンスの次のパス `/var/cif/cacheinvalidation` に作成されていることを確認します。 ノード名は、パターン「`cmd_{{timestamp}}`」に従います。
* 各パブリッシュインスタンスで同じノードが作成されていることを確認します。

次に、キャッシュが正しくクリアされているかどうかを確認します。
1. 対応する PLP および PDP ページに移動します。
2. コマースエンジンの製品名またはカテゴリ名を更新します。 変更内容は、キャッシュの設定に基づいてAEMにすぐに反映されるわけではありません。
3. 次に示すように、サーブレット API をトリガーします。

   ```
   curl --location '{Author AEM Instance Url}/bin/cif/invalidate-cache' \
   --header 'Content-Type: application/json' \
   --header 'Authorization: ••••••' \ // Mandatory
   --header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
   --data '{
       "productSkus": ["Sku1", "Sku2"], // Optional: Pass the corresponding sku which got updated.
       "categoryUids":["CategoryUid"], // Optional : Pass the corresponding category-uid which got updated.
       "storePath": "/content/venia/us/en", // Mandatory : Needs to be given to know for which site we are removing the clear cache.
   }'
   ```

すべてが正常に動作すると、新しい変更がすべてのインスタンスに反映されます。 変更がパブリッシュインスタンスに表示されない場合は、関連する PLP および PDP ページにプライベート/匿名ブラウザーウィンドウでアクセスしてみてください。

>[!NOTE]
>
> パブリッシュインスタンスには、複数レベルのキャッシュレイヤーを含めることができます。 この機能は、AEMの内部メモリと Dispatcher からキャッシュをクリアする場合にのみ使用されます。

## キャッシュ無効化 API のクリア {#clear-cache-api}

これは、AEMからコマース関連データのキャッシュをクリアする場合は常にトリガーする必要がある API です。

要求の種類：`POST`

### ヘッダー

| パラメーター | 値 | 必須/必須 | コメント |
|------------------------------|-------------------|---|---|
| `Content-Type` | `application/json` | 必須 |  |
| `Authorization` | 対応するオーサーのユーザー資格情報（認証タイプ：基本認証） | 必須 | 対応するユーザー名とパスワードを追加します。 |


### ペイロード

次の表に、この機能が標準で提供する既存の属性を示します。 これらの `InvalidateType` プロパティは、必須属性（`storePath` など）と組み合わせて指定する必要があります。

| `invalidateType` | 値 | タイプ（配列/文字列/ブール値） | これにより、Dispatcher のキャッシュはクリアされますか。 | コメント |
|------------------------------|-------------------|---|---|---|
| `productSkus` | 製品の SKU - キャッシュから無効にする必要があります。 | 配列 | はい | 次のパターンを使用して、内部メモリからキャッシュを消去します：<br>```"\"sku\":\\s*\""```<br>Dispatcher<br><ul><li>対応する SKU の PDP ページキャッシュをクリアします</li><li>対応するカテゴリページのキャッシュを消去します（コマースからの graphql 応答に基づく）</li><li>次のクエリに基づいてキャッシュをクリアします。</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content, '{storePath}')<br>AND ( (content.[product] IN ('sku1','sku2') AND content.[productType] = 'combinedSku')<br> OR (content.[selection] IN ('sku1','sku2') AND content.[selectionType] IN ('combinedSku', 'sku')))``` |
| `categoryUids` | カテゴリの UID - キャッシュから無効にする必要があります。 | 配列 | はい | 次のパターンを使用して、内部メモリからキャッシュを消去します：<br>```"\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\""```<br>Dispatcher<br><ul><li>対応するデータ（その子カテゴリページを含む）のカテゴリページのキャッシュをクリアします</li><li>対応するカテゴリを持つすべての PDP ページをクリアします</li><li>次のクエリに基づいてキャッシュをクリアします。</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content,'{storePath}')<br>AND ((content.[categoryId] in ('category1','category2')<br>AND content.[categoryIdType] in ('uid'))<br>OR (content.[category] in ('category1','category2') AND content.[categoryType] in ('uid')))``` |
| `regexPatterns` | 正規表現パターンに基づいてGraphQL応答データをクリアする必要がある場合は、これを使用します。 | 配列 | いいえ | |
| `cacheNames` | この値は、対応するCIF GraphQL Client Configuration Factory/対応する StorePath GraphQL設定/GraphQL キャッシュ設定で定義されます。 | 配列 | いいえ | |
| `invalidateAll` | True または false | ブール値 | はい | |

この表は、すべての API 呼び出しで渡す必要がある必須プロパティを示しています。

| プロパティ | 値 | タイプ（配列/文字列/ブール値） | これにより、Dispatcher のキャッシュはクリアされますか。 | コメント |
|------------------------------|-------------------|---|---|---|
| `storePath` | キャッシュの削除元となるサイトパスの対応する値（例：venia プロジェクトとの参照としての `/content/venia/us/en`）。 | 文字列 | はい | これは、`invalidateType.` の組み合わせで指定する必要があります |

### API リクエストのサンプル

```
curl --location 'https://author-p10603-e145552-cmstg.adobeaemcloud.com/bin/cif/invalidate-cache' \
--header 'Content-Type: application/json' \
--header 'Authorization: ••••••' \
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

既存の属性ベースの機能（`categoryUids` など）で現在対応していないキャッシュをクリアする必要がある場合は、[ この参照ファイル ](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/ExtendedCategoryUidInvalidation.java) を参照して、新しいパターンを追加し、現在の実装が処理する範囲を超えてキャッシュからクリアする必要がある追加の `invalidatePaths` を定義します。

### 新しいカスタム属性の追加 {#new-custom-attribute}

例えば、既存の属性をキャッシュのクリアに使用しない場合は、独自の属性を柔軟に作成し、対応する機能を定義できます。

* AEMの内部メモリ（graphql レスポンス）からキャッシュをクリアするだけの場合は、[ このリファレンス ](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomInvalidation.java) に従う必要があります。
* 内部メモリと Dispatcher キャッシュからキャッシュをクリアする必要がある場合は、[ このリファレンス ](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomDispatcherInvalidation.java) に従う必要があります。
  >[!NOTE]
  >
  > `getPatterns()` メソッドに対して `null` を返すことで、内部消去キャッシュを無視できます。
