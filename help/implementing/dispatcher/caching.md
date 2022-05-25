---
title: AEM as a Cloud Service でのキャッシュ
description: 'AEM as a Cloud Service でのキャッシュ '
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: 2df0c88d82554362879f6302e8f7c784cb96d2b8
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 63%

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
   >サロゲート制御ヘッダーは、管理されるAdobeCDN に適用されます。 を使用している場合、 [顧客管理 CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en#point-to-point-CDN)の場合、CDN プロバイダーに応じて異なるヘッダーが必要になる場合があります。

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

### BLOB ストレージに格納できるほど大きい画像とコンテンツ {#images}

2022 年 5 月中旬以降に作成されたプログラム ( 特に、65000より大きいプログラム ID の場合 ) のデフォルトの動作は、デフォルトでキャッシュされると同時に、リクエストの認証コンテキストも考慮されます。 古いプログラム ( プログラム ID が65000以下 ) は、デフォルトでは BLOB コンテンツをキャッシュしません。

どちらの場合も、Apache/Dispatcher レイヤーでキャッシュヘッダーをより詳細なレベルで上書きするには、Apache を使用します `mod_headers` ディレクティブ。次に例を示します。

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

Dispatcher レイヤーのキャッシュヘッダーを変更する場合は、あまり広くキャッシュしないように注意してください。HTML/テキストの節の説明を参照してください [上](#html-text)) をクリックします。 また、（キャッシュではなく）非公開にするアセットが、 `LocationMatch` ディレクティブフィルター。

#### 新しいデフォルトのキャッシュ動作 {#new-caching-behavior}

AEMレイヤーは、キャッシュヘッダーが既に設定されているかどうかと、リクエストタイプの値に応じて、キャッシュヘッダーを設定します。 キャッシュ制御ヘッダーが設定されていない場合、パブリックコンテンツはキャッシュされ、認証済みトラフィックはプライベートに設定されます。 キャッシュ制御ヘッダーが設定されている場合、キャッシュヘッダーは変更されません。

| キャッシュ制御ヘッダーが存在しますか？ | 要求のタイプ | AEMがキャッシュヘッダーを |
|------------------------------|---------------|------------------------------------------------|
| 不可 | 公開 | Cache-Control:public, max-age=600, immutable |
| 不可 | 認証済み | Cache-Control:private, max-age=600, immutable |
| 対応 | 任意 | 変更せずそのままにする必要があります |

お勧めしませんが、 Cloud Manager 環境変数を設定することで、新しいデフォルトの動作を変更して、古い動作 ( プログラム ID が65000以下 ) に従うようにすることができます `AEM_BLOB_ENABLE_CACHING_HEADERS` を false に設定します。

#### 以前のデフォルトのキャッシュ動作 {#old-caching-behavior}

AEMレイヤーは、デフォルトでは BLOB コンテンツをキャッシュしません。

>[!NOTE]
>Cloud Manager 環境変数AEM_BLOB_ENABLE_CACHING_HEADERS を true に設定して、古いデフォルトの動作を、新しい動作 (65000より大きいプログラム ID) と一致するように変更することをお勧めします。 プログラムが既にライブになっている場合は、変更後に、コンテンツが期待どおりに動作することを確認してください。

>[!NOTE]
>その他のメソッド ( [dispatcher-ttl AEM ACS Commons プロジェクト](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)が値を上書きすることはありません。

### ノードストア内の他のコンテンツファイルタイプ {#other-content}

* デフォルトのキャッシュなし
* HTML／Text ファイルタイプに使用する `EXPIRATION_TIME` 変数はデフォルトに設定できません
* キャッシュの有効期限は、HTML/Text の節で説明したのと同じ LocationMatch 方法で、適切な正規表現を指定することで設定できます

### その他の最適化 {#further-optimizations}

* を使用しない `User-Agent` の一部として `Vary` ヘッダー。 デフォルトの Dispatcher 設定（アーキタイプバージョン 28 以前）の古いバージョンには、これが含まれていました。次の手順を使用して削除することをお勧めします。
   * で vhost ファイルを見つけます。 `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * 次の行を削除またはコメントアウトします。 `Header append Vary User-Agent env=!dont-vary` すべての vhost ファイルから、default.vhost を除き、読み取り専用です。
* 以下を使用： `Surrogate-Control` ブラウザーのキャッシュとは無関係に CDN キャッシュを制御するヘッダー
* 適用を検討 [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) および [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) ディレクティブを使用して、バックグラウンドでの更新を許可し、キャッシュのミスを回避し、ユーザーのコンテンツを迅速かつ新しく保ちます。
   * これらのディレクティブを適用する方法は多数ありますが、30 分を追加します。 `stale-while-revalidate` すべてのキャッシュ制御ヘッダーへの接続は、出発点として適切です。
* 様々なコンテンツタイプの例が次に示されています。独自のキャッシュルールを設定する際に、ガイドとして使用できます。 具体的な設定と要件を慎重に検討し、テストしてください。

   * 12 時間後に可変クライアントライブラリリソースをキャッシュし、12 時間後にバックグラウンド更新をおこないます。

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * MISS を避けるために、不変のクライアントライブラリリソースをバックグラウンド更新で長期（30 日）にキャッシュします。

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * HTMLページを 5 分間キャッシュし、バックグラウンド更新をおこなうと、ブラウザーでは 1 時間、CDN では 12 時間をキャッシュします。 Cache-Control ヘッダーは常に追加されるので、/content/*の下の一致する html ページが公開されるようにすることが重要です。 そうでない場合は、より具体的な正規表現を使用することを検討してください。

      ```
      <LocationMatch "^/content/.*\.html$">
         Header unset Cache-Control
         Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * ブラウザーではバックグラウンド更新 1 時間、CDN では 12 時間で、コンテンツサービス/Sling モデルエクスポーターの json 応答を 5 分間キャッシュします。

      ```
      <LocationMatch "^/content/.*\.model\.json$">
         Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * MISS を避けるために、コア画像コンポーネントからの不変 URL をバックグラウンド更新で長期（30 日）にキャッシュします。

      ```
      <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * MISS を避けるために、24 時間の画像やビデオなど、DAM の可変リソースをキャッシュし、12 時間後にバックグラウンド更新をおこないます

      ```
      <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

### HEADリクエスト動作 {#request-behavior}

AdobeCDN で、以下のHEADに関するリソースリクエストを受信したとき **not** キャッシュされた場合、リクエストは、Dispatcher インスタンスやAEMインスタンスによってGETリクエストとして変換され、受け取られます。 応答がキャッシュ可能な場合、以降のHEADリクエストは CDN から提供されます。 応答がキャッシュできない場合、後続のHEAD要求は、 `Cache-Control` TTL。

## Dispatcher キャッシュの無効化 {#disp}

一般に、Dispatcher キャッシュを無効にする必要はありません。代わりに、コンテンツが再公開される際に Dispatcher がキャッシュを更新し、CDN がキャッシュの有効期限のヘッダーを考慮することを信頼できます。

### アクティベーション／非アクティベーション中の Dispatcher キャッシュの無効化 {#cache-activation-deactivation}

以前のバージョンの AEM と同様に、ページの公開または非公開では、Dispatcher のキャッシュからコンテンツがクリアされます。キャッシュの問題の疑いがある場合は、問題のページを再公開し、ServerAlias localhost（Dispatcher キャッシュの無効化に必要）に一致する仮想ホストが使用可能であることを確認する必要があります。


パブリッシュインスタンスは、オーサーから新しいバージョンのページまたはアセットを受け取ると、フラッシュエージェントを使用して Dispatcher 上の適切なパスを無効にします。更新されたパスは、親と共に、Dispatcher キャッシュから削除されます（削除されるレベルは [statfilelevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#invalidating-files-by-folder-level) で設定できます）。

### 明示的な Dispatcher キャッシュの無効化 {#explicit-invalidation}

一般的に、Dispatcher 内のコンテンツを手動で無効にする必要はありませんが、必要に応じて無効にすることができます。

>[!NOTE]
>AEM as a Cloud Service 以前は、Dispatcher キャッシュを無効にする方法が 2 通りありました。
>
>1. パブリッシュ Dispatcher のフラッシュエージェントを指定して、レプリケーションエージェントを呼び出す
>2. `invalidate.cache` API を直接呼び出す（例：`POST /dispatcher/invalidate.cache`）

>
>Dispatcher の `invalidate.cache` API アプローチは、特定の Dispatcher ノードのみを指すので、今後サポートされなくなります。AEM as a Cloud Service は、個々のノードレベルではなくサービスレベルで動作するので、 [AEM からのキャッシュページの無効化](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=ja) ページで説明されている無効化手順は、AEM as a Cloud Service では無効になります。

レプリケーションフラッシュエージェントを使用する必要があります。これは、[レプリケーション API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html) を使用して実行できます。フラッシュエージェントエンドポイントは設定できませんが、フラッシュエージェントを実行するパブリッシュサービスと一致する Dispatcher を指すように事前設定されています。フラッシュエージェントは、通常、OSGi のエージェントまたはイベントによってトリガーされます。

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 
-->

次に図で示します。

![CDN](assets/cdnd.png "CDN")

Dispatcher キャッシュがクリアされない問題が発生した場合は、[カスタマーサポート](https://helpx.adobe.com/jp/support.ec.html)にお問い合わせください。必要に応じて Dispatcher キャッシュをフラッシュします。

アドビが管理する CDN は TTL に従うので、フラッシュする必要はありません。問題の疑いがある場合は、[カスタマーサポート](https://helpx.adobe.com/support.ec.html)にお問い合わせください。必要に応じてアドビが管理する CDN キャッシュをフラッシュします。

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
