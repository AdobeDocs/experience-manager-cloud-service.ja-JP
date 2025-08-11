---
title: Edge Delivery Servicesを使用したアダプティブFormsの公開
description: 実稼動用にEdge Delivery Servicesを使用してアダプティブFormsを公開、設定およびアクセスする方法について説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
keywords: [ フォームの公開、Edge Delivery Services、フォーム設定、CORS、リファラーフィルター ]
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: 746
ht-degree: 2%

---

# Edge Delivery Servicesを使用したアダプティブFormsの公開

アダプティブフォームを公開すると、エンドユーザーがEdge Delivery Services上でアクセスして送信できるようになります。 このプロセスには、フォームの公開、セキュリティ設定の設定、ライブフォームへのアクセスという 3 つの主なフェーズが含まれます。

**成し遂げること：**

- Edge Delivery Servicesへのフォームの公開
- フォーム送信のセキュリティ設定の指定
- 公開済みフォームへのアクセスと検証
- 適切な URL ルーティングと CORS ポリシーの設定

## 前提条件

- Edge Delivery Services テンプレートを使用して作成されたアダプティブフォーム
- フォームがテスト済みで、実稼動環境で使用できる状態
- AEM Forms作成者の権限
- Cloud Managerへのアクセス（実稼動用）
- フォームブロックコードへの開発者アクセス（送信設定用）

## 公開プロセスの概要

フォームのEdge Delivery Servicesへの公開は、次の 3 段階のアプローチに従います。

- **フェーズ 1：フォームの公開** - フォームを CDN に公開し、公開ステータスを確認する
- **フェーズ 2：セキュリティの設定** – 安全に送信するための CORS ポリシーとリファラーフィルターの設定
- **フェーズ 3：アクセスと検証** - フォームの機能をテストし、ワークフロー全体を検証する

各フェーズは前のフェーズに基づいて構築され、安全で機能的なデプロイメントを確保します。

### フェーズ 1：フォームを公開する

+++ 手順 1：公開の開始

1. **フォームへのアクセス**：アダプティブフォームをユニバーサルエディターで開きます
2. **公開を開始**：ツールバーの **公開** アイコンをクリックします

   ![「公開」をクリック](/help/forms/assets/publish-icon-eds-form.png)

+++


+++ 手順 2：レビューと確認

1. **公開アセットのレビュー**：フォームを含む、公開中のすべてのアセットが表示されます

   ![「公開」をクリックした場合](/help/forms/assets/on-click-publish.png)

2. **公開を確認**:「**公開**」をクリックして続行します
3. **成功の検証**：確認メッセージを探します

   ![公開成功](/help/forms/assets/publish-success.png)

+++


+++ 手順 3：公開ステータスの確認

**ステータスを確認**：現在のステータスを表示するには、「**公開**」アイコンを再度クリックします

![公開ステータス](/help/forms/assets/publish-status.png)

**検証チェックポイント：**

- フォームのステータスがエディターに「公開済み」と表示される
- 公開プロセス中にエラーメッセージが表示されません
- フォームが公開済みアセットリストに表示される

+++


+++ 公開済みFormsの管理

**フォームを非公開にするには：**

1. フォームをエディターで開きます
2. 右上隅の「。..」メニュー（⋯）をクリックします
3. **非公開** を選択します。

![ フォームを非公開 ](/help/forms/assets/unpublish--form.png)

+++


### フェーズ 2：セキュリティ設定の構成

+++ セキュリティ設定が必要な理由

安全なフォーム送信を有効にするには、次のセキュリティ設定を行う必要があります。

- Edge Delivery ServicesがAEMにデータを送信できるようにする
- AEM インスタンスへの不正アクセスの防止
- フォーム送信用の CORS （クロスオリジンリソース共有）を有効にする
- 正当なEdge Delivery ドメインのみを許可するようにリクエストをフィルタリングします

>[!IMPORTANT]
>
>**実稼動環境で必須**：これらの設定は、フォーム送信が実稼動環境で機能するために必須です。

+++



+++ 手順 1：フォーム送信 URL の設定

