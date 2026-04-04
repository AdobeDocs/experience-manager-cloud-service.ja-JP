---
title: Forms Experience Builderの基本を学ぶ
description: Forms Experience BuilderでAIを利用して、初めてフォームを作成する場合の基本について説明します。 例とベストプラクティスを紹介するステップバイステップチュートリアル。
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: c4f838bc-a001-48e7-afaa-c2ff9034f5d4
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 4%

---

# Forms Experience Builderの基本を学ぶ {#getting-started-forms-experience-builder}

Forms Experience Builderなら、AI （人工知能）を活用して、自然言語による記述を包括的なデジタルフォームに変換できます。これにより、フォーム作成に革命がもたらされます。 このガイドでは、最初のフォームを作成し、Forms Experience Builderを強力なものにするコアコンセプトについて説明します。

## Forms Experience Builderとは何ですか？ {#what-is-forms-experience-builder}

Forms Experience Builderは、AIを活用したフォーム作成ツールです。会話言語を使用して、洗練されたデジタルフォームを作成できます。 従来のドラッグ&amp;ドロップ操作によるインターフェイスや複雑なコーディングの代わりに、求めているものを記述するだけで、AIがフォームを作成します。

**主な機能：**

* **自然言語フォーム作成** - フォームの要件を簡単な英語で説明します

* **インテリジェントなインポートと変換** – 既存のドキュメントをインタラクティブなフォームに変換します

* **スマートフィールドの生成** – 事前入力オプションを備えたAIを活用したフィールド

* **ビジネスロジックの自動化** – 会話による条件付きルールと検証の作成

* **システム統合** - フォームを既存のビジネス ワークフローに接続します

## 前提条件 {#prerequisites-getting-started}

始める前に、次の項目を確認してください。

* **Forms Experience Builder**&#x200B;へのアクセス – 早期アクセスプログラムを通じて利用可能
* **AEM Forms as a Cloud Service** - アダプティブ Forms コアコンポーネントを使用した実稼動用オーサー環境
* **基本的な理解** - フォームの概念とビジネス要件に関する知識

技術的なセットアップ要件と環境設定について詳しくは、[Forms Experience Builderのデプロイと設定](deploy-forms-experience-builder.md)を参照してください。

## フォームの作成方法 {#two-ways-to-create-forms}

