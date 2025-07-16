---
title: WAF ルールを含むトラフィックフィルタールール
description: Web アプリケーションファイアウォール（WAF）ルールを含むトラフィックフィルタールールの設定。
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
feature: Security
role: Admin
source-git-commit: c54f77a7e0a034bab5eeddcfe231973575bf13f4
workflow-type: tm+mt
source-wordcount: '4582'
ht-degree: 82%

---


# WAF ルールを含むトラフィックフィルタールール {#traffic-filter-rules-including-waf-rules}

トラフィックフィルタールールを使用して、CDN レイヤーでリクエストをブロックまたは許可できます。これは、次のようなシナリオで役立つ場合があります。

* 新しいサイトの公開前に、特定のドメインへのアクセスを社内トラフィックに制限する
* ボリューム DoS 攻撃の影響を受けにくくするようにレート制限を設定
* 悪意のある IP アドレスからページをターゲティングされるのを防止する

これらのトラフィックフィルタールールの多くは、すべてのAEM as a Cloud Service Sites およびFormsのお客様が利用できます。 *標準トラフィックフィルタールール* と呼ばれ、主にリクエストプロパティとリクエストヘッダー（IP、ホスト名、パス、ユーザーエージェントなど）に対して動作します。 標準のトラフィックフィルタールールには、トラフィックスパイクを防ぐためのレート制限ルールが含まれています。

