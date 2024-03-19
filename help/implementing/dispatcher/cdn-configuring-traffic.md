---
title: CDN でのトラフィックの設定
description: 設定ファイルでルールとフィルターを宣言し、Cloud Manager 設定パイプラインを使用して CDN にデプロイすることで、CDN トラフィックを設定する方法について説明します。
feature: Dispatcher
source-git-commit: 0a0c9aa68b192e8e2a612f50a58ba5f9057c862d
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 2%

---


# CDN でのトラフィックの設定 {#cdn-configuring-cloud}

>[!NOTE]
>この機能は、まだ一般には利用できません。 早期採用プログラムに参加するには、E メールを送信します。 `aemcs-cdn-config-adopter@adobe.com` および使用例を説明します。

AEMas a Cloud Serviceオファーでは、 [Adobeが管理する CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) 受信要求または送信応答の特性を変更するレイヤー。 このページで詳しく説明する次のルールは、次の動作を実現するように宣言できます。

* [リクエスト変換](#request-transformations)  — ヘッダー、パス、パラメーターなど、受信リクエストの側面を変更します。
* [応答変換](#response-transformations)  — クライアントに戻る途中のヘッダー（Web ブラウザーなど）を変更します。
* [クライアント側リダイレクター](#client-side-redirectors)  — ブラウザーのリダイレクトのトリガー。
* [接触チャネルセレクター](#origin-selectors)  — 別の接触チャネルバックエンドへのプロキシ。

また、CDN で設定できるのはトラフィックフィルタールール（WAF を含む）で、CDN で許可または拒否されるトラフィックを制御します。 この機能は既にリリースされており、詳しくは、 [WAF ルールを含むトラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md) ページに貼り付けます。

さらに、CDN が接触チャネルと通信できない場合は、自己ホスト型カスタムエラーページ（その後レンダリングされる）を参照するルールを記述できます。 詳しくは、 [CDN エラーページの設定](/help/implementing/dispatcher/cdn-error-pages.md) 記事。

ソース管理下の設定ファイルで宣言されているこれらのルールはすべて、 [Cloud Manager の設定パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). 設定ファイルの累積サイズは 100 KB を超えないことに注意してください。

## 評価の順序 {#order-of-evaluation}

機能的には、前述の様々な機能は次の順序で評価されます。

![画像](/help/implementing/dispatcher/assets/order.png)

## 設定 {#initial-setup}

CDN でトラフィックを設定する前に、次の手順を実行する必要があります。

* まず、Git プロジェクトの最上位フォルダーに次のフォルダーとファイル構造を作成します。

```
config/
     cdn.yaml
```

* 次に、 `cdn.yaml` 設定ファイルには、メタデータと以下の例で説明するルールの両方を含める必要があります。

## リクエスト変換 {#request-transformations}

リクエスト変換ルールを使用すると、受信リクエストを変更できます。 このルールは、正規表現を含む様々な一致条件に基づく、パス、クエリパラメーター、ヘッダー（Cookie を含む）の設定、設定解除および変更をサポートします。 また、変数を設定し、後で評価順序で参照することもできます。

使用例は様々で、アプリケーションを簡素化またはレガシー URL をマッピングするために、URL の書き換えが含まれます。

前述のように、サイズは設定ファイルに制限があるので、より大きな要件を持つ組織では、 `apache/dispatcher` レイヤー。

設定例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:  
  experimental_requestTransformations:
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
 
      - name: unset-header-rule
        when:
          reqProperty: path
          like: /unset-header
        actions:
          - type: unset
            reqHeader: x-some-header
 
      - name: set-query-param-rule
        when:
          reqProperty: path
          equals: /set-query-param
        actions:
          - type: set
            queryParam: someParam
            value: someValue
 
      - name: unset-query-param-rule
        when:
          reqProperty: path
          equals: /unset-query-param
        actions:
          - type: unset
            queryParam: someParam
 
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
 
      - name: set-req-cookie-rule
        when:
          reqProperty: path
          equals: /set-req-cookie
        actions:
          - type: set
            reqCookie: someParam
            value: someValue
 
      - name: unset-req-cookie-rule
        when:
          reqProperty: path
          equals: /unset-req-cookie
        actions:
          - type: unset
            reqCookie: someParam
 
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some value
 
      - name: unset-variable-rule
        when:
          reqProperty: path
          equals: /unset-variable
        actions:
          - type: unset
            var: some_var_name
 
      - name: replace-segment
        when:
          reqProperty: path
          like: /replace-segment/*
        actions:
          - type: replace
            reqProperty: path
            match: /replace-segment/
            value: /segment-was-replaced/
 
      - name: replace-extension
        when:
          reqProperty: path
          like: /replace-extension/*.html
        actions:
          - type: replace
            reqProperty: path
            match: \.html
            value: ''
 
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
```

**アクション**

次の表に、使用可能なアクションを示します。

| 名前 | プロパティ | 意味 |
|-----------|--------------------------|-------------|
| **設定** | reqHeader, value | 指定したヘッダーに指定した値を設定します。 |
|     | queryParam、value | 指定されたクエリパラメーターに指定された値を設定します。 |
|     | reqCookie、値 | 指定された cookie に指定された値を設定します。 |
|     | var, value | 指定した変数に指定した値を設定します。 |
| **未設定** | reqHeader | 指定したヘッダーを削除します。 |
|         | queryParam | 指定したクエリパラメーターを削除します。 |
|         | reqCookie | 指定した Cookie を削除します。 |
|         | var | 指定した変数を削除します。 |
|         | queryParamMatch | 指定した正規表現に一致するすべてのクエリパラメーターを削除します。 |
| **置換** | reqProperty, match, value | リクエストプロパティの一部を新しい値に置き換えます。 現在、「path」プロパティのみがサポートされています。 |

### 変数 {#variables}

変数は、リクエストの変換時に設定し、後で評価シーケンスで参照することができます。 詳しくは、 [評価順序](#order-of-evaluation) 図を参照してください。

設定例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:   
  experimental_requestTransformations:
    rules:
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some_value
 
  experimental_responseTransformations:
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

## 応答変換 {#response-transformations}

応答変換ルールを使用すると、CDN の送信応答のヘッダーを設定および設定解除できます。 また、リクエスト変換ルールで以前に設定された変数を参照するには、上記の例を参照してください。

設定例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  experimental_responseTransformations:
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
 
      # Example: Multi-action on response header
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
```

**アクション**

次の表に、使用可能なアクションを示します。

| 名前 | プロパティ | 意味 |
|-----------|--------------------------|-------------|
| **設定** | reqHeader, value | 指定されたヘッダーに応答内の指定された値を設定します。 |
| **未設定** | respHeader | 指定したヘッダーを応答から削除します。 |

## 接触チャネルセレクター {#origin-selectors}

AEM CDN を利用して、Adobe以外のアプリケーション（おそらくパスごとまたはサブドメインごと）を含む様々なバックエンドにトラフィックをルーティングできます。

設定例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_originSelectors:
    rules:
      - name: example-com
        when: { reqProperty: path, like: /proxy-me* }
        action:
          type: selectOrigin
          originName: example-com
          # useCache: false
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
|-----------|--------------------------|-------------|
| **selectOrigin** | originName | 定義された起源の 1 つの名前。 |
|     | useCache （オプション、デフォルトは true） | このルールに一致する要求にキャッシュを使用するかどうかを示すフラグ。 |

**起源**

オリジンへの接続は SSL のみで、ポート 443 を使用します。

| プロパティ | 意味 |
|------------------|--------------------------------------|
| **name** | 「action.originName」で参照できる名前。 |
| **ドメイン** | カスタムバックエンドへの接続に使用するドメイン名。 また、SSL SNI および検証にも使用されます。 |
| **ip** （オプション、サポートされる iv4 および ipv6） | 指定した場合、「domain」ではなくバックエンドへの接続に使用されます。 SSL SNI および検証には、「ドメイン」が引き続き使用されます。 |
| **forwardHost** （オプション、デフォルトは false） | true に設定した場合、クライアントリクエストの「Host」ヘッダーがバックエンドに渡されます。それ以外の場合は、「domain」値が「Host」ヘッダーに渡されます。 |
| **forwardCookie** （オプション、デフォルトは false） | true に設定した場合、クライアントリクエストの「Cookie」ヘッダーがバックエンドに渡されます。それ以外の場合は、Cookie ヘッダーが削除されます。 |
| **forwardAuthorization** （オプション、デフォルトは false） | true に設定した場合、クライアントリクエストの「Authorization」ヘッダーがバックエンドに渡されます。それ以外の場合は、Authorization ヘッダーが削除されます。 |
| **timeout** （オプション、秒単位、デフォルトは 60） | バックエンドサーバーが HTTP 応答本文の最初のバイトを配信するのを CDN が待機する秒数。 また、この値は、バックエンドサーバーに対するバイトのタイムアウト間隔としても使用されます。 |

## クライアント側リダイレクター {#client-side-redirectors}

301、302 および同様のクライアント側リダイレクトに対して、クライアント側のリダイレクトルールを使用できます。 ルールが一致する場合、CDN は応答として、ステータスコードとメッセージ（例：HTTP/1.1 301 Moved Permanently）、およびロケーションヘッダーセットを含むステータス行を使用して応答します。

絶対位置と固定値を持つ相対位置の両方が許可されます。

設定例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_redirects:
    rules:
      - name: redirect-absolute
        when: { reqProperty: path, equals: "/page.html" }
        action:
          type: redirect
          status: 301
          location: https://example.com/page
      - name: redirect-relative
        when: { reqProperty: path, equals: "/anotherpage.html" }
        action:
          type: redirect
          location: /anotherpage
```

| 名前 | プロパティ | 意味 |
|-----------|--------------------------|-------------|
| **redirect** | location | 「Location」ヘッダーの値。 |
|     | status （オプション、デフォルトは 301） | リダイレクトメッセージで使用される HTTP ステータス（デフォルトでは 301）。許可されている値は 301、302、303、307、308 です。 |
