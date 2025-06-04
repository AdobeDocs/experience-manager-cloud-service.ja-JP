---
title: AEM Forms用 AI アシスタント（Forms Experience Builder）
description: フォームフラグメントを使用した強力なフォームの迅速な作成
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: a8d64082-a23f-4919-ad66-042faad77d29
source-git-commit: ab071b9159f3d4db275313080d7c14a46096c4de
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---

# AEM Forms用 AI アシスタント（Forms Experience Builder）

>[!NOTE]
>
>
> AEM Forms用 AI アシスタント（Forms Experience Builder）の機能は、**早期導入プログラム** で利用できます。 興味がある場合は、住所からmailto:aem-forms-ea@adobe.comに簡単なメールを送信して、機能へのアクセスをリクエストします。

>[!IMPORTANT]
>
> **ドキュメントは変更される場合があります**：このドキュメントは現在製品に対してテスト中であり、更新および改訂される可能性があります。 AEM Forms用 AI アシスタントが早期導入プログラム中に進化し続けると、機能、コマンド、例が変わる場合があります。

AEM Forms用 AI アシスタントは、フォームの作成方法を変革します。自然言語で必要なものを簡単に説明し、フォームが実現するのを見守るだけです。 Forms Management UI、アダプティブFormsエディター、ユニバーサルエディターで使用でき、意図を理解し、探しているものを正確に構築します。

## はじめに：話しかけるだけです

AI アシスタントは、知識のある同僚と会話するようなものです。 複雑なメニューや設定を学習する代わりに、作成したいものを記述するだけです。

### クイックスタート

紹介ビデオを視聴して、すぐに使い始めます。

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

### AI アシスタントへのアクセス

AI アシスタントには、AEM Formsの 3 つの異なる場所からアクセスできます。

1. **Forms Management UI**
   - Adobe Experience Manager/Forms/Formsとドキュメントに移動します。
   - インターフェイスの左側にある「AI アシスタント」アイコンを探します
   - アイコンをクリックして、AI アシスタント パネルを開きます

   ![AI アシスタント アイコン*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}

