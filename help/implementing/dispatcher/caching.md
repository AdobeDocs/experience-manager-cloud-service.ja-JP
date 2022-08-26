---
title: AEM as a Cloud Service でのキャッシュ
description: 'AEM as a Cloud Service でのキャッシュ '
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: a624b4f1999238adae2f6a03c2169cb30de9f730
workflow-type: tm+mt
source-wordcount: '2591'
ht-degree: 75%

---

# はじめに {#intro}

トラフィックは、CDN を経由して Apache Web サーバーレイヤーに渡されます。このレイヤーは、Dispatcher を含むモジュールをサポートします。パフォーマンスを向上させるために、Dispatcher は主にキャッシュとして使用され、公開ノードでの処理を制限します。
Dispatcher の設定にルールを適用して、デフォルトのキャッシュ有効期限の設定を変更し、CDN でのキャッシュを可能にします。Dispatcher の設定で `enableTTL` が有効な場合、Dispatcher は、結果として生成されるキャッシュの有効期限のヘッダーも順守します。これは、再公開されるコンテンツの外部でも特定のコンテンツが更新されることを意味します。

また、このページでは、Dispatcher キャッシュの無効化の方法、およびクライアントサイドライブラリに関するブラウザーレベルでのキャッシュの動作についても説明します。

## キャッシュ {#caching}

### HTML/Text {#html-text}

* デフォルトでは、Apache レイヤーで生成される `cache-control` ヘッダーに基づいて、ブラウザーによって 5 分間キャッシュされます。CDN はこの値も順守します。
* デフォルトの HTML/Text キャッシュ設定は、`global.vars` で `DISABLE_DEFAULT_CACHING` 変数を次のように定義することで無効にできます。

```
Define DISABLE_DEFAULT_CACHING
```

これは、例えば、デフォルトで年齢ヘッダーが 0 に設定されているので、ビジネスロジックで（カレンダー日に基づいた値による）年齢ヘッダーの微調整が必要な場合に便利です。ただし、**デフォルトのキャッシュをオフにする場合は注意が必要です。**

