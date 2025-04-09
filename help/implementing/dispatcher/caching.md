---
title: AEM as a Cloud Service でのキャッシュ
description: AEM as a Cloud Service でのキャッシュの基本について
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
role: Admin
source-git-commit: 4a586a0022682dadbc57bab1ccde0ba2afa78627
workflow-type: tm+mt
source-wordcount: '3071'
ht-degree: 94%

---

# はじめに {#intro}

トラフィックは、CDN を経由して Apache Web サーバーレイヤーに渡されます。このレイヤーは、Dispatcher を含むモジュールをサポートします。パフォーマンスを向上させるために、主にキャッシュとして Dispatcher を使用し、パブリッシュノードでの処理を制限します。
Dispatcher 設定にルールを適用して、デフォルトのキャッシュ有効期限設定を変更すると、CDN でキャッシュできるようになります。Dispatcher の設定で `enableTTL` が有効な場合、Dispatcher は、結果として生成されるキャッシュの有効期限のヘッダーも順守します。これは、再公開されているコンテンツ以外でも特定のコンテンツを更新することを意味します。

このページでは、どのように Dispatcher キャッシュが無効化にされるか、また、クライアントサイドライブラリに関するブラウザーレベルでのキャッシュの動作についても説明します。

## キャッシュ {#caching}

Caching of HTTP responses in AEM as a Cloud Service’s CDN is controlled by the following HTTP response headers from the origin: `Cache-Control`, `Surrogate-Control`, or `Expires`.

These cache headers are typically set in AEM Dispatcher vhost configurations using mod_headers, but can also be set in custom Java™ code running in AEM Publish itself (see [How to enable CDN caching](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/enable-caching)).

