---
title: Edge Delivery Services フォーム送信での 403 Forbidden エラーのトラブルシューティング
description: Edge Delivery ServicesからAEM Publish にフォームを送信する際に 403 Forbidden エラーを診断し、解決する方法を説明します。 このガイドでは、CORS、Dispatcher ルール、リファラーフィルターの問題など、一般的な原因について説明します。
feature: Edge Delivery Services
role: Admin, Developer
exl-id: f397e059-f1b3-4afa-bd38-8f5fc591bb22
source-git-commit: d457bf9af377176222c2b96816fbbc4265e6b167
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 3%

---

# Edge Delivery Services フォーム送信での 403 Forbidden エラーのトラブルシューティング {#troubleshooting-403-forbidden-edge-delivery}

Edge Delivery ServicesからAEM Publish にフォームを送信すると、**403 Forbidden** エラーが発生する場合があります。 このエラーは、通常、セキュリティ設定が原因で、サーバーがリクエストの処理を拒否していることを示します。 この記事は、この問題の最も一般的な原因を特定して解決するのに役立ちます。

## 問題の説明

Edge Delivery ServicesからAEM Publish にフォームを送信すると、**403 Forbidden** エラーが発生する。 エラーは次のように表示されます。

- HTTP ステータスコード：403
- エラーメッセージ：「禁止」または「アクセスが拒否されました」
- AEM送信サーブレットに到達せずにフォーム送信が失敗する

この問題は、通常、Edge Delivery Services ドメイン（`.aem.live`、`.aem.page`、`.hlx.page`、`.hlx.live`）でホストされているフォームがEdge パブリッシュインスタンスにデータを送信しようとするAEM統合で発生します。

>[!IMPORTANT]
>
>リポジトリを設定すると、同じリポジトリを使用して複数のサイトをホストできます。 フォーム送信が正しく機能するには、各サイトドメインを個別に許可リストに追加する必要があります。
>
>**例：**
>
>- リポジトリ : `https://github.com/adobe/abc`
>- サイト 1: `main--abc--adobe.aem.live`
>- サイト 2:`main--abc1--adobe.aem.live`
>
>両方のサイトでフォームを送信するには、両方のドメインで別々の許可リストエントリが必要です。

## 一般的な原因と解決策

Edge Delivery Services フォーム送信で 403 Forbidden エラーが発生すると、複数の原因が考えられます。 次のトラブルシューティング手順に順番に従います。

### &#x200B;1. CORS （クロスオリジンリソース共有）の問題

**症状：**

- ブラウザーコンソールに CORS 関連のエラーメッセージが表示される
- 「ネットワーク」タブには、サーバーに到達する前にブロックされているリクエストが表示されます
- 「クロスオリジンリクエストがブロックされました」と記載されたエラーメッセージ

**診断：**

1. ブラウザー開発者ツール （F12）を開く
2. 「コンソール」タブで CORS エラーメッセージを確認します
3. `Access to fetch at 'https://publish-xxx.adobeaemcloud.com' from origin 'https://main--repo--owner.aem.live' has been blocked by CORS policy` のようなメッセージを探します。

**解決策：**
AEMで CORS を設定して、特定のEdge Delivery サイトドメインからのリクエストを許可します。

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Sites - Add each site domain individually
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc--adobe\.aem\.live$)#" CORSTrusted=true
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc1--adobe\.aem\.live$)#" CORSTrusted=true

# Legacy Franklin domains (if still in use)
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

>[!NOTE]
>
>`main--abc--adobe.aem.live` と `main--abc1--adobe.aem.live` を実際のサイトドメインに置き換えます。 同じリポジトリからホストされる各サイトには、個別の CORS 設定エントリが必要です。

CORS 設定について詳しくは、『 [CORS 設定ガイド &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors) 』を参照してください。

### 2.Dispatcherのルール

**症状：**

- ブラウザーコンソールで CORS メッセージを使用しないと、403 エラーが発生する
- リクエストはサーバーに到達していますが、Dispatcherによってブロックされています
- AEM アプリケーションレイヤーに到達する前にエラーが発生しました

**診断：**

