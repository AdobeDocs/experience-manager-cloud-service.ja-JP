---
title: WAF ルールを含むトラフィックフィルタールール
description: Web アプリケーションファイアウォール（WAF）ルールを含むトラフィックフィルタールールの設定。
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
feature: Security
role: Admin
source-git-commit: fd729f12b4d6ff94ba4f3c86b8b8c1a0d3627c16
workflow-type: tm+mt
source-wordcount: '4278'
ht-degree: 66%

---


# WAF ルールを含むトラフィックフィルタールール {#traffic-filter-rules-including-waf-rules}

トラフィックフィルタールールは、CDN レイヤーでのリクエストをブロックまたは許可します。これは、次のようなシナリオで役立ちます。

* 新しいサイトが公開される前に、社内トラフィックへの特定のドメインへのアクセスを制限する。
* ボリューム型DoS攻撃の影響を受けにくくするには、レート制限を設定します。
* 悪意のあることが知られているIP アドレスがページをターゲットにするのを防ぎます。


これらのトラフィックフィルタールールの多くは、AEM as a Cloud Service Sites および Forms のすべてのお客様が利用できます。 *標準トラフィックフィルタールール*&#x200B;として、IP、ホスト名、パス、ユーザーエージェントなどのリクエストプロパティで動作します。 標準トラフィックフィルタールールには、トラフィックスパイクを防ぐためのレート制限ルールが含まれます。

トラフィックフィルタールールのサブカテゴリには、Extended Security （旧称WAF-DDoS Protection）またはExtended Security for Healthcare （旧称Enhanced Security）ライセンスが必要です。 これらの強力なルールは、WAF（Web Application Firewall）トラフィックフィルタールール（または&#x200B;*WAF ルール*）と呼ばれ、この記事で後述する[WAF フラグ ](#waf-flags-list)にアクセスできます。

トラフィックフィルタールールは、Cloud Manager 設定パイプラインを通じて、開発環境、ステージ環境および本番環境のタイプにデプロイできます。 設定ファイルは、コマンドラインツールを使用して高速開発環境（RDE）にデプロイできます。

