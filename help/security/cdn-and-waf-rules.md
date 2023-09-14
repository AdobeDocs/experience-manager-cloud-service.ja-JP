---
title: トラフィックフィルタルールの設定（WAF ルールを使用）
description: トラフィックフィルタルール（WAF ルールと共に）を使用してトラフィックをフィルタリングする
source-git-commit: b1b184b63ab6cdeb8a4e0019c31a34db59438a3d
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 2%

---


# トラフィックをフィルタリングするためのトラフィックフィルタルールの設定（WAF ルールを使用） {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>この機能は、まだ一般には利用できません。 継続中のアーリーアダプタープログラムに参加するには、E メールを送信します。 **aemcs-waf-adopter@adobe.com**（組織の名前や機能への関心に関するコンテキストを含む）

Adobeは、お客様の Web サイトに対する攻撃を軽減しようとしますが、悪意のあるトラフィックがアプリケーションに到達しないように、特定のパターンに一致するトラフィックを積極的にフィルタリングすると便利です。 考えられるアプローチは次のとおりです。

* などの Apache レイヤーモジュール `mod_security`
* Cloud Manager の設定パイプラインを通じて CDN にデプロイされるトラフィックフィルタールールの設定

この記事では、トラフィックフィルタールールのアプローチについて説明します。 これらのルールのほとんどは、IP、パス、ユーザーエージェントなど、リクエストのプロパティとリクエストヘッダーに基づいてリクエストをブロックまたは許可します。 これらのルールは、すべてのAEMas a Cloud ServiceサイトおよびFormsのお客様が設定できます。

WAF(Web Application Firewall) アドオンにライセンスを持つお客様は、「WAF traffic filter rules」と呼ばれる追加のカテゴリのルールを設定することもできます（つまり、WAF のルールを設定する必要があります）。 これらの WAF ルールは、悪意のあるトラフィックに関連付けられていると知られている様々なパターンに一致するリクエストをブロックします。 この機能のライセンスの詳細については、Adobeのアカウントチームにお問い合わせください。 アーリーアダプタープログラム中に追加のライセンスは必要ありません。

トラフィックフィルタールールは、実稼動（サンドボックス以外）プログラムのすべてのクラウド環境タイプ（RDE、開発、ステージング、実稼動）にデプロイできます。

## セットアップ {#setup}

1. まず、Git の最上位フォルダーに次のフォルダーとファイル構造を作成します。

   ```
   config/
        cdn/
           cdn.yaml
   ```

