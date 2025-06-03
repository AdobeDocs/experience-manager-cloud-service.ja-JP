---
title: AEM Forms用 AI アシスタント（Forms Experience Builder）
description: フォームフラグメントを使用した強力なフォームの迅速な作成
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: d3ade6ee9216b44b55d6808d8acffe83f1e263c9
workflow-type: tm+mt
source-wordcount: '2061'
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

AEM Forms用 AI アシスタント（Forms Experience Builder）は、自然言語プロンプトを通じて、一般的なフォーム作成タスクを合理化することで、オーサリングエクスペリエンスを強化します。 Forms Management UI、アダプティブFormsエディター、ユニバーサルエディターで使用でき、作成と設定の両方のアクションをサポートすることで、よりスマートで迅速な構築を可能にします。 このガイドは、基本を学び、その機能を最大限に活用するのに役立ちます。

## はじめに

詳しく説明する前に、AI アシスタントにアクセスしてやり取りする際の基本について説明します。

### AI アシスタントへのアクセス

AI アシスタントには、AEM Formsの 3 つの異なる場所からアクセスできます。

1. **Forms Management UI**
   - Adobe Experience Manager/Forms/Formsとドキュメントに移動します。
   - インターフェイスの左側にある「AI アシスタント」アイコンを探します
   - アイコンをクリックして、AI アシスタント パネルを開きます

   ![AI アシスタント アイコン*](/help/edge/docs/forms/assets/forms-manager.gif)

2. **アダプティブFormsエディター**
   - Adobe Experience Manager/Forms/Formsとドキュメントに移動します。
   - フォームを選択して編集用に開きます
   - エディターインターフェイスで AI アシスタント アイコンをクリックします

   ![AI アシスタント アイコン*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif)

3. **ユニバーサルエディター**

   - Adobe Experience Manager/Forms/Formsとドキュメントに移動します。
   - インターフェイスの左側にある「AI アシスタント」アイコンを探します
   - エディターインターフェイスで AI アシスタント アイコンをクリックします

AI アシスタントは、現在の場所とタスクに基づいて機能を調整し、各コンテキストに関連する支援を提供します。

### 操作方法：

- リクエストを自然言語で入力するだけです。
- `/` を使用して、使用可能なコマンドまたはクイックアクションのリストを表示します。
- アシスタントで特定のフィールドを設定または更新する場合は、`@fieldName` を使用して特定のフォームフィールド（`@firstName`、`@emailAddress` など）を参照します。
- 画像、PDF、Figma ファイル、またはその他のデザインアセットをアップロードすると、AI アシスタントが要件をより深く理解するのに役立ちます。


### クイックスタート

紹介ビデオを視聴して、すぐに使い始めます。

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)


このビデオでは、すべての環境でのアシスタントの起動、基本的なインタラクション、その機能の概要について説明します。

## AI アシスタントのコマンド リファレンス

