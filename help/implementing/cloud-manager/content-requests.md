---
title: Cloud Serviceコンテンツリクエストについて
description: Adobeからコンテンツリクエストライセンスを購入している場合は、Adobe Experience Cloud as a Service が測定するコンテンツリクエストのタイプと、組織の Analytics レポートツールとの相違について説明します。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
source-git-commit: e31b05f0cef6c5ca3a1c00b757eac013aa43bb90
workflow-type: tm+mt
source-wordcount: '2690'
ht-degree: 4%

---

# Cloud Serviceコンテンツリクエスト

## はじめに {#introduction}

Cloud Serviceコンテンツリクエストは、データのサーバー側収集を通じて測定されます。 コレクションは、CDN ログ分析を通じて有効になります。

>[!NOTE]
>また、 [アーリーアダプターのお客様](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter)クライアント側のコレクションは、RUM(Real User Monitoring) 測定を通じても有効になります。 詳しくは、 [この記事](#real-user-monitoring-for-aem-as-a-cloud-service).

## Cloud Serviceコンテンツリクエストについて {#understaing-cloud-service-content-requests}

コンテンツリクエストは、AEMas a Cloud Serviceの CDN から取得したログファイルを自動分析することで、Adobe Experience Manager as a Cloud Serviceの端でサーバーサイドで自動的に収集されます。 これは、リクエストの返却先HTMLを分離することでおこなわれます `(text/html)` または JSON `(application /Json)` CDN のコンテンツ、および以下に説明するいくつかのインクルージョンルールと除外ルールに基づいて作成されます。 コンテンツリクエストは、CDN キャッシュから提供される返されるコンテンツや、CDN(AEM Dispatcher) の元に戻されるコンテンツとは独立しておこなわれます。

クライアント側のコレクションである Real User Monitoring(RUM)Data Service は、ユーザーの操作をより正確に反映し、Web サイトのエンゲージメントを確実に測定できます。 これにより、顧客はページトラフィックとパフォーマンスに関する高度なインサイトを得ることができます。 これは、Adobeが管理する CDN または非Adobeが管理する CDN のどちらかを使用する両方のお客様にとって有益です。 さらに、Adobeが管理していない CDN を使用しているお客様に対して自動トラフィックレポートを有効にできるようになったので、Adobeとトラフィックレポートを共有する必要がなくなりました。

独自の CDN をAEMas a Cloud Serviceの上に持ち込むお客様の場合、サーバー側のレポートでは、ライセンスが必要なコンテンツリクエストとの比較に使用できない数字が生じます。 これらの数値は、外部 CDN の端で顧客が測定する必要があります。 これらのお客様、クライアント側のレポートおよび関連するパフォーマンスについては、 [AdobeRUM データサービス](#real-user-monitoring-for-aem-as-a-cloud-service) は、推奨されるAdobeです。 詳しくは、 [リリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter) を参照してください。

## サーバー側コレクション {#serverside-collection}

よく知られているボットを除外するルールが用意されています。これには、サイトを定期的に訪問して検索インデックスやサービスを更新する、既知のサービスが含まれます。

### Cloud Serviceコンテンツリクエストの相違 {#content-requests-variances}

コンテンツリクエストは、次の表に要約されるように、組織の Analytics レポートツールとの相違を持つ可能性があります。 一般に *しない* クライアント側の計測を通じてデータを収集する analytics ツールを使用して、特定のサイトのコンテンツリクエスト数を報告します。これは、多くの場合、トリガーされるユーザーの同意に依存しているので、トラフィックの大部分が欠落しているからです。 AEMas a Cloud Serviceの上に独自の CDN を追加するお客様向けに、ログファイルのサーバーサイドでデータを収集する Analytics ツール、または CDN レポートを使用すると、カウントが向上します。 ページ・ビューおよび関連するパフォーマンスのレポートでは、AdobeRUM データ・サービスがAdobe推奨オプションです。

| 差異の理由 | 説明 |
|---|---|
| エンドユーザーの同意 | クライアント側の実装に依存する Analytics ツールは、多くの場合、ユーザーの同意がトリガーされるかどうかに依存します。 これは、トラッキングされないトラフィックの大部分を表している可能性があります。 コンテンツリクエストを独自に測定する場合は、Analytics ツールに依存してサーバー側または CDN レポートのデータを収集することをお勧めします。 |
| タグ付け | Adobe Experience Manager(AEM) コンテンツリクエストとして追跡されるすべてのページまたは API 呼び出しに対して、Analytics トラッキングでタグ付けされない場合があります。 |
| タグ管理ルール | Tag Management のルール設定によって、ページ上の様々なデータ収集設定がおこなわれ、その結果、コンテンツリクエストの追跡との組み合わせに相違が生じる場合があります。 |
| ボット | AEM によって事前に識別および削除されていない不明なボットは、トラッキング不一致の原因となる場合があります。 |
| レポートスイート | 同じ AEM インスタンスとドメインに属するページが、異なる Analytics レポートスイートにデータを送信する場合があります。 |
| サードパーティのモニタリングツールとセキュリティツール | モニタリングツールやセキュリティスキャンツールによっては、Analytics レポートでは追跡されない AEM のコンテンツリクエストが生成される場合があります。 |
| API アクセス | ページまたはAdobe Experience Manager API にプログラムでアクセスすると、Analytics レポートで追跡されないAEMのコンテンツリクエストが生成される場合があります。 |
| プリフェッチリクエスト | ページを事前にロードして速度を上げるプリフェッチサービスを使用すると、コンテンツリクエストのトラフィックが大幅に増加する可能性があります。 |
| DDoS | Adobeは、DDOS 攻撃からのトラフィックを自動的に検出して除外しようとしますが、DDOS 攻撃がすべて検出される保証はありません。 |
| トラフィックブロッカー | ブラウザーでトラッカーブロッカーを使用すると、一部のリクエストの追跡がオプトアウトされる可能性があります。 |
| ファイアウォール | ファイアウォールによって、Analytics のトラッキングがブロックされる可能性があります。このシナリオは、企業ファイアウォールでより頻繁に使用されます。 |

関連トピック [ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md).

### 含まれるコンテンツリクエストのタイプ {#included-content-requests}

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP コード 100-299 | 含む | これらは、すべてのコンテンツまたは部分的なコンテンツを配信する通常のリクエストです。 |
| 自動化用の HTTP ライブラリ | 含む | 例：<br>・ Amazon CloudFront<br>・ Apache Http Client<br>・非同期 Http クライアント<br>・ Axios<br>・アズレウス<br>・ Curl<br>・ GitHub ノードフェッチ<br>・ Guzzle<br>・ Go-http-client<br>・ヘッドレスクロム<br>・ Java™ Client<br>・ジャージー<br>・ Node Oembed<br>・ okhttp<br>・ Python リクエスト<br>・ Reactor Netty<br>・ Wget<br>・ WinHTTP |
| 監視およびヘルスチェックツール | 含む | これらは、サイトの特定の側面を監視するために顧客が設定します。 例えば、可用性や実際のユーザーパフォーマンスなどです。 用途 `/system/probes/health` サイトからの実際のHTMLページではなく、エンドポイント。<br>例：<br>・ Amazon-Route53-Health-Check-Service<br>・ EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>・ Runvison-Site24 x 7<br>・ Mozilla/5.0 以降 ( 互換； UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>・ SoundEyes-Dragonfly-x1<br>・ OmtrBot/1.0<br>・ WebMon/2.0.0 |
| `<link rel="prefetch">` リクエスト | 含む | 次のページの読み込み速度を上げるには、ユーザーがリンクをクリックする前にブラウザーで一連のページを読み込むように設定し、既にキャッシュに存在している必要があります。 *注意：これにより、トラフィックが大幅に増加しています* — 取得されるこれらのページの数に応じて異なります。 |
| Adobe AnalyticsまたはGoogle Analyticsレポートをブロックするトラフィック | 含む | サイトの訪問者には、Google AnalyticsやAdobe Analyticsの正確性に影響を与えるプライバシーソフトウェア（広告ブロッカーなど）がインストールされていることは、より一般的です。 AEMas a Cloud Serviceは、クライアント側ではなく、Adobeが運用するインフラストラクチャへの最初のエントリポイントに対するリクエストをカウントします。 |

関連トピック [ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md).

### 除外されたコンテンツリクエストのタイプ {#excluded-content-request}

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP コード 500 以降 | 除外済み | AEMas a Cloud Serviceまたは顧客カスタムコードで問題が発生した場合に、訪問者にエラーが返されました。 |
| HTTP コード 400-499 | 除外済み | コンテンツが存在しない (404) 場合や、その他のコンテンツまたはリクエスト関連の問題がある場合に、訪問者に返されたエラー。 |
| HTTP コード 300-399 | 除外済み | これらは、サーバー上で何かが変更されたかを確認する、または別のリソースにリクエストをリダイレクトする、適切なリクエストです。 コンテンツ自体が含まれていないので、課金対象になりません。 |
| /libs/*に移動するリクエスト | 除外済み | AEMの内部 JSON リクエスト（課金対象でない CSRF トークンなど）。 |
| DDOS 攻撃からのトラフィック | 除外済み | DDOS 保護。 AEMは一部の DDOS 攻撃を自動検出し、ブロックします。 検出された場合は、DDOS 攻撃は課金対象ではありません。 |
| AEMas a Cloud ServiceNewRelic 監視 | 除外済み | AEMas a Cloud Service的グローバル監視。 |
| 顧客がCloud Serviceプログラムを監視するための URL | 除外済み | 可用性を外部で監視するための推奨 URL。<br><br>`/system/probes/health` |
| AEMas a Cloud Serviceポッドウォームアップサービス | 除外済み | ユーザーエージェント： skyline-service-warmup/1。* |
| よく知られている検索エンジン、ソーシャルネットワーク、HTTP ライブラリ（Fastly によってタグ付け） | 除外済み | サイトを定期的に訪問し、検索インデックスやサービスを更新するよく知られたサービス：<br><br>例：<br>・ AddSearchBot<br>・ AhrefsBot<br>・ Applebot<br>・ Ask Jeeves Corporate Spider<br>・ Bingbot<br>・ BingPreview<br>・ BLEXBot<br>・ BuiltWith<br>・ Bytespider<br>・ CrawlerKengo<br>・ Facebookexternalhit<br>・ Google AdsBot<br>・ Google AdsBot Mobile<br>・ Googlebot<br>・ Googlebot Mobile<br>・ lmspider<br>・ LucidWorks<br>・ MJ12bot<br>・ Pingdom<br>・ Pinterest<br>・ SemrushBot<br>・ SiteImprove<br>・ StashBot<br>・ StatusCakes<br>・ YandexBot |
| 除外Commerce integration framework呼び出し | 除外済み | これらは、Commerce integration frameworkに転送されるAEMに対しておこなわれる要求です。URL はで始まります。 `/api/graphql` — 二重計数を避けるために、Cloud Serviceの請求はできません。 |
| 除外 `manifest.json` | 除外済み | マニフェストは API 呼び出しではありません。デスクトップまたは携帯電話に Web サイトをインストールする方法に関する情報を提供するために、ここに記載されています。 Adobeは次に対する JSON リクエストをカウントしない `/etc.clientlibs/*/manifest.json` |
| 除外 `favicon.ico` | 除外済み | 返されるコンテンツはHTMLや JSON ではありませんが、SAMLHTMLフローなどのシナリオでは、favicon が認証として返される場合があるので、カウントから明示的に除外されることがわかります。 |

## クライアント側コレクション {#cliendside-collection}

### AEM as a Cloud Serviceの Real User Monitoring(RUM) {#real-user-monitoring-for-aem-as-a-cloud-service}

>[!INFO]
>
>この機能は、アーリーアダプタープログラムでのみ使用できます。
>AEM Cloud Serviceバージョンを使用する必要があります **2023.11.14227** RUM データサービスを有効にするためには、上記の手順を実行します。

### 概要 {#overview}

Real User Monitoring(RUM) は、Web サイトやアプリケーションのデジタルユーザーエクスペリエンスをリアルタイムでキャプチャおよび分析する、パフォーマンス監視テクノロジーの一種です。 Web アプリケーションのリアルタイムパフォーマンスを可視化し、エンドユーザーエクスペリエンスに関する正確なインサイトを提供します。

Real User Monitoring(RUM) は、URL の開始からリクエストがブラウザーに返されるまで、主要なパフォーマンス指標に関する深いインサイトを提供します。開発者は、アプリケーションを拡張して、エンドユーザーが簡単に使用できるようにします。

### RUM データ監視サービスのメリットを受けられるのは誰ですか？ {#who-can-benefit-from-rum-data-monitoring-service}

RUM Data Service は、Adobeの CDN を利用する人にとって有益です。ユーザーの操作をより正確に反映し、既存のサーバー側 CDN ログページビューと比較できるクライアント側のページビュー数を反映して、Web サイトのエンゲージメントを確実に測定できます。 さらに、独自の CDN を使用するお客様は、Adobeにより、自動トラフィックレポートを合理化できるようになりました。これにより、Adobeとトラフィックレポートを共有する必要がなくなりました。

また、Adobeの CDN を使用しているお客様と、独自の CDN を使用しているお客様の両方について、ページのパフォーマンスに関する高度なインサイトを得る絶好の機会です。

### RUM(Real User Monitoring) データ・サービスの仕組みの理解 {#understand-how-the-rum-data-service-works}

Adobe Experience Managerは、Real User Monitoring(RUM) を使用して、顧客とAdobeが、Adobe Experience Managerを利用したサイトとの訪問者の関わり方を理解し、パフォーマンスの問題を診断し、実験の効果を測定するのに役立ちます。 RUM は、サンプリングを通じて訪問者のプライバシーを保持します。すべてのページビューのごく一部のみが監視され、すべての個人情報 (PII) の適切な除外が監視されます。

### Real User Monitoring(RUM) とプライバシー {#rum-and-privacy}

Adobe Experience Managerでの実際のユーザー監視は、訪問者のプライバシーを保持し、データ収集を最小限に抑えるように設計されています。 訪問者の場合、訪問中のサイトで個人情報が収集されず、Adobeに利用できなくなります。

サイトオペレーターは、この機能を通じて監視を有効にするために追加のオプトインは必要ないので、RUM 監視を有効にするためにエンドユーザーが受け入れる追加のポップアップはありません。

### RUM データサンプリング {#rum-data-sampling}

従来の Web 分析ソリューションでは、すべての訪問者のデータを収集しようとします。 Adobe Experience Managerの Real User Monitoring では、ページビューのごく一部からの情報のみが取り込まれます。 Real User Monitoring(RUM) は、分析の代わりとなるのではなく、サンプリングおよび匿名化を目的としています。 デフォルトでは、ページのサンプリング率は 1:100 です。 現時点では、サンプリングレートを増減させるために、サイトオペレーターがこの数値を設定することはできません。 合計トラフィックを正確に推定するために、100 ページビューごとに詳細なデータを 1 つから収集し、全体的なトラフィックの概算を信頼できる方法で示します。」

データを収集するかどうかをページビューごとに決定するので、複数のページでのインタラクションを追跡することは事実上不可能になります。 RUM には、訪問、訪問者、セッションの概念がなく、ページビューのみが含まれます。 これは設計によるものです。

### 収集されるデータ {#what-data-is-being-collected}

Real User Monitoring(RUM) は、個人を特定できる情報の収集を防ぐように設計されています。 Adobe Experience Managerの Real User Monitoring で収集できる情報の完全なセットを次に示します。

* 訪問するサイトのホスト名。次に例を示します。 `experienceleague.adobe.com`
* デスクトップやモバイルなど、ページの表示に使用される幅広いユーザーエージェントのタイプ。
* 次のようなデータ収集の時刻。 `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* 訪問するページの URL。例： `https://experienceleague.adobe.com/docs`
* リファラー URL （ユーザーがリンクをたどった場合は、現在のページにリンクしたページの URL）
* 次のような形式の、ランダムに生成されたページビューの ID。 `2Ac6`
* 次のようなサンプリングレートの重みまたは逆。 `100`. つまり、100 ページビューのうち 1 つだけが記録されます。
* ページを読み込む順序、または訪問者として操作する順序での、チェックポイントまたは特定のイベントの名前。
* 前述のチェックポイントに対してユーザーが操作する DOM 要素のソースまたは識別子。 例えば、これは画像の可能性があります
* 上記のチェックポイントに対してユーザーが操作するターゲット、または外部ページへのリンク。 例：`https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* コア Web Vitals(CWV) のパフォーマンス指標、最大のコンテンツペイント (LCP)、最初の入力遅延 (FID)、累積レイアウトシフト (CLS) では、訪問者のエクスペリエンスの質を説明します。

### Real User Monitoring(RUM) データ・サービスの設定方法 {#how-to-set-up-them-rum-data-service}

* アーリーアダプタープログラムに参加したい場合は、次の宛にメールを送信してください： `aemcs-rum-adopter@adobe.com`Adobe IDに関連付けられた電子メールアドレスから、実稼動、ステージ、開発環境のドメイン名と共に入力します。 Adobeの製品チームが Real User Monitoring(RUM) データサービスを有効にします。
* この作業が完了すると、Adobeの製品チームが顧客コラボレーションチャネルを作成します。
* Adobeの製品チームから連絡を受け、ドメインキーとデータダッシュボードの URL を提供します。この URL でページビュー数および [コア Web バイタル (CWV)](https://web.dev/vitals/) クライアント側の Real User Monitoring(RUM) コレクションによって収集される指標。
* その後、ドメインキーを使用してデータダッシュボードの URL にアクセスし指標を表示する方法について説明します。

### 実際のユーザー監視 (RUM) データの使用方法 {#how-rum-data-is-being-used}

RUM データは、次の目的で有益です。

* お客様のサイトのパフォーマンスのボトルネックを特定し、修正する
* 独自の CDN を使用しているお客様のページビュー数を含む、効率的な自動トラフィックレポート。つまり、Adobeとトラフィックレポートを共有する必要はありません。
* 互換性を高めるために、Adobe Experience Managerが同じページ上の他のスクリプト（分析、ターゲティング、外部ライブラリなど）とどのようにやり取りするかを理解するため。

### ページビュー数とパフォーマンス指標の相違に関する制限事項と理解 {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

このデータを分析する際に、Real User Monitoring(RUM) によってレポートされるページビューやその他のパフォーマンス指標に相違が生じる場合と生じない場合があります。 これらの相違は、リアルタイムのクライアント側の監視に固有のいくつかの要因に起因する可能性があります。 お客様が RUM データを解釈する際に留意すべき重要な考慮事項は次のとおりです。

1. **トラッカーブロッカー**

   * トラッカーブロッカーやプライバシー拡張を使用するエンドユーザーは、Real User Monitoring(RUM) のデータ収集を妨げる可能性があります。これらのツールは、トラッキングスクリプトの実行を制限するからです。 この制限により、過少報告されたページビュー数とユーザーのインタラクションが発生し、実際のサイトアクティビティと RUM によってキャプチャされたデータとの間に矛盾が生じる可能性があります。

1. **API/JSON 呼び出しの取得に関する制限**

   * RUM データサービスは、クライアント側のエクスペリエンスに重点を置いており、現時点では、バックエンド API や JSON 呼び出しを取り込んでいません。 Real User Monitoring(RUM) データからこれらの呼び出しを除外すると、CDN Analytics で測定されるコンテンツリクエストからの相違が生じます。

### FAQ {#faq}

1. **監視に含めるまたは除外するパスを設定するにはどうすればよいですか？**

   お客様は、次の変数を使用して、Cloud Manager の設定内で環境変数を設定することで、監視対象の URL を含める、または除外するパスを設定できます。 `AEM_WEBVITALS_EXCLUDE` および `AEM_WEBVITALS_INCLUDE_PATHS`

   デフォルトでは、「含める」設定は「/content」をターゲットに設定されています。 ここで設定する必要があるパスは、ブラウザーに表示される URL パスではなく、システム内のコンテンツパスであることに注意してください。 この区別は、特定のニーズに合わせて設定を正確にセットアップおよびカスタマイズするための重要な要素です。

1. **Adobeは、インタラクションが顧客が管理する CDN に到達する前、または顧客が管理する CDN に到達した時点で、すべてのページビューを追跡できますか。**

   はい。

1. **お客様は、RUM データ・サービス・スクリプトを Dynatrace などのサード・パーティ製システムと統合できますか。**

   はい。

1. **「次のペイントへのインタラクション」、「最初のバイトまでの時間」、「最初のコンテンツのペイント」の Web バイタル指標が収集されているか。**

   次のペイント (INP) と最初のバイトまでの時間 (TTFB) へのインタラクションが収集されます。  現時点では、最初のコンテンツブルペイントは収集されません。