1. `cdn.yaml` には、メタデータと、トラフィックフィルタールールおよび WAF ルールのリストが含まれている必要があります。

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     trafficFilters:
       rules:
         ...
   ```

「kind」パラメーターは「CDN」に、バージョンはスキーマのバージョン（現在は「1」）に設定する必要があります。 後述の例を参照してください。


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. WAF ルールを設定するには、新しいプログラムシナリオと既存のプログラムシナリオの両方で、以下の説明に従って、Cloud Manager で WAF を有効にする必要があります。 WAF 用に別のライセンスを購入する必要があります。

   1. 新しいプログラムで WAF を設定するには、 **WAF-DDOS 保護** のチェックボックス **セキュリティ** 」タブを使用します。 引き続き、 [実稼動プログラムの追加](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) プログラムを作成するには

   1. 既存のプログラムで WAF を設定するには、 **プログラムを編集** オプションを使用する場合は、 [プログラムの編集](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) ドキュメント。 次に、 **セキュリティ** ウィザードのタブでは、WAF-DDOS オプションをいつでもオンまたはオフにできます

1. RDE 以外の環境タイプの場合は、Cloud Manager 設定パイプラインを実行します。このパイプラインは以下に説明するように設定できます。

   1. Cloud Manager ホームページのパイプラインカードから、を選択します。 **実稼動パイプラインを追加** または **実稼動以外のパイプラインを追加** 「パイプライン追加」ウィザードを起動するには
   1. 選択 **デプロイメントパイプライン** （「設定」タブ内）

      ![「デプロイメントパイプライン」オプションを選択します。](/help/security/assets/deployment.png)

   1. パイプラインに名前を付け、デプロイメントトリガーを選択して、 **続行**
   1. Adobe Analytics の **ソースコード** タブ、選択 **ターゲットのデプロイメント**&#x200B;を選択し、「 **Config**

      ![ターゲットのデプロイメントを選択](/help/security/assets/target-deployment.png)

   1. 必要に応じて、リポジトリとブランチを選択します。 選択した環境に設定パイプラインが存在する場合、この選択は無効になります。

      ![設定パイプラインの概要](/help/security/assets/config-pipeline.png)

      >[!NOTE]
      >
      > これらのパイプラインを設定または実行するには、ユーザーがデプロイメントマネージャーとしてログインする必要があります。
      > また、環境ごとに 1 つの設定パイプラインのみを設定および実行できます。

   1. 「**保存**」を選択します。新しいパイプラインがパイプラインカードに表示され、準備が整ったら実行できます。
   1. RDE の場合は、コマンドラインが使用されますが、現時点では RDE はサポートされていません。

## トラフィックフィルタールールの構文 {#rules-syntax}

次の項目を設定できます。 `traffic filter rules` を使用して、IP、ユーザーエージェント、リクエストヘッダー、ホスト名、地域、url などのパターンを照合します。

WAF 製品のライセンスを持つお客様は、トラフィックフィルタールールの特別なカテゴリを設定することもできます。 `WAF traffic filter rules` （または WAF ルールの略）1 つ以上の WAF フラグを参照するもの。このフラグは、以下のセクションにリストされています。

次に、WAF ルールも含む一連のトラフィックフィルタールールの例を示します。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

cdn.yaml ファイルのトラフィックフィルタールールの形式を以下に示します。 後の節の例を参照してください。


| **プロパティ** | **ほとんどのトラフィックフィルタールール** | **WAF トラフィックフィルタルール** | **タイプ** | **デフォルト値** | **説明** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | ルール名（64 文字）（英数字と — のみを含めることができます） |
| when | X | X | `Condition` | - | 基本的な構造は次のとおりです。<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>以下の「条件構造の構文」を参照してください。ここでは、ゲッター、述語および複数の条件を組み合わせる方法について説明しています。 |
| アクション | X | X | `Action` | ログ | log、allow、block、log、または action オブジェクト。デフォルトは log です。 |
| rateLimit | X |   | `RateLimit` | 定義なし | レート制限の設定。 レート制限は、定義されていない場合、無効になります。<br><br>以下に、rateLimit 構文と例を説明する別の節を示します。 |

### 条件の構造 {#condition-structure}

条件は、単純な条件または条件のグループにすることができます。

**単純条件**

単純条件は、ゲッターと述語で構成されています。

```
{ <getter>: <value>, <predicate>: <value> }
```

**グループ条件**

条件のグループは、複数の単純な条件やグループ条件で構成されます。

```
<allOf|anyOf>:
  - { <getter>: <value>, <predicate>: <value> }
  - { <getter>: <value>, <predicate>: <value> }
  - <allOf|anyOf>:
    - { <getter>: <value>, <predicate>: <value> }
