---
title: Forms Experience Builder の概要
description: Forms Experience Builder を使用して最初の AI を利用したフォームを作成する際の基本について説明します。 例とベストプラクティスを示したステップバイステップのチュートリアル。
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---


# Forms Experience Builder の概要 {#getting-started-forms-experience-builder}

Forms Experience Builder は、AI を活用して、自然言語の説明を完全に機能するデジタルフォームに変換することにより、フォーム作成に革命をもたらします。 このガイドは、最初のフォームを作成し、Forms Experience Builder を強力にする中心概念を理解するのに役立ちます。

## Forms Experience Builder とは {#what-is-forms-experience-builder}

Forms Experience Builder は、会話言語を使用して高度なデジタルフォームを作成できる、AI を利用したフォーム作成ツールです。 従来のドラッグ&amp;ドロップインターフェイスや複雑なコーディングの代わりに、必要なものを記述するだけで、AI がフォームを作成します。

**主な機能：**

* **自然言語フォームの作成** - フォーム要件をプレーン英語で説明します

* **インテリジェントなインポートと変換** – 既存ドキュメントをインタラクティブなフォームに変換します

* **スマートフィールドの生成** - オプションが事前入力された、AI を利用したフィールド

* **ビジネスロジックの自動化** – 会話を通じて、条件付きルールと検証を作成します

* **システム統合** - フォームを既存のビジネスワークフローに接続します

## 前提条件 {#prerequisites-getting-started}

開始する前に、次のことを確認します。

* **Forms Experience Builder へのアクセス** – 早期アクセスプログラムを通じて利用できます
* **AEM Forms as a Cloud Service** - アダプティブ Forms コアコンポーネントを使用した実稼動オーサー環境
* **基本的な理解** - フォームの概念とビジネス要件に関する知識

