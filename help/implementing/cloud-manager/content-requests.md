---
title: Cloud Service コンテンツリクエストについて
description: アドビからコンテンツリクエストライセンスを購入している方のために、Adobe Experience Cloud as a Service が測定するコンテンツリクエストのタイプと、組織の分析レポートツールとの相違について説明します。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 2f02b9d70e56f4aafd802e986974533197f7d7a5
workflow-type: tm+mt
source-wordcount: '2276'
ht-degree: 51%

---

# Cloud Service コンテンツリクエストについて

## はじめに {#introduction}

コンテンツリクエストには、AEM Sites に送信されるリクエストが含まれます。 これらのリクエストは、Edge Delivery ServicesまたはContent Delivery Network （CDN）などのお客様が提供するキャッシングシステムを経由します。 これらのリクエストは、構造化データを HTML 形式または JSON 形式で配信し、ページビュー（ページやエクスペリエンスフラグメントなど）または JSON 戻り値をヘッドレス方式で API を通じてサポートします。

ユーザーが HTML または JSON を使用してページを表示すると、コンテンツリクエストがカウントされます。 最初のキャッシュシステムがリクエストを受信した時点でこのリクエストを測定します。 コンテンツリクエストをカウントする目的で、特定の HTTP リクエストが含められたり除外されたりします。 HTTP の[含まれるコンテンツリクエスト](#included-content-requests)と[除外されるコンテンツリクエスト](#excluded-content-requests)の完全なリストを参照してください。

>[!NOTE]
>
>コンテンツリクエストビューに表示されるデータは、24 時間ごとに更新されます。

## Cloud Service コンテンツリクエストについて {#understanding-cloud-service-content-requests}

*ページリクエスト*&#x200B;とは、メインページエクスペリエンスをレンダリングするのに必要なコア構造化コンテンツ（HTML や JSON など）を取得する HTTP リクエストを指します。 画像やスクリプトなどのアセットのリクエストは含まれません。

デフォルトのCDNを使用しているお客様の場合、AEM as a Cloud Serviceでは、コンテンツリクエストがサーバーサイドレベルで測定されます。 この測定は自動的に行われ、クライアントサイドの分析トラッキングに依存しません。

AEM（Adobe Experience Manager）as a Cloud Service は、AEM インスタンスによって生成され、CDN で受信された応答タイプに基づいてコンテンツリクエストを識別します。 特に、HTML（`text/html`）または JSON（`application/json`）を返すリクエストがカウントされます。 これらの形式は通常、従来のサイトレンダリングまたはヘッドレス配信のいずれかでプライマリページコンテンツを配信します。

JavaScript ファイル、CSS スタイルシート、画像などの静的アセットのリクエストは、コンテンツリクエストとしてカウントされません。

>[!NOTE]
>API リクエストがページレベルのコンテンツ（ヘッドレス配信など）として機能するHTMLまたはJSONを返す場合、そのコンテキストに応じてコンテンツリクエストとしてカウントされます。

コンテンツリクエストは、応答が CDN キャッシュから提供されたか、元の AEM 環境に転送されたかに関係なく測定されます。

<!--
 REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website  engagement.
-->

### Cloud Service コンテンツリクエストの相違 {#content-requests-variances}

コンテンツリクエストは、次の表にまとめられているように、組織の分析レポートツール内で差異が生じる場合があります。 一般に、サイトのコンテンツリクエスト数のレポートにクライアントサイドのインストルメンテーションに依存する分析ツールを使用しないでください。 これらのツールは、アクティブ化するユーザーの同意に依存しているため、多くの場合、トラフィックの大部分が見逃されることがあります。 ログファイルやCDN レポートでサーバーサイドのデータを収集する分析ツールは、独自のCDNをAEM as a Cloud Serviceに追加するお客様向けに、より良いカウントを提供します。

| 差異の理由 | 説明 |
|---|---|
| エンドユーザーの同意 | クライアント側の計測機能に依存する Analytics ツールは、多くの場合、ユーザーの同意がトリガーされるかどうかに依存します。 このワークフローは、トラフィックの大部分がトラッキングされていないことを表している可能性があります。 コンテンツリクエストを独自に測定する場合は、アドビでは、分析ツールに依存してサーバーサイドまたは CDN レポートのデータを収集することをお勧めします。 |
| タグ付け | Adobe Experience Manager コンテンツリクエストとして追跡されるすべてのページまたは API 呼び出しに対して、Analytics トラッキングでタグ付けされない場合があります。 |
| タグ管理ルール | タグ管理ルールの設定により、ページ上で様々なデータ収集設定が行われ、その結果、コンテンツリクエストのトラッキングとは何らかの不一致が生じる場合があります。 |
| ボット | AEM が事前に識別および削除していない不明なボットは、トラッキング不一致の原因となる場合があります。 |
| レポートスイート | 同じ AEM インスタンス内のページは、異なる分析レポートスイートに報告できます。 このプロセスでは、設定に応じて、データを複数のスイートに分割できます。 |
| サードパーティのモニタリングツールとセキュリティツール | モニタリングツールやセキュリティスキャンツール（稼動時間チェッカーや脆弱性スキャナーなど）によっては、ページがリクエストされ、分析レポートには表示されないサーバーサイドコンテンツリクエストが生成される場合があります。 |
| API アクセス | APIを介したAEM ページまたはコンテンツへのリクエスト（例：Adobe Experience Manager as a Headless CMS）は、引き続きコンテンツリクエストとしてカウントされますが、分析トラッキングはトリガーされません。 |
| プリフェッチリクエスト | プリフェッチ（例えば、サービスワーカーやエッジ関数の使用）では、事前にページをリクエストすることでトラフィック量が増加する場合があります。 これらのリクエストは、サーバーサイドでカウントされますが、クライアントサイドの分析コードは実行されません。 |
| DDoS | アドビでは、フィルタリングを使用して、多くの DDoS 攻撃を検出およびブロックします。 ただし、フィルターを適用する前に、一部の攻撃リクエストがコンテンツリクエストとしてカウントされる場合があります。 |
| トラフィックブロッカー | ブラウザー内のプライバシー機能や企業のファイアウォールにより、分析スクリプトの読み込みがブロックされる場合があります。 これらのユーザーは、引き続きサーバーサイドのコンテンツリクエストを生成します。 |
| ファイアウォール | 企業または地域のファイアウォールにより、分析呼び出しがアドビサーバーに到達できない場合があります。その結果、分析でレポートが不足する一方で、サーバーサイドのカウントは影響を受けません。 |

ライセンス制限に対するコンテンツリクエストの使用状況の表示とトラッキングについて詳しくは、[ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md)を参照してください。

## サーバーサイドのコレクションルール {#serverside-collection}

AEM as a Cloud Serviceでは、コンテンツリクエストのカウントにサーバーサイドのコレクションルールを適用します。 これらのルールでは、AIやLLMのweb クローラーが認識されるなどの既知のボット（検索エンジンweb クローラーなど）や、サイトに定期的にpingを送信する一連のモニタリングサービスは除外されます。 この除外リストに含まれていないその他の合成、自動、または監視トラフィックは、請求可能なコンテンツリクエストとしてカウントされます。

次の表に、含まれるコンテンツリクエストと除外されるコンテンツリクエストのタイプと、それぞれの簡単な説明を示します。

### 含まれるコンテンツリクエストのタイプ {#included-content-requests}

>[!NOTE]
>API リクエストがHTML レスポンスを返す場合、その使用コンテキストに応じて、コンテンツリクエストとして分類されます。 通常、UI 以外のデータを返す API リクエストは除外されます。

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP コード 100-299 | 次のものが含まれます。 | HTMLまたはJSON コンテンツの一部または全部を返す正常なリクエストが含まれます。<br>HTTP Code 206：これらのリクエストは、完全なコンテンツの一部のみを配信します。 部分的なリクエストは、ページコンテンツのレンダリングに使用されるHTMLまたはJSON レスポンスの一部を配信する場合に含まれます。 |
| 自動化用の HTTP ライブラリ | 次のものが含まれます。 | ページコンテンツを取得するツールまたはライブラリによって行われるリクエスト。 例としては、次のようなものがあります。<br>・ Amazon CloudFront<br>・ Apache Http Client<br>・非同期HTTP Client<br>・ Axios<br>・ Azureus<br>・ Curl<br>・ GitHub Node Fetch<br>・ Guzzle<br>・ Go-http-client<br>・ ヘッドレス Chrome<br>・ Java™ Client<br>・ Jersey<br>・ Node Oembed<br>・ okhttp<br>・ Python Requests<br>・・<br> Netty&rbrace; Wget<br>・ WinHTTP<br>・ Fast HTTP<br>・ GitHub Node Fetch<br>・ Reactor Netty<br><br> トラフィックが既知のボットとして分類されていない場合は、カスタムエージェントまたはAI駆動型の自動化を含めることもできます。 |
| 監視ツールおよびヘルスチェックツール | 次のものが含まれます。 | ページのヘルスまたは可用性を監視するのに使用されるリクエスト。詳しくは、<br>[除外されたコンテンツリクエストのタイプ](#excluded-content-request)を参照してください。<br>例には、次のようなものがあります。<br>• `Amazon-Route53-Health-Check-Service`<br>• EyeMonIT_bot_version_0.1_[（https://eyemonit.com/）](https://eyemonit.com/)<br>• Investis-Site24x7<br>• Mozilla/5.0 以降（互換；UptimeRobot/2.0；[https://uptimerobot.com/](https://uptimerobot.com/)）<br>• ThousandEyes-Dragonfly-x1<br>• OmtrBot/1.0<br>• WebMon/2.0.0 |
| `<link rel="prefetch">` リクエスト | 次のものが含まれます。 | お客様がコンテンツをプリロードまたはプリフェッチすると（例えば、`<link rel="prefetch">` を使用）、これらのサーバーサイドリクエストがカウントされます。 このアプローチでは、プリフェッチされるページの数に応じて、トラフィックが増加する場合があります。 |
| Adobe Analytics または Google Analytics レポートをブロックするトラフィック | 次のものが含まれます。 | サイトの訪問者が、Google Analytics や Adobe Analytic sの正確性に影響を与えるプライバシーソフトウェア（広告ブロッカーなど）をインストールしていることがよくあります。 AEM as a Cloud Service は、クライアントサイドではなく、アドビが運用するインフラストラクチャへの最初のエントリポイントに対するリクエストをカウントします。 |

[&#x200B; ライセンスダッシュボード &#x200B;](/help/implementing/cloud-manager/license-dashboard.md)も参照してください。

### 除外されたコンテンツリクエストのタイプ {#excluded-content-request}

| リクエストタイプ | コンテンツリクエスト | 説明 |
| --- | --- | --- |
| HTTP Code 500+ | 除外済み | AEM as a Cloud Service または顧客カスタムコードで問題が発生した場合に、訪問者にエラーが返されました。 |
| HTTP コード 400-499 | 除外済み | コンテンツが存在しない（404）場合や、その他のコンテンツまたはリクエスト関連の問題がある場合に、訪問者にエラーが返されました。 |
| HTTP コード 300-399 | 除外済み | サーバー上で何かが変更されたかを確認する、または別のリソースにリクエストをリダイレクトする適切なリクエストです。 コンテンツ自体が含まれていないので、課金対象になりません。 |
| `/libs/`* に移動するリクエスト | 除外済み | AEM の内部 JSON リクエスト（課金対象でない CSRF トークンなど）。 |
| DDoS 攻撃からのトラフィック | 除外済み | DDoS 保護。 AEM は一部の DDoS 攻撃を自動検出しブロックします。 DDoS 攻撃は、検出された場合、課金対象ではありません。 |
| AEM as a Cloud Service NewRelic 監視 | 除外済み | AEM as a Cloud Service グローバル監視。 |
| 顧客が Cloud Service プログラムを監視するための URL | 除外済み | Adobeでは、URLを使用して可用性またはヘルスチェックを外部で監視することをお勧めします。<br><br>`/system/probes/health`<br><br>Edge Delivery サイトを監視する場合、Adobeでは、任意のページに対する`GET`件のリクエストではなく`HEAD`件のリクエストを使用することをお勧めします。 `/system/probes/health` パスがEdge Deliveryに存在しません。 |
| AEM as a Cloud Service ポッドウォームアップサービス | 除外済み | エージェント：skyline-service-warmup/1.* |
| よく知られている検索エンジン、ソーシャルネットワーク、HTTP ライブラリ（Fastly によってタグ付け） | 除外済み | サイトを定期的に訪問し、検索インデックスやサービスを更新するよく知られたサービス：<br><br>例：<br>・AddSearchBot<br>・AhrefsBot<br>・Applebot<br>・Ask Jeeves Corporate Spider<br>・Bingbot<br>・BingPreview<br>・BLEXBot<br>・BuiltWith<br>・Bytespider<br>・CrawlerKengo<br>・Facebookexternalhit<br>・Google AdsBot<br>・Google AdsBot Mobile<br>・Googlebot<br>・Googlebot Mobile<br>・lmspider<br>・LucidWorks<br>•`MJ12bot`<br>・Pinterest<br>・SemrushBot<br>・SiteImprove<br>・StashBot<br>・StatusCake<br>・YandexBot<br>・ContentKing<br>・Claudebot |
| 有名なAI/LLMweb クローラー（Fastlyのタグ付け） | 除外済み | 既知のボットとして識別された、AI/LLMweb クローラーからのリクエスト（例：`User-Agent`または他のボット分類シグナル） これらのリクエストには課金されません。<br><br>このような除外されたボットの例としては、ChatGPT、Gmail Image Proxy、Baidu Spider、Outbrain、Yahoo! メールプロキシ、aiHitBot、Mail.Ru Bot、DomainStatsBot、Rainmeter、MetaInspector、Yahoo Gemini。<br><br>AI エージェントが既知のボットとして識別されない場合（汎用ブラウザー`User-Agent`を使用するなど）、そのリクエストは請求可能なコンテンツリクエストとしてカウントされる場合があります。 |
| コマース統合フレームワーク呼び出しの除外 | 除外済み | 二重カウントを避けるために、AEM に対して行われたリクエストで、Commerce Integration Framework に転送されます（URL は `/api/graphql` で始まります）。これらは Cloud Service の請求対象ではありません。 |
| クライアントライブラリ （/etc.clientlibs/*） – 除外 | 除外済み | /etc.clientlibs/*のリクエストは、AEMで使用されるプラットフォームレベルのクライアントライブラリアセットとランタイム設定ファイルです。 これらのリクエストは、顧客が作成したコンテンツやビジネスデータを配信するものではないため、コンテンツリクエストとしてカウントされません。 |
| `favicon.ico` を除外 | 除外済み | 返されるコンテンツを HTML や JSON にしないでください。ただし、SAML 認証フローなどの特定のシナリオでは、favicon が HTML として返されることが確認されています。 その結果、favicon はカウントから明示的に除外されます。 |
| エクスペリエンスフラグメント（XF） – 同じドメインの再利用 | 除外済み | 同じドメインでホストされているページ（リクエストホストに一致するリファラーヘッダーで識別される）からXF パス（`/content/experience-fragments/...`など）に対して行われたリクエスト。<br><br> 例：`aem.customer.com`のホームページが、同じドメインのバナーまたはカードのXFを取り込んでいます。<br><br>・ URLが/content/experience-fragments/...<br>・ リファラードメインが&#x200B;`request_x_forwarded_host`<br><br>**と一致しますメモ：** エクスペリエンスフラグメントのパスがカスタマイズされている場合（`/XFrags/...`や`/content/experience-fragments/`以外のパスを使用するなど）、リクエストは除外されず、同じドメインの場合でもカウントされる可能性があります。 Adobeでは、除外ロジックが正しく適用されるように、Adobeの標準XF パス構造を使用することをお勧めします。 |

## コンテンツリクエストの管理 {#managing-content-requests}

[Cloud Service コンテンツリクエストの分散](#content-requests-variances)で述べたように、コンテンツリクエストは、CDNに到達するトラフィックなど、いくつかの理由により、予想よりも高くなる可能性があります。 AEMをご利用のお客様は、ライセンスの範囲内でコンテンツのリクエストを監視および管理できます。 コンテンツリクエストの管理は、実装技術と[&#x200B; トラフィックフィルタールール &#x200B;](/help/security/traffic-filter-rules-including-waf.md)を組み合わせて行います。

### コンテンツリクエストを管理するための実装手法 {#implementation-techniques-to-manage-crs}

* ページが見つからない応答がHTTP ステータス 404で配信されていることを確認します。 ステータスが200で返された場合、コンテンツリクエストにカウントされます。
* ヘルスチェックまたは監視ツールを/system/probes/health URLにルーティングするか、GETの代わりにHEAD メソッドを使用して、コンテンツリクエストが発生しないようにします。
* コンテンツの鮮度に対するニーズと、サイトに統合したカスタム検索web クローラーのAEMライセンスコストとのバランスを取ります。 過度にアクティブなweb クローラーは、多くのコンテンツリクエストを消費します。
* 2つの別々のコンテンツリクエストを避けるには、任意のリダイレクトをクライアントサイド（JavaScript リダイレクトを使用したステータス 200）ではなく、サーバーサイド（ステータス 301または302）として処理します。
* ページをレンダリングするために読み込まれるAEMからのJSON応答であるAPI呼び出しを組み合わせるか減らします。
* ブラウザーのユーザーエージェントがAEMに正しく渡されていることを確認します。 これにより、上記の「既知の検索エンジン」コンテンツリクエスト除外ルールが活用されます。 特定のヘッドレス実装またはCDN設定で、発信元のユーザーエージェントが失われることがあります。 そのような場合は、除外を防ぎ、ユーザーエージェントが通過した場合よりも高いコンテンツリクエストにつながる可能性があります。

### コンテンツリクエストを管理するためのトラフィックフィルタールール {#traffic-filter-rules-to-manage-crs}

コンテンツリクエストをより適切に制御するには、フィルタールールを定義する前にCDN トラフィックを分析します。 [CDN ログ分析ツール &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/cloud-manager/devops/cdn-log-analysis)を使用すると、CDNのパフォーマンスとリクエスト パターンに関するインサイトを得ることができます。 まず、トラフィックの送信元と、予期しないシグナリングパターンが存在するかどうかを確認します（一般的なボットパターンは、空のユーザーエージェントを使用することです）。

**監視および記録する項目：**

* 顧客国
* クライアントネットワーク（自律型システム/AS）
* クライアント IP
* ユーザーエージェントとボットのカテゴリ

リクエスト変換を使用して、リクエストログにプロパティを追加し、CDN ログとダッシュボードに表示できます。 例えば、分析のためにボット名とクライアントネットワーク（AS名）をログに記録するには、次の手順を実行します。

```yaml
requestTransformations:
  rules:
    - name: log-on-request
      when: "*"
      actions:
        - type: set
          logProperty: bot_name
          value: { reqProperty: botName }
        - type: set
          logProperty: cli_network
          value: { reqProperty: clientAsName }
```

不要なトラフィック（国、ネットワーク、ボット、またはその他のシグナル）を特定したら、トラフィックフィルタールールでブロックできます。 クライアントの国、ネットワーク、またはボット名でブロックするルールの例：

```yaml
trafficFilters:
  rules:
    - name: block-bad-client-traffic
      when:
        anyOf:
          - { reqProperty: clientCountry, equals: "XX" }
          - { reqProperty: clientAsName, equals: "UnwantedClientNetwork" }
          - { reqProperty: botName, equals: "UnwantedBot" }
          - { reqHeader: user-agent, exists: false }
          - { reqHeader: user-agent, equals: '' }
      action: block
```

サンプル値を、ブロックする国コード、ネットワークまたはボット名に置き換えます。 その他のオプションについては、[&#x200B; トラフィックフィルタールールの構文](/help/security/traffic-filter-rules-including-waf.md#rules-syntax)および[条件構造](/help/implementing/dispatcher/cdn-configuring-traffic.md#condition-structure)を参照してください。

ある日トラフィックを持つサイトを過負荷にして、次の日に消えてしまうボットもあります。 このような機能は、特定のIP アドレスまたはユーザーエージェントをブロックする試みを複雑にする可能性があります。 一般的なアプローチの1つは、[&#x200B; レート制限ルール &#x200B;](/help/security/traffic-filter-rules-including-waf.md#rate-limit-rules)を導入することです。 [例](/help/security/traffic-filter-rules-including-waf.md#ratelimiting-examples)を確認し、リクエストの速度が速い場合に許容値と一致するルールを作成します。 一般的なレート制限を許可する例外については、[条件構造](/help/implementing/dispatcher/cdn-configuring-traffic.md#condition-structure)構文を確認してください。

