---
title: WAF ルールを含むトラフィックフィルタールール
description: Web Application Firewall(WAF) ルールを含むトラフィックフィルタールールの設定
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: 1683819d4f11d4503aa0d218ecff6375fc5c54d1
workflow-type: tm+mt
source-wordcount: '3312'
ht-degree: 2%

---


# WAF ルールを含むトラフィックフィルタールール {#traffic-filter-rules-including-waf-rules}

>[!NOTE]
>この機能は、11 月にステージング環境と実稼動環境へ段階的に展開され、まもなく開発環境で使用できるようになる予定です。 ステージ上および実稼動環境での事前アクセスを電子メールで要求することができます **aemcs-waf-adopter@adobe.com**.

トラフィックフィルタールールを使用して、CDN レイヤーでリクエストをブロックまたは許可できます。これは、次のようなシナリオで役立つ場合があります。

* 新しいサイトが公開される前に、特定のドメインへのアクセスを社内トラフィックに制限する
* ボリューム DoS 攻撃の影響を受けにくくするためのレート制限の設定
* 悪意のある IP アドレスがページのターゲティングから除外されるのを防ぐ

これらのトラフィックフィルタールールのほとんどは、AEMのas a Cloud ServiceサイトおよびFormsのすべてのお客様が利用できます。 主に、IP、ホスト名、パス、ユーザーエージェントなど、リクエストのプロパティとリクエストヘッダーで動作します。