```

| **プロパティ** | **タイプ** | **意味** |
|---|---|---|
| **allOf** | `array[Condition]` | **および** 操作。 true を指定すると、リストに表示されているすべての条件が true を返します。 |
| **anyOf** | `array[Condition]` | **または** 操作。 リストに表示された条件のいずれかが true を返す場合は true |

**ゲッター**

| **プロパティ** | **タイプ** | **説明** |
|---|---|---|
| reqProperty | `string` | リクエストプロパティ。<br><br>次のいずれか： `path` , `queryString`, `method`, `tier`, `domain`, `clientIp`, `clientCountry`<br><br>domain プロパティは、要求のホストヘッダーを小文字で変換したものです。 文字列の比較に役立つので、大文字と小文字の区別による一致の排除はおこなわれません。<br><br>The `clientCountry` は、次の 2 つの文字コードを使用します： [https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) |
| reqHeader | `string` | 指定された名前のリクエストヘッダーを返します |
| queryParam | `string` | 指定された名前のクエリパラメータを返します |
| cookie | `string` | 指定された名前の Cookie を返します |

**述語**

| **プロパティ** | **タイプ** | **意味** |
|---|---|---|
| **が次の値と等しい** | `string` | ゲッターの結果が指定された値と等しい場合は true |
| **doesNotEqual** | `string` | ゲッターの結果が指定された値と等しくない場合は true |
| **「いいね！」** | `string` | 取得結果が指定されたパターンと一致する場合は true |
| **notLike** | `string` | getter の結果が指定されたパターンに一致しない場合は true |
| **一致** | `string` | 取得結果が指定された正規表現と一致する場合は true |
| **doesNotMatch** | `string` | getter の結果が指定された正規表現と一致しない場合は true |
| **の** | `array[string]` | 指定されたリストにゲッター結果が含まれている場合は true |
| **notIn** | `array[string]` | 指定されたリストにゲッター結果が含まれていない場合は true |

### アクション構造 {#action-structure}

指定者 `action` アクションタイプ (allow、block、log) を指定する文字列か、他のすべてのオプションのデフォルト値、またはルールタイプがで定義されるオブジェクトを指定できるフィールド `type` 必須フィールドと、そのタイプに適用できる他のオプション。

**アクションタイプ**

アクションは、次の表に示すタイプに従って優先順位付けされ、実行される順序アクションを反映するように順序付けされます。

| **名前** | **許可されたプロパティ** | **意味** |
|---|---|---|
| **許可** | `wafFlags`（オプション） | wafFlags が存在しない場合、はそれ以上のルール処理を停止し、応答を提供します。 wafFlags が存在する場合、指定された WAF 保護が無効になり、追加のルール処理に進みます。 |
| **ブロック** | `status, wafFlags` （オプションで、相互に排他的） | wafFlags が存在しない場合、他のすべてのプロパティをバイパスして HTTP エラーを返します。エラーコードは status プロパティによって定義されます。またはデフォルトは 406 です。 wafFlags が存在する場合は、指定された WAF 保護を有効にし、さらにルール処理を続行します。 |
| **ログ** | `wafFlags`（オプション） | は、ルールがトリガーされたという事実をログに記録します。そうしないと、処理に影響を与えません。 wafFlags は無効です |

### WAF フラグリスト {#waf-flags-list}

The `wafFlag` プロパティには、次のものを含めることができます。

| **フラグ ID** | **フラグ名** | **説明** |
|---|---|---|
| SQLI | SQL 挿入 | SQL インジェクションとは、任意のデータベースクエリを実行して、アプリケーションへのアクセス権を取得したり、特権情報を取得したりする試みです。 |
| バックドア | 裏口 | バックドア信号は、共通のバックドアファイルがシステム上に存在するかどうかを判断する要求です。 |
| CMDEXE | コマンドの実行 | コマンド実行とは、ユーザ入力を介して任意のシステムコマンドを介して、ターゲットシステムを制御または損傷させる試みです。 |
| XSS | クロスサイトスクリプティング | クロスサイトスクリプティングは、悪意のある JavaScript コードを介してユーザーのアカウントや Web ブラウジングセッションをハイジャックしようとする試みです。 |
| トラバーサル | ディレクトリトラバーサル | ディレクトリ・トラバーサルとは、機密情報を取得するために、システム全体で特権を持つフォルダをナビゲートする試みです。 |
| USERAGENT | 攻撃工具 | 攻撃ツールとは、自動化されたソフトウェアを使用して、セキュリティの脆弱性を特定したり、検出された脆弱性を悪用したりすることです。 |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI 攻撃は、 [Log4Shell の脆弱性](https://en.wikipedia.org/wiki/Log4Shell) 2.16.0より前のバージョンの Log4J に存在する |
| AWS SSRF | AWS-SSRF | Server Side Request Forgery(SSRF) は、Web アプリケーションによっておこなわれたリクエストを、内部システムをターゲットにして送信しようとするリクエストです。 AWS SSRF 攻撃は、SSRF を使用してAmazon Web Services(AWS) キーを取得し、S3 バケットとそのデータにアクセスします。 |
| BHH | 不正なホップヘッダー | 不正なホップヘッダーは、不正な Transfer-Encoding(TE) ヘッダーまたは Content-Length(CL) ヘッダー、または正しい形式の TE および CL ヘッダーを通じて、HTTP スマーグの試行を示しています |
| ABNORMALPATH | 異常経路 | 「パスの異常」は、元のパスが正規化されたパス ( 例えば、 `/foo/./bar` が `/foo/bar`) |
| 圧縮 | 圧縮が検出されました | POSTリクエスト本文は圧縮されているので、検査できません。 例えば、「Content-Encoding: gzip」リクエストヘッダーが指定され、POST本文がプレーンテキストではない場合、 |
| DOUBLEENCODING | 二重エンコーディング | 二重エンコーディングは、html 文字を二重エンコーディングする方法をチェックします |
| FORCEFULLBROWSEING | 強力な参照 | 強制的な閲覧は、管理ページへのアクセスに失敗した試みです |
| NOTUTF8 | 無効なエンコーディング | 無効なエンコードにより、サーバーは悪意のある文字をリクエストから応答に変換し、サービス拒否または XSS のいずれかを引き起こす可能性があります |
| JSON-ERROR | JSON エンコーディングエラー | POST、PUT、またはPATCHのリクエスト本文。「Content-Type」リクエストヘッダー内に JSON が含まれていると指定されますが、JSON 解析エラーが含まれます。 これは、多くの場合、プログラミングエラーや、自動または悪意のある要求に関連しています。 |
| MALFORMED-DATA | リクエスト本文のデータの形式が正しくありません | 「Content-Type」リクエストヘッダーに従った形式でないPOST、PUTまたはPATCHのリクエスト本文。 例えば、「Content-Type: application/x-www-form-urlencoded」リクエストヘッダーが指定され、POST本文に json が含まれている場合、 これは、多くの場合、プログラミングエラー、自動化されたリクエスト、または悪意のあるリクエストです。 エージェント 3.2 以降が必要です。 |
| SANS | 悪意のある IP トラフィック | [SANS Internet Storm Center](https://isc.sans.edu/) 悪意のあるアクティビティに関与したと報告された IP アドレスのリスト |
| SIGSCI-IP | ネットワーク効果 | SignalSciences によってフラグ付けされた IP：決定エンジンによって悪意のあるシグナルによって IP がフラグ付けされると、その IP がすべての顧客に伝播されます。 フラグの期間中に追加のシグナルが含まれる IP アドレスからの以降の要求は、ログに記録されます。 |
| NO-CONTENT-TYPE | 「Content-Type」リクエストヘッダーがありません | 「Content-Type」リクエストヘッダーを持たないPOST、PUTまたはPATCHリクエスト。 この場合、デフォルトのアプリケーションサーバーでは「Content-Type: text/plain; charset=us-ascii」と想定する必要があります。 自動リクエストや悪意のあるリクエストの多くには、「コンテンツタイプ」が欠落している可能性があります。 |
| 能亜 | ユーザーエージェントがありません | 多くの自動リクエストや悪意のあるリクエストでは、リクエストをおこなうデバイスのタイプを識別するのを困難にするために、偽のユーザーエージェントや見つからないユーザーエージェントを使用します。 |
| TORNODE | Tor トラフィック | Tor は、ユーザーの ID を隠すソフトウェアです。 Tor トラフィックのスパイクは、攻撃者がその場所をマスクしようとしていることを示す場合があります。 |
| DATACENTER | データセンタートラフィック | データセンタートラフィックは、特定されたホスティングプロバイダから発生する非オーガニックトラフィックです。 このタイプのトラフィックは、一般に、実際のエンドユーザーと関連付けられるわけではありません。 |
| NULLBYTE | Null バイト | Null バイトは通常、リクエスト内では出現せず、リクエストの形式が正しくなく、悪意のある可能性があることを示します。 |
| IMPOSTOR | SearchBot Impostor | ボットインポスターの検索は、Googleまたは Bing の検索ボットのフリをしているが、正当ではない人です。 は、単独での応答に依存しませんが、最初にクラウドで解決する必要があるので、事前ルールで使用しないでください。 |
| PRIVATEFILE | プライベートファイル | プライベートファイルは、通常、Apache などの本質上機密です `.htaccess` 機密情報を漏洩する可能性のあるファイル、または設定ファイル |
| スキャナ | スキャナ | 一般的なスキャンサービスとツールを特定します。 |
| RESPONSESPLIT | HTTP 応答分割 | HTTP 応答にヘッダーを挿入するために、アプリケーションへの入力として CRLF 文字が送信されるタイミングを識別します |
| XML-ERROR | XML エンコーディングエラー | POST、PUT、またはPATCHのリクエスト本文。「Content-Type」リクエストヘッダー内に XML を含むと指定されますが、XML 解析エラーが含まれます。 これは、多くの場合、プログラミングエラーや、自動または悪意のある要求に関連しています。 |

## 検討事項 {#considerations}

* 2 つの競合するルールが作成された場合、許可ルールが常にブロックルールより優先されます。 例えば、特定のパスをブロックするルールと、特定の IP アドレスを 1 つ許可するルールを作成した場合、ブロックされたパス上のその IP アドレスからのリクエストが許可されます。

* ルールが一致し、ブロックされた場合、CDN は次の応答を返します。 `406` リターンコード。

* 設定ファイルには、Git リポジトリにアクセスできるすべてのユーザーが読み取れるので、シークレットを含めないでください。

## ルールの例 {#examples}

以下にいくつかのルールの例を示します。 詳しくは、 [レート制限セクション](#rules-with-rate-limits) さらに下に、レート制限の例を示します。

**例 1**

このルールは、IP 192.168.1.1 からの要求をブロックします。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
     rules:
       - name: "block-request-from-ip"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
         action:
           type: block
```

