---
title: Edge Delivery Services を使用したアダプティブフォームの公開
description: 実稼動環境での使用を目的として、Edge Delivery Services を使用してアダプティブフォームを公開、設定、アクセスする方法について説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
keywords: フォームの公開, Edge Delivery Services, フォーム設定, CORS, リファラーフィルター
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 100%

---

# Edge Delivery Services を使用したアダプティブフォームの公開

アダプティブフォームを公開すると、Edge Delivery Services でエンドユーザーがアクセスおよび送信できます。このプロセスには、フォームの公開、セキュリティ設定の指定、ライブフォームへのアクセスという 3 つの主なフェーズが含まれます。

**達成されること：**

- フォームから Edge Delivery Services への公開
- フォーム送信のセキュリティ設定の指定
- 公開済みフォームへのアクセスと検証
- 適切な URL ルーティングと CORS ポリシーの設定

## 前提条件

- Edge Delivery Services テンプレートを使用して作成されたアダプティブフォーム
- フォームがテスト済みで、実稼動環境で使用できる状態
- AEM Forms のオーサー権限
- Cloud Manager へのアクセス（実稼動環境の設定用）
- フォームブロックコードへの開発者アクセス（送信設定用）

## プロビジョニングプロセスの概要

Edge Delivery Services へのフォームの公開は、次の 3 段階のアプローチに従います。

- **フェーズ 1：フォームの公開** - フォームを CDN に公開し、公開ステータスを確認します
- **フェーズ 2：セキュリティ設定** - 安全な送信のために CORS ポリシーとリファラーフィルターを設定します
- **フェーズ 3：アクセスと検証** - フォームの機能をテストし、ワークフロー全体を検証します

各フェーズは前のフェーズに基づいて作成され、安全で機能的なデプロイメントを確保します。

### フェーズ 1：フォームの公開

+++ 手順 1：公開を開始

1. **フォームにアクセス**：アダプティブフォームをユニバーサルエディターで開きます
2. **公開を開始**：ツールバーの「**公開**」アイコンをクリックします

   ![「公開」をクリック](/help/edge/docs/forms/universal-editor/assets/publish-form-ue.png)

+++


+++ 手順 2：レビューと確認

1. **公開アセットをレビュー**：フォームを含む、公開中のすべてのアセットが表示されます

   ![「公開」をクリックした場合](/help/edge/docs/forms/universal-editor/assets/publish-form-ue-review.png)

2. **公開を確認**：「**公開**」をクリックして続行します
3. **成功を検証**：確認メッセージを探します

   ![公開成功](/help/edge/docs/forms/universal-editor/assets/publish-form-ue-success.png)

+++


+++ 手順 3：公開ステータスを検証

**ステータスを確認**：現在のステータスを表示するには、「**公開**」アイコンをもう一度クリックします

![公開ステータス](/help/edge/docs/forms/universal-editor/assets/publish-form-ue-validate.png)

**検証チェックポイント：**

- フォームのステータスがエディターに「公開済み」と表示される
- 公開プロセス中にエラーメッセージが表示されない
- フォームが公開済みアセットリストに表示される

+++


+++ 公開済みフォームを管理

**フォームを非公開にするには：**

1. エディターでフォームを開きます
2. 右上隅の 3 つのドットメニュー（⋯）をクリックします
3. 「**非公開**」を選択します

![フォームを非公開](/help/edge/docs/forms/universal-editor/assets/unpublish-ue.png)

+++


### フェーズ 2：セキュリティ設定の指定

+++ セキュリティ設定が必要な理由

安全なフォーム送信を有効にするには、次のセキュリティ設定を指定する必要があります。

- Edge Delivery Services が AEM にデータを送信できるようにする
- AEM インスタンスへの不正アクセスを防止する
- フォーム送信用の CORS（クロスオリジンリソース共有）を有効にする
- 正当な Edge Delivery ドメインのみを許可するようにリクエストをフィルタリングする

>[!IMPORTANT]
>
>**実稼動環境に必須**：実稼動環境でフォーム送信が機能するには、これらの設定が必須です。

+++



+++ 手順 1：フォーム送信 URL を設定する

**目的**：AEM インスタンスへのフォーム送信を直接行います

**ファイルの場所**：Edge Delivery Services プロジェクトの `blocks/form/constant.js`

