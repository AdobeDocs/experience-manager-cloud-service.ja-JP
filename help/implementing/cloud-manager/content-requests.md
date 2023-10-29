---
title: Cloud Serviceコンテンツリクエストについて
description: Adobeからコンテンツリクエストライセンスを購入している場合は、Adobe Experience Cloud as a Service が測定するコンテンツリクエストのタイプと、組織の Analytics レポートツールとの相違について説明します。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
source-git-commit: 25a4a6b9ae09cb71f50317990af1718db1e14355
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 12%

---

# Cloud Serviceコンテンツリクエスト

## Cloud Serviceコンテンツリクエストの相違{#content-requests-variances}

コンテンツリクエストは、次の表に要約されるように、組織の Analytics レポートツールとの相違を持つ可能性があります。 一般に、Analytics ツールは、クライアント側の計測機能を使用してデータを収集します <b>を使用しない</b> 特定のサイトに対するコンテンツリクエスト数をレポートする場合は、多くの場合、トリガーされるエンドユーザーの同意に依存しているので、トラフィックの大部分が欠落しています。 AEMas a Cloud Serviceの上に独自の CDN を追加するお客様向けに、ログファイルのサーバーサイドでデータを収集する Analytics ツール、または CDN レポートを使用すると、カウントが向上します。 ページビューおよび関連するパフォーマンスのレポートでは、AdobeRUM データサービスが推奨Adobeです。

| 差異の理由 | 説明 |
|---|---|
| エンドユーザーの同意 | クライアント側の実装に依存する Analytics ツールは、多くの場合、エンドユーザーの同意がトリガーされるかどうかに依存しています。 これは、トラッキングされないトラフィックの大部分を表している可能性があります。 コンテンツリクエストを独自に測定する場合は、Analytics ツールに依存してサーバー側または CDN レポートのデータを収集することをお勧めします。 |
| タグ付け | Adobe Experience Manager(AEM) コンテンツリクエストとして追跡されるすべてのページまたは API 呼び出しに対して、Analytics トラッキングでタグ付けされない場合があります。 |
| タグ管理ルール | Tag Management のルール設定によって、ページ上の様々なデータ収集設定がおこなわれ、その結果、コンテンツリクエストの追跡との組み合わせに相違が生じる場合があります。 |
| ボット | AEM によって事前に識別および削除されていない不明なボットは、トラッキング不一致の原因となる場合があります。 |
| レポートスイート | 同じ AEM インスタンスとドメインに属するページが、異なる Analytics レポートスイートにデータを送信する場合があります。 |
| サードパーティのモニタリングツールとセキュリティツール | モニタリングツールやセキュリティスキャンツールによっては、Analytics レポートでは追跡されない AEM のコンテンツリクエストが生成される場合があります。 |
| API アクセス | ページまたはAdobe Experience Manager API にプログラムでアクセスすると、Analytics レポートで追跡されないAEMのコンテンツリクエストが生成される場合があります。 |
| プリフェッチリクエスト | ページを事前にロードして速度を上げるプリフェッチサービスを使用すると、コンテンツリクエストのトラフィックが大幅に増加する可能性があります。 |
| DDoS | アドビでは、DDoS 攻撃からのトラフィックを自動的に検出して除外するためのあらゆる取り組みを講じていますが、発生し得るすべての DDoS 攻撃が検出される保証はありません。 |
| トラフィックブロッカー | ブラウザーでトラッカーブロッカーを使用すると、一部のリクエストの追跡がオプトアウトされる可能性があります。 |
| ファイアウォール | ファイアウォールによって、Analytics のトラッキングがブロックされる可能性があります。このシナリオは、企業ファイアウォールでより頻繁に使用されます。 |

関連トピック [ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md).

## Cloud Serviceコンテンツリクエストについて {#about-content-request}

コンテンツリクエストは、AEMのas a Cloud Serviceの CDN から取得したログファイルを自動分析することで、Adobe Experience Manager(AEM) の端で自動的に追跡されます。このとき、CDN からHTMLを返す (text/html) または JSON(application/json) コンテンツを分離し、以下で説明する包含ルールと除外ルールに基づきます。 コンテンツリクエストは、CDN キャッシュから提供される返されたコンテンツとは独立しておこなわれるか、CDN(AEM Dispatchers) の元に戻されます。

独自の CDN をAEMas a Cloud Serviceの上に持ち込むお客様の場合、この追跡によって、ライセンスが必要なコンテンツリクエストとの比較に使用できない数値が生じます。この数値は、外部の CDN の端で顧客が測定する必要があります。

よく知られているボットを除外するルールが用意されています。これには、サイトを定期的に訪問して検索インデックスやサービスを更新する、既知のサービスが含まれます。