**例 2**

このルールは、パスに対する要求をブロックします `/helloworld` Chrome を含むユーザーエージェントを使用して公開時：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
     rules:
       - name: "block-request-from-chrome-on-path-helloworld-for-publish-tier"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
           allOf:
            - { reqProperty: path, equals: /helloworld }
            - { reqProperty: tier, equals: publish }
            - { reqHeader: user-agent, matches: '.*Chrome.*'  }
           action:
             type: block
```

**例 3**

このルールは、クエリパラメーターを含むリクエストをブロックします `foo`ですが、IP 192.168.1.1 からのすべてのリクエストを許可します。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when: { queryParam: url-param, equals: foo }
        action:
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action:
          type: allow
```

**例 4**

このルールは、パス/block-me への要求をブロックし、SQLI または XSS パターンに一致するすべての要求をブロックします。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

**例 4**

このルールは、OFAC 国へのアクセスをブロックします。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: block-ofac-countries
        when:
          allOf:
            - { reqProperty: tier, equals: publish }
            - reqProperty: clientCountry
              in:
                - SY
                - BY
                - MM
                - KP
                - IQ
                - CD
                - SD
                - IR
                - LR
                - ZW
                - CU
                - CI
        action: block
```

## レート制限付きルール {#rules-with-rate-limits}

時間の経過と共に一致が特定のレートを超える場合にのみ、ルールに一致するトラフィックをブロックすることが望ましいことがあります。 の値の設定 `rateLimit` プロパティは、ルール条件に一致する要求の割合を制限します。

### rateLimit の構造 {#ratelimit-structure}

| **プロパティ** | **タイプ** | **デフォルト** | **意味** |
|---|---|---|---|
| 制限 | 10 ～ 10000の整数 | 必須 | ルールがトリガーされる 1 秒あたりのリクエスト数です。 |
| window | integer enum: 1、10 または 60 | 10 | リクエスト率が計算されるサンプリングウィンドウ（秒）。 |
| 違約金 | 60 ～ 3600 の整数 | 300（5 分） | 一致するリクエストがブロックされる期間（秒単位）（最も近い分に丸められます）。 |
| groupBy | 配列[ゲッター] | なし | レートリミッターカウンターは、一連の要求プロパティ（clientIp など）によって集計されます。 |

### 例 {#ratelimiting-examples}

**例 1**

このルールは、過去 60 秒で 100 req/sec を超えた場合、5m のクライアントをブロックします。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    - name: limit-requests-client-ip
      when:
        reqProperty: path
        like: '*'
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: block
```

