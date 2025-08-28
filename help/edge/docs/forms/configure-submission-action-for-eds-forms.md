---
title: Edge Delivery Services を使用したAEM Forms の送信アクションの設定
description: Edge Delivery Servicesを使用して AEM Forms で送信アクションを設定する方法について学習します。 Forms Submission Service とAEM Publish Submit Action のいずれかを選択して、フォームデータを安全かつ効率的に処理します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2d16a9bd1f498dd0f824e867fd3b5676fb311bb3
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 79%

---

# AEM Forms の送信アクションの設定

AEM Forms と Edge Delivery Services を使用して、フォーム送信処理を設定し、データをスプレッドシート、メール、バックエンドシステムにルーティングします。

## クイック決定ガイド

送信方法を選択します。

| メソッド | 次に最適 | 設定の複雑さ | ユースケース |
|--------|----------|------------------|-----------|
| **Forms 送信サービス** | シンプルなデータキャプチャ | 低 | お問い合わせフォーム、調査、基本データ収集 |
| **AEM パブリッシュ送信** | 複雑なワークフロー | 高 | エンタープライズ統合、カスタム処理、ワークフロー |

## 前提条件

送信アクションを設定する前に、次を確認します。

- AEM Forms as a Cloud Service インスタンス
- Edge Delivery Services プロジェクトが設定されている
- ドキュメントオーサリングまたはユニバーサルエディターを使用してフォームが作成済みである
- ターゲットの宛先（スプレッドシート、メールシステム、AEM）に必要な権限がある

+++ 方法 1：Forms 送信サービス

Forms 送信サービスは、シンプルなデータキャプチャシナリオに最適な、アドビがホストするエンドポイントです。

### サポートされる宛先

- **スプレッドシート**：Google Sheets、Microsoft Excel（OneDrive／SharePoint）
- **メール**：フォームデータを指定されたメールアドレスに送信します

### 設定手順

1. **宛先アクセスを設定**
   - スプレッドシートの場合：ターゲットスプレッドシートで `forms@adobe.com` に編集権限を付与します
   - メールの場合：受信者のメールアドレスにアクセスできることを確認します

2. **フォーム送信を設定**
   - フォームをオーサリング環境で開きます
   - 送信アクションを「Forms 送信サービス」に設定します
   - ターゲットスプレッドシートの URL またはメールアドレスを指定します
   - フォームを保存して公開します

3. **送信をテスト**
   - フォームを通じてテストデータを送信します
   - ターゲットの宛先にデータが表示されることを確認します
   - 送信に失敗した場合はエラーログを確認します

### 重要な注意事項

- サービスアカウント `forms@adobe.com` には、ターゲットスプレッドシートへの編集アクセス権が必要です
- フォームを送信するとすぐにメール通知が送信されます
- データ検証はサービスレベルで行われます

![Forms 送信サービスのフロー](/help/forms/assets/eds-fss.png)

+++

+++ 方法 2：AEM パブリッシュ送信

複雑な処理のために、フォームデータを AEM as a Cloud Service パブリッシュインスタンスに直接送信します。

### AEM パブリッシュを使用するタイミング

- 送信後に必要なカスタム AEM ワークフロー
- フォームデータモデル（FDM）とデータベースの統合
- サードパーティサービスとの統合（Marketo、Power Automate、Workfront Fusion）
- Azure Blob Storage または SharePoint ドキュメントライブラリ
- 複雑なサーバーサイド検証または処理ロジック

### 使用可能な送信アクション

- [REST エンドポイントに送信](/help/forms/configure-submit-action-restpoint.md)
- [AEM メールサービス経由でメール送信](/help/forms/configure-submit-action-send-email.md)
- [フォームデータモデルを使用して送信](/help/forms/configure-data-sources.md)
- [AEM ワークフローを起動](/help/forms/aem-forms-workflow-step-reference.md)
- [SharePoint に送信](/help/forms/configure-submit-action-sharepoint.md)
- [OneDrive に送信](/help/forms/configure-submit-action-onedrive.md)
- [Azure Blob Storage に送信](/help/forms/configure-submit-action-azure-blob-storage.md)
- [Microsoft Power Automate への送信](/help/forms/forms-microsoft-power-automate-integration.md)
- [Adobe Workfront Fusion への送信](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [Adobe Marketo Engage への送信](/help/forms/submit-adaptive-form-to-marketo-engage.md)

![AEM パブリッシュ送信のフロー](/help/forms/assets/eds-aem-publish.png)

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

#### &#x200B;4. フォームの設定

1. ユニバーサルエディターでフォームを作成します
2. AEM Forms アクションをターゲットにする送信アクションを設定します
3. 送信エンドポイントパスを指定します
4. Edge Delivery サイトにフォームを公開します

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
| **フォームの送信に失敗する** | コンソールのエラーを確認し、エンドポイント URL を検証し、権限を確認します |
| **埋め込みフォームが表示されない** | フォームソースに CORS ヘッダーを設定し、フォーム URL を検証します |
| **AEM の 403／401 エラー** | Sling リファラーフィルターを更新し、認証設定を確認します |
| **データがスプレッドシートに到達しない** | `forms@adobe.com` に編集アクセス権があることを検証し、スプレッドシートの URL を確認します |
| **CORS エラー** | フォームソースに適切な `Access-Control-Allow-Origin` ヘッダーを追加します |

+++

## 設定例

+++ スプレッドシート送信付きのドキュメントベースのフォーム

1. Google Docs／Sheets でフォーム構造を作成します
2. Forms 送信サービスのエンドポイントを設定します
3. `forms@adobe.com` にターゲットスプレッドシートへの編集権限を付与します
4. ドキュメントを Edge Delivery サイトに公開します
5. フォーム送信とデータフローをテストします

+++

+++ AEM ワークフローを使用したユニバーサルエディターフォーム

1. ユニバーサルエディターでフォームを構築します
2. 送信アクションを「AEM ワークフローを起動」に設定します
3. AEM パブリッシュで Dispatcher とリファラーフィルターを設定します
4. CDN ルーティングルールを設定します
5. フォームを公開し、ワークフロー実行をテストします

+++

## ベストプラクティス

- シンプルなデータキャプチャシナリオには **Forms 送信サービスを使用**&#x200B;します
- 複雑な処理や統合が必要な場合は、**AEM パブリッシュを選択**&#x200B;します
- 実稼動環境へのデプロイメント前に、ステージング環境で&#x200B;**徹底的にテスト**&#x200B;します
- AEM ログとコンソールエラーを使用して&#x200B;**送信を監視**&#x200B;します
- 送信に失敗した場合は、**適切なエラー処理を実装**&#x200B;します
- クライアントレベルとサーバーレベルの両方で&#x200B;**データを検証**&#x200B;します
- すべてのフォーム送信とデータ転送に **HTTPS を使用**&#x200B;します

## 関連トピック

- [EDS Forms でのドキュメントベースのオーサリング](/help/edge/docs/forms/tutorial.md)
- [EDS Forms でのユニバーサルエディター](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [AEM Forms Submission Service](/help/forms/forms-submission-service.md)
- [データソースの設定](/help/forms/configure-data-sources.md)
- [AEM Forms Workflow リファレンス](/help/forms/aem-forms-workflow-step-reference.md)