1. リクエスト URL が任意のDispatcher フィルタールールと一致するかどうかを確認します。
2. POST リクエストをブロックする可能性のある `/filter` ルールについて、Dispatcherの設定を確認します
3. Dispatcher設定でフォーム送信エンドポイントが許可されていることを確認します。

**解決策：**
フォーム送信リクエストを許可するようにDispatcher設定を更新します。

1. フォーム送信エンドポイントへの POST リクエストが許可されていることを確認します
2. Edge Delivery ドメインに適したフィルタールールの追加
3. 送信サーブレットのパスがブロックされていないことを確認

Dispatcher フィルター設定の例：

```apache
/filter {
  # Allow POST requests to form submission servlet
  /0100 { /type "allow" /method "POST" /url "/content/forms/af/*" }
  /0101 { /type "allow" /method "POST" /url "/adobe/forms/af/submit/*" }
  /0102 { /type "allow" /method "POST" /url "/content/forms/portal/submit/adaptiveform" }
}
```

### &#x200B;3. リファラーフィルターの問題

**症状：**

- ブラウザーコンソールで 403 エラーが発生し、CORS の問題が発生しない
- リクエストはAEMに到達したが、Sling Referrer Filter によって拒否される
- AEM アプリケーションレイヤーでエラーが発生します

**診断：**
AEM エラーログでリファラーフィルターの却下メッセージを確認します。

1. [Cloud Managerから AEM Cloud Service ログにアクセスする](/help/implementing/cloud-manager/manage-logs.md)
2. 以下を含む `aemerror.log` 内のエントリを探します。
   - 「リファラーフィルターが拒否されました」
   - &quot;org.apache.sling.security.impl.ReferrerFilter&quot;
   - リファラーの検証エラーを示すメッセージ

**ログエントリの例：**

```
[ERROR] org.apache.sling.security.impl.ReferrerFilter Referrer filter rejected request with referrer 'https://main--abc--adobe.aem.live' for POST /content/forms/af/submit
```

**解決策：**
リファラーフィルターを設定して、特定のEdge Delivery サイトのドメインを許可します。

1. OSGi 設定ファイル `org.apache.sling.security.impl.ReferrerFilter.cfg.json` を作成または更新します。

2. 特定のサイトドメインを使用して次の設定を追加します。

   ```json
   {
     "allow.empty": false,
     "allow.hosts": [
       "main--abc--adobe.aem.live",
       "main--abc1--adobe.aem.live"
     ],
     "allow.hosts.regexp": [
       "https://.*\\.aem\\.live:443",
       "https://.*\\.aem\\.page:443",
       "https://.*\\.hlx\\.page:443",
       "https://.*\\.hlx\\.live:443"
     ],
     "filter.methods": [
       "POST",
       "PUT",
       "DELETE",
       "COPY",
       "MOVE"
     ],
     "exclude.agents.regexp": [
       ""
     ]
   }
   ```

3. Cloud Managerを使用した設定のデプロイ

>[!IMPORTANT]
>
>**リポジトリ設定の場合：** 各サイトドメインを個別に `allow.hosts` アレイに追加する必要があります。 正規表現パターンのみを使用しても、すべてのシナリオで十分とは限らない場合があります。 包括的なカバレッジに特定のドメインと正規表現パターンの両方を含めます。

>[!WARNING]
>
>AEM のリファラーフィルターは OSGi 設定ファクトリではありません。つまり、AEM サービスで一度にアクティブになる設定は 1 つだけです。可能であれば、カスタムリファラーフィルター設定を追加しないでください。これにより、AEMのネイティブ設定が上書きされ、製品の機能が損なわれる可能性があります。

## 診断ステップ

403 エラーの具体的な原因を特定するには、次の手順に従います。

### 手順 1：ブラウザーコンソールの確認

1. ブラウザー開発者ツール （F12）を開く
2. 「コンソール」タブに移動します。
3. フォーム送信の試行
4. CORS 関連のエラーメッセージを探します

**CORS エラーが存在する場合：** 上記の CORS ソリューションに従います。
**CORS エラーがない場合：** 手順 2 に進みます。

### 手順 2:「ネットワーク」タブを確認する

1. ブラウザー開発者ツール （F12）を開く
2. 「ネットワーク」タブに移動します。
3. フォーム送信の試行
4. 失敗したリクエストの詳細の確認
5. 応答ヘッダーとステータスの確認

