---
title: コンテンツフラグメント
description: Adobe Experience Manager as a Cloud Service のコンテンツフラグメントを使用すると、ページのオーサリング時にも使用できる、チャネルに依存しないコンテンツの設計、作成、キュレーション、使用が可能になります。
exl-id: 7a44fc4e-3793-4aa3-8c21-db0567c93244
solution: Experience Manager Sites
feature: Authoring, Content Fragments
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '1267'
ht-degree: 100%

---

# コンテンツフラグメント {#content-fragments}

Adobe Experience Manager（AEM）as a Cloud Service のコンテンツフラグメントは、[ページに依存しないアセットとして作成および管理](/help/sites-cloud/administering/content-fragments/overview.md)されるので、チャネルに特化しないコンテンツを（場合によってはチャネル固有の）バリエーションと共に作成できます。コンテンツページをオーサリングする際に、これらのフラグメントとそれらのバリエーションを使用できます。

>[!CAUTION]
>
>このページは、基本的な用語および概念をフラグメントの作成および管理や、AEM ページ以外のチャネルへの構造化コンテンツフラグメントの配信に関する情報と共に紹介している[コンテンツフラグメントの使用方法](/help/sites-cloud/administering/content-fragments/overview.md)（および関連ページ）と併せて読む必要があります。

>[!NOTE]
>
>コンテンツフラグメントは **Sites** 機能ですが、**Assets** として保存されます。
>
>引き続き **[Assets](/help/assets/content-fragments/content-fragments-managing.md)** コンソールから管理できますが、現在は主に&#x200B;**[コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)**&#x200B;コンソールで管理されています。
>
>コンテンツフラグメントをオーサリングするエディターは 2 つあります。
>
>* [コンテンツフラグメント - オーサリング](/help/sites-cloud/administering/content-fragments/authoring.md)の新しいエディターには、主に&#x200B;**コンテンツフラグメント**&#x200B;コンソールからアクセスします。
>* [オリジナルエディター](/help/assets/content-fragments/content-fragments-variations.md)には、主に **Assets** コンソールからアクセスします。

