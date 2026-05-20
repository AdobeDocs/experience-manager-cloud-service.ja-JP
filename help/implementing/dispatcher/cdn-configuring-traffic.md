---
title: CDN でのトラフィックの設定
description: 設定ファイルでルールとフィルターを宣言し、Cloud Manager 設定パイプラインを使用して CDN にデプロイすることで、CDN トラフィックを設定する方法について説明します。
feature: Dispatcher
exl-id: e0b3dc34-170a-47ec-8607-d3b351a8658e
role: Admin
source-git-commit: 8371bceaf116cdcd4e0542dd1b8d772d2d12a05d
workflow-type: tm+mt
source-wordcount: '2637'
ht-degree: 76%

---


# CDN でのトラフィックの設定 {#cdn-configuring-cloud}

AEM as a Cloud Service では、受信リクエストまたは送信応答の特性を変更する、[アドビが管理する CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) レイヤーで設定可能な機能のコレクションを提供します。 このページで詳しく説明する次のルールは、次の動作を実現するために宣言できます。

* [リクエスト変換](#request-transformations) - ヘッダー、パスおよびパラメーターなど、受信リクエストの側面を変更します。
* [応答変換](#response-transformations) - クライアント（web ブラウザーなど）に戻る途中のヘッダーを変更します。
* [サーバーサイドのリダイレクト](#server-side-redirectors) - ブラウザーのリダイレクトをトリガーします。
* [接触チャネルセレクター](#origin-selectors) - 別の接触チャネルバックエンドにプロキシ処理します。

また、CDN で許可または拒否するトラフィックを制御するトラフィックフィルタールール（WAF を含む）も CDN で設定できます。 この機能は既にリリースされています。詳しくは、[WAF ルールを含むトラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)ページを参照してください。

さらに、CDN でその接触チャネルに接続できない場合は、自己ホスト型のカスタムエラーページ（その後レンダリングされる）を参照するルールを書き込むことができます。 詳しくは、[CDN エラーページの設定](/help/implementing/dispatcher/cdn-error-pages.md)の記事を参照してください。

すべてのルールは、ソース管理の設定ファイルで宣言され、Cloud Manager の[設定パイプライン](/help/operations/config-pipeline.md)を使用してデプロイされます。 トラフィックフィルタールールを含む設定ファイルの累積サイズが 100KB を超えることはできません。

一般的なシナリオの追加のコードスニペットについては、「[CDN Configuration Snippets for Common Scenarios](/help/implementing/dispatcher/cdn-configuration-snippets-common-scenarios.md)」の記事を参照してください。

## 評価の順序 {#order-of-evaluation}

機能的には、前述の様々な機能が次のシーケンスで評価されます。

![評価の順序](/help/implementing/dispatcher/assets/order.png)

## 設定 {#initial-setup}

CDN でトラフィックを設定する前に、次のことを行う必要があります。

1. 以下の節の様々な設定スニペットを参照して、`cdn.yaml` または類似の名前のファイルを作成します。

   すべてのスニペットには、[設定パイプライン](/help/operations/config-pipeline.md#common-syntax)で説明されているこれらの共通プロパティがあります。 `kind` プロパティの値は *CDN* に設定し、`version` プロパティは *1* に設定する必要があります。

   ```
   kind: "CDN"
   version: "1"
   ```

1. [設定パイプライン](/help/operations/config-pipeline.md#folder-structure)で説明されているように、*config* または類似の名前の最上位フォルダーの下のどこかにファイルを配置します。

1. [設定パイプライン](/help/operations/config-pipeline.md#managing-in-cloud-manager)の説明に従って、Cloud Manager で設定パイプラインを作成します。

1. 設定をデプロイします。

## ルール構文 {#configuration-syntax}

以下の節で説明するルールタイプは、共通の構文を共有しています。

一般的なルール構文は、名前、`when`条件、アクションまたはアクションを含むリストエントリです。

```
- name: <name>
  when: <condition>
  action: <action>
```

[&#x200B; トラフィックフィルタールール &#x200B;](/help/security/traffic-filter-rules-including-waf.md)の各トップレベルセクション（`requestTransformations`、`responseTransformations`、`redirects`、`originSelectors`、および`trafficFilters`）は、独自のアクションタイプとプロパティのセットをサポートしています。許可される`type`値とフィールドは、そのセクションのテーブルと例で定義されますが、すべてのルールの種類で共有されるわけではありません。 `requestTransformations`や`responseTransformations`などのセクションでは、`actions` プロパティでyaml リストとして指定された複数のアクションをサポートしています。

when 句は、ドメイン、パス、クエリ文字列、ヘッダー、Cookie などのプロパティに基づいて、ルールを評価するかどうかを決定します。 構文はルールタイプ間で同じです。以下の[条件構造](#condition-structure)を参照してください。 トラフィックフィルタールール（WAFを含む）では、同じ条件の構文が使用されます。アクション、レート制限、WAF固有の動作については、[WAF ルールを含むトラフィックフィルタールール &#x200B;](/help/security/traffic-filter-rules-including-waf.md)を参照してください。

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
| **allOf** | `array[Condition]` | **AND** 操作。 リストに表示されているすべての条件が true を返す場合は true |
| **anyOf** | `array[Condition]` | **OR** 操作。 リストに表示された条件のいずれかが true を返す場合は true |

**getter**

| **プロパティ** | **タイプ** | **説明** |
|---|---|---|
| reqProperty | `string` | リクエストプロパティ。<br><br>次のいずれか：<br><ul><li>`path`：URL のフルパスをクエリパラメーターなしで返します。 （エスケープされていないバリアントには `pathRaw` を使用）</li><li>`originalPath`: クエリパラメーター（CDN リクエスト変換の前のパス）を使用せずに、リクエストの不変の元のパスを返します。</li><li>`url`：完全な URL をクエリパラメーターを含めて返します。 （エスケープされていないバリアントには `urlRaw` を使用）</li><li>`originalUrl`: クエリパラメーター（CDN リクエスト変換の前のURL）を含む、リクエストの不変の元の完全URLを返します。</li><li>`queryString`：URL のクエリ部分を返します</li><li>`method`：リクエストで使用される HTTP メソッドを返します。</li><li>`tier`：`author`、`preview` または `publish` のいずれか 1 つを返します。</li><li>`domain`：小文字のドメインプロパティ（`Host` ヘッダーで定義）を返します</li><li>`clientIp`：クライアント IP を返します。</li><li>`forwardedDomain`：`X-Forwarded-Host` ヘッダーで定義されている最初のドメインを小文字で返します。</li><li>`forwardedIp`：`X-Forwarded-For` ヘッダーの最初の IP を返します。</li><li>`clientRegion`：[ISO 3166-2](https://en.wikipedia.org/wiki/ISO_3166-2) で説明されているように、クライアントがいる地域を識別する国の下位区分コードを返します。</li><li>`clientCountry`：クライアントがいる国を識別する 2 文字のコード（[地域指標シンボル](https://en.wikipedia.org/wiki/Regional_indicator_symbol)）を返します。</li><li>`clientContinent`：クライアントがいる大陸を識別する 2 文字のコード（AF、AN、AS、EU、NA、OC、SA）を返します。</li><li>`clientAsNumber`：クライアント IP に関連付けられた[自律システム](https://en.wikipedia.org/wiki/Autonomous_system_(Internet))番号を返します。</li><li>`clientAsName`：自律システム番号に関連付けられた名前を返します。</li></ul> |
| reqHeader | `string` | 指定された名前のリクエストヘッダーを返します |
| queryParam | `string` | 指定された名前のクエリパラメーターを返します |
| reqCookie | `string` | 指定された名前の Cookie を返します |
| postParam | `string` | リクエスト本文から指定された名前の Post パラメーターを返します。 本文がコンテンツタイプ `application/x-www-form-urlencoded` の場合にのみ機能します |

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

* request プロパティ `clientIp` は、`equals`、`doesNotEqual`、`in`、`notIn` の述語でのみ使用できます。 `clientIp` は、`in` および `notIn` 述語を使用する際に IP 範囲に対して比較することができます。 次の例では、クライアント IP が IP 範囲 192.168.0.0/24（192.168.0.0～192.168.0.255）内にあるかどうかを評価する条件を実装しています。

```
when:
  reqProperty: clientIp
  in: [ "192.168.0.0/24" ]
```

* 正規表現を使用する際は、[regex101](https://regex101.com/) および [Fastly Fidle](https://fiddle.fastly.dev/) の使用をお勧めします。 また、Fastly による正規表現の処理方法について詳しくは、[fastly ドキュメント - Fastly VCL の正規表現](https://www.fastly.com/documentation/reference/vcl/regex/#best-practices-and-common-mistakes)を参照してください。

アクションノードの詳細は、ルールタイプによって異なります。概要については、以下の個々の節で説明します。

設定ルールでは、環境変数として定義された秘密鍵を参照できます（[設定秘密鍵](/help/implementing/dispatcher/cdn-credentials-authentication.md)を参照してください）。

## リクエスト変換 {#request-transformations}

リクエスト変換ルールを使用すると、受信リクエストを変更できます。 このルールは、正規表現を含む様々な一致条件に基づいて、パス、クエリパラメーターおよびヘッダー（Cookie を含む）の設定、設定解除および変更をサポートします。 また、変数を設定して、後の評価シーケンスで参照することもできます。

ユースケースは多様で、アプリケーションの簡素化やレガシー URL のマッピング用の URL の書き換えが含まれます。

前述したように、設定ファイルにはサイズ制限があるので、より大きな要件を持つ組織では `apache/dispatcher` レイヤーでルールを定義する必要があります。

設定例：

```
kind: "CDN"
version: "1"
data:
  requestTransformations:
    removeMarketingParams: true
    rules:
      - name: set-header-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: some value
      - name: set-header-with-reqproperty-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: {reqProperty: path}
      - name: unset-header-rule
        when:
          reqProperty: path
          like: /unset-header
        actions:
          - type: unset
            reqHeader: x-some-header
      - name: unset-matching-query-params-rule
        when:
          reqProperty: path
          equals: /unset-matching-query-params
        actions:
          - type: unset
            queryParamMatch: ^removeMe_.*$
      - name: unset-all-query-params-except-exact-two-rule
        when:
          reqProperty: path
          equals: /unset-all-query-params-except-exact-two
        actions:
          - type: unset
            queryParamMatch: ^(?!leaveMe$|leaveMeToo$).*$
      - name: multi-action
        when:
          reqProperty: path
          like: /multi-action
        actions:
          - type: set
            reqHeader: x-header1
            value: body set by transformation rule
          - type: set
            reqHeader: x-header2
            value: '201'
      - name: replace-html
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
            reqProperty: path
            op: replace
            match: \.html$
            replacement: ""
      - name: log-on-request
        when: "*"
        actions:
          - type: set
            logProperty: forwarded_host
            value:
              reqHeader: x-forwarded-host
```

**アクション**

次の表に、使用可能なアクションを示します。

| 名前 | プロパティ | 意味 |
|-----------|--------------------------|-------------|
| **set** | reqProperty、値 | 指定されたリクエストパラメーターを設定します（「path」プロパティのみサポートされています） |
|     | reqHeader、値 | 指定されたリクエストヘッダーを特定の値に設定します。 |
|     | queryParam、値 | 指定されたクエリパラメーターを特定の値に設定します。 |
|     | reqCookie、値 | 指定されたリクエスト cookie を特定の値に設定します。 |
|     | logProperty、値 | 指定された CDN ログプロパティを特定の値に設定します。 |
|     | var、値 | 指定された変数を特定の値に設定します。 |
| **unset** | reqProperty | 指定されたリクエストパラメーターを削除します（「path」プロパティのみサポートされています） |
|     | reqHeader、値 | 指定されたリクエストヘッダーを削除します。 |
|     | queryParam、値 | 指定されたクエリパラメーターを削除します。 |
|     | reqCookie、値 | 指定された cookie を削除します。 |
|     | logProperty、値 | 指定された CDN ログプロパティを削除します。 |
|     | var | 指定した変数を削除します。 |
|     | queryParamMatch | 指定した正規表現に一致するすべてのクエリパラメーターを削除します。 |
|     | queryParamDoesNotMatch | 指定した正規表現に一致しないすべてのクエリパラメーターを削除します。 |
| **transform** | op:replace、（reqProperty、reqHeader、queryParam、reqCookie、var のいずれか）、match、replacement | リクエストパラメーターの一部（「path」プロパティのみサポートされています）、またはリクエストヘッダー、クエリパラメーター、cookie、変数のいずれかを新しい値に置き換えます。 |
|              | op:tolower、（reqProperty、reqHeader、queryParam、reqCookie、var のいずれか） | リクエストパラメーター（「path」プロパティのみサポートされています）またはリクエストヘッダー、クエリパラメーター、Cookie、変数のいずれかを小文字の値に設定します。 |

置換アクションでは、次に示すように、キャプチャグループをサポートしています。

```
      - name: extract-country-code-from-path
        when:
          reqProperty: path
          matches: ^/([a-zA-Z]{2})(/.*|$)
        actions:
          - type: set
            var: country-code
            value:
              reqProperty: path
          - type: transform
            var: country-code
            op: replace
            match: ^/([a-zA-Z]{2})(/.*|$)
            replacement: \1
      - name: replace-jpg-with-jpeg
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
            reqProperty: path
            op: replace
            match: (.*)(\.jpg)$
            replacement: "\1\.jpeg"
```

アクションは連結できます。 例：

```
actions:
    - type: transform
      reqProperty: path
      op: replace
      match: \.html$
      replacement: ""
    - type: transform
      reqProperty: path
      op: tolower
```

### 変数 {#variables}

変数は、リクエストの変換時に設定し、後で評価シーケンスで参照することができます。 詳しくは、[評価の順序](#order-of-evaluation)を参照してください。

設定例：

```
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some_value

  responseTransformations:
    rules:
      - name: set-response-header-while-variable
        when:
          var: some_var_name
          equals: some_value
        actions:
          - type: set
            respHeader: x-some-header
            value: some header value
```

### ログプロパティ {#logproperty}

リクエストと応答の変換を使用して、CDN ログに独自のログプロパティを追加できます。

設定例：

```
requestTransformations:
  rules:
    - name: log-on-request
      when: "*"
      actions:
        - type: set
          logProperty: forwarded_host
          value:
            reqHeader: x-forwarded-host
responseTransformations:
  rules:
    - name: log-on-response
      when: '*'
      actions:
        - type: set
          logProperty: cache_control
          value:
            respHeader: cache-control
```

ログ例：

```
{
"timestamp": "2025-03-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/content/hello.png",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 200,
"res_age": 0,
"pop": "PAR",
"rules": "",
"forwarded_host": "example.com",
"cache_control": "max-age=300"
}
```

## 応答変換 {#response-transformations}

応答変換ルールを使用すると、CDN の送信応答のヘッダー、Cookie、ステータスを設定および設定解除できます。 また、リクエスト変換ルールで以前に設定された変数を参照するには、上記の例を参照してください。

設定例：

```
kind: "CDN"
version: "1"
data:
  responseTransformations:
    rules:
      - name: set-response-header-rule
        when:
          reqProperty: path
          like: /set-response-header
        actions:
          - type: set
            value: value-set-by-resp-rule
            respHeader: x-resp-header
      - name: unset-response-header-rule
        when:
          reqProperty: path
          like: /unset-response-header
        actions:
          - type: unset
            respHeader: x-header1
      - name: multi-action-response-header-rule
        when:
          reqProperty: path
          like: /multi-action-response-header
        actions:
          - type: set
            respHeader: x-resp-header-1
            value: value-set-by-resp-rule-1
          - type: set
            respHeader: x-resp-header-2
            value: value-set-by-resp-rule-2
      - name: status-code-rule
        when:
          reqProperty: path
          like: status-code
        actions:
          - type: set
            respProperty: status
            value: '410'
      - name: set-response-cookie-with-attributes-as-object
        when: '*'
        actions:
          - type: set
            respCookie: first-name
            value: first-value
            attributes:
              expires: '2025-08-29T10:00:00'
              domain: example.com
              path: /some-path
              secure: true
              httpOnly: true
              extension: ANYTHING
      - name: unset-response-cookie
        when: '*'
        actions:
          - type: unset
            respCookie: third-name
```

**アクション**

次の表に、使用可能なアクションを示します。

| 名前 | プロパティ | 意味 |
|-----------|--------------------------|-------------|
| **set** | respProperty、値 | 応答プロパティを設定します。 ステータスコードを設定するには、「status」プロパティのみをサポートします。 |
|     | respHeader、値 | 指定された応答ヘッダーを特定の値に設定します。 |
|     | respCookie、属性（有効期限、ドメイン、パス、セキュア、httpOnly、拡張子）、値 | 特定の属性を持つ指定されたリクエスト cookie を特定の値に設定します。 |
|     | logProperty、値 | 指定された CDN ログプロパティを特定の値に設定します。 |
|     | var、値 | 指定された変数を特定の値に設定します。 |
| **unset** | respHeader | 指定したヘッダーを応答から削除します。 |
|     | respCookie、値 | 指定された cookie を削除します。 |
|     | logProperty、値 | 指定された CDN ログプロパティを削除します。 |
|     | var | 指定した変数を削除します。 |

## 接触チャネルセレクター {#origin-selectors}

AEM CDN を利用して、アドビ以外のアプリケーション（おそらくパスごとまたはサブドメインごと）を含む様々なバックエンドにトラフィックをルーティングできます。

リクエストプロパティ `originalPath`と`originalUrl`は、それぞれ不変の元のパス（クエリパラメーターを含まない）と完全なURL （クエリパラメーターを含む）であり、CDN [&#x200B; リクエスト変換](#request-transformations)の前に取得されます。 評価順序の早い段階で書き換えられた値ではなく、クライアントが最初に送信した値にルールを固定する必要がある場合、`when`条件で使用します。 パスのみのマッチングには`originalPath`を使用します。クエリ文字列が条件の一部である必要がある場合は`originalUrl`を使用します（例えば、特定の最初のリクエスト URLに対するルーティングまたはフィルタリング）。

設定例：

```
kind: "CDN"
version: "1"
data:
  originSelectors:
    rules:
      - name: example-com
        when: { reqProperty: originalPath, like: /proxy* }
        action:
          type: selectOrigin
          originName: example-com
          # skipCache: true
          # headers:
          #   Authorization: ${{AUTH_TOKEN}}
    origins:
      - name: example-com
        domain: www.example.com
        # ip: '1.1.1.1'
        # forwardHost: true
        # forwardCookie: true
        # forwardAuthorization: true
        # timeout: 20
```

**アクション**

次の表に、使用可能なアクションを示します。

| 名前 | プロパティ | 意味 |
|---------------------|--------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **selectOrigin** | originName | 定義された接触チャネルの 1 つの名前。 |
|                     | skipCache（オプション、デフォルトは false） | このルールに一致するリクエストにキャッシュを使用するかどうかを示すフラグ。 デフォルトでは、応答は応答キャッシュヘッダー（例：Cache-Control または Expires）に従ってキャッシュされます |
|                     | ヘッダー（オプション、デフォルトは`{}`） | ルールがトリガーされたときに、選択したバックエンドに送信される追加のHTTP ヘッダーを含むキーと値のペア。 ヘッダー名に対応するキーとヘッダー値に対応する値を含む |
| **selectAemOrigin** | originName | 定義済みのAEM オリジンの1つの名前（サポートされている値：`static`）。 |
|                     | skipCache（オプション、デフォルトは false） | このルールに一致するリクエストにキャッシュを使用するかどうかを示すフラグ。 デフォルトでは、応答は応答キャッシュヘッダー（例：Cache-Control または Expires）に従ってキャッシュされます |
|                     | ヘッダー（オプション、デフォルトは`{}`） | ルールがトリガーされたときに、選択したバックエンドに送信される追加のHTTP ヘッダーを含むキーと値のペア。 ヘッダー名に対応するキーとヘッダー値に対応する値を含む |

**接触チャネル**

接触チャネルへの接続は SSL のみで、ポート 443 を使用します。

| プロパティ | 意味 |
|------------------|--------------------------------------|
| **name** | 「action.originName」で参照できる名前。 |
| **ドメイン** | カスタムバックエンドへの接続に使用するドメイン名。 また、SSL SNI および検証にも使用されます。 |
| **ip**（オプション、iv4 および ipv6 でサポート） | 指定した場合、「domain」ではなくバックエンドへの接続に使用されます。 SSL SNI および検証には、「domain」が引き続き使用されます。 |
| **forwardHost**（オプション、デフォルトは false） | true に設定した場合、クライアントリクエストの「Host」ヘッダーがバックエンドに渡されます。それ以外の場合は、「domain」値が「Host」ヘッダーに渡されます。 |
| **forwardCookie**（オプション、デフォルトは false） | true に設定した場合、クライアントリクエストの「cookie」ヘッダーがバックエンドに渡されます。それ以外の場合は、cookie ヘッダーが削除されます。 |
| **forwardAuthorization**（オプション、デフォルトは false） | true に設定した場合、クライアントリクエストの「Authorization」ヘッダーがバックエンドに渡されます。それ以外の場合は、Authorization ヘッダーが削除されます。 |
| **timeout**（オプション、秒単位、デフォルトは 60） | バックエンドサーバーが HTTP 応答本文の最初のバイトを配信することを CDN が待機する秒数。 また、この値は、バックエンドサーバーに対するバイトのタイムアウト間隔としても使用されます。 |

>[!IMPORTANT]
>
>**domain**&#x200B;の値に`.adobeaemcloud.com`を含めることはできません。 adobeaemcloud.com ドメインに直接プロキシすることはできません。 この制限は、不要なリクエストループから保護します。 AEM as a Cloud Service環境にトラフィックをプロキシするには、代わりに、AEMaaCS環境にインストールされている[&#x200B; カスタムドメイン &#x200B;](#proxying-to-aemaacs)をオリジンバックエンドとして使用します。

### カスタムドメインをAEM静的層にプロキシ化する {#proxy-custom-domain-static}

オリジン セレクターを使用すると、[&#x200B; フロントエンドパイプライン &#x200B;](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)を使用してデプロイされたAEMの静的コンテンツにAEM パブリッシュトラフィックをルーティングできます。 ユースケースには、ページと同じドメイン（例：example.com/static）または明示的に異なるドメイン（例：static.example.com）で静的リソースを提供することが含まれます。

これを実現できるオリジンセレクタールールの例を以下に示します。

```
kind: CDN
version: '1'
data:
  originSelectors:
    rules:
      - name: select-aem-static-origin
        when:
          reqProperty: domain
          equals: static.example.com
        action:
          type: selectAemOrigin
          originName: static
```

### Edge Delivery Service に対するプロキシ処理 {#proxying-to-edge-delivery}

AEM パブリッシュから AEM Edge Delivery Service にトラフィックをルーティングするために、オリジンセレクターの使用が必要になることがあります。

* 一部のコンテンツは AEM パブリッシュで管理するドメインによって配信され、同じドメインの他のコンテンツは Edge Delivery Service によって配信されます。
* Edge Delivery Service で配信されるコンテンツでは、トラフィックフィルタールールやリクエスト／応答の変換など、設定パイプラインを通じてデプロイされるルールのメリットを得ることができます。
* Edge Delivery 設定パイプラインを使用すると、`trafficFilters`、`originSelectors`、`redirects` などのルールを定義して、アドビが管理する CDN 設定を指定できます。<!-- https://wiki.corp.adobe.com/pages/editpage.action?pageId=3610084282 -->

これを実現できるオリジンセレクタールールの例を以下に示します。

```
kind: CDN
version: '1'
data:
  originSelectors:
    rules:
      - name: select-edge-delivery-services-origin
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqProperty: domain
              equals: <Production Host>
            - reqProperty: path
              matches: "^(/scripts/.*|/styles/.*|/fonts/.*|/blocks/.*|/icons/.*|.*/media_.*|/favicon.ico)"
        action:
          type: selectOrigin
          originName: aem-live
    origins:
      - name: aem-live
        domain: main--repo--owner.aem.live
```

>[!NOTE]
>
>アドビが管理する CDN が使用されているので、Edge Delivery Service の[プッシュ無効化の設定ドキュメント](https://www.aem.live/docs/byo-dns#setup-push-invalidation)に従って、**管理対象**&#x200B;モードでプッシュ無効化を設定する必要があります。


### AEMaaCS環境へのプロキシ {#proxying-to-aemaacs}

`adobeaemcloud.com` ドメインをCDN設定のオリジンとして直接使用することはできません。 これを行うと、不要なリクエストループから保護するために拒否されます（ドメインに`.adobeaemcloud.com`を含めることはできません）。 これは、Edge Delivery サイト用にインストールされたドメインからルーティングする場合にも当てはまります。

カスタムドメイン （`www.example.com`）が既にAEMaaCS環境にインストールされている場合、デフォルトのルーティングはCDN ルールなしでAEM バックエンドにルーティングされます。 （例えば、`pXXXX-eYYYY`から`pXXXX-eZZZZ`まで）またはEdge Delivery サイトからAEMaaCS環境への相互環境のルーティングが必要な場合は、オリジン セレクターを使用します。

このような場合（例えば、`/graphql`などの特定のパスをバックエンドにルーティングするために）AEM as a Cloud Service環境にトラフィックをプロキシするには、AEMaaCS環境にカスタムドメインをインストールし、そのカスタムドメインをCDN設定のオリジンとして使用します。

**例：** AEM パブリッシュ層が`publish-pXXXXX-eYYYYY.adobeaemcloud.com`に到達できる場合は、`originSelectors`でそのドメインを使用しないでください。 代わりに：

1. パブリッシュサービスを指すカスタムドメイン（例：`aem-publish-origin.example.com`）をAEMaaCS環境にインストールします。
2. CDN設定で、そのカスタムドメインを持つオリジンを定義し、目的のパス（例：`/graphql`）をそのオリジンにルーティングします。

```
kind: CDN
version: '1'
data:
  originSelectors:
    rules:
      - name: graphql-to-aem-publish
        when:
          allOf:
            - reqProperty: domain
              equals: www.example.com
            - reqProperty: originalPath
              like: /graphql*
        action:
          type: selectOrigin
          originName: aem-publish-origin
    origins:
      - name: aem-publish-origin
        domain: aem-publish-origin.example.com
```


## サーバーサイドのリダイレクト {#server-side-redirectors}

301、302 および同様のクライアントサイドリダイレクトに対して、クライアントサイドのリダイレクトルールを使用できます。 ルールが一致する場合、CDN は応答として、ステータスコードとメッセージ（例：HTTP/1.1 301 Moved Permanently）、および場所ヘッダーセットを含むステータス行で応答します。

絶対位置と固定値を持つ相対位置の両方が使用されます。

トラフィックフィルタールールを含む設定ファイルの累積サイズが 100KB を超えることはできません。

設定例：

```
kind: "CDN"
version: "1"
data:
  redirects:
    rules:
      - name: redirect-absolute
        when: { reqProperty: originalPath, equals: "/page.html" }
        action:
          type: redirect
          status: 301
          location: https://example.com/page
      - name: redirect-relative
        when: { reqProperty: originalPath, equals: "/anotherpage.html" }
        action:
          type: redirect
          location: /anotherpage
```

| 名前 | プロパティ | 意味 |
|-----------|--------------------------|-------------|
| **リダイレクト** | location | 「Location」ヘッダーの値。 |
|     | ステータス（オプション、デフォルトは 301） | リダイレクトメッセージで使用される HTTP ステータス（デフォルトでは 301）で、許可されている値は 301、302、303、307、308 です。 |

リダイレクトの場所は、文字列リテラル（例：https://www.example.com/page）か、必要に応じて変換されるプロパティ（例：path）の結果のどちらかで、次の構文で表されます。

```
redirects:
  rules:
    - name: country-code-redirect
      when: { reqProperty: path, like: "/" }
      action:
        type: redirect
        location:
          reqProperty: clientCountry
          transform:
            - op: replace
              match: '^(.*)$'
              replacement: 'https://www.example.com/\1/home'
            - op: tolower
    - name: www-redirect
      when: { reqProperty: domain, equals: "example.com" }
      action:
        type: redirect
        location:
          reqProperty: url
          transform:
            - op: replace
              match: '^/(.*)$'
              replacement: 'https://www.example.com/\1'
```
