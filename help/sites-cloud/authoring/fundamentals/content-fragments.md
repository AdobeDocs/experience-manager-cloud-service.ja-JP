---
title: コンテンツフラグメント
description: Adobe Experience Manager as a Cloud Service のコンテンツフラグメントを使用すると、ページに依存しないコンテンツの設計、作成、キュレーション、使用が可能になります。
exl-id: 7a44fc4e-3793-4aa3-8c21-db0567c93244
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: ht
source-wordcount: '1166'
ht-degree: 100%

---

# コンテンツフラグメント {#content-fragments}

Adobe Experience Manager（AEM）as a Cloud Service のコンテンツフラグメントは、[ページに依存しないアセットとして作成および管理されます](/help/sites-cloud/administering/content-fragments/content-fragments.md)。

これによりチャネルに依存しないコンテンツを、様々なバリエーション（チャネル固有）で作成できます。その後、コンテンツページをオーサリングする際に、これらのフラグメントとそれらのバリエーションを使用できます。

更新された JSON エクスポーターと共に構造化コンテンツフラグメントを使用して、AEM コンテンツをコンテンツサービス経由で AEM ページ以外のチャネルに配信することもできます。

>[!NOTE]
>
>**コンテンツフラグメント**&#x200B;と&#x200B;**[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)**&#x200B;は、AEM 内の異なる機能です。
>
>* **コンテンツフラグメント**&#x200B;は、主にテキストや関連画像などの編集コンテンツです。これは、デザインやレイアウトを含まない純粋なコンテンツです。
>* **エクスペリエンスフラグメント**&#x200B;は完全にレイアウトされたコンテンツなので、web ページのフラグメントになります。
>
>エクスペリエンスフラグメントには、コンテンツフラグメントの形式でコンテンツを含めることができますが、その逆はできません。

>[!CAUTION]
>
>このページは、基本的な用語および概念をフラグメントの作成および管理と共に紹介している[コンテンツフラグメントの使用方法](/help/sites-cloud/administering/content-fragments/content-fragments.md)（および関連ページ）と併せて読む必要があります。

コンテンツフラグメントでは、次のアクションを実行できます。

* **マーケティングおよびキャンペーン戦略**
   * 集中管理されたコンテンツフラグメントでコンテンツをレビューします。
* **クリエイティブプロフェッショナル**
   * コンテンツフラグメントに関連付けられたコレクションを介してクリエイティブアセットを追跡します。
* **コピーライター**
   * AEM コンテンツフラグメントエディターで書き込みます。
   * コンテンツのバリエーションを作成できます。
   * 関連性の高いコンテンツをコンテンツフラグメントと関連付けることができます。
   * バージョン管理やワークフローを使用できます。
   * コンテンツフラグメントを共有できます。
   * 翻訳を集中管理できます。
* **プロデューサーおよびジャーニー管理者**
   * AEM のオーサリングで事前定義されたフラグメントとバリエーションから選択します。
   * コピーライターやクリエイティブが集中管理されたフラグメントやアセットを更新できるので、フラグメントと連携し関連付けられたコンテンツが常に最新の状態に維持されます。
   * 適切にキュレーションされた関連メディアコンテンツと連携できます。
   * アドホックコンテンツのバリエーションをフラグメント内で集中管理したまま、それらのバリエーションをその場で作成できます。

## ページへのコンテンツフラグメントの追加 {#adding-a-content-fragment-to-your-page}

1. 編集するページを開きます。
2. **コンテンツフラグメント**&#x200B;コンポーネントを、**コンポーネント**&#x200B;ブラウザーまたは「**新規コンポーネントを挿入**」のいずれかから開きます。
3. 次のいずれかを実行できます。
   * **Assets** ブラウザーを開いて、**コンテンツフラグメント**&#x200B;をフィルタリングします（デフォルトは画像）。次に、必要なフラグメントをコンポーネントインスタンスにドラッグします。
   * コンテンツフラグメントコンポーネントを選択して、ツールバーの「**設定**」を選択します。ダイアログで、選択ダイアログを開き、必要な&#x200B;**コンテンツフラグメント**&#x200B;を参照して選択できます。

   >[!NOTE]
   >
   >特定のコンテンツフラグメントをページに直接ドラッグすることもできます。これにより、関連コンポーネントが自動的に作成されます（コンテンツフラグメント）。