**例 2**

過去 60 秒で 100 req/sec を超えた場合に、パス/critical/resource で 60 秒に対する要求をブロックします。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when: { reqProperty: path, equals: /critical/resource }
        action:
          type: block
        rateLimit: { limit: 100, window: 60, penalty: 60 }
```

## CDN ログ {#cdn-logs}

AEM as a Cloud Serviceは CDN ログへのアクセスを提供します。CDN ログは、キャッシュヒット率の最適化や、CDN および WAF ルールの設定などの使用例に役立ちます。 CDN ログは Cloud Manager に表示されます **ログをダウンロード** ダイアログが表示されます。

「rules」プロパティは、一致するトラフィックフィルタールールを示し、次のパターンを持ちます。

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

例：

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

ルールは、次のように動作します。

* 一致するルールの顧客宣言ルール名は、matches 属性に表示されます。
* action 属性は、ルールがブロック、許可またはログの影響を与えたかどうかを詳しく説明します。
* WAF がライセンスされ、有効になっている場合、waf 属性には、設定に waf ルールがリストされているかどうかに関係なく、検出された waf ルール（SQLI など。これは顧客宣言名とは独立していることに注意してください）がリストされます。
* 一致する顧客宣言ルールがなく、一致する waf ルールがない場合、rules 属性プロパティは空白になります。

一般に、一致するルールは、CDN ヒット、パス、ミスのどれであるかに関係なく、CDN へのすべてのリクエストのログエントリに表示されます。 ただし、WAF ルールは、CDN のミスまたは合格と見なされる CDN へのリクエストに対してのみログエントリに表示されますが、CDN のヒットには表示されません。

次の例に、cdn.yaml と 2 つの CDN ログエントリの例を示します。


```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS ]
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/block-me",
"method": "GET",
"res_ctype": "",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=path-rule,action=blocked"
}
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"rid": "974e67f6",
"host": "example.com",
"url": "/?sqli=%27%29%20UNION%20ALL%20SELECT%20NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--%20fAPK",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

