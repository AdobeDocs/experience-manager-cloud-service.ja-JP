---
title: リファレンステーマ
seo-title: Reference Themes
description: AEM Forms には、ソフトウェア配布から取得してフォームのスタイル設定に使用できるアダプティブフォームテーマが用意されています。
seo-description: AEM Forms provides adaptive forms themes that you can get from Software Distribution and use to style a form.
discoiquuid: a1229970-5a5a-4f76-a880-278f972587cc
source-git-commit: 3ca1996ac3a19151c0c05bd972f0aec07edabf69
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 56%

---


# Formsas a Cloud Serviceの参照アセット {#reference-themes}

参照テーマ、テンプレート、およびフォームデータモデルは、 [参照アセットパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.0.0.zip). これにより、アダプティブFormsの開発をすばやく開始し、迅速に進めることができます。 以下を使用できます。 [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager.html?lang=ja) このパッケージをAEM Formsas a Cloud Service環境にデプロイする場合。

パッケージに含まれる参照アセットは次のとおりです。

## テーマ {#themes}

[テーマ](/help/forms/themes.md)を使用すると、CSS に関する深い知識がなくてもフォームのスタイルを設定できます。次のテーマが含まれます。

* Beryl
* Tranquil
* Ultramarine
* Urbane
* Canva

各テーマには、独自のエレガントなスタイルが含まれていて、ユーザー向けの使いやすいアダプティブフォームの作成に使用できます。パネル、テキストボックス、数値ボックス、ラジオボタン、表、スイッチなど、セレクター用の独自のスタイル設定が含まれています。これらのテーマ内のスタイルは、要件に基づいています。たとえば、特定のシナリオでは、クリーンなフォントを含む最小限のテーマが必要です。Urbane テーマを使用すると、その外観を実現できます。

![リファレンステーマ](/help/forms/assets/ref-themes.png)

このパッケージに含まれるテーマはレスポンシブで、これらのテーマ内のスタイルはモバイルディスプレイとデスクトップディスプレイに対して定義されます。 様々なデバイス上のほとんどの最新のブラウザーは、これらのテーマのいずれかが適用されたフォームを問題なくレンダリングできます。

パッケージのインストールについて詳しくは、[パッケージの作業方法](/help/implementing/developing/tools/package-manager.md)を参照してください。

### ベリル {#beryl}

Beryl テーマは、We.Gov アダプティブフォームで使用され、背景画像、透明度および大きくてフラットなアイコンの使用を強調します。以下のスクリーンショットで、Beryl テーマの外観と、フォームのスタイル設定がどのように拡張されるかを確認できます。

![Beryl テーマ](/help/forms/assets/beryl.png)

<!--[Click to enlarge

](assets/beryl-1.png)-->

<!-- ## Exec {#exec}

Exec theme avoids solid background fills to emphasize form components. Selecting and clicking components changes font colors. In comparison to the default Canvas theme, font color of the text in the selected tab changes to dark blue. Notice how the navigation and submit buttons are different from the Beryl theme.

![Exec theme](/help/forms/assets/exec.png) -->

<!--[Click to enlarge

](assets/exec-1.png)-->

<!-- ## Exec Light {#exec-light}

Exec Light theme uses white space to create a seamless experience. The Next and Submit buttons get a solid fill and 3D shadow. Selected tabs on the left get an arrow instead of double-check marks.

![Exec light theme](/help/forms/assets/exec-light.png) -->

<!--[Click to enlarge

](assets/exec-light-1.png)-->

<!-- ## Liberty {#liberty}

Liberty theme uses a minimalist approach to highlight the important. For example, the font color of the visited tab changes to green. You can only see the bottom-outline of the text box which emulates the look of a paper-based form with lines. The active text box has a black bottom-outline while others get light gray bottom-outline.

![Liberty theme](/help/forms/assets/liberty.png) -->
<!--[Click to enlarge](assets/liberty-1.png)-->

### Tranquil {#tranquil}

Tranquil テーマは、Tranquil カラースキームの明るいシェーディングと暗いシェーディングを提供して、フォームの様々なコンポーネントを強調します。たとえば、ラジオボタン、パネルおよびタブは、様々なシェーディングの緑色になります。

![Tranquil テーマ](/help/forms/assets/tranquil.png)

<!--[Click to enlarge](assets/tranquil-1.png)-->

### Ultramarine {#ultramarine}

Ultramarine テーマは、濃い青色のシェーディングを使用して、タブ、パネル、テキストボックス、ボタンなどのコンポーネントを強調します。

![Ultramarine テーマ](/help/forms/assets/ultramarine.png)
<!--[Click to enlarge](assets/ultramarine-1.png)-->

### Urbane {#urbane}

Urbane テーマは、フォームの最小限の機能的外観を強調します。Urbane テーマをフォームに適用すると、コンポーネントはフラットになります。パネルには細いアウトラインが付けられ、モダンな外観を作成します。

![Urbane テーマ](/help/forms/assets/urbane.png)
<!--[Click to enlarge](assets/urbane-1.png)-->

<!-- ## U.S. Web Design Standards {#u-s-web-design-standards}

U.S. Web Design Standards theme, as the name suggests, uses typefaces and styles described in the Draft U.S. Web Design Standards site. The web standard is used by federal organizations to create consistent web experiences across federal government websites.

![U.S. Web Design Standards Theme](/help/forms/assets/us-web-standards.png) -->
<!--[Click to enlarge](assets/usgov.png)-->


## テンプレート

テンプレートを使用すると、コンポーネントをドラッグ&amp;ドロップして、アダプティブフォームの初期構造を定義できます。 次のアセットが含まれます。

### 基本 {#basic}

基本テンプレートを使用すると、登録フォームをすばやく作成できます。

![基本テーマ](/help/forms/assets/exec.png)

### 空白 {#blank}

基本テンプレートには空のキャンバスが用意されており、組織に合わせてアダプティブフォームの初期構造を作成することができます。

## フォームデータモデル

### Microsoft® Dynamics 365

Microsoft Dynamics 365 データモデルは、Microsoft Dynamics 365 をデータソースとして使用する場合に役立ちます。 また、データを読み取り、更新、削除し、Microsoft Dynamics 365 データソースに追加するサンプルサービスも提供しています。

![Microsoft® Dynamics 365 フォームデータモデル](/help/forms/assets/microsoft-dynamic-fdm.png)

### Salesforce

Salesforce データモデルは、Salesforce をデータソースとして使用する際に役立ちます。 また、Salesforce に対して、データの読み取り、更新、削除、追加を行うサンプルサービスも提供します。

![Salesforce フォームデータモデル](/help/forms/assets/salesforce-fdm.png)