技術的な設定要件と環境設定について詳しくは、[Forms Experience Builder のデプロイと設定 &#x200B;](deploy-forms-experience-builder.md) を参照してください。

## フォームの作成方法 {#two-ways-to-create-forms}

Forms ウィザードを使用して { コアコンポーネントテンプレート [&#x200B; または &#x200B;](/help/forms/creating-adaptive-form-core-components.md)2}Edge Delivery Services[&#x200B; のテンプレート、テーマおよびその他のオプションを選択した後、Forms Experience Builder では、主に次の 2 つの方法でフォームを作成できます。](/help/edge/docs/forms/universal-editor/create-forms.md)

### &#x200B;1. ゼロから作成する {#create-from-scratch}

要件を自然言語で記述したフォームの作成

**用途：**

* 要件からの新しいフォームの構築

* 新しいビジネスプロセス用のフォームの作成

* 明確な仕様があるものの、既存のドキュメントがない場合

**例：**

     次の情報を使用して、お客様のフィードバックフォームを作成します。
     – 製品評価（1～5 つ星） 
     – 詳細なフィードバックのコメントフィールド 
     – お客様のメール（オプション） 
    &#x200B;- メール通知に送信 

>[!VIDEO](https://video.tv.adobe.com/v/3473104)



### 2.読み込みと変換 {#import-and-convert}

既存のドキュメントをインタラクティブなデジタルフォームに変換する。

このオプションを使用する前に、PDF ファイルまたはフォームの画像をアップロードします。 PDFは、AcroForm または XFA ベースのPDF フォームのいずれかです。 [&#x200B; その他のタイプのPDF forms](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/forms/document-services/pdf-forms-and-documents) の場合は、Adobe Acrobatの [&#x200B; フォームを準備 &#x200B;](https://helpx.adobe.com/in/acrobat/using/creating-distributing-pdf-forms.html) オプションを使用して、AcroForm に変換します

**用途：**

* 既存のPDF formsの変換

* 紙ベースのプロセスの最新化

* 既存のフォームデザインを拡張する場合

**例：**

    /create-form 添付のPDF ファイルをアダプティブフォームに変換する 

>[!VIDEO](https://video.tv.adobe.com/v/3474042)


## 最初のフォーム：ステップバイステップのチュートリアル {#first-form-tutorial}

基本的なワークフローを理解するために、シンプルな連絡先フォームを作成しましょう。

### 手順 1：簡単な説明から始める {#step-1-simple-description}

フォームの基本的な説明から始めます。

     名前、メール、メッセージのフィールドを含む基本的な連絡先フォームの作成 

これにより、3 つの必須フィールドを持つフォームが作成されます。

![3 つの必須フィールドを持つフォーム – 自然言語プロンプトを使用して作成 &#x200B;](/help/forms/assets/forms-experience-builder-contact-us-form.png)

### 手順 2：検証と要件の追加 {#step-2-add-validation}

検証ルールを使用してフォームを強化します。

     適切な検証を使用して、@name および@email 必須フィールドを設定する 

`@` 記号は、ターゲットを変更するための特定のフィールドを参照します。

![&#x200B; 自然言語プロンプトを使用した form experience builder の検証を追加しました &#x200B;](/help/forms/assets/forms-experience-builder-contact-us-form-add-validation.png)


### 手順 3：ユーザーエクスペリエンスの向上 {#step-3-improve-ux}

有用なプレースホルダーテキストとガイダンスを追加：

     プレースホルダーテキストを追加します：「Your full name」、「your.email@company.com」@email@message 「Tell us how we help （お手伝いできることをお聞かせください）」を@name リックします 

![forms experience builder で自然言語プロンプトを使用した検証を追加しました &#x200B;](/help/forms/assets/forms-experience-builder-contact-us-form-add-placeholder.png)

### 手順 4：高度な機能の追加 {#step-4-advanced-features}

追加機能を含める：

    2 つのドロップダウンを追加 
    
    &#x200B;- 「一般質問」、「サポートリクエスト」、「セールス問い合わせ」、「パートナーシップ」 
    
    &#x200B;- オプション付き緊急度レベル （低、Medium、高） 


![forms experience builder で自然言語プロンプトを使用するドロップダウンコンポーネントを追加しました &#x200B;](/help/forms/assets/forms-experience-builder-contact-us-form-add-dropdown.png)


### 手順 5：条件付きロジックの実装 {#step-5-conditional-logic}

次のようなルールを追加して、スマートでコンテキストに対応した動作を作成します。

     フォームの読み込み時に@urgencyLevel ドロップダウンを非表示にする 
    @urgencyLevel ドロップダウン（低、Medium、高）は、「サポートリクエスト」@inquiryType 等しい場合にのみ表示します 

これらは 2 つの異なるルールです。1 つはフォームの読み込み時に緊急度レベルのドロップダウンを非表示にするルールで、もう 1 つは問い合わせタイプが「サポートリクエスト」の場合にのみドロップダウンを表示するルールです。 個別のプロンプトで各ルールを作成する必要があります。一度に作成できるルールは 1 つだけです。

## AI 会話アプローチについて {#ai-conversation-approach}

Forms Experience Builder では、次の操作が可能な対話型インターフェイスを使用します。

### @記号を含む参照フィールド {#reference-fields}

特定のフィールドを参照するには、`@fieldName` を使用します。

    @email を必須フィールドにする 
     米国の形式の場合は@phoneNumber に検証を追加する 
     テキスト@submitButton 「メッセージを送信」に変更する 

>[!VIDEO](https://video.tv.adobe.com/v/3474043)


### 自然言語コマンドの使用 {#natural-language-commands}

必要な内容を分かりやすい英語で説明します。

     – 会社情報のセクションを追加 
     – 部門選択用のドロップダウンを作成 
     – 再開用にファイルのアップロードを含める 
    &#x200B;- フォームの送信時にメール通知を設定する 

### 増分ビルド {#build-incrementally}

シンプルなスタートから徐々に複雑さを増していきます。

1. **基本構造** – 最初に必須フィールドを作成します
2. **検証を追加** – 必須フィールドと形式検証を実装します
3. **UX の強化** - プレースホルダー、ヘルプテキスト、スタイルを追加します
4. **ロジックの実装** – 条件ルールとビジネスロジックを追加します
5. **送信の設定** - フォーム処理と通知の設定


## 一般的なフォームパターン {#common-form-patterns}

### お問い合わせフォームとフィードバックフォーム {#contact-feedback-forms}

**基本お問い合わせフォーム：**

     次のフォームでお問い合わせフォームを作成：
     – 名前（必須） 
    &#x200B;- メール（必須、検証済み） 
     – 件名ドロップダウン（一般、サポート、セールス、パートナーシップ） 
    &#x200B;- メッセージ（必須、複数行） 
     – 送信ボタン 

**顧客フィードバックフォーム：**

     次の情報を使用して、お客様のフィードバックフォームを作成します。
     – 製品評価（1～5 つ星） 
     – 詳細なフィードバックのコメントフィールド 
     – お客様のメール（オプション） 
    &#x200B;- メール通知に送信 

### 登録およびオンボーディングフォーム {#registration-onboarding-forms}

**ユーザー登録：**

     次を使用してユーザー登録フォームを作成：
     – 個人情報（名前、メール、電話） 
    &#x200B;- アカウントの環境設定（ニュースレター、通知） 
     – 利用条件の承諾 
     – 有効性の検証を使用したパスワードの作成 

**従業員のオンボーディング：**

     次を使用して、従業員のオンボーディングフォームを作成します。
     – 個人情報および連絡先情報 
     – 雇用情報および開始日 
    &#x200B;- ドキュメントアップロード（履歴書、ID、税金フォーム） 
     – 特典の選択および環境設定 

### 調査および評価フォーム {#survey-assessment-forms}

**顧客満足度調査：**

     顧客満足度調査の作成：
     – 総合評価（1 ～ 10 件） 
    &#x200B;- カテゴリ評価（製品、サービス、サポート） 
    &#x200B;- オープンエンドのフィードバックセクション 
     – 人口統計情報（オプション） 

**スキル評価：**

     次のスキル評価フォームを作成します：
     – 習熟度レベルを持つスキルカテゴリ 
     – 各スキルのエクスペリエンス期間 
     – 認定およびトレーニング情報 
     – 自己評価と目標 

## テストと検証 {#testing-validation}

### 常にフォームをテストする {#always-test-forms}

フォームをデプロイする前に、次の手順に従います。

1. **すべてのフィールドをテスト** – 検証が正しく機能することを確認します

2. **条件付きロジックの検証** - ルールが正しくトリガーすることを確認します

3. **送信をテスト** - データが正しく処理されていることを確認します

4. **様々なデバイスで検証** - モバイルの互換性を確保します

5. **関係者とのレビュー** - エンドユーザーからフィードバックを得る

### 一般的な検証パターン {#validation-patterns}

**メールの検証：**

     フィールドにメールフォーマット検証@email 追加 

**電話番号の検証：**

    @phoneNumber に米国の電話番号形式の検証を追加 

**年齢の検証：**

     年齢の検証を追加：@dateOfBirth では 18 歳以上である必要があります 

**ファイルアップロードの検証：**

     ファイルタイプの検証を追加：@resume で許可されるのは、PDF、DOC、DOCX のみです 
     ファイルサイズの制限を追加：@resume で最大 5 MB

## 次の手順 {#next-steps}

これで基本を理解したので、次の詳細なトピックを参照してください。

* **[LLM 拡張スマートフィールド](forms-experience-builder-llm-smart-fields.md)** - AI 知識を使用して、事前入力されたオプションを含むフィールドを作成します。
* **[AI を活用したフォームの作成](forms-experience-builder-prompt-examples-library.md)** – 高度なプロンプトパターンと例
* **[インテリジェントなインポートと変換](intelligent-import-conversion.md)** – 既存のドキュメントをフォームに変換
* **[フォームの送信と統合](form-submission-integration.md)** - フォームをビジネスシステムに接続します


## 関連記事

* [Forms Experience Builder の概要](product-overview.md)
* [LLM 拡張スマートフィールド](forms-experience-builder-llm-smart-fields.md)
* [AI を活用したフォームの作成](forms-experience-builder-prompt-examples-library.md)
* [インテリジェントなインポートと変換](intelligent-import-conversion.md)
* [フォームの送信と統合](form-submission-integration.md)
* [よくある質問](forms-experience-builder-frequently-asked-questions.md)