この機能に関する専門知識をすばやく得るには、[ チュートリアルを完了](#tutorial)します。

>[!NOTE]
>リクエスト/レスポンスの編集、リダイレクトの宣言、AEM以外のオリジンへのプロキシなど、その他のCDN トラフィック設定オプションについては、「[CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md) トラフィックの設定」を参照してください。


## この記事の編集方法 {#how-organized}

この記事は、次の節で構成されています。

* **トラフィック保護の概要：**&#x200B;悪意のあるトラフィックから保護される方法を説明します。
* **ルールを設定するための推奨プロセス：** web サイトを保護する高度な方法について説明します。
* **設定：**&#x200B;高度なWAF ルールを含む、トラフィックフィルタールールの設定、設定、デプロイ方法について説明します。
* **ルール構文：`cdn.yaml`設定ファイルで** トラフィックフィルタールールを宣言する方法を説明します。 これには、すべての Sites および Forms の顧客が利用できるトラフィックフィルタールールとその機能をライセンスするユーザー向けの WAF ルールのサブカテゴリの両方が含まれます。
* **ルールの例：**&#x200B;最初に、宣言されたルールの例を参照してください。
* **レート制限ルール：**&#x200B;レート制限ルールを使用して、大量の攻撃からサイトを保護する方法を説明します。
* **トラフィックフィルタールールのアラート：** ルールがトリガーされたときに通知するアラートを設定します。
* **発信元のデフォルト トラフィックの急増アラート：** DDoS攻撃を示唆するトラフィックが発信元に急増した場合に通知されます。
* **CDN ログ：**&#x200B;トラフィックに一致する宣言済みルールと WAF フラグを確認します。
* **ダッシュボードツール：** CDN ログを分析して、新しいトラフィックフィルタールールを作成する方法を説明します。
* **推奨されるスタータールール：**&#x200B;使用を開始するための一連のルール。
* **チュートリアル：** ダッシュボードツールを使用して適切なルールを宣言する方法など、機能に関する情報。

## トラフィック保護の概要 {#traffic-protection-overview}

現在のデジタル環境では、悪意のあるトラフィックの脅威は常に存在します。 アドビは、リスクの重大性を認識し、お客様のアプリケーションを保護し、攻撃の発生率を軽減するためのいくつかのアプローチを提供します。

エッジでは、アドビが管理する CDN が、フラッド攻撃やリフレクション攻撃／増幅攻撃を含む、ネットワークレイヤー（レイヤー 3 およびレイヤー 4）での DoS 攻撃を吸収します。

デフォルトでは、アドビは、特定のしきい値を超えた予期せぬ高トラフィックのバーストによるパフォーマンスの低下を防ぐための対策を講じています。 サイトの可用性に影響を与える DoS 攻撃が発生した場合、アドビのオペレーションチームにアラートが送信され、解決策が講じられます。

顧客は、コンテンツ配信フローの様々なレイヤーでルールを設定することで、アプリケーションレイヤーの攻撃（レイヤー7）を軽減するための積極的な対策を講じます。

例えば、Apache レイヤーでは、特定のコンテンツへのアクセスを制限するために、[Dispatcher モジュール ](https://experienceleague.adobe.com/ja/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration#configuring-access-to-content-filter)または[ModSecurity](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection)のいずれかを設定します。

この記事で説明しているように、トラフィックフィルタールールは、Cloud Managerの[設定パイプライン ](/help/operations/config-pipeline.md)を使用してAdobe Managed CDNにデプロイされます。 *標準トラフィックフィルタールール* （IP、パス、ヘッダー、レート制限）を超えると、お客様は&#x200B;*WAF ルール*&#x200B;のライセンスを取得します。

## 推奨プロセス {#suggested-process}

適切なトラフィックフィルタールールを決定するための、推奨されるエンドツーエンドの大まかなプロセスを次に示します。

1. 実稼動環境以外および実稼動環境の設定パイプラインの指定について詳しくは、[設定](#setup)の節を参照してください。
1. *WAF トラフィックフィルタールール*&#x200B;のライセンスを取得したお客様は、Cloud Managerでそれらを有効にできます。

   >[!IMPORTANT]
   >
   >WAF ルール *のライセンスを取得しても、*&#x200B;はライセンスを取得しません。 この機能は、Cloud Managerの「**セキュリティ**」タブで&#x200B;**WAF-DDOS Protection**&#x200B;がチェックされるまで非アクティブのままです。 この機能を有効にするには、[実稼動プログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)または[ プログラムの編集](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)を参照してください。

1. ライセンスが付与されている場合のWAF ルールなど、トラフィックフィルタールールの使用方法を説明するチュートリアルを読み、完了してください。 このチュートリアルでは、開発環境にルールのデプロイ、悪意のあるトラフィックのシミュレート、[CDN ログ](#cdn-logs)のダウンロード、[ダッシュボードツール](#dashboard-tooling)での分析を行う方法を説明します。
1. 推奨されるスタータールールを `cdn.yaml` にコピーし、一部のルールをログモードにして、本番環境に設定をデプロイします。
1. トラフィックを収集した後、[ダッシュボードツール](#dashboard-tooling)を使用して結果を分析し、一致の有無を確認します。 偽陽性を確認し、必要な調整をおこない、最終的にすべてのスタータールールをブロックモードで有効にします。
1. 必要に応じて、CDN ログの分析に基づいてカスタムルールを追加します。まず、開発環境でシミュレートされたトラフィックを使用してテストしてから、ログモード、次にブロックモードでステージ環境および本番環境にデプロイします。
1. トラフィックを継続的に監視し、脅威の状況の進化に応じてルールを変更します。

## 設定 {#setup}

1. WAF ルールなどトラフィックフィルタールールのセットを含むファイル `cdn.yaml` を作成します。 例：

   ```
   kind: "CDN"
   version: "1"
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

   `data` ノード上のプロパティの説明について詳しくは、[設定パイプラインの使用](/help/operations/config-pipeline.md#common-syntax)を参照してください。 `kind` プロパティの値は *CDN* に設定し、バージョンは `1` に設定する必要があります。


1. WAF ルールがライセンスされている場合は、*Cloud Managerでこの機能を有効にする必要があります*。 WAFのライセンス認証ルールでは、ライセンス認証は行われません。 この機能は、**WAF-DDOS Protection**&#x200B;がCloud Managerの「セキュリティ」タブでオンになるまで非アクティブのままです。

   次の説明に従って、新規および既存のプログラムシナリオの両方で機能を有効にします。

   1. 新しいプログラムでWAFを設定するには、[実稼動プログラムを作成する](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)際に&#x200B;**セキュリティ** タブの&#x200B;**WAF-DDOS Protection** チェックボックスをオンにします。

   1. 既存のプログラムでWAFを設定するには、[ プログラムを編集します](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)。 「**セキュリティ**」タブで、**WAF-DDOS Protection** オプションをオンにして機能を有効にするか、オフにして機能を無効にします。 この設定はいつでも変更できます。

      機能を有効にした後に&#x200B;*アクティブ*&#x200B;であることを確認するには、トラフィックがサイトに流れたら、[CDN ログ ](#cdn-logs)を調べます。 `waf`属性を含む`rules` プロパティを含むログエントリを探します。 次に例を示します。

      `"rules": "*waf=*" `

      この属性は、WAF ルールがデプロイされる前であっても、WAFがアクティブになると表示されます。

1. [設定パイプラインの記事](/help/operations/config-pipeline.md#managing-in-cloud-manager)の説明に従って、Cloud Manager で設定パイプラインを作成します。 パイプラインは、最上位`config` フォルダーを参照し、下のどこかに`cdn.yaml` ファイルが配置されています。[設定パイプラインの使用](/help/operations/config-pipeline.md#folder-structure)を参照してください。

## トラフィックフィルタールールの構文 {#rules-syntax}

IP、ユーザーエージェント、ヘッダー、ホスト名、地域、URLなどのパターンを一致させるには、*トラフィックフィルタールール*&#x200B;を設定できます。

Extended SecurityまたはExtended Security for Healthcare ライセンスをお持ちのお客様は、*WAF ルール*&#x200B;を設定して、[WAF フラグ ](#waf-flags-list)を参照してください。

WAF ルールも含む一連のトラフィックフィルタールールの例を以下に示します。

```
kind: "CDN"
version: "1"
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

`cdn.yaml` ファイル内のトラフィックフィルタールールの形式を以下に示します。 後の節に記載されている[その他の例](#examples)と、[レート制限ルール](#rate-limit-rules)に関する別の節を参照してください。


| **プロパティ** | **ほとんどのトラフィックフィルタールール** | **WAF トラフィックフィルタルール** | **タイプ** | **デフォルト値** | **説明** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | ルール名（長さは 64 文字、英数字と - のみを使用できます） |
| when | X | X | `Condition` | - | 基本的な構造は次のとおりです。<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br> ゲッター、述語、および複数の条件を組み合わせる方法については、*CDN*&#x200B;でのトラフィックの設定の[条件構造](/help/implementing/dispatcher/cdn-configuring-traffic.md#condition-structure)を参照してください。 |
| アクション | X | X | `Action` | log | ログ、許可、ブロック、または Action オブジェクト。 デフォルトは log です。 |
| rateLimit | X |   | `RateLimit` | 定義なし | レート制限の設定。 定義されていない場合、レート制限は無効になります。<br><br>以下に、rateLimit 構文と例を説明する別のセクションを示します。 |

### アクション構造 {#action-structure}

`action` は、アクション（allow、block、log）を指定する文字列や、アクションタイプ（allow、block、log）と wafFlags や status などのオプションの両方で構成されるオブジェクトのいずれかです。

**アクションタイプ**

アクションは、次の表に示すタイプに従って優先順位付けされ、実行される順序アクションを反映するように並べ替えられます。

| **名前** | **許可されたプロパティ** | **意味** |
|---|---|---|
| **許可** | `wafFlags`（任意）、`alert`（任意） | wafFlags が存在しない場合、それ以上のルール処理を停止し、サービング応答に進みます。 wafFlags が存在する場合、指定された WAF 保護が無効になり、追加のルール処理に進みます。 <br>アラートを指定した場合、ルールが 5 分間に 10 回トリガーされると、アクションセンター通知が送信されます。 特定のルールに対してアラートがトリガーされると、翌日（UTC）まで再度起動されません。 |
| **block** | `status, wafFlags`（任意、相互に排他的）、`alert`（任意） | wafFlags が存在しない場合、他のすべてのプロパティをバイパスする HTTP エラーを返します。エラーコードは status プロパティによって定義されるか、デフォルトの 406 となります。 wafFlags が存在する場合は、指定された WAF 保護を有効にし、さらにルール処理を続行します。 <br>アラートを指定した場合、ルールが 5 分間に 10 回トリガーされると、アクションセンター通知が送信されます。 特定のルールに対してアラートがトリガーされると、翌日（UTC）まで再度起動されません。 |
| **log** | `wafFlags`（任意）、`alert`（任意） | ルールがトリガーされたことをログに記録します。トリガーされていない場合、処理に影響は及びません。 wafFlags は影響を受けません。 <br>アラートを指定した場合、ルールが 5 分間に 10 回トリガーされると、アクションセンター通知が送信されます。 特定のルールに対してアラートがトリガーされると、翌日（UTC）まで再度起動されません。 |

### WAFのフラグ一覧 {#waf-flags-list}

ライセンス可能なWAF トラフィックフィルタールールで使用される`wafFlags` プロパティは、次を参照します。

#### 悪意のあるトラフィック

| **フラグ ID** | **フラグ名** | **説明** |
|---|---|---|
| ATTACK | 攻撃 | 悪意のあるトラフィック（SQLI、CMDEXE、XSS など）に関連するフラグの集計。 このフラグを効果的に使用する方法について詳しくは、[推奨される WAF ルール](#recommended-waf-starter-rules)の節を参照してください。 |
| ATTACK-FROM-BAD-IP | 不正 IP からの攻撃 | ATTACK フラグに類似していますが、`BAD-IP` フラグと「論理 AND 演算」されるので、リクエストが ATTACK と BAD-IP の両方に一致した場合にフラグが付けられます。 このフラグを効果的に使用する方法について詳しくは、[推奨される WAF ルール](#recommended-waf-starter-rules)の節を参照してください。 |
| SQLI | SQL インジェクション | SQL インジェクションとは、任意のデータベースクエリを実行して、アプリケーションへのアクセス権や権限情報を取得したりしようとする試みです。 |
| バックドア | バックドア | バックドア信号は、共通のバックドアファイルがシステム上に存在するかどうかの判断を試みるリクエストです。 |
| CMDEXE | コマンドの実行 | コマンドの実行とは、ユーザー入力による任意のシステムコマンドを通じて、ターゲットシステムを制御したり損傷したりしようとする試みです。 |
| CMDEXE-NO-BIN | `/bin/` を除くコマンドの実行 | AEM アーキテクチャにより、`/bin` での偽陽性を無効にしながら、`CMDEXE` と同じレベルの保護を提供します。 |
| XSS | クロスサイトスクリプティング | クロスサイトスクリプティングとは、悪意のある JavaScript コードを通じてユーザーのアカウントまたは web ブラウジングセッションをハイジャックしようとする試みです。 |
| トラバーサル | ディレクトリトラバーサル | ディレクトリトラバーサルとは、機密情報を取得することを目的として、システム全体の権限フォルダーを移動しようとする試みです。 |
| USERAGENT | 攻撃ツール | 攻撃ツールでは、自動化されたソフトウェアを使用して、セキュリティの脆弱性を特定したり、発見された脆弱性の悪用を試みたりします。 |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI 攻撃では、Log4J バージョン 2.16.0 より前の [Log4Shell 脆弱性](https://ja.wikipedia.org/wiki/Log4Shell)を悪用しようと試みます |
| CVE | CVE | CVE （Common Vulnerabilities and Exposures）を特定するためのフラグ。 常にフラグ `CVE-<CVE Number>` と組み合わせます。 Adobeが保護するCVEについて詳しくは、Adobeにお問い合わせください。 |

#### 疑わしいトラフィック

| **フラグ ID** | **フラグ名** | **説明** |
|---|---|---|
| ABNORMALPATH | 異常なパス | 異常なパスは、元のパスが正規化されたパスと異なることを示します（例えば、`/foo/./bar` は `/foo/bar` に正規化されます） |
| BAD-IP | 不正な IP | `SANS` や `TORNODE` などのデータセットに含まれるか、WAF による悪意のある動作の事前検出に基づいて、悪意があると判明している IP アドレスからのリクエストを特定します |
| BHH | 不正なホップヘッダー | 不正なホップヘッダーは、不正な形式の Transfer-Encoding（TE）ヘッダーまたは Content-Length（CL）ヘッダー、適切な形式の TE および CL ヘッダーを介した HTTP スマグリングの試みを示します |
| CODEINJECTION | コードインジェクション | コードインジェクションとは、ユーザー入力による任意のアプリケーションコードコマンドを通じて、ターゲットシステムを制御したり損傷したりしようとする試みです。 |
| COMPRESSED | 検出された圧縮 | POST リクエスト本文が圧縮されており、検査できません。 例えば、`Content-Encoding: gzip` リクエストヘッダーが指定され、POST 本文がプレーンテキストではない場合です。 |
| RESPONSESPLIT | HTTP 応答分割 | HTTP 応答にヘッダーを挿入するために CRLF 文字をアプリケーションへの入力として送信するタイミングを指定します。 |
| NOTUTF8 | 無効なエンコーディング | 無効なエンコーディングでは、サーバーがリクエストの悪意のある文字をレスポンスに変換し、サービス拒否または XSS を引き起こす可能性があります。 |
| MALFORMED-DATA | リクエスト本文内の不正なデータ | 「Content-Type」リクエストヘッダーに従って不正な形式である POST、PUT、PATCH リクエストの本文です。 例えば、「Content-Type: application/x-www-form-urlencoded」リクエストヘッダーが指定され、JSON である POST 本文が含まれているとします。 これは、多くの場合、プログラミングエラーや、自動リクエスト、悪意のあるリクエストです。 エージェント 3.2 以降が必要です。 |
| SANS | 悪意のある IP トラフィック | [SANS Internet Storm Center](https://isc.sans.edu/) には、悪意のあるアクティビティにエンゲージしたと報告された IP アドレスのリストが含まれます。 |
| NO-CONTENT-TYPE | 「Content-Type」リクエストヘッダーなし | 「Content-Type」リクエストヘッダーを持たない POST、PUT または PATCH リクエストです。 この場合、アプリケーションサーバーでは、デフォルトで「Content-Type: text/plain; charset=us-ascii」を想定する必要があります。 自動化された悪意のあるリクエストの多くには、「Content-Type」が欠落している可能性があります。 |
| NOUA | ユーザーエージェントなし | リクエストに「User-Agent」ヘッダーが含まれていなかったか、ヘッダー値が設定されていなかったことを示します。 |
| NULLBYTE | Null バイト | 通常、Null バイトはリクエストには表示されず、リクエストの形式が正しくなく、悪意がある可能性があることを示します。 |
| OOB-DOMAIN | アウトオブバンドドメイン | アウトオブバンドドメインは通常、ネットワークアクセスが許可されている脆弱性を識別するために、侵入テストで使用されます。 |
| PRIVATEFILE | プライベートファイル | プライベートファイルは、Apache `.htaccess` ファイルや、機密情報の漏洩につながる可能性のある設定ファイルなど、本来、部外秘のものです。 |
| スキャナー | スキャナー | 一般に使用されるスキャンサービスおよびツールを指定します。 |

#### その他の交通

| **フラグ ID** | **フラグ名** | **説明** |
|---|---|---|
| DATACENTER | データセンター | リクエストの発信元が既知のホスティングプロバイダーであることを識別します。 このタイプのトラフィックは、通常、実際のエンドユーザーに関連付けられません。 |
| DOUBLEENCODING | 二重エンコーディング | 二重エンコーディングでは、HTML 文字の二重エンコーディングを回避する方法を確認します |
| JSON-ERROR | JSON エンコーディングエラー | 「Content-Type」リクエストヘッダー内に JSON を含むように指定されている POST、PUT、PATCH リクエスト本文には、JSON 解析エラーが含まれています。 これは、多くの場合、プログラミングエラー、自動リクエストまたは悪意のあるリクエストに関係しています。 |
| TORNODE | Tor トラフィック | Tor は、ユーザーの ID を隠すソフトウェアです。 Tor トラフィックのスパイクは、攻撃者がその場所をマスクしようとしていることを示す可能性があります。 |
| XML-ERROR | XML エンコーディングエラー | 「Content-Type」リクエストヘッダー内に XML を含むように指定されているが、XML 解析エラーが含まれている POST、PUT または PATCH リクエスト本文です。 これは、多くの場合、プログラミングエラー、自動リクエストまたは悪意のあるリクエストに関係しています。 |

## 考慮事項 {#considerations}

* 2 つの競合するルールを作成した場合は、許可ルールが常にブロックルールより優先されます。 例えば、特定のパスをブロックするルールと、特定の1つのIP アドレスを許可するルールを作成した場合、ブロックされたパス上のそのIP アドレスからのリクエストは許可されます。

* ルールが一致してブロックされた場合、CDN は `406` リターンコードで応答します。

* 設定ファイルには、Git リポジトリにアクセスできる人なら誰でも読み取ることができるため、シークレットは含まれていません。

* Cloud Manager で定義された IP 許可リストは、トラフィックフィルタールールよりも優先されます。

* WAF ルールの一致は、CDN のミスおよびパスに関して CDN ログにのみ表示され、ヒットには表示されません。

## ルールの例 {#examples}

ルールの例をいくつか以下に示します。 レート制限ルールの例については、さらに下の[レート制限ルール](#rate-limit-rules)の節を参照してください。

**例 1**

このルールは、**IP192.168.1.1** からのリクエストをブロックします。

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
     rules:
       - name: "block-request-from-ip"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
         action:
           type: block
```

**例 2**

このルールは、Chromeを含むUser-Agentを使用したパブリッシュ時のパス `/helloworld`へのリクエストをブロックします。

```
kind: "CDN"
version: "1"
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

このルールは、パス `/block-me` へのリクエストをパブリッシュ時にブロックし、`SQLI` または `XSS` パターンに一致するすべてのリクエストをブロックします。 この例には、`SQLI`および`XSS` [WAF フラグ ](#waf-flags-list)を参照するWAF トラフィックフィルタールールが含まれているため、別のライセンスが必要です。

```
kind: "CDN"
version: "1"
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

特定の条件に基づいて、受信リクエストの一定のレートを超えた場合にトラフィックをブロックすることが望ましい場合があります。 `rateLimit` プロパティの値を設定すると、ルール条件に一致するリクエストのレートが制限されます。

レート制限ルールでは、WAF フラグを参照できません。 Sites と Forms のすべてのお客様が使用できます。

レート制限は、CDN POP ごとに計算されます。 例えば、モントリオール、マイアミ、ダブリンの POP のトラフィックレートがそれぞれ 1 秒あたり 80、90、120 リクエストだとします。 さらに、レート制限ルールが上限 100 に設定されています。 その場合、ダブリンへのトラフィックのみがレート制限されます。

レート制限は、エッジに到達するトラフィック、接触チャネルに到達するトラフィック、またはエラーの数に基づいて評価されます。

### rateLimit構造体 {#ratelimit-structure}

| **プロパティ** | **タイプ** | **デフォルト** | **意味** |
|---|---|---|---|
| limit | 10～10000 の整数 | 必須 | ルールがトリガーされる、1 秒あたりのリクエスト数のリクエストレート（CDN POP あたり）です。 |
| window | 整数列挙：1、10 または 60 | 10 | リクエストレートが計算されるサンプリングウィンドウ（秒単位）です。 カウンターの精度は、ウィンドウのサイズによって異なります（ウィンドウが大きいほど精度が高くなります）。 例えば、1 秒のウィンドウでは 50％の精度、60 秒のウィンドウでは 90％の精度が期待できます。 |
| penalty | 60～3600 の整数 | 300（5 分） | 一致するリクエストがブロックされる期間（秒単位）です（最も近い分に四捨五入）。 |
| 回数 | すべて、取得、エラー | すべて | エッジトラフィック（すべて）、接触チャネルトラフィック（取得）、またはエラーの数（エラー）に基づいて評価します。 |
| groupBy | 配列[ゲッター] | なし | レート制限カウンターは、一連のリクエストプロパティ（clientIpなど）によって集計されます。 |

### 例 {#ratelimiting-examples}

**例 1**

このルールは、過去10秒間に平均60 req/秒（CDN POPあたり）を超えた場合、クライアントを5分間ブロックします。

```
kind: "CDN"
version: "1"
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

高度なシナリオの追加のコードスニペットについては、「[CDN Configuration Snippets for Common Scenarios](/help/implementing/dispatcher/cdn-configuration-snippets-common-scenarios.md)」の記事を参照してください。

## CVE ルール {#cve-rules}

WAFのライセンスが付与されている場合、Adobeでは、多くの既知のCVE （一般的な脆弱性とエクスポージャー）に対して保護するためのブロッキングルールが自動的に適用され、新しいCVEが検出された直後に追加されます。 お客様は、CVE ルール自体を設定しません。

トラフィックリクエストがCVEに一致する場合、対応するCDN ログエントリに表示されます。

特定のCVEに関する質問がある場合や、特定のCVE ルールを無効にしたい場合は、Adobe サポートにお問い合わせください。

## トラフィックフィルタールールアラート {#traffic-filter-rules-alerts}

5 分間に 10 回トリガーされた場合にアクションセンター通知を送信するルールを設定できます。 このようなルールにより、特定のトラフィックパターンが発生した際にアラートが表示されるので、必要な措置を講じることができます。 特定のルールに対してアラートがトリガーされると、翌日（UTC）まで再度トリガーされません。

メールを受信するために必要な通知プロファイルの設定方法などについて詳しくは、[アクションセンター](/help/operations/actions-center.md)を参照してください。

![アクションセンターの通知](/help/security/assets/traffic-filter-rules-actions-center-alert.png)


アラートプロパティは、すべてのアクションタイプ（許可、ブロック、ログ）のアクションノードに適用できます。

```
kind: "CDN"
version: "1"
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

## 発信元でのデフォルトのトラフィックスパイクの警告 {#traffic-spike-at-origin-alert}

同じIP アドレスからの高トラフィックがオリジンに達すると、[ アクション センター](/help/operations/actions-center.md)のメール通知で警告が表示され、DDoS攻撃が疑われます。

このしきい値を満たした場合、AdobeはそのIP アドレスからのトラフィックをブロックします。レート制限トラフィックフィルタールールの設定など、オリジンを保護するためのさらなる対策を講じます。 ガイド付きのチュートリアルについては、「[ トラフィックルールを使用したDoSおよびDDoS攻撃のブロック」チュートリアル ](#tutorial-blocking-DDoS-with-rules)を参照してください。

システムはデフォルトでこのアラートを有効にしますが、*defaultTrafficAlerts* プロパティを使用して無効にできます。このプロパティはfalseに設定されます。 アラートがトリガーされると、翌日（UTC）まで再度トリガーされません。

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
   defaultTrafficAlerts: false
```

## CDN ログ {#cdn-logs}

AEM as a Cloud Service では、ユーザーが CDN ログにアクセスできるようになっています。このログは、キャッシュヒット率の最適化などのユースケースやトラフィックフィルタールールの設定に役立ちます。 CDN ログは、オーサーサービスやパブリッシュサービスの選択時に Cloud Manager の&#x200B;**ログをダウンロード**&#x200B;ダイアログに表示されます。

CDN ログは最大5分遅れます。

`rules` プロパティは、一致するトラフィックフィルタールールを次のパターンで示します。

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

例：

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

ルールは次のように動作します。

* 一致するルールの、ユーザーが宣言したルール名が `match` 属性にリストされます。
* `action` 属性は、ルールがブロック、許可、ログのいずれであるかを決定します。
* WAF がライセンス取得済みで有効になっている場合、`waf` 属性には検出されたすべての WAF フラグ（SQLI など）がリストされます。 この動作は、WAF フラグがルールにリストされているかどうかに関係なくtrueです。 このロギングは、insightを宣言する新しいルールに提供するためのものです。
* ユーザーが宣言したルールが一致せず、WAF ルールも一致しない場合、`rules` プロパティは空白になります。

前述のように、WAF ルールの一致は、CDN のミスとパスに関して CDN ログにのみ表示され、ヒットには表示されません。

以下の例では、サンプル `cdn.yaml` と 2 つの CDN ログエントリを示しています。


```
kind: "CDN"
version: "1"
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
| *ttfb* | *Time To First Byte* の略称です。 リクエストの開始から、応答本文のストリーミングが開始される前の時点までの時間間隔です。 |
| *cli_ip* | クライアントの IP アドレスです。 |
| *cli_country* | クライアント国の 2 文字の [ISO 3166-1](https://ja.wikipedia.org/wiki/ISO_3166-1) alpha-2 国コードです。 |
| *rid* | リクエストを一意に識別するために使用されるリクエストヘッダーの値です。 |
| *req_ua* | 特定の HTTP リクエストの作成を担当するユーザーエージェントです。 |
| *host* | リクエストの対象となる証明機関です。 |
| *URL* | クエリパラメーターを含む完全なパスです。 |
| *method* | 「GET」や「POST」など、クライアントによって送信される HTTP メソッドです。 |
| *res_ctype* | リソースの元のメディアタイプを示すために使用される Content-Type です。 |
| *cache* | キャッシュの状態です。 指定できる値は、HIT、MISS、PASS です |
| *status* | 整数値としての HTTP ステータスコードです。 |
| *res_age* | 応答が（すべてのノードで）キャッシュされた時間です（秒単位）。 |
| *pop* | CDN キャッシュサーバーのデータセンターです。 |
| *rules* | 一致するルールの名前です。<br><br>また、一致がブロックされたかどうかも示します。 <br><br>例：「`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`」<br><br>一致するルールがない場合は空です。 |

## ダッシュボードツール {#dashboard-tooling}

アドビでは、Cloud Manager 経由でダウンロードされた CDN ログを取り込むために、ダッシュボードツールをコンピューターにダウンロードするメカニズムを提供します。 トラフィックを分析し、WAF ルールを含め、宣言する適切なトラフィックフィルタールールの決定に役立てるには、このツールを使用します。

ダッシュボードツールでは、[AEMCS-CDN-Log-Analysis-Tooling](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling) Github リポジトリから直接クローンを作成できます。

ダッシュボードツールの具体的な使用方法については、[チュートリアル](#tutorial)を参照してください。

## 推奨されるスタータールール {#recommended-starter-rules}

アドビでは、以下のトラフィックフィルタールールから始めて、時間の経過と共に絞り込むことをお勧めします。 *標準ルール*&#x200B;はSitesまたはForms ライセンスで利用できますが、*WAF ルール*&#x200B;にはExtended Security （旧称WAF-DDoS Protection）またはExtended Security for Healthcare （旧称Enhanced Security）ライセンスが必要です。

### 推奨される標準ルール {#recommended-nonwaf-starter-rules}

次のルールから開始します。

1. レート制限（ログモード）：
   * 特定の IP からのトラフィックがレート制限を超えた場合にログに記録します。 アラートを受信していないことを検証した後、ブロックモードに変更します。アラートを受信した場合は、制限値が低すぎることを示します。
2. 特定の国（ブロックモード）：
   * 特定の国からのトラフィックをブロックします（ビジネス要件に基づいて国コードを変更します）

```
kind: "CDN"
version: "1"
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

### 推奨される WAF ルール {#recommended-waf-starter-rules}

既存の設定に次のルールを追加します。

1. ATTACK-FROM-BAD-IP フラグ（ブロックモード）：
   * 疑わしいパターン（[WAF フラグリスト](#waf-flags-list)内の一部を含む）に一致し、悪意があると判明している IP アドレスから発信されたトラフィックをすぐにブロックします。
   * ATTACK-FROM-BAD-IP フラグは、両方の条件（パターンマッチと既知の悪意のあるIP）を満たし、偽陽性のリスクを最小限に抑えます。 したがって、このルールをブロッキングモードで安全かつ即座に適用できます。
2. ATTACK フラグ（ログモード）：
   * 疑わしいパターンに一致するが、既知の悪意のある IP アドレスから発信されたものではないトラフィックを（ブロックするのではなく）最初にログに記録します。 ブロックするのではなくログに記録するというこの慎重なアプローチは、正当なトラフィックを誤ってブロックしてしまうこと（誤検知）を回避するのに役立ちます。
   * 正当な要求が正しくフラグ付けされていないことを確認するには、このルールをデプロイした後でCDN ログを分析します。 正当なトラフィックが影響を受けていないことが確認したら、ブロックモードに切り替えます。

>[!NOTE]
>
> 経験は、ATTACK フラグに関連する偽陽性がまれであることを示しています。 したがって、実用的な戦略は、疑わしいトラフィックをすべて即座にブロックし、CDN ログ分析を使用して、正当なトラフィックに対する許可ルールを特定して導入することです。 各組織は、独自のリスク許容度を評価し、不用意に正当な要求をブロックするリスクから、より優れた保護の利点を比較検討します。

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

### 従来の推奨される WAF ルール {#previous-waf-starter-rules}

2025年7月より前に、アドビでは、以下にリストする WAF ルールを推奨していましたが、これらは引き続き有効で、悪意のあるトラフィックに対する防御に効果的です。 新しい推奨ルールへの移行に関する考慮事項について詳しくは、チュートリアルを参照してください。

+++ 展開すると、従来の推奨される WAF ルールが表示されます。

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

+++

## チュートリアル {#tutorial}

WAF ルールを含むトラフィックフィルタールールに関する実用的な知識と経験を得るには、[一連のチュートリアル ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview)を進めてください。

チュートリアルには、次が含まれます。

* 標準およびWAF トラフィックフィルタールールの概要。
* サービス拒否（DoS）などの攻撃をブロックするには、推奨標準ルールとWAF トラフィックフィルタールールを設定します。
* Cloud Manager設定パイプラインを使用したルールのデプロイ。
* ツールを使用してルールをテストし、悪意のあるトラフィックをシミュレートする。
* Log Analysis Toolingを使用した結果の分析。
* ベストプラクティス。