トラフィックフィルター規則のサブカテゴリには、拡張セキュリティライセンスまたは WAF-DoS 保護ライセンスが必要で、今年中に利用可能になる予定です。 これらの強力なルールは、WAF(Web Application Firewall) トラフィックフィルタールール（または WAF ルール）と呼ばれ、 [WAF フラグ](#waf-flags-list) この記事で後述。

トラフィックフィルタールールは、Cloud Manager 設定パイプラインを通じて、実稼動（サンドボックス以外）プログラムの開発、ステージ、実稼動環境のタイプにデプロイできます。 RDE のサポートは今後提供される予定です。

## この記事の編成方法 {#how-organized}

この記事は、次の節で構成されています。

* **トラフィック保護の概要：** 悪意のあるトラフィックから保護される方法を説明します。
* **ルールを設定するための推奨プロセス：** Web サイトを保護するための高度な方法についてお読みください。
* **設定：** 高度な WAF ルールを含むトラフィックフィルタールールの設定、設定、デプロイ方法について説明します。
* **ルール構文：** トラフィックフィルタールールを `cdn.yaml` 設定ファイル。 これには、すべての Sites およびFormsの顧客が利用できるトラフィックフィルタールールと、その機能をライセンスするユーザー向けの WAF ルールのサブカテゴリの両方が含まれます。
* **ルールの例：** 宣言されたルールの例を参照して、作業を進めてください。
* **レート制限ルール：** レート制限ルールを使用して、大量の攻撃からサイトを保護する方法を説明します。
* **CDN ログ：** トラフィックに一致する宣言済みルールと WAF フラグを確認します。
* **ダッシュボードツール：** CDN ログを分析して、新しいトラフィックフィルタールールを生成します。
* **推奨されるスタータールール：** 使用を開始するための一連のルール。
* **チュートリアル：** ダッシュボードツールを使用して適切なルールを宣言する方法など、機能に関する実用的な知識。

フィードバックをいただくか、E メールでトラフィックフィルタールールに関するご質問をお寄せください **aemcs-waf-adopter@adobe.com**.

## トラフィック保護の概要 {#traffic-protection-overview}

現在のデジタル状況では、悪意のあるトラフィックが常に存在する脅威です。 アドビは、リスクの重大性を認識し、お客様のアプリケーションを保護し、発生時の攻撃を軽減するためのいくつかのアプローチを提供します。

エッジでは、Adobeが管理する CDN は、フラッド攻撃や反射/増幅攻撃を含む、ネットワーク層（レイヤ 3 およびレイヤ 4）での DoS 攻撃を吸収します。

デフォルトでは、Adobeは、特定のしきい値を超えた予期せぬ高トラフィックのバーストによるパフォーマンスの低下を防ぐための対策を講じています。 サイトの可用性に影響を与える DoS 攻撃が発生した場合、Adobeのオペレーションチームはアラートを受け、軽減策を講じます。

お客様は、コンテンツ配信フローの様々なレイヤーでルールを設定することで、アプリケーションレイヤー攻撃（レイヤー 7）を軽減するための積極的な対策を講じることができます。

例えば、Apache レイヤーでは、お客様が [dispatcher モジュール](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-access-to-content-filter) または [ModSecurity](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection.html?lang=en) 特定のコンテンツへのアクセスを制限する場合。

また、この記事で説明するように、トラフィックフィルタールールは、Cloud Manager の設定パイプラインを使用して、Adobe管理 CDN にデプロイできます。 IP アドレス、パス、ヘッダーなどのプロパティに基づくトラフィックフィルタールールや、レート制限の設定に基づくルールに加えて、お客様は、WAF ルールと呼ばれる強力なトラフィックフィルタールールのサブカテゴリをライセンスできます。

## 推奨プロセス {#suggested-process}

適切なトラフィックフィルタールールを検討するための、エンドツーエンドで推奨される概要プロセスを次に示します。

1. 実稼動以外および実稼動以外の設定パイプラインを設定します。詳しくは、 [設定](#setup) 」セクションに入力します。
1. WAF トラフィックフィルタールールのサブカテゴリをライセンスしたお客様は、Cloud Manager でそのサブカテゴリを有効にする必要があります。
1. このチュートリアルを読んで、ライセンスを取得している場合は WAF ルールを含むトラフィックフィルタールールの使用方法を具体的に理解してみてください。 このチュートリアルでは、開発環境にルールをデプロイし、悪意のあるトラフィックをシミュレートし、をダウンロードする方法について説明します。 [CDN ログ](#cdn-logs)を作成し、それらを分析します。 [ダッシュボードツール](#dashboard-tooling).
1. 推奨されるスタータールールを次にコピーします。 `cdn.yaml` ログモードで実稼動環境に設定をデプロイします。
1. トラフィックを収集した後、 [ダッシュボードツール](#dashboard-tooling) 一致があるかどうかを確認する 偽陽性を探し、必要な調整を行い、最終的にはブロックモードでスタータールールを有効にします。
1. CDN ログの分析に基づくカスタムルールを追加します。まず、開発環境でトラフィックをシミュレートしてテストしてから、ログモードでステージング環境と実稼動環境にデプロイしてから、ブロックモードにします。
1. トラフィックを継続的に監視し、脅威の状況が変化するにつれてルールに変更を加えます。

## セットアップ {#setup}

1. まず、Git のプロジェクトの最上位フォルダーに次のフォルダーとファイル構造を作成します。

   ```
   config/
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
       # Block simple path
       - name: block-path
         when:
           allOf:
             - reqProperty: tier
               matches: "author|publish"
             - reqProperty: path
               equals: '/block/me'
         action: block
   ```

The `kind` パラメーターは次のように設定する必要があります： `CDN` のバージョンは、現在のスキーマのバージョンに設定する必要があります。 `1`. 後述の例を参照してください。


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. WAF ルールのライセンスが必要な場合は、新規および既存のプログラムシナリオで、以下の説明に従って、Cloud Manager でこの機能を有効にする必要があります。

   1. 新しいプログラムで WAF を設定するには、 **WAF-DDOS 保護** のチェックボックス **セキュリティ** タブ [実稼働プログラムを追加します。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

   1. 既存のプログラムで WAF を設定するには、次の手順に従います。 [プログラムの編集](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) また、 **セキュリティ** 「 」タブの「 」チェックボックスをオフまたはオンにします。 **WAF-DDOS** オプションをいつでも使用できます。

1. RDE 以外の環境タイプの場合は、Cloud Manager でターゲット化したデプロイメント設定パイプラインを作成します。

   * [実稼動パイプラインについては、このドキュメントを参照してください。](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [実稼動以外のパイプラインについては、このドキュメントを参照してください。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

RDE の場合は、コマンドラインが使用されますが、現時点では RDE はサポートされていません。

## トラフィックフィルタールールの構文 {#rules-syntax}

次の項目を設定できます。 `traffic filter rules` を使用して、IP、ユーザーエージェント、リクエストヘッダー、ホスト名、地域、url などのパターンを照合します。

拡張セキュリティまたは WAF-DoS 保護セキュリティの機能をライセンスするお客様は、トラフィックフィルタルールの特別なカテゴリを設定することもできます。 `WAF traffic filter rules` （または WAF ルールは短く）1 つ以上の [WAF フラグ](#waf-flags-list).

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

トラフィックフィルタールールの形式 ( `cdn.yaml` ファイルについては、以下で説明します。 参照 [その他の例](#examples) 後の節では、 [レート制限ルール](#rate-limit-rules).


| **プロパティ** | **ほとんどのトラフィックフィルタールール** | **WAF トラフィックフィルタルール** | **タイプ** | **デフォルト値** | **説明** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | ルール名（64 文字）（英数字と — のみを含めることができます） |
| when | X | X | `Condition` | - | 基本的な構造は次のとおりです。<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[条件構造の構文を参照してください。](#condition-structure) 以下では、ゲッター、述語および複数の条件の組み合わせ方法について説明します。 |
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
| reqCookie | `string` | 指定された名前の Cookie を返します |
| postParam | `string` | 本文から指定された名前のパラメータを返します。 本文がコンテンツタイプの場合にのみ機能します `application/x-www-form-urlencoded` |

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
| **は存在しています** | `boolean` | true に設定し、プロパティが存在する場合、または false に設定し、プロパティが存在しない場合。 |

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

The `wafFlags` プロパティは、ライセンス可能な WAF トラフィックフィルタールールで使用でき、次を参照できます。

| **フラグ ID** | **フラグ名** | **説明** |
|---|---|---|
| SQLI | SQL 挿入 | SQL インジェクションとは、任意のデータベースクエリを実行して、アプリケーションへのアクセス権を取得したり、特権情報を取得したりする試みです。 |
| バックドア | 裏口 | バックドア信号は、共通のバックドアファイルがシステム上に存在するかどうかを判断する要求です。 |
| CMDEXE | コマンドの実行 | コマンド実行とは、ユーザ入力を介して任意のシステムコマンドを介して、ターゲットシステムを制御または損傷させる試みです。 |
| XSS | クロスサイトスクリプティング | クロスサイトスクリプティングは、悪意のある JavaScript コードを介してユーザーのアカウントや Web ブラウジングセッションをハイジャックしようとする試みです。 |
| トラバーサル | ディレクトリトラバーサル | ディレクトリ・トラバーサルとは、機密情報を取得するために、システム全体で特権を持つフォルダをナビゲートする試みです。 |
| USERAGENT | 攻撃工具 | 攻撃ツールとは、自動化されたソフトウェアを使用して、セキュリティの脆弱性を特定したり、検出された脆弱性を悪用したりすることです。 |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI 攻撃は、 [Log4Shell の脆弱性](https://en.wikipedia.org/wiki/Log4Shell) 2.16.0より前のバージョンの Log4J に存在する |
| BHH | 不正なホップヘッダー | 不正なホップヘッダーは、不正な Transfer-Encoding(TE) ヘッダーまたは Content-Length(CL) ヘッダー、または正しい形式の TE および CL ヘッダーを通じて、HTTP スマーグの試行を示しています |
| ABNORMALPATH | 異常経路 | 「パスの異常」は、元のパスが正規化されたパス ( 例えば、 `/foo/./bar` が `/foo/bar`) |
| DOUBLEENCODING | 二重エンコーディング | 二重エンコーディングは、html 文字を二重エンコーディングする方法をチェックします |
| NOTUTF8 | 無効なエンコーディング | 無効なエンコードにより、サーバーは悪意のある文字をリクエストから応答に変換し、サービス拒否または XSS のいずれかを引き起こす可能性があります |
| JSON-ERROR | JSON エンコーディングエラー | POST、PUT、またはPATCHのリクエスト本文。「Content-Type」リクエストヘッダー内に JSON が含まれていると指定されますが、JSON 解析エラーが含まれます。 これは、多くの場合、プログラミングエラーや、自動または悪意のある要求に関連しています。 |
| MALFORMED-DATA | リクエスト本文のデータの形式が正しくありません | 「Content-Type」リクエストヘッダーに従った形式でないPOST、PUTまたはPATCHのリクエスト本文。 例えば、「Content-Type: application/x-www-form-urlencoded」リクエストヘッダーが指定され、POST本文に json が含まれている場合、 これは、多くの場合、プログラミングエラー、自動化されたリクエスト、または悪意のあるリクエストです。 エージェント 3.2 以降が必要です。 |
| SANS | 悪意のある IP トラフィック | [SANS Internet Storm Center](https://isc.sans.edu/) 悪意のあるアクティビティに関与したと報告された IP アドレスのリスト |
| SIGSCI-IP | ネットワーク効果 | SignalSciences によってフラグ付けされた IP：決定エンジンによって悪意のあるシグナルによって IP がフラグ付けされると、その IP がすべての顧客に伝播されます。 フラグの期間中に追加のシグナルが含まれる IP アドレスからの以降の要求は、ログに記録されます。 |
| NO-CONTENT-TYPE | 「Content-Type」リクエストヘッダーがありません | 「Content-Type」リクエストヘッダーを持たないPOST、PUTまたはPATCHリクエスト。 この場合、デフォルトのアプリケーションサーバーでは「Content-Type: text/plain; charset=us-ascii」と想定する必要があります。 自動リクエストや悪意のあるリクエストの多くには、「コンテンツタイプ」が欠落している可能性があります。 |
| 能亜 | ユーザーエージェントがありません | 多くの自動リクエストや悪意のあるリクエストでは、リクエストをおこなうデバイスのタイプを識別するのを困難にするために、偽のユーザーエージェントや見つからないユーザーエージェントを使用します。 |
| TORNODE | Tor トラフィック | Tor は、ユーザーの ID を隠すソフトウェアです。 Tor トラフィックのスパイクは、攻撃者がその場所をマスクしようとしていることを示す場合があります。 |
| NULLBYTE | Null バイト | Null バイトは通常、リクエスト内では出現せず、リクエストの形式が正しくなく、悪意のある可能性があることを示します。 |
| PRIVATEFILE | プライベートファイル | プライベートファイルは、通常、Apache などの本質上機密です `.htaccess` 機密情報を漏洩する可能性のあるファイル、または設定ファイル |
| スキャナ | スキャナ | 一般的なスキャンサービスとツールを特定します。 |
| RESPONSESPLIT | HTTP 応答分割 | HTTP 応答にヘッダーを挿入するために、アプリケーションへの入力として CRLF 文字が送信されるタイミングを識別します |
| XML-ERROR | XML エンコーディングエラー | POST、PUT、またはPATCHのリクエスト本文。「Content-Type」リクエストヘッダー内に XML を含むと指定されますが、XML 解析エラーが含まれます。 これは、多くの場合、プログラミングエラーや、自動または悪意のある要求に関連しています。 |

## 検討事項 {#considerations}

* 2 つの競合するルールが作成された場合、許可ルールが常にブロックルールより優先されます。 例えば、特定のパスをブロックするルールと、特定の IP アドレスを 1 つ許可するルールを作成した場合、ブロックされたパス上のその IP アドレスからのリクエストが許可されます。

* ルールが一致し、ブロックされた場合、CDN は次の応答を返します。 `406` リターンコード。

* 設定ファイルには、Git リポジトリにアクセスできるすべてのユーザーが読み取れるので、シークレットを含めないでください。

## ルールの例 {#examples}

以下にいくつかのルールの例を示します。 詳しくは、 [レート制限セクション](#rules-with-rate-limits) さらに下に、レート制限ルールの例を示します。

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
        when:
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

このルールは、パスへの要求をブロックします `/block-me`、およびは、 `SQLI` または `XSS` パターン。 この例には、 `SQLI` および `XSS` [WAF フラグ](#waf-flags-list)を使用する場合は、個別のライセンスが必要になります。

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

**例 5**

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
            - reqProperty: tier
              matches: "author|publish"
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

## レート制限ルール {#rate-limits-rules}

特定の条件に基づく、特定の受信リクエストの速度を超える場合は、トラフィックをブロックするほうが望ましいことがあります。 の値の設定 `rateLimit` プロパティは、ルール条件に一致する要求の割合を制限します。

レート制限ルールは、WAF フラグを参照できません。 Sites およびFormsのすべてのお客様が利用できます。

レート制限は、CDN POP ごとに計算されます。 例えば、モントリオール、マイアミおよびダブリンの POP で、それぞれリクエストが 80、90、120 のトラフィック率をエクスペリエンスし、レート制限ルールが 100 の制限に設定されているとします。 この場合、ダブリンへのトラフィックのみがレート制限されます。

### rateLimit の構造 {#ratelimit-structure}

| **プロパティ** | **タイプ** | **デフォルト** | **意味** |
|---|---|---|---|
| 制限 | 10 ～ 10000の整数 | 必須 | ルールがトリガーされる 1 秒あたりのリクエスト数（CDN POP あたり）。 |
| window | integer enum: 1、10 または 60 | 10 | リクエスト率が計算されるサンプリングウィンドウ（秒）。 |
| 違約金 | 60 ～ 3600 の整数 | 300（5 分） | 一致するリクエストがブロックされる期間（秒単位）（最も近い分に丸められます）。 |
| groupBy | 配列[ゲッター] | なし | レートリミッターカウンターは、一連の要求プロパティ（clientIp など）によって集計されます。 |

### 例 {#ratelimiting-examples}

**例 1**

このルールは、最近の 60 秒で 100 req/sec（CDN POP あたり）を超える場合、5m のクライアントをブロックします。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: block
```

**例 2**

過去 60 秒で 100 req/sec （CDN POP あたり）を超えた場合に、パス/critical/resource で 60 秒に対するリクエストをブロックします。

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

AEM as a Cloud Serviceは、CDN ログへのアクセスを提供します。CDN ログは、キャッシュヒット率の最適化や、トラフィックフィルタールールの設定などの使用例に役立ちます。 CDN ログは Cloud Manager に表示されます **ログをダウンロード** ダイアログが表示されます。

CDN ログは、最大 5 分遅れる場合があります。

The `rules` プロパティは、一致するトラフィックフィルタールールを示し、次のパターンを持ちます。

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

次に例を示します。

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

ルールは、次のように動作します。

* 一致するルールの顧客宣言ルール名は、 `match` 属性。
* The `action` 属性は、ルールがブロック、許可またはログの影響を与えたかどうかを決定します。
* WAF がライセンスを受け、有効になっている場合は、 `waf` 属性は、WAF フラグがどのルールにもリストされているかどうかに関係なく、検出された WAF フラグ（SQLI など）をリストします。 これは、宣言する新しいルールの可能性に関するインサイトを提供するためです。
* 一致する顧客宣言ルールがなく、一致する waf ルールがない場合、 `rules` プロパティは空白になります。

一般に、一致するルールは、CDN ヒット、パス、ミスのどれであるかに関係なく、CDN へのすべてのリクエストのログエントリに表示されます。 ただし、WAF ルールは、CDN のミスまたは合格と見なされる CDN へのリクエストに対してのみログエントリに表示されますが、CDN のヒットには表示されません。

以下の例は、サンプルを示しています `cdn.yaml` と 2 つの CDN ログエントリを追加します。


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

## ダッシュボードツール {#dashboard-tooling}

Adobeは、ダッシュボードツールをコンピューターにダウンロードして、Cloud Manager を通じてダウンロードされた CDN ログを取り込むためのメカニズムを提供します。 このツールを使用すると、トラフィックを分析して、WAF ルールを含む、宣言する適切なトラフィックフィルタールールを考案できます。

ダッシュボードツールは、 [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) GitHub リポジトリ。

[チュートリアルを参照](#tutorial) を参照してください。

## 推奨されるスタータールール {#recommended-starter-rules}

以下の推奨ルールを `cdn.yaml` をクリックして開始します。 ログモードから開始し、トラフィックを分析し、問題が発生したら、ブロックモードに変更します。 Web サイトのライブトラフィックに固有の特性に基づいてルールを変更することもできます。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds 100 req/sec on a time window of 1sec
    - name: limit-requests-client-ip
      when:
        reqProperty: path
        like: '*'
      rateLimit:
        limit: 100
        window: 1
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    # Block requests coming from OFAC countries
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
      action: log
    # Enable recommended WAF protections (only works if WAF is licensed enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        matches: "author|publish"
      action:
        type: log
        wafFlags:
          - SANS
          - SIGSCI-IP
          - TORNODE
          - NOUA
          - SCANNER
          - USERAGENT
          - PRIVATEFILE
          - ABNORMALPATH
          - TRAVERSAL
          - NULLBYTE
          - BACKDOOR
          - LOG4J-JNDI
          - SQLI
          - XSS
          - CODEINJECTION
          - CMDEXE
          - NO-CONTENT-TYPE
          - UTF8
    # Disable protection against CMDEXE on /bin (only works if WAF is licensed enabled for your environment)
    - name: allow-cdmexe-on-root-bin
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            matches: "^/bin/.*"
      action:
        type: log
        wafFlags:
          - CMDEXE
```

## チュートリアル {#tutorial}

[チュートリアルの操作](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html) トラフィックフィルタールールに関する実用的な知識と経験を得る。

このチュートリアルでは、次の手順を説明します。

* Cloud Manager 設定パイプラインの設定
* ツールを使用して悪意のあるトラフィックをシミュレートする
* WAF ルールを含むトラフィックフィルタールールの宣言
* ダッシュボードツールを使用した結果の分析
* ベストプラクティス
