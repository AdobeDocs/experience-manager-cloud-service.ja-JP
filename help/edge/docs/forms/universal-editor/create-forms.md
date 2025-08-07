---
title: Edge Delivery Servicesを使用したアダプティブFormsの作成と公開
description: 技術的な精度と明確さを重視して、コアコンポーネントまたはAEMのForms テンプレートを使用してアダプティブ Edge Delivery Servicesを作成、オーサリング、公開する手順を説明します。
keywords: アダプティブフォーム，エッジ配信サービス，コアコンポーネント，ユニバーサルエディター，フォーム作成，AEM forms, テンプレート選択，フォーム公開
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1774'
ht-degree: 5%

---


# Edge Delivery Servicesを使用したアダプティブFormsの作成と公開

このドキュメントでは、Edge Delivery Servicesを使用してAEMでアダプティブFormsを作成、設定および公開する手順について説明します。 コアコンポーネントとEdge Delivery Servicesのテンプレートについて説明します。

このガイドを最後まで学習すると、次の方法を理解することができます。

- ユースケースに適したテンプレートタイプの選択
- コアコンポーネントまたはEdge Delivery Servicesテンプレートを使用してフォームを作成する
- 正しいエディターを使用してフォームを作成する
- フォームの設定とEdge Delivery Servicesへの公開
- 公開済みフォームへのアクセスとデプロイメントの確認

## テンプレートの選択

開始する前に、要件に適合するテンプレートタイプを決定します。

| 条件 | コアコンポーネントテンプレート | Edge Delivery Servicesテンプレート |
|-------------------------|-----------------------------------------|-------------------------------------|
| に最適 | エンタープライズワークフロー、複雑な統合 | 高パフォーマンスの公開フォーム |
| エディター | アダプティブフォームエディター | ユニバーサルエディター |
| 公開 | AEM公開+ Edge Delivery Services | Edge Delivery Servicesのみ |
| 複雑性 | 高度なフォーム機能 | 合理化された高速なフォーム |
| 統合 | 完全なAEM エコシステム | Git ベースの開発 |
| 学習曲線 | AEM ユーザーになじみがある | 最新のシンプルなアプローチ |

**決定ガイダンス：**

- 複雑なワークフローやAEMの深い統合に **コアコンポーネント** を使用する場合や、既存のAEM アセットを活用する場合は、
- パフォーマンス、シンプルさ、最新の開発手法を実現するには、**Edge Delivery Services** を使用します。

![ テンプレート選択の決定 ](/help/edge/docs/forms/universal-editor/assets/template-selection-decision.svg)
*適切なテンプレートタイプを選択するための決定フローチャート*

## 前提条件

続行する前に、次の前提条件が満たされていることを確認してください。

### 技術要件

- **AEM Forms as a Cloud Service**: Forms ライセンスを持つアクティブなオーサーインスタンス。
- **GitHub アカウント**：リポジトリ管理のための個人用または組織用のアカウントです。
- **リポジトリ設定**：次のいずれかを選択します。
   - **新規プロジェクト**:[ アダプティブFormsブロックを使用して新しいAEM プロジェクトを作成します ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)。 リポジトリーは、Edge Delivery Services用に事前設定されています。
   - **既存のプロジェクト**:[ アダプティブ Forms ブロックを既存のリポジトリーに追加 ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) して、設定を更新します。

### 環境設定

- **AEMと GitHub の接続**:AEM インスタンスと GitHub リポジトリの間の [ 接続の確立 ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)。
- **Edge Delivery Services**: リポジトリが自動デプロイメント用に設定されていることを確認してください。
- **権限**：フォームの作成と公開に必要なアクセス権があることを確認します。

### 設定の検証


1. GitHub リポジトリにアダプティブ Forms ブロックが含まれていることを確認します。
2. AEMと GitHub リポジトリ間の接続をテストします。
3. コンテンツをEdge Delivery Servicesに公開できることを確認します。



## フォームの作成と公開のワークフロー

このプロセスは、次の 3 つの主なフェーズで構成されます。

- **フェーズ 1:**&#x200B;[ テンプレートの選択とフォームの作成 ](#step-1-template-selection-and-form-creation)
- **フェーズ 2:**&#x200B;[ フォームのオーサリングとデザイン ](#step-2-form-authoring-and-design)
- **フェーズ 3:**&#x200B;[ 設定と公開 ](#step-3-configuration-and-publishing)

各フェーズには、正しい設定を確認するための検証手順が含まれます。

![3 段階ワークフロー ](/help/edge/docs/forms/universal-editor/assets/three-phase-workflow.svg)
*フォームの作成と公開に関する 3 つの主なフェーズの概要*

### 手順 1：テンプレートの選択とフォームの作成

テンプレートの選択に基づいてワークフローを選択します。

>[!BEGINTABS]

>[!TAB Edge Delivery Services テンプレート ]

**ユースケース：** 高性能フォームと最新の開発ワークフロー。