| コマンド | 説明 | 目的 | 使用コンテキスト | 例 | 主な機能 |
|---------|-------------|---------|---------------|----------|--------------|
| /create-form | Forms Management UI またはForms エディターで新しいフォームを開始する | 完全に新しいフォームの作成をゼロから開始します | Forms Management UI、アダプティブFormsエディター | /create-form 添付のPDFに基づくカスタマーフィードバック調査 | フォーム構造のオプションを提供し、フォームを作成します。 デザイン参照の **添付ファイルをサポート** |
| /add-form | ユニバーサルエディターでの新しいフォームの追加 | ユニバーサルエディター内に新しいフォームブロックまたはコンポーネントを追加します | Edge Delivery Services用ユニバーサルエディター | /add-form 名前とメールアドレスを指定した連絡先フォーム | フォームブロックを挿入し、ブロックベースの編集を行います。 レイアウトガイダンス用 **添付ファイルをサポート** |
| /update-layout | フォームのレイアウトをアコーディオン、タブベース、ウィザードまたは単一ページレスポンシブデザインに変更する | 全体的な構造レイアウトおよびナビゲーション パターンを修正します。 | すべての編集環境 | 3 つのステップを持つ/update-layout ウィザード | アコーディオン、タブ、ウィザード、単一ページレスポンシブオプション |
| /update-field | 既存のフォームフィールドのプロパティと設定の変更 | ラベル、検証、書式設定、動作などのフィールド属性を変更します | すべての編集環境 | 検証では/update-field@email 必須です | ラベル、検証ルール、フィールドタイプ、デフォルト、表示。 フィールドデザインの例に使用できる **添付ファイルをサポート** |
| /create-rule | フォームの動的動作と条件付きロジックの作成 | ビジネスロジック、計算、条件付きインタラクションを実装 | すべての編集環境 | /create-rule @maritalStatus が「既婚」に等しい場合に@spouseName を表示する | 条件付き表示、計算、検証、値設定 |
| /create-panel | 新しいパネルを作成（関連するフィールドをグループ化するためのコンテナ） | 構造コンテナを追加して、フォームフィールドを論理的に整理します | すべての編集環境 | /create-panel 名前、電子メール、電話を使用した個人情報 | フィールドグループ、タイトル、レイアウトオプション、折りたたみ可能なセクション。 パネルレイアウト参照の **添付ファイルをサポート** |
| /add-panel | ユニバーサルエディターのフォームパネルへの画像の変換 | アップロードされた画像を AI を使用して分析し、構造化されたフォームパネルに変換します | ユニバーサルエディター | アップロードされたフォーム画像から/add-panel | 画像認識、ビジュアルから機能への変換、レイアウトの保持。 画像解析用 **添付ファイルが必要** |
| /configure-submit | フォーム送信アクションとデータ処理の設定 | ユーザーが入力済みフォームを送信したときの動作を定義します | すべての編集環境 | `support@company.com` にメールを送信する/configure-submit | メール，REST API, ワークフロー，スプレッドシート，データベース，Power Automate |
| /help | AI アシスタント内のアクセス支援およびドキュメント | AEM Formsに関するコンテキストヘルプ、ガイダンス、回答を提供します。 | すべての編集環境 | /help 複数手順のフォームを作成するにはどうすればよいですか？ | 機能の説明、ガイド、ベストプラクティス、トラブルシューティング |

### コマンド カテゴリ

| カテゴリ | コマンド | プライマリのユースケース |
|----------|----------|-------------------|
| フォームの作成 | /create-form, /add-form | 新しいフォームの開始、フォームブロックの追加 |
| 構造とレイアウト | /update-layout, /create-panel, /add-panel | フォーム構造の整理、ビジュアルデザイン |
| フィールド管理 | /update-field | 個々のフォーム要素の設定 |
| ロジックとルール | /create-rule | 動的な動作と検証の追加 |
| 送信 | /configure-submit | データ処理とワークフローの設定 |
| サポート | /help | お問い合わせとドキュメント |

### 構文ガイドライン

| 要素 | 形式 | 例 | メモ |
|---------|--------|---------|-------|
| コマンド | /command-name | /create-form | 常にスラッシュで開始 |
| フィールド参照 | @fieldName | @email, @firstName | 既存のフィールドに@記号を使用する |
| 自然言語 | Command +説明 | /create-rule if 条件のフィールドを表示 | コマンドと説明テキストの組み合わせ |
| 複数のアクション | 別のコマンド | /create-panel then /update-layout | 一度に 1 つのコマンドを適用 |


### 環境固有の機能

| 環境 | 使用可能なコマンド | 特別な機能 |
|-------------|-------------------|------------------|
| Forms Management UI | /create-form, /help | フォームレベルの作成と管理 |
| アダプティブFormsエディターとユニバーサルエディター | すべてのコマンド | フル機能セット、詳細構成 |



### フィールドリファレンスの構文（コンテキスト要素）

`@fieldName` を使用して既存のフィールドを参照します。

- `@firstName` – 名フィールド
- `@email` - メールフィールド
- `@phoneNumber` – 電話番号フィールド
- `@dateOfBirth` – 生年月日フィールド

### コンポーネントタイプ

このリストでは、一般的なコンポーネントタイプについて説明します。 AI は、バリエーションやより特殊なタイプを認識する場合がありますが、これらの正確な用語を使用すると最適な結果が得られます。

- `text input` - 1 行のテキストフィールド
- `text area` – 複数行テキストフィールド
- `dropdown` - リストを選択
- `checkbox` - シングルチェックボックス
- `checkbox group` – 複数のチェックボックス
- `radio group` - ラジオボタングループ
- `date picker` – 日付の選択
- `file upload` - ファイル添付
- `panel` - フィールドをグループ化するためのコンテナ


## コア機能と拡張されたプロンプトの例

AI アシスタントは、幅広いコマンドを理解できます。 次に、その機能を示すいくつかの例を示します。 「パネル」、「テキスト入力」、「チェックボックス」などのコンポーネントに対して正確な用語を使用することを忘れないでください。

