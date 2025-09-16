---
title: Edge Delivery Services を使用したアダプティブフォームの作成と公開
description: 技術的な正確さと明確さに焦点を当てて、AEM の Edge Delivery Services テンプレートを使用してアダプティブフォームを作成、オーサリング、公開する手順について説明します。
keywords: アダプティブフォーム、Edge Delivery Services、ユニバーサルエディター、フォームの作成、AEM Forms、フォームの公開
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: ht
source-wordcount: '1005'
ht-degree: 100%

---


# Edge Delivery Services を使用したアダプティブフォームの作成と公開

このドキュメントでは、AEMのEdge Delivery Services テンプレートを使用して、アダプティブフォームを作成、設定および公開する手順を順を追って説明します。フォームの作成から本番環境へのデプロイまでのワークフロー全体について説明します。

このガイドでは、次の操作方法について説明します。

- Edge Delivery Services テンプレートを使用したフォームの作成
- ユニバーサルエディターを使用したフォームの作成
- フォームの設定と Edge Delivery Services への公開
- 公開済みフォームへのアクセスとデプロイメントの検証



## 前提条件

続行する前に、次の前提条件が満たされていることを確認します。


- **AEM Forms as a Cloud Service**：Forms ライセンスを持つアクティブなオーサーインスタンス。
- **GitHub アカウント**：リポジトリ管理のための個人用または組織用のアカウント。
- **リポジトリ設定**：次のいずれかを選択します。
   - **新規プロジェクト**：[アダプティブフォームブロックを含む新しい AEM プロジェクトを作成します](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)。リポジトリは、Edge Delivery Services 用に事前設定されています。
   - **既存のプロジェクト**：[既存のリポジトリにアダプティブフォームブロックを追加](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)し、設定を更新します。

- **AEM と GitHub の接続**：AEM インスタンスと GitHub リポジトリ間の[接続を確立](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)します。
- **Edge Delivery Services**：リポジトリが自動デプロイメント用に設定されていることを確認します。
- **権限**：フォームの作成と公開に必要なアクセス権があることを確認します。

- GitHub リポジトリにアダプティブフォームブロックが含まれていることを確認します。



## フォームの作成と公開のワークフロー

このプロセスは、次の 3 つの主なフェーズで構成されます。

