---
title: AEM Forms 用 AI アシスタント（Forms Experience Builder）
description: フォームフラグメントを使用した強力なフォームの迅速な作成
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
source-git-commit: 1d378e6c8ac714779e77314d3457a14d40cd222f
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 100%

---


# AEM Forms 用 AI アシスタント（Forms Experience Builder）の基本を学ぶ

>[!NOTE]
>
>
> AEM Forms 用 AI アシスタント（Forms Experience Builder）の機能は、**早期導入プログラム**&#x200B;で利用できます。詳しくは、勤務先のアドレスから :aem-forms-ea@adobe.com にメールを送信して、機能へのアクセスをリクエストします。

>[!IMPORTANT]
>
> **ドキュメントは変更される場合があります**：このドキュメントは現在製品に対してテスト中であり、更新および改訂される可能性があります。早期導入プログラム期間中、AEM Forms 用 AI アシスタントは進化し続けるため、機能、コマンド、例が変更される場合があります。

AEM Forms 用 AI アシスタントは、フォームの作成方法を変革します。自然言語で必要なものを簡単に説明し、フォームが実現するのを確認するだけです。Forms Management UI、アダプティブフォームエディター、ユニバーサルエディターで使用でき、意図を理解し、求めているものを正確に構築します。

## はじめに：話しかけるだけ

AI アシスタントは、知識のある同僚と会話するようなものです。複雑なメニューや設定を学習する代わりに、作成したいものを記述するだけです。

### クイックスタート

概要ビデオを視聴して、すぐに使い始めましょう。

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

### AI アシスタントへのアクセス

AI アシスタントには、AEM Forms の 3 つの異なる場所からアクセスできます。

1. **Forms Management UI**
   - Adobe Experience Manager／Forms／フォームとドキュメントに移動します。
   - インターフェイスの左側にある「AI アシスタント」アイコンを探します
   - アイコンをクリックして、AI アシスタントパネルを開きます

   ![AI アシスタントアイコン*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}

