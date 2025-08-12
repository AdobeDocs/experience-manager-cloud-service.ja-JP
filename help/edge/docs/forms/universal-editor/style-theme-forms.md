---
title: AEM Forms の Edge Delivery Services のテーマとスタイルのカスタマイズ
description: Edge Delivery Services 経由で配信される AEM Forms のテーマとスタイルを効果的にカスタマイズし、一貫性のあるブランド化されたユーザーエクスペリエンスを実現します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ac780399-34fe-457d-aaf4-b675656c024d
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 55%

---

# フォームの外観をカスタマイズ

AEM Forms用Edge Delivery Servicesのフォームスタイル設定には、CSS カスタムプロパティ、ブロックベースのアーキテクチャ、コンポーネント固有のターゲティング戦略に関する高度な知識が必要です。 従来のフォームスタイル設定アプローチとは異なり、アダプティブ Forms ブロックは、Edge Delivery Servicesのパフォーマンスとアクセシビリティのメリットを維持しながら、一貫したテーマ設定を可能にする体系的な設計トークンシステムを実装します。

アダプティブ Forms ブロックアーキテクチャは、すべてのフォームコンポーネントで標準化されたHTML構造を生成し、CSS のターゲティングとカスタマイズに対して予測可能なパターンを作成します。 この一貫性により、開発者は、Edge Delivery Servicesを非常に高速にするブロックベースのパフォーマンス最適化を維持しながら、複雑なフォーム実装全体に拡張できる包括的なスタイルシステムを実装できます。

この包括的なガイドでは、CSS カスタムプロパティシステム、コンポーネントのEdge Delivery Services構造パターン、高度なスタイル設定手法など、HTML エコシステム内のフォームスタイル設定の技術的基礎について説明します。 このドキュメントでは、高度なブランド化されたフォームエクスペリエンスを作成するための理論的な理解と実践的な実装ガイダンスの両方を提供します。

## マスター内容

**CSS カスタムプロパティのマスター**：カラースキーム、タイポグラフィスケール、間隔システム、レイアウトパラメーターなど、フォームの外観を制御する完全な変数システムについて説明します。 これらのプロパティを上書きおよび拡張して、包括的なブランドテーマを実装する方法を説明します。

**コンポーネントアーキテクチャの理解**：各フォームコンポーネントタイプで使用されるHTML構造パターンに関する深い知識を得ることで、基盤となる機能やアクセシビリティ機能を損なうことなく、CSS の正確なターゲティングとカスタマイズを可能にします。

**高度なスタイル設定手法**：状態ベースのスタイル設定、レスポンシブデザインの統合、Edge Delivery Servicesの高速読み込み特性を維持するパフォーマンスが最適化されたカスタマイズ戦略など、高度なスタイルパターンを実装します。

**プロフェッショナルな実装戦略**：設計システムの統合、保守可能な CSS アーキテクチャ、複雑なスタイルシナリオのトラブルシューティング手法など、フォームスタイル設定に対する業界標準のアプローチを説明します。

## フォームフィールドタイプについて