4. 最初に、**メイン**&#x200B;要素および&#x200B;**マスター**（バリエーション）からのコンテンツが表示されます。必要に応じて、[他のエレメントやバリエーションを選択](#selecting-the-element-or-variation)できます。

   ![Assets ブラウザーのコンテンツフラグメント](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >その他の編集機能について詳しくは、次を参照してください。
   >
   >* [レスポンシブレイアウト](/help/sites-cloud/authoring/features/responsive-layout.md)
   >* [ページのコンテンツの編集](/help/sites-cloud/authoring/fundamentals/editing-content.md)


### 要素またはバリエーションの選択 {#selecting-the-element-or-variation}

フラグメントの&#x200B;**設定**&#x200B;ダイアログを開き、フラグメントを現在のページで使用するように設定します。ダイアログは、使用されるコンポーネントによって異なる場合があります。

>[!NOTE]
>
>[コンテンツフラグメントコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=ja)も参照してください。

適切な設定ダイアログで、以下をはじめとする使用可能なパラメーターを選択できます。

* **コンテンツフラグメント**
   * 使用するフラグメントを指定します。
* **ディスプレイモード**：
   * **単一のテキスト要素**
   * **複数の要素**
* **エレメント**
   * 使用するモデルに応じて選択を使用できます。

   >[!NOTE]
   >
   >使用できるエレメントは、使用するモデルによって異なります。

* **バリエーション**
   * デフォルトの「**マスター**」は常に利用できます。
   * フラグメントにバリエーションが作成されている場合に選択できます。

* **ID**

   * **コンポーネントに適用する HTML ID 属性。**

### フラグメントエディターへのクイック接続 {#quick-connection-to-fragment-editor}

コンポーネントツールバーの&#x200B;**編集**&#x200B;アイコンを使用して、フラグメントのソースを開いて（アセットを）編集できます。この機能により、[コンテンツフラグメントを編集および管理できます](/help/sites-cloud/administering/content-fragments/content-fragments.md)。

>[!CAUTION]
>
>フラグメントソースの編集は、そのコンテンツフラグメントを参照するすべてのページに影響します。

### 中間コンテンツの追加 {#adding-in-between-content}

特定のコンテンツフラグメントをページに追加すると、フラグメントの各 HTML 段落間（および上部／下部）に&#x200B;**コンポーネントをここにドラッグ**&#x200B;プレースホルダーが表示されます。

これにより、ルートフラグメントを変更することなく、フラグメントコンテンツの[中間（中間コンテンツ）](/help/sites-cloud/administering/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments)（の利用可能な任意のポイント）にコンテンツを追加できます。

中間コンテンツでは、次のことができます。

* [コンポーネントブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)からコンポーネントを追加する。
* [Assets ブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)からアセットを追加する。
* [関連コンテンツ](#using-associated-content)を中間コンテンツのソースとして使用する。

>[!CAUTION]
>
>中間コンテンツは、ページコンテンツです。中間コンテンツはコンテンツフラグメントに保存されません。

![コンポーネントの挿入](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>フラグメント自体に[ビジュアルアセット（画像）を挿入](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)することもできます。
>
>フラグメント自体に挿入されたビジュアルアセットは、フラグメントの前の段落に配置されます。つまり、ビジュアルアセットと前の段落の間に中間コンテンツを配置することはできません。このレベルの接続が必要な場合は、画像をフラグメントに（[混在メディアフラグメント](/help/sites-cloud/administering/content-fragments/content-fragments.md#fragments-with-visual-assets)として）追加できます。

>[!CAUTION]
>
>ページのコンテンツフラグメントに中間コンテンツを追加した後に、基になるコンテンツフラグメントの構造をコンテンツフラグメントエディターなどで変更すると、エラーや予期しない結果を引き起こすおそれがあります。
>
>これが発生した場合、中間コンテンツはそのまま維持されます。
>
>* 中間コンポーネントは、フラグメントフローのコンポーネントのシーケンス内に絶対位置を持ちます。この位置は、フラグメント内の段落のコンテンツが変更されても変更されません。
>
>  中間段落は隣に位置する（フラグメント）段落とコンテキスト関係を持たないので、これにより、相対位置が変更したかのように見せることができます。
>* 2 つの段落構造が競合する場合を除きます。競合する場合、中間コンテンツは（内部的には存在していますが）表示されません。


### 関連コンテンツの使用 {#using-associated-content}

[コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/content-fragments.md)に[コンテンツを関連付けた](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md)場合、これらのアセットは（フラグメントをコンテンツページに配置した後に）サイドパネルから使用できます。関連付けられたコンテンツは、事実上、[中間コンテンツ](/help/sites-cloud/administering/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments)用のコンテンツの特別なソースになります。

>[!NOTE]
>
>[ビジュアルアセット（画像など）](/help/sites-cloud/administering/content-fragments/content-fragments.md#fragments-with-visual-assets)をフラグメントやページに追加するには、様々な方法があります。

>[!NOTE]
>
>1 つのページに複数のコンテンツフラグメントがある場合、「**関連コンテンツ**」タブにすべてのフラグメントに適切なアセットが表示されます。

コンテンツが関連付けられたフラグメントをページに追加すると、新しいタブ（「**関連コンテンツ**」）がサイドパネルに開きます。

ここから、アセットを必要な場所（既存の位置または適切なコンポーネントが作成される必要がある位置）にドラッグできます。

![画像の挿入](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### フラグメントに挿入されたアセット {#assets-inserted-into-the-fragment}

アセット（画像など）がフラグメント自体に（[混在メディアフラグメント](/help/sites-cloud/administering/content-fragments/content-fragments.md#fragments-with-visual-assets)として）挿入されている場合、ページエディターでこれらのアセットを編集するためのオプションは制限されます。

例えば、画像の場合、次のことができます。

* 画像の切り抜き、回転または反転
* タイトルまたは代替テキストの追加
* サイズの指定
* レイアウトの設定

移動、コピー、削除などの他の変更は、フラグメントエディターで行う必要があります。

### 公開 {#publishing}

フラグメントを公開済みの web ページで使用できるようにするには、フラグメントを公開する必要があります。

* フラグメントは、[フラグメントをコンテンツフラグメントコンソールで作成](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#publishing-and-referencing-a-fragment)した後に公開できます。
* 公開されるページに&#x200B;*非公開のフラグメント*&#x200B;があると、そのタイミングでフラグメントも公開できます。
