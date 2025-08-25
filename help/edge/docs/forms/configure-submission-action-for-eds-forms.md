---
title: Edge Delivery Services を使用したAEM Forms の送信アクションの設定
description: Edge Delivery Servicesを使用して AEM Forms で送信アクションを設定する方法について学習します。 Forms Submission Service とAEM Publish Submit Action のいずれかを選択して、フォームデータを安全かつ効率的に処理します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2d16a9bd1f498dd0f824e867fd3b5676fb311bb3
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 13%

---

# AEM Formsの送信アクションの設定

Edge Delivery ServicesのAEM Formsを使用してデータをスプレッドシート、メール、バックエンドシステムにルーティングするためのフォーム送信処理を設定します。

## クイック決定ガイド

送信方法を選択します。

| メソッド | 次に最適 | セットアップの複雑さ | ユースケース |
|--------|----------|------------------|-----------|
| **Forms送信サービス** | シンプルなデータキャプチャ | 低 | お問い合わせフォーム、調査、基本データ収集 |
| **AEM公開送信** | 複雑なワークフロー | 高 | エンタープライズ統合、カスタム処理、ワークフロー |

## 前提条件

送信アクションを設定する前に、次を確認します。

- AEM Forms as a Cloud Service インスタンス
- Edge Delivery Services プロジェクトが設定されました
- ドキュメントオーサリングまたはユニバーサルエディターを使用して作成されたフォーム
- ターゲットの宛先（スプレッドシート、メールシステムまたはAEM）に必要な権限

+++ 方法 1:Forms送信サービス

Forms送信サービスは、Adobeでホストされるエンドポイントであり、シンプルなデータキャプチャシナリオに最適です。

### サポートされる宛先

- **スプレッドシート**:Google シート、Microsoft Excel （OneDrive/SharePoint）
- **メール**：フォームデータを指定したメールアドレスに送信します

### 設定手順

1. **宛先アクセスの設定**
   - スプレッドシートの場合：ターゲットスプレッドシートの `forms@adobe.com` に編集権限を付与します
   - メールの場合：受信者のメールアドレスがアクセス可能であることを確認します

2. **フォーム送信の設定**
   - オーサリング環境でフォームを開きます
   - 送信アクションを「Forms送信サービス」に設定する
   - ターゲットスプレッドシートの URL またはメールアドレスを指定
   - フォームを保存して公開します

3. **テスト送信**
   - フォームを使用したテストデータの送信
   - データがターゲットの宛先に表示されることを確認します
   - 送信に失敗した場合のエラーログの確認

### 重要な注意事項

- サービス アカウント `forms@adobe.com` はターゲット スプレッドシートへの編集アクセスが必要です
- メール通知は、フォーム送信時に直ちに送信されます
- データの検証はサービス・レベルで行われる

![Forms送信サービスフロー ](/help/forms/assets/eds-fss.png)

+++

+++ 方法 2:AEMの送信内容の公開

複雑な処理のために、フォームデータをAEM as a Cloud Service パブリッシュインスタンスに直接送信します。

### AEMの公開を使用するタイミング

- 送信後に必要なカスタム AEM ワークフロー
- フォームデータモデル（FDM）とデータベースの統合
- サードパーティのサービス統合（Marketo、Power Automate、Workfront Fusion）
- Azure Blob Storage またはSharePoint ドキュメントライブラリ
- 複雑なサーバーサイドの検証または処理ロジック

### 使用可能な送信アクション

