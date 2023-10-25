---
title: WAF ルールを含むトラフィックフィルタールール
description: Web Application Firewall(WAF) ルールを含むトラフィックフィルタールールの設定
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: 221f6df73fe660c6f8dbf79affdccdd081ad3906
workflow-type: tm+mt
source-wordcount: '4210'
ht-degree: 1%

---


# WAF ルールを含むトラフィックフィルタールール {#traffic-filter-rules-including-waf-rules}

>[!NOTE]
>
>この機能は、まだ一般には利用できません。 継続中のアーリーアダプタープログラムに参加するには、E メールを送信します。 **aemcs-waf-adopter@adobe.com**（組織の名前や機能への関心に関するコンテキストを含む）

トラフィックフィルタールールを使用して、CDN レイヤーでリクエストをブロックまたは許可できます。これは、次のようなシナリオで役立つ場合があります。

* 新しいサイトが公開される前に、特定のドメインへのアクセスを社内トラフィックに制限する
* ボリューム DDoS 攻撃の影響を受けにくくするためのレート制限の設定
* 悪意のある IP アドレスがページのターゲティングから除外されるのを防ぐ

これらのトラフィックフィルタールールの一部は、AEMのas a Cloud ServiceサイトおよびFormsのすべてのお客様が利用できます。 主に、IP、ホスト名、パス、ユーザーエージェントなど、リクエストのプロパティとリクエストヘッダーで動作します。

