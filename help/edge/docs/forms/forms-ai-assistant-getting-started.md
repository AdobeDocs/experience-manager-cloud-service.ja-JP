---
title: Forms Experience Builder の概要
description: Forms Experience Builder を使用して、すべてのユーザータイプに対応するプログレッシブディスクロージャーのフォームを作成および管理する方法を説明します
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 9996bc602ae6169dd1aade622d5dbc5b1addeb54
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 15%

---


# Forms Experience Builder の概要

>[!NOTE]
>
> Forms Experience Builder 機能は、**早期導入プログラム** で利用できます。 興味がある場合は、住所から `aem-forms-ea@adobe.com` に簡単なメールを送信して、機能へのアクセスをリクエストします。

>[!IMPORTANT]
>
> **ドキュメントは変更される場合があります**：このドキュメントは現在製品に対してテスト中であり、更新および改訂される可能性があります。Forms Experience Builder が早期導入プログラム中に進化し続けると、機能、コマンド、例が変わる場合があります。

この包括的なガイドは、対話型 AI テクノロジーを使用したフォームの作成と管理を開始する際に役立ちます。 初めてのフォームを作成する初心者でも、高度な機能を活用したい高度なユーザーでも、Forms Experience Builder の機能を順を追って説明する詳細な情報と実例が表示されます。

## 前提条件と設定

### &#x200B;1. アクセスを要求

Forms Experience Builder へのアクセス権がない場合：

1. **アクセスを要求**：勤務先のメールから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にメールを送信します
2. **情報を含める**：組織名とプロジェクトの詳細
3. **承認を待つ**: Adobeは、オンボーディング手順を確認して提供します

### &#x200B;2. Formsが有効になっていることを確認する

Forms Experience Builder を使用する前に、お使いの環境で [AEM Formsが有効になっていることを確認してください ](/help/forms/setup-forms-cloud-service.md)。


### 3.環境のセットアップ