- **フェーズ 1：**[ フォームの作成](#step-1-form-creation)
- **フェーズ 2：**[フォームのオーサリングとデザイン](#step-2-form-authoring-and-design)
- **フェーズ 3：**[設定と公開](#step-3-configuration-and-publishing)

各フェーズには、正しい設定を確認するための検証手順が含まれます。


### 手順 1：フォームの作成

1. **フォームの作成にアクセス**
   - AEM Forms as a Cloud Service オーサーインスタンスにログインします。
   - **Adobe Experience Manager**／**Forms**／**フォームとドキュメント**&#x200B;に移動します。
   - **作成**／**アダプティブフォーム**&#x200B;の順にクリックします。

1. **テンプレートを選択**
   - 「**ソース**」タブで、**Edge Delivery Services ベースのテンプレート**&#x200B;を選択します。
   - 「**作成**」ボタンが有効になります。

     ![EDS フォームを作成](/help/edge/assets/create-eds-forms.png)

1. **オプションを設定（オプション）**
   - **「データソース」タブ**：必要に応じて、データ統合を選択します。
   - **「送信」タブ**：送信アクションを選択します（後で設定できます）。
   - **「配信」タブ**：公開／非公開のスケジュールを設定します。

1. **フォーム設定を完了**
   - 「**作成**」をクリックして、フォームの作成ウィザードを開きます。
   - 以下を入力します。
      - **名前**：内部識別子（スペースなし、ハイフン使用）。
      - **タイトル**：フォームの表示名。
      - **GitHub URL**：リポジトリ URL（例：`https://github.com/your-org/your-repo`）。

   ![フォームを作成ウィザード](/help/edge/assets/create-form-wizard.png)

1. **検証**
   - 「**作成**」をクリックしたら、次を検証します。
      - ユニバーサルエディターでフォームが開く。
      - GitHub の URL が正しくリンクされている。
      - コンポーネントパレットが使用できる。
      - フォームキャンバスが表示される。

   ![ユニバーサルエディターのインターフェイス](/help/edge/assets/author-form.png)

**結果**：ユニバーサルエディターでフォームをオーサリングする準備が整いました。

### 手順 2：フォームのオーサリングとデザイン


1. **コンポーネントライブラリへのアクセス**
   - ユニバーサルエディターでコンテンツブラウザーを開きます。
   - コンテンツツリーで、**アダプティブフォーム**&#x200B;コンポーネントに移動します。

   ![コンテンツツリーのナビゲーション](/help/edge/assets/content-tree.png)

1. **フォームフィールドを追加**
   - **追加**&#x200B;アイコンをクリックして、コンポーネントライブラリを開きます。
   - **アダプティブフォームコンポーネント**&#x200B;リストからコンポーネントを追加します。
   - コンポーネントをフォームキャンバスにドラッグ＆ドロップします。

   ![コンポーネントを追加](/help/edge/assets/add-component.png)

1. **フォームをデザイン**
   - プロパティパネルでフィールドのプロパティを設定します。
   - 検証ルールと動作を設定します。
   - 必要に応じてスタイルとレイアウトを調整します。

   ![完了した登録フォーム](/help/edge/assets/contact-us.png)

#### 検証

- すべての必須フィールドが存在する。
- フィールドプロパティが正しく設定されている。
- レイアウトはレスポンシブでアクセス可能である。
- 検証ルールが期待どおりに機能する。

#### 次の手順

- データ処理の[送信アクションを設定](/help/edge/docs/forms/universal-editor/submit-action.md)します。
- 高度な機能について詳しくは、[ユニバーサルエディターガイド](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)を参照してください。

### 手順 3：設定と公開

Edge Delivery Services を設定してフォームを公開します。

**設定：**&#x200B;自動（手動設定は不要）。

- フォームの作成中に、GitHub リポジトリ接続と Edge Delivery Services 設定が作成されます。
- 公開エンドポイントは自動的に設定されます。

**検証：**

- フォームの設定に設定が表示されていることを確認します。
- GitHub URL が正しくリンクされていることを確認します。

![自動 EDS 設定](/help/edge/assets/aem-instance-eds-configuration.png)

#### フォームの公開

1. ユニバーサルエディターで、「**公開**」ボタン（右上隅）をクリックします。
2. ダイアログで公開の成功を確認します。
3. ステージング済みバージョンとライブバージョン用に生成された URL に注意してください。

   ![ユニバーサルエディターの公開](/help/edge/assets/publish-form.png)

- [公開ガイド](/help/edge/docs/forms/universal-editor/publish-forms.md)

## フォーム URL

公開したフォームには、Edge Delivery Services の URL を通じてアクセスできます。

### URL 構造

- **ステージング済み（プレビュー／テスト）：**

  ```
  https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
  ```

- **ライブ（実稼動）：**

  ```
  https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
  ```

#### URL パラメーター

- `<branch>`：GitHub 分岐名（例：`main`、`develop`）
- `<repo>`：GitHub リポジトリ名（例：`my-forms-project`）
- `<owner>`：GitHub 組織またはユーザー名（例：`company-name`）
- `<form_name>`：AEM で定義されたフォーム識別子（例：`contact-us`）

#### 例

組織 `acme-corp` の下にあるリポジトリ `forms-project` のフォーム `contact-us` の例：

- **ステージング済み：** `https://main--forms-project--acme-corp.aem.page/content/forms/af/contact-us`
- **ライブ：** `https://main--forms-project--acme-corp.aem.live/content/forms/af/contact-us`

#### 環境の違い

- **ステージング済み（.page）：**&#x200B;テストの最新の変更。
- **ライブ（.live）：**&#x200B;実稼動用に公開されたコンテンツ。

![URL 構造](/help/edge/docs/forms/universal-editor/assets/url-structure.svg)
*Edge Delivery Services フォーム URL 構造の分類*

#### 視覚的な例

**Edge Delivery Services テンプレート：**

- ステージング済み：![登録フォームのステージング済みバージョン](/help/forms/assets/registration-form-staged-version.png)
- ライブ：![登録フォームのライブバージョン](/help/forms/assets/registration-form-live-version.png)

## トラブルシューティング

Edge Delivery Services を使用した AEM Forms の一般的な問題と解決策を以下に示します。

+++フォームが読み込まれない

**問題：**&#x200B;フォーム URL が 404 または空白のページを返す。

**解決策：**

- URL から `.html` 拡張子を削除します。
- フォームが公開されていることを検証します。
- アダプティブフォームブロックの GitHub リポジトリを確認します。
- フォーム名が URL と一致することを確認します（大文字と小文字を区別）。

+++

+++設定の問題

**問題：** Edge Delivery Services の設定が機能しない。

**解決策：**

- GitHub の URL が `https://github.com/owner/repository` の形式であることを確認します。
- 設定で正しい分岐名を使用します。
- リポジトリへのアクセスを検証します（パブリックまたは認証済み）。
- 正しい GitHub の詳細については、`fstab.yaml` を確認します。

+++

+++公開の問題

**問題：**&#x200B;変更がライブサイトに表示されない。

**解決策：**

- CDN キャッシュが更新されるまで 2～3 分待機します。
- 公開ワークフローが完了したことを確認します。
- まず、ステージング済みの（.page）環境でテストします。
- GitHub リポジトリが更新されていることを確認します。

+++

+++ユニバーサルエディターの問題

**問題：** フォームを編集できないか、コンポーネントが読み込まれない。

**解決策：**

- サポートされているブラウザー（Chrome、Firefox、Safari）を使用します。
- ブラウザーのキャッシュと Cookie を消去します。
- ネットワーク接続を検証します。
- 作成者の権限を確認します。

+++

+++フォーム送信エラー

**問題：**&#x200B;フォーム送信が機能しない。

**解決策：**

- フォームプロパティで送信アクションを設定します。
- 送信エンドポイントを手動でテストします。
- フォームを埋め込む場合は、CORS 設定を確認します。
- 必須フィールドが設定されていることを確認します。

+++

+++パフォーマンスの問題

**問題：**&#x200B;フォームの読み込みが遅いか、パフォーマンスが低い。

**解決策：**

- 画像を最適化します。
- 不要なコンポーネントを削除します。
- Edge Delivery Services CDN を活用します。
- カスタム JavaScript／CSS を最小限に抑えます。

+++

+++ヘルプの表示

問題が解決しない場合：

1. Adobe Experience Cloud サービスのステータスを確認してください。
2. [Edge Delivery Services ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=ja)を確認してください。
3. [Adobe Experience League コミュニティ](https://experienceleaguecommunities.adobe.com/)にアクセスしてください。
4. アドビカスタマーケアにお問い合わせください。

+++

## 次の手順

フォームの作成と公開を完了したら、次を考慮します。

- [送信アクションの設定](/help/edge/docs/forms/universal-editor/submit-action.md)：データ処理と統合を設定します。
- [フォームデータモデル](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)：フォームをバックエンドデータソースに接続します。
- [Edge Delivery Services ベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=ja)：パフォーマンスを最大限に高めます。
- [フォーム分析](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html?lang=ja)：フォームのパフォーマンスとユーザーの行動を追跡します。