### ログ形式 {#cdn-log-format}

以下に、CDN ログで使用されるフィールド名の一覧と簡単な説明を示します。

| **フィールド名** | **説明** |
|---|---|
| *timestamp* | TLS の終了後にリクエストが開始した時刻。 |
| *tfb* | の略称 *最初のバイトまでの時間*. リクエストが開始してから、応答本文がストリーミングを開始するまでの時間間隔です。 |
| *cli_ip* | クライアントの IP アドレス。 |
| *cli_country* | 2 文字 [ISO 3166-1](https://ja.wikipedia.org/wiki/ISO_3166-1) 顧客の国コードの alpha-2。 |
| *rid* | リクエストを一意に識別するために使用されるリクエストヘッダーの値。 |
| *req_ua* | 特定の HTTP リクエストを実行するユーザーエージェントです。 |
| *host* | リクエストが意図されている権限。 |
| *URL* | クエリパラメーターを含む完全パス。 |
| *メソッド* | 「GET」や「POST」など、クライアントによって送信される HTTP メソッド。 |
| *res_ctype* | リソースの元のメディアタイプを示すために使用される Content-Type です。 |
| *cache* | キャッシュの状態。 指定できる値は、HIT、MISS、PASS です。 |
| *status* | HTTP ステータスコード（整数値）。 |
| *res_age* | 応答が（すべてのノードで）キャッシュされた時間（秒）。 |
| *ポップ* | CDN キャッシュサーバーのデータセンター。 |
| *rules* | 一致するルールの名前。<br><br>また、一致がブロックになったかどうかも示します。 <br><br>例：`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`&quot;<br><br>一致するルールがない場合は空です。 |
