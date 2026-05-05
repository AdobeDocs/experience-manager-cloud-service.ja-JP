---
title: 一般的なシナリオのCDN設定スニペット
description: Adobeで管理されているCDNおよびお客様が管理するCDN設定のコピー可能なYAML パターン（エッジ認証、リダイレクト、キャッシュのバリエーション、トラフィックシェーピング、レート制限など）。
feature: Dispatcher
role: Admin
source-git-commit: ab43facbd4c34c92878e303acf2fef9cc127e28a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# 一般的なシナリオのCDN設定スニペット {#cdn-configuration-snippets}

この記事では、AEM as a Cloud Serviceの実用的な`cdn.yaml` パターンについて説明します。 [CDN トラフィックルール ](/help/implementing/dispatcher/cdn-configuring-traffic.md)、[お客様が管理するCDN資格情報](/help/implementing/dispatcher/cdn-credentials-authentication.md)、および[WAF](/help/security/traffic-filter-rules-including-waf.md)を含むトラフィックフィルタールールの機能ドキュメントと一緒に使用します。 Cloud Manager [config パイプライン ](/help/operations/config-pipeline.md)を使用してスニペットをデプロイします。

>[!NOTE]
>
>ホスト名、パス、IP範囲、キー、しきい値を、プログラムに一致する値に置き換えます。 非実稼動環境での変更を昇格する前にテストします。

## 顧客管理CDN {#customer-managed-cdn}

### 一部のドメインのみのEdge キー認証の設定 {#edge-auth-selected-hosts}

問題：[顧客が管理するCDN](/help/implementing/dispatcher/cdn.md#point-to-point-cdn)では、一部の顧客ホスト名に対して認証を適用する必要がありますが、パブリッシュに到達する他のホスト名はそのヘッダーなしで使用できます（ロールアウト中や、CDNの背後に1つのブランドドメインしかない場合など）。

解決策：`X-Forwarded-Host`の最初のホスト名がターゲット ホスト名に等しい場合にのみ、`X-AEM-Edge-Key`認証が必要です（例：`example.com`）。 ルールは`forwardedDomain` リクエストプロパティを使用して、その一致を実行し、エッジ認証者に対して`authenticate` アクションを実行します。 プログラムのホスト名、認証者名、主要なプレースホルダーを置き換えます。

```yaml
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-key-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_1}}
        edgeKey2: ${{CDN_EDGEKEY_2}}
    rules:
      - name: edge-key-auth-rule
        when: { reqProperty: forwardedDomain, equals: "example.com" }
        action:
          type: authenticate
          authenticator: edge-key-auth
```

### VPN IPから送信されないリクエストに対するEdge キー認証の設定 {#edge-auth-trusted-ips}

問題：BYOCDNのエッジキー認証を設定しますが、VPN IPのパブリッシュドメインにのみ直接アクセスを許可します

解決策：クライアント IPがVPN IPのリストに含まれていない場合にのみ、X-AEM-Edge-Key認証が必要です

```yaml
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-key-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_1}}
        edgeKey2: ${{CDN_EDGEKEY_2}}
    rules:
      - name: edge-key-auth-rule
        when: { reqProperty: clientIp, notIn: ["10.0.0.1", "11.0.0.0/24", "<other VPN IPs>"] }
        action:
          type: authenticate
          authenticator: edge-key-auth
```

## リダイレクト {#redirects}

### APEX ドメインからwwwへのリダイレクト {#apex-to-www}

```yaml
kind: "CDN"
version: "1"
data:
 redirects:
   rules:
     - name: non-www-to-www-redirect
       when:
         reqProperty: domain
         doesNotMatch: '^www\.'
       action:
         type: redirect
         status: 301
         location:
           join:
             format: 'https://www.%s%s'
             args:
               - reqProperty: domain
               - reqProperty: url
```

### キャッシュキーの変更 {#cache-key}

CDNは、個別の「キャッシュキー」フィールドを公開しません。 URLはキャッシュに参加するので、URLを変更してキャッシュエントリを分割できます。例えば、[ リクエスト変換](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations)を通じてクエリパラメーターを追加します。

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: set-request-different-cache-curl
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqHeader: user-agent
              matches: curl
        actions:
          - type: set
            queryParam: cache
            value: 'curl'
```

### 正規化されたパスへのリダイレクト {#trailing-slash}

ブラウザーが公開時に末尾のスラッシュ （例：`https://www.example.com/path/`から`https://www.example.com/path`まで）をリクエストすると、永続的なリダイレクトを送信します。

```yaml
kind: "CDN"
version: "1"
data:
  redirects:
    rules:
      - name: remove-trailing-slash
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqProperty: domain
              equals: www.example.com
            - reqProperty: originalPath
              matches: ^/(.+)/$
        action:
          type: redirect
          status: 301
          location:
            reqProperty: originalPath
            transform:
              - op: replace
                match: ^/(.+)/$
                replacement: https://www.example.com/\1
```

### JSON Cookieからの情報の抽出 {#json-cookie}

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: options-response
        when: { reqProperty: tier, equals: publish }
        actions:
        - type: set
          reqHeader: x-mycookie-info
          value:
            reqCookie: mycookie
            transform: 
            - 'base64decode'
            - { op: 'replace', match: '"info":\s*"([^"]*)"', replacement: '\1'} 
```

## クロスオリジン設定 {#cross-origin}

### CDNからのOPTIONS リクエストの提供 {#options-from-cdn}

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: options-response
        when:
          allOf: 
            - { reqProperty: path, like: /mypathi*  }
            - { reqProperty: method, equals: "OPTIONS" }
            - { reqHeader: Origin, equals: "https://example.com" }
        actions:
          - type: respond
            status: 200
            reason: "OK"
            headers:
              content-type: 'text/plain'
              access-control-allow-origin: { reqHeader: Origin }
              access-control-allow-methods: "*"
              access-control-allow-headers: "*"
```

## トラフィックフィルター {#traffic-filters}

### レート制限ASN {#rate-limit-asn}

問題：IPごとのレート制限により、分散型サービス拒否（DDoS）パターンを見落とす可能性があります。各アドレスがしきい値を下回るので、正当で不正なトラフィックはIP層で同じように見えます。

解決策：同じネットワーク名を共有するホストをリミッターが集約するように、自律的なシステム名（`clientAsName`）でリクエストをカウントします。 スニペットは、リクエストごとに`clientAsName`をログプロパティに書き込み、その値でグループ化されたオーサーとパブリッシュにレート制限を適用します。 多くのユーザーは1つのASNを共有できます（大規模なISPや企業のVPN離脱など）。そのため、チューニングでは慎重に制限を行い、CDN ログに誤検出がないか監視します。

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: log-on-request
        when: "*"
        actions:
          - type: set
            logProperty: client_as_name
            value:
              reqProperty: clientAsName
  trafficFilters:
    rules:
    - name: limit-requests-client-as-name
      when:
        reqProperty: tier
        matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        count: all
        groupBy:
          - reqProperty: clientAsName
      action: block
```