* AEM as a Cloud Service の SDK Dispatcher ツールを使用して、`global.vars` の `EXPIRATION_TIME` 変数を定義することにより、すべての HTML/Text コンテンツに対して上書きできます。
* 次の apache mod_headers ディレクティブを使用して、CDN とブラウザーキャッシュを独立に制御するなど、より詳細なレベルで上書きできます。

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Surrogate-Control "max-age=3600"
        Header set Age 0
   </LocationMatch>
   ```

   >[!NOTE]
   >サロゲート制御ヘッダーは、アドビが管理する CDN に適用されます。[顧客が管理する CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=ja#point-to-point-CDN) を使用する場合、CDN プロバイダーに応じて異なるヘッダーが必要になる場合があります。

   グローバルキャッシュコントロールヘッダーや、広い範囲の正規表現に一致するヘッダーを設定する場合は、非公開にするコンテンツに適用されないように注意が必要です。複数のディレクティブを使用して、ルールをきめ細かく適用することを検討してください。ただし、ディスパッチャーのドキュメントに記載されているように、ディスパッチャーが検出したキャッシュヘッダーにキャッシュを適用できないことが検出された場合、AEM as a Cloud Service によってキャッシュヘッダーが削除されます。AEM で常にキャッシュヘッダーを適用するように強制するには、次のように **always** オプションを追加します。

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
      Header always set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >[dispatcher-ttl AEM ACS Commons プロジェクト](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)を含む他のメソッドでは、値は上書きされません。

   >[!NOTE]
   >しかし、それでも Dispatcher は、独自の[キャッシュルール](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html?lang=ja)に従ってコンテンツをキャッシュする可能性があります。コンテンツを本当にプライベートにするには、Dispatcher によってキャッシュされないようにする必要があります。

### クライアントサイドライブラリ（js、css） {#client-side-libraries}

* AEM のクライアントサイドライブラリフレームワークを使用すると、変更が新しいファイルとして一意のパスで表示されるので、JavaScript と CSS コードは、ブラウザーで無期限にキャッシュできるように生成されます。つまり、クライアントライブラリを参照する HTML は必要に応じて作成されるので、顧客は公開時に新しいコンテンツを体験できます。「immutable」値を考慮しない古いブラウザーでは、cache-control は「immutable」または 30 日に設定されます。
* 詳しくは、[クライアントサイドライブラリとバージョンの整合性](#content-consistency)を参照してください。

### BLOB ストレージに格納される大きい画像とコンテンツ {#images}

2022年5月中旬以降に作成されたプログラム（特に、プログラム ID が 65000 より大きい場合）のデフォルトの動作は、デフォルトでキャッシュされると同時に、リクエストの認証コンテキストも考慮されます。古いプログラム（プログラム ID が 65000 以下）は、デフォルトでは BLOB コンテンツをキャッシュしません。

どちらの場合も、Apache／Dispatcher レイヤーでキャッシュヘッダーをより詳細なレベルで上書きするには、Apache `mod_headers` ディレクティブを使用します。次に例を示します。

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

Dispatcher レイヤーのキャッシュヘッダーを変更する場合は、あまり広くキャッシュしないように注意してください。[上記](#html-text)の HTML/Text の節の説明を参照してください。また、（キャッシュせずに）非公開にするアセットが、`LocationMatch` ディレクティブフィルターの一部ではないことも確認してください。

#### 新しいデフォルトのキャッシュ動作 {#new-caching-behavior}

AEM レイヤーは、キャッシュヘッダーの設定の有無、およびリクエストタイプの値に応じて、キャッシュヘッダーを設定します。キャッシュ制御ヘッダーが設定されていない場合、パブリックコンテンツはキャッシュされ、認証済みトラフィックはプライベートに設定されます。キャッシュ制御ヘッダーが設定されている場合、キャッシュヘッダーは変更されません。

| キャッシュ制御ヘッダーが存在するか？ | リクエストタイプ | AEM が次に対してキャッシュヘッダーを設定 |
|------------------------------|---------------|------------------------------------------------|
| いいえ | パブリック | Cache-Control: public, max-age=600, immutable |
| いいえ | 認証済み | Cache-Control: private, max-age=600, immutable |
| はい | 任意 | 変更されない |

推奨はしませんが、Cloud Manager の環境変数 `AEM_BLOB_ENABLE_CACHING_HEADERS` を false に設定することで、新しいデフォルトの動作を古い動作（プログラム ID が 65000 以下）に従うように変更することが可能です。

#### 以前のデフォルトのキャッシュ動作 {#old-caching-behavior}

AEM レイヤーは、デフォルトでは BLOB コンテンツをキャッシュしません。

>[!NOTE]
>Cloud Manager 環境変数 AEM_BLOB_ENABLE_CACHING_HEADERS を true に設定して、古いデフォルトの動作を、新しい動作（65000 より大きいプログラム ID）と一致するように変更することをお勧めします。プログラムが既に実稼働している場合は、変更後に、コンテンツが期待どおりに動作することを確認してください。

>[!NOTE]
>[dispatcher-ttl AEM ACS Commons プロジェクト](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)を含む他のメソッドでは、値は上書きされません。

### ノードストア内の他のコンテンツファイルタイプ {#other-content}

* デフォルトのキャッシュなし
* HTML／Text ファイルタイプに使用する `EXPIRATION_TIME` 変数はデフォルトに設定できません
* キャッシュの有効期限は、HTML/Text の節で説明したのと同じ LocationMatch 方法で、適切な正規表現を指定することで設定できます

### その他の最適化 {#further-optimizations}

* `User-Agent` を `Vary` ヘッダーの一部として使用しないでください。（アーキタイプバージョン 28 以前）の古いバージョンのデフォルトの Dispatcher 設定には、これが含まれているので、次の手順を使用して削除することをお勧めします。
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

   * HTML ページを 5 分間キャッシュし、バックグラウンド更新でブラウザーに 1 時間、CDN に 12 時間キャッシュします。Cache-Control ヘッダーは常に追加されるので、/content/* 下の一致する html ページが公開を意図したものであることが重要です。そうでない場合は、より詳細な正規表現の使用を検討してください。

      ```
      <LocationMatch "^/content/.*\.html$">
         Header unset Cache-Control
         Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * コンテンツサービス／Sling モデルエクスポーターの json レスポンスを 5 分間キャッシュし、バックグラウンド更新でブラウザーに 1 時間、CDN に 12 時間キャッシュします。

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

   * ミスを避けるために、24 時間の画像やビデオなど、DAM の可変リソースをキャッシュし、12 時間後にバックグラウンド更新を行います

      ```
      <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

### HEAD リクエスト動作 {#request-behavior}

キャッシュされて&#x200B;**いない**&#x200B;リソースに対する HEAD リクエストを Adobe CDN で受信すると、リクエストは Dispatcher や AEM インスタンスによって GET リクエストとして変換および受信されます。応答がキャッシュ可能な場合、以降の HEAD リクエストは CDN から提供されます。レスポンスがキャッシュ可能でない場合、それ以降の HEAD リクエストは `Cache-Control` TTL に依存する期間、Dispatcher や AEM インスタンスに引き渡されます。

<!---### Marketing campaign parameters {#marketing-parameters}

Marketing campaign parameters are added to a website to track different marketing campaigns but rarely have impact on how the website should look like. That's why in the dispatcher they can mostly be ignored for dispatcher caching decisions. This can be achieved by setting the [ignoreUrlParams](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters) parameter.
Adobe maintains a list of commonly used marketing query parameters in the file `conf.dispatcher.d/cache/marketing_query_parameters.any`. Uncomment the lines that are used by the websites marketing campaigns and uncomment the `/ignoreUrlParams` section in the enabled farm.

```
/ignoreUrlParams {
 	/0001 { /glob "*" /type "deny" }
 	$include "../cache/marketing_query_parameters.any"
}
```
-->

## Dispatcher キャッシュの無効化 {#disp}

一般に、Dispatcher キャッシュを無効にする必要はありません。代わりに、コンテンツが再公開される際に Dispatcher がキャッシュを更新し、CDN がキャッシュの有効期限のヘッダーを考慮することを信頼できます。

### アクティベーション／非アクティベーション中の Dispatcher キャッシュの無効化 {#cache-activation-deactivation}

以前のバージョンの AEM と同様に、ページの公開または非公開では、Dispatcher のキャッシュからコンテンツがクリアされます。キャッシュに問題があると疑われる場合は、該当するページを再度公開し、ServerAlias localhost に一致する仮想ホスト（Dispatcher キャッシュの無効化に必要）が使用可能であることを確認する必要があります。

パブリッシュインスタンスは、オーサーから新しいバージョンのページまたはアセットを受け取ると、フラッシュエージェントを使用して Dispatcher 上の適切なパスを無効にします。更新されたパスは、親と共に、Dispatcher キャッシュから削除されます（削除されるレベルは [statfilelevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#invalidating-files-by-folder-level) で設定できます）。

## Dispatcher キャッシュの明示的な無効化 {#explicit-invalidation}

Adobeでは、標準のキャッシュヘッダーを使用して、コンテンツ配信のライフサイクルを制御することをお勧めします。 ただし、必要に応じて、Dispatcher 内のコンテンツを直接無効にすることができます。

以下のリストに、（オプションで無効化の完了をリッスンしながら）キャッシュを明示的に無効にする場合があるシナリオを示します。

* エクスペリエンスフラグメントやコンテンツフラグメントなどのコンテンツを公開した後、それらの要素を参照する公開済みおよびキャッシュされたコンテンツを無効化します。
* 参照ページが正常に無効化された場合に外部システムに通知します。

キャッシュを明示的に無効にする方法は 2 つあります。

* 推奨されるアプローチは、オーサーから Sling コンテンツ配布 (SCD) を使用することです。
* レプリケーション API を使用して、パブリッシュ Dispatcher フラッシュレプリケーションエージェントを呼び出す。

アプローチは、階層の可用性、イベントの重複排除機能、イベント処理の保証の点で異なります。 次の表に、これらのオプションの概要を示します。

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>該当なし</th>
    <th>階層の可用性</th>
    <th>重複排除 </th>
    <th>保証 </th>
    <th>アクション </th>
    <th>影響 </th>
    <th>説明 </th>
  </tr>  
  <tr>
    <td>Sling コンテンツ配布 (SCD)API</td>
    <td>オーサー</td>
    <td>Discovery API を使用するか、 <a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">重複排除モード</a>.</td>
    <td>少なくとも 1 回は。</td>
    <td>
     <ol>
       <li>ADD</li>
       <li>DELETE</li>
       <li>無効化</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>階層/統計レベル</li>
       <li>階層/統計レベル</li>
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
    <td>パブリッシュ</td>
    <td>不可能です。すべてのパブリッシュインスタンスで発生するイベントです。</td>
    <td>ベストエフォート。</td>
    <td>
     <ol>
       <li>有効化</li>
       <li>無効化</li>
       <li>DELETE</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>階層/統計レベル</li>
       <li>階層/統計レベル</li>
       <li>階層/統計レベル</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>コンテンツを公開し、キャッシュを無効にします。</li>
       <li>オーサー層/パブリッシュ層から — コンテンツを削除し、キャッシュを無効にします。</li>
       <li><p><strong>オーサー層から</strong>  — コンテンツを削除し、キャッシュを無効にします（パブリッシュエージェントの AEM オーサー層からトリガーされる場合）。</p>
           <p><strong>パブリッシュ層から</strong>  — キャッシュのみを無効化します（フラッシュエージェントまたはリソースのみフラッシュエージェントの AEM パブリッシュ層からトリガーされた場合）。</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

キャッシュの無効化に直接関連する 2 つのアクションは、Sling Content Distribution(SCD)API 無効化とレプリケーション API 無効化です。

また、表からは、次のことがわかります。

* SCD API は、正確な知識を必要とする外部システムとの同期など、すべてのイベントが保証される必要がある場合に必要です。 無効化呼び出しの時点でパブリッシュ層のアップスケーリングイベントがある場合、新しい各パブリッシュが無効化を処理すると、追加のイベントが発生します。

* レプリケーション API の使用は一般的な使用例ではありませんが、キャッシュを無効にするトリガーがオーサー層ではなくパブリッシュ層から提供される場合に使用します。 これは、Dispatcher の TTL が設定されている場合に役立ちます。

最後に、Dispatcher のキャッシュを無効にする場合は、オーサーから SCD API の無効化アクションを使用することをお勧めします。 また、イベントをリッスンして、さらにダウンストリームアクションをトリガー化することもできます。

### Sling コンテンツ配布 (SCD) {#sling-distribution}

>[!NOTE]
>以下の手順を使用する場合、カスタムコードはローカルではなく、AEM Cloud Service開発環境でテストする必要があることに注意してください。

オーサーの SCD アクションを使用する場合、実装パターンは次のようになります。

1. オーサーから、カスタムコードを記述して Sling コンテンツ配布を呼び出します。 [API](https://sling.apache.org/documentation/bundles/content-distribution.html)を呼び出し、パスのリストを持つ無効化アクションを渡す場合、以下の処理を実行します。

```
@Reference
private Distributor distributor;