| 機能カテゴリ | 説明 | プロンプトの例 |
| ------------------------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **フォームの作成** | ゼロから、または説明に基づいて新しいフォームを開始します。 | `Create a new form titled 'Employee Onboarding'.` <br> `Generate a customer feedback form with fields for name, email, rating (1-5 stars), and comments.` <br> `Start a simple contact form with name, email, and message fields.` <br> `Design a multi-page registration form for an event.` <br> `Create a form based on the attached PDF template.` |
| **読み込み設計** | 既存のデザイン（画像、Figma、PDF）をAEM フォームに変換する。 | `Import the form design from this uploaded PDF file.` <br> `Convert the uploaded Figma design into an adaptive form, focusing on the 'User Profile' frame.` <br> `Use this JPEG image of our old paper form to create a new digital version.` <br> `Create a form based on the layout of the attached PNG.` <br> `Recreate the form shown in the attached screenshot with modern styling.` |
| **コンポーネントとパネルの追加** | 様々なフォームフィールドや構造コンテナ（パネル）を追加します。 | `Add a text input field for 'First Name'.` <br> `Add a 'Personal Details' panel with fields for full name, date of birth, and phone number.` <br> `Insert a checkbox group for 'Interests' with options: Technology, Sports, Music.` <br> `Add a file upload component for 'Resume'.` <br> `Create a repeatable panel named 'WorkExperience' with fields for company, title, and dates.` <br> `Add a panel matching the layout shown in the attached design mockup.` |
| **レイアウトの調整** | フォームのレイアウトの構造と外観を変更します。 | `Change the 'Personal Details' panel to a two-column layout.` <br> `Set the overall form layout to a wizard (multi-step) navigation.` <br> `Make the header section span the full width of the form.` <br> `Adjust the spacing between fields in the 'Address' panel to be compact.` <br> `Align all field labels to the left.` <br> `Update the form layout to match the attached wireframe.` |
| **ルールの作成とロジック** | 動的動作、計算および条件付き表示を実装します。 | `Make the 'Spouse Name' field visible only if 'Marital Status' is selected as 'Married'.` <br> `Calculate the 'Total Amount' by multiplying @quantity and @price.` <br> `Enable the submit button only when the @termsAndConditions checkbox is checked.` <br> `Set the value of @countryCode to '+1' if @country is 'United States'.` <br> `If @age is less than 18, show a message 'Must be 18 or older'.` |
| **フィールドプロパティの更新** | ラベル、プレースホルダーなど、特定のフォームフィールドの属性を変更します。 | `Change the label of @email to 'Primary Email Address'.` <br> `Set the @comment field to be a multi-line text area.` <br> `Make the @phoneNumber field mandatory.` <br> `Add placeholder text 'Enter your ZIP code' to the @zipCode field.` <br> `Change the @country field to a dropdown and populate it with: USA, Canada, UK, Germany.` <br> `Update the help description for @password to 'Must include an uppercase letter, a number, and be at least 8 characters long.'` <br> `Set the maximum length of the @username field to 15 characters.` <br> `Configure the @dateOfBirth field to use a date picker.` <br> `Style the @email field to match the design shown in the attached image.` |
| **送信アクション** | ユーザーがフォームを送信したときの動作を定義します。 | `Configure the form to submit data to the REST endpoint /api/v2/application-submit.` <br> `Set up an email submission to hr@example.com and sales@example.com on successful submission.` <br> `Trigger an AEM workflow named 'NewLeadProcessing' when this form is submitted.` <br> `On submit, redirect the user to a thank you page at /content/thankyou.html.` |
| **テーマ設定** | 既存のAEM Forms テーマを適用して、フォームのスタイルを設定します。 | `Apply the 'Modern Business' theme to this form.` <br> `Switch to the 'Accessible Dark' theme.` <br> `Revert to the default canvas theme.` <br> `Apply styling that matches the brand guidelines shown in the attached style guide.` |
| **ナビゲーションと構造** | ナビゲーション要素を追加するか、フォームの一部を再編成します。 | `Add a 'Next' button to the current panel and a 'Previous' button to the next panel.` <br> `Create a Table of Contents based on the form's panels.` <br> `Move the 'Address' panel to be before the 'Contact Information' panel.` |
| **検証** | フィールドに特定の検証ルールを設定します。 | `Set a regex pattern for the @employeeID field to be 'EMP\d{5}'.` <br> `Ensure the @age field only accepts numeric values between 18 and 99.` <br> `Validate the @email field to ensure it is a valid email format.` |
| **プランのレビュー** （ユニバーサルエディター） | 実行前に、アシスタントが提案した変更をプレビューします。 | `Add a contact form with fields for name, email, subject, and message.` （アシスタントが作成するコンポーネントとプロパティのプランを表示し、[ 適用 ] をクリックします）。<br> `Create a form based on the attached design file.` （アシスタントが添付ファイルを分析し、実装前に詳細な計画を表示します）。 |