**目的**：フォーム送信をAEM インスタンスにダイレクトする

**ファイルの場所**:Edge Delivery Services プロジェクト内の `blocks/form/constant.js`

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

- `constant.js` ファイルが正しいAEM公開 URL で更新される
- URL が環境（実稼動、ステージングまたはローカル）と一致する
- URL の末尾のスラッシュなし

+++



+++ 手順 2:CORS 設定の指定

**目的**:Edge Delivery Services ドメインからのフォーム送信リクエストを許可する

**実装**:CORS 設定をAEM Dispatcher または Apache 設定に追加します

```apache
# Local Development Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Services - Preview/Stage Environment  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true

# Edge Delivery Services - Production Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

**検証チェックポイント：**

- Dispatcher 設定に適用される CORS ルール
- 必要なすべてのドメイン（localhost、hlx.page、hlx.live）が含まれています
- ターゲット環境にデプロイされた設定

**リファレンスドキュメント：**

- [CORS 設定ガイド ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [ リファラーフィルタードキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)

+++



+++ 手順 3：リファラーフィルターの設定

**目的**：書き込み操作を、許可されたEdge Delivery Services ドメインに制限する

**実装方法**:AEM as a Cloud ServiceのCloud Managerを使用してを設定する

**設定ファイル**：をプロジェクトの OSGi 設定に追加します

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

- **`allow.empty`**: リファラーヘッダーのないリクエストを拒否します
- **`allow.hosts.regexp`**:Edge Delivery Services ドメインからのリクエストを許可します
- **`filter.methods`**：これらの HTTP メソッドにフィルタリングを適用します
- **`exclude.agents.regexp`**：ユーザーエージェントがフィルタリングから除外されました

**検証チェックポイント：**

- Cloud Managerを介してデプロイされたリファラーフィルターの設定
- AEM パブリッシュインスタンスでアクティブな設定
- Edge Delivery Services ドメインからのフォーム送信のテストが機能します
- 承認されていないドメインのフォーム送信はブロックされます

**リファレンスドキュメント：**

- [Cloud Managerを使用したリファラーフィルターの設定 ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)

+++


### フェーズ 3：公開済みフォームへのアクセス



+++ Edge Delivery Servicesの URL 構造

**標準 URL 形式：**

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
```

**URL コンポーネント：**

- **`<branch>`**:Git ブランチ名（通常は `main`）
- **`<repo>`**: リポジトリ名
- **`<owner>`**:GitHub 組織またはユーザー名
- **`<form_name>`**：フォームの名前（小文字、ハイフン）

**環境固有の URL:**

```
# Production Environment (.aem.live)
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form

# Preview Environment (.aem.page) 
https://main--universaleditor--wkndforms.aem.page/content/forms/af/wknd-form
```

+++



+++ 検証の最終手順

**フォームアクセシビリティの検証：**

1. **フォームの読み込みをテスト**：フォーム URL にアクセスして、フォームが正しく読み込まれていることを確認します
2. **フォーム送信をテスト**：フォームに入力して送信し、データ処理を確認します
3. **レスポンシブデザインの確認**：異なるデバイスや画面サイズでフォームをテストします
4. **セキュリティの検証**:CORS およびリファラーフィルターが正しく動作していることを確認します

**期待される結果：**

- エラーなしでフォームを読み込む
- すべてのフォームフィールドが正しくレンダリングされます
- フォーム送信プロセスが正常に実行されました
- 設定した宛先（スプレッドシート、メールなど）にデータが表示される
- CORS やセキュリティポリシーに関連するコンソールエラーはありません。

+++


## 次の手順


- [フォーム送信アクションの設定](/help/edge/docs/forms/universal-editor/submit-action.md)
- [フォームのスタイルとテーマ](/help/edge/docs/forms/universal-editor/style-theme-forms.md)
- [レスポンシブフォームレイアウトの作成](/help/edge/docs/forms/universal-editor/responsive-layout.md)
- [reCAPTCHA 保護の追加](/help/edge/docs/forms/universal-editor/recaptcha-forms.md)