>[!NOTE]
>
>**コンテンツフラグメント**&#x200B;と&#x200B;**[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fragments/content-fragments.md)**&#x200B;は、AEM 内の異なる機能です。
>* **コンテンツフラグメント**&#x200B;は、定義と構造を備えたエディトリアルコンテンツですが、視覚的なデザインやレイアウトは追加されていません。コンテンツフラグメントを使用すれば、テキスト、数値、日付などの構造化データにアクセスできます。
>* **エクスペリエンスフラグメント**&#x200B;は完全にレイアウトされたコンテンツであり、web ページのフラグメントです。
>
>エクスペリエンスフラグメントには、コンテンツフラグメントの形式でコンテンツを含めることができますが、その逆はできません。
>
>詳しくは、[AEM のコンテンツフラグメントとエクスペリエンスフラグメントについて](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=ja#content-fragments)を参照してください。

コンテンツフラグメントは、次のことを可能にします。

* **マーケティングとキャンペーン戦略**
   * 一元的に管理されるコンテンツフラグメントを使用してコンテンツをレビューします。
* **クリエイティブプロフェッショナル**
   * コンテンツフラグメントに関連付けられたコレクションを介したクリエイティブアセットのトラッキング。
* **コピーライター**
   * AEM コンテンツフラグメントエディターに書き込みます。
   * コンテンツのバリエーションを作成できます。
   * 関連するコンテンツをコンテンツフラグメントに関連付けることができます。
   * バージョン管理／ワークフローを使用できます。
   * コンテンツフラグメントを共有できます。
   * 翻訳を一元的に管理できます。
* **プロデューサーおよびジャーニー管理者**
   * AEM でのオーサリングで事前定義済みのフラグメントとバリエーションから選択します。
   * コピーライターおよびクリエイターが一元管理されたフラグメントとアセットで更新することで、フラグメントと関連コンテンツを常に最新の状態に保つことができます。
   * 適切にキュレーションされた関連メディアコンテンツと連携できます。
   * その場でアドホックコンテンツのバリエーションを作成しながら、それらのバリエーションをフラグメントで一元的に管理できます。

## ページへのコンテンツフラグメントの追加 {#adding-a-content-fragment-to-your-page}

1. 編集するページを開きます。
2. **コンテンツフラグメント**&#x200B;コンポーネントを、**コンポーネント**&#x200B;ブラウザーまたは「**新規コンポーネントを挿入**」のいずれかから開きます。
3. 次のいずれかを実行できます。
   * **Assets** ブラウザーを開いて、**コンテンツフラグメント**&#x200B;をフィルタリングします（デフォルトは画像）。次に、必要なフラグメントをコンポーネントインスタンスにドラッグします。
   * コンテンツフラグメントコンポーネントを選択し、ツールバーから「**設定**」を選択します。ダイアログで、選択ダイアログを開き、必要な&#x200B;**コンテンツフラグメント**&#x200B;を参照して選択できます。

   >[!NOTE]
   >
   >特定のコンテンツフラグメントをページに直接ドラッグすることもできます。これにより、関連コンポーネントが自動的に作成されます（コンテンツフラグメント）。

4. 最初に、**メイン**&#x200B;要素および&#x200B;**マスター**（バリエーション）からのコンテンツが表示されます。必要に応じて、[他の要素やバリエーションを選択](#selecting-the-element-or-variation)できます。

   ![Assets ブラウザーのコンテンツフラグメント](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >その他の編集機能について詳しくは、次を参照してください。
   >
   >* [レスポンシブレイアウト](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
   >* [ページのコンテンツの編集](/help/sites-cloud/authoring/page-editor/edit-content.md)

### 要素またはバリエーションの選択 {#selecting-the-element-or-variation}

フラグメントの&#x200B;**設定**&#x200B;ダイアログを開き、フラグメントを現在のページで使用するように設定します。ダイアログは、使用するコンポーネントに応じて異なります。

>[!NOTE]
>
>[コンテンツフラグメントコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=ja)も参照してください。

適切な設定ダイアログで、次のような使用可能なパラメーターを選択できます。

* **コンテンツフラグメント**
   * 使用するフラグメントを指定します。
* **ディスプレイモード**：
   * **単一のテキスト要素**
   * **複数の要素**
* **要素**
   * 使用するモデルに応じて選択できます。

  >[!NOTE]
  >
  >使用できる要素は、使用するモデルによって異なります。

* **バリエーション**
   * デフォルトの「**プライマリ**」は常に利用できます。
   * フラグメントのバリエーションが作成された場合は、選択を使用できます。

* **ID**

   * **コンポーネントに適用する HTML ID 属性。**

### フラグメントエディターへのクイック接続 {#quick-connection-to-fragment-editor}

コンポーネントツールバーの&#x200B;**編集**&#x200B;アイコンを使用して、フラグメントのソースを開いて（アセットを）編集できます。この機能により、[コンテンツフラグメントを編集および管理できます](/help/sites-cloud/administering/content-fragments/overview.md)。

>[!CAUTION]
>
>これまでと同様に、フラグメントソースを編集すると、そのコンテンツフラグメントを参照するすべてのページに影響します。

### 中間コンテンツの追加 {#adding-in-between-content}

特定のコンテンツフラグメントがページに追加されると、フラグメントの各 HTML 段落の間（および上と下）に「**コンポーネントをここにドラッグ**」プレースホルダーが存在します。

これにより、ルートフラグメントを変更することなく、[フラグメントコンテンツの中間](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments)に（利用可能な任意の位置に）にさらにコンテンツ（つまり、中間コンテンツ）を追加できます。

中間コンテンツの場合は、次のことができます。

* [コンポーネントブラウザー](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)からコンポーネントを追加する。
* [Assets ブラウザー](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser)からアセットを追加する。
* [関連コンテンツ](#using-associated-content)を中間コンテンツのソースとして使用する。

>[!CAUTION]
>
>中間コンテンツは、ページコンテンツです。コンテンツフラグメントには保存されません。

![コンポーネントの挿入](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>フラグメント自体に[ビジュアルアセット（画像）を挿入](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)することもできます。
>
>フラグメント自体に挿入されたビジュアルアセットは、フラグメントの前の段落に配置されます。つまり、ビジュアルアセットと前の段落の間に中間コンテンツを配置することはできません。このレベルの接続が必要な場合は、画像をフラグメントに（[混在メディアフラグメント](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)として）追加できます。

>[!CAUTION]
>
>ページのコンテンツフラグメントに中間コンテンツを追加した後に、基になるコンテンツフラグメントの構造をコンテンツフラグメントエディターなどで変更すると、エラーや予期しない結果を引き起こすおそれがあります。
>
>これが発生した場合、中間コンテンツはそのまま維持されます。
>
>* 中間コンポーネントは、フラグメントフロー内のコンポーネントのシーケンス内で絶対的な位置を持ちます。フラグメント内の段落のコンテンツが変更されても、この位置は変更されません。
>
>  中間段落は隣に位置する（フラグメント）段落とコンテキスト関係を持たないので、これにより、相対位置が変更したかのように見せることができます。
>* 2 つの段落構造が競合する場合を除きます。競合する場合、中間コンテンツは（内部的には存在していますが）表示されません。

### 関連コンテンツの使用 {#using-associated-content}

[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)に[コンテンツを関連付けた](/help/assets/content-fragments/content-fragments-assoc-content.md)場合、これらのアセットは（フラグメントをコンテンツページに配置した後に）サイドパネルから使用できます。関連付けられたコンテンツは、事実上、[中間コンテンツ](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments)用のコンテンツの特別なソースになります。

>[!NOTE]
>
>[ビジュアルアセット（画像など）](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)をフラグメントやページに追加するには、様々な方法があります。

>[!NOTE]
>
>1 つのページに複数のコンテンツフラグメントがある場合、「**関連コンテンツ**」タブに、すべてのフラグメントに適したアセットが表示されます。

関連コンテンツを含むフラグメントをページに追加すると、サイドパネルで新しいタブ（**関連コンテンツ**）が開きます。

ここから、アセットを必要な場所（既存のコンポーネント、または適切なコンポーネントが作成される必要な位置）にドラッグできます。

![画像の挿入](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### フラグメントに挿入されたアセット {#assets-inserted-into-the-fragment}

アセット（画像など）がフラグメント自体に（[混在メディアフラグメント](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)として）挿入されている場合、ページエディターでこれらのアセットを編集するためのオプションは制限されます。

例えば、画像の場合、次のことができます。

* 画像の切り抜き、回転、反転。
* タイトルまたは代替テキストを追加します。
* サイズを指定します。
* レイアウトを設定することもできます。

移動、コピー、削除などの他の変更は、フラグメントエディターで行う必要があります。

### 公開 {#publishing}

フラグメントを公開済みの web ページで使用できるようにするには、フラグメントを公開する必要があります。

* フラグメントは、[フラグメントをコンテンツフラグメントコンソールで作成](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment)した後に公開できます。
* 公開されるページに&#x200B;*非公開のフラグメント*&#x200B;があると、そのタイミングでフラグメントも公開できます。

## コンテンツフラグメントの書き出し {#exporting-content-fragments}

Adobe Target に書き出す場合は、JSON を使用してフラグメントを配信できます。以下を参照してください。

* [Adobe Target との統合](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Adobe Target へのコンテンツフラグメントの書き出し](/help/sites-cloud/integrating/content-fragments-target.md)