## 最適な結果を得るためのベストプラクティス

AI アシスタントを最大限に活用するには、次のヒントに留意してください。

- **シンプルなビルドを増分的に開始：** 最初は複雑な複数ステップのリクエストではなく、小さく具体的なコマンド（「名」のテキスト入力を追加など）から始めます。
- **AEM Formsの用語を使用：** アシスタントがより深く理解できるように、「パネル」、「テキスト入力フィールド」、「チェックボックスグループ」、「送信アクション」、「ルール」などの用語を使用します。
- **フィールドを明確に参照：** 既存のフィールドを設定する場合は、`@fieldName` の表記（`Make @firstName mandatory` など）を使用します。
- **計画のレビュー** 「適用」をクリックする前に、ユニバーサルエディターでアシスタントが提案した変更について、常に慎重に計画をレビューします。
- **手動による検証：** アシスタントが変更を加えた後は、常にフォームをプレビューおよびテストして、動作が期待どおりに表示されることを確認します。 AI は強力なツールですが、最終的な検証が重要です。
- **繰り返し処理と絞り込み：** 最初のプロンプトで正確な結果が得られない場合は、リクエストの言い換えまたは分割を小さなステップに分割してみてください。
- **フィードバックの提供：** 組み込みのフィードバックメカニズムを使用して、アシスタントが学習および改善するのを支援します（「フィードバックとサポート」の節を参照）。

## AI アシスタントの製品ヘルプ

AEM Forms用 AI アシスタントは、ビルドだけでなく、AEM Formsの様々な機能を学習、理解、使用するのにも役立ちます。

### サポートされるヘルプトピック

アシスタントに次のような質問をすることができます。

- 「アダプティブフォームをゼロから新規作成するにはどうすればよいですか？」
- アダプティブFormsのパネルとは何ですか？また、どのように使用されますか？
- 「テーマをフォームに適用する方法を説明する。」
- 「フォームとパネルでサポートされているレイアウトタイプは何ですか？」
- 「メールの送信など、様々な送信アクションを設定するにはどうすればよいですか？」
- 「Figma デザインを使用してフォームを作成する方法を説明できますか？」
- 「複数手順のフォームを作成する最善の方法は何ですか？」

### ヘルプの要求方法：

1. AI アシスタントをForms Management UI またはアダプティブFormsエディターで開きます。
2. 自然言語で質問を入力します（例：「繰り返し可能なパネルを追加するには？」）。
3. アシスタントは次のように応答します。
   - 詳しい手順。
   - AEM Formsの概念の説明。
   - 関連する Adobe Experience League ドキュメントへのリンク（該当する場合）。

### より良いヘルプを得るためのヒント：

- **具体的：** 明確な質問を 1 つずつ尋ねます。
- **キーワードを使用：** AEM Formsの機能または UI 要素に関連するキーワードを含みます（「アダプティブフォームエディター」、「ルールエディター」、「テーマ」など）。
- **必要に応じてフレーズを変更：** アシスタントが必要な情報を理解できない、または提供できない場合は、質問を簡略化するか、別の用語を使用してみてください。


## よくある問題のトラブルシューティング

- **アシスタントが応答しません：**
   - サポートされる環境（Forms管理 UI、アダプティブFormsエディター、ユニバーサルエディター）でアクティブに作業していることを確認します。
   - インターネット接続を確認してください。
   - [AI アシスタント ] パネルを閉じてから、もう一度開いてみてください。

- **不正確または予期しない応答：**
   - より具体的または単純にするために、リクエストのフレーズを変更します。
   - 複雑なリクエストを小さな個々のコマンドに分類します。
   - 標準のAEM Forms用語を使用していることを確認します。

- **デザインの読み込み問題（PDF/Figma/Image）:**
   - デザインファイルが明確で、適切に構造化され、読みやすいことを確認します。
   - ファイル形式がサポートされていることを確認します（PDF、Figma リンク、一般的な画像タイプ（PNG、JPGなど）。
   - Figma の場合、ターゲットにするフレームが明確に定義され、アクセス可能であることを確認します。

