---
title: Cloud Service コンテンツリクエストについて
description: アドビからコンテンツリクエストライセンスを購入している場合は、Adobe Experience Cloud as a Service が測定するコンテンツリクエストのタイプと、組織の分析レポートツールとの相違について説明します。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 96bf1d56d24da851ad4713e3cb0728fd7a18da18
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 94%

---

# Cloud Service コンテンツリクエスト

## はじめに {#introduction}

コンテンツリクエストとは、AEM Sites（AEM Sites の Edge Delivery Services との接続を含む）または顧客提供のキャッシュシステム（コンテンツ配信ネットワークなど）に送信されるリクエストで、ページビュー（ページやエクスペリエンスフラグメントなど）を通じた HTML 形式や、API 呼び出し（ヘッドレス方式）を通じた JSON 形式でコンテンツまたはデータを配信します。コンテンツリクエストは、ページビューまたは 5 回の API 呼び出しとしてカウントされ、コンテンツリクエストを受信する最初のキャッシュシステムの入力時に測定されます。コンテンツリクエストをカウントする目的で、特定の HTTP リクエストが含められたり除外されたりします。含まれる HTTP リクエストと除外される HTTP リクエストの完全なリストおよびその技術的な定義については、ドキュメントを参照してください。

## Cloud Service コンテンツリクエストについて {#understanding-cloud-service-content-requests}

