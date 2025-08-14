---
title: Edge Delivery Servicesを使用したアダプティブFormsの作成と公開
description: 技術的な正確性と明確さを重視し、AEMのEdge Delivery Services テンプレートを使用してアダプティブ Formsを作成、オーサリングおよび公開する手順を説明します。
keywords: アダプティブフォーム，エッジ配信サービス，ユニバーサルエディター，フォーム作成，AEM forms, フォーム公開
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 4%

---


# Edge Delivery Servicesを使用したアダプティブFormsの作成と公開

このドキュメントでは、AEMのEdge Delivery Services テンプレートを使用して、アダプティブFormsを作成、設定および公開する手順を順を追って説明します。 フォームの作成から実稼動デプロイメントまでの完全なワークフローについて説明します。

このガイドを最後まで学習すると、次の方法を理解することができます。

- Edge Delivery Services テンプレートを使用したフォームの作成
- ユニバーサルエディターを使用したフォームの作成
- フォームの設定とEdge Delivery Servicesへの公開
- 公開済みフォームへのアクセスとデプロイメントの確認



## 前提条件

続行する前に、次の前提条件が満たされていることを確認してください。


- **AEM Forms as a Cloud Service**: Forms ライセンスを持つアクティブなオーサーインスタンス。
- **GitHub アカウント**：リポジトリ管理のための個人用または組織用のアカウントです。
- **リポジトリ設定**：次のいずれかを選択します。
   - **新規プロジェクト**:[ アダプティブFormsブロックを使用して新しいAEM プロジェクトを作成します ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)。 リポジトリーは、Edge Delivery Services用に事前設定されています。
   - **既存のプロジェクト**:[ アダプティブ Forms ブロックを既存のリポジトリーに追加 ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) して、設定を更新します。

- **AEMと GitHub の接続**:AEM インスタンスと GitHub リポジトリの間の [ 接続の確立 ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)。
- **Edge Delivery Services**: リポジトリが自動デプロイメント用に設定されていることを確認してください。
- **権限**：フォームの作成と公開に必要なアクセス権があることを確認します。

- GitHub リポジトリにアダプティブ Forms ブロックが含まれていることを確認します。



## フォームの作成と公開のワークフロー

このプロセスは、次の 3 つの主なフェーズで構成されます。

- **フェーズ 1:**&#x200B;[ フォームの作成 ](#step-1-form-creation)
- **フェーズ 2:**&#x200B;[ フォームのオーサリングとデザイン ](#step-2-form-authoring-and-design)
- **フェーズ 3:**&#x200B;[ 設定と公開 ](#step-3-configuration-and-publishing)

各フェーズには、正しい設定を確認するための検証手順が含まれます。


### 手順 1：フォームの作成

1. **アクセスフォームの作成**
   - AEM Forms as a Cloud Service オーサーインスタンスにログインします。
   - **Adobe Experience Manager**／**Forms**／**フォームとドキュメント**&#x200B;に移動します。
   - **作成**／**アダプティブフォーム**&#x200B;の順にクリックします。

1. **テンプレートを選択**
   - 「**Source**」タブで、**Edge Delivery Servicesベースのテンプレート** を選択します。
   - **作成** ボタンが有効になります。

     ![EDS フォームを作成](/help/edge/assets/create-eds-forms.png)

1. **オプションを設定（オプション）**
   - **「データSource」タブ**：必要に応じて、「データ統合」を選択します。
   - **「送信」タブ**：送信アクションを選択します（後で設定できます）。
   - **「配信」タブ**：公開/非公開のスケジュールを設定します。

1. **フォーム設定の完了**
   - **作成** をクリックして、フォーム作成ウィザードを開きます。
   - 以下を入力します。
      - **名前**：内部識別子（スペースなし、ハイフン使用）。
      - **タイトル**：フォームの表示名。
      - **GitHub URL**：リポジトリ URL （例：`https://github.com/your-org/your-repo`）。

   ![フォームを作成ウィザード](/help/edge/assets/create-form-wizard.png)

1. **検証**
   - **作成** をクリックした後、次の点を確認します。
      - フォームがユニバーサルエディターで開きます。
      - GitHub の URL が正しくリンクされている。
      - コンポーネントパレットを使用できます。
      - フォームキャンバスが表示されます。

   ![ ユニバーサルエディターインターフェイス ](/help/edge/assets/author-form.png)

**結果：** ユニバーサルエディターでフォームをオーサリングする準備が整いました。

### 手順 2：フォームのオーサリングとデザイン


1. **Access コンポーネントライブラリ**
   - ユニバーサルエディターでコンテンツブラウザーを開きます。
   - コンテンツツリーで **アダプティブフォーム** コンポーネントに移動します。

   ![ コンテンツツリーのナビゲーション ](/help/edge/assets/content-tree.png)

1. **フォームフィールドの追加**
   - **追加** アイコンをクリックして、コンポーネントライブラリを開きます。
   - **アダプティブフォームコンポーネント** リストからコンポーネントを選択します。
   - コンポーネントをフォームキャンバスにドラッグ&amp;ドロップします。

   ![ コンポーネントを追加 ](/help/edge/assets/add-component.png)

1. **フォームのデザイン**
   - プロパティパネルでフィールドのプロパティを設定します。
   - 検証ルールと動作を設定します。
   - 必要に応じて、スタイル設定とレイアウトを調整します。

   ![ 記入済みの登録フォーム ](/help/edge/assets/contact-us.png)

#### 検証

- すべての必須フィールドが存在します。
- フィールドプロパティが正しく設定されている。
- レイアウトはレスポンシブでアクセス可能です。
- 検証ルールは期待どおりに機能します。

#### 次の手順