* **Edge Delivery Services（EDS）の場合：**

   * [Edge Delivery Services Formsの設定環境](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
   * [Edge Delivery Forms テンプレートを使用して新しいフォームを作成します](/help/edge/docs/forms/universal-editor/create-forms.md)

* **コアコンポーネントベースのフォームの場合：**

   * Adobe Experience Manager インスタンスで、Forms / Formsとドキュメントに移動します。
   * [コアコンポーネントテンプレートを使用して新しいページを作成](/help/forms/creating-adaptive-form-core-components.md)

## クイックスタート

### Forms Experience Builder へのアクセス

**ユニバーサルエディター**

* ユニバーサルエディターで EDS ページを開きます
* 左側のパネルに表示されているForms Experience Builder アイコンを見つけます
* クリックして対話型インターフェイスを開きます

**アダプティブフォームエディター**

* AEM/Forms/Formsとドキュメントに移動します。
* コアコンポーネントベースのフォームを作成または編集用に開きます
* エディターツールバーでForms Experience Builder アイコンをクリックします

### 最初のフォーム

開始するには、次のシンプルな会話を試してください。

```
👤 You: "Create a simple contact form"
🤖 AI: "I'll create a contact form with name, email, and message fields for you."

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation."
```

### 基本コマンド

| シンボル | 目的 | 使用方法 |
|--------|---------|------------|
| `/` | クイックアクションとショートカット | フォームを作成する場合は「`/create`」、サポートする場合は「`/help`」と入力します |
| `@` | 既存のフォームフィールドの参照 | 特定のフィールドを変更するには、`@fieldName` を入力してください（例：`@email`） |
| テキスト | 自然な会話 | 必要な情報を記述します：「必須の電話番号フィールドを追加」 |

### 成功のためのヒント

* **具体的**:「検証付きの必須メールフィールドを追加」は、「メールを追加」よりも効果的です
* **既存のフィールドを参照**：フォームを変更する際に `@fieldName` を使用する
* **ヘルプを表示**:「`/help`」と入力した後、質問を入力します
* **反復**：最適な結果を得るために、一度に 1 つの変更を行います


## フォームの作成を開始する方法

### 1.自然言語プロンプトから開始する

フォーム要件を自然言語で記述すると、Forms Experience Builder によって完全なフォーム構造が生成されます。

**例：**

* 「個人情報、財務情報およびドキュメントのアップロードを含むローン申請フォームを作成する」
* 「評価、コメント、製品カテゴリを含む顧客フィードバックフォームの作成」
* 「支払い処理に関する会議には複数手順の登録フォームが必要です」

### 2.読み込みと変換

既存のフォームとドキュメントを最新のインタラクティブなエクスペリエンスに変換する：

**サポートされているソース：**

* **PDF forms**：静的 PDF をアップロードして、検証機能を備えたインタラクティブデジタルフォームに変換します。
* **スクリーンショットまたは画像**：紙のフォームの写真をアップロードして、機能のあるデジタルバージョンを生成します
* **HTML Forms**：高度な機能を備えた Enhanced AEM Formsに対して、基本的な Web フォームをインポートして変換します
* **XFA Forms**：従来の XFA ベースのフォームを最新のレスポンシブフォームに変換する
* **URL**:UX を向上させて、既存の web フォームをネイティブのAEM Formsに変換します

**読み込み方法：**

1. Forms Experience Builder インターフェイスの添付ファイルアイコンをクリックします
2. ファイル（PDF、画像、Figma デザインなど）をアップロード
3. 要件を説明します。
   * 「このPDF フォームをデジタル版に変換する」
   * 「このスクリーンショットレイアウトに一致するフォームを作成」
   * 「Figma デザインからこのフォームを作成してください」

**サポートされているファイルタイプ：**

* **画像** （PNG、JPG、GIF）：フォームレイアウト、UI モックアップ、スキャンされたフォーム
* **PDF ファイル**：既存のフォーム、仕様、ドキュメント
* **Figma ファイル**：デザインプロトタイプ、ブランドガイドライン
* **デザインファイル**：ビジュアル参照、スタイルガイド

### 主要なインタラクション

#### フォーム要素の追加

**基本の追加：**

```
👤 You: "Add a section for personal information"
🤖 AI: "Added a personal information panel with standard fields"

👤 You: "Include a file upload for resume"
🤖 AI: "Added a secure file upload component for documents"

👤 You: "Add a dropdown for country selection"
🤖 AI: "Added a country dropdown with common options"
```

**詳細仕様：**

```
👤 You: "Add a personal information panel with fields for full name, date of birth, phone number, and email address"
🤖 AI: "Created a personal information panel with all requested fields and appropriate validation"

👤 You: "Include a secure file upload component for documents, limited to PDF files under 5MB"
🤖 AI: "Added a file upload field with PDF restriction and 5MB size limit"

👤 You: "Add a country dropdown with options for USA, Canada, UK, and Germany"
🤖 AI: "Added a country dropdown with the specified options"
```

#### 動的動作の作成

**シンプルなロジック：**

```
👤 You: "Show additional fields when 'Other' is selected"
🤖 AI: "Created a conditional rule that shows additional fields when 'Other' is chosen"

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation"

👤 You: "Calculate the total automatically"
🤖 AI: "Added calculation logic to automatically compute totals"
```

**複雑なビジネスルール：**

```
👤 You: "Show the spouse information fields only when marital status is set to 'Married'"
🤖 AI: "Created a conditional rule that displays spouse fields based on marital status"

👤 You: "Calculate the total cost by multiplying quantity and price, then add 10% tax"
🤖 AI: "Added calculation logic with quantity, price, and tax computation"

👤 You: "Enable the submit button only when all required fields are completed and terms are accepted"
🤖 AI: "Created validation logic that enables submission only when all conditions are met"
```

#### フォームのレイアウトとデザイン

**レイアウトの変更：**

```
👤 You: "Make this a multi-step form"
🤖 AI: "Converted the form to a progressive layout with navigation"

👤 You: "Organize fields in two columns"
🤖 AI: "Updated the layout to display fields in a two-column arrangement"

👤 You: "Convert to an accordion layout"
🤖 AI: "Transformed the form to use accordion-style sections"
```

**デザインの改良：**

```
👤 You: "Create a wizard-style form with 3 steps: personal info, preferences, and review"
🤖 AI: "Created a wizard form with three distinct steps and navigation"

👤 You: "Arrange the address fields in a compact two-column layout"
🤖 AI: "Organized address fields in a compact two-column format"

👤 You: "Update the layout to match the attached wireframe"
🤖 AI: "Modified the layout to match the provided design reference"
```

### 統合設定

Forms Experience Builder では、様々な送信エンドポイントを設定して、Forms を外部のシステムやサービスと接続できます。

| 統合タイプ | 設定コマンド | ユースケース |
|------------------|---------------|----------|
| **メール** | 「フォームをメールに送信」 | フォーム送信の通知と確認 |
| **REST API** | &quot;REST エンドポイントへの送信&quot; | カスタムアプリケーションとサードパーティシステム |
| **クラウドストレージ** | &quot;Azure/SharePointに保存&quot; | ドキュメントの保存とファイル管理 |
| **ワークフロー** | 「Power Automate に接続」 | ビジネス・プロセスの自動化と承認 |
| **マーケティング** | 「Marketoとの統合」 | リード管理とマーケティング自動化 |

**高度な統合の例：**

```
👤 You: "Send form submissions to hr@company.com and create a case in our CRM system"
🤖 AI: "Configured email submission and CRM integration"

👤 You: "Submit data to our REST API endpoint and trigger the new customer workflow"
🤖 AI: "Set up REST API submission with workflow triggers"

👤 You: "Email responses to the sales team and add the lead to our marketing automation platform"
🤖 AI: "Configured multi-channel submission with email and marketing automation"
```





## 高度なフォーム操作


### 複雑なルールの作成

ユーザーのインタラクションに対応し、データの整合性を確保する高度な検証およびビジネスロジックを作成します。

```
👤 You: "Show the address section only if the user selects 'Ship to different address'"
🤖 AI: "Created a conditional rule that shows/hides the address panel based on checkbox selection"
```

### 複数ステップのフォーム作成

```
👤 You: "Create a progressive form with 3 steps: personal info, preferences, confirmation"
🤖 AI: "Created a progressive form with navigation between steps and validation at each stage"
```

### 高度なフィールドタイプ

* ドキュメント管理のための検証とサイズ制限を含むファイルのアップロード
* スケジュール設定の制約とビジネス ルールを使用した日付選択
* ユーザーの選択に基づいて変化する動的なオプションを含むドロップダウン
* 複雑なデシジョンツリー用の条件付きロジックを備えたラジオボタン


### PDFからフォームへの変換

```
👤 You: "Convert this PDF into an interactive form"
🤖 AI: "Analyzed the PDF and created a form with appropriate field types and validation"
```

### フォームコンバージョンの URL

```
👤 You: "Create a form from this website"
🤖 AI: "Extracted form elements and created a native AEM Form with enhanced functionality"
```

### パフォーマンス分析

```
👤 You: "Analyze this form's conversion performance"
🤖 AI: "Provided insights on form effectiveness and suggested optimizations"
```

### 高度なカスタマイズ

#### カスタム検証ルール

* ユーザー入力に基づいて動的なフォームの動作を作成するフィールドの依存関係
* フォームエクスペリエンスをユーザーのニーズに合わせて調整する複雑な条件付きロジック
* ユーザーに明確なガイダンスを提供するカスタムエラーメッセージ
* 複数の入力間でデータの一貫性を確保するクロスフィールド検証

#### レイアウトの最適化

* モバイルの応答性により、フォームがすべてのデバイスでシームレスに動作することを保証します
* 障害のあるユーザーがフォームを使用できるようにするアクセシビリティコンプライアンス
* ユーザーエンゲージメントと完了率を向上させるビジュアルデザインの改善
* 摩擦を軽減し、満足度を向上させるユーザーエクスペリエンスの強化

#### 統合ワークフロー

* ビジネスワークフローを通じてフォーム送信をルーティングする、複数手順の承認プロセス
* フォームデータを外部システムで必要な形式に変換するデータ変換
* 特定のルールと計算をフォーム送信に適用するカスタムビジネスロジック
* システムの問題からの正常な回復を提供する高度なエラー処理

## コマンドリファレンス

### 基本コマンド

| シンボル | 目的 | 使用方法 |
|--------|---------|------------|
| `/` | クイックアクションとショートカット | フォームを作成する場合は「`/create`」、サポートする場合は「`/help`」と入力します |
| `@` | 既存のフォームフィールドの参照 | 特定のフィールドを変更するには、`@fieldName` を入力してください（例：`@email`） |
| テキスト | 自然な会話 | 必要な情報を記述します：「必須の電話番号フィールドを追加」 |

### スラッシュコマンド

| コマンド | コンテキスト | 使用例 |
|---------|---------|---------------|
| `/create-form` | すべての環境 | `/create-form customer survey` |
| `/add-form` | ユニバーサルエディター | `/add-form contact form` |
| `/update-layout` | フォームエディター | `/update-layout wizard with 3 steps` |
| `/update-field` | フォームエディター | `/update-field @email to be required` |
| `/create-rule` | フォームエディター | `/create-rule show @spouse if married` |
| `/create-panel` | フォームエディター | `/create-panel Personal Information` |
| `/configure-submit` | フォームエディター | `/configure-submit to email support` |
| `/help` | すべての環境 | `/help multi-step forms` |

### フィールド参照

`@fieldName` を使用して既存のフィールドを参照します。

* `@firstName`, `@lastName` *名前フィールド
* `@email`、`@phoneNumber` *連絡先フィールド
* `@address`、`@city`、`@zipCode` *住所フィールド
* `@dateOfBirth`、`@startDate` *日付フィールド

### コンポーネントタイプ

フォーム要素を記述する際は、以下の用語を使用します。

* `text input` * 1 行のテキストフィールド
* `text area` *複数行テキストフィールド
* `dropdown` * オプション付きリストを選択
* `checkbox` *単一チェックボックス
* `checkbox group` *複数のチェックボックス
* `radio group` * ラジオ ボタン グループ
* `date picker` *日付選択フィールド
* `file upload` * ファイル添付フィールド
* `panel` * フィールドをグループ化するためのコンテナ

### 統合コマンド

| サービス | 自然言語コマンド | 要件 |
|---------|--------------------------|--------------|
| メール | 「[ メール」に送信 ] | 有効なメールアドレス |
| REST API | &quot;REST エンドポイントへの送信 [URL]&quot; | API エンドポイントと資格情報 |
| Azure ストレージ | 「Azure ストレージにファイルを保存」 | ストレージアカウント設定 |
| SharePoint | 「SharePointの店舗 [ サイト ]」 | SharePoint サイトへのアクセス |
| Power Automated | 「トリガーの Power Automate フロー」 | フロー設定 |
| Marketo | &quot;Marketoにリードを追加&quot; | Marketo API 資格情報 |

### ヒント

1. **自然言語を使用**:AI は複雑なリクエストを認識し、詳細な要件を解釈できます
2. **具体的**：詳細な説明を使用すると、より良い結果とより正確なフォームの生成が得られます
3. **反復**：会話を通じてフォームを調整し、完全なユーザーエクスペリエンスを達成します
4. **コンテキストの活用**：既存のフォーム要素を参照して、既存の要素を基に作成
5. **徹底的にテスト**：すべてのユーザーシナリオを検証して、フォームが期待どおりに動作することを確認します

## 製品ヘルプと学習

Forms Experience Builder では、AEM Formsの機能についても学習できます。

### 次のような質問をします。

* 複数のステップから成るフォームはどのように作成すればよいですか？
* 「パネルとセクションの違いは何ですか？」
* 「メール通知を設定するにはどうすればよいですか？」
* 「モバイル対応フォームのベストプラクティスは何ですか？」
* 「フォームにテーマを適用するにはどうすればよいですか？」

### ヘルプ情報：

* AEM Formsの概念と用語
* 複雑な機能に対するステップごとの手順
* ベストプラクティスとレコメンデーション
* よくある問題のトラブルシューティング

## ベストプラクティス

### フォームデザイン

* **シンプルに**：不可欠なフィールドから始めて、必要な場合にのみ複雑を追加して、ユーザーに圧倒されないようにします
* **明確なラベルの使用**：フォーム内でユーザーをガイドする説明ラベルを使用して、フィールドの目的を明確にします
* **ヘルプテキストの提供**：コンテキストヘルプと例を含む複雑なフィールドを案内します
* **徹底的にテスト**：すべてのユーザーパスを検証して、すべてのシナリオでフォームが正しく動作することを確認します

### ユーザーエクスペリエンス

* **プログレッシブディスクロージャー**：認知負荷を軽減し完了率を向上させるために、コンテキストに基づいて関連するフィールドを表示します
* **クリアなナビゲーション**：フォーム内の位置と残りの手順を理解しやすくします
* **レスポンシブデザイン**：アクセシビリティを最大限に高めるために、すべてのデバイスと画面サイズでフォームが確実に機能するようにします
* **アクセシビリティ**:WCAG ガイドラインに従って、障害のあるユーザーがフォームを使用できるようにします

### パフォーマンス

* **フィールド数を最適化**：フォームの放棄を減らし、完了率を向上させるために必要な情報のみを要求する
* **適切な検証の使用**：送信前にエラーを防ぎ、迅速なフィードバックとガイダンスを提供する
* **テストの完了率**：分析とユーザーのフィードバックを通じて、フォームの有効性を監視および向上させます
* **定期的な更新**：最適なパフォーマンスを実現するために、ビジネスニーズやユーザーの期待に応じてフォームを常に最新の状態に保ちます

### ブランドの一貫性

* **ブランドテンプレートの作成**：フォームの作成を開始する前に、組織の色、フォント、スタイルを使用してブランド化されたフォームテンプレートを準備します
* **スタイル標準を定義**: プロンプトで参照できる一貫したボタン スタイル、フィールド レイアウト、間隔ガイドラインを確立します
* **ブランドアセットの使用**：フォームを作成する際に簡単に参照できるように、ロゴ、カラーコード、ブランドガイドラインを準備します
* **テンプレートライブラリ**：一般的なユースケース（連絡先、登録、フィードバック）用のブランドフォームテンプレートのコレクションを作成します
* **スタイルプロンプト**：ブランド固有の手順を含めます。「ボタンおよび企業フォントの Helvetica には会社青（#1234AB）を使用します」

### 最良の結果を得るためのヒント

**シンプルな作業から始めて、構築しましょう**

* 基本的なリクエストから開始する：「お問い合わせフォームを作成してください」
* 詳細を徐々に追加する：「メールフィールドに検証を追加してください」
* テストと調整：「電話フィールドをオプションにしてください」

**必要に応じて指定する**

* 「見た目を良くして」の代わりに
* 「プロフェッショナルな配色と洗練されたタイポグラフィを使ってください」と入力してみます

**自然言語を使用**

* 「テキスト入力コンポーネントを追加してください」の代わりに
* 「名のフィールドを追加してください」を試します

**既存の要素の参照**

* 既存のフィールドに `@fieldName` を使用：「@email を必須にします」
* フィールド名については、「@phoneNumber フィールドを更新します」と明記してください。

**複雑なリクエストの分類**

* 大きなリクエストを 1 つするのではなく、小さなリクエストを複数試します
* ステップごとにフォームを作成します
* 次に移動する前に各変更をテストします

## トラブルシューティング

| 問題 | 簡易修正 |
|-------|-----------|
| **インターフェイスが読み込まれない** | ブラウザーを更新し、インターネット接続を確認する |
| **コマンドが機能しない** | `/help` を試すか、代わりに自然言語を使用してください |
| **@fieldName 認識されません** | スペルをチェックし、最初にフィールドが存在することを確認する |
| **ファイルのアップロードに失敗** | 10MB 未満のPDF/JPG/PNG を使用する |
| **フォームが正しく表示されない** | 具体的には、「モバイルに対応させる」を参照してください。 |
| **統合に失敗** | API 資格情報と権限の検証 |

**サポートが必要ですか？** 入力 `/help` に続いて具体的な質問を入力するか、システム管理者にお問い合わせください。

その他のサポートについては、メインの [Forms Experience Builder プロンプトライブラリを参照するか ](ai-assistant-prompt-library.md) システム管理者に技術的なサポートを依頼してください。
