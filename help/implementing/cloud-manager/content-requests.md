---
title: Cloud Service コンテンツリクエストについて
description: アドビからコンテンツリクエストライセンスを購入している方のために、Adobe Experience Cloud as a Service が測定するコンテンツリクエストのタイプと、組織の分析レポートツールとの相違について説明します。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 7bf48596f64dd9682fa2fb3e5d5db513a8a7fbdc
workflow-type: tm+mt
source-wordcount: '2054'
ht-degree: 67%

---

# Cloud Service コンテンツリクエストについて

## はじめに {#introduction}

コンテンツリクエストには、AEM Sites に送信されるリクエストが含まれます。これらのリクエストは、Edge Delivery Services またはコンテンツ配信ネットワーク（CDN）などの顧客提供のキャッシュシステムを通じてルーティングされる場合があります。これらのリクエストは、構造化データを HTML 形式または JSON 形式で配信し、ページビュー（ページやエクスペリエンスフラグメントなど）または JSON 戻り値をヘッドレス方式で API を通じてサポートします。

ユーザーが HTML または JSON を使用してページを表示すると、コンテンツリクエストがカウントされます。最初のキャッシュシステムがリクエストを受信した時点でこのリクエストを測定します。コンテンツリクエストをカウントする目的で、特定の HTTP リクエストが含められたり除外されたりします。HTTP の[含まれるコンテンツリクエスト](#included-content-requests)と[除外されるコンテンツリクエスト](#excluded-content-request)の完全なリストを参照してください。

>[!NOTE]
>
>コンテンツリクエストビューに表示されるデータは、24 時間ごとに更新されます。

## Cloud Service コンテンツリクエストについて {#understanding-cloud-service-content-requests}

*ページリクエスト*&#x200B;とは、メインページエクスペリエンスをレンダリングするのに必要なコア構造化コンテンツ（HTML や JSON など）を取得する HTTP リクエストを指します。画像やスクリプトなどのアセットのリクエストは含まれません。

標準の CDN を使用しているお客様の場合、AEM as a Cloud Service では、サーバーサイドレベルで測定されたコンテンツリクエストがカウントされます。この測定は自動的に行われ、クライアントサイドの分析トラッキングに依存しません。

AEM（Adobe Experience Manager）as a Cloud Service は、AEM インスタンスによって生成され、CDN で受信された応答タイプに基づいてコンテンツリクエストを識別します。特に、HTML（`text/html`）または JSON（`application/json`）を返すリクエストがカウントされます。これらの形式は通常、従来のサイトレンダリングまたはヘッドレス配信のいずれかでプライマリページコンテンツを配信します。

JavaScript ファイル、CSS スタイルシート、画像などの静的アセットのリクエストは、コンテンツリクエストとしてカウントされません。

>[!NOTE]
>API リクエストがページレベルのコンテンツとして機能する HTML または JSON を返す場合（ヘッドレス配信など）、コンテキストによってはコンテンツリクエストとしてカウントされることがあります。

コンテンツリクエストは、応答が CDN キャッシュから提供されたか、元の AEM 環境に転送されたかに関係なく測定されます。

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Cloud Service コンテンツリクエストの相違 {#content-requests-variances}

コンテンツリクエストは、次の表にまとめられているように、組織の分析レポートツール内で差異が生じる場合があります。一般に、サイトのコンテンツリクエスト数のレポートにクライアントサイドのインストルメンテーションに依存する分析ツールを使用しないでください。これらのツールは、アクティブ化するユーザーの同意に依存しているため、多くの場合、トラフィックの大部分が見逃されることがあります。AEM as a Cloud Service の上に独自の CDN を追加するお客様向けに、ログファイルのサーバーサイドでデータを収集する Analytics ツール、または CDN レポートを使用すると、精度が向上します。

| 差異の理由 | 説明 |
|---|---|
| エンドユーザーの同意 | クライアント側の計測機能に依存する Analytics ツールは、多くの場合、ユーザーの同意がトリガーされるかどうかに依存します。このワークフローは、トラフィックの大部分がトラッキングされていないことを表している可能性があります。コンテンツリクエストを独自に測定する場合は、アドビでは、分析ツールに依存してサーバーサイドまたは CDN レポートのデータを収集することをお勧めします。 |
| タグ付け | Adobe Experience Manager コンテンツリクエストとして追跡されるすべてのページまたは API 呼び出しに対して、Analytics トラッキングでタグ付けされない場合があります。 |
| タグ管理ルール | タグ管理ルールの設定により、ページ上で様々なデータ収集設定が行われ、その結果、コンテンツリクエストのトラッキングとは何らかの不一致が生じる場合があります。 |
| ボット | AEM が事前に識別および削除していない不明なボットは、トラッキング不一致の原因となる場合があります。 |
| レポートスイート | 同じ AEM インスタンス内のページは、異なる分析レポートスイートに報告できます。このプロセスでは、設定に応じて、データを複数のスイートに分割できます。 |
| サードパーティのモニタリングツールとセキュリティツール | モニタリングツールやセキュリティスキャンツール（稼動時間チェッカーや脆弱性スキャナーなど）によっては、ページがリクエストされ、分析レポートには表示されないサーバーサイドコンテンツリクエストが生成される場合があります。 |
| API アクセス | API 経由（例えば、ヘッドレス CMS としての Adobe Experience Manager 経由）の AEM ページまたはコンテンツへのリクエストは、引き続きコンテンツリクエストとしてカウントされますが、分析トラッキングはトリガーされません。 |
| プリフェッチリクエスト | プリフェッチ（例えば、サービスワーカーやエッジ関数の使用）では、事前にページをリクエストすることでトラフィック量が増加する場合があります。これらのリクエストは、サーバーサイドでカウントされますが、クライアントサイドの分析コードは実行されません。 |
| DDoS | アドビでは、フィルタリングを使用して、多くの DDoS 攻撃を検出およびブロックします。ただし、フィルターを適用する前に、一部の攻撃リクエストがコンテンツリクエストとしてカウントされる場合があります。 |
| トラフィックブロッカー | ブラウザー内のプライバシー機能や企業のファイアウォールにより、分析スクリプトの読み込みがブロックされる場合があります。これらのユーザーは、引き続きサーバーサイドのコンテンツリクエストを生成します。 |
| ファイアウォール | 企業または地域のファイアウォールにより、分析呼び出しがアドビサーバーに到達できない場合があります。その結果、分析でレポートが不足する一方で、サーバーサイドのカウントは影響を受けません。 |

ライセンス制限に対するコンテンツリクエストの使用状況の表示とトラッキングについて詳しくは、[ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md)を参照してください。

## サーバーサイドのコレクションルール {#serverside-collection}

AEM as a Cloud Serviceは、サーバーサイドのコレクションルールを適用して、コンテンツリクエストをカウントします。 これらのルールは、認識された AI/LLM クローラーや、サイトに対して定期的に ping を実行する一連の監視サービスなど、よく知られているボット（検索エンジンクローラーなど）を除外します。 この除外リストにない他の合成、自動または監視タイプのトラフィックは、課金対象のコンテンツリクエストとしてカウントされます。

次の表に、含まれるコンテンツリクエストと除外されるコンテンツリクエストのタイプと、それぞれの簡単な説明を示します。

### 含まれるコンテンツリクエストのタイプ {#included-content-requests}

>[!NOTE]
>API リクエストが HTML 応答を返す場合、使用コンテキストに応じてコンテンツリクエストとして分類されることがあります。通常、UI 以外のデータを返す API リクエストは除外されます。

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP コード 100-299 | 次のものが含まれます。 | 完全または部分的な HTML コンテンツまたは JSON コンテンツを返す成功したリクエストが含まれます。<br>HTTP コード 206：これらのリクエストでは、完全なコンテンツの一部のみが配信されます。ページコンテンツのレンダリングに使用されるHTMLまたは JSON 応答の一部を配信する場合、一部のリクエストが含まれます。 |
| 自動化用の HTTP ライブラリ | 次のものが含まれます。 | ページコンテンツを取得するツールまたはライブラリによって行われるリクエスト。例えば、次のようなものがあります。<br>・ Amazon CloudFront<br>・ Apache Http Client<br>・非同期 HTTP Client<br>・ Axios<br>・ Azureus<br>・ Curl<br>・ GitHub Node Fetch<br>・ Guzzle<br>・ Go-http-client<br>・ ヘッドレス Chrome<br>・ Java™ Client<br>・ Jersey<br>・ Node Oembed<br>・ okhttp<br>・ Python リクエスト <br>・ Reactor Netty<br>・ Wget<br>・ WinHTTP <br>・ Fast HTTP<br> <br> <br><br>・ GitHub ノード取得・ Reactor Netty トラフィックが既知のボットとして分類されていない場合は、カスタムエージェントや AI 駆動の自動処理を含めることもできます。 |
| 監視ツールおよびヘルスチェックツール | 次のものが含まれます。 | ページのヘルスまたは可用性を監視するのに使用されるリクエスト。詳しくは、<br>[除外されたコンテンツリクエストのタイプ](#excluded-content-request)を参照してください。<br>例には、次のようなものがあります。<br>• `Amazon-Route53-Health-Check-Service`<br>• EyeMonIT_bot_version_0.1_[（https://eyemonit.com/）](https://eyemonit.com/)<br>• Investis-Site24x7<br>• Mozilla/5.0 以降（互換；UptimeRobot/2.0；[https://uptimerobot.com/](https://uptimerobot.com/)）<br>• ThousandEyes-Dragonfly-x1<br>• OmtrBot/1.0<br>• WebMon/2.0.0 |
| `<link rel="prefetch">` リクエスト | 次のものが含まれます。 | お客様がコンテンツをプリロードまたはプリフェッチすると（例えば、`<link rel="prefetch">` を使用）、これらのサーバーサイドリクエストがカウントされます。このアプローチでは、プリフェッチされるページの数に応じて、トラフィックが増加する場合があります。 |
| Adobe Analytics または Google Analytics レポートをブロックするトラフィック | 次のものが含まれます。 | サイトの訪問者が、Google Analytics や Adobe Analytic sの正確性に影響を与えるプライバシーソフトウェア（広告ブロッカーなど）をインストールしていることがよくあります。AEM as a Cloud Service は、クライアントサイドではなく、アドビが運用するインフラストラクチャへの最初のエントリポイントに対するリクエストをカウントします。 |

[ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md)も参照してください。

### 除外されたコンテンツリクエストのタイプ {#excluded-content-request}

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP Code 500+ | 除外済み | AEM as a Cloud Service または顧客カスタムコードで問題が発生した場合に、訪問者にエラーが返されました。 |
| HTTP コード 400-499 | 除外済み | コンテンツが存在しない（404）場合や、その他のコンテンツまたはリクエスト関連の問題がある場合に、訪問者にエラーが返されました。 |
| HTTP コード 300-399 | 除外済み | サーバー上で何かが変更されたかを確認する、または別のリソースにリクエストをリダイレクトする適切なリクエストです。コンテンツ自体が含まれていないので、課金対象になりません。 |
| `/libs/`* に移動するリクエスト | 除外済み | AEM の内部 JSON リクエスト（課金対象でない CSRF トークンなど）。 |
| DDoS 攻撃からのトラフィック | 除外済み | DDoS 保護。AEM は一部の DDoS 攻撃を自動検出しブロックします。DDoS 攻撃は、検出された場合、課金対象ではありません。 |
| AEM as a Cloud Service NewRelic 監視 | 除外済み | AEM as a Cloud Service グローバル監視。 |
| 顧客が Cloud Service プログラムを監視するための URL | 除外済み | アドビでは、この URL を使用して、可用性やヘルスチェックを外部から監視することをお勧めします。<br><br>`/system/probes/health` |
| AEM as a Cloud Service ポッドウォームアップサービス | 除外済み | エージェント：skyline-service-warmup/1。* |
| よく知られている検索エンジン、ソーシャルネットワーク、HTTP ライブラリ（Fastly によってタグ付け） | 除外済み | サイトを定期的に訪問し、検索インデックスやサービスを更新するよく知られたサービス：<br><br>例：<br>・AddSearchBot<br>・AhrefsBot<br>・Applebot<br>・Ask Jeeves Corporate Spider<br>・Bingbot<br>・BingPreview<br>・BLEXBot<br>・BuiltWith<br>・Bytespider<br>・CrawlerKengo<br>・Facebookexternalhit<br>・Google AdsBot<br>・Google AdsBot Mobile<br>・Googlebot<br>・Googlebot Mobile<br>・lmspider<br>・LucidWorks<br>•`MJ12bot`<br>・Pinterest<br>・SemrushBot<br>・SiteImprove<br>・StashBot<br>・StatusCake<br>・YandexBot<br>・ContentKing<br>・Claudebot |
| よく知られた AI/LLM クローラー（Fastly がタグ付け） | 除外済み | よく知られているボットとして識別された、認識された AI/LLM クローラーからのリクエスト（例えば、`User-Agent` やその他のボット分類シグナルによって）。 これらのリクエストは請求できません。<br><br>AI エージェントが既知のボットとして識別されない場合（例えば、汎用のブラウザーリク `User-Agent` ストを使用する場合）、そのリクエストは課金対象のコンテンツリクエストとしてカウントされる場合があります。 |
| コマース統合フレームワーク呼び出しの除外 | 除外済み | 二重カウントを避けるために、AEM に対して行われたリクエストで、Commerce Integration Framework に転送されます（URL は `/api/graphql` で始まります）。これらは Cloud Service の請求対象ではありません。 |
| `manifest.json` を除外 | 除外済み | マニフェストは API 呼び出しではありません。ここでは、デスクトップまたは携帯電話に web サイトをインストールする方法に関する情報を提供します。アドビは `/etc.clientlibs/*/manifest.json` に対する JSON リクエストをカウントするべきではありません |
| `favicon.ico` を除外 | 除外済み | 返されるコンテンツを HTML や JSON にしないでください。ただし、SAML 認証フローなどの特定のシナリオでは、favicon が HTML として返されることが確認されています。その結果、favicon はカウントから明示的に除外されます。 |
| エクスペリエンスフラグメント（XF） – 同じドメインの再利用 | 除外済み | 同じドメインでホストされるページから XF パス（`/content/experience-fragments/...` など）に対して行われるリクエスト（リクエストホストに一致するリファラーヘッダーで識別される）。<br><br>例：同じドメインのバナーまたはカードの XF を取り込む `aem.customer.com` 上のホームページ。<br><br>・ URL が/content/experience-fragments/...<br>・ リファラードメインが一致 `request_x_forwarded_host`<br><br>**注意：** エクスペリエンスフラグメントのパスがカスタマイズされている場合（例えば、`/XFrags/...` や `/content/experience-fragments/` 以外のパスを使用している場合）、リクエストは除外されず、同じドメインであってもカウントされる場合があります。 Adobeでは、Adobeの標準 XF パス構造を使用して、除外ロジックが正しく適用されるようにすることをお勧めします。 |

## コンテンツリクエストの管理 {#managing-content-requests}

上記の節 [Cloud Service コンテンツリクエストの相違 ](#content-requests-variances) で説明したように、コンテンツリクエストは、様々な理由により、予期よりも多くなる可能性があります。一般的なスレッドは、CDN にヒットするトラフィックです。  AEMのお客様には、ライセンス予算に合わせてコンテンツリクエストをモニタリングし、管理することが有利です。  コンテンツリクエストの管理は、通常、実装技術と [ トラフィックフィルタールール ](/help/security/traffic-filter-rules-including-waf.md) を組み合わせたものです。

### コンテンツリクエストを管理する実装手法 {#implementation-techniques-to-manage-crs}

* ページが見つからないという応答は、HTTP ステータス 404 で配信されます。  ステータス 200 で返された場合、コンテンツリクエストにカウントされます。
* ヘルスチェックまたはモニタリングツールを/system/probes/health URL にルーティングするか、GETの代わりにHEAD メソッドを使用して、コンテンツリクエストの発生を避けます。
* サイトと統合したカスタム検索クローラーのAEM ライセンスコストと、コンテンツの鮮度に関するニーズのバランスを取ります。  過度にアグレッシブなクローラーは、多くのコンテンツリクエストを消費する可能性があります。
* 2 つの異なるコンテンツリクエストが発生するのを避けるために、リダイレクトをクライアントサイド（JavaScript リダイレクトの場合はステータス 200）ではなくサーバーサイド（ステータス 301 または 302）で処理します。
* API 呼び出しを結合または短縮します。API 呼び出しは、ページをレンダリングするために読み込むことができるAEMからの JSON 応答です。
* ブラウザーのユーザーエージェントがAEMに正しく渡されていることを確認します。 これは、前述の「よく知られた検索エンジン」コンテンツリクエストの除外ルールを活用します。  特定のヘッドレス実装または CDN 設定で、発信者ユーザーエージェントが失われることもあります。 その場合、除外が防がれ、ユーザーエージェントをパススルーした場合よりも高いコンテンツリクエストが発生する可能性があります。

### コンテンツリクエストを管理するトラフィックフィルタールール {#traffic-filter-rules-to-manage-crs}

* 一般的なボットパターンは、空のユーザーエージェントを使用することです。  実装とトラフィックパターンを見直して、空のユーザーエージェントが役に立つかどうかを確認します。  このトラフィックをブロックする場合は、推奨される [ 構文 ](/help/security/traffic-filter-rules-including-waf.md#rules-syntax) を次に示します。

```
trafficFilters:
  rules:
    - name: block-missing-user-agent
      when:
        anyOf:
          - { reqHeader: user-agent, exists: false }
          - { reqHeader: user-agent, equals: '' }
      action: block
```

* ある日ボットが非常に激しくサイトに当たり、次の日には消えてしまう場合もあります。 このような機能は、特定の IP アドレスまたはユーザーエージェントをブロックしようとする試みを台無しにする可能性があります。  一般的なアプローチの 1 つは、[ レート制限ルール ](/help/security/traffic-filter-rules-including-waf.md#rate-limit-rules) を導入することです。  [ 例 ](/help/security/traffic-filter-rules-including-waf.md#ratelimiting-examples) を確認し、リクエストの急速な割合に対する許容値に一致するルールを作成します。  一般的なレート制限を許可する必要がある例外について、[ 条件構造 ](/help/security/traffic-filter-rules-including-waf.md#condition-structure) の構文を確認します。
