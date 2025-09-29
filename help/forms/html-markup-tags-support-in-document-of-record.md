---
title: レコードのドキュメントでサポートされるHTML マークアップタグ
description: レコードのドキュメントの生成で、レンダリングの動作やアクセシビリティに関する考慮事項など、HTMLのマークアップタグのリファレンスガイドがサポートされるようになりました
feature: Adaptive Forms
role: Developer, User
exl-id: 8481b0dc-aae7-4bd2-acfe-1f1b6d747683
source-git-commit: 1794ed6cac612ee4600c2f8e1ced18c6130b64a2
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 9%

---


# レコードのドキュメントでサポートされるHTML マークアップタグ

## このリファレンスで説明する内容

AEM Formsは、レコードのドキュメント（DoR） PDF を生成する際、リッチテキストフィールドでHTMLのマークアップタグをサポートするようになりました。 このガイドでは、アダプティブHTMLで安全に使用できるForms マークアップタグと、生成されたドキュメントでのレンダリング方法について説明します。

フォームにリッチテキストコンテンツ（太字の書式設定、リスト、リンクなど）を追加する場合は、サポートされるタグとその制限事項を理解することが重要です。 このリファレンスは、レコードのドキュメントでコンテンツを正しく表示し、アクセス可能な状態を維持するために適切なタグを選択するのに役立ちます。

## 開始する前に

### 前提条件

次の点に精通している必要があります。

- 基本的なHTML マークアップ構文
- [レコードのドキュメントの基本事項](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- アクセシビリティの原則と WCAG ガイドライン
- PDFのアクセシビリティ要件
- HTMLのマークアップを受け入れるアダプティブフォームコンポーネント

### 考慮事項

レコードのドキュメント（DoR）は、タグ付けされたPDFにすることができ、支援テクノロジーに対するアクセシビリティと適切な構造を確保するのに役立ちます。 タグ付きPDF出力を有効にするには、[XCI プロパティ `config/present/pdf/tagged` を `true`](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file) に設定します。 PDFを生成したら、アクセシビリティタグが正しく適用されていることを確認することが重要です。 [Adobe Acrobatを使用してアクセシビリティタグを確認し ](https://helpx.adobe.com/in/acrobat/using/create-verify-pdf-accessibility.html) ドキュメントがアクセシビリティ標準を満たしていることを確認できます。

### 新機能

レコードのドキュメントでのリッチテキストのサポートは、最近の機能強化です。 以前は、リッチテキストコンテンツは、生成されたドキュメントではプレーンテキストとして表示されていました。 この新しい機能により、フォーマットされたコンテンツをPDF出力で正しくレンダリングできます。

## HTML タグのサポートリファレンス

### 完全にサポートされるタグ

適切なアクセシビリティノードの作成により、次のタグが完全にサポートされます。

| HTML Tag | 説明 | レコードのドキュメントのサポート | アクセシビリティ | 例 |
|----------|-------------|-------------|---------------|---------|
| `<p>` | 段落 | はい | 完全にサポート - `<P>` ノードを修正 | `<p>This is a paragraph.</p>` |
| `<br/>` | 改行 | はい | 完全にサポート – ノード内 `<P>` | `<p>Line 1<br/>Line 2</p>` |
| `<b>` | 太字 | はい | 完全にサポート – ノード内 `<P>` | `<b>bold text</b>` |
| `<i>` | 斜体 | はい | 完全にサポート – ノード内 `<P>` | `<i>italic text</i>` |
| `<span>` | 汎用インラインコンテナ | はい | ブロック要素内 | `<span>styled text</span>` |
| `<sub>` | 下付き文字 | はい | 完全にサポート – ブロック要素内 | `H<sub>2</sub>O` |
| `<sup>` | 上付き文字 | はい | 完全にサポート – ブロック要素内 | `E=mc<sup>2</sup>` |
| `<a>` | ハイパーリンク | はい | 限定的なサポート – 適切なネストが必要 | `<a href="url">link text</a>` |


#### リストのアクセシビリティの問題

現在のリストレンダリングでは、適切なリスト構造ではなく `<P>` 個のノードが作成されます。

```
Current: <P>1. First item
Current: <P>2. Second item

Expected: <L>
Expected:   <LI>
Expected:     <LBL>1.
Expected:     <LBody>First item
```

### サポートされていないタグ

これらのタグはサポートされておらず、正しくレンダリングされません。

| HTML Tag | 説明 | 代替ソリューション |
|----------|-------------|---------------------|
| `<h1>` - `<h6>` | 見出しタグ | スタイル設定された `<p>` タグまたはデザインレベルのヘッダーの使用 |
| `<img>` | 画像 | 個別の画像フィールドまたはデザインテンプレートを使用する |
| `<code>` | コードブロック | `<span>` スタイル設定でモノスペースフォントを使用 |
| `<blockquote>` | ブロック見積 | スタイル設定された `<p>` タグをインデントで使用 |
| `<table>` | テーブル | アダプティブフォームのテーブルコンポーネントの使用 |

## コードの例

### 基本的なテキストフォーマット

```html
<!--  Supported - renders correctly -->
<p>This paragraph contains <b>bold text</b> and <i>italic text</i>.</p>

<!--  Supported - combined formatting -->
<p>This text is <i><b>bold and italic</b></i>.</p>

<!--  Unsupported - headings don't work -->
<h1>This won't render as a heading</h1>
```

### リスト

```html
<!-- ⚠️ Partially supported - renders but not accessible -->
<ol>
  <li>First numbered item</li>
  <li>Second numbered item</li>
</ol>

<ul>
  <li>First bullet point</li>
  <li>Second bullet point</li>
</ul>
```

### リンク

```html
<!--  Supported - but must be within block elements -->
<p>Visit our <a href="https://example.com">website</a> for more information.</p>

<!--  Incorrect - link not properly nested -->
<a href="https://example.com">Standalone link</a>
```

### 指数表記

```html
<!--  Supported - but limited accessibility -->
<p>Water formula: H<sub>2</sub>O</p>
<p>Einstein's equation: E=mc<sup>2</sup></p>
```

## 関連するコンテンツ


- [アダプティブフォームにおけるレコードのドキュメントの生成](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- [コアコンポーネントのレコードのドキュメントを生成](/help/forms/generate-document-of-record-core-components.md)
- [レコードのドキュメントのテンプレートのカスタマイズ](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record)