**機能：** ユニバーサルエディターのオーサリングとEdge Delivery Servicesのパブリッシング。

#### 手順

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

>[!TAB  コアコンポーネントテンプレート ]

**ユースケース：** エンタープライズワークフローと複雑な統合。

**機能：** アダプティブFormsエディターのオーサリング、デュアル公開（AEMとEdge Delivery Services）、高度なフォーム機能。

#### 手順

1. **アクセスフォームの作成**
   - AEM Forms as a Cloud Service オーサーインスタンスにログインします。
   - **Adobe Experience Manager**／**Forms**／**フォームとドキュメント**&#x200B;に移動します。
   - **作成**／**アダプティブフォーム**&#x200B;の順にクリックします。

1. **テンプレートとテーマを選択**
   - 「**Source**」タブで、「**コアコンポーネントベースのテンプレート** を選択します。
   - スタイル設定の **テーマ** を選択します。
   - **作成** ボタンが有効になります。

   ![ コアコンポーネントテンプレートの選択 ](/help/forms/assets/core-component-based-template.png)

1. **オプションを設定（オプション）**
   - **「データSource」タブ**：必要に応じて、「データ統合」を選択します。
   - **「送信」タブ**：送信アクションを選択します（後で設定できます）。
   - **「配信」タブ**：公開/非公開のスケジュールを設定します。

1. **フォーム設定の完了**
   - **作成** をクリックして、フォーム作成ウィザードを開きます。
   - 以下を入力します。
      - **名前**：内部識別子（スペースなし、ハイフン使用）。
      - **タイトル**：フォームの表示名。
      - **パス**:AEM リポジトリ内のストレージの場所。

     ![フォームを作成ウィザード](/help/forms/assets/create-cc-form.png)

1. **検証**
   - **作成** をクリックした後、次の点を確認します。
      - アダプティブFormsエディターでフォームが開きます。
      - コンポーネントツールバーが使用可能です。
      - プロパティパネルにアクセスできます。
      - テーマのスタイル設定が適用されます。

     ![アダプティブフォームエディター](/help/forms/assets/af-editor-form.png)

**結果：** アダプティブ Forms エディターでフォームをオーサリングする準備が整いました。

>[!ENDTABS]

### 手順 2：フォームのオーサリングとデザイン

オーサリングエクスペリエンスはテンプレートによって異なります。

- **Edge Delivery Services テンプレート**: ユニバーサルエディター
- **コアコンポーネントテンプレート**：アダプティブFormsエディター

![ エディターの比較 ](/help/edge/docs/forms/universal-editor/assets/editor-comparison.svg)
*ユニバーサルエディターとアダプティブFormsエディターの機能の比較*

>[!BEGINTABS]

>[!TAB  ユニバーサルエディター（Edge Delivery Services） ]

**インターフェイス：** 最新の合理化された編集で、パフォーマンスが最適化されています。

#### フォームコンポーネントの追加

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
*s 必要に応じてスタイルとレイアウトを調整します。

   ![ 記入済みの登録フォーム ](/help/edge/assets/contact-us.png)

#### 検証

- すべての必須フィールドが存在します。
- フィールドプロパティが正しく設定されている。
- レイアウトはレスポンシブでアクセス可能です。
- 検証ルールは期待どおりに機能します。

#### 次の手順

- データを処理するための [ 送信アクションの設定 ](/help/edge/docs/forms/universal-editor/submit-action.md)。
- 高度な機能については、[ ユニバーサルエディターガイド ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg) を参照してください。

>[!TAB  アダプティブ Forms エディター（コアコンポーネント） ]

**インターフェイス：** 高度なフォーム機能を備えたフル機能の編集。

#### フォームコンポーネントの追加

1. **Access コンポーネントライブラリ**
   - 「**コンポーネントをここにドラッグ**」セクションで「**コンポーネントを挿入**」をクリックします。

   ![ コンポーネント挿入領域 ](/help/forms/assets/drag-components-af-editor.png)

2. **フォームフィールドの追加**
   - **アダプティブフォームコンポーネント** リストを参照します。
   - 目的のコンポーネントをフォームにドラッグします。
   - パネル、ウィザード、データ統合などの高度なコンポーネントを使用します。

   ![ コンポーネントライブラリを追加 ](/help/forms/assets/add-component-af.png)

3. **フォームのデザイン**
   - プロパティパネルでフィールドのプロパティを設定します。
   - 複雑な検証ルールとビジネスロジックを設定します。
   - テーマと高度なスタイル設定を適用します。

   ![ 入力済みの登録フォーム ](/help/forms/assets/af-editor-form.png)

#### 検証

- すべての必須フィールドが存在します。
- 複雑な検証ルールが設定されます。
- テーマのスタイル設定が適用されます。
- データ統合は意図したとおりに機能します（該当する場合）。

#### 次の手順