Forms ウィザードを使用して、[&#x200B; コアコンポーネントテンプレート &#x200B;](/help/forms/creating-adaptive-form-core-components.md)または[Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md)のテンプレート、テーマ、およびその他のオプションを選択した後、Forms Experience Builderでは、フォーム作成に対する2つの主なアプローチが提供されます。

### &#x200B;1. ゼロから作成 {#create-from-scratch}

自然言語の要件説明を使用してフォームを作成します。

**使用するタイミング：**

* 要件から新しいフォームを作成する

* 新しいビジネスプロセスのためのフォームの作成

* 仕様は明確だが、既存のドキュメントがない場合

**例：**

    次の内容を含む顧客フィードバックフォームを作成します。
     – 製品の評価（1 ～ 5つ星） 
     – 詳細なフィードバック用のコメントフィールド 
     – 顧客の電子メール（オプション） 

>[!VIDEO](https://video.tv.adobe.com/v/3473104)



### &#x200B;2. 読み込みと変換 {#import-and-convert}

既存のドキュメントをインタラクティブなデジタルフォームに変換。

このオプションを使用する前に、PDF ファイルまたはフォームの画像をアップロードします。 PDFは、AcroFormまたはXFA ベースのPDF フォームのいずれかです。 [その他の種類のPDF forms](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/forms/document-services/pdf-forms-and-documents)については、Adobe Acrobatの[Prepare Form](https://helpx.adobe.com/in/acrobat/using/creating-distributing-pdf-forms.html) オプションを使用して、AcroFormに変換します

**使用するタイミング：**

* 既存のPDF formsの変換

* 紙ベースのプロセスを最新化

* 強化するために既存のフォームデザインが

**例：**

    /create-form添付されたPDF ファイルをアダプティブフォームに変換

>[!VIDEO](https://video.tv.adobe.com/v/3474042)


## 最初のフォーム：ステップバイステップチュートリアル {#first-form-tutorial}

簡単な問い合わせフォームを作成して、基本的なワークフローを理解しましょう。

### ステップ 1：簡単な説明から始める {#step-1-simple-description}

最初に、基本的なフォームの説明を入力します。

    名前、メール、メッセージのフィールドを使用して基本的な連絡先フォームを作成します。

これにより、3つの必須フィールドを含むフォームが作成されます。

![3つの必須フィールドを含むフォーム – 自然言語プロンプトを使用して作成](/help/forms/assets/forms-experience-builder-contact-us-form.png)

### 手順2：検証と要件の追加 {#step-2-add-validation}

検証ルールを使用してフォームを強化します。

    適切な検証を行って、@name と @email の必須フィールドを作成します。

`@`記号は、ターゲット変更の特定のフィールドを参照しています。

![自然言語プロンプトを使用して、フォームエクスペリエンスビルダーに検証を追加しました](/help/forms/assets/forms-experience-builder-contact-us-form-add-validation.png)


### ステップ 3：ユーザーエクスペリエンスの向上 {#step-3-improve-ux}

役に立つプレースホルダーテキストとガイダンスを追加：

    プレースホルダーテキストを追加してください。@name &quot;生年月日&quot;, @email &quot;your.email@company.com&quot;, @message &quot;どのようにお手伝いできるかお聞かせください&quot;

![Forms Experience Builderで自然言語プロンプトを使用して検証を追加しました](/help/forms/assets/forms-experience-builder-contact-us-form-add-placeholder.png)

### 手順4：高度な機能の追加 {#step-4-advanced-features}

追加の機能を含めます。

    2つのドロップダウンを追加
    
    &#x200B;- オプション付きの問い合わせタイプ：「一般質問」、「サポートリクエスト」、「営業担当者からの問い合わせ」、「パートナーシップ」 
    
    &#x200B;- オプション付きの緊急性レベル（低、Medium、高） 


![Forms Experience Builderで自然言語プロンプトを使用してドロップダウンコンポーネントを追加しました](/help/forms/assets/forms-experience-builder-contact-us-form-add-dropdown.png)


### 手順5：条件付きロジックの実装 {#step-5-conditional-logic}

次のようなルールを追加することで、コンテキストに即したスマートなビヘイビアーを作成します。

     フォームの読み込み時に@urgencyLevel ドロップダウンを非表示にする
    @urgencyLevel 「サポートリクエスト」に等しい場合にのみドロップダウン（低、Medium、高）@inquiryType表示する

これらは2つの異なるルールです。1つはフォームの読み込み時に緊急レベルのドロップダウンを非表示にし、もう1つは問い合わせタイプが「サポート依頼」の場合にのみ表示します。 個別のプロンプトで各ルールを作成する必要があります。一度に作成できるルールは1つだけです。

## AI会話アプローチを理解する {#ai-conversation-approach}

Forms Experience Builderでは、会話型インターフェイスを使用して、次のことを実行できます。

### @記号を含む参照フィールド {#reference-fields}

`@fieldName`を使用して特定のフィールドを参照します：

    必須フィールドを@email成
    米国の形式の@phoneNumberに検証を追加
     テキストを「メッセージを送信」@submitButton変更

>[!VIDEO](https://video.tv.adobe.com/v/3474043)


### 自然言語コマンドの使用 {#natural-language-commands}

目的を明確な英語で記述する：

     – 会社情報のセクションを追加
     – 部門選択のドロップダウンを作成
     – 履歴書のファイルアップロードを含める

### 段階的に構築 {#build-incrementally}

シンプルに始めて、徐々に複雑さを加えていきます。

1. **基本構造** – 最初に必須フィールドを作成します
2. **検証を追加** – 必須フィールドと形式の検証を実装します
3. **UXの強化** - プレースホルダー、ヘルプテキスト、スタイル設定を追加
4. **ロジックの実装** – 条件付きルールとビジネス ロジックの追加
5. **送信の設定** - フォーム処理と通知の設定


## 共通のフォームパターン {#common-form-patterns}

### 問い合わせフォームとフィードバックフォーム {#contact-feedback-forms}

**基本問い合わせフォーム：**

    次の連絡先フォームを作成します。
     – 名前（必須） 
     – 電子メール（必須、検証済み） 
     – 件名ドロップダウン（一般、サポート、セールス、パートナーシップ） 
     – メッセージ（必須、複数行） 

**顧客フィードバックフォーム：**

    次の内容を含む顧客フィードバックフォームを作成します。
     – 製品の評価（1 ～ 5つ星） 
     – 詳細なフィードバック用のコメントフィールド 
     – 顧客の電子メール（オプション） 

### 登録フォームとオンボーディングフォーム {#registration-onboarding-forms}

**ユーザー登録：**

    次のユーザー登録フォームを作成します。
     – 個人情報（名前、電子メール、電話） 
    &#x200B;- アカウント設定（ニュースレター、通知） 
     – 利用条件の承諾
     – 強度の検証を使用したパスワード作成

**従業員オンボーディング：**

    次の情報を含む従業員オンボーディングフォームを作成します。
     – 個人情報と連絡先情報
     – 雇用情報と開始日
     – 文書のアップロード（履歴書、ID、税務フォーム） 
     – 特典の選択と設定

### 調査/評価フォーム {#survey-assessment-forms}

**顧客満足度調査：**

    次の機能を使用して顧客満足度アンケートを作成します。
     – 総合評価（1 ～ 10尺度） 
    &#x200B;- カテゴリ評価（製品、サービス、サポート） 
    &#x200B;- オープンエンドのフィードバックセクション 
    &#x200B;- デモグラフィック情報（オプション） 

**スキル評価：**

     スキル評価フォームの作成：
     – 熟練度レベルを持つスキルカテゴリ 
     – 各スキルの体験期間
     – 資格認定とトレーニング情報
     – 自己評価と目標

## テストと検証 {#testing-validation}

### フォームを常にテストする {#always-test-forms}

フォームをデプロイする前に：

1. **すべてのフィールドをテストする** – 検証が正しく機能することを確認します

2. **条件付きロジックを検証** - ルールが適切にトリガーされていることを確認します

3. **テスト送信** - データが正しく処理されていることを確認します

4. **様々なデバイスで検証** - モバイルの互換性を確保

5. **関係者とのレビュー** - エンドユーザーからのフィードバックを取得

### 一般的な検証パターン {#validation-patterns}

**電子メール検証：**

    電子メール形式の検証をフィールド@email追加

**電話番号の検証：**

    米国内の電話番号の形式の検証を@phoneNumber
に追加します
**年齢の検証：**

    年齢を追加の検証：@dateOfBirth
の場合は18歳以上である必要があります
**ファイルのアップロードの検証：**

     ファイルの種類を追加の検証：PDF、DOC、DOCXのみ@resume許可
     ファイルサイズの制限を追加：@resume
の最大5 MB
<!-- 

## Next steps {#next-steps}

Now that you understand the basics, explore these advanced topics:

* **[LLM-enhanced smart fields](forms-experience-builder-llm-smart-fields.md)** - Create fields with pre-populated options using AI knowledge
* **[AI-powered form creation](forms-experience-builder-prompt-examples-library.md)** - Advanced prompt patterns and examples
* **[Intelligent import and conversion](intelligent-import-conversion.md)** - Transform existing documents into forms
* **[Form submission and integration](form-submission-integration.md)** - Connect forms to your business systems

-->


## 関連記事

* [Forms Experience Builderの概要](product-overview.md)

<!-- 
* [LLM-enhanced smart fields](forms-experience-builder-llm-smart-fields.md)
* [AI-powered form creation](forms-experience-builder-prompt-examples-library.md)
* [Intelligent import and conversion](intelligent-import-conversion.md)
* [Form submission and integration](form-submission-integration.md)
* [Frequently asked questions](forms-experience-builder-frequently-asked-questions.md)

-->