トラフィックフィルター規則のサブカテゴリには、拡張セキュリティライセンスまたは WAF-DDoS 保護ライセンスが必要です。これらの強力なルールは、WAF（Web Application Firewall）トラフィックフィルタールール（または略して *WAF ルール）と呼ばれ* この記事で後述する [WAF フラグ ](#waf-flags-list) へのアクセス権を持ちます。

トラフィックフィルタールールは、Cloud Manager 設定パイプラインを通じて、開発環境、ステージ環境および実稼動環境のタイプにデプロイできます。設定ファイルは、コマンドラインツールを使用して迅速な開発環境（RDE）にデプロイできます。

[チュートリアルに従って](#tutorial)、この機能に関する具体的な専門知識をすばやく構築します。

>[!NOTE]
>リクエスト／応答の編集、リダイレクトの宣言、AEM 以外の接触チャネルへのプロキシ処理など、CDN でのトラフィックの設定に関連する追加オプションについては、[CDN でのトラフィックの設定](/help/implementing/dispatcher/cdn-configuring-traffic.md)の記事を参照してください。


## この記事の編成方法 {#how-organized}

この記事は、次の節で構成されています。

* **トラフィック保護の概要：**&#x200B;悪意のあるトラフィックから保護される方法を説明します。
* **ルールを設定するための推奨プロセス：** web サイトを保護する高度な方法について説明します。
* **設定：**&#x200B;高度な WAF ルールを含むトラフィックフィルタールールのセットアップ、設定、デプロイ方法について説明します。
* **ルール構文：`cdn.yaml`設定ファイルで** トラフィックフィルタールールを宣言する方法を説明します。これには、すべての Sites および Forms の顧客が利用できるトラフィックフィルタールールとその機能をライセンスするユーザー向けの WAF ルールのサブカテゴリの両方が含まれます。
* **ルールの例：**&#x200B;宣言されたルールの例を参照して、作業を進めてください。
* **レート制限ルール：**&#x200B;レート制限ルールを使用して、大量の攻撃からサイトを保護する方法を説明します。
* **トラフィックフィルタールールアラート：**&#x200B;ルールをトリガーした際に通知されるアラートを設定します。
* **接触チャネルでのトラフィックスパイクを示すデフォルトアラート：** DDoS 攻撃を示すトラフィックの急増が接触チャネルで発生した場合に通知を受信します。
* **CDN ログ：**&#x200B;トラフィックに一致する宣言済みルールと WAF フラグを確認します。
* **ダッシュボードツール：** CDN ログを分析して、新しいトラフィックフィルタールールを作成する方法を説明します。
* **推奨されるスタータールール：**&#x200B;使用を開始するための一連のルール。
* **チュートリアル：**&#x200B;ダッシュボードツールを使用して適切なルールを宣言する方法など、機能に関する実用的な知識を説明します。

## トラフィック保護の概要 {#traffic-protection-overview}

現在のデジタル環境では、悪意のあるトラフィックの脅威は常に存在します。アドビは、リスクの重大性を認識し、お客様のアプリケーションを保護し、攻撃の発生率を軽減するためのいくつかのアプローチを提供します。

エッジでは、アドビが管理する CDN が、フラッド攻撃やリフレクション攻撃／増幅攻撃を含む、ネットワークレイヤー（レイヤー 3 およびレイヤー 4）での DoS 攻撃を吸収します。

デフォルトでは、アドビは、特定のしきい値を超えた予期せぬ高トラフィックのバーストによるパフォーマンスの低下を防ぐための対策を講じています。サイトの可用性に影響を与える DoS 攻撃が発生した場合、アドビのオペレーションチームにアラートが送信され、解決策が講じられます。

お客様は、コンテンツ配信フローの様々なレイヤーでルールを設定することで、アプリケーションレイヤー攻撃（レイヤー 7）を回避するための積極的な対策を講じることができます。

例えば、Apache レイヤーでは、お客様が [Dispatcher モジュール](https://experienceleague.adobe.com/ja/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration#configuring-access-to-content-filter)または [ModSecurity](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection) を設定して、特定のコンテンツへのアクセスを制限できます。

この記事で説明するように、トラフィックフィルタールールは、Cloud Manager の[設定パイプライン](/help/operations/config-pipeline.md)を使用して、アドビが管理する CDN にデプロイできます。IP アドレス、パス、ヘッダーなどのプロパティに基づく *標準のトラフィックフィルタールール* や、レート制限の設定に基づくルールに加えて、お客様は、*WAF ルール* と呼ばれるトラフィックフィルタールールの強力なサブカテゴリのライセンスを取得することもできます。

## 推奨プロセス {#suggested-process}

適切なトラフィックフィルタールールを検討するための、エンドツーエンドで推奨される概要プロセスを次に示します。

1. 実稼動環境以外および実稼動環境の設定パイプラインの指定について詳しくは、[設定](#setup)の節を参照してください。
1. *WAF トラフィックフィルタールールのライセンスを取得しているお客様は* それらをCloud Managerで有効にする必要があります。
1. このチュートリアルを読んで、ライセンスを取得している場合は WAF ルールを含むトラフィックフィルタールールの使用方法を具体的に学びます。このチュートリアルでは、開発環境にルールのデプロイ、悪意のあるトラフィックのシミュレート、[CDN ログ](#cdn-logs)のダウンロード、[ダッシュボードツール](#dashboard-tooling)での分析を行う方法を説明します。
1. 推奨されるスタータールールを `cdn.yaml` にコピーし、一部のルールをログモードにして、設定を実稼動環境にデプロイします。
1. トラフィックを収集した後、[ダッシュボードツール](#dashboard-tooling)を使用して結果を分析し、一致の有無を確認します。偽陽性を探し、必要な調整を行って、最終的にブロックモードですべてのスタータールールを有効にします。
1. 必要に応じて、CDN ログの分析に基づいてカスタムルールを追加します。まず、開発環境でシミュレーショントラフィックを使用してテストしてから、ログモードでステージ環境と実稼動環境にデプロイし、次にブロックモードでデプロイします。
1. トラフィックを継続的に監視し、脅威の状況の進化に応じてルールを変更します。

## 設定 {#setup}

1. WAF ルールを含む一連のトラフィックフィルタールールを含んだファイル `cdn.yaml` を作成します。 例：

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

   `data` ノード上のプロパティの説明について詳しくは、[設定パイプラインの使用](/help/operations/config-pipeline.md#common-syntax)を参照してください。`kind` プロパティの値は *CDN* に設定し、バージョンは `1` に設定する必要があります。


1. WAF ルールにライセンスが付与されている場合は、新規および既存のプログラムシナリオの両方について、以下で説明するように、Cloud Manager で機能を有効にする必要があります。

   1. 新しいプログラムで WAF を設定するには、[実稼動プログラムを追加](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)する際に「**セキュリティ**」タブの「**WAF-DDOS 保護**」チェックボックスをオンにします。

   1. 既存のプログラムで WAF を設定するには、[プログラムを編集](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)し、任意の時点で「**セキュリティ**」タブで「**WAF-DDOS**」オプションをオフまたはオンにします。

1. [config パイプラインの記事 ](/help/operations/config-pipeline.md#managing-in-cloud-manager) の説明に従って、Cloud Managerで config パイプラインを作成します。 パイプラインは、`cdn.yaml` ファイルが下の任意の場所に配置された最上位レベルの `config` フォルダーを参照します。詳しくは、[設定パイプラインの使用](/help/operations/config-pipeline.md#folder-structure)を参照してください。

## トラフィックフィルタールールの構文 {#rules-syntax}

*トラフィックフィルタールール* を設定して、IP、ユーザーエージェント、リクエストヘッダー、ホスト名、地域、url などのパターンを照合できます。

Enhanced Security またはWAF-DDoS Protection Security 製品のライセンスを取得しているお客様は、*WAF トラフィックフィルタールール* （略して *WAF ルール*）と呼ばれる、1 つ以上の [WAF フラグ ](#waf-flags-list) を参照する特別なカテゴリのトラフィックフィルタールールも設定できます。

WAF ルールも含む一連のトラフィックフィルタールールの例を以下に示します。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

`cdn.yaml` ファイル内のトラフィックフィルタールールの形式を以下に示します。後の節に記載されている[その他の例](#examples)と、[レート制限ルール](#rate-limit-rules)に関する別の節を参照してください。


| **プロパティ** | **ほとんどのトラフィックフィルタールール** | **WAF トラフィックフィルタルール** | **タイプ** | **デフォルト値** | **説明** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | ルール名（長さは 64 文字、英数字と - のみを使用できます） |
| when | X | X | `Condition` | - | 基本的な構造は次のとおりです。<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[条件構造の構文を参照](#condition-structure)してください。ゲッター、述語および複数の条件を組み合わせる方法について記載しています。 |
| アクション | X | X | `Action` | log | ログ、許可、ブロック、または Action オブジェクト。デフォルトは log です。 |
| rateLimit | X |   | `RateLimit` | 定義なし | レート制限の設定。定義されていない場合、レート制限は無効になります。<br><br>以下に、rateLimit 構文と例を説明する別のセクションを示します。 |

### 条件の構造 {#condition-structure}

条件は、単純条件または条件のグループにすることができます。

**単純条件**

単純条件は、getter と述語で構成されています。

```
{ <getter>: <value>, <predicate>: <value> }
```

**グループ条件**

条件グループは、複数の単純条件やグループ条件で構成されます。

```
<allOf|anyOf>:
  - { <getter>: <value>, <predicate>: <value> }
  - { <getter>: <value>, <predicate>: <value> }
  - <allOf|anyOf>:
    - { <getter>: <value>, <predicate>: <value> }
```

| **プロパティ** | **タイプ** | **意味** |
|---|---|---|
| **allOf** | `array[Condition]` | **AND** 操作。リストに表示されているすべての条件が true を返す場合は true |
| **anyOf** | `array[Condition]` | **OR** 操作。リストに表示された条件のいずれかが true を返す場合は true |

**getter**

| **プロパティ** | **タイプ** | **説明** |
|---|---|---|
| reqProperty | `string` | リクエストプロパティ。<br><br>次のいずれか：<br><ul><li>`path`：URL のフルパスをクエリパラメーターなしで返します。（エスケープされていないバリアントには `pathRaw` を使用）</li><li>`url`：完全な URL をクエリパラメーターを含めて返します。（エスケープされていないバリアントには `urlRaw` を使用）</li><li>`queryString`：URL のクエリ部分を返します</li><li>`method`：リクエストで使用される HTTP メソッドを返します。</li><li>`tier`：`author`、`preview` または `publish` のいずれか 1 つを返します。</li><li>`domain`：小文字のドメインプロパティ（`Host` ヘッダーで定義）を返します</li><li>`clientIp`：クライアント IP を返します。</li><li>`forwardedDomain`：`X-Forwarded-Host` ヘッダーで定義されている最初のドメインを小文字で返します。</li><li>`forwardedIp`：`X-Forwarded-For` ヘッダーの最初の IP を返します。</li><li>`clientRegion`：[ISO 3166-2](https://en.wikipedia.org/wiki/ISO_3166-2) で説明されているように、クライアントがいる地域を識別する国の下位区分コードを返します。</li><li>`clientCountry`：クライアントがいる国を識別する 2 文字のコード（[地域指標記号](https://en.wikipedia.org/wiki/Regional_indicator_symbol)）を返します。</li><li>`clientContinent`：クライアントがいる大陸を識別する 2 文字のコード（AF、AN、AS、EU、NA、OC、SA）を返します。</li><li>`clientAsNumber`：クライアント IP に関連付けられた[自律システム](https://en.wikipedia.org/wiki/Autonomous_system_(Internet))番号を返します。</li><li>`clientAsName`：自律システム番号に関連付けられた名前を返します。</li></ul> |
| reqHeader | `string` | 指定された名前のリクエストヘッダーを返します |
| queryParam | `string` | 指定された名前のクエリパラメーターを返します |
| reqCookie | `string` | 指定された名前の Cookie を返します |
| postParam | `string` | リクエスト本文から指定された名前の Post パラメーターを返します。本文がコンテンツタイプ `application/x-www-form-urlencoded` の場合にのみ機能します |

**述語**

| **プロパティ** | **タイプ** | **意味** |
|---|---|---|
| **equals** | `string` | getter の結果が指定された値と等しい場合は true |
| **doesNotEqual** | `string` | ゲッターの結果が指定された値と等しくない場合は true |
| **like** | `string` | getter の結果が指定されたパターンと一致する場合は true |
| **notLike** | `string` | getter の結果が指定されたパターンに一致しない場合は true |
| **matches** | `string` | getter の結果が指定された正規表現と一致する場合は true |
| **doesNotMatch** | `string` | getter の結果が指定された正規表現と一致しない場合は true |
| **in** | `array[string]` | 指定されたリストに getter の結果が含まれている場合は true |
| **notIn** | `array[string]` | 指定されたリストに getter の結果が含まれていない場合は true |
| **exists** | `boolean` | true に設定し、プロパティが存在する場合、または false に設定し、プロパティが存在しない場合は true |

**備考**

* request プロパティ `clientIp` は、`equals`、`doesNotEqual`、`in`、`notIn` の述語でのみ使用できます。`clientIp` は、`in` および `notIn` 述語を使用する際に IP 範囲に対して比較することができます。次の例では、クライアント IP が IP 範囲 192.168.0.0/24（192.168.0.0～192.168.0.255）内にあるかどうかを評価する条件を実装しています。

```
when:
  reqProperty: clientIp
  in: [ "192.168.0.0/24" ]
```

* 正規表現を使用する際は、[regex101](https://regex101.com/) および [Fastly Fidle](https://fiddle.fastly.dev/) の使用をお勧めします。また、Fastly による正規表現の処理方法について詳しくは、[fastly ドキュメント - Fastly VCL の正規表現](https://www.fastly.com/documentation/reference/vcl/regex/#best-practices-and-common-mistakes)を参照してください。


### アクション構造 {#action-structure}

`action` は、アクション（allow、block、log）を指定する文字列や、アクションタイプ（allow、block、log）と wafFlags や status などのオプションの両方で構成されるオブジェクトのいずれかです。

**アクションタイプ**

アクションは、次の表に示すタイプに従って優先順位付けされ、実行される順序アクションを反映するように並べ替えられます。

| **名前** | **許可されたプロパティ** | **意味** |
|---|---|---|
| **許可** | `wafFlags`（任意）、`alert`（任意） | wafFlags が存在しない場合、それ以上のルール処理を停止し、サービング応答に進みます。wafFlags が存在する場合、指定された WAF 保護が無効になり、追加のルール処理に進みます。<br>アラートを指定した場合、ルールが 5 分間に 10 回トリガーされると、アクションセンター通知が送信されます。特定のルールに対してアラートがトリガーされると、翌日（UTC）まで再度アラートはトリガーされません。 |
| **block** | `status, wafFlags`（任意、相互に排他的）、`alert`（任意） | wafFlags が存在しない場合、他のすべてのプロパティをバイパスする HTTP エラーを返します。エラーコードは status プロパティによって定義されるか、デフォルトの 406 となります。wafFlags が存在する場合は、指定された WAF 保護を有効にし、さらにルール処理を続行します。<br>アラートを指定した場合、ルールが 5 分間に 10 回トリガーされると、アクションセンター通知が送信されます。特定のルールに対してアラートがトリガーされると、翌日（UTC）まで再度アラートはトリガーされません。 |
| **log** | `wafFlags`（任意）、`alert`（任意） | ルールがトリガーされたことをログに記録します。トリガーされていない場合、処理に影響は及びません。wafFlags は影響を受けません。<br>アラートを指定した場合、ルールが 5 分間に 10 回トリガーされると、アクションセンター通知が送信されます。特定のルールに対してアラートがトリガーされると、翌日（UTC）まで再度アラートはトリガーされません。 |

### WAF フラグリスト {#waf-flags-list}

ライセンス可能な WAF トラフィックフィルタールールで使用可能な `wafFlags` プロパティは、以下を参照できます。

#### 悪意のあるトラフィック

| **フラグ ID** | **フラグ名** | **説明** |
|---|---|---|
| ATTACK | 攻撃 | 悪意のあるトラフィック （SQLI、CMDXE、XSS など）に関連するフラグの集計。 このフラグを効果的に使用する方法については、[ 推奨されるWAF ルールの節 ](#recommended-waf-starter-rules) を参照してください。 |
| ATTACK-FROM-BAD-IP | 不正 IP からの攻撃 | ATTACK フラグと似ていますが、「LOGICAL AND-ed」が `BAD-IP` フラグ付きなので、ATTACK と BAD-IP の両方に一致する場合はリクエストがフラグ付けされます。 このフラグを効果的に使用する方法については、[ 推奨されるWAF ルールの節 ](#recommended-waf-starter-rules) を参照してください。 |
| SQLI | SQL インジェクション | SQL インジェクションとは、任意のデータベースクエリを実行して、アプリケーションへのアクセス権や権限情報を取得したりしようとする試みです。 |
| バックドア | バックドア | バックドア信号は、共通のバックドアファイルがシステム上に存在するかどうかの判断を試みるリクエストです。 |
| CMDEXE | コマンドの実行 | コマンドの実行とは、ユーザー入力による任意のシステムコマンドを通じて、ターゲットシステムを制御したり損傷したりしようとする試みです。 |
| CMDEXE-NO-BIN | `/bin/` を除くコマンドの実行 | AEM アーキテクチャにより、`/bin` での偽陽性を無効にしながら、`CMDEXE` と同じレベルの保護を提供します。 |
| XSS | クロスサイトスクリプティング | クロスサイトスクリプティングとは、悪意のある JavaScript コードを通じてユーザーのアカウントまたは web ブラウジングセッションをハイジャックしようとする試みです。 |
| トラバーサル | ディレクトリトラバーサル | ディレクトリトラバーサルとは、機密情報を取得することを目的として、システム全体の権限フォルダーを移動しようとする試みです。 |
| USERAGENT | 攻撃ツール | 攻撃ツールでは、自動化されたソフトウェアを使用して、セキュリティの脆弱性を特定したり、発見された脆弱性の悪用を試みたりします。 |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI 攻撃では、Log4J バージョン 2.16.0 より前の [Log4Shell 脆弱性](https://ja.wikipedia.org/wiki/Log4Shell)を悪用しようと試みます |
| CVE | CVE | CVE を識別するフラグ。常にフラグ `CVE-<CVE Number>` と組み合わせます。アドビが保護する CVE について詳しくは、アドビにお問い合わせください。 |

#### 不審なトラフィック

| **フラグ ID** | **フラグ名** | **説明** |
|---|---|---|
| ABNORMALPATH | 異常なパス | 異常なパスは、元のパスが正規化されたパスと異なることを示します（例えば、`/foo/./bar` は `/foo/bar` に正規化されます） |
| BAD-IP | 不正な IP | `SANS` や `TORNODE` などのデータセットに含まれるか、WAFによって以前に悪意のある動作が検出されたことにより、悪意のあることが判明している IP アドレスからのリクエストを特定します |
| BHH | 不正なホップヘッダー | 不正なホップヘッダーは、不正な形式の Transfer-Encoding（TE）ヘッダーまたは Content-Length（CL）ヘッダー、適切な形式の TE および CL ヘッダーを介した HTTP スマグリングの試みを示します |
| CODEINJECTION | コードインジェクション | コードインジェクションとは、ユーザー入力による任意のアプリケーションコードコマンドを通じて、ターゲットシステムを制御したり損傷したりしようとする試みです。 |
| COMPRESSED | 検出された圧縮 | POST リクエスト本文が圧縮されており、検査できません。例えば、`Content-Encoding: gzip` リクエストヘッダーが指定され、POST 本文がプレーンテキストではない場合です。 |
| RESPONSESPLIT | HTTP 応答分割 | HTTP 応答にヘッダーを挿入するために CRLF 文字をアプリケーションへの入力として送信するタイミングを指定します。 |
| NOTUTF8 | 無効なエンコーディング | 無効なエンコーディングでは、サーバーがリクエストの悪意のある文字をレスポンスに変換し、サービス拒否または XSS を引き起こす可能性があります。 |
| MALFORMED-DATA | リクエスト本文内の不正なデータ | 「Content-Type」リクエストヘッダーに従って不正な形式である POST、PUT、PATCH リクエストの本文です。例えば、「Content-Type: application/x-www-form-urlencoded」リクエストヘッダーが指定され、JSON である POST 本文が含まれているとします。これは、多くの場合、プログラミングエラーや、自動リクエスト、悪意のあるリクエストです。エージェント 3.2 以降が必要です。 |
| SANS | 悪意のある IP トラフィック | [SANS Internet Storm Center](https://isc.sans.edu/) には、悪意のあるアクティビティにエンゲージしたと報告された IP アドレスのリストが含まれます。 |
| NO-CONTENT-TYPE | 「Content-Type」リクエストヘッダーなし | 「Content-Type」リクエストヘッダーを持たない POST、PUT または PATCH リクエストです。この場合、アプリケーションサーバーでは、デフォルトで「Content-Type: text/plain; charset=us-ascii」を想定する必要があります。自動化された悪意のあるリクエストの多くには、「Content-Type」が欠落している可能性があります。 |
| NOUA | ユーザーエージェントなし | リクエストに「User-Agent」ヘッダーが含まれていなかったか、ヘッダー値が設定されていなかったことを示します。 |
| NULLBYTE | Null バイト | 通常、Null バイトはリクエストには表示されず、リクエストの形式が正しくなく、悪意がある可能性があることを示します。 |
| OOB-DOMAIN | アウトオブバンドドメイン | アウトオブバンドドメインは通常、ネットワークアクセスが許可されている脆弱性を識別するために、侵入テストで使用されます。 |
| PRIVATEFILE | プライベートファイル | プライベートファイルは、Apache `.htaccess` ファイルや、機密情報の漏洩につながる可能性のある設定ファイルなど、本来、部外秘のものです。 |
| スキャナー | スキャナー | 一般に使用されるスキャンサービスおよびツールを指定します。 |

#### その他のトラフィック

| **フラグ ID** | **フラグ名** | **説明** |
|---|---|---|
| DATACENTER | データセンター | リクエストの発信元が既知のホスティングプロバイダーであることを識別します。このタイプのトラフィックは、通常、実際のエンドユーザーに関連付けられません。 |
| DOUBLEENCODING | 二重エンコーディング | 二重エンコーディングでは、HTML 文字の二重エンコーディングを回避する方法を確認します |
| JSON-ERROR | JSON エンコーディングエラー | 「Content-Type」リクエストヘッダー内に JSON を含むように指定されている POST、PUT、PATCH リクエスト本文には、JSON 解析エラーが含まれています。これは、多くの場合、プログラミングエラー、自動リクエストまたは悪意のあるリクエストに関係しています。 |
| TORNODE | Tor トラフィック | Tor は、ユーザーの ID を隠すソフトウェアです。Tor トラフィックのスパイクは、攻撃者がその場所をマスクしようとしていることを示す可能性があります。 |
| XML-ERROR | XML エンコーディングエラー | 「Content-Type」リクエストヘッダー内に XML を含むように指定されているが、XML 解析エラーが含まれている POST、PUT または PATCH リクエスト本文です。これは、多くの場合、プログラミングエラー、自動リクエストまたは悪意のあるリクエストに関係しています。 |

## 考慮事項 {#considerations}

* 2 つの競合するルールを作成した場合は、許可ルールが常にブロックルールより優先されます。例えば、特定のパスをブロックするルールと 1 つの特定の IP アドレスを許可するルールを作成する場合、ブロックされたパス上のその IP アドレスからのリクエストは許可されます。

* ルールが一致してブロックされた場合、CDN は `406` リターンコードで応答します。

* 設定ファイルは、Git リポジトリにアクセスできるユーザーなら誰でも読み取れるので、設定ファイルにはシークレットを含めないでください。

* Cloud Manager で定義された IP 許可リストは、トラフィックフィルタールールよりも優先されます。

* WAF ルールの一致は、CDN のミスおよびパスに関して CDN ログにのみ表示され、ヒットには表示されません。

## ルールの例 {#examples}

ルールの例をいくつか以下に示します。レート制限ルールの例については、さらに下の[レート制限ルール](#rate-limit-rules)の節を参照してください。

**例 1**

このルールは、**IP192.168.1.1** からのリクエストをブロックします。

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

このルールは、Chrome を含む User-Agent を使用した、パブリッシュ上のパス `/helloworld` に対するリクエストをブロックします。

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

このルールは、クエリパラメーター `foo` を含むリクエストを公開時にブロックしますが、IP 192.168.1.1 からのリクエストをすべて許可します。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when:
          allOf:
            - { queryParam: url-param, equals: foo }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action:
          type: allow
```

**例 4**

このルールは、パス `/block-me` へのリクエストをパブリッシュ時にブロックし、`SQLI` または `XSS` パターンに一致するすべてのリクエストをブロックします。この例には、`SQLI` および `XSS` [WAF フラグ](#waf-flags-list)を参照する WAF トラフィックフィルタールールが含まれているので、別途ライセンスが必要になります。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

**例 5**

このルールは、OFAC 諸国へのアクセスをブロックします。

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

## レート制限ルール

特定の条件に基づいて、受信リクエストの一定のレートを超えた場合にトラフィックをブロックすることが望ましい場合があります。`rateLimit` プロパティの値を設定すると、ルール条件に一致するリクエストのレートが制限されます。

レート制限ルールでは、WAF フラグを参照できません。Sites と Forms のすべてのお客様が使用できます。

レート制限は、CDN POP ごとに計算されます。例えば、モントリオール、マイアミ、ダブリンの POP のトラフィックレートがそれぞれ 1 秒あたり 80、90、120 リクエストだとします。さらに、レート制限ルールが上限 100 に設定されています。その場合、ダブリンへのトラフィックのみがレート制限されます。

レート制限は、エッジに到達するトラフィック、接触チャネルに到達するトラフィック、またはエラーの数に基づいて評価されます。

### rateLimit の構造 {#ratelimit-structure}

| **プロパティ** | **タイプ** | **デフォルト** | **意味** |
|---|---|---|---|
| limit | 10～10000 の整数 | 必須 | ルールがトリガーされる、1 秒あたりのリクエスト数のリクエストレート（CDN POP あたり）です。 |
| window | 整数列挙：1、10 または 60 | 10 | リクエストレートが計算されるサンプリングウィンドウ（秒単位）です。カウンターの精度は、ウィンドウのサイズによって異なります（ウィンドウが大きいほど精度が高くなります）。例えば、1 秒のウィンドウでは 50％の精度、60 秒のウィンドウでは 90％の精度が期待できます。 |
| penalty | 60～3600 の整数 | 300（5 分） | 一致するリクエストがブロックされる期間（秒単位）です（最も近い分に四捨五入）。 |
| 回数 | すべて、取得、エラー | すべて | エッジトラフィック（すべて）、接触チャネルトラフィック（取得）、またはエラーの数（エラー）に基づいて評価します。 |
| groupBy | 配列[ゲッター] | なし | レートリミッターカウンターは、一連のリクエストプロパティ（clientIp など）によって集計されます。 |

### 例 {#ratelimiting-examples}

**例 1**

このルールは、最後の 10 秒間に平均 60 リクエスト/秒（CDN POP あたり）を超えると、クライアントを 5 ミリ秒間ブロックします。

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
        count: all
        groupBy:
          - reqProperty: clientIp
      action: block
```

**例 2**

10 秒の時間ウィンドウで、接触チャネルへのリクエストが 1 秒あたり 平均 100 件（CDN POP あたり）を超えた場合、パス /critical/resource 上のリクエストを 60 秒間ブロックします。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when:
          allOf:
            - { reqProperty: path, equals: /critical/resource }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
        rateLimit: { limit: 100, window: 10, penalty: 60, count: fetches }
```

## CVE ルール {#cve-rules}

WAF のライセンスを取得している場合、アドビでは、多数の既知の CVE（一般的な脆弱性と暴露）を防ぐためにブロックルールを自動的に適用しており、新しい CVE は検出されると直ちに追加される可能性があります。お客様自身で、CVE ルールを設定する必要はありません。

トラフィックリクエストが CVE に一致する場合、対応する CDN ログエントリに表示されます。

特定の CVE に関する質問がある場合、または組織が無効にする特定の CVE ルールがある場合は、アドビサポートにお問い合わせください。

## トラフィックフィルタールールアラート {#traffic-filter-rules-alerts}

5 分間に 10 回トリガーされた場合にアクションセンター通知を送信するルールを設定できます。このようなルールにより、特定のトラフィックパターンが発生した際にアラートが表示されるので、必要な措置を講じることができます。特定のルールに対してアラートがトリガーされると、翌日（UTC）まで再度アラートはトリガーされません。

メールを受信するために必要な通知プロファイルの設定方法などについて詳しくは、[アクションセンター](/help/operations/actions-center.md)を参照してください。

![アクションセンターの通知](/help/security/assets/traffic-filter-rules-actions-center-alert.png)


アラートプロパティは、すべてのアクションタイプ（許可、ブロック、ログ）のアクションノードに適用できます。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
          alert: true
```

## 接触チャネルでのトラフィックスパイクを示すデフォルトアラート {#traffic-spike-at-origin-alert}

[アクションセンター](/help/operations/actions-center.md)メール通知は、接触チャネルに大量のトラフィックが送信された際に送信されます。この場合、同じ IP アドレスから高しきい値のリクエストが送信されているため、DDoS 攻撃が示唆されています。

このしきい値に達すると、アドビはその IP アドレスからのトラフィックをブロックしますが、接触チャネルを保護するための追加の対策を講じることをお勧めします。例えば、低いしきい値でトラフィックスパイクをブロックするようにレート制限トラフィックフィルタールールを設定することができます。ガイド付きのウォークスルーについては、[トラフィックルールを使用した DoS および DDoS 攻撃のブロック（チュートリアル）](#tutorial-blocking-DDoS-with-rules)を参照してください。

このアラートはデフォルトで有効になっていますが、*defaultTrafficAlerts* プロパティを false に設定し、無効化することもできます。アラートがトリガーされると、翌日（UTC）まで再度アラートはトリガーされません。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
   defaultTrafficAlerts: false
```

## CDN ログ {#cdn-logs}

AEM as a Cloud Service では、ユーザーが CDN ログにアクセスできるようになっています。このログは、キャッシュヒット率の最適化などのユースケースやトラフィックフィルタールールの設定に役立ちます。CDN ログは、オーサーサービスやパブリッシュサービスの選択時に Cloud Manager の&#x200B;**ログをダウンロード**&#x200B;ダイアログに表示されます。

CDN ログは、最大 5 分遅れる場合があります。

`rules` プロパティは、一致するトラフィックフィルタールールを次のパターンで示します。

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

次に例を示します。

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

ルールは次のように動作します。

* 一致するルールの、ユーザーが宣言したルール名が `match` 属性にリストされます。
* `action` 属性は、ルールがブロック、許可、ログのいずれであるかを決定します。
* WAF がライセンス取得済みで有効になっている場合、`waf` 属性には検出されたすべての WAF フラグ（SQLI など）がリストされます。これは、WAF フラグがルールにリストされていたかどうかに関係なく当てはまります。これは、宣言する可能性のある新しいルールに関するインサイトを提供するためです。
* ユーザーが宣言したルールが一致せず、WAF ルールも一致しない場合、`rules` プロパティは空白になります。

前述のように、WAF ルールの一致は、CDN のミスとパスに関して CDN ログにのみ表示され、ヒットには表示されません。

以下の例では、サンプル `cdn.yaml` と 2 つの CDN ログエントリを示しています。


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

CDN ログで使用されるフィールド名と、それらの簡単な説明を以下に示します。

| **フィールド名** | **説明** |
|---|---|
| *timestamp* | TLS 終了後のリクエストの開始時刻です。 |
| *ttfb* | *Time To First Byte* の略称です。リクエストの開始から、応答本文のストリーミングが開始される前の時点までの時間間隔です。 |
| *cli_ip* | クライアントの IP アドレスです。 |
| *cli_country* | クライアント国の 2 文字の [ISO 3166-1](https://ja.wikipedia.org/wiki/ISO_3166-1) alpha-2 国コードです。 |
| *rid* | リクエストを一意に識別するために使用されるリクエストヘッダーの値です。 |
| *req_ua* | 特定の HTTP リクエストの作成を担当するユーザーエージェントです。 |
| *host* | リクエストの対象となる証明機関です。 |
| *URL* | クエリパラメーターを含む完全なパスです。 |
| *method* | 「GET」や「POST」など、クライアントによって送信される HTTP メソッドです。 |
| *res_ctype* | リソースの元のメディアタイプを示すために使用される Content-Type です。 |
| *cache* | キャッシュの状態です。指定できる値は、HIT、MISS、PASS です |
| *status* | 整数値としての HTTP ステータスコードです。 |
| *res_age* | 応答が（すべてのノードで）キャッシュされた時間です（秒単位）。 |
| *pop* | CDN キャッシュサーバーのデータセンターです。 |
| *rules* | 一致するルールの名前です。<br><br>また、一致がブロックされたかどうかも示します。<br><br>例：「`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`」<br><br>一致するルールがない場合は空です。 |

## ダッシュボードツール {#dashboard-tooling}

アドビでは、Cloud Manager 経由でダウンロードされた CDN ログを取り込むために、ダッシュボードツールをコンピューターにダウンロードするメカニズムを提供します。このツールを使用すると、トラフィックを分析して、宣言する適切なトラフィックフィルタールール（WAF ルールなど）を作成するのに役立ちます。

ダッシュボードツールでは、[AEMCS-CDN-Log-Analysis-Tooling](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling) Github リポジトリから直接クローンを作成できます。

ダッシュボードツールの使用方法に関する具体的な手順については、[ チュートリアル ](#tutorial) を参照してください。

## 推奨されるスタータールール {#recommended-starter-rules}

Adobeでは、以下のトラフィックフィルタールールから始めて、時間の経過と共に絞り込むことをお勧めします。 *標準規則* は Sites またはForms ライセンスで使用できますが、*WAF規則* には Enhanced Security またはWAF-DDoS Protection ライセンスが必要です。

### 推奨される標準規則 {#recommended-nonwaf-starter-rules}

次のルールから開始します。

1. レート制限（ログモード）:
   * 特定の IP からのトラフィックがレート制限を超えた場合にログに記録します。 アラートを受信していないことを検証した後、ブロックモードに変更します。アラートを受信した場合、制限値が低すぎることを示します。
2. 特定の国（ブロックモード）:
   * 特定の国からのトラフィックをブロックします（ビジネス要件に基づいて国コードを変更します）

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds an average of 100 req/sec to origin on a time window of 10sec
    - name: limit-origin-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 100
        window: 10
        count: fetches
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    #  Block client for 5m when it exceeds an average of 500 req/sec on a time window of 10sec
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 500
        window: 10
        count: all
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
      alert: true
    # Block requests coming from OFAC countries
    - name: ofac-countries
      when:
        allOf:
          - { reqProperty: tier, in: ["author", "publish"] }
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

### 推奨されるWAF ルール {#recommended-waf-starter-rules}

既存の設定に次のルールを追加します。

1. ATTACK-FROM-BAD-IP フラグ（ブロック モード）:
   * 疑わしいパターン （[WAF フラグ リスト ](#waf-flags-list) の一部を含む）に一致し、悪意のあることが判明している IP アドレスからのトラフィックを直ちにブロックします。
   * ATTACK-FROM-BAD-IP フラグは本質的に両方の条件（パターン一致と既知の悪意のある IP）を満たし、誤検知のリスクを最小限に抑えます。 したがって、このルールをすぐにブロッキングモードで安全に適用できます。
2. 攻撃フラグ （ログ モード）:
   * 最初は、疑わしいパターンに一致するが、既知の悪意のある IP アドレスから発信されていないトラフィックを（ブロックではなく）ログに記録します。 このようにブロックではなく慎重にログに記録するアプローチを使用すると、正当なトラフィックを誤ってブロックする（誤検知する）のを回避できます。
   * このルールをデプロイした後は、CDN ログを慎重に分析し、正当な要求が正しくフラグ付けされていないことを確認します。 正当なトラフィックが影響を受けていないことを確認したら、ブロックモードに切り替えます。

>[!NOTE]
> 私たちの経験によると、ATTACK フラグに関連する誤検出はまれです。 したがって、IP アドレスが悪意のあるものではないことがわかっている場合でも、疑わしいトラフィックをすべて直ちにブロックし、その後 CDN ログ分析を使用して正当なトラフィックの許可ルールを特定して導入することは、実用的な戦略です。 各組織は、リスクに対する独自の許容度を評価し、より大きな保護のメリットと、正当なリクエストを誤ってブロックするリスクを比較検討する必要があります。
>

```
    # blocks likely attack traffic, which also comes from suspected IPs
    - name: attacks-from-bad-ips-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: block
        wafFlags:
          - ATTACK-FROM-BAD-IP
    # log likely attack traffic, and later switch to block mode if false positives aren't observed
    - name: attacks-from-any-ips-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: log
        wafFlags:
          - ATTACK
```

### 従来の推奨WAF ルール {#previous-waf-starter-rules}

2025 年 7 月より、Adobeは、悪意のあるトラフィックに対する防御において引き続き有効かつ効果的である、以下に示すWAFの規則を推奨しています。 新しい推奨ルールへの移行に関する考慮事項については、チュートリアルを参照してください。

<details>
  <summary>を展開して、従来の推奨されるWAF ルールを表示します。</summary>

```
    # Enable recommended WAF protections (only works if WAF is licensed enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: log
        wafFlags:
          - TRAVERSAL
          - CMDEXE-NO-BIN
          - XSS
          - LOG4J-JNDI
          - BACKDOOR
          - USERAGENT
          - SQLI
          - SANS
          - TORNODE
          - NOUA
          - SCANNER
          - PRIVATEFILE
          - NULLBYTE
```

</details>

## チュートリアル {#tutorial}

[ 一連のチュートリアル ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview) を通じて、WAFのルールを含むトラフィックフィルタールールに関する実践的な知識と経験を得ます。

このチュートリアルには次が含まれます。

* 標準およびWAF トラフィックフィルタールールの概要
* DoS （Denial of Service）などの攻撃をブロックするための推奨される標準およびWAF トラフィックフィルタールールの設定
* Cloud Manager設定パイプラインを使用したルールのデプロイ
* 悪意のあるトラフィックをシミュレートするツールを使用したルールのテスト
* ログ分析ツールを使用した結果の分析
* ベストプラクティス




