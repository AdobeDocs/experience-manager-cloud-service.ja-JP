---
title: Cloud Service コンテンツリクエストについて
description: アドビからコンテンツリクエストライセンスを購入している方のために、Adobe Experience Cloud as a Service が測定するコンテンツリクエストのタイプと、組織の分析レポートツールとの相違について説明します。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: bd207a7c3e9e5e52202456fa95dd31293639725f
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 46%

---

# Cloud Service コンテンツリクエストについて

## はじめに {#introduction}

コンテンツリクエストには、AEM Sitesに送信されたリクエストが含まれます。 これらのリクエストは、Edge Delivery Servicesまたはコンテンツ配信ネットワーク（CDN）などのお客様が提供するキャッシュシステムを経由してルーティングされる場合があります。 これらのリクエストは、HTML形式または JSON 形式の構造化データを提供し、ヘッドレスな方法で API を介してページビュー（ページ、エクスペリエンスフラグメントなど）または JSON 返しをサポートします。

HTMLまたは JSON を使用してページが表示されると、システムはコンテンツリクエストをカウントします。 最初のキャッシュシステムが受信した時点でリクエストを測定します。 コンテンツリクエストをカウントする目的で、特定の HTTP リクエストが含められたり除外されたりします。HTTP[ 含まれるコンテンツリクエスト ](#included-content-requests) および [ 除外されたコンテンツリクエスト ](#excluded-content-request) の完全なリストをご覧ください。

## Cloud Service コンテンツリクエストについて {#understanding-cloud-service-content-requests}

*ページリクエスト* とは、メインページエクスペリエンスのレンダリングに必要なコア構造化コンテンツ（HTMLや JSON など）を取得する HTTP リクエストを指します。 画像やスクリプトなどのアセットのリクエストは含まれません。

標準の CDN を使用している場合、AEM as a Cloud Serviceは、サーバーサイドレベルで測定されたコンテンツリクエストをカウントします。 この測定は自動的に行われ、クライアントサイドの分析トラッキングには依存しません。

AEM（Adobe Experience Manager）as a Cloud Serviceは、AEM インスタンスによって生成され、CDN で受信される応答タイプに基づいてコンテンツリクエストを識別します。 特に、HTML（`text/html`）または JSON （`application/json`）を返すリクエストがカウントされます。 これらの形式は、通常、従来のサイトレンダリングまたはヘッドレス配信用のプライマリページコンテンツを配信します。

JavaScript ファイル、CSS スタイルシート、画像などの静的アセットのリクエストは、コンテンツリクエストとしてカウントされません。

>[!NOTE]
>API リクエストが、（例えば、ヘッドレス配信などで）ページレベルのコンテンツとして機能するHTMLまたは JSON を返す場合でも、コンテキストによっては、コンテンツリクエストとしてカウントされる場合があります。

コンテンツリクエストは、レスポンスが CDN キャッシュから提供されたか、オリジン AEM環境に転送されたかに関係なく測定されます。

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Cloud Service コンテンツリクエストの相違 {#content-requests-variances}

次の表にまとめられているように、コンテンツリクエストには、組織の分析レポートツール内で相違が生じる可能性があります。 一般に、サイトのコンテンツリクエスト数のレポートにクライアントサイドのインストルメンテーションに依存する分析ツールを使用しないでください。これらのツールは、アクティブ化するユーザーの同意に依存しているため、多くの場合、トラフィックの大部分が見逃されることがあります。AEM as a Cloud Service の上に独自の CDN を追加するお客様向けに、ログファイルのサーバーサイドでデータを収集する Analytics ツール、または CDN レポートを使用すると、精度が向上します。

| 差異の理由 | 説明 |
|---|---|
| エンドユーザーの同意 | クライアント側の計測機能に依存する Analytics ツールは、多くの場合、ユーザーの同意がトリガーされるかどうかに依存します。このワークフローは、トラフィックの大部分がトラッキングされていないことを表している可能性があります。コンテンツリクエストを自分で測定する場合、Adobeでは、サーバーサイドまたは CDN レポートからデータを収集する際に Analytics ツールを使用することをお勧めします。 |
| タグ付け | Adobe Experience Manager コンテンツリクエストとして追跡されるすべてのページまたは API 呼び出しに対して、Analytics トラッキングでタグ付けされない場合があります。 |
| タグ管理ルール | タグ管理ルールの設定により、ページ上で様々なデータ収集設定が行われ、その結果、コンテンツリクエストのトラッキングとは何らかの不一致が生じる場合があります。 |
| ボット | AEM が事前に識別および削除していない不明なボットは、トラッキング不一致の原因となる場合があります。 |
| レポートスイート | 同じAEM インスタンス内のページは、異なる Analytics レポートスイートにレポートできます。 このプロセスでは、設定に応じて、データを複数のスイートに分割できます。 |
| サードパーティのモニタリングツールとセキュリティツール | 監視およびセキュリティスキャンツール（稼動時間チェッカーや脆弱性スキャナーなど）は、ページをリクエストし、Analytics レポートに表示されないサーバーサイドのコンテンツリクエストを生成する場合があります。 |
| API アクセス | API を使用して（例えば、Adobe Experience Manager as a Headless CMSを介して）AEM ページまたはコンテンツに対するリクエストは、引き続きコンテンツリクエストとしてカウントされますが、トリガー分析のトラッキングはカウントされません。 |
| プリフェッチリクエスト | プリフェッチ（サービスワーカーやエッジ機能の使用など）は、ページを事前にリクエストすることで、トラフィック量を増やすことができます。 これらのリクエストは、サーバーサイドでカウントされますが、クライアントサイドの分析コードは実行されません。 |
| DDoS | Adobeでは、フィルタリングを使用して、多くの DDoS 攻撃を検出およびブロックします。 ただし、一部の攻撃リクエストは、フィルターが適用される前に、コンテンツリクエストとしてカウントされる場合があります。 |
| トラフィックブロッカー | ブラウザー内のプライバシー機能や企業のファイアウォールにより、分析スクリプトの読み込みがブロックされている場合があります。 これらのユーザーは、引き続きサーバーサイドのコンテンツリクエストを生成します。 |
| ファイアウォール | 企業または地域のファイアウォールの設定により、Analytics の呼び出しがAdobe サーバーに到達しなくなる可能性があり、サーバーサイドのカウントは影響を受けませんが、Analytics でレポートが不十分になる可能性があります。 |

ライセンス制限に対するコンテンツリクエストの使用状況の表示と追跡について詳しくは、[ ライセンスダッシュボード ](/help/implementing/cloud-manager/license-dashboard.md) を参照してください。

## サーバーサイドのコレクションルール {#serverside-collection}

AEM as a Cloud Serviceは、コンテンツリクエストをカウントするサーバーサイドルールを適用します。 これらのルールには、よく知られているボット（検索エンジンクローラーなど）や、サイトに対して定期的に ping を実行するサービスの監視などの非ユーザートラフィックを除外するロジックが含まれています。

次の表に、含まれるコンテンツリクエストと除外されるコンテンツリクエストのタイプと、それぞれの簡単な説明を示します。

### 含まれるコンテンツリクエストのタイプ {#included-content-requests}

>[!NOTE]
>API リクエストがHTML応答を返す場合、使用コンテキストに応じて、コンテンツリクエストとして分類される場合があります。 UI 以外のデータを返す API リクエストは、通常、除外されます。

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP コード 100-299 | 次のものが含まれます。 | HTMLまたは JSON コンテンツの全体または一部を返す成功したリクエストが含まれます。<br>HTTP コード 206：これらのリクエストは、完全なコンテンツの一部のみを配信します。 例えば、ビデオや大きな画像などです。 ページコンテンツのレンダリングに使用されるHTMLまたは JSON 応答の一部を配信する場合、部分的なコンテンツリクエストが含まれます。 |
| 自動化用の HTTP ライブラリ | 次のものが含まれます。 | ページコンテンツを取得するツールまたはライブラリが行うリクエスト。 例えば、次のようなものがあります。<br>・ Amazon CloudFront<br>・ Apache Http Client<br>・非同期 HTTP Client<br>・ Axios<br>・ Azureus<br>・ Curl<br>・ GitHub Node Fetch<br>・ Guzzle<br>・ Go-http-client<br>・ ヘッドレス Chrome<br>・ Java™ Client<br>・ Jersey<br>・ Node Oembed<br>・ okhttp<br>・ Python リクエスト <br>・ Reactor Netty<br>・ Wget<br>・ WinHTTP <br>・ Fast HTTP<br> <br>・ GitHub ノード取得・ Reactor Netty |
| 監視ツールおよびヘルスチェックツール | 次のものが含まれます。 | ページの正常性または可用性を監視するために使用されるリクエスト。<br> 除外されたコンテンツリクエストのタイプ [ を参照してください ](#excluded-content-request)。<br> 例を次に示します。<br>・ `Amazon-Route53-Health-Check-Service`<br>・ EyeMonIT_bot_version_0.1_[ （https://eyemonit.com/） ](https://eyemonit.com/)<br>・ Investis-Site24x7<br>・ Mozilla/5.0+（compatible; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/)） <br>・ ThousandsEyes-Dragonfly-x1<br>・ OmtrBot/1.0<br>・ WebMon/2.0.0 |
| `<link rel="prefetch">` リクエスト | 次のものが含まれます。 | ユーザーが（`<link rel="prefetch">` などを使用して）コンテンツをプリロードまたはプリフェッチすると、システムはそれらのサーバーサイドリクエストをカウントします。 このアプローチを使用すると、プリフェッチされるページの数に応じて、トラフィックが増加する可能性があることに注意してください。 |
| Adobe Analytics または Google Analytics レポートをブロックするトラフィック | 次のものが含まれます。 | サイトの訪問者が、Google Analytics や Adobe Analytic sの正確性に影響を与えるプライバシーソフトウェア（広告ブロッカーなど）をインストールしていることがよくあります。AEM as a Cloud Service は、クライアントサイドではなく、アドビが運用するインフラストラクチャへの最初のエントリポイントに対するリクエストをカウントします。 |

[ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md)も参照してください。

### 除外されたコンテンツリクエストのタイプ {#excluded-content-request}

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP Code 500+ | 除外済み | AEM as a Cloud Service または顧客カスタムコードで問題が発生した場合に、訪問者にエラーが返されました。 |
| HTTP コード 400-499 | 除外済み | コンテンツが存在しない（404）場合や、その他のコンテンツまたはリクエスト関連の問題がある場合に、訪問者にエラーが返されました。 |
| HTTP コード 300-399 | 除外済み | サーバー上で何かが変更されたかを確認する、または別のリソースにリクエストをリダイレクトする適切なリクエストです。コンテンツ自体が含まれていないので、課金対象になりません。 |
| `/libs/`*へのリクエスト | 除外済み | AEM の内部 JSON リクエスト（課金対象でない CSRF トークンなど）。 |
| DDoS 攻撃からのトラフィック | 除外済み | DDoS 保護。AEM は一部の DDoS 攻撃を自動検出しブロックします。DDoS 攻撃は、検出された場合、課金対象ではありません。 |
| AEM as a Cloud Service NewRelic 監視 | 除外済み | AEM as a Cloud Service グローバル監視。 |
| 顧客が Cloud Service プログラムを監視するための URL | 除外済み | アドビでは、この URL を使用して、可用性やヘルスチェックを外部から監視することをお勧めします。<br><br>`/system/probes/health` |
| AEM as a Cloud Service ポッドウォームアップサービス | 除外済み |
| エージェント：skyline-service-warmup/1。* |
| よく知られている検索エンジン、ソーシャルネットワーク、HTTP ライブラリ（Fastly によってタグ付け） | 除外済み | サイトを定期的に訪問し、検索インデックスやサービスを更新するよく知られたサービス：<br><br>例：<br>・AddSearchBot<br>・AhrefsBot<br>・Applebot<br>・Ask Jeeves Corporate Spider<br>・Bingbot<br>・BingPreview<br>・BLEXBot<br>・BuiltWith<br>・Bytespider<br>・CrawlerKengo<br>・Facebookexternalhit<br>・Google AdsBot<br>・Google AdsBot Mobile<br>・Googlebot<br>・Googlebot Mobile<br>・lmspider<br>・LucidWorks<br>•`MJ12bot`<br>・Pinterest<br>・SemrushBot<br>・SiteImprove<br>・StashBot<br>・StatusCake<br>・YandexBot<br>・ContentKing<br>・Claudebot |
| コマース統合フレームワーク呼び出しの除外 | 除外済み | 二重カウントを避けるために、AEM に対して行われたリクエストで、Commerce Integration Framework に転送されます（URL は `/api/graphql` で始まります）。これらは Cloud Service の請求対象ではありません。 |
| `manifest.json` を除外 | 除外済み | マニフェストは API 呼び出しではありません。ここでは、デスクトップまたは携帯電話に web サイトをインストールする方法に関する情報を提供します。アドビは `/etc.clientlibs/*/manifest.json` に対する JSON リクエストをカウントするべきではありません |
| `favicon.ico` を除外 | 除外済み | 返されるコンテンツを HTML や JSON にしないでください。ただし、SAML 認証フローなどの特定のシナリオでは、favicon が HTML として返されることが確認されています。その結果、favicon はカウントから明示的に除外されます。 |
