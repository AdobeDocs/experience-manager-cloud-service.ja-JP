---
title: Cloud Service コンテンツリクエストについて
description: アドビからコンテンツリクエストライセンスを購入している場合は、Adobe Experience Cloud as a Service が測定するコンテンツリクエストのタイプと、組織の分析レポートツールとの相違について説明します。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 16941385a05358d9a5cf3f57405b8f2174902af2
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 53%

---

# Cloud Serviceコンテンツリクエストについて

## はじめに {#introduction}

コンテンツリクエストとは、AEM Sitesに対して行われるリクエストを指します。これには、コンテンツ配信ネットワークなど、Edge Delivery Servicesまたはお客様が提供するキャッシュシステムに関連するリクエストが含まれます。 これらのリクエストは、コンテンツやデータをページビュー（ページやエクスペリエンスフラグメントなど）を通じてHTML形式で、または API 呼び出しを通じて JSON 形式でヘッドレス方式で配信します。 コンテンツリクエストは、ページビューまたは 5 回の API 呼び出しとしてカウントされ、コンテンツリクエストを受信する最初のキャッシュシステムの入力時に測定されます。 コンテンツリクエストをカウントする目的で、特定の HTTP リクエストが含められたり除外されたりします。含まれる HTTP リクエストと除外される HTTP リクエストの完全なリストおよびその技術的な定義については、ドキュメントを参照してください。

## Cloud Serviceコンテンツリクエストについて {#understanding-cloud-service-content-requests}