2. **アダプティブフォームエディター**
   - Adobe Experience Manager／Forms／フォームとドキュメントに移動します。
   - フォームを選択して編集用に開きます
   - エディターインターフェイスで AI アシスタントアイコンをクリックします

   ![AI アシスタントアイコン*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

3. **ユニバーサルエディター**

   - Adobe Experience Manager／Forms／フォームとドキュメントに移動します。
   - インターフェイスの左側にある「AI アシスタント」アイコンを探します
   - エディターインターフェイスで AI アシスタントアイコンをクリックします

### 開始方法：簡単な会話

AI アシスタントの使用を開始する最適な方法は、自然言語を使用することです。その方法を次に示します。

**何が必要かを説明する：**

- 「Web サイトの連絡先フォームを作成してください」
- 「評価尺度を含む顧客フィードバックフォームが必要です」
- 「今後のイベントの登録フォームを作成してください」
- 「製品満足度に関する簡単な調査を作成してください」

**必要に応じて詳細を追加：**

- 「名前、メール、電話、メッセージのフィールドを使用して連絡先フォームを作成してください」
- 「会議には複数のステップから成る登録フォームが必要です」
- 「5 つ星の評価とコメントセクションを使用した顧客フィードバックフォームを作成してください」

**既存のフィールドを参照：**

- 「メールフィールドを必須にします」（@email）
- 「電話番号フィールドに検証を追加します」（@phoneNumber）
- 「既婚の場合にのみ配偶者の情報を表示します」（@spouseInfo および @maritalStatus）

### 他にできること

自然言語以外にも、AI アシスタントには以下の方法でやり取りすることができます。

- **ファイルのアップロード**：画像、PDF、Figma デザインを添付して、想定している AI を表示します
- **クイックコマンドの使用**：`/` と入力すると、一般的なアクションに使用できるショートカットが表示されます
- **参照固有のフィールド**：`@fieldName` を使用して、既存のフォームフィールド（`@firstName`、`@emailAddress` など）を変更します

## 作成できる内容：効果的な例

次に、シンプルな自然言語を使用して実行できる実際の例を示します。

### 新しいフォームを開始します。

**簡単なアプローチ：**

```
"Create a contact form"
```

**より詳細なアプローチ：**

```
"Create a professional contact form for a law firm with fields for name, email, phone, case type, and message. Make it mobile-friendly."
```

**デザインリファレンスを使用：**

```
"Create a contact form based on the attached design mockup. Include all the fields shown in the layout."
```

### フォーム要素の追加

**基本の追加：**

```
"Add a section for personal information"
"Include a file upload for resume"
"Add a dropdown for country selection"
```

**詳細仕様：**

```
"Add a personal information panel with fields for full name, date of birth, phone number, and email address"
"Include a secure file upload component for documents, limited to PDF files under 5MB"
"Add a country dropdown with options for USA, Canada, UK, and Germany"
```

### 動的動作の作成

**シンプルなロジック：**

```
"Show additional fields when 'Other' is selected"
"Make the email field required"
"Calculate the total automatically"
```

**複雑なビジネスルール：**

```
"Show the spouse information fields only when marital status is set to 'Married'"
"Calculate the total cost by multiplying quantity and price, then add 10% tax"
"Enable the submit button only when all required fields are completed and terms are accepted"
```

### フォームのレイアウトとデザイン

**レイアウトの変更：**

```
"Make this a multi-step form"
"Organize fields in two columns"
"Convert to an accordion layout"
```

**デザインの改良：**

```
"Create a wizard-style form with 3 steps: personal info, preferences, and review"
"Arrange the address fields in a compact two-column layout"
"Update the layout to match the attached wireframe"
```

<!-- 

### Submission and Integration

**Basic submission:**

```
"Send form data to our email"
"Save responses to a spreadsheet"
"Redirect to a thank you page"
```

**Advanced integration:**

```
"Send form submissions to hr@company.com and create a case in our CRM system"
"Submit data to our REST API endpoint and trigger the new customer workflow"
"Email responses to the sales team and add the lead to our marketing automation platform"
```

-->

## 添付ファイルの操作

AI が探しているものを正確に理解できるように、ファイルをアップロードします。

### サポートされているファイルタイプ

| ファイルタイプ | 次に最適 | 使用例 |
|-----------|----------|-------------|
| **画像**（PNG、JPG、GIF） | フォームレイアウト、UI モックアップ、紙のフォームスキャン | 「このレイアウトに一致するフォームを作成してください」 |
| **PDF ファイル** | 変換する既存のフォーム、仕様 | 「この PDF フォームをデジタルに変換してください」 |
| **Figma ファイル** | プロトタイプの設計、ブランドガイドライン | 「Figma デザインからこのフォームを作成してください」 |
| **設計ファイル** | ビジュアル参照、スタイルガイド | 「このデザインのスタイル設定に合わせてください」 |

### 添付ファイルの使用方法

1. AI アシスタントインターフェイスの&#x200B;**添付ファイルアイコンをクリックします**
2. お使いのデバイスから&#x200B;**テストファイルを選択します**
3. 添付ファイルを参照して、**必要な内容を記述します**
   - 「添付されたこの PDF に基づいてフォームを作成してください」
   - 「この画像のレイアウトに合わせて連絡先フォームを作成してください」
   - 「この紙のフォームをデジタル版に変換してください」

### 添付ファイルを使用したベストプラクティス

- **クリアで高品質な画像を使用**&#x200B;して、AI 分析を改善
- **添付ファイルごとに 1 つの概念**（レイアウト、スタイル設定など）に焦点を当てる
- 添付ファイルと一緒に&#x200B;**必要な内容を記述する**
- 最適な処理のために&#x200B;**ファイルを 10 MB 未満に保つ**

## 最良の結果を得るためのヒント

### シンプルな作業から開始し、構築する

- 基本的なリクエストから開始する：「お問い合わせフォームを作成してください」
- 詳細を徐々に追加する：「メールフィールドに検証を追加してください」
- テストと調整：「電話フィールドをオプションにしてください」

### 必要に応じて具体的に指定する

- 「見た目を良くして」の代わりに
- 「プロフェッショナルな配色と洗練されたタイポグラフィを使ってください」と入力してみます

### 自然言語を使用する

- 「テキスト入力コンポーネントを追加してください」の代わりに
- 「名のフィールドを追加してください」を試します

### 既存の要素を参照する

- 既存のフィールドに `@fieldName` を使用：「@email を必須にします」
- フィールド名については、「@phoneNumber フィールドを更新します」と明記してください。

### 複雑なリクエストは分割する

- 大きなリクエストを 1 つするのではなく、小さなリクエストを複数試します
- ステップごとにフォームを作成します
- 次に移動する前に各変更をテストします

## 製品ヘルプと学習

AI アシスタントから、AEM Formsの機能について学習することもできます。

### 次のような質問をします。

- 複数のステップから成るフォームはどのように作成すればよいですか？
- 「パネルとセクションの違いは何ですか？」
- 「メール通知を設定するにはどうすればよいですか？」
- 「モバイル対応フォームのベストプラクティスは何ですか？」
- 「フォームにテーマを適用するにはどうすればよいですか？」

### ヘルプ情報：

- AEM Formsの概念と用語
- 複雑な機能に対するステップごとの手順
- ベストプラクティスとレコメンデーション
- よくある問題のトラブルシューティング

## 高度な機能のリファレンス

高度な機能を試してみたいユーザー向け：

### クイックコマンド

`/` と入力して、使用可能なショートカットを確認します。

| コマンド | 目的 | 例 |
|---------|---------|---------|
| `/create-form` | 新しいフォームの開始 | `/create-form customer survey` |
| `/add-form` | ユニバーサルエディターでのフォームの追加 | `/add-form contact form` |
| `/update-layout` | フォーム構造の変更 | `/update-layout wizard with 3 steps` |
| `/update-field` | フィールドプロパティの変更 | `/update-field @email to be required` |
| `/create-rule` | 動的動作の追加 | `/create-rule show @spouse if married` |
| `/create-panel` | フィールドコンテナの追加 | `/create-panel Personal Information` |
| `/help` | ヘルプ | `/help multi-step forms` |

<!-- 
| `/configure-submit` | Set up form submission | `/configure-submit to email support` |
-->

### フィールドリファレンスの構文

`@fieldName` を使用して既存のフィールドを参照します。

- `@firstName` – 名フィールド
- `@email` - メールフィールド
- `@phoneNumber` – 電話番号フィールド
- `@dateOfBirth` – 生年月日フィールド

### コンポーネントタイプ

最適な結果を得るには、次の用語を使用します。

- `text input` - 1 行のテキストフィールド
- `text area` - 複数行のテキストフィールド
- `dropdown` - リストを選択
- `checkbox` - 単一のチェックボックス
- `checkbox group` – 複数のチェックボックス
- `radio group` - ラジオボタングループ
- `date picker` – 日付の選択
- `file upload` - ファイル添付
- `panel` - フィールドをグループ化するためのコンテナ

## トラブルシューティング

### よくある問題と解決策

**AI アシスタントが応答しません：**

- インターネット接続を確認する
- サポート対象の環境にいることを確認する
- AI アシスタントパネルを閉じて再度開く

**予期しない結果：**

- より具体的にリクエストを言い換えてみる
- 複雑なリクエストをより小さな手順に分割する
- 標準の AEM Forms 用語を使用する

**フィールド参照が機能しない：**

- フィールド名が表示されているとおりに正確に入力されているか確認する
- 既存フィールドに `@fieldName` 構文を使用する
- フィールドを参照する前に、そのフィールドが存在することを確認します

**デザインの読み込み問題：**

- ファイルが明確かつ適切に構造化されていることを確認する
- サポートされている形式（PDF、PNG、JPG、Figma）を使用する
- ファイルサイズを 10 MB 未満にする

## フィードバックとサポート

AI アシスタントの改善にご協力ください。

- **フィードバックの提供**：AI アシスタントインターフェイスの「フィードバック」ボタンを使用します
- **問題の報告**：公式チャネルからアドビサポートにお問い合わせください
- **エクスペリエンスの共有**：お客様のご意見は、アシスタントをより良くするために役立ちます

## 関連リソース

[AEM Forms AI アシスタント - プロンプトライブラリ](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md)