The cache key for CDN resources contains the full request url, including query parameters, so every different query parameter will produce a different cache entry. Consider removing unwanted query parameters; [see below](#marketing-parameters) for improving cache hit ratio.

Origin responses that contain `private`, `no-cache` or `no-store` in  `Cache-Control` are not cached by the AEM as a Cloud Service’s CDN (see [How to disable CDN caching
](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/disable-caching) for more details).  Also, responses that are setting cookies, i.e. have a `Set-Cookie` response header are not cached by the CDN.

### HTML/Text {#html-text}

Dispatcher configuration sets some default caching headers for `text/html` content type.

* デフォルトでは、Apache レイヤーが送出する `cache-control` ヘッダーに基づいて、ブラウザーによって 5 分間キャッシュされます。CDN はこの値も順守します。
* デフォルトの HTML/Text キャッシュ設定は、`global.vars` で `DISABLE_DEFAULT_CACHING` 変数を次のように定義することで無効にできます。

```
Define DISABLE_DEFAULT_CACHING
```

このメソッドは、例えば、デフォルトで年齢ヘッダーが 0 に設定されているので、ビジネスロジックで（カレンダー日に基づいた値による）年齢ヘッダーの微調整が必要な場合に便利です。ただし、**デフォルトのキャッシュをオフにする場合は注意が必要です。**

* AEM as a Cloud Service の SDK Dispatcher ツールを使用して、`global.vars` の `EXPIRATION_TIME` 変数を定義することにより、すべての HTML/Text コンテンツに対して上書きできます。
* 次の Apache `mod_headers` ディレクティブを使用して、CDN とブラウザーキャッシュを個別に制御するなど、より細かいレベルでオーバーライドすることができます。

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header set Cache-Control "max-age=200"
       Header set Surrogate-Control "max-age=3600"
       Header set Age 0
  </LocationMatch>
  ```

  >[!NOTE]
  >サロゲート制御ヘッダーは、アドビが管理する CDN に適用されます。[顧客が管理する CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=ja#point-to-point-CDN) を使用する場合、CDN プロバイダーに応じて異なるヘッダーが必要になる場合があります。

  グローバルキャッシュコントロールヘッダーまたは広範囲の正規表現に一致するヘッダーを設定する場合は、プライベートに保つ必要があるコンテンツに適用されないように注意が必要です。複数のディレクティブを使用して、ルールをきめ細かく適用することを検討してください。とは言え、Dispatcher のドキュメントに記載されているように、AEM as a Cloud Service は Dispatcher によってキャッシュ不可であることが検出されたものに対してキャッシュヘッダーが適用されていることを検出すると、キャッシュヘッダーを削除します。AEM で常にキャッシュヘッダーを適用するように強制するには、次のように **`always`** オプションを追加できます。

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header unset Cache-Control
       Header unset Expires
       Header always set Cache-Control "max-age=200"
       Header set Age 0
  </LocationMatch>
  ```

  `src/conf.dispatcher.d/cache` の下のファイルに次のルール（デフォルト設定）があることを確認する必要があります。

  ```
  /0000
  { /glob "*" /type "allow" }
  ```

* 特定のコンテンツが **CDN で**&#x200B;キャッシュされないようにするには、Cache-Control ヘッダーを *private* に設定します。例えば、次の例では、**secure** という名前のディレクトリ下の HTML コンテンツが CDN でキャッシュされないようにしています。

  ```
     <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
     Header unset Cache-Control
     Header unset Expires
     Header always set Cache-Control "private"
    </LocationMatch>
  ```

* プライベートに設定された HTML コンテンツは CDN でキャッシュされませんが、[権限に影響を受けるキャッシュ](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=ja)が設定されている場合は Dispatcher でキャッシュでき、許可されたユーザーのみにコンテンツを提供できるようになります。

  >[!NOTE]
  >[Dispatcher-ttl AEM ACS Commons プロジェクト](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)を含む他のメソッドでは、値は上書きされません。

  >[!NOTE]
  >Dispatcher は独自の[キャッシュルール](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html?lang=ja)に従ってコンテンツをキャッシュする場合があります。コンテンツを完全にプライベートにするには、Dispatcher によってコンテンツがキャッシュされないようにします。

### クライアントサイドライブラリ（js、css） {#client-side-libraries}

* AEM のクライアントサイドライブラリフレームワークを使用する場合、変更があると一意のパスを持つ新しいファイルとして表現されるので、JavaScript と CSS コードはブラウザーが無期限にキャッシュできるような方法で生成されます。つまり、クライアントライブラリを参照する HTML は必要に応じて作成されるので、顧客は公開時に新しいコンテンツを体験できます。「不変」の値を考慮しない古いブラウザーでは、キャッシュコントロールは「不変」または 30 日に設定されます。
* 詳しくは、[クライアントサイドライブラリとバージョンの整合性](#content-consistency)を参照してください。

### BLOB ストレージに格納される大きい画像とコンテンツ {#images}

2022年5月中旬以降に作成されたプログラム（特に、プログラム ID が 65000 より大きい場合）のデフォルトの動作は、デフォルトでキャッシュされると同時に、リクエストの認証コンテキストも考慮されます。古いプログラム（プログラム ID が 65000 以下）は、デフォルトでは BLOB コンテンツをキャッシュしません。

どちらの場合も、キャッシュヘッダーは、Apache `mod_headers` ディレクティブを使用して、Apache／Dispatcher レイヤーでより細かいレベルでオーバーライドすることができます。次に例を示します。

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

Dispatcher レイヤーでキャッシュヘッダーを変更する場合は、広くキャッシュしすぎないように注意してください。[上記](#html-text)の「HTML/テキスト」節のディスカッションを参照してください。また、（キャッシュせずに）非公開にするアセットが、`LocationMatch` ディレクティブフィルターの一部ではないことも確認してください。

BLOB ストアに格納される JCR リソース（16 KB を超える）は、通常、AEM による 302 リダイレクトとして提供されます。これらのリダイレクトはインターセプトされ、その後に CDN が続き、コンテンツが BLOB ストアから直接配信されます。これらの応答でカスタマイズできるヘッダーのセットは限られています。例えば、`Content-Disposition` をカスタマイズするには、Dispatcher ディレクティブを次のように使用する必要があります。

```
<LocationMatch "\.(?i:pdf)$">
  ForceType application/pdf
  Header set Content-Disposition inline
  </LocationMatch>
```

BLOB 応答でカスタマイズ可能なヘッダーのリストは次のとおりです。

```
content-security-policy
x-frame-options
x-xss-protection
x-content-type-options
x-robots-tag
access-control-allow-origin
content-disposition
permissions-policy
referrer-policy
x-vhost
content-disposition
cache-control
vary
```

#### 新しいデフォルトのキャッシュ動作 {#new-caching-behavior}

AEM レイヤーは、キャッシュヘッダーがすでに設定されているかおよびリクエストタイプの値に応じて、キャッシュヘッダーを設定します。キャッシュコントロールヘッダーが設定されていない場合、公開コンテンツはキャッシュされ、認証済みトラフィックはプライベートに設定されます。キャッシュコントロールヘッダーが設定されている場合、キャッシュヘッダーは変更されません。

| キャッシュ制御ヘッダーが存在するか？ | リクエストタイプ | AEM が次に対してキャッシュヘッダーを設定 |
|------------------------------|---------------|------------------------------------------------|
| いいえ | パブリック | Cache-Control: public, max-age=600, immutable |
| いいえ | 認証済み | Cache-Control: private, max-age=600, immutable |
| はい | いずれか | 変更されない |

推奨はしませんが、Cloud Manager の環境変数 `AEM_BLOB_ENABLE_CACHING_HEADERS` を false に設定することで、新しいデフォルトの動作を古い動作（プログラム ID が 65000 以下）に従うように変更することが可能です。

#### 以前のデフォルトのキャッシュ動作 {#old-caching-behavior}

AEM レイヤーは、デフォルトでは BLOB コンテンツをキャッシュしません。

>[!NOTE]
>Cloud Manager 環境変数 AEM_BLOB_ENABLE_CACHING_HEADERS を true に設定して、古いデフォルトの動作を、新しい動作（65000 より大きいプログラム ID）と一致するように変更します。プログラムが既に実稼働している場合は、変更後に、コンテンツが期待どおりに動作することを確認してください。

現在、プライベートとマークされた Blob ストレージ内の画像は、[権限に影響を受けるキャッシュ](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=ja)を使用して Dispatcher でキャッシュできません。画像は常に AEM 接触チャネルから要求され、ユーザーが承認されている場合に提供されます。

>[!NOTE]
>[dispatcher-ttl AEM ACS Commons プロジェクト](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)などの他のメソッドでは、値は上書きされません。

### ノードストア内の他のコンテンツファイルタイプ {#other-content}

* デフォルトのキャッシュなし
* HTML／Text ファイルタイプに使用する `EXPIRATION_TIME` 変数はデフォルトに設定できません
* キャッシュの有効期限は、HTML/Text の節で説明したのと同じ LocationMatch 方法で、適切な正規表現を指定することで設定できます

### その他の最適化 {#further-optimizations}

* `User-Agent` を `Vary` ヘッダーの一部として使用しないでください。（アーキタイプバージョン 28 以前）の古いバージョンのデフォルトの Dispatcher 設定にはこれが含まれていたため、次の手順を使用して削除することをお勧めします。
   * `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost` で vhost ファイルを見つけます。
   * すべての vhost ファイルから、`Header append Vary User-Agent env=!dont-vary` を行ごと削除またはコメントアウトします（読み取り専用の default.vhost を除く）。
* ブラウザーのキャッシュとは別に、CDN キャッシュを制御するために `Surrogate-Control` ヘッダーを使用します。
* [`stale-while-revalidate`](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) および [`stale-if-error`](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) ディレクティブを適用することで、バックグラウンドでの更新を可能にし、キャッシュミスを回避して、ユーザーにとって高速で最新のコンテンツを維持することを検討してください。
   * これらのディレクティブを適用する方法は多数ありますが、30 分の `stale-while-revalidate` をすべてのキャッシュ制御ヘッダーに追加することは、出発点として適切です。
* 様々なコンテンツタイプの例が次に示されています。これらは、独自のキャッシュルールを設定する際にガイドとして使用できます。具体的な設定と要件を慎重に検討し、テストしてください。

   * 可変クライアントライブラリリソースを 12 時間キャッシュし、12 時間後にバックグラウンド更新を行います。

     ```
     <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
        Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * ミスを避けるために、不変のクライアントライブラリリソースをバックグラウンド更新で長期（30 日）にキャッシュします。

     ```
     <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
        Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * HTML のページを 5 分間キャッシュし、バックグラウンドの更新をブラウザーで 1 時間、CDN で 12 時間行います。Cache-Control ヘッダーは常に追加されるので、/content/* 下の一致する html ページが公開を意図したものであることが重要です。そうでない場合は、より詳細な正規表現の使用を検討してください。

     ```
     <LocationMatch "^/content/.*\.html$">
        Header unset Cache-Control
        Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
        Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * コンテンツサービス／Sling モデルエクスポーターの json レスポンスを 5 分間キャッシュし、バックグラウンド更新でブラウザーに1 時間、CDN に 12 時間キャッシュします。

     ```
     <LocationMatch "^/content/.*\.model\.json$">
        Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
        Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * ミスを避けるために、コア画像コンポーネントからの不変 URL をバックグラウンド更新で長期（30 日）にキャッシュします。

     ```
     <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
        Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * ミスを避けるために、24 時間の画像やビデオなど、DAM の可変リソースをキャッシュし、12 時間後にバックグラウンド更新を行います.

     ```
     <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
        Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

### CDN キャッシュヒット率の分析 {#analyze-chr}

ダッシュボードを使用した CDN ログのダウンロードとサイトのキャッシュサイト比の分析に関する情報は、[キャッシュヒット率の分析チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/caching/cdn-cache-hit-ratio-analysis.html?lang=ja)を参照してください。

### HEAD リクエスト動作 {#request-behavior}

キャッシュされて&#x200B;**いない**&#x200B;リソースに対する HEAD リクエストを Adobe CDN で受信すると、そのリクエストは Dispatcher や AEM インスタンスによって GET リクエストとして変換および受信されます。応答がキャッシュ可能な場合、以降の HEAD リクエストは CDN から提供されます。応答がキャッシュ可能でない場合、それ以降の HEAD リクエストは `Cache-Control` TTL に依存する期間、Dispatcher や AEM インスタンス、あるいはその両方に引き渡されます。

### マーケティングキャンペーンパラメーター {#marketing-parameters}

Web サイトの URL には、キャンペーンの成功をトラックするために使用されるマーケティングキャンペーンパラメーターが含まれることがよくあります。

2023年10月以降に作成された環境では、キャッシュリクエストを改善するために、CDN は、一般的なマーケティング関連のクエリパラメーター（特に、次の正規表現パターンに一致するパラメーター）を削除します。

```
^(utm_.*|gclid|gdftrk|_ga|mc_.*|trk_.*|dm_i|_ke|sc_.*|fbclid|msclkid|ttclid)$
```

この機能は、[CDN 設定](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#request-transformations)の `requestTransformations` フラグを使用してオンとオフを切り替えることができます。

例えば、CDN レベルでマーケティングパラメーターの削除を停止するには、次のセクションを含む設定を使用して `removeMarketingParams: false` をデプロイする必要があります。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  requestTransformations:
    removeMarketingParams: false
```

`removeMarketingParams` 機能が CDN レベルで無効になっている場合でも、Dispatcher 設定の `ignoreUrlParams` プロパティを設定することをお勧めします。[Dispatcher の設定 - URL パラメーターの無視](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#ignoring-url-parameters)を参照してください。

マーケティングパラメーターを無視する方法は 2 つあります。（最初のクエリは、クエリパラメーターを使用してキャッシュバスティングを無視する場合に推奨されます）。

1. すべてのパラメーターを無視し、使用するパラメータを選択的に許可します。
次の例では、`page` および `product` パラメーターのみが無視されず、リクエストは発行者に転送されます。

```
/ignoreUrlParams {
   /0001 { /glob "*" /type "allow" }
   /0002 { /glob "page" /type "deny" }
   /0003 { /glob "product" /type "deny" }
}
```

1. マーケティングパラメーターを除くすべてのパラメーターを許可します。ファイル [marketing_query_parameters.any](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.dispatcher.d/cache/marketing_query_parameters.any) は、無視される一般的マーケティングパラメーターのリストを定義します。アドビはこのファイルを更新しません。マーケティングプロバイダーに応じて、ユーザーが拡張できます。

```
/ignoreUrlParams {
   /0001 { /glob "*" /type "deny" }
   $include "../cache/marketing_query_parameters.any"
}
```


## Dispatcher キャッシュの無効化 {#disp}

通常、Dispatcher キャッシュを無効にする必要はありません。代わりに、コンテンツが再公開される際に Dispatcher がキャッシュを更新し、CDN がキャッシュの有効期限のヘッダーを考慮することを信頼できます。

### アクティベーション／非アクティベーション中の Dispatcher キャッシュの無効化 {#cache-activation-deactivation}

以前のバージョンの AEM と同様に、ページを公開または非公開にすると、Dispatcher のキャッシュからコンテンツがクリアされます。キャッシュに問題があると疑われる場合は、該当するページを再度公開し、`ServerAlias` localhost に一致する仮想ホスト（Dispatcher キャッシュの無効化に必要）が使用可能であることを確認する必要があります。

>[!NOTE]
>For proper Dispatcher invalidation, make sure that requests from &quot;127.0.0.1&quot;, &quot;localhost&quot;, &quot;\*.local&quot;, &quot;\*.adobeaemcloud.com&quot;, and &quot;\*.adobeaemcloud.net&quot; are all matched and handled by a vhost configuration so the request can be served. この作業を行うには、[AEM archetype](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.d/available_vhosts/default.vhost) の参照パターンに従って、キャッチオール vhost 設定で「*」をグローバルに一致させます。または、前述のリストがいずれかの vhost にキャッチされるようにすることもできます。

パブリッシュインスタンスは、オーサーから新しいバージョンのページまたはアセットを受け取ると、フラッシュエージェントを使用して Dispatcher 上の該当するパスを無効にします。更新されたパスは、親と共に、Dispatcher キャッシュから削除されます（削除されるレベルは [statfilelevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#invalidating-files-by-folder-level) で設定できます）。

## Dispatcher キャッシュの明示的な無効化 {#explicit-invalidation}

アドビでは、標準のキャッシュヘッダーを使用して、コンテンツ配信のライフサイクルを制御することをお勧めします。ただし、必要に応じて、Dispatcher のコンテンツを直接無効にすることもできます。

次のリストには、キャッシュを明示的に無効にするシナリオ（オプションで無効化の完了をリッスン）が含まれています。

* エクスペリエンスフラグメントやコンテンツフラグメントなどのコンテンツを公開した後、それらの要素を参照する公開済みおよびキャッシュされたコンテンツを無効化します。
* 参照ページが正常に無効化されると外部システムに通知します。

キャッシュを明示的に無効にする方法は 2 つあります。

* 推奨されるアプローチは、オーサーから Sling コンテンツ配布（SCD）を使用することです。
* もう 1 つのアプローチは、Replication API を使用して、パブリッシュ Dispatcher フラッシュレプリケーションエージェントを呼び出すことです。

アプローチは、階層の可用性、イベントの重複排除機能、イベント処理の保証の観点によって異なります。次の表に、これらのオプションの概要を示します。

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>アプローチ</th>
    <th>階層の可用性</th>
    <th>重複排除 </th>
    <th>保証 </th>
    <th>アクション </th>
    <th>影響 </th>
    <th>説明 </th>
  </tr>  
  <tr>
    <td>Sling コンテンツ配布（SCD）API</td>
    <td>オーサー</td>
    <td>Discovery API を使用するか、<a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">重複排除モード</a>を有効にすることで可能です。</td>
    <td>少なくとも 1 回。</td>
    <td>
     <ol>
       <li>追加</li>
       <li>削除</li>
       <li>無効化</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>階層／統計レベル</li>
       <li>階層／統計レベル</li>
       <li>レベルのリソースのみ</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>コンテンツを公開し、キャッシュを無効にします。</li>
       <li>コンテンツを削除し、キャッシュを無効にします。</li>
       <li>コンテンツを公開せずに無効化します。</li>
     </ol>
     </td>
  </tr>
  <tr>
    <td>レプリケーション API</td>
    <td>公開</td>
    <td>不可です。すべてのパブリッシュインスタンスで発生するイベントです。</td>
    <td>ベストエフォート。</td>
    <td>
     <ol>
       <li>アクティブ化</li>
       <li>非アクティブ化</li>
       <li>削除</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>階層／統計レベル</li>
       <li>階層／統計レベル</li>
       <li>階層／統計レベル</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>コンテンツを公開し、キャッシュを無効にします。</li>
       <li>オーサー層／パブリッシュ層から - コンテンツを削除し、キャッシュを無効にします。</li>
       <li><p><strong>オーサー層から</strong> - コンテンツを削除し、キャッシュを無効にします（パブリッシュエージェントの AEM オーサー層からトリガーされる場合）。</p>
           <p><strong>パブリッシュ層から</strong> - キャッシュのみを無効化します（フラッシュエージェントまたはリソースのみフラッシュエージェントの AEM パブリッシュ層からトリガーされる場合）。</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

キャッシュの無効化に直接関連する 2 つのアクションは、Sling コンテンツ配布（SCD）API の Invalidate and Replication API のディアクティベートです。

また、表からは、次のことがわかります。

* SCD API は、正確な知識を必要とする外部システムとの同期など、すべてのイベントを保証する必要がある場合に必要です。無効化呼び出しの時点でパブリッシュ層のアップスケーリングイベントがある場合、新しいパブリッシュがそれぞれ無効化を処理すると、追加のイベントが発生します。

* Replication API の使用は一般的なユースケースではありませんが、キャッシュを無効にするトリガーがオーサー層ではなくパブリッシュ層から提供される場合に使用できます。この方法は、Dispatcher の TTL が設定されている場合に役立ちます。

最後に、Dispatcher のキャッシュを無効にする場合は、オーサーの SCD API の無効化アクションを使用することをお勧めします。また、イベントをリッスンして、さらにダウンストリームアクションをトリガーすることもできます。

### Sling コンテンツ配布（SCD） {#sling-distribution}

>[!NOTE]
>以下の手順を使用する場合、カスタムコードはローカルではなく、AEM Cloud Service 開発環境でテストします。

オーサーで SCD アクションを使用する場合、実装パターンは次のようになります。

1. オーサーからカスタムコードを記述して Sling コンテンツ配布 [API](https://sling.apache.org/documentation/bundles/content-distribution.html) を呼び出し、パスのリストを含む無効化アクションを渡します。

```
@Reference
private Distributor distributor;

ResourceResolver resolver = ...; // the resource resolver used for authorizing the request
String agentName = "publish";    // the name of the agent used to distribute the request

String pathToInvalidate = "/content/to/invalidate";
DistributionRequest distributionRequest = new SimpleDistributionRequest(DistributionRequestType.INVALIDATE, false, pathToInvalidate);
distributor.distribute(agentName, resolver, distributionRequest);
```

* （オプション）すべての Dispatcher インスタンスで無効化されるリソースを反映するイベントをリッスンします。


```
package org.apache.sling.distribution.journal.shared;

import org.apache.sling.discovery.DiscoveryService;
import org.apache.sling.distribution.journal.impl.event.DistributionEvent;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import static org.apache.sling.distribution.DistributionRequestType.INVALIDATE;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_PATHS;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_TYPE;
import static org.apache.sling.distribution.event.DistributionEventTopics.AGENT_PACKAGE_DISTRIBUTED;
import static org.osgi.service.event.EventConstants.EVENT_TOPIC;

@Component(immediate = true, service = EventHandler.class, property = {
        EVENT_TOPIC + "=" + AGENT_PACKAGE_DISTRIBUTED
})
public class InvalidatedHandler implements EventHandler {
    private static final Logger LOG = LoggerFactory.getLogger(InvalidatedHandler.class);

    @Reference
    private DiscoveryService discoveryService;

    @Override
    public void handleEvent(Event event) {

        String distributionType = (String) event.getProperty(DISTRIBUTION_TYPE);

        if (INVALIDATE.name().equals(distributionType)) {
            boolean isLeader = discoveryService.getTopology().getLocalInstance().isLeader();
            // process the OSGi event on the leader author instance
            if (isLeader) {
                String[] paths = (String[]) event.getProperty(DISTRIBUTION_PATHS);
                String packageId = (String) event.getProperty(DistributionEvent.PACKAGE_ID);
                invalidated(paths, packageId);
            }
        }
    }

    private void invalidated(String[] paths, String packageId) {
        // custom logic
        LOG.info("Successfully applied package with id {}, paths {}", packageId, paths);
    }
}
```

<!-- Optionally, instead of using the isLeader approach, one could add an OSGi configuration for the PID org.apache.sling.distribution.journal.impl.publisher.DistributedEventNotifierManager and property deduplicateEvent=true. But we'll stick with just one strategy and not mention it (double-check this).**review this**-->

* （オプション）上記の `invalidated(String[] paths, String packageId)` メソッドでビジネスロジックを実行します。

>[!NOTE]
>
>Dispatcher が無効化されると、Adobe CDN はフラッシュされません。アドビが管理する CDN は TTL に従うので、フラッシュする必要はありません。

### レプリケーション API {#replication-api}

レプリケーション API の非アクティブ化アクションを使用する際の実装パターンを次に示します。

1. パブリッシュ層で Replication API を呼び出して、パブリッシュ Dispatcher フラッシュレプリケーションエージェントをトリガーします。

フラッシュエージェントのエンドポイントは設定できませんが、フラッシュエージェントと共に実行するパブリッシュサービスと一致させて、 Dispatcher を指すように事前設定されています。

フラッシュエージェントは、通常、OSGi のイベントまたはワークフローに基づくカスタムコードでトリガーできます。

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals("flush");
  }
});

Replicator.replicate (session,ReplicationActionType.DELETE,paths, options);
```

<!-- In general, it will not be necessary to manually invalidate content in the dispatcher, but it is possible if needed.

>[!NOTE]
>Prior to AEM as a Cloud Service, there were two ways of invalidating the dispatcher cache.
>
>1. Invoke the replication agent, specifying the publish dispatcher flush agent
>2. Directly calling the `invalidate.cache` API (for example, `POST /dispatcher/invalidate.cache`)
>
>The dispatcher's `invalidate.cache` API approach will no longer be supported since it addresses only a specific dispatcher node. AEM as a Cloud Service operates at the service level, not the individual node level and so the invalidation instructions in the [Invalidating Cached Pages From AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) page are not longer valid for AEM as a Cloud Service.

The replication flush agent should be used. This can be done using the [Replication API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). The flush agent endpoint is not configurable but pre-configured to point to the dispatcher, matched with the publish service running the flush agent. The flush agent can typically be triggered by OSGi events or workflows.

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 

The diagram presented below illustrates this.

![CDN](assets/cdnd.png "CDN")

If there is a concern that the dispatcher cache is not clearing, contact [customer support](https://helpx.adobe.com/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

## クライアントサイドライブラリとバージョンの整合性 {#content-consistency}

ページは、HTML、JavaScript、CSS、画像で構成されています。JS ライブラリ間の依存関係を考慮して、[クライアントサイドライブラリ（clientlibs）フレームワーク](/help/implementing/developing/introduction/clientlibs.md)を使用し、JavaScript および CSS リソースを HTML ページに読み込むことをお勧めします。

clientlibs フレームワークは、自動でバージョン管理を行います。つまり、デベロッパーはソース管理で JS ライブラリに対する変更をチェックインでき、顧客がリリースをプッシュすると最新バージョンが利用可能になります。このワークフローがない場合、デベロッパーは新しいバージョンのライブラリへの参照で HTML を手動で変更する必要があります。同じライブラリが多数の HTML テンプレートを共有している場合は特に負担がかかります。

新しいバージョンのライブラリが実稼動環境にリリースされると、参照する HTML ページは、更新されたライブラリバージョンへの新しいリンクで更新されます。ブラウザーのキャッシュが特定の HTML ページに対して期限切れになった後は、古いライブラリがブラウザーのキャッシュから読み込まれる心配はありません。これは、（AEM の）更新されたページが、必ず新しいバージョンのライブラリを参照するようになったからです。更新された HTML ページには、最新のライブラリバージョンがすべて含まれています。

この機能の背後にあるメカニズムは、シリアル化されたハッシュで、クライアントライブラリリンクに追加されます。これにより、ブラウザーが CSS/JS をキャッシュするための、一意のバージョン付き URL が確保されます。シリアル化されたハッシュは、クライアントライブラリの内容が変更された場合にのみ更新されます。つまり、新しいデプロイメントであっても、関連のない更新（クライアントライブラリの基になる CSS/JS に対する変更がない）が発生した場合、参照は同じままになります。その結果、ブラウザーキャッシュの中断を減らすことができます。

### クライアントサイドライブラリの Longcache バージョンの有効化 - AEM as a Cloud Service の SDK クイックスタート {#enabling-longcache}

HTML ページにインクルードされるデフォルトの clientlib は、次の例のようになります。

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

厳密な clientlib のバージョン管理が有効な場合、クライアントライブラリに長期ハッシュキーがセレクターとして追加されます。その結果、clientlib の参照は次のようになります。

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

厳密な clientlib のバージョン管理は、すべての AEM as a Cloud Service 環境で、デフォルトで有効になっています。

ローカル SDK クイックスタートで厳密な clientlib のバージョン管理を有効にするには、次の操作を実行します。

1. OSGi Configuration manager `<host>/system/console/configMgr` へ移動する。
1. Adobe Granite HTML Library Manager の OSGi Config を探します。
   * 「厳密なバージョン管理」チェックボックスをオンにして有効にします。
   * 「**長期クライアントサイドキャッシュキー**」というラベルの付いたフィールドに、値「/.*;hash」を入力します。
1. 変更内容を保存します。AEM as a Cloud Service は、開発、ステージング、実稼動環境でこの設定を自動的に有効にするので、この設定をソース管理に保存する必要はありません。
1. クライアントライブラリのコンテンツが変更されるたびに、新しいハッシュキーが生成され、HTML 参照が更新されます。