- 高度なワークフロー用に [ 送信アクションを設定 ](/help/forms/configure-submit-actions-core-components.md) します。
- エンタープライズ機能の [ コアコンポーネントガイド ](/help/forms/creating-adaptive-form-core-components.md)。

>[!ENDTABS]

### 手順 3：設定と公開

Edge Delivery Servicesを設定してフォームを公開します。 プロセスは、テンプレートタイプによって異なります。

#### Edge Delivery Services設定

>[!BEGINTABS]
>[!TAB Edge Delivery Services テンプレート （自動） ]

**設定：** 自動（手動設定は不要）

- GitHub リポジトリ接続とEdge Delivery Services設定は、フォームの作成中に作成されます。
- 公開エンドポイントは自動的に設定されます。

**検証：**

- 設定がフォームの設定に表示されることを確認します。
- GitHub URL が正しくリンクされていることを確認します。

![ 自動 EDS 構成 ](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB  コアコンポーネントテンプレート（手動） ]

**設定：** 手動セットアップが必要です。

#### 手動の設定手順

1. **設定ツールへのアクセス**
   - **ツール**/**Cloud Services**/**Edge Delivery Services Configuration** に移動します。

   ![EDS 構成アクセス ](/help/edge/assets/select-eds-conf.png)

1. **設定の作成**
   - フォーム名と一致するフォルダーを選択します（例：`forms/enrollment-form`）。
   - **作成**/**設定** をクリックします。

   ![EDS 構成の作成 ](/help/forms/assets/create-eds-conf.png)

1. **プロパティの設定**
   - 「**Edge Delivery Services設定**」をクリックします。
   - **プロパティ** を選択して、設定ダイアログを開きます。

   ![設定プロパティ](/help/forms/assets/eds-conf.png)

1. **パラメーターの設定**
   - **必須：**
      - **Organization**:GitHub の組織名。
      - **サイト名**:GitHub リポジトリ名。
      - **ブランチ**：ブランチ名（メインの場合は空のままにします）。
   - **オプション：**
      - **Edge ホスト** : デフォルト （.page と.live の両方に公開）。
      - **サイト認証トークン**：安全な認証用（必要に応じて）。

1. **設定を保存**
   - 「**保存して閉じる**」をクリックします。

#### 検証

- 設定が正常に作成されました。
- GitHub の組織とリポジトリが正しく指定されている。
- ブランチの設定はリポジトリ構造と一致します。
- フォームが設定フォルダーに表示されます。

>[!ENDTABS]

#### フォームの公開

>[!BEGINTABS]
>[!TAB  ユニバーサルエディターの公開 ]

**Edge Delivery Services テンプレートの場合**

1. ユニバーサルエディターで、「**公開**」ボタン（右上隅）をクリックします。
2. ダイアログで公開の成功を確認します。
3. ステージングバージョンとライブバージョンの URL が生成されることに注意してください。

   ![ ユニバーサルエディターの公開 ](/help/edge/assets/publish-form.png)

- [公開ガイド](/help/edge/docs/forms/universal-editor/publish-forms.md)

>[!TAB  アダプティブFormsエディターの公開 ]

1. Experience Manager Forms コンソールで、公開するフォームを選択します。
2. ツールバーの **[!UICONTROL 公開]** をクリックします。 公開する参照アセットを確認します。

![アダプティブフォームエディターでフォームを公開](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> 詳しくは [Experience Manager Formsでの公開の管理 ](/help/forms/manage-publication.md) を参照してください。

>[!ENDTABS]

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

**コアコンポーネントテンプレート：**

- ステージング：![ 登録フォームのステージバージョン ](/help/forms/assets/enrollment-form-staged-version.png)
- ライブ：![ 登録フォームのライブバージョン ](/help/forms/assets/enrollment-form-live-version.png)

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

+++ヘルプ

問題が解決しない場合：

1. Adobe Experience Cloud サービスのステータスを確認します。
2. [Edge Delivery Servicesのドキュメント ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/overview) を確認してください。
3. [Adobe Experience League コミュニティ ](https://experienceleaguecommunities.adobe.com/?profile.language=ja) にアクセスしてください。
4. Adobe カスタマーケアにお問い合わせください。

+++

## 次の手順

フォームの作成と公開を完了したら、次の点を考慮します。

### 即時アクション

- このガイドを使用したフォームのテスト。
- GitHub リポジトリとAEMの接続を検証します。
- サンプルフォームを確認します。

### 高度なトピック

- [ 送信アクションの設定 ](/help/edge/docs/forms/universal-editor/submit-action.md)：データ処理と統合を設定します。
- [ フォームデータモデル ](/help/forms/create-form-data-models.md)：フォームをバックエンドデータソースに接続します。

### パフォーマンスの最適化

- [Edge Delivery Servicesのベストプラクティス ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/overview): パフォーマンスを最大限に高めます。
- [Form Analytics](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html)：フォームのパフォーマンスとユーザーの行動を追跡します。