**リクエストがサーバーに到達しない場合：**&#x200B;Dispatcherの問題である可能性があります。
**リクエストがサーバーに到達したが失敗した場合：** リファラーフィルターの問題である可能性があります。

### 手順 3:AEM ログの確認

1. Cloud Manager へのアクセス
2. 環境→の環境への移動→ ログ
3. `aemerror.log` のダウンロードまたは表示
4. フォーム送信前後のエントリの検索
5. リファラーフィルターまたはセキュリティ関連のメッセージを探します

## 予防とベストプラクティス

### 1.設定時の適切な構成

- Edge Delivery Servicesの初期設定時に、CORS、Dispatcherおよびリファラーフィルターを設定します
- **新しいサイトごとに：** すべての許可リストに特定のドメインを追加する*（CORS、リファラーフィルター）
- 運用開始前に、開発環境でフォーム送信をテストする

### 2.環境固有の構成

- 開発環境、ステージング環境および実稼動環境に異なる設定を使用する
- ローカル開発テストに localhost ドメインを含める
- リポジトリへの許可リストアクセスが必要なすべてのサイトドメインを文書化 **する**

### &#x200B;3. モニタリングとログ

- リファラーフィルターの却下に対するログ監視の設定
- フォーム送信コードに適切なエラー処理を実装する
- テスト中にブラウザー開発者ツールを使用する

### &#x200B;4. ドキュメントとチームの知識

- 同じリポジトリを使用するすべてのサイト ドメインの **レジストリの管理**
- トラブルシューティング手順に関する開発チームのトレーニング
- Edge Delivery Services フォーム設定のチェックリストを管理します
- 許可リストに加える既存のリポジトリから新しいサイトが作成されるたびに **更新** します。

## リポジトリ設定のサイトドメイン管理

Helix-5 およびリポーレスアーキテクチャでは、次のガイドラインに従います。

### 新しいサイトの作成時

1. **サイトドメインを特定** （例：`main--newsite--adobe.aem.live`）
2. **CORS 設定を更新** して新しいドメインを含める
3. **リファラーフィルターを更新** して、新しいドメインを `allow.hosts` に含める
4. 新しいサイトからの **フォーム送信のテスト**
5. **新しいドメインをドキュメント化** して、サイトレジストリに追加します

### ドメイン命名パターン

- 標準パターン：`{branch}--{site}--{owner}.aem.live`
- 同じリポジトリを共有しても、各サイトは一意のドメインを取得します
- `.aem.live` ドメインと `.aem.page` ドメインの両方を使用できます

### 設定の管理

- セキュリティを強化するために、`allow.hosts` で特定のドメインエントリを使用する
- 正規表現パターンを追加して対象範囲を拡大
- 許可リストに加える サイトの追加や削除に合わせて定期的に監査および更新する。

## その他のリソース

- [AEM ヘッドレスとリファラーフィルターの設定](/help/headless/deployment/referrer-filter.md)
- [CORS 設定ガイド &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [&#x200B; クロスオリジンリソース共有について &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)
- [Edge Delivery Services Forms ドキュメント](/help/edge/docs/forms/universal-editor/publish-forms.md)

## 関連トピック

- [送信アクションの設定](/help/forms/configuring-submit-actions.md)
- [Forms 送信サービス](/help/forms/forms-submission-service.md)
- [Edge 配信サービスの概要](/help/edge/overview.md)


**追加のヘルプが必要な場合は、** これらのトラブルシューティング手順に従った後も問題が引き続き発生する場合は、次の情報を使用してAdobeのカスタマーサポートにお問い合わせください。

- 具体的なエラーメッセージ
- AEM Cloud Service 環境の詳細
- フォーム送信アクセスが必要な **すべてのEdge Delivery Services サイトドメイン**
- エラーが発生した時点からの関連ログエントリ

**追加のヘルプが必要な場合は、** これらのトラブルシューティング手順に従った後も問題が引き続き発生する場合は、次の情報を使用してAdobeのカスタマーサポートにお問い合わせください。

- 具体的なエラーメッセージ
- AEM Cloud Service 環境の詳細
- Edge Delivery Services ドメイン情報
- エラーが発生した時点からの関連ログエントリ
