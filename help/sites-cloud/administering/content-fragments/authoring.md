---
title: コンテンツフラグメントのオーサリング
description: コンテンツフラグメントのコンテンツを作成する方法を理解し、目的に応じてそのコンテンツのバリエーションを作成します。 これにより、ヘッドレス配信とページオーサリングの両方の柔軟性が向上します。
feature: Content Fragments
role: User, Developer, Architect
exl-id: a2f2b617-3bdf-4a22-ab64-95f2c65adc82
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '2251'
ht-degree: 4%

---

# コンテンツフラグメントのオーサリング {#authoring-content-fragments}

コンテンツフラグメントのオーサリングは、ヘッドレス配信とページオーサリングの両方に焦点を当てています。

コンテンツフラグメントには 2 つのエディターを使用できます。 この節で説明するエディター：

* は、ヘッドレスコンテンツ配信用に開発されています（ただし、すべてのシナリオで使用できます）。
* は、 **コンテンツフラグメント** コンソール

このエディターでは、次の情報が表示されます。

* [自動保存](#saving-autosaving)：誤って編集内容が失われるのを防ぎます。
* [コンテンツ参照としてのアセットのインラインアップロード](#reference-images)を使用する必要がありますが、最初に Asset DAM にアップロードする必要はありません。
* [プレビュー](#preview-content-fragment) コンテンツフラグメントによって配信されるレンダリングされたエクスペリエンスの
* 次の機能を持つ [公開](#publish-content-fragment) および [非公開](#unpublish-content-fragment) をクリックします。
* 次の機能を持つ [関連付けられた言語コピーを表示して開く](#view-language-copies) 」と入力します。
* 次の機能を持つ [バージョンの詳細を表示](#view-version-history) 」と入力します。 選択したバージョンに戻すこともできます。
* 次の機能を持つ [親参照を表示して開く](#view-parent-references).
* コンテンツフラグメントの階層表示とその参照 ( [構造ツリー](#structure-tree).

>[!WARNING]
>
>この節で説明するエディターは、です。 *のみ* 次の場所で使用可能： *オンライン* Adobe Experience Manager(AEM)as a Cloud Service。

## コンテンツフラグメントエディター {#content-fragment-editor}

コンテンツフラグメントエディターを初めて開くと、次の 4 つの主な領域が表示されます。

* 上部のツールバー：主要な情報とアクション
   * コンテンツフラグメントコンソールへのリンク（ホームアイコン）
   * モデルとフォルダーに関する情報
   * リンク先 [プレビュー（モデルにデフォルトのプレビュー URL パターンが設定されている場合）](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-fragment-model-properties)
   * [公開](#publish-content-fragment)、および [非公開](#unpublish-content-fragment) アクション
   * すべてを表示するオプション **親参照** （リンクアイコン）
   * フラグメント **[ステータス](/help/sites-cloud/administering/content-fragments/managing.md#statuses-content-fragments)**、最後に保存した情報
   * 元の（アセットベースの）エディターに切り替える切り替え

     >[!WARNING]
     >
     >元のエディターが同じタブに開きます。 両方のエディターを同時に開くことはお勧めしません。

* 左側のパネル：表示 **[バリエーション](#variations)** コンテンツフラグメントとその **フィールド**:
   * これらのリンクは、 [コンテンツフラグメント構造に移動する](#navigate-structure)
* 右パネル：タブを表示します。 [プロパティ（メタデータ）とタグの表示](#view-properties-tags)、 [バージョン履歴](#view-version-history)、および [言語コピー](#view-language-copies)
   * （内） **プロパティ** タブを更新するには、 **タイトル** および **説明** フラグメントの場合は、 **バリエーション**
* 中央パネル：選択したバリエーションの実際のフィールドとコンテンツを表示します
   * コンテンツの編集が可能
   * if **タブプレースホルダー** フィールドは、ここに表示されるモデル内で定義され、ナビゲーションに使用できます。フィールドは、水平方向に表示されるか、ドロップダウンリストとして表示されます。

![コンテンツフラグメントエディター — 概要](assets/cf-authoring-overview.png)

## コンテンツフラグメント構造に移動する {#navigate-structure}

単一のコンテンツフラグメント

* 次の 2 つのレベルで構成されます。

   * **[バリエーション](#variations)** コンテンツフラグメントの
   * **フィールド**  — コンテンツフラグメントモデルで定義され、すべてのバリエーションで使用されます。

* 様々な参照を含めることができます。

### バリエーションとフィールド {#variations-and-fields}

左側のパネルには、次の情報が表示されます。

* リスト **[バリエーション](#variations)** このフラグメント用に作成された
   * **メイン** は、コンテンツフラグメントの最初の作成時に存在するバリエーションです。後で他のバリエーションを追加できます。
   * バリエーションを選択して開き、編集できます。
   * また、 [バリエーションを作成](#create-variation)
* の **フィールド** フラグメント内とそのバリエーション内：
   * アイコンは、 [データタイプ](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)
   * テキストはフィールド名です。
   * これらを組み合わせると、（現在のバリエーションの）中央パネルのフィールドコンテンツへの直接リンクが提供されます。

### リンク先に移動 {#follow-links}

エディターの様々な部分で、リンクアイコンが表示されます。 これを使用して、表示される項目（コンテンツフラグメントモデル、親参照、参照されているフラグメントなど）を開くことができます。

![コンテンツフラグメントエディター — リンクアイコン](assets/cf-authoring-link-icon.png)

### 構造ツリー {#structure-tree}

を開きます。 **構造ツリー** 」タブをクリックして、コンテンツフラグメントの階層構造とその参照を表示します。 リンクアイコンを使用して参照に移動します。

![コンテンツフラグメントエディター — 構造ツリー](assets/cf-authoring-structure-tree.png)

>[!NOTE]
>
>詳しくは、 [コンテンツフラグメント構造の分析 — 構造ツリー](/help/sites-cloud/administering/content-fragments/analysis.md#structure-tree) を参照してください。

## 保存と自動保存 {#saving-autosaving}

<!-- CHECK: cannot be saved, no undo, redo -->

更新をおこなうたびに、コンテンツフラグメントが自動的に保存されます。 最後に保存した時間が上部のツールバーに表示されます。

## バリエーション {#variations}

[バリエーション](/help/sites-cloud/administering/content-fragments/overview.md#main-and-variations) は、AEMコンテンツフラグメントの重要な機能です。 これにより、 **メイン** 特定のチャネルやシナリオで使用するコンテンツ。ヘッドレスなコンテンツ配信やページオーサリングをより柔軟におこなえます。

エディターから、次の操作を実行できます。

* [バリエーションを作成](#create-variation) の **メイン** コンテンツ

* コンテンツの編集に必要なバリエーションを選択

* [バリエーションの名前を変更](#rename-variation)

* [バリエーションの削除](#delete-variation)

### バリエーションを作成 {#create-variation}

コンテンツフラグメントのバリエーションを作成するには：

1. 左側のパネルで、 **プラス記号** (**バリエーションを作成**) の右側にある **バリエーション**.

   >[!NOTE]
   >
   >最初のバリエーションを作成すると、既存のバリエーションが同じパネルに表示されます。

   ![コンテンツフラグメントエディター — 最初のバリエーションを作成する](assets/cf-authoring-create-variation-01.png)

1. ダイアログで、 **タイトル** のバリエーションに対して、 **説明** 必要に応じて、

   ![コンテンツフラグメントエディター — バリエーションを作成ダイアログ](assets/cf-authoring-create-variation-02.png)

1. **作成** バリエーション。 リストに表示されます。

### バリエーションの名前を変更 {#rename-variation}

の名前を変更するには **バリエーション**:

1. 必要なバリエーションを選択します。

1. を開きます。 **プロパティ** 」タブを右側のパネルに表示します。

1. バリエーションを更新 **タイトル**.

1. 次のいずれかを押します。 **戻る** または、別のフィールドに移動して、変更を自動保存します。 タイトルは **バリエーション** パネルが左側に表示されます。


### バリエーションの削除 {#delete-variation}

コンテンツフラグメントのバリエーションを削除するには：

>[!NOTE]
>
>を削除することはできません **メイン**.

1. 「バリエーション」を選択します。

1. Adobe Analytics の **バリエーション** パネルで、削除アイコン（ごみ箱）を選択します。

   ![コンテンツフラグメントエディター — バリエーションを削除アイコン](assets/cf-authoring-delete-variation.png)

1. ダイアログが表示されます。選択 **削除** をクリックしてアクションを確定します。

## 複数行テキストフィールドの編集 — プレーンテキストまたは Markdown {#edit-multi-line-text-fields-plaintext-markdown}

**[複数行テキスト](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)** フィールドは、次の 3 つの形式のいずれかを持つことができます。

* プレーンテキスト
* [Markdown](/help/sites-cloud/administering/content-fragments/markdown.md)
* [リッチテキスト](#edit-multi-line-text-fields-rich-text)

「プレーンテキスト」または「Markdown」として定義されたフィールドには、（画面上の）書式設定オプションのないシンプルなテキストボックスがあります。

![コンテンツフラグメントエディター — 複数行テキスト — 全画面表示](assets/cf-authoring-multilinetext-plaintext-markdown.png)

## 複数行テキストフィールドを編集 — リッチテキスト {#edit-multi-line-text-fields-rich-text}

の場合 **[複数行テキスト](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)** 次のように定義されたフィールド **リッチテキスト**&#x200B;には、様々な機能を使用できます。

* コンテンツを編集します。
   * 取り消し／やり直し
   * テキストとして貼り付け/貼り付け
   * コピー
   * 段落書式を選択
   * テーブルを作成/管理
   * テキストの書式設定；太字、斜体、下線、色
   * 段落の配置を設定
   * リストの作成/管理（箇条書き、番号付き）
   * テキストをインデント、減らす、増やす
   * 現在の書式をクリア
   * リンクを挿入
   * 画像アセットへの参照を選択して挿入
   * 特殊文字を追加する
* [全画面表示エディター](#full-screen-editor-rich-text)  — フルスクリーンとインフローを切り替える
* [統計](#statistics-rich-text)
* [比較と同期](#compare-and-synchronize-rich-text)

次に例を示します。

![コンテンツフラグメントエディター — 複数行テキスト — 全画面表示切り替え](assets/cf-authoring-multilinetext-fullscreen-toggle.png)

>[!NOTE]
>
>複数行テキストフィールドも、適切な [アイコン](#fields-datatypes-icons) （内） **フィールド** パネル。

### 全画面表示エディター — リッチテキスト {#full-screen-editor-rich-text}

全画面表示エディターでは、インフロー時と同じ編集オプションを提供しますが、テキスト用のスペースが増えます。

次に例を示します。

![コンテンツフラグメントエディター — 複数行テキスト — 全画面表示](assets/cf-authoring-multilinetext-fullscreen.png)

### 統計 — リッチテキスト {#statistics-rich-text}

アクション **統計** [ 複数行 ] フィールドに、テキストに関する情報の範囲を表示します。

次に例を示します。

![コンテンツフラグメントエディター — 統計](assets/cf-authoring-multilinetext-statistics.png)

### 比較と同期 — リッチテキスト {#compare-and-synchronize-rich-text}

アクション **比較** は、 **バリエーション** を開きます。

これにより、複数行フィールドがフルスクリーンで開き、次の操作がおこなわれます。

* 両方のコンテンツを表示 **メイン** そして現在の **バリエーション** 並行して、違いが強調されている

* 違いは色で示されます。

   * 緑は（バリエーションに）追加されたコンテンツを示します
   * 赤は削除されたコンテンツを示します（バリエーションからの削除）
   * 青は置換されたテキストを示します

* には、 **同期** アクション：コンテンツを同期します。 **メイン** 現在のバリエーションに

   * if **メイン** が更新された場合、これらの変更はバリエーションに転送されます
   * バリエーションが更新されている場合、これらの変更は **メイン**

  >[!CAUTION]
  >
  >同期を使用できるのは、変更をコピーする場合のみです *から&#x200B;**メイン**バリエーションに*.
  >
  >変更の転送 *～の変化から&#x200B;**メイン*** はオプションとして使用できません。

例えば、バリエーションコンテンツが完全に書き換えられたシナリオの場合、同期によってその新しいコンテンツが、 **メイン**:

![コンテンツフラグメントエディター — 比較と同期](assets/cf-authoring-multilinetext-compare.png)

## 参照を管理 {#manage-references}

### フラグメント参照 {#fragment-references}

[フラグメント参照](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#fragment-reference-nested-fragments) は、次の目的で使用できます。

* [既存のコンテンツフラグメントへの参照を作成する](#create-reference-existing-content-fragment)
* [コンテンツフラグメントを作成し、それを参照します。](#create-reference-content-fragment)

#### 既存のコンテンツフラグメントへの参照を作成する {#create-reference-existing-content-fragment}

既存のコンテンツフラグメントへの参照を作成するには：

1. 「 」フィールドを選択します。
1. 選択 **既存のフラグメントを追加**.
1. フラグメントセレクターから必要なフラグメントを選択します。

   >[!NOTE]
   >
   >一度に 1 つのフラグメントのみを選択できます。

#### コンテンツフラグメントを作成し、参照します。 {#create-reference-content-fragment}

または、 [選択 **新しいフラグメントを作成** 開く **作成** ダイアログ](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment). 作成されたフラグメントは、参照されます。

### コンテンツ参照 {#content-references}

[コンテンツ参照](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-reference) は、画像、ページ、エクスペリエンスフラグメントなど、他のAEMコンテンツタイプを参照するために使用されます。

#### 参照画像 {#reference-images}

In **コンテンツ参照** 次の両方を実行できるフィールド：

* リポジトリに既に存在する参照アセット
* フィールドに直接アップロードするので、 **Assets** アップロードするコンソール

  >[!NOTE]
  >
  >画像を **コンテンツ参照** フィールド、 **必須**:
  >
  >* 持っている **ルートパス** ( [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-reference)) をクリックします。 画像を保存する場所を指定します。
  >* 含める **画像** （許可されたコンテンツタイプのリスト）

アセットを追加するには、次のいずれかを実行します。

* 新しいアセットファイルを（例えば、ファイルシステムから） **コンテンツ参照** フィールド
* を使用します。 **アセットを追加** 「 」アクションを選択して、次のいずれかを選択します。 **アセットを参照** または **アップロード** をクリックして、使用する適切なセレクターを開きます。

  ![コンテンツフラグメントエディター — アセットオプションを追加](assets/cf-authoring-add-asset-options.png)

#### 参照ページ {#reference-pages}

AEMページ、エクスペリエンスフラグメントまたはその他のコンテンツタイプへの参照を追加するには、次の手順を実行します。

1. 選択 **コンテンツのパスを追加**.

1. 入力フィールドに必要なパスを追加します。

1. 次で確認： **追加**.

### 親参照を表示 {#view-parent-references}

上部のツールバーでリンクアイコンを選択すると、すべての親参照のリストが開きます。

次に例を示します。

![コンテンツフラグメントエディター — 参照を表示](assets/cf-authoring-show-references-link.png)

ウィンドウが開き、関連するすべての参照が表示されます。 参照を開くには、名前、タイトル、またはリンクアイコンを選択します。

次に例を示します。

![コンテンツフラグメントエディター — 参照を表示](assets/cf-authoring-show-references.png)

## プロパティとタグを表示する {#view-properties-tags}

右側のパネルの「プロパティ」タブでは、プロパティ（メタデータ）とタグを表示できます。 プロパティは次のいずれかになります。

* （の） **コンテンツフラグメント** - if **メイン** は現在選択されています
* 特定の **バリエーション**

![コンテンツフラグメントエディター — プロパティ](assets/cf-authoring-properties.png)

### プロパティとタグを編集 {#edit-properties-tags}

「プロパティ」タブ（右パネル）では、次の項目も編集できます。

* **タイトル**
* **説明**
* **タグ**：ドロップダウンリストまたは選択ダイアログの使用

  ![コンテンツフラグメントエディター — タグを管理](assets/cf-authoring-edit-tags.png)

### コンテンツフラグメントモデルを開く {#open-content-fragment-model}

次の場合： **メイン** オンにすると、基になるコンテンツフラグメントモデルの名前が「プロパティ」セクションに表示されます。 リンクアイコンを選択すると、モデルが別のタブで開きます。

次に例を示します。

![コンテンツフラグメントエディター — コンテンツフラグメントモデルを開く](assets/cf-authoring-open-model.png)

## バージョン履歴の表示 {#view-version-history}

Adobe Analytics の **バージョン履歴** 右のパネルの「 」タブに、現在のバージョンと以前のバージョンの詳細が表示されます。

>[!NOTE]
>
>コンテンツフラグメントの公開時に新しいバージョンが作成されます。

![コンテンツフラグメントエディター — バージョン履歴の概要](assets/cf-authoring-version-history-overview.png)

### 特定のバージョンに戻す {#revert-version}

どのバージョンにも戻すことができます。

特定のバージョンに戻すには：

1. バージョンの横にある 3 つのドットのアイコンを選択します。

1. 選択 **元に戻す**.

![コンテンツフラグメントエディター — バージョン履歴を元に戻す](assets/cf-authoring-version-history-revert.png)

## 言語コピーの表示 {#view-language-copies}

Adobe Analytics の **言語プロパティ** 関連する言語コピーのタブの詳細が表示されます。 リンクアイコンを選択すると、そのコピーが別のタブで開きます。

次に例を示します。

![コンテンツフラグメントエディター — 言語コピーを開く](assets/cf-authoring-open-language-copies.png)

>[!NOTE]
>
>コンテンツフラグメントの翻訳と言語コピーの作成について詳しくは、 [AEMヘッドレス翻訳ジャーニー](/help/journey-headless/translation/overview.md).


## フラグメントをプレビュー {#preview-content-fragment}

コンテンツフラグメントエディターを使用すると、編集内容を外部フロントエンドアプリケーションでプレビューするオプションを作成者に提供できます。

この機能を使用するには、まず次の操作が必要です。

* IT チームと協力して、JSON 出力を使用してコンテンツフラグメントをレンダリングする外部フロントエンドアプリケーションを設定します。
* 外部フロントエンドアプリケーションが設定されると、 **デフォルトのプレビュー URL パターン** は、 [適切なコンテンツフラグメントモデルのプロパティ](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties).

URL が定義されると、 **プレビュー** ボタンがアクティブです。 このボタンを選択すると、（別のタブで）外部アプリケーションを起動して、コンテンツフラグメントをレンダリングできます。

## フラグメントを公開 {#publish-content-fragment}

以下が可能です。 **公開** フラグメントを次のいずれかに変更します。

* インスタンスをプレビュー
* 発行インスタンス

フラグメントは、エディターまたはコンソールから公開できます。 詳しくは、 [フラグメントの公開とプレビュー](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment) を参照してください。

## フラグメントを非公開にする {#unpublish-content-fragment}

また、 **非公開** フラグメントを次のいずれかから選択します。

* インスタンスをプレビュー
* 発行インスタンス

フラグメントは、エディターまたはコンソールから非公開にすることができます。 詳しくは、 [フラグメントの非公開](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment) を参照してください。

## フィールド、データタイプおよびアイコン {#fields-datatypes-icons}

The **フィールド** パネルには、コンテンツフラグメント内のすべてのフィールドがリストされます。 アイコンは、 **[データタイプ](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)**:

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><p><b>1 行のテキスト</b></p> </td>
   <td><p> <img src="assets/cf-authoring-single-line-text-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>複数行テキスト</b></p> </td>
   <td><p> <img src="assets/cf-authoring-multi-line-text-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>数値</b></p> </td>
   <td><p> <img src="assets/cf-authoring-number-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>ブール値</b></p> </td>
   <td><p> <img src="assets/cf-authoring-boolean-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>日時</b></p> </td>
   <td><p> <img src="assets/cf-authoring-date-time-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>列挙</b></p> </td>
   <td><p> <img src="assets/cf-authoring-enumeration-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>タグ</b></p> </td>
   <td><p> <img src="assets/cf-authoring-tags-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>コンテンツ参照</b></p> </td>
   <td><p> <img src="assets/cf-authoring-content-reference-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>フラグメント参照</b></p> </td>
   <td><p> <img src="assets/cf-authoring-fragment-reference-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>JSON オブジェクト</b></p> </td>
   <td><p> <img src="assets/cf-authoring-json-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>タブプレースホルダー</b></p><p>実際のアイコンでは表されませんが、 <b>タブプレースホルダー</b> は左側のパネルに表示されます。 <br>中央のパネルでも、図のように水平方向に表示されるか、ドロップダウンリストで表示されます（水平方向に表示するには数が多すぎる場合）。</p> </td>
   <td><p> <img src="assets/cf-authoring-tab-icon.png"> </p></td>
  </tr>
 </tbody>
</table>

## 役に立つ知識 {#good-to-know}

* コンテンツフラグメントを編集するには、 [適切な権限](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). 問題が発生している場合は、システム管理者にお問い合わせください。

  例えば、 `edit` 権限エディターは読み取り専用になります。

* コンテンツフラグメントモデルでは、多くの場合、 **タイトル** および **説明**. これらのフィールドが存在する場合、それらはユーザー定義のフィールドであり、 *中央パネル* フラグメントの編集中に

  コンテンツフラグメントとそのバリエーションには、とも呼ばれるメタデータフィールド（バリエーションのプロパティ）もあります。 **タイトル** および **説明**. これらのフィールドは、コンテンツフラグメントの不可欠な部分で、フラグメントの作成時に最初に定義されます。 これらは、 *右パネル* フラグメントの編集中に

* 詳しくは、 Assets のドキュメントを参照してください [元のコンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-variations.md)  — 両方から利用できます **Assets** コンソールと **コンテンツフラグメント** コンソール。

* 必要に応じて、プロジェクトチームがエディターをカスタマイズできます。 詳しくは、 [コンテンツフラグメントコンソールおよびエディターのカスタマイズ](/help/implementing/developing/extending/content-fragments-console-and-editor.md) 詳しくは、を参照してください。