- **フィールド `@fieldName` が認識されません：**
   - フォーム内のフィールドの正確な名前を再度確認します。 フィールド名は大文字と小文字が区別され、正確に一致する必要があります。
   - 変更しようとしている場合は、フィールドが既に存在することを確認します。


## フィードバックとサポート

AI アシスタントの継続的な改善に役立つ情報をお寄せください。

- **フィードバックを提供：** AI アシスタントのインターフェイス内で組み込みの **[ フィードバックを提供 ] コマンドまたはボタン** を使用して、エクスペリエンスの共有、問題の報告、機能強化の提案を行います。 （例：`/feedback` と入力するか、フィードバックアイコンを探します）。
- **公式サポート：** 重要な問題やその他のサポートについては、Adobeの公式サポートチャネルまたは組織の指定されたサポート連絡先からお問い合わせください。


## 関連するコンテンツ

[AEM Forms AI アシスタント – プロンプトライブラリ](/help/edge/docs/forms/ai-assistant-prompt-library.md)

## 添付ファイルの操作

AI アシスタントは、フォームの作成および設定操作を拡張するために、添付ファイルをサポートします。 様々なファイルタイプを添付して、変換する視覚的なコンテキスト、デザイン参照、既存のフォームを提供できます。

### サポートされる添付ファイルタイプ

| ファイルタイプ | ユースケース | 添付ファイルをサポートするコマンド | 例 |
|-----------|-----------|-----------------------------------|----------|
| **画像** （PNG、JPG、JPEG、GIF） | フォームレイアウト参照、UI モックアップ、紙のフォームスキャン | /create-form, /add-form, /create-panel, /add-panel, /update-field | 目的のレイアウトのスクリーンショットをアップロード |
| **PDF ファイル** | 変換する既存のフォーム、設計仕様 | /create-form, /add-form, /create-panel, /add-panel | PDF アプリケーションフォームの変換 |
| **Figma ファイル** | システム参照、UI プロトタイプの設計 | /create-form, /add-form, /create-panel | Figma デザインフレームの読み込み |
| **デザインファイル** （スケッチ、Adobe XDの書き出し） | ビジュアルデザインリファレンス | /create-form, /add-form, /create-panel | リファレンスデザインのシステムコンポーネント |

### 添付ファイルの使用方法

1. **コマンドの前またはコマンドを使用してアタッチ：**

   - AI アシスタント インターフェイスの添付ファイルアイコンをクリックします
   - デバイスからファイルを選択
   - 添付ファイルを参照するコマンドを入力してください

2. **コマンドの参照添付ファイル：**

   ```
   /create-form based on the attached PDF application form
   /add-panel using the layout shown in the uploaded image
   /create-panel following the design in the attached Figma file
   /update-field @email to match the style in the attached screenshot
   ```

3. **複数の添付ファイル：**

   - 比較や参照のために複数のファイルを添付できます
   - 使用する添付ファイルを「最初に添付された画像を使用」または「PDF ファイルに基づく」から指定します

### 添付のベストプラクティス

- **クリアで高品質な画像：** アップロードした画像をクリアで読みやすくし、AI 分析を向上
- **関連するファイル名：** AI がコンテキストを理解しやすくするために、わかりやすいファイル名を使用します
- **単一のフォーカス：** 各添付ファイルは、1 つの特定の側面（レイアウト、フィールドデザインなど）にフォーカスする必要があります。
- **サポートされている形式：** 互換性を最大限に高めるために、一般的な形式（PNG、JPG、PDF）にスティックします
- **ファイルサイズ：** 最適な処理速度を実現するために、添付ファイルのサイズを 10 MB 未満に抑える

### 添付ワークフローの例

**用紙フォームの変換：**

1. 用紙をはっきりとスキャンまたは写真に収める
2. 画像ファイルのアップロード
3. 次のコマンドを使用します：`/create-form based on the attached form image, converting all fields to digital equivalents`

**デザインシステムのマッチング：**

1. 関連するデザインコンポーネントの書き出しまたはスクリーンショット
2. デザイン参照をアタッチする
3. 次のコマンドを使用します：`/create-panel following the visual style and layout shown in the attached design`

**フィールドのスタイル設定の参照：**

1. 目的のフィールド表示のスクリーンショットを添付
2. 次のコマンドを使用します：`/update-field @email to match the styling and layout shown in the attached image`