標準の CDN を使用しているお客様の場合、Cloud Service コンテンツリクエストは、サーバーサイドのデータ収集を通じて測定されます。コレクションは、CDN ログ分析を通じて有効になります。コンテンツリクエストは、AEM as a Cloud Service CDN からのログファイルを自動分析することで、Adobe Experience Manager as a Cloud Service のエッジにあるサーバーサイドで自動的に収集されます。この処理は、HTML `(text/html)` または JSON `(application/json)` コンテンツを返すリクエストを CDN から分離し、以下で説明するいくつかの包含ルールと除外ルールに基づいて行われます。コンテンツリクエストは、返されたコンテンツ（CDN キャッシュから提供）または CDN（AEM の Dispatcher）のオリジンに戻されるコンテンツとは独立して行われます。

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Cloud Service コンテンツリクエストの相違 {#content-requests-variances}

コンテンツリクエストには、次の表にまとめられているように、組織の分析レポートツールとは違いがあります。一般に、クライアントサイドの計測機能を使用してデータを収集し、特定のサイトに対するコンテンツリクエストの数をレポートする分析ツールは使用&#x200B;*しないでください*。なぜなら、多くの場合、分析ツールはユーザーの同意に応じてトリガーされるため、トラフィックの大部分が欠落しているからです。AEM as a Cloud Service の上に独自の CDN を追加するお客様向けに、ログファイルのサーバーサイドでデータを収集する Analytics ツール、または CDN レポートを使用すると、精度が向上します。ページビューおよび関連するパフォーマンスのレポートでは、[Adobe RUM データサービス](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md)がアドビ推奨のオプションです。

| 差異の理由 | 説明 |
|---|---|
| エンドユーザーの同意 | クライアント側の計測機能に依存する Analytics ツールは、多くの場合、ユーザーの同意がトリガーされるかどうかに依存します。これは、トラフィックの大部分がトラッキングされていないことを表している可能性があります。コンテンツリクエストを独自に測定する場合は、Analytics ツールに依存してサーバー側または CDN レポートのデータを収集することをお勧めします。 |
| タグ付け | Adobe Experience Manager コンテンツリクエストとして追跡されるすべてのページまたは API 呼び出しに対して、Analytics トラッキングでタグ付けされない場合があります。 |
| タグ管理ルール | タグ管理ルールの設定により、ページ上で様々なデータ収集設定が行われ、その結果、コンテンツリクエストのトラッキングとは何らかの不一致が生じる場合があります。 |
| ボット | AEM によって事前に識別および削除されていない不明なボットは、トラッキング不一致の原因となる場合があります。 |
| レポートスイート | 同じ AEM インスタンスとドメインに属するページが、異なる Analytics レポートスイートにデータを送信する場合があります。 |
| サードパーティのモニタリングツールとセキュリティツール | モニタリングツールやセキュリティスキャンツールによっては、Analytics レポートでは追跡されない AEM のコンテンツリクエストが生成される場合があります。 |
| API アクセス | ページまたは Adobe Experience Manager API にプログラムでアクセスすると、Analytics レポートで追跡されない AEM のコンテンツリクエストが生成される場合があります。 |
| プリフェッチリクエスト | ページを事前にロードして速度を上げるプリフェッチサービスを使用すると、コンテンツリクエストのトラフィックが大幅に増加する可能性があります。 |
| DDoS | アドビでは、DDoS 攻撃からのトラフィックを自動的に検出して除外しようとしていますが、発生し得るすべての DDoS 攻撃が検出される保証はありません。 |
| トラフィックブロッカー | ブラウザーでトラッカーブロッカーを使用すると、一部のリクエストの追跡がオプトアウトされる可能性があります。 |
| ファイアウォール | ファイアウォールによって、Analytics のトラッキングがブロックされる可能性があります。このシナリオは、企業のファイアウォールで発生頻度が高くなります。 |

[ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md)も参照してください。

## サーバーサイドのコレクションルール {#serverside-collection}

よく知られているボットを除外するルールが用意されています。これには、検索インデックスまたはサービスを更新するためにサイトに定期的にアクセスするよく知られているサービスも含まれます。

### 含まれるコンテンツリクエストのタイプ {#included-content-requests}

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP コード 100-299 | 次のものが含まれます。 | これらは、すべてのコンテンツまたはコンテンツの一部を配信する通常のリクエストです。 |
| 自動化用の HTTP ライブラリ | 次のものが含まれます。 | 例：<br>・Amazon CloudFront<br>・Apache Http Client<br>・非同期 Http クライアント<br>・Axios<br>・アズレウス<br>・Curl<br>・GitHub ノードフェッチ<br>・Guzzle<br>・Go-http-client<br>・ヘッドレスクロム<br>・ Java™ Client<br>・ジャージー<br>・Node Oembed<br>・okhttp<br>・Python リクエスト<br>・Reactor Netty<br>・Wget<br>・WinHTTP |
| 監視ツールおよびヘルスチェックツール | 次のものが含まれます。 | これらは、サイトの特定の側面を監視するために顧客が設定します。例えば、可用性や実際のユーザーパフォーマンスなどです。これらが/system/probes/health for health checks などの特定のエンドポイントをターゲットにしている場合は、サイトの実際のHTMLページではなく、`/system/probes/health` エンドポイントを使用することをお勧めします。[ 以下を参照 ](#excluded-content-request)<br> 例：<br>・ Amazon-Route53-Health-Check-Service<br>・ EyeMonIT_bot_version_0.1_[ （https://www.eyemon.it/） ](https://www.eyemon.it/)<br>・ Investis-Site24x7<br>・ Mozilla/5.0+（compatible; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/)） <br>・ ThousandsEyes-Dragonfly-x1<br>・ OmtrBot/2.0.0<br> |
| `<link rel="prefetch">` リクエスト | 次のものが含まれます。 | 次のページの読み込み速度を上げるには、ユーザーがリンクをクリックする前にブラウザーで一連のページを読み込むように設定し、既にキャッシュに存在している必要があります。*注意：これにより、取得されるこれらのページの数に応じて、トラフィックが大幅に増加します*。 |
| Adobe Analytics または Google Analytics レポートをブロックするトラフィック | 次のものが含まれます。 | サイトの訪問者が、Google Analytics や Adobe Analytic sの正確性に影響を与えるプライバシーソフトウェア（広告ブロッカーなど）をインストールしていることがよくあります。AEM as a Cloud Service は、クライアントサイドではなく、アドビが運用するインフラストラクチャへの最初のエントリポイントに対するリクエストをカウントします。 |

[ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md)も参照してください。

### 除外されたコンテンツリクエストのタイプ {#excluded-content-request}

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP Code 500+ | 除外済み | AEM as a Cloud Service または顧客カスタムコードで問題が発生した場合に、訪問者にエラーが返されました。 |
| HTTP コード 400-499 | 除外済み | コンテンツが存在しない（404）場合や、その他のコンテンツまたはリクエスト関連の問題がある場合に、訪問者にエラーが返されました。 |
| HTTP コード 300-399 | 除外済み | これらは、サーバー上で何かが変更されたかを確認する、または別のリソースにリクエストをリダイレクトする適切なリクエストです。コンテンツ自体が含まれていないので、課金対象になりません。 |
| /libs/* に移動するリクエスト | 除外済み | AEM の内部 JSON リクエスト（課金対象でない CSRF トークンなど）。 |
| DDoS 攻撃からのトラフィック | 除外済み | DDoS 保護。AEM は一部の DDoS 攻撃を自動検出しブロックします。DDoS 攻撃は、検出された場合、課金対象ではありません。 |
| AEM as a Cloud Service NewRelic 監視 | 除外済み | AEM as a Cloud Service グローバル監視。 |
| 顧客が Cloud Service プログラムを監視するための URL | 除外済み | 可用性またはヘルスチェックを外部で監視するには、URL を使用することをお勧めします。<br><br>`/system/probes/health` |
| AEM as a Cloud Service ポッドウォームアップサービス | 除外済み |
| エージェント：skyline-service-warmup/1。* |
| よく知られている検索エンジン、ソーシャルネットワーク、HTTP ライブラリ（Fastly によってタグ付け） | 除外済み | サイトを定期的に訪問し、検索インデックスやサービスを更新するよく知られたサービス：<br><br>例：<br>・ AddSearchBot<br>・ AhrefsBot<br>・ Applebot<br>・ Ask Jeeves Corporate Spider<br>・ Bingbot<br>・ BingPreview<br>・ BLEXBot<br>・ BuiltWith<br>・ Bytespider<br>・ CrawlerKengo<br>・ Facebookexternalhit<br>・ Google AdsBot<br>・ Google AdsBot Mobile<br>・ Googlebot<br>・ Googlebot Mobile<br>・ lmspider<br>・ LucidWorks<br>・ MJ12bot<br>・ Pingdom<br>・ Pinterest<br>・ SemrushBot<br>・ SiteImprove<br>・ StashBot<br>・ StatusCakes<br>・ YandexBot |
| コマース統合フレームワーク呼び出しの除外 | 除外済み | これらは、二重カウントを避けるために、AEM に対して行われたリクエストで、Commerce Integration Framework に転送されます（URL は `/api/graphql` で始まります）。これらは Cloud Service の請求対象ではありません。 |
| `manifest.json` を除外 | 除外済み | マニフェストは API 呼び出しではなく、デスクトップまたは携帯電話に web サイトをインストールする方法に関する情報を提供するためにここに記載されています。アドビは `/etc.clientlibs/*/manifest.json` に対する JSON リクエストをカウントするべきではありません |
| `favicon.ico` を除外 | 除外済み | 返されるコンテンツは HTML や JSON ではありませんが、SAML 認証フローなどのシナリオでは、favicon が HTML として返される場合があるので、カウントから明示的に除外されることがわかります。 |