スタイル設定を開始する前に、アダプティブフォームブロックでサポートされている一般的なフォームの[フィールドタイプ](/help/edge/docs/forms/universal-editor/create-custom-component.md#supported-fieldtypes)を確認します。

- 入力フィールド：テキスト入力、メール入力、パスワード入力などが含まれます。
- チェックボックスグループ：複数のオプションを選択するために使用します。
- ラジオグループ：グループから 1 つのオプションのみを選択する場合に使用します。
- ドロップダウン：選択ボックスとも呼ばれ、リストから 1 つのオプションを選択するのに使用します。
- パネル／コンテナ：関連するフォーム要素をグループ化するのに使用します。

## 基本的なスタイル設定の原則

特定のフォームフィールドのスタイルを設定する前に、[CSS の基本概念](https://www.w3schools.com/css/css_intro.asp)を理解することが重要です。

- [セレクター](https://www.w3schools.com/css/css_selectors.asp)：CSS セレクターを使用すると、特定の HTML 要素をスタイル設定の対象にできます。要素セレクター、クラスセレクターまたは ID セレクターを使用できます。
- [プロパティ](https://www.w3schools.com/css/css_syntax.asp)：CSS プロパティは、要素の外観を定義します。フォームフィールドのスタイル設定に関する一般的なプロパティには、色、背景色、境界線、パディング、余白などがあります。
- [ボックスモデル](https://www.w3schools.com/css/css_boxmodel.asp)：CSS ボックスモデルは、パディング、境界線、余白で囲まれたコンテンツ領域として、HTML 要素の構造を記述します。
- フレックスボックス／グリッド：CSS [フレックスボックス](https://www.w3schools.com/css/css3_flexbox.asp)および[グリッドレイアウト](https://www.w3schools.com/css/css_grid.asp)は、レスポンシブで柔軟なデザインを作成するのに強力なツールです。




## CSS カスタムプロパティを使用した包括的なフォームスタイル設定

アダプティブFormsブロックは、カスタムプロパティ（CSS 変数）に基づいて構築された高度な CSS アーキテクチャを使用して、すべてのフォームコンポーネントに対して体系的なテーマ設定と一貫したスタイル設定を可能にします。 この構造を理解することは、フォームのカスタマイズとブランディングを効果的に行ううえで不可欠です。

### forms.css アーキテクチャについて

デフォルトのフォームスタイルは、プロジェクトリポジトリ（`/blocks/form/form.css`）に配置され、メンテナンス性、一貫性、カスタマイズの柔軟性を優先する構造化されたアプローチに従います。 このアーキテクチャは、次のいくつかの主要なコンポーネントで構成されます。

**CSS カスタムプロパティの基盤**：スタイルシステムは、`:root` レベルで定義された CSS カスタムプロパティに基づいて構築されており、すべてのフォームコンポーネントを通じて連鎖する一元的なテーマシステムを提供します。 これらの変数は、カラー、タイポグラフィ、間隔およびレイアウトプロパティのデザイントークンを設定します。

**ブロックベースの CSS 構造**:Edge Delivery Servicesは、`.form` クラスが、すべてのフォーム関連スタイルのプライマリ名前空間として機能するブロックベースのアーキテクチャを採用し、適切なスコープ分離を確保し、CSS の他のページコンポーネントとの競合を防ぎます。

**コンポーネント固有のスタイル設定**：個々のフォームコンポーネントは、一貫性のあるラッパーパターン（`.{Type}-wrapper`）を使用してスタイル設定されます。このパターンは、デザインシステム全体の整合性を維持しながら、様々なフィールドタイプに対して予測可能なターゲティングを提供します。

### CSS カスタムプロパティのリファレンスとカスタマイズ

フォームのスタイルシステムには、フォームの外観と動作のあらゆる側面を制御する 50 を超える CSS カスタムプロパティが含まれています。 これらのプロパティを理解すると、デザインの一貫性を維持しながら、包括的なカスタマイズが可能になります。

+++ カラー変数とテーマ変数

カラーシステムは、慎重に整理されたカスタムプロパティを通じて、フォームの完全な視覚的基盤を確立します。

```css
:root {
    /* Primary color system */
    --background-color-primary: #fff;
    --label-color: #666;
    --border-color: #818a91;
    --form-error-color: #ff5f3f;
    
    /* Button color system */
    --button-primary-color: #5F8DDA;
    --button-secondary-color: #666;
    --button-primary-hover-color: #035fe6;
    
    /* Form-specific color applications */
    --form-background-color: var(--background-color-primary);
    --form-input-border-color: var(--border-color);
    --form-invalid-border-color: #ff5f3f;
    --form-label-color: var(--label-color);
}
```

**実践的なカスタマイズの例**：フォームにダークテーマを実装するには、ベースカラー変数を上書きします。

```css
:root {
    --background-color-primary: #1a1a1a;
    --label-color: #e0e0e0;
    --border-color: #404040;
    --form-error-color: #ff6b6b;
    --button-primary-color: #4a9eff;
}
```

この単一の変更は、システムがハードコードされた値ではなく変数参照を使用しているので、すべてのフォームコンポーネントに伝播されます。

+++

+++ 文字体裁と間隔の変数

テキストの配置とレイアウトの間隔を設定する変数を使用すると、テキストの表示とレイアウトの間隔を包括的に制御できます。

```css
:root {
    /* Font size system */
    --form-font-size-m: 22px;
    --form-font-size-s: 18px;
    --form-font-size-xs: 16px;
    
    /* Component-specific typography */
    --form-label-font-size: var(--form-font-size-s);
    --form-label-font-weight: 400;
    --form-title-font-weight: 600;
    --form-input-font-size: 1rem;
    
    /* Spacing system */
    --form-field-horz-gap: 40px;
    --form-field-vert-gap: 20px;
    --form-input-padding: 0.75rem 0.6rem;
    --form-padding: 0 10px;
}
```

**実用的なカスタマイズの例**：小さなタイポグラフィでよりコンパクトなフォームレイアウトを作成するには：

```css
:root {
    --form-font-size-m: 18px;
    --form-font-size-s: 14px;
    --form-font-size-xs: 12px;
    --form-field-horz-gap: 20px;
    --form-field-vert-gap: 15px;
    --form-input-padding: 0.5rem 0.4rem;
}
```

+++

+++ レイアウト変数と構造変数

レイアウト変数は、フォームの寸法、グリッドの動作、コンポーネントの配置を制御します。

```css
:root {
    /* Form layout */
    --form-width: 100%;
    --form-columns: 12;
    --form-submit-width: 100%;
    
    /* Card-based components */
    --form-card-border-radius: 4px;
    --form-card-padding: 0.6rem 0.8rem;
    --form-card-shadow: 0 1px 2px rgb(0 0 0 / 3%);
    --form-card-hover-shadow: 0 2px 4px rgb(0 0 0 / 6%);
    
    /* Wizard-specific layout */
    --form-wizard-padding: 0px;
    --form-wizard-padding-bottom: 160px;
    --form-wizard-step-legend-padding: 10px;
}
```

**実用的なカスタマイズの例**：視覚的な深度を強化してカードスタイルのフォームを作成するには：

```css
:root {
    --form-card-border-radius: 12px;
    --form-card-padding: 1.5rem 2rem;
    --form-card-shadow: 0 4px 12px rgb(0 0 0 / 8%);
    --form-card-hover-shadow: 0 8px 24px rgb(0 0 0 / 12%);
    --form-background-color: #f8f9fa;
}

.form {
    background: var(--form-background-color);
    border-radius: var(--form-card-border-radius);
    box-shadow: var(--form-card-shadow);
    padding: var(--form-card-padding);
    max-width: 600px;
    margin: 2rem auto;
}
```

+++

### CSS スタイル設定パターンとベストプラクティス

アダプティブ Forms ブロックは、すべてのコンポーネントにわたって保守性、パフォーマンスおよび一貫性のあるスタイル設定を確実に行うための、特定の CSS パターンに従います。

+++ プライマリのスタイルパターン

**ブロックレベルのフォームコンテナ**：全体的なレイアウトと背景のスタイル設定のプライマリフォームコンテナをターゲットに設定します。

```css
.form {
    /* Form-wide styles */
    max-width: 800px;
    margin: 0 auto;
    background-color: var(--form-background-color);
    padding: var(--form-padding);
    border-radius: var(--form-card-border-radius);
}
```

**コンポーネントラッパーパターン**：一貫性のあるラッパークラスを使用して、特定のフィールドタイプをターゲットに設定します。

```css
/* Text input fields */
.form .text-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
    border-radius: 4px;
    width: 100%;
}

/* Email input fields */
.form .email-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
}

/* Button styling */
.form .button-wrapper button {
    background-color: var(--form-button-background-color);
    color: var(--form-button-color);
    padding: var(--form-button-padding);
    border: var(--form-button-border);
    font-size: var(--form-button-font-size);
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s ease;
}

.form .button-wrapper button:hover {
    background-color: var(--form-button-background-hover-color);
}
```

+++

+++ 高度なカスタマイズパターン

**フィールド固有のターゲティング**：固有のスタイル要件に対応するために、個々のフィールドを名前でターゲットに設定します。

```css
/* Style specific fields */
.form .field-email input {
    background-image: url('data:image/svg+xml;...'); /* Email icon */
    background-repeat: no-repeat;
    background-position: right 12px center;
    padding-right: 40px;
}

.form .field-phone input {
    text-align: center;
    letter-spacing: 1px;
    font-family: monospace;
}
```

**状態ベースのスタイル設定**：検証とインタラクションの状態を実装します。

```css
/* Validation states */
.form .field-wrapper[data-valid="false"] input {
    border-color: var(--form-error-color);
    box-shadow: 0 0 0 2px rgba(255, 95, 63, 0.1);
}

.form .field-wrapper[data-valid="true"] input {
    border-color: #28a745;
    box-shadow: 0 0 0 2px rgba(40, 167, 69, 0.1);
}

/* Focus states */
.form .text-wrapper input:focus,
.form .email-wrapper input:focus {
    outline: none;
    border-color: var(--button-primary-color);
    box-shadow: 0 0 0 2px rgba(95, 141, 218, 0.2);
}
```

+++


## コンポーネント構造

アダプティブフォームブロックは、様々なフォーム要素に対して一貫した HTML 構造を提供し、スタイルと管理を簡単にします。スタイル設定の目的で CSS を使用してコンポーネントを操作できます。

+++ 一般コンポーネント（ドロップダウン、ラジオグループ、チェックボックスグループを除く）：

ドロップダウン、ラジオグループ、チェックボックスグループを除くすべてのフォームフィールドには、次の HTML 構造があります。

#### 一般コンポーネントの HTML 構造

```HTML
  <div class="{Type}-wrapper field-{Name}   field-wrapper" data-required={Required}>
     <label for="{FieldId}" class="field-label">First   Name</label>
     <input type="{Type}" placeholder="{Placeholder}"   maxlength="{Max}" id={FieldId}" name="{Name}"   aria-describedby="{FieldId}-description">
     <div class="field-description" aria-live="polite"  id="{FieldId}-description">
      Hint - First name should be minimum 3 characters  and a maximum of 10 characters.
     </div>
  </div>
```

- クラス：div 要素には、特定の要素とスタイル設定をターゲットにする、いくつかのクラスがあります。フォームフィールドをスタイル設定する CSS セレクターを開発するには、`{Type}-wrapper` または `field-{Name}` クラスが必要です。
- {Type}：フィールドタイプ別にコンポーネントを識別します。例えば、テキスト（text-wrapper）、数値（number-wrapper）、日付（date-wrapper）です。
- {Name}：名前別にコンポーネントを識別します。フィールドの名前に使用できる文字は英数字のみで、名前内の複数の連続するダッシュは 1 つのダッシュ `(-)` に置き換えられ、フィールド名の開始ダッシュと終了ダッシュは削除されます。例えば、名（field-first-name field-wrapper）です。
- {FieldId}：フィールドの一意の ID で、自動的に生成されます。
- {Required}：フィールドが必須かどうかを示すブール値です。
- ラベル：`label` 要素はフィールドの説明テキストを提供し、`for` 属性を使用して入力要素に関連付けます。
- 入力：`input` 要素は、入力するデータのタイプを定義します。例えば、テキスト、番号、メールです。
- 説明（オプション）：クラス `field-description` の `div` は、ユーザーに追加情報または手順を提供します。

**HTML 構造の例**

```HTML
<div class="text-wrapper field-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

#### 一般コンポーネントの CSS セレクター

```css
/* Primary Pattern: Target field wrapper by type */
.form .{Type}-wrapper {
    /* Container styling for specific field types */
    margin-bottom: 1rem;
    border-radius: 4px;
}

/* Primary Pattern: Target input fields within wrapper */
.form .{Type}-wrapper input {
    /* Input field styling using CSS custom properties */
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
}

/* Context-specific: Target element by field name when higher specificity needed */
.form .field-{Name} input {
    /* Field-specific customizations */
    /* Use this pattern for unique styling requirements */
}
```

- `.form .{Type}-wrapper`：フィールドタイプに基づいてフィールドラッパー要素をターゲットに設定します。 例えば、`.form .text-wrapper` は、すべてのテキストフィールドコンテナをターゲットにします。
- `.form .{Type}-wrapper input`：ラッパー内の実際の入力要素をターゲットにします。 これは、フォーム入力のスタイル設定に推奨されるパターンです。
- `.form .field-{Name}`：特定のフィールド名に基づいて要素をターゲット設定します。 例えば、`.form .field-first-name` は「名」フィールドコンテナをターゲットにします。 `.form .field-{Name} input` を使用して、入力要素を具体的にターゲットに設定します。
- **回避**:`main .form form .{Type}-wrapper` – これにより、不要な CSS 特異性が生じ、管理が困難になります。

**一般コンポーネントの CSS セレクターの例**

```css
/* Primary Pattern: Target all text input fields */
.form .text-wrapper input {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
    background-color: var(--form-input-background-color);
}

/* Context-specific: Target field by name when higher specificity needed */
.form .field-first-name input {
    text-transform: capitalize;
    border-color: var(--button-primary-color);
}

/* Alternative with main context if needed */
main .form .text-wrapper input {
    /* Use only when you need higher specificity */
    color: var(--form-label-color);
}
```

+++

+++ ドロップダウンコンポーネント

ドロップダウンメニューの場合、`input` 要素の代わりに `select` 要素を使用します。

#### ドロップダウンコンポーネントの HTML 構造

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**HTML 構造の例**

```HTML
<div class="drop-down-wrapper field-country field-wrapper" data-required="true">
  <label for="country" class="field-label">Country</label>
  <select id="country" name="country">
    <option value="">Select Country</option>
    <option value="US">United States</option>
    <option value="CA">Canada</option>
  </select>
  <div class="field-description" aria-live="polite" id="country-description">
    Please select your country of residence.
  </div>
</div>
```

#### ドロップダウンコンポーネントの CSS セレクター

次の CSS に、ドロップダウンコンポーネントの CSS セレクターの例をいくつか示します。

```css
/* Primary Pattern: Target the dropdown wrapper */
.form .drop-down-wrapper {
    /* Container layout using flexbox */
    display: flex;
    flex-direction: column;
    margin-bottom: var(--form-field-vert-gap);
}

/* Target the select element */
.form .drop-down-wrapper select {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    background-color: var(--form-input-background-color);
    font-size: var(--form-input-font-size);
    color: var(--form-label-color);
}

/* Style the label */
.form .drop-down-wrapper .field-label {
    margin-bottom: 5px;
    font-weight: var(--form-label-font-weight);
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
}
```

- ラッパーをターゲットにする：最初のセレクター（`.drop-down-wrapper`）は外側のラッパー要素をターゲットにし、スタイルがドロップダウンコンポーネント全体に適用されるようにします。
- Flexbox レイアウト：Flexbox は、ラベル、ドロップダウン、説明を垂直に配置して、すっきりとしたレイアウトを実現します。
- ラベルのスタイル設定：ラベルは太字のフォントとわずかな余白で目立ちます。
- ドロップダウンのスタイル設定：`select` 要素には、境界線、パディング、丸い角が追加され、洗練された外観が得られます。
- 背景色：視覚的な調和を図るために、一貫した背景色を設定します。
- 矢印のカスタマイズ：オプションのスタイルでは、デフォルトのドロップダウン矢印を非表示にし、Unicode 文字と位置を使用してカスタム矢印を作成します。

+++

+++ ラジオグループ

ドロップダウンコンポーネントと同様に、ラジオグループにも独自の HTML 構造と CSS 構造があります。

#### ラジオグループの HTML 構造

```HTML
<fieldset class="radio-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="radio" value="" id="{UniqueId}" data-field-type="radio-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

**HTML 構造の例**

```HTML
<fieldset class="radio-group-wrapper field-color field-wrapper" id="color_preference" name="color_preference" data-required="true">
  <legend for="color_preference" class="field-label">Favorite Color:</legend>
  <% for each radio in Group %>
    <div class="radio-wrapper field-color">
      <input type="radio" value="red" id="color_red" data-field-type="radio-group" name="color_preference">
      <label for="color_red" class="field-label">Red</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="green" id="color_green" data-field-type="radio-group" name="color_preference">
      <label for="color_green" class="field-label">Green</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="blue" id="color_blue" data-field-type="radio-group" name="color_preference">
      <label for="color_blue" class="field-label">Blue</label>
    </div>
  <% end for %>
</fieldset>
```

#### ラジオグループの CSS セレクター

- フィールドセットのターゲティング

```css
/* Target radio group container */
.form .radio-group-wrapper {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    margin-bottom: var(--form-field-vert-gap);
}
```

このセレクターは、クラス radio-group-wrapper を持つフィールドセットをターゲットにします。これは、ラジオグループ全体に一般的なスタイルを適用する場合に便利です。

- ラジオボタンラベルのターゲティング

```css
/* Target radio button labels */
.form .radio-wrapper label {
    font-weight: var(--form-label-font-weight);
    margin-right: 10px;
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
    cursor: pointer;
}
```

- 名前に基づいて、特定のフィールドセット内のすべてのラジオボタンラベルをターゲットにする

```css
/* Target all radio button labels within a specific fieldset based on its name */
.form .field-color .radio-wrapper label {
    /* Field-specific radio label customizations */
    /* Add your custom styles here */
}
```

+++

+++ チェックボックスグループ

#### チェックボックスグループの HTML 構造

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="checkbox-wrapper field-{Name}">
      <input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

**HTML 構造の例**

```HTML
<fieldset class="checkbox-group-wrapper field-topping field-wrapper" id="topping_preference" name="topping_preference" data-required="false">
  <legend for="topping_preference" class="field-label">Pizza Toppings:</legend>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="pepperoni" id="topping_pepperoni" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_pepperoni" class="field-label">Pepperoni</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="mushrooms" id="topping_mushrooms" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_mushrooms" class="field-label">Mushrooms</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="onions" id="topping_onions" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_onions" class="field-label">Onions</label>
  </div>
</fieldset>
```

#### チェックボックスグループの CSS セレクター

- 外側のラッパーのターゲティング：これらのセレクターは、ラジオグループとチェックボックスグループの両方の最も外側にあるコンテナをターゲットにし、グループ構造全体に一般的なスタイルを適用できます。これは、間隔、整列、その他のレイアウト関連のプロパティを設定する場合に便利です。

```css
/* Primary Pattern: Targets radio group wrappers */
.form .radio-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between radio groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}

/* Primary Pattern: Targets checkbox group wrappers */
.form .checkbox-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between checkbox groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}
```

- ターゲットグループラベル：このセレクターは、ラジオとチェックボックスの両方のグループラッパー内の`.field-label` 要素をターゲットとします。これにより、これらのグループ専用のラベルのスタイルを設定でき、グループがさらに目立つようになります。

```css
/* Primary Pattern: Target group labels */
.form .radio-group-wrapper legend,
.form .checkbox-group-wrapper legend {
    font-weight: var(--form-title-font-weight); /* Makes the group label bold */
    margin-bottom: 0.5rem;
    font-size: var(--form-fieldset-legend-font-size);
    color: var(--form-fieldset-legend-color);
    padding: var(--form-fieldset-legend-padding);
    border: var(--form-fieldset-legend-border);
}
```

- 個々の入力とラベルのターゲティング：これらのセレクターは、個々のラジオボタン、チェックボックスおよび関連するラベルをより詳細に制御できます。これらを使用して、サイズ調整や間隔の調整を行ったり、より明確な視覚スタイルを適用したりできます。

```css
/* Primary Pattern: Styling radio buttons */
.form .radio-group-wrapper input[type="radio"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling radio button labels */
.form .radio-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}

/* Primary Pattern: Styling checkboxes */
.form .checkbox-group-wrapper input[type="checkbox"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling checkbox labels */
.form .checkbox-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}
```

- ラジオボタンとチェックボックスの外観のカスタマイズ：この方法では、デフォルトの入力を非表示にし、`:before` および `:after` 擬似要素を使用して、「チェック済み」状態に基づいて外観を変更するカスタムビジュアルを作成します。

```css
/* Hide the default radio button or checkbox */
.form .radio-group-wrapper input[type="radio"],
.form .checkbox-group-wrapper input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    width: 1px;
    height: 1px;
}

/* Create a custom radio button */
.form .radio-group-wrapper input[type="radio"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 50%;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .radio-group-wrapper input[type="radio"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    box-shadow: inset 0 0 0 3px var(--form-input-background-color);
}

/* Create a custom checkbox */
.form .checkbox-group-wrapper input[type="checkbox"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 2px;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16"><path fill="white" d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"/></svg>');
    background-repeat: no-repeat;
    background-position: center;
}
```

+++

+++ パネル／コンテナコンポーネント

#### パネル／コンテナコンポーネントの HTML 構造

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
  </div>
</fieldset>
```

**HTML 構造の例**

```HTML
<fieldset class="panel-wrapper field-login field-wrapper">
  <legend for="login" class="field-label" data-visible="false">Login Information</legend>
  <div class="text-wrapper field-username field-wrapper">
    <label for="username" class="field-label">Username</label>
    <input type="text" placeholder="Enter your username" maxlength="50" id="username" name="username">
    <div class="field-description" aria-live="polite" id="username-description">
      Please enter your username or email address.
    </div>
  </div>
  <div class="password-wrapper field-password field-wrapper">
    <label for="password" class="field-label">Password</label>
    <input type="password" placeholder="Enter your password" maxlength="20" id="password" name="password">
    <div class="field-description" aria-live="polite" id="password-description">
      Your password must be at least 8 characters long.
    </div>
  </div>
</fieldset>
```

- fieldset 要素は、パネルコンテナとして機能し、クラス panel-wrapper と、パネル名（field-login）に基づいてスタイル設定する追加クラスがあります。
- 凡例要素（`<legend>`）は、「Login Information」というテキストとクラスのフィールドラベルを含むパネルタイトルとして機能します。 data-visible=&quot;false&quot; 属性を JavaScript で使用すると、タイトルの表示／非表示を制御できます。
- フィールドセット内では、複数。{Type}-wrapper 要素（この場合は .text-wrapper と .password-wrapper）がパネル内の個々のフォームフィールドを表します。
- 各ラッパーには、前の例と同様にラベル、入力フィールド、説明が含まれています。


#### パネル／コンテナコンポーネントの CSS セレクターの例

1. パネルのターゲティング：

```CSS
  /- Target the entire panel container */
  main .form form .panel-wrapper {
    /- Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

- `.panel-wrapper` セレクターは、クラス panel-wrapper を使用してすべての要素のスタイルを設定し、すべてのパネルに一貫した外観を作成します。

1. パネルタイトルのターゲティング：

```CSS
  /- Target the legend element (panel title) */
  .panel-wrapper legend {
    /- Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /- Optional: create a separation line */
  }
```

- `.panel-wrapper legend` セレクターは、パネル内の凡例要素のスタイルを設定し、タイトルを視覚的に目立たせます。


1. パネル内の個々のフィールドのターゲティング：　

```CSS
/- Target all form field wrappers within a panel */
main .form form .panel-wrapper .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

- `.panel-wrapper .{Type}-wrapper` セレクターは、パネル内の `.{Type}-wrapper` クラスを使用してすべてのラッパーをターゲットにし、フォームフィールド間の間隔をスタイル設定できるようにします。

1. 特定のフィールドのターゲティング（オプション）：

```CSS
  /- Target the username field wrapper */
  main .form form .panel-wrapper .text-wrapper.field-username {
    /- Add your styles here (specific to username field) */
  }

  /- Target the password field wrapper */
  main .form form .panel-wrapper .password-wrapper.field-password {
    /- Add your styles here (specific to password field) */
  }
```

- これらのオプションのセレクターを使用すると、パネル内の特定のフィールドラッパーをターゲットにして、ユーザー名フィールドをハイライト表示するなど、独自のスタイルを設定できます。


+++

+++ 繰り返し可能なパネル

#### 繰り返し可能なパネルの HTML 構造

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
</fieldset>
```

**HTML 構造の例**

```HTML
<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-1" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-1" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-1" name="contacts[0].name">
    <div class="field-description" aria-live="polite" id="name-1-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-1" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-1" name="contacts[0].email">
    <div class="field-description" aria-live="polite" id="email-1-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>

<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-2" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-2" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-2" name="contacts[1].name">
    <div class="field-description" aria-live="polite" id="name-2-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-2" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-2" name="contacts[1].email">
    <div class="field-description" aria-live="polite" id="email-2-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>
```

各パネルの構造は単一パネルの例と同じですが、次の追加の属性があります。

- data-repeatable=&quot;true&quot;：この属性は、JavaScript またはフレームワークを使用して、パネルを動的に繰り返すことができることを示します。

- 一意の ID と名前：パネル内の各要素には、パネルのインデックスに基づく一意の ID（例：name-1、email-1）と name 属性（例：name=&quot;contacts[0].name&quot;）があります。これにより、複数のパネルが送信された場合に適切なデータ収集ができるようになります。


#### 繰り返し可能なパネルの CSS セレクター

- すべての繰り返し可能なパネルのターゲティング：

```CSS
  /- Target all panels with the repeatable attribute */
 main .form form .panel-wrapper[data-repeatable="true"] {
    /- Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

セレクターを使用すると、繰り返し可能なすべてのパネルのスタイルが設定され、一貫したルックアンドフィールが保証されます。


- パネル内の個々のフィールドのターゲティング：

```CSS
/- Target all form field wrappers within a repeatable panel */
main .form form .panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

このセレクターを使用すると、繰り返し可能なパネル内のすべてのフィールドラッパーのスタイルが設定され、フィールド間の一貫した間隔が維持されます。

- （パネル内の）特定のフィールドのターゲティング：

```CSS
/- Target the name field wrapper within the first panel */
main .form form .panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /- Add your styles here (specific to first name field) */
}

/- Target all
```


+++


+++ ファイル添付

#### 添付ファイルの HTML 構造

```HTML
<div class="file-wrapper field-{FileName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false"> File Attachment </legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
    <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="{id}" name="{FileName}" autocomplete="off" multiple="" required="required">
  </div>
  <div class="files-list">
    <div data-index="0" class="file-description">
      <span class="file-description-name">ClaimForm.pdf</span>
      <span class="file-description-size">26 kb</span>
      <button class="file-description-remove" type="button"></button>
    </div>
  </div>
</div>
```

**HTML 構造の例**


```HTML
<div class="file-wrapper field-claim_form field-wrapper">
  <legend for="claim_form" class="field-label" data-visible="false">File Attachment</legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
  </div>
  <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="claim_form"
         name="claim_form" autocomplete="off" multiple="" required="required" data-max-file-size="2MB">
  <div class="files-list">
    </div>
</div>
```

- class 属性は、添付ファイル（claim_form）の指定された名前を使用します。
- 入力要素の id 属性と name 属性は、添付ファイル名（claim_form）に一致します。
- files-list セクションは、最初は空です。ファイルのアップロード時に JavaScript を使用して動的に設定されます。


#### 添付ファイルコンポーネントの CSS セレクター

- 添付ファイルコンポーネント全体のターゲティング：

```CSS
/- Target the entire file attachment component */
main .form form .file-wrapper {
  /- Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

このセレクターでは、凡例、ドラッグ領域、入力フィールド、リストを含む添付ファイルコンポーネント全体をスタイル設定します。

- 特定の要素のターゲティング：

```CSS
/- Target the drag and drop area */
main .form form .file-wrapper .file-drag-area {
  /- Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/- Target the file input element */
main .form form .file-wrapper input[type="file"] {
  /- Add your styles here (e.g., hide the default input) */
  display: none;
}

/- Target individual file descriptions within the list (populated dynamically) */
main .form form .file-wrapper .files-list .file-description {
  /- Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/- Target the file name within the description */
main .form form .file-wrapper .files-list .file-description .file-description-name {
  /- Add your styles here (e.g., font-weight) */
  font-weight: bold;
}
```

これらのセレクターでは、添付ファイルコンポーネントの様々な部分を個別にスタイル設定できます。スタイルは、デザインの好みに合わせて調整できます。

+++



## コンポーネントのスタイル設定

フォームフィールドは、特定のタイプ（`{Type}-wrapper`）または個人名（`field-{Name}`）に基づいてスタイル設定できます。これにより、フォームの外観をより詳細に制御およびカスタマイズできます。

+++ フィールドタイプに基づくスタイル設定

CSS セレクターを使用すると、特定のフィールドタイプをターゲットにし、スタイルを一貫して適用できます。

#### HTML 構造

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**HTML 構造の例**

```HTML
<div class="text-wrapper field-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="number-wrapper field-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="email-wrapper field-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

- 各フィールドは、いくつかのクラスを持つ `div` 要素でラップされます。
   - `{Type}-wrapper`：フィールドのタイプを識別します。例：`form-text-wrapper`、`form-number-wrapper`、`form-email-wrapper`。
   - `field-{Name}`：フィールドを名前で識別します。例：`form-name`、`form-age`、`form-email`。
   - `field-wrapper`：すべてのフィールドラッパーの汎用クラス。
- `data-required` 属性は、フィールドが必須かオプションかを示します。
- 各フィールドには、対応するラベル、入力要素、プレースホルダーや説明などの潜在的な追加要素があります。




#### CSS セレクターの例

```CSS
/- Primary Pattern: Target all text input fields */
.form .text-wrapper input {
  /- Add your styles here */
  width: 100%;
  padding: var(--form-input-padding);
}

/- Primary Pattern: Target all number input fields */
.form .number-wrapper input {
  /- Add your styles here */
  letter-spacing: 2px; /- Example for adding letter spacing to all number fields */
  text-align: center;
}
```

+++

+++ フィールド名に基づくスタイル設定

また、個々のフィールドを名前でターゲットにして、一意のスタイルを適用することもできます。

#### HTML 構造

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

**HTML 構造の例**

```HTML
<div class="number-wrapper field-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp" aria-describedby="otp-description">
  <div class="field-description" aria-live="polite" id="otp-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```


#### CSS セレクターの例

```CSS
/- Primary Pattern: Target specific field by name */
.form .field-otp input {
   letter-spacing: 2px;
   text-align: center;
   font-family: monospace;
}

/- Context-specific: Use higher specificity when needed */
main .form .field-otp input {
   /- Use only when you need to override other styles */
   font-weight: bold;
}
```

この CSS は、クラス `field-otp` を持つ要素内にあるすべての入力要素をターゲットとします。Edge Delivery Servicesのフォーム構造は、「アダプティブFormsのブロック規則」に従います。この規則では、名前が「otp」のフィールドの「field-otp」のように、コンテナはフィールド固有のクラスでマークされます。


## CSS ファイルの構造と実装

### **リファレンス実装**

完全なフォームのスタイル設定の参照は、AEM Forms ボイラープレートリポジトリで利用できます。

```
https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/blocks/form/form.css
```

このファイルは、CSS カスタムプロパティシステムの正規実装として機能し、すべてのフォームのスタイル設定の基盤となります。 これには、すべての CSS 変数、コンポーネントのスタイルパターン、レスポンシブデザイン実装に関する包括的な定義が含まれます。

+++

+++ プロジェクトの統合

Edge Delivery Services プロジェクトで、次の構造化アプローチを使用してフォームのスタイル設定を実装します。

```
/blocks/form/form.css          // Core form block styles (copied from boilerplate)
/styles/styles.css             // Global site styles and CSS variable overrides
/styles/lazy-styles.css        // Additional component enhancements
```

+++

+++ 実装方法

**CSS カスタムプロパティオーバーライド**：グローバルスタイルのフォーム変数を上書きして、ブランド固有のテーマ設定を実装します。

```css
/* In /styles/styles.css */
:root {
    /* Brand-specific overrides */
    --button-primary-color: #your-brand-color;
    --form-background-color: #your-background;
    --label-color: #your-text-color;
}
```

**コンポーネント固有のカスタマイズ**:
CSS 変数システムを維持しながら、コンポーネント固有のスタイル設定を追加します。

```css
/* Enhanced component styling */
.form .text-wrapper input {
    border-radius: var(--form-card-border-radius);
    transition: all 0.2s ease;
}

.form .text-wrapper input:focus {
    transform: translateY(-1px);
    box-shadow: 0 0 0 3px rgba(var(--button-primary-color), 0.1);
}
```

**レスポンシブデザインの統合**：メディアクエリ内で CSS カスタムプロパティを利用して、一貫したレスポンシブ動作を実現します。

```css
@media (max-width: 768px) {
    :root {
        --form-input-padding: 0.875rem;
        --form-field-vert-gap: 1rem;
        --form-padding: 1rem;
    }
}
```

+++

### スタイル設定の完全な実装の例

この節では、CSS カスタムプロパティを使用して、最新のブランドフォームを作成する方法を説明します。 実装は、理解とナビゲーションを容易にするために明確なサブセクションに分類されています。



+++ &#x200B;1. ブランドテーマの変数

CSS カスタムプロパティを使用して、ブランドのカラーパレット、間隔およびタイポグラフィを定義します。

```css
/* Custom brand theme */
:root {
  /* Brand color system */
  --brand-primary: #2563eb;
  --brand-secondary: #64748b;
  --brand-success: #059669;
  --brand-error: #dc2626;
  --brand-background: #f8fafc;
  
  /* Override form variables */
  --background-color-primary: #ffffff;
  --button-primary-color: var(--brand-primary);
  --button-primary-hover-color: #1d4ed8;
  --form-error-color: var(--brand-error);
  --form-background-color: var(--brand-background);
  --label-color: var(--brand-secondary);
  --border-color: #d1d5db;
  
  /* Enhanced spacing */
  --form-input-padding: 1rem;
  --form-field-vert-gap: 1.5rem;
  --form-padding: 2rem;
  
  /* Modern typography */
  --form-font-size-s: 16px;
  --form-label-font-weight: 500;
}
```


+++

+++ &#x200B;2. フォームコンテナのスタイル設定

現代的な背景、境界線の半径、影をフォームコンテナに適用して、視覚的に訴えかけるようにします。


```css
/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}
```




+++

+++ 3.入力フィールドのスタイル

テキスト、メール、数値入力フィールドのスタイルを設定して、クリーンで現代的な外観を実現します。


```css
/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}
```


+++

+++ 4.追加カスタマイズ

必要に応じて特定のフィールド、状態またはコンポーネントをターゲット設定することで、フォームのスタイル設定をさらに拡張できます。 詳細パターンについては、前の節を参照してください。

```css
/* Custom brand theme */
:root {
    /* Brand color system */
    --brand-primary: #2563eb;
    --brand-secondary: #64748b;
    --brand-success: #059669;
    --brand-error: #dc2626;
    --brand-background: #f8fafc;
    
    /* Override form variables */
    --background-color-primary: #ffffff;
    --button-primary-color: var(--brand-primary);
    --button-primary-hover-color: #1d4ed8;
    --form-error-color: var(--brand-error);
    --form-background-color: var(--brand-background);
    --label-color: var(--brand-secondary);
    --border-color: #d1d5db;
    
    /* Enhanced spacing */
    --form-input-padding: 1rem;
    --form-field-vert-gap: 1.5rem;
    --form-padding: 2rem;
    
    /* Modern typography */
    --form-font-size-s: 16px;
    --form-label-font-weight: 500;
}

/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}

/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}

.form .text-wrapper input:focus,
.form .email-wrapper input:focus,
.form .number-wrapper input:focus {
    border-color: var(--brand-primary);
    box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
    transform: translateY(-1px);
}

/* Enhanced button styling */
.form .button-wrapper button[type="submit"] {
    background: linear-gradient(135deg, var(--brand-primary) 0%, #1d4ed8 100%);
    color: white;
    border: none;
    border-radius: 8px;
    padding: 1rem 2rem;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s ease;
    width: 100%;
    box-shadow: 0 4px 12px rgba(37, 99, 235, 0.3);
}

.form .button-wrapper button[type="submit"]:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(37, 99, 235, 0.4);
}
```

この包括的なアプローチにより、CSS カスタムプロパティを使用して、アダプティブ Forms ブロックシステムの構造の整合性とアクセシビリティ機能を維持しながら、高度なテーマ設定を可能にする方法が示されます。

+++

## CSS の問題のトラブルシューティング

+++ CSS 特異性の問題

```css
/- ❌ Problem: Styles not applying */
.text-wrapper input {
  color: red;
}

/- ✅ Solution: Match or exceed existing specificity */
.form .text-wrapper input {
  color: red;
}

/- ✅ Alternative: Use higher specificity when needed */
main .form .text-wrapper input {
  color: red;
}
```

+++

+++ CSS 変数の上書きの問題

```css
/- ❌ Problem: Variables not working */
.form {
  --form-border-color: blue; /- Local scope only */
}

/- ✅ Solution: Define in root scope */
:root {
  --form-border-color: blue; /- Global scope */
}
```

+++

+++ フォームステートのスタイル設定

```css
/- Validation states */
.form .field-wrapper.error input {
  border-color: var(--form-error-color);
}

.form .field-wrapper.success input {
  border-color: var(--form-success-color);
}

/- Loading state */
.form[data-submitting="true"] {
  opacity: 0.7;
  pointer-events: none;
}

/- Disabled state */
.form input:disabled {
  background-color: var(--form-input-disabled-background);
  cursor: not-allowed;
}
```

+++

+++ 一般的なセレクターのエラー

```css
/- ❌ Incorrect: Assumes direct nesting */
.form form input {
  /- This might miss inputs in wrappers */
}

/- ✅ Correct: Target actual structure */
.form .text-wrapper input {
  /- Targets actual HTML structure */
}

/- ❌ Avoid: Unnecessary specificity */
main .form form .text-wrapper input {
  /- Too specific, harder to override */
}

/- ✅ Preferred: Balanced specificity */
.form .text-wrapper input {
  /- Easier to maintain and override */
}
```

+++



### **コンポーネント固有のベストプラクティス**


+++ ボタンのスタイル

```css
/- Primary buttons */
.form .button-wrapper button[type="submit"] {
  background-color: var(--form-focus-color);
  color: white;
  border: none;
  padding: var(--form-input-padding);
  border-radius: var(--form-border-radius);
}

/- Secondary buttons */
.form .button-wrapper button[type="reset"] {
  background-color: transparent;
  color: var(--form-text-color);
  border: 1px solid var(--form-border-color);
}
```

+++

+++ レスポンシブフォームデザイン

```css
/- Mobile-first approach */
.form {
  width: 100%;
  padding: 1rem;
}

/- Tablet and up */
@media (min-width: 768px) {
  .form {
    max-width: var(--form-max-width);
    padding: var(--form-padding);
  }
}
```

+++

## ベストプラクティスのまとめ

1. **CSS カスタムプロパティの使用**：一貫したテーマ設定のために変数を活用する
2. **ブロックベースのアーキテクチャに従う**:`.form` をプライマリブロックセレクターとして使用します
3. **特定性の過剰を避ける**：必要でない限り、`main .form form` を使用しない
4. **ターゲットラッパー**：コンポーネントのターゲティングに `.{Type}-wrapper` パターンを使用します
5. **一貫性の維持**：プロジェクト全体で同じセレクターパターンを使用します
6. **デバイス間でのテスト**：モバイル、タブレット、デスクトップでフォームが適切に機能することを確認します
7. **アクセシビリティを検証**：スタイルがスクリーンリーダーやキーボードナビゲーションに干渉しないようにします