ResourceResolver resolver = ...; // the resource resolver used for authorizing the request
String agentName = "publish";    // the name of the agent used to distribute the request

String pathToInvalidate = "/content/to/invalidate";
DistributionRequest distributionRequest = new SimpleDistributionRequest(DistributionRequestType.INVALIDATE, false, pathToInvalidate);
distributor.distribute(agentName, resolver, distributionRequest);
```

* （オプション）すべての Dispatcher インスタンスに対して無効化されるリソースを反映するイベントをリッスンします。


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

* （オプション）ビジネスロジックを `invalidated(String[] paths, String packageId)` メソッドを使用します。

>[!NOTE]
>
>Dispatcher が無効化されると、AdobeCDN はフラッシュされません。 Adobeが管理する CDN は TTL に従うので、フラッシュする必要はありません。

### レプリケーション API {#replication-api}

レプリケーション API の非アクティブ化アクションを使用する際の実装パターンを次に示します。

1. パブリッシュ層で、レプリケーション API を呼び出して、パブリッシュ Dispatcher フラッシュレプリケーションエージェントをトリガーにします。

フラッシュエージェントエンドポイントは設定できず、フラッシュエージェントと共に実行されるパブリッシュサービスと一致する Dispatcher を指すように事前に設定されています。

フラッシュエージェントは、通常、OSGi のイベントまたはワークフローに基づくカスタムコードによってトリガーされます。

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals(“flush”);
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

If there is a concern that the dispatcher cache isn't clearing, contact [customer support](https://helpx.adobe.com/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

## クライアントサイドライブラリとバージョンの整合性 {#content-consistency}

ページは、HTML、JavaScript、CSS、画像で構成されます。JS ライブラリ間の依存関係を考慮して、[クライアントサイドライブラリ（clientlibs）フレームワーク](/help/implementing/developing/introduction/clientlibs.md)を活用し、JavaScript および CSS リソースを HTML ページに読み込むことをお勧めします。

clientlibs フレームワークは、自動バージョン管理を提供します。つまり、開発者はソース管理で JS ライブラリに対する変更をチェックインでき、最新バージョンは、顧客がリリースをプッシュしたときに利用可能になります。この機能がないと、開発者は新しいバージョンのライブラリを参照して HTML を手動で変更する必要があります。同じライブラリを共有する HTML テンプレートが多い場合は特に負担がかかります。

新しいバージョンのライブラリが実稼動環境にリリースされると、参照する HTML ページは、更新されたライブラリバージョンへの新しいリンクで更新されます。特定の HTML ページのブラウザーキャッシュの有効期限が切れると、（AEM から）更新されたページが新しいバージョンのライブラリを参照することが保証されるので、古いライブラリがブラウザーキャッシュから読み込まれる心配はありません。更新された HTML ページには、最新のライブラリバージョンがすべて含まれます。

このメカニズムはシリアル化されたハッシュで、クライアントライブラリリンクに追加され、ブラウザーが CSS／JS をキャッシュするための一意のバージョン付き URL を確保します。シリアル化されたハッシュは、クライアントライブラリの内容が変更された場合にのみ更新されます。つまり、新しいデプロイメントでも、関係ない更新（クライアントライブラリの基になる CSS／JS の変更はなし）が発生した場合、参照は同じままになるので、ブラウザーのキャッシュの中断が少なくなります。

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
   * 「長期クライアントサイドキャッシュキー」というラベルの付いたフィールドに、値「/.*;hash」を入力します。
1. 変更内容を保存します。AEM as a Cloud Service は、開発、ステージ、実稼動環境でこの設定を自動的に有効にするので、この設定をソース管理に保存する必要はありません。
1. クライアントライブラリのコンテンツが変更されるたびに、新しいハッシュキーが生成され、HTML 参照が更新されます。