- データを処理するための [ 送信アクションの設定 ](/help/edge/docs/forms/universal-editor/submit-action.md)。
- 高度な機能については、[ ユニバーサルエディターガイド ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg) を参照してください。

### 手順 3：設定と公開

Edge Delivery Servicesを設定してフォームを公開します。

**設定：** 自動（手動設定は不要）

- GitHub リポジトリ接続とEdge Delivery Services設定は、フォームの作成中に作成されます。
- 公開エンドポイントは自動的に設定されます。

**検証：**

- 設定がフォームの設定に表示されることを確認します。
- GitHub URL が正しくリンクされていることを確認します。

![ 自動 EDS 構成 ](/help/edge/assets/aem-instance-eds-configuration.png)

#### フォームの公開

1. ユニバーサルエディターで、「**公開**」ボタン（右上隅）をクリックします。
2. ダイアログで公開の成功を確認します。
3. ステージングバージョンとライブバージョンの URL が生成されることに注意してください。

   ![ ユニバーサルエディターの公開 ](/help/edge/assets/publish-form.png)

- [公開ガイド](/help/edge/docs/forms/universal-editor/publish-forms.md)

## フォーム URL

公開されたフォームには、Edge Delivery Servicesの URL からアクセスできます。

### URL 構造

- **ステージング（プレビュー/テスト）:**

  ```
  https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
  ```

- **ライブ（実稼動）:**

  ```
  https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
  ```

#### URL パラメーター

- `<branch>`:GitHub ブランチ名（例：`main`、`develop`）
- `<repo>`:GitHub リポジトリ名（例：`my-forms-project`）
- `<owner>`:GitHub 組織またはユーザー名（例：`company-name`）
- `<form_name>`:AEMで定義されたフォーム識別子（例：`contact-us`）

#### 例

例えば、リポジトリ `contact-us` の組織 `forms-project` の下にあるフォーム `acme-corp` です。

- **ステージング：** `https://main--forms-project--acme-corp.aem.page/content/forms/af/contact-us`
- **ライブ：** `https://main--forms-project--acme-corp.aem.live/content/forms/af/contact-us`

#### 環境の違い

- **ステージング済み（.page）:** テストの最新の変更。
- **ライブ（.live）:** 実稼動用に公開されたコンテンツ。

![URL 構造 ](/help/edge/docs/forms/universal-editor/assets/url-structure.svg)
*Edge Delivery Services フォーム URL 構造の分類*

#### ビジュアルの例

**Edge Delivery Services テンプレート：**

- ステージング：![ 登録フォームのステージングされたバージョン ](/help/forms/assets/registration-form-staged-version.png)
- ライブ：![ 登録フォームのライブバージョン ](/help/forms/assets/registration-form-live-version.png)

## トラブルシューティング

Edge Delivery Servicesを使用したAEM Formsの一般的な問題と解決策を以下に示します。

+++フォームが読み込まれない

**問題：** フォーム URL が 404 または空白のページを返す。

**解決策：**

- URL から `.html` 拡張機能を削除します。
- フォームが公開されていることを確認します。
- アダプティブ Forms ブロックの GitHub リポジトリを確認してください。
- フォーム名が URL と一致することを確認します（大文字と小文字を区別）。

+++

+++設定の問題

**問題：** Edge Delivery Servicesの設定が機能しません。

**解決策：**

- GitHub の URL が `https://github.com/owner/repository` の形式であることを確認します。
- 設定で正しいブランチ名を使用します。
- リポジトリへのアクセスを確認します（パブリックまたは認証済み）。
- 正しい GitHub の詳細については、`fstab.yaml` を確認してください。

+++

+++公開の問題

**問題：** 変更がライブサイトに表示されません。

**解決策：**

- CDN キャッシュが更新されるまで 2～3 分待ちます。
- 公開ワークフローが完了したことを確認します。
- まず、ステージングされた（.page）環境でテストします。
- GitHub リポジトリが更新されていることを確認します。

+++

+++ユニバーサルエディターの問題

**問題：** フォームを編集できないか、コンポーネントが読み込まれない。

**解決策：**

- サポートされているブラウザー（Chrome、Firefox、Safari）を使用します。
- ブラウザーのキャッシュと Cookie をクリアします。
- ネットワーク接続を確認します。
- 作成者の権限を確認します。

+++

+++フォーム送信エラー

**問題：** フォーム送信が機能しない。

**解決策：**

- フォームプロパティで送信アクションを設定します。
- 送信エンドポイントを手動でテストします。
- フォームを埋め込む場合は、CORS 設定を確認します。
- 必須フィールドが設定されていることを確認します。

+++

+++パフォーマンスの問題

**問題：** フォームの読み込みが遅いか、パフォーマンスが低下している。

**解決策：**

- 画像を最適化します。
- 不要なコンポーネントを削除します。
- Edge Delivery Services CDN の活用
- カスタム JavaScript/CSS を最小化します。

+++

+++ヘルプの表示

問題が解決しない場合：

1. Adobe Experience Cloud サービスのステータスを確認します。
2. [Edge Delivery Servicesのドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/overview) を確認してください。
3. [Adobe Experience League コミュニティ ](https://experienceleaguecommunities.adobe.com/) にアクセスしてください。
4. Adobe カスタマーケアにお問い合わせください。

+++

## 次の手順

フォームの作成と公開を完了したら、次の点を考慮します。

- [ 送信アクションの設定 ](/help/edge/docs/forms/universal-editor/submit-action.md)：データ処理と統合を設定します。
- [ フォームデータモデル ](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)：フォームをバックエンドデータソースに接続します。
- [Edge Delivery Servicesのベストプラクティス ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/overview): パフォーマンスを最大限に高めます。
- [Form Analytics](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html)：フォームのパフォーマンスとユーザーの行動を追跡します。