- [REST エンドポイントに送信](/help/forms/configure-submit-action-restpoint.md)
- [AEM メールサービスを使用したメールの送信](/help/forms/configure-submit-action-send-email.md)
- [フォームデータモデルを使用して送信](/help/forms/configure-data-sources.md)
- [AEM ワークフローを起動](/help/forms/aem-forms-workflow-step-reference.md)
- [SharePoint に送信](/help/forms/configure-submit-action-sharepoint.md)
- [OneDrive に送信](/help/forms/configure-submit-action-onedrive.md)
- [Azure Blob Storage への送信](/help/forms/configure-submit-action-azure-blob-storage.md)
- [Microsoft Power Automate への送信](/help/forms/forms-microsoft-power-automate-integration.md)
- [Adobe Workfront Fusion への送信](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [Adobe Marketo Engageへの送信](/help/forms/submit-adaptive-form-to-marketo-engage.md)

![AEM公開送信フロー ](/help/forms/assets/eds-aem-publish.png)

### 設定要件

#### &#x200B;1. Edge DeliveryでAEM インスタンス URL を更新する

`constant.js` の下にある `form` ブロックの `submitBaseUrl` ファイルの AEM Cloud Service インスタンス URL を更新します。 環境に応じて URL を設定できます。

**Cloud Service インスタンスの場合**

```js
export const submitBaseUrl = '<aem-publish-instance-URL>';
```

**ローカル開発用**

```js
export const submitBaseUrl = 'http://localhost:<port-number>';
```

#### &#x200B;2. OSGi リファラーフィルター

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

OSGi リファラーフィルターの設定について詳しくは、「[ リファラーフィルター ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter) ガイドを参照してください。

#### &#x200B;3. CORS （クロスオリジンリソース共有）の問題

AEMで CORS を設定して、特定のEdge Delivery サイトドメインからのリクエストを許可します。

**開発者 Localhost**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true
```

**Edge Delivery Sites – 各サイトドメインを個別に追加する**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc--adobe\.aem\.live$)#" CORSTrusted=true
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc1--adobe\.aem\.live$)#" CORSTrusted=true
```

**従来の Franklin ドメイン（まだ使用中の場合）**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

>[!NOTE]
>
>`main--abc--adobe.aem.live` と `main--abc1--adobe.aem.live` を実際のサイトドメインに置き換えます。 同じリポジトリからホストされる各サイトには、個別の CORS 設定エントリが必要です。

CORS 設定について詳しくは、『 [CORS 設定ガイド ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors) 』を参照してください。


お使いのローカル開発で CORS を有効にするには、[ クロスオリジンリソース共有（CORS）について ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) を参照してください。

<!--
#### 4. CDN Redirect Rules

Configure your Edge Delivery CDN to route submissions:

- Route requests from `/adobe/forms/af/submit/...` to your AEM Publish instance
- Implementation varies by CDN provider (Fastly, Akamai, Cloudflare)-->

#### &#x200B;4. フォーム設定

1. ユニバーサルエディターでのフォームの作成
2. Target AEM Forms アクションへの送信アクションの設定
3. 送信エンドポイントのパスを指定
4. Edge Delivery サイトへのフォームの公開

+++
<!--
+++ Form Embedding

Embed forms created in one location into different web pages or sites.

### Use Cases

- Reuse standard forms across multiple landing pages
- Include specialized forms in Document-Authored content
- Maintain single form across multiple EDS projects

### CORS Configuration

Configure Cross-Origin Resource Sharing on the form source:

1. **Add CORS Headers** to form source responses:
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`  
   - `Access-Control-Allow-Headers: Content-Type`

2. **Example Configuration**:

        # Configuration for site hosting the form
        headers:
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS

### Embedding Steps

1. **Create and Publish Form**
   - Build form using Document Authoring or Universal Editor
   - Configure submission method (FSS or AEM Publish)
   - Publish to standalone URL

2. **Configure CORS**
   - Set up CORS headers on form source site
   - Allow host page domain to fetch form

3. **Embed in Host Page**
   - Add form embedding block to host page
   - Point block to published form URL
   - Publish host page

![Embedded Form Architecture](/help/forms/assets/eds-embedded-form.png)

+++-->

+++ よくある問題

| 問題 | 解決策 |
|-------|----------|
| **フォーム送信が失敗する** | コンソールエラーの確認、エンドポイント URL の確認、権限の確認 |
| **埋め込みフォームが表示されない** | フォームソースに CORS ヘッダーを設定し、フォーム URL を確認する |
| AEMの **403/401 エラー** | Sling リファラーフィルターを更新し、認証設定を確認する |
| **データがスプレッドシートに到達しない** | 編集アクセス権 `forms@adobe.com` あることを確認し、スプレッドシート URL を確認します |
| **CORS エラー** | フォームソースへの適切な `Access-Control-Allow-Origin` ヘッダーの追加 |

+++

## 設定例

+++ スプレッドシート送信付きのドキュメントベースのフォーム

1. Google Docs/シートでのフォーム構造の作成
2. Forms送信サービスエンドポイントの設定
3. ターゲットスプレッドシートへ `forms@adobe.com` 編集アクセス権の付与
4. Edge Delivery サイトへのドキュメントの公開
5. フォーム送信とデータフローのテスト

+++

+++ AEM ワークフローを使用したユニバーサルエディターフォーム

1. ユニバーサルエディターでのフォームの作成
2. 「AEM Workflow の呼び出し」に対する送信アクションの設定
3. AEM パブリッシュに対するDispatcherおよびリファラーフィルターの設定
4. CDN ルーティングルールの設定
5. フォームを公開してワークフローの実行をテスト

+++

## ベストプラクティス

- 簡単なデータキャプチャシナリオでの **Forms送信サービスの使用**
- 複雑な処理や統合が必要な場合に **AEM公開を選択**
- 実稼動デプロイメントの前に、ステージング環境で **十分にテスト** します
- **AEM ログとコンソールエラーを使用した送信の監視**
- 失敗した送信に対する **適切なエラー処理の実装**
- クライアントレベルとサーバーレベルの両方で **データを検証**
- すべてのフォーム送信とデータ送信に **HTTPS を使用**

## 関連トピック

- [EDS Formsを使用したドキュメントベースのオーサリング](/help/edge/docs/forms/tutorial.md)
- [EDS Formsを使用したユニバーサルエディター](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [AEM Forms Submission Service](/help/forms/forms-submission-service.md)
- [データソースの設定](/help/forms/configure-data-sources.md)
- [AEM Forms ワークフローリファレンス](/help/forms/aem-forms-workflow-step-reference.md)