2. **アダプティブFormsエディター**
   - Adobe Experience Manager/Forms/Formsとドキュメントに移動します。
   - フォームを選択して編集用に開きます
   - エディターインターフェイスで AI アシスタント アイコンをクリックします

   ![AI アシスタント アイコン*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

3. **ユニバーサルエディター**

   - Adobe Experience Manager/Forms/Formsとドキュメントに移動します。
   - インターフェイスの左側にある「AI アシスタント」アイコンを探します
   - エディターインターフェイスで AI アシスタント アイコンをクリックします

### 使い方：簡単な会話

AI アシスタントの使用を開始する最適な方法は、自然言語を使用することです。 その方法を次に示します。

**必要なものを記述してください：**

- 「Web サイトの連絡先フォームを作成する」
- 「評価尺度を含むカスタマーフィードバックフォームが必要です」
- 「今後のイベントの登録フォームを作成する」
- 「製品満足度に関する簡単な調査の作成」

**詳細を追加する：**

- 「名前、メール、電話、メッセージのフィールドを使用して連絡先フォームを作成する」
- 「会議には複数のステップから成る登録フォームが必要です」
- 「5 つ星の評価とコメントセクションを使用した顧客フィードバックフォームの作成」

**既存のフィールドを参照：**

- 「メールフィールドを必須にする」（@email）
- 「電話番号フィールドに検証を追加」（@phoneNumber:）
- 「既婚の場合にのみ配偶者の情報を表示する」（@spouseInfo および@maritalStatus）

### あなたにもできること

自然言語以外にも、AI アシスタントは以下の方法でやり取りすることができます。

- **ファイルのアップロード**：イメージ、PDF、Figma デザインを添付して、想定している AI を表示します
- **クイックコマンドの使用**:`/` と入力すると、一般的なアクションに使用できるショートカットが表示されます
- **参照固有のフィールド**:`@fieldName` を使用して、既存のフォームフィールド（`@firstName`、`@emailAddress` など）を変更します

## 作成できる内容：有効な例

次に、シンプルな自然言語を使用して実行できる実際の例を示します。

### 新しいフォームの開始

**シンプルアプローチ：**

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

**基本追加：**

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

**複雑なビジネス・ルール：**

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

### 送信と統合

**基本送信：**

```
"Send form data to our email"
"Save responses to a spreadsheet"
"Redirect to a thank you page"
```

**高度な統合：**

```
"Send form submissions to hr@company.com and create a case in our CRM system"
"Submit data to our REST API endpoint and trigger the new customer workflow"
"Email responses to the sales team and add the lead to our marketing automation platform"
```

## 添付ファイルの操作

AI が探しているものを正確に理解できるように、ファイルをアップロードします。

### サポートされているファイルタイプ

| ファイルタイプ | に最適 | 使用例 |
|-----------|----------|-------------|
| **画像** （PNG、JPG、GIF） | フォームレイアウト、UI モックアップ、紙のフォームスキャン | 「このレイアウトに一致するフォームを作成する」 |
| **PDF ファイル** | 変換する既存のフォーム、仕様 | 「このPDF フォームをデジタルに変換する」 |
| **Figma ファイル** | プロトタイプの設計、ブランドガイドライン | 「Figma デザインからこのフォームを作成」 |
| **設計ファイル** | ビジュアル参照、スタイルガイド | 「このデザインのスタイル設定に合わせる」 |

### 添付ファイルの使用方法

1. AI アシスタント インターフェイスの **添付ファイルアイコンをクリック**
2. デバイスから **ファイルを選択** します
3. 添付ファイルを参照する **必要な内容を記述**:
   - 「添付されたこのPDFに基づいてフォームを作成する」
   - 「この画像のレイアウトに合わせて連絡先フォームを作成する」
   - 「この紙の用紙をデジタル版に変換する」

### 添付ファイルを使用したベストプラクティス

- **クリアで高品質な画像を使用** して AI 解析を改善
- **添付ファイルごとに 1 つの概念（レイアウト** スタイル設定など）に焦点を当てる
- **望むものを添付ファイルと共に記述**
- 最適な処理のために **ファイルを 10 MB 未満に保つ**

## 最良の結果を得るためのヒント

### シンプルな作業から開始し、構築する

- 基本的なリクエストから開始する：「お問い合わせフォームを作成する」
- 詳細を徐々に追加する：「メールフィールドに検証を追加します」
- テストと調整：「電話フィールドをオプションにする」

### 必要に応じて具体的に指定

- 代わりに、「美しくする」
- 試す：「プロのカラーとクリーンなタイポグラフィを使用する」

### 自然言語を使用

- 代わりに、「テキスト入力コンポーネントを追加」を使用します
- 試す：「名のフィールドを追加」

### 既存の要素の参照

- 既存のフィールドに `@fieldName` を使用：「@email を必須にする」
- フィールド名については、「@phoneNumber フィールドを更新」と明記してください。

### 複雑なリクエストの分類

- 大きなリクエストを 1 つするのではなく、小さなリクエストを複数試します
- ステップごとにフォームを作成する
- 次の変更に移動する前に各変更をテスト

## 製品ヘルプとラーニング

AI アシスタントから、AEM Formsの機能について学習することもできます。

### 次のような質問をします。

- 複数手順フォームを作成するにはどうすればよいですか？
- 「パネルとセクションの違いは何ですか？」
- 「メール通知を設定するにはどうすればよいですか？」
- 「モバイル対応フォームのベストプラクティスは何ですか？」
- 「フォームにテーマを適用するにはどうすればよいですか？」

### ヘルプ情報：

- AEM Formsの概念と用語
- 複雑な機能の手順
- ベストプラクティスと推奨事項
- 一般的な問題のトラブルシューティング

## 高度な機能リファレンス

高度な機能を試してみたいユーザー向け：

### クイックコマンド

`/` と入力して、使用可能なショートカットを確認します：

| コマンド | 目的 | 例 |
|---------|---------|---------|
| `/create-form` | 新しいフォームを開始 | `/create-form customer survey` |
| `/add-form` | ユニバーサルエディターでのフォームの追加 | `/add-form contact form` |
| `/update-layout` | フォーム構造の変更 | `/update-layout wizard with 3 steps` |
| `/update-field` | フィールドプロパティの変更 | `/update-field @email to be required` |
| `/create-rule` | 動的動作の追加 | `/create-rule show @spouse if married` |
| `/create-panel` | フィールドコンテナの追加 | `/create-panel Personal Information` |
| `/configure-submit` | フォーム送信の設定 | `/configure-submit to email support` |
| `/help` | お問い合わせ | `/help multi-step forms` |

### フィールドリファレンスの構文

`@fieldName` を使用して既存のフィールドを参照します。

- `@firstName` – 名フィールド
- `@email` - メールフィールド
- `@phoneNumber` – 電話番号フィールド
- `@dateOfBirth` – 生年月日フィールド

### コンポーネントタイプ

最適な結果を得るには、次の用語を使用します。

- `text input` - 1 行のテキストフィールド
- `text area` – 複数行テキストフィールド
- `dropdown` - リストを選択
- `checkbox` - シングルチェックボックス
- `checkbox group` – 複数のチェックボックス
- `radio group` - ラジオボタングループ
- `date picker` – 日付の選択
- `file upload` - ファイル添付
- `panel` - フィールドをグループ化するためのコンテナ

## トラブルシューティング

### よくある問題と解決策

**AI アシスタントが応答しません：**

- インターネット接続の確認
- サポート対象の環境にいることを確認する
- AI アシスタント パネルを閉じて再度開きます

**予期しない結果：**

- より具体的に要求を言い換えてみてください
- 複雑なリクエストをより小さな手順に分割
- 標準のAEM Forms用語の使用

**フィールド参照が機能しない：**

- チェックフィールド名は、表示されるとおりに正確に入力されます
- 既存 `@fieldName` フィールドに構文を使用する
- フィールドを参照する前に、そのフィールドが存在することを確認します

**設計インポートの問題：**

- ファイルが明確かつ適切に構造化されていることを確認する
- サポートされている形式（PDF、PNG、JPG、Figma）を使用する
- ファイルサイズは 10 MB 未満にしてください

## フィードバックとサポート

AI アシスタントの改善にご協力ください。

- **フィードバックを提供**:AI Assistant インターフェイスの [ フィードバック ] ボタンを使用します
- **問題を報告**：公式チャネルからAdobe サポートにお問い合わせください
- **エクスペリエンスを共有**：入力した内容は、すべてのユーザーにとってアシスタントをより良いものにするのに役立ちます

## 関連リソース

[AEM Forms AI アシスタント – プロンプトライブラリ](/help/edge/docs/forms/ai-assistant-prompt-library.md)