**設定例：**

```javascript
// Production Environment
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';

// Local Development Environment  
export const submitBaseUrl = 'http://localhost:4503';

// Staging Environment
export const submitBaseUrl = 'https://publish-staging-p120-e12.adobeaemcloud.com';
```

**検証チェックポイント：**

- `constant.js` ファイルが正しい AEM 公開 URL で更新されている
- URL が環境（実稼動環境、ステージング環境、ローカル）と一致している
- URL の末尾にスラッシュが含まれていない

+++



+++ 手順 2：CORS 設定を指定

**目的**：Edge Delivery Services ドメインからのフォーム送信リクエストを許可します

**実装**：AEM Dispatcher または Apache 設定に CORS 設定を追加します

```apache
# Local Development Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Services - Preview/Stage Environment  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true

# Edge Delivery Services - Production Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

**検証チェックポイント：**

- Dispatcher 設定に CORS ルールが適用されている
- 必要なすべてのドメイン（localhost、hlx.page、hlx.live）が含まれている
- 設定がターゲット環境にデプロイされている

**参照ドキュメント：**

- [CORS 設定ガイド](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [リファラーフィルタードキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)

+++



+++ 手順 3：リファラーフィルターを設定

**目的**：書き込み操作を許可された Edge Delivery Services ドメインに制限します

**実装方法**：AEM as a Cloud Service の Cloud Manager 経由で設定します

**設定ファイル**：プロジェクトの OSGi 設定に追加します

```json
{
  "allow.empty": false,
  "allow.hosts": [],
  "allow.hosts.regexp": [
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

**設定の分類：**

- **`allow.empty`**：リファラーヘッダーのないリクエストを却下します
- **`allow.hosts.regexp`**：Edge Delivery Services ドメインからのリクエストを許可します
- **`filter.methods`**：これらの HTTP メソッドにフィルタリングを適用します
- **`exclude.agents.regexp`**：フィルタリングからユーザーエージェントを除外します

**検証チェックポイント：**

- リファラーフィルター設定が Cloud Manager 経由でデプロイされている
- AEM パブリッシュインスタンスで設定がアクティブである
- Edge Delivery Services ドメインからのテストフォーム送信が機能している
- 不正ドメインからのフォーム送信がブロックされている

**参照ドキュメント：**

- [Cloud Manager 経由のリファラーフィルターの設定](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)

+++


### フェーズ 3：公開済みフォームへのアクセス



+++ Edge Delivery Services の URL 構造

**標準 URL 形式：**

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
```

**URL コンポーネント：**

- **`<branch>`**：Git 分岐名（通常は `main`）
- **`<repo>`**：リポジトリ名
- **`<owner>`**：GitHub 組織またはユーザー名
- **`<form_name>`**：フォームの名前（小文字、ハイフン）

**環境固有の URL：**

```
# Production Environment (.aem.live)
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form

# Preview Environment (.aem.page) 
https://main--universaleditor--wkndforms.aem.page/content/forms/af/wknd-form
```

+++



+++ 検証の最終手順

**フォームアクセシビリティの検証：**

1. **フォームの読み込みをテスト**：フォームの URL にアクセスし、正しく読み込まれることを確認します
2. **フォーム送信をテスト**：フォームに入力して送信し、データ処理を確認します
3. **レスポンシブデザインを確認**：様々なデバイスと画面サイズでフォームをテストします
4. **セキュリティを検証**：CORS とリファラーフィルターが正しく動作していることを確認します

**期待される結果：**

- エラーなしでフォームが読み込まれる
- すべてのフォームフィールドが正しくレンダリングされる
- フォーム送信プロセスが正常に完了する
- 設定した宛先（スプレッドシート、メールなど）にデータが表示される
- CORS やセキュリティポリシーに関連するコンソールエラーが発生しない

+++


## 次の手順


- [フォーム送信アクションの設定](/help/edge/docs/forms/universal-editor/submit-action.md)
- [フォームのスタイルとテーマ](/help/edge/docs/forms/universal-editor/style-theme-forms.md)
- [レスポンシブフォームレイアウトの作成](/help/edge/docs/forms/universal-editor/responsive-layout.md)
- [reCAPTCHA 保護の追加](/help/edge/docs/forms/universal-editor/recaptcha-forms.md)