トラフィックフィルタ規則のサブカテゴリには、拡張セキュリティライセンスまたは WAF-DoS 保護セキュリティライセンスが必要です。 これらの強力なルールは、WAF(Web Application Firewall) トラフィックフィルタールール（または WAF ルール）と呼ばれ、 [WAF フラグ](#waf-flags-list) この記事で後述。 Sites およびFormsのお客様は、この高度な機能のライセンスについて詳しくは、Adobeのアカウントチームにお問い合わせください。

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
* **チュートリアル：** ダッシュボードツールを使用して適切なルールを宣言する方法など、機能に関する実用的な知識。
<!-- About the tutorial: sets the context for a linked tutorial, which gives you practical knowledge about the feature, including how to use dashboard tooling to declare the right rules. -->

## トラフィック保護の概要 {#traffic-protection-overview}

現在のデジタル状況では、悪意のあるトラフィックが常に存在する脅威です。 アドビは、リスクの重大性を認識し、お客様のアプリケーションを保護し、発生時の攻撃を軽減するためのいくつかのアプローチを提供します。

エッジでは、Adobeが管理する CDN は、フラッド攻撃や反射/増幅攻撃を含む、ネットワーク層（レイヤ 3 およびレイヤ 4）での DDoS 攻撃を吸収します。

デフォルトでは、Adobeは、特定のしきい値を超えた予期せぬ高トラフィックのバーストによるパフォーマンスの低下を防ぐための対策を講じています。 サイトの可用性に影響を与える DDoS 攻撃が発生した場合、Adobeのオペレーションチームに警告が表示され、軽減策が講じられます。

お客様は、コンテンツ配信フローの様々なレイヤーでルールを設定することで、アプリケーションレイヤー攻撃（レイヤー 7）を軽減するための積極的な対策を講じることができます。

例えば、Apache レイヤーでは、お客様が [dispatcher モジュール](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-access-to-content-filter) または [ModSecurity](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection.html?lang=en) 特定のコンテンツへのアクセスを制限する場合。

また、この記事で説明するように、トラフィックフィルタールールは、Cloud Manager の設定パイプラインを使用して CDN にデプロイできます。 IP アドレス、パス、ヘッダーなどのプロパティに基づくトラフィックリクエストベースのトラフィックフィルタールールに加えて、お客様は、WAF ルールと呼ばれるトラフィックフィルタールールの強力なサブカテゴリをライセンスできます。

## 推奨プロセス {#suggested-process}

適切なトラフィックフィルタールールを検討するための、エンドツーエンドで推奨される概要プロセスを次に示します。

1. 実稼動以外の設定パイプラインと実稼動以外の設定パイプラインを設定します ( [設定](#setup) 」セクションに入力します。
1. WAF トラフィックフィルタールールのサブカテゴリをライセンスしたお客様は、Cloud Manager でそのサブカテゴリを有効にする必要があります。
1. このチュートリアルを読んで、ライセンスを取得している場合は WAF ルールを含むトラフィックフィルタールールの使用方法を具体的に理解してみてください。 このチュートリアルでは、開発環境にルールをデプロイし、悪意のあるトラフィックをシミュレートし、をダウンロードする方法について説明します。 [CDN ログ](#cdn-logs)を作成し、それらを分析します。 [ダッシュボードツール](#dashboard-tooling).
1. 推奨される初期ルールを次の場所にコピーします。 `cdn.yaml` ログモードで設定を実稼動環境にデプロイします。
1. トラフィックを収集した後、 [ダッシュボードツール](#dashboard-tooling) 一致があるかどうかを確認する 偽陽性を探し、必要な調整を行い、最終的にブロックモードでデフォルトのルールを有効にします。
1. CDN ログの分析に基づくカスタムルールを追加します。まず、開発環境でトラフィックをシミュレートしてテストし、次にログモードでステージング環境と実稼動環境にデプロイしてから、ブロックモードにします。
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

1. WAF ルールを設定するには、新しいプログラムシナリオと既存のプログラムシナリオの両方で、以下の説明に従って、Cloud Manager で WAF を有効にする必要があります。 WAF 用に別のライセンスを購入する必要があります。

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

このルールは、パスへの要求をブロックします `/block-me`、およびは、 `SQLI` または `XSS` パターン。 この例には、 `SQLI` および `XSS` [WAF フラグ](#waf-flags-list)：別のライセンスが必要です。

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

時間の経過と共に一致が特定のレートを超える場合にのみ、ルールに一致するトラフィックをブロックすることが望ましいことがあります。 の値の設定 `rateLimit` プロパティは、ルール条件に一致する要求の割合を制限します。

レート制限ルールは、WAF フラグを参照できません。 Sites およびFormsのすべてのお客様が利用できます。

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

AEM as a Cloud Serviceは CDN ログへのアクセスを提供します。CDN ログは、キャッシュヒット率の最適化や、CDN および WAF ルールの設定などの使用例に役立ちます。 CDN ログは Cloud Manager に表示されます **ログをダウンロード** ダイアログが表示されます。

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

* 一致するルールの顧客宣言ルール名は、matches 属性に表示されます。
* action 属性は、ルールがブロック、許可またはログに影響したかどうかを詳しく説明します。
* WAF がライセンスされ、有効になっている場合、waf 属性には、設定に waf ルールが含まれているかどうかに関係なく、検出された waf ルール（SQLI など。これは顧客宣言名とは独立した名前です）がリストされます。
* 一致する顧客宣言ルールがなく、一致する waf ルールがない場合、rules 属性プロパティは空白になります。

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

## チュートリアル {#tutorial}

Adobeは、ダッシュボードツールをコンピューターにダウンロードして、Cloud Manager を通じてダウンロードされた CDN ログを取り込むためのメカニズムを提供します。 このツールを使用すると、トラフィックを分析して、WAF ルールを含む、宣言する適切なトラフィックフィルタールールを考案できます。 この節では、まず、開発環境でのダッシュボードツールに慣れるための手順と、その知識を活用して実稼動環境でルールを作成する方法に関するガイダンスを提供します。

ダッシュボードツールは、 [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) GitHub リポジトリ。


### ダッシュボードツールの概要 {#dashboard-getting-familiar}

1. 開発環境に関連付けられた Cloud Manager の非実稼動環境設定パイプラインを作成します。 最初に、 **デプロイメントパイプライン** オプション。 次に、 **ターゲットのデプロイメント**、設定、リポジトリ、Git ブランチの順に選択し、コードの場所を/config に設定します。

   ![実稼動以外のパイプラインを追加してデプロイメントを選択](/help/security/assets/waf-select-pipeline1.png)

   ![実稼動以外のパイプラインを追加してターゲットを選択](/help/security/assets/waf-select-pipeline2.png)

[実稼動以外のパイプラインの設定の詳細については、このドキュメントを参照してください。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

1. ワークスペースで、ルートレベルにフォルダー設定を作成し、という名前のファイルを追加します。 `cdn.yaml`を使用する場合は、ブロックモードではなくログモードで設定し、シンプルなルールを宣言します。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: log
```

1. 変更をコミットしてプッシュし、設定パイプラインを使用して設定をデプロイします。

   ![設定パイプラインを実行](/help/security/assets/waf-run-pipeline.png)

1. 設定がデプロイされたら、にアクセスしてみます。 `https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me` web ブラウザーを使用するか、以下の curl コマンドを使用します。 そのページは存在しないので、404 エラーページが表示されます。

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. Cloud Manager から CDN ログをダウンロードし、ルールが期待どおりに一致し、ルール名と一致するルールプロパティを持つことを検証します。

   ```
   "rules": "match=log-rule-example"
   ```

   ![ログをダウンロードを選択](/help/security/assets/waf-download-logs1.png)

   ![ログをダウンロード](/help/security/assets/waf-download-logs2.png)

1. ダッシュボードツールを使用して Docker イメージを読み込み、README に従って CDN ログを取り込みます。 次のスクリーンショットに示すように、適切な期間、適切な環境および適切なフィルターを選択します。

   ![ダッシュボードから時間を選択](/help/security/assets/dashboard-select-time.png)

   ![ダッシュボードから環境を選択](/help/security/assets/dashboard-select-env.png)

1. 適切なフィルターを適用すると、ダッシュボードに期待されたデータが読み込まれていることを確認できます。 以下のスクリーンショットでは、ルール log-rule-example が、Web ブラウザーと curl を使用して、アイルランドにある同じ IP で過去 2 時間に 3 回トリガーされています。

   ![開発ダッシュボードデータの表示](/help/security/assets/dashboard-see-data-logmode.png)
   ![開発ダッシュボードのデータウィジェットを表示する](/help/security/assets/dashboard-see-data-logmode2.png)

1. 次に、cdn.yaml を変更してルールをブロックモードにし、ページが期待どおりにブロックされるようにします。 次に、前の手順に従って、設定パイプラインをコミット、プッシュ、トリガーします。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: block
```

1. 設定がデプロイされたら、にアクセスしてみます。 `https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me` web ブラウザーを使用するか、以下の curl コマンドを使用します。 406 エラーページが表示され、リクエストがブロックされたことを示します。

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. もう一度、CDN ログを Cloud Manager でダウンロードし（注意：新しいリクエストが CDN ログに公開されるまでに最大 5 分かかります）、前の手順と同様に、ダッシュボードツールに読み込みます。 完了したら、ダッシュボードを更新します。 以下のスクリーンショットに示すように、はに対する要求です。 `/log/me` は、ルールによってブロックされています。

   ![製品ダッシュボードデータの表示](/help/security/assets/dashboard-see-data-blockmode.png)
   ![製品ダッシュボードデータの表示](/help/security/assets/dashboard-see-data-blockmode2.png)

1. WAF トラフィックフィルタを有効にしている場合（GA の後に追加のライセンスが必要になる）、WAF トラフィックフィルタルールを使用してログモードで繰り返し、ルールを展開します。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: log-waf-flags
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
```

1. 次のようなツールを使用 [nikto](https://github.com/sullo/nikto/tree/master) をクリックして、一致するリクエストを生成します。 以下のコマンドは、1 分以内に約 550 件の悪意のあるリクエストを送信します。

   ```
   ./nikto.pl -useragent "MyAgent (Demo/1.0)" -D V -Tuning 9 -ssl -h https://publish-pXXXXX-eYYYYY.adobeaemcloud.com
   ```

1. Cloud Manager から CDN ログをダウンロードし（表示には最大 5 分かかる場合があります）、一致する宣言済みルールと WAF フラグの両方が表示されることを検証します。

   ご覧のように、Nikto が作成したリクエストのいくつかは、WAF によって悪意のあるリクエストとしてフラグ付けされています。 Nikto は CMDEXE、SQLI、NULLBYTE の脆弱性を悪用しようとしたのがわかります。 Nikto を使用して、アクションをログからブロックに変更し、スキャンを再トリガーした場合、以前にフラグを設定したすべてのリクエストが今回ブロックされます。

   ![WAF データを表示](/help/security/assets/dashboard-see-data-waf.png)


   リクエストがいずれかの WAF フラグと一致する場合は、宣言されたルールの一部でなくても、それらの WAF フラグが表示されます。これにより、まだ一致ルールを宣言していない、悪意のある新しいトラフィックが常に認識されます。 次に例を示します。

   ```
   "rules": "match=log-waf-flags,waf=SQLI,action=blocked"
   ```

1. ログモードで、レート制限を使用するルールで繰り返します。 設定パイプラインをコミット、プッシュ、トリガーして、設定を適用します。

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
          limit: 10
          window: 1
          penalty: 60
          groupBy:
            - reqProperty: clientIp
        action: log
```

1. 次のようなツールを使用 [ベジータ](https://github.com/tsenart/vegeta) トラフィックを生成します。

   ```
   echo "GET https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com" | vegeta attack -duration=5s | tee results.bin | vegeta report
   ```

1. ツールを実行した後、CDN ログをダウンロードし、ダッシュボードに取り込んで、レートリミッタールールがトリガーされたことを確認できます

   ![WAF データを表示](/help/security/assets/waf-dashboard-ratelimiter-1.png)

   ![WAF データを表示](/help/security/assets/waf-dashboard-ratelimiter-2.png)

   ルールを確認できるように **limit-requests-client-ip** がトリガーされました。

   これで、トラフィックフィルタールールの動作について理解できたので、実稼動環境に移行できます。

### 実稼動環境へのルールのデプロイ {#dashboard-prod-env}

最初は、ルールをログモードで宣言して、偽陽性がないこと、つまり正当なトラフィックが誤ってブロックされることを検証します。

1. 実稼動環境に関連付けられた実稼動設定パイプラインを作成します。

1. 以下の推奨ルールを cdn.yaml にコピーします。 Web サイトのライブトラフィックに固有の特性に基づいてルールを変更することもできます。 設定パイプラインをコミット、プッシュ、トリガーします。 ルールがログモードになっていることを確認します。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
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
    # Enable recommended WAF protections (only works if WAF is enabled for your environment)
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
    # Disable protection against CMDEXE on /bin
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

1. 悪意のあるトラフィックをブロックするためのルールを追加します。 例えば、サイトを攻撃している特定の IP などです。

1. サイトのトラフィック量に応じて、数分、数時間または数日後に、Cloud Manager から CDN ログをダウンロードし、ダッシュボードで分析します。

1. 以下に、考慮事項を示します。
   1. 宣言されたルールに一致するトラフィックはグラフとリクエストログに表示されるので、宣言されたルールがトリガーされているかどうかを簡単に確認できます。
   1. WAF フラグに一致するトラフィックは、ルールにログインしていなくても、グラフやリクエストログに表示されます。 これにより、悪意のあるトラフィックが新たに発生した可能性が常に認識され、必要に応じて新しいルールを作成できます。 宣言されたルールに反映されていない WAF フラグを見て、宣言を検討してください。
   1. 一致ルールについて、リクエストログで偽陽性を調べ、それらをルールから除外できるかどうかを確認します。 例えば、特定のパスに対してのみ偽陽性である可能性があります。

1. 適切なルールを設定してモードをブロックし、追加のルールを追加することを検討します。 より多くのトラフィックを分析する際には、一部のルールをログモードのままにしておく必要がある可能性があります。

1. 設定を再デプロイします。

1. 繰り返し処理され、ダッシュボードを頻繁に分析します。

