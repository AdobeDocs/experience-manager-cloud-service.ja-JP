---
title: Edge Delivery Services を使用したAEM Forms の送信アクションの設定
description: Edge Delivery Servicesを使用して AEM Forms で送信アクションを設定する方法について学習します。 Forms Submission Service とAEM Publish Submit Action のいずれかを選択して、フォームデータを安全かつ効率的に処理します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 12%

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

#### &#x200B;1. AEM Dispatcherの設定

AEM パブリッシュインスタンスでDispatcherを設定します。

- **送信パスを許可**:`filters.any` への POST リクエストを許可するように `/adobe/forms/af/submit/...` を変更します
- **リダイレクトなし**:Dispatcher ルールでフォーム送信パスがリダイレクトされないようにします

#### &#x200B;2. OSGi リファラーフィルター

AEM OSGi コンソール（`/system/console/configMgr`）で：

1. 「Apache Sling Referrer Filter」を探します
2. 「Allow Hosts」リストにEdge Delivery ドメインを追加する
3. `https://your-eds-domain.hlx.page` などのドメインを含める

#### &#x200B;3. CDN リダイレクトルール

送信をルーティングするようにEdge Delivery CDN を設定します。

- `/adobe/forms/af/submit/...` からのリクエストをAEM パブリッシュインスタンスにルーティングする
- 実装は CDN プロバイダー（Fastly、Akamai、Cloudflare）によって異なります

#### &#x200B;4. フォーム設定

1. ユニバーサルエディターでのフォームの作成
2. Target AEM Forms アクションへの送信アクションの設定
3. 送信エンドポイントのパスを指定
4. Edge Delivery サイトへのフォームの公開

+++

+++ フォームの埋め込み（オプション）

1 つの場所で作成されたフォームを別の web ページや web サイトに埋め込みます。

### ユースケース

- 複数のランディングページでの標準フォームの再利用
- ドキュメント作成コンテンツへの専用のフォームの組み込み
- 複数の EDS プロジェクトにわたって単一フォームを維持

### CORS 設定

フォームソースでクロスオリジンリソース共有を設定します。

1. フォームソースの応答に **CORS ヘッダーを追加** します。
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`
   - `Access-Control-Allow-Headers: Content-Type`

2. **設定例**:

       &#x200B;# フォームをホストするサイトの設定 
       headers:
       - パス：/forms/**
       custom:
       Access-Control-Allow-Origin: https://host-domain.com
       Access-Control-Allow-Methods: GET（OPTIONS） 
   

### ステップの埋め込み

1. **フォームの作成と公開**
   - ドキュメントオーサリングまたはユニバーサルエディターを使用したフォームの作成
   - 送信方法を設定（FSS またはAEM公開）
   - スタンドアロン URL に公開

2. **CORS の設定**
   - フォームソースサイトでの CORS ヘッダーの設定
   - ホストページドメインによるフォームの取得を許可

3. **ホストページへの埋め込み**
   - フォーム埋め込みブロックをホストページに追加
   - ブロックを公開済みフォームの URL にポイント
   - ホストページを公開

![埋め込みフォームアーキテクチャ](/help/forms/assets/eds-embedded-form.png)

+++

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