標準の CDN を使用しているお客様の場合、Cloud Service コンテンツリクエストは、サーバーサイドのデータ収集を通じて測定されます。コレクションは、CDN ログ分析を通じて有効になります。AEM（Adobe Experience Manager）のas a Cloud Serviceは、サーバーサイドでエッジのコンテンツリクエストを自動的に収集します。 AEM as a Cloud Service CDN で生成されたログファイルを分析します。 このプロセスは、HTML `(text/html)` または JSON `(application/json)` コンテンツを返すリクエストを CDN から分離することで行われ、以下に説明するいくつかの包含および除外ルールに基づいています。 コンテンツが CDN キャッシュから提供されるか、CDN オリジンに返されるかに関係なく（AEM Dispatcher を使用して）、コンテンツリクエストが発生します。

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Cloud Serviceコンテンツリクエストの相違 {#content-requests-variances}

次の表にまとめられているように、コンテンツリクエストには、組織の Analytics レポートツール内で相違が生じる可能性があります。 一般に、サイトのコンテンツリクエスト数のレポートにクライアントサイドのインストルメンテーションに依存する分析ツールを使用しないでください。 これらのツールは、アクティブ化するユーザーの同意に依存しているため、多くの場合、トラフィックの大部分を見逃します。 AEM as a Cloud Service上に独自の CDN を追加しているお客様向けのログファイルまたは CDN レポートでサーバーサイドでデータを収集する Analytics ツールでは、カウントを改善できます。

| 差異の理由 | 説明 |
|---|---|
| エンドユーザーの同意 | クライアント側の計測機能に依存する Analytics ツールは、多くの場合、ユーザーの同意がトリガーされるかどうかに依存します。このワークフローは、トラフィックの大部分が追跡されていないことを表している可能性があります。 コンテンツリクエストを独自に測定する場合は、Analytics ツールに依存してサーバー側または CDN レポートのデータを収集することをお勧めします。 |
| タグ付け | Adobe Experience Manager コンテンツリクエストとして追跡されるすべてのページまたは API 呼び出しに対して、Analytics トラッキングでタグ付けされない場合があります。 |
| タグ管理ルール | タグ管理ルールの設定により、ページ上で様々なデータ収集設定が行われ、その結果、コンテンツリクエストのトラッキングとは何らかの不一致が生じる場合があります。 |
| ボット | AEMが事前に識別および削除していない不明なボットがあると、トラッキング不一致が発生する場合があります。 |
| レポートスイート | 同じ AEM インスタンスとドメインに属するページが、異なる Analytics レポートスイートにデータを送信する場合があります。 |
| サードパーティのモニタリングツールとセキュリティツール | モニタリングツールやセキュリティスキャンツールによっては、Analytics レポートでは追跡されない AEM のコンテンツリクエストが生成される場合があります。 |
| API アクセス | ページまたは Adobe Experience Manager API にプログラムでアクセスすると、Analytics レポートで追跡されない AEM のコンテンツリクエストが生成される場合があります。 |
| プリフェッチリクエスト | ページを事前にロードして速度を上げるプリフェッチサービスを使用すると、コンテンツリクエストのトラフィックが大幅に増加する可能性があります。 |
| DDoS | Adobeは、DDOS 攻撃からトラフィックを自動的に検出して除外しようとしますが、発生し得るすべての DDOS 攻撃が検出される保証はありません。 |
| トラフィックブロッカー | ブラウザーでトラッカーブロッカーを使用すると、一部のリクエストの追跡がオプトアウトされる可能性があります。 |
| ファイアウォール | ファイアウォールによって、Analytics のトラッキングがブロックされる可能性があります。このシナリオは、企業のファイアウォールで発生頻度が高くなります。 |

[ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md)も参照してください。

## サーバーサイドの収集ルール {#serverside-collection}

よく知られているボットを除外するルールが用意されています。これには、検索インデックスまたはサービスを更新するためにサイトに定期的にアクセスするよく知られているサービスも含まれます。

### 含まれるコンテンツリクエストのタイプ {#included-content-requests}

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP コード 100-299 | 次のものが含まれます。 | コンテンツの全部または一部を配信する通常のリクエスト。 |
| 自動化用の HTTP ライブラリ | 次のものが含まれます。 | 例：<br>・ Amazon CloudFront<br>・ Apache Http Client<br>・非同期 HTTP クライアント <br>・ Axios<br>・ Azureus<br>・ Curl<br>・ GitHub Node Fetch<br>・ Guzzle<br>・ Go-http-client<br>・ ヘッドレス Chrome<br>・ Java™ Client<br>・ Jersey<br>・ Node Oembed<br> <br>・ Python リクエスト <br>・ Reactor Netty<br>・ Wget<br>・ WinHTTP<br>・ Fast HTTP <br> <br>・ GitHub ノードの取得・ Reactor Netty |
| 監視ツールおよびヘルスチェックツール | 次のものが含まれます。 | サイトの特定の側面を監視するために顧客によって設定されます。 例えば、可用性や実際のユーザーパフォーマンスなどです。ヘルスチェックの `/system/probes/health` のような特定のエンドポイントをターゲットにしている場合、Adobeでは、サイトの実際のHTMLページではなく、`/system/probes/health` エンドポイントを使用することをお勧めします。 [ 以下を参照 ](#excluded-content-request)<br> 例：<br>・ `Amazon-Route53-Health-Check-Service`<br>・ EyeMonIT_bot_version_0.1_[ （https://eyemonit.com/） ](https://eyemonit.com/)<br>・ Investis-Site24x7<br>・ Mozilla/5.0+（compatible; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/)） <br>・ ThousandsEyes-Dragonfly-x1<br>・ OmtrBot/1.0<br>・ WebMon/2.0.0 |
| `<link rel="prefetch">` リクエスト | 次のものが含まれます。 | 次のページの読み込み速度を上げるには、ユーザーがリンクをクリックする前にブラウザーで一連のページを読み込むように設定し、既にキャッシュに存在している必要があります。*注意：このアプローチでは、トラフィックが大幅に増加します*。これは、プリフェッチされるページの数によって異なります。 |
| Adobe Analytics または Google Analytics レポートをブロックするトラフィック | 次のものが含まれます。 | サイトの訪問者が、Google Analytics や Adobe Analytic sの正確性に影響を与えるプライバシーソフトウェア（広告ブロッカーなど）をインストールしていることがよくあります。AEM as a Cloud Service は、クライアントサイドではなく、アドビが運用するインフラストラクチャへの最初のエントリポイントに対するリクエストをカウントします。 |

[ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md)も参照してください。

### 除外されたコンテンツリクエストのタイプ {#excluded-content-request}

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP Code 500+ | 除外済み | AEM as a Cloud Service または顧客カスタムコードで問題が発生した場合に、訪問者にエラーが返されました。 |
| HTTP コード 400-499 | 除外済み | コンテンツが存在しない（404）場合や、その他のコンテンツまたはリクエスト関連の問題がある場合に、訪問者にエラーが返されました。 |
| HTTP コード 300-399 | 除外済み | 適切なリクエストは、サーバーで何かが変更されたかどうかを確認するか、リクエストを別のリソースにリダイレクトします。 コンテンツ自体が含まれていないので、課金対象になりません。 |
| /libs/* に移動するリクエスト | 除外済み | AEM の内部 JSON リクエスト（課金対象でない CSRF トークンなど）。 |
| DDoS 攻撃からのトラフィック | 除外済み | DDoS 保護。AEM は一部の DDoS 攻撃を自動検出しブロックします。DDoS 攻撃は、検出された場合、課金対象ではありません。 |
| AEM as a Cloud Service NewRelic 監視 | 除外済み | AEM as a Cloud Service グローバル監視。 |
| 顧客が Cloud Service プログラムを監視するための URL | 除外済み | Adobeでは、この URL を使用して、可用性やヘルスチェックを外部でモニタリングすることをお勧めします。<br><br>`/system/probes/health` |
| AEM as a Cloud Service ポッドウォームアップサービス | 除外済み |
| エージェント：skyline-service-warmup/1。* |
| よく知られている検索エンジン、ソーシャルネットワーク、HTTP ライブラリ（Fastly によってタグ付け） | 除外済み | 検索インデックスまたはサービスを更新するためにサイトを定期的に訪問するよく知られたサービス：<br><br> 例：<br>・ AddSearchBot<br>・ AhrefsBot<br>・ Applebot<br>・ Ask Jeeves Corporate Spider<br>・ Bingbot<br>・ BingPreview<br>・ BLEXBot<br>・ BuiltWith<br>・ Bytespider<br>・ CrawlerKengo<br>・ Facebookexternalhit<br>・ Google Bot<br>・ Google Bot Mobile<br>・ Mobile<br>・ Googleogleoglebot bot<br>・ Googlebot Mobile<br>・ lmspider<br>・ LucidWorks<br>・ `MJ12bot`<br>・ Pinterest<br> <br> <br> <br> <br>・ SemrushBot の・・ StashBot の・・ StatusBotBot の・・ Claudebot |
| コマース統合フレームワーク呼び出しの除外 | 除外済み | AEMに対して行われた、Commerce integration frameworkに転送されるリクエスト（URL は `/api/graphql` で始まります）は、二重カウントを避けるために、Cloud Serviceに対して請求できません。 |
| `manifest.json` を除外 | 除外済み | マニフェストは API 呼び出しではありません。 ここでは、デスクトップまたは携帯電話に web サイトをインストールする方法に関する情報を提供します。 アドビは `/etc.clientlibs/*/manifest.json` に対する JSON リクエストをカウントするべきではありません |
| `favicon.ico` を除外 | 除外済み | 返されるコンテンツはHTMLや JSON にしないでください。ただし、SAML 認証フローなどの特定のシナリオでは、お気に入りがHTMLとして返されるようになりました。 その結果、お気に入りはカウントから明示的に除外されます。 |
| 別のバックエンドへの CDN プロキシ | 除外済み | [CDN 接触チャネルセレクター技術](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors)を使用して AEM 以外の別のバックエンドにルーティングしたリクエストは、AEM にヒットしないので除外されます。 |