### 含まれるコンテンツリクエストのタイプ{#included-content-requests}

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP コード 100-299 | 含む | これらは、すべてのコンテンツまたは部分的なコンテンツを配信する通常のリクエストです。 |
| 自動化用の HTTP ライブラリ | 含む | 例：<br>・ Amazon CloudFront<br>・ Apache Http Client<br>・非同期 Http クライアント<br>・ Axios<br>・アズレウス<br>・ Curl<br>・ GitHub ノードフェッチ<br>・ Guzzle<br>・ Go-http-client<br>・ヘッドレスクロム<br>・ Java™ Client<br>・ジャージー<br>・ Node Oembed<br>・ okhttp<br>・ Python リクエスト<br>・ Reactor Netty<br>・ Wget<br>・ WinHTTP |
| 監視およびヘルスチェックツール | 含む | これらは、サイトの特定の側面を監視するために顧客が設定します。 例えば、可用性や実際のユーザーパフォーマンスなどです。 用途 `/system/probes/health` サイトからの実際のHTMLページではなく、エンドポイント。<br>例：<br>・ Amazon-Route53-Health-Check-Service<br>・ EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>・ Runvison-Site24 x 7<br>・ Mozilla/5.0 以降 ( 互換； UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>・ SoundEyes-Dragonfly-x1<br>・ OmtrBot/1.0<br>・ WebMon/2.0.0 |
| `<link rel="prefetch">` リクエスト | 含む | 次のページの読み込み速度を上げるには、ユーザーがリンクをクリックする前にブラウザーで一連のページを読み込むように設定し、既にキャッシュに存在している必要があります。 *注意：これにより、トラフィックが大幅に増加しています* — 取得されるこれらのページの数に応じて異なります。 |
| Adobe AnalyticsまたはGoogle Analyticsレポートをブロックするトラフィック | 含む | サイトの訪問者には、Google AnalyticsやAdobe Analyticsの正確性に影響を与えるプライバシーソフトウェア（広告ブロッカーなど）がインストールされていることは、より一般的です。 AEMas a Cloud Serviceは、クライアント側ではなく、Adobeが運用するインフラストラクチャへの最初のエントリポイントに対するリクエストをカウントします。 |

関連トピック [ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md).

### 除外されたコンテンツリクエストのタイプ{#excluded-content-request}

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP コード 500 以降 | 除外済み | AEMas a Cloud Serviceまたは顧客カスタムコードで問題が発生した場合に、訪問者にエラーが返されました。 |
| HTTP コード 400-499 | 除外済み | コンテンツが存在しない (404) 場合や、その他のコンテンツまたはリクエスト関連の問題がある場合に、訪問者に返されたエラー。 |
| HTTP コード 300-399 | 除外済み | これらは、サーバー上で何かが変更されたかを確認する、または別のリソースにリクエストをリダイレクトする、適切なリクエストです。 コンテンツ自体が含まれていないので、課金対象になりません。 |
| /libs/*に移動するリクエスト | 除外済み | AEMの内部 JSON リクエスト（課金対象でない CSRF トークンなど）。 |
| DDOS 攻撃からのトラフィック | 除外済み | DDOS 保護。 AEMは一部の DDOS 攻撃を自動検出し、ブロックします。 検出された場合は、DDOS 攻撃は課金対象ではありません。<br><br>自動検出された DDOS の種類：<br>・ DDOSBlockedCiphersSHA<br>・ DDOSBlockedPattern<br>・ DDOSSuspticeRequest |
| AEMas a Cloud ServiceNewRelic 監視 | 除外済み | AEMas a Cloud Service的グローバル監視。 |
| 顧客がCloud Serviceプログラムを監視するための URL | 除外済み | 可用性を外部で監視するための推奨 URL。<br><br>`/system/probes/health` |
| AEMas a Cloud Serviceポッドウォームアップサービス | 除外済み | ユーザーエージェント： skyline-service-warmup/1。* |
| よく知られている検索エンジン、ソーシャルネットワーク、HTTP ライブラリ（Fastly によってタグ付け） | 除外済み | サイトを定期的に訪問し、検索インデックスやサービスを更新するよく知られたサービス：<br><br>例：<br>・ AddSearchBot<br>・ AhrefsBot<br>・ Applebot<br>・ Ask Jeeves Corporate Spider<br>・ Bingbot<br>・ BingPreview<br>・ BLEXBot<br>・ BuiltWith<br>・ Bytespider<br>・ CrawlerKengo<br>・ Facebookexternalhit<br>・ Google AdsBot<br>・ Google AdsBot Mobile<br>・ Googlebot<br>・ Googlebot Mobile<br>・ lmspider<br>・ LucidWorks<br>・ MJ12bot<br>・ Pingdom<br>・ Pinterest<br>・ SemrushBot<br>・ SiteImprove<br>・ StashBot<br>・ StatusCakes<br>・ YandexBot |
| 除外Commerce integration framework呼び出し | 除外済み | これらは、Commerce integration frameworkに転送されるAEMに対しておこなわれる要求です。URL はで始まります。 `/api/graphql` — 二重計数を避けるために、Cloud Serviceの請求はできません。 |
| 除外 `manifest.json` | 除外済み | マニフェストは API 呼び出しではありません。デスクトップまたは携帯電話に Web サイトをインストールする方法に関する情報を提供するために、ここに記載されています。 Adobeは次に対する JSON リクエストをカウントしない `/etc.clientlibs/*/manifest.json` |
| 除外 `favicon.ico` | 除外済み | 返されるコンテンツはHTMLや JSON ではありませんが、SAMLHTMLフローなどのシナリオでは、favicon が認証として返される場合があるので、カウントから明示的に除外されることがわかります。 |
