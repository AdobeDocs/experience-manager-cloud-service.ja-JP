---
title: AEM Edge Functionsでのキャッシュ
description: CDN キャッシュとEdge関数のキャッシュの取り込み方法、キャッシュ動作の設定方法、およびキャッシュされたコンテンツを両方のレイヤー間でパージする方法について説明します。
feature: Developing, Edge Delivery Services
role: Developer
source-git-commit: 4d3659aef1a180192a79b791f6ea840f576f5e63
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 1%

---

# AEM Edge Functionsでのキャッシュ {#edge-functions-caching}

>[!IMPORTANT]
>
>AEM Edge Functionsは&#x200B;**ベータ**&#x200B;機能です。 機能やドキュメントは予告なく変更される場合があります。 早期アクセスプログラムに参加してフィードバックを提供するには、[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)にメールを送信してください。

このページでは、AEM Edge Functions内でのキャッシュの仕組みに関する詳細な技術的ガイダンスを提供します。これには、2 キャッシュアーキテクチャ、コード内のキャッシュ動作の制御方法、コンテンツが変更されたときにキャッシュエントリをパージする方法などが含まれます。

AEM as a Cloud Service キャッシュの仕組みについて一般的な背景については、[AEM as a Cloud Serviceでのキャッシュ ](/help/implementing/dispatcher/caching.md)および[AEM as a Cloud ServiceでのCDN](/help/implementing/dispatcher/cdn.md)を参照してください。 コードの例については、[AEM Edge Functions Boilerplate — Caching](https://github.com/adobe/aem-edge-functions-boilerplate/blob/main/README.md#caching)を参照してください。

## アーキテクチャのキャッシュ {#architecture}

AEM Edge関数は、CDNと、関数が取得するバックエンドサービスの間に配置されます。 これらのバックエンドには、AEMパブリッシュインスタンス、サードパーティ API、外部データベース、またはコード呼び出しを行う任意のHTTP エンドポイントを使用できます。 リクエストフローには&#x200B;**2つの個別のキャッシュ**&#x200B;があり、それぞれ独立して動作します。

```
Browser → AEM CDN (CDN Cache) → AEM Edge Functions (Fetch Cache) → Backend (AEM, APIs, etc.)
```

| キャッシュ | キャッシュするもの | 影響を受けるユーザー | パージする方法 |
|---|---|---|---|
| **CDN キャッシュ** | Edge関数のブラウザーへの応答 | Edge関数によって設定された応答ヘッダー（`Cache-Control`、`Surrogate-Control`、`Surrogate-Key`） | [CDN キャッシュパージ API](/help/implementing/dispatcher/cdn-cache-purge.md) |
| **Edge関数がキャッシュを取得** | Edge関数内の`fetch()`呼び出しに対するバックエンド応答、およびCore Cache API経由で保存されたデータ | バックエンド応答ヘッダー、フェッチ呼び出し時の`CacheOverride`、またはCore Cache API経由のプログラマティック サロゲートキー | `aio aem edge-functions purge-cache` CLI コマンドまたは`purgeSurrogateKey()` |

各キャッシュには異なるスコープ、異なるコントロール、異なるパージ メカニズムがあるため、この2層アーキテクチャを理解することは不可欠です。 効果的なキャッシュを実現するには、両方のレベルで慎重に設定する必要があります。

## CDN キャッシュ （外部） {#cdn-cache}

CDN キャッシュは、ブラウザーとEdge機能の間にあります。 Edge関数の&#x200B;**response**&#x200B;をキャッシュします。 Edge関数のレスポンスに標準のHTTP キャッシュヘッダーを設定することで、その動作を制御できます。

```js
return new Response(body, {
  headers: {
    'Surrogate-Key': 'page-home product-123',
    'Cache-Control': 'public, max-age=3600'
  }
});
```

複数のサロゲートキーは、スペースで区切られます。 これらのサロゲート キーを使用して、[CDN キャッシュ パージ API](/help/implementing/dispatcher/cdn-cache-purge.md)を使用してCDN キャッシュをパージできます。 サロゲートキーのパージの概念は、[ リソースのグループのキャッシュをパージ ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache#purge-the-cache-for-a-group-of-resources)で説明したものと同じです。主な違いは、ここでのCDN サロゲートキーがバックエンドではなくEdge機能コードによって設定されることです。

## Edge関数の取得キャッシュ（内部） {#fetch-cache}

Edge関数の取得キャッシュは、Edge関数と呼び出すバックエンドの間にあります。 Edge関数コード内で行われた&#x200B;**バックエンドの応答**&#x200B;から`fetch()`呼び出しをキャッシュします。 また、[**Core Cache API**](https://js-compute-reference-docs.edgecompute.app/docs/fastly:cache/CoreCache/insert)または&#x200B;[**Simple Cache API**](https://js-compute-reference-docs.edgecompute.app/docs/fastly:cache/SimpleCache)を介してコードに格納されているデータも保持します。プログラムによるキャッシュ インターフェイスを使用すると、キャッシュされる内容、時間、サロゲート キーの下を詳細に制御できます。

これは、Edge関数の送信レスポンスに設定したヘッダーの影響を受ける&#x200B;**影響を受けません。バックエンドのレスポンス ヘッダー、フェッチ呼び出しの[`CacheOverride`](https://js-compute-reference-docs.edgecompute.app/docs/fastly:cache-override/CacheOverride/) オプション、またはCore Cache APIへの書き込み時にプログラムで割り当てたサロゲート キーによってのみ影響を受けます。**

>[!NOTE]
>
>ブラウザーに対するEdge関数の&#x200B;*送信レスポンス*&#x200B;に設定した`Surrogate-Key` ヘッダーは、この内部キャッシュではなく、**外部CDN キャッシュ**&#x200B;を制御します。 内部キャッシュのサロゲート キーは、バックエンドの`Surrogate-Key`応答ヘッダーから取得するか、Core Cache APIへの書き込み時に割り当てたキーから取得します。

### バックエンドの回答のキャッシュ {#cache-override}

特定の期間のバックエンド応答をキャッシュするには：

```js
import { CacheOverride } from "fastly:cache-override";

const response = await fetch(request, {
  backend: "my-origin",
  cacheOverride: new CacheOverride({ ttl: 300 })
});
```

### キャッシュのバイパス {#cache-pass}

フェッチ キャッシュを完全にバイパスし、常にバックエンドからフェッチするには、`pass` モードを使用します。

```js
import { CacheOverride } from "fastly:cache-override";

const response = await fetch(request, {
  backend: "my-origin",
  cacheOverride: new CacheOverride({ mode: "pass" })
});
```

## キャッシュの消去 {#cache-purging}

キャッシュされたコンテンツが古くなったら、明示的にパージする必要があります。 2つのキャッシュは独立して動作するため、無効化しているレイヤーとその相互作用を理解することが重要です。

### 両方のレイヤー間でパージを調整する {#coordinating-purges}

Edge関数はバックエンドとしてCDNの背後に配置されているため（[ オリジン セレクター](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors)を介して到達できます）、一方のキャッシュ レイヤーを他方なしでパージすると、予期しない結果が生じる可能性があります。

1. **CDN キャッシュ**&#x200B;のみをパージすると、次のリクエストでEdge関数が呼び出されます。 Edge関数のフェッチキャッシュに古いデータが保持されている場合は、古いコンテンツが返されます。CDNは再びキャッシュします。
2. **Edge関数キャッシュのみをパージ**&#x200B;すると、内部状態はクリアされますが、CDNは、有効期限が切れるか、個別にパージされるまで、以前にキャッシュされたコピーを引き続き提供します。

**ベストプラクティス：**&#x200B;基礎となるデータが変更された場合、**両方** キャッシュをパージ – 外側のレイヤーにはCDN キャッシュパージ APIを、内側のEdge関数レイヤーには`purge-cache` （または`purgeSurrogateKey()`）を使用します。 両方のレイヤーで一貫したサロゲートキーを使用すると、調整された無効化が簡単になります。 このパターンの完全な例については、[AEM Edge Functions Boilerplate — Purging](https://github.com/adobe/aem-edge-functions-boilerplate/blob/main/README.md#purging-the-edge-function-fetch-cache)を参照してください。

### CDN キャッシュのパージ {#purge-cdn-cache}

外部CDN キャッシュ （CDN レイヤーにキャッシュされたEdge関数のレスポンス）をパージするには、[CDN キャッシュパージ API](/help/implementing/dispatcher/cdn-cache-purge.md)を使用します。 これは、CDNにキャッシュされているすべてのAEM as a Cloud Service コンテンツに対して使用されるものと同じパージ メカニズムです。ステップバイステップのガイダンスについては、[CDN キャッシュをパージする方法](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache)を参照してください。

AEM as a Cloud Service アーキテクチャでは、Edge Functionsは[ オリジンセレクター](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors)を介してCDNからトラフィックを受け取ります（[CDN ルーティング ](/help/implementing/developing/introduction/edge-functions.md#cdn-routing)も参照）。 完全なリクエストフローは次のとおりです。

```
Client → AEM CDN (VCL) → Origin Selector → Edge Function → Backend
```

CDNは、Edge関数から返された最終応答をキャッシュします。 CDNのパージでは、外部キャッシュされたレスポンスが&#x200B;**only** クリアされます。これは、Edge関数の内部キャッシュには影響しません。

### Edge関数の取得キャッシュのパージ {#purge-fetch-cache}

`purge-cache` CLI コマンドは、**Edge関数のフェッチ キャッシュ** （Edge関数内にキャッシュされたバックエンド応答）をパージします。 外部CDN キャッシュを&#x200B;**not** パージします。 完全なCLI オプションとフラグについては、[`purge-cache` コマンド リファレンス ](https://github.com/adobe/aio-cli-plugin-aem-edge-functions/blob/main/README.md#purge-cache)を参照してください。

#### サロゲート キーの由来 {#surrogate-key-origin}

パージ コマンドで使用されるサロゲート キーは、キャッシュされたコンテンツに保存された時点で&#x200B;**タグ付けされていたキーと一致する必要があります**。 これは、AEM CDNで使用される[ サロゲート キーベースのパージ ](/help/implementing/dispatcher/cdn-cache-purge.md#surrogate-key-purge)と同じ概念ですが、Edge関数の内部キャッシュに適用されます。 これらのキーは次の場所から取得されます。

- Edge関数がバックエンドから取得したときにバックエンドが返す`Surrogate-Key`応答ヘッダー。
- [Core Cache API](https://js-compute-reference-docs.edgecompute.app/docs/fastly:cache/CoreCache/insert)への書き込み時にプログラムで割り当てるキー（キャッシュエントリの挿入時に`surrogateKeys` オプションを使用するなど）。

例えば、バックエンドが次のように応答する場合：

```
HTTP/1.1 200 OK
Content-Type: text/html
Surrogate-Key: page-about product-456 category-shoes
Cache-Control: public, max-age=3600
```

次に、キャッシュされた応答に、3つのサロゲートキー（`page-about`、`product-456`、および`category-shoes`）がタグ付けされます。 後で、これらのキーのいずれかを使用してパージできます。

```bash
# Purge all cached content tagged with "product-456"
aio aem edge-functions purge-cache <function-name> --surrogateKey product-456

# Purge multiple keys at once
aio aem edge-functions purge-cache <function-name> -k page-about -k category-shoes
```

>[!TIP]
>
>コンテンツモデルにマッピングする代替キーの命名規則を選択します（例：ページパス （`page-about`）、コンテンツ ID （`product-456`）、コンテンツタイプ （`category-shoes`）など）。 これにより、コンテンツの変更時に、ターゲットキャッシュの無効化を直感的に行うことができます。

#### すべて消去 {#purge-all}

```bash
# Purge all cached content (use with caution)
aio aem edge-functions purge-cache <function-name> --all
```

#### ソフトパージ {#soft-purge}

`--soft` フラグを使用してソフトパージを実行します。ソフトパージでは、古いエントリがキャッシュに保持され、古い再検証を有効にしながらバックエンドの負荷が軽減されます。

```bash
aio aem edge-functions purge-cache <function-name> --surrogateKey product-456 --soft
```

#### プログラムによるパージ {#programmatic-purge}

また、[`purgeSurrogateKey`](https://js-compute-reference-docs.edgecompute.app/docs/fastly:compute/purgeSurrogateKey)を使用して、Edge関数コード内からプログラムでサロゲートキーをパージすることもできます。

```js
import { purgeSurrogateKey } from "fastly:compute";

// Hard purge (immediate removal)
purgeSurrogateKey("product-456");

// Soft purge (retain stale entries for revalidation)
purgeSurrogateKey("product-456", true);
```

>[!CAUTION]
>
>キャッシュされたすべてのコンテンツをパージすると、バックエンドへのトラフィックが増加します。 `--all` フラグを慎重に使用し、可能な場合はターゲットを絞ったサロゲート キーのパージを優先します。