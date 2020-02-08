---
title: ページのコンテンツの編集
description: ページを作成したら、必要な変更をおこなうためにコンテンツを編集できます
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# ページのコンテンツの編集{#editing-page-content}

ページが作成されたら（新規作成、またはローンチやライブコピーの一部として作成）、コンテンツを編集して、必要な更新をおこなうことができます。

コンテンツは、ページにドラッグ可能な[コンポーネント](/help/sites-cloud/authoring/features/components-console.md)（コンテンツのタイプに適したもの）を使用して追加されます。コンポーネントはその後、そのまま編集したり、移動や削除をおこなったりすることができます。

>[!NOTE]
>
>ページを編集するための適切なアクセス権と権限がアカウントにある必要があります。
>
>問題が発生した場合は、システム管理者にお問い合わせください。
<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to edit pages.
-->

>[!NOTE]
>
>If your page and/or template has been appropriately set up, then you can use [responsive layout](/help/sites-cloud/authoring/features/responsive-layout.md) when editing.

>[!TIP]
>
>When in **Edit** mode, links in your content are visible, but **not accessible**. Use [Preview mode](#previewing-pages) if you want to navigate using the links in your content.

## ページツールバー {#page-toolbar}

ページツールバーを使用すると、ページ設定に応じた適切な機能にアクセスできます。

![ページのツールバー](/help/sites-cloud/authoring/assets/editing-page-toolbar.png)

ツールバーを使用すると、様々なオプションにアクセスできます。現在のコンテキストと設定によっては、一部のオプションを使用できないことがあります。

* **サイドパネルを切り替え**

   サイドパネルが開きます（または閉じます）。このパネルには、[アセットブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)、[コンポーネントブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)および[コンテンツツリー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree)が含まれています。

   ![サイドパネル切り替え](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **ページ情報**

   ページの詳細およびページに対して実行できるアクション（ページ情報の表示と編集、ページのプロパティの表示、およびページの公開／非公開など）を含む[ページ情報](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information)メニューにアクセスできます。

   ![ページ情報ボタン](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **エミュレーター**

   別のデバイスでのページのルックアンドフィールをエミュレートするために使用する[エミュレーターツールバー](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate)を切り替えます。レイアウトモードでは自動的に切り替わります。

   ![エミュレータボタン](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

   ContextHubを開き [ます](/help/sites-cloud/authoring/personalization/contexthub.md)。 プレビューモードでのみ使用できます。

   ![コンテキストハブボタン](/help/sites-cloud/authoring/assets/context-hub.png)

* **ページタイトル**

   情報のためにのみ表示されます。

   ![ページタイトル](/help/sites-cloud/authoring/assets/page-title.png)

* **モードセレクター**

   現在の[モード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)が表示され、別のモード（編集、レイアウト、タイムワープ、ターゲット設定など）を選択できます。

   ![モード選択ボタン](/help/sites-cloud/authoring/assets/mode-selector.png)

* **プレビュー**

   [プレビューモード](#preview-mode)を有効にします。公開時に表示されるとおりにページを表示します。

   ![「プレビュー」ボタン](/help/sites-cloud/authoring/assets/preview.png)

* **注釈**

   ページをレビューするときに、ページに[注釈](/help/sites-cloud/authoring/fundamentals/annotations.md)を追加できます。最初の注釈を追加後、アイコンは、ページ上の注釈の数を示す数字に切り替わります。

   ![注釈ボタン](/help/sites-cloud/authoring/assets/annotations.png)

### ステータスの通知 {#status-notification}

If a page is part of a [workflow](/help/sites-cloud/authoring/workflows/overview.md) or multiple workflows, this information is shown in a notification bar at the top of the screen when editing the page.

![ワークフロー通知](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>ステータスバーは、適切な権限を持つユーザーアカウントにのみ表示されます。

通知には、ページに対して実行されているワークフローが一覧表示されます。ユーザーが現在のワークフローステップに関係している場合は、[ワークフローのステータスに影響する](/help/sites-cloud/authoring/workflows/participating.md)オプションや、ワークフローの詳細を取得するオプションを使用できます。例えば、次のようなものがあります。

* **完了** - 「作業項目の完 **了」ダイアログを開きます** 。
* **委任** - [作業項目の **完了]ダイアログ**
* **詳細の表示** — ワークフローの **詳細** ・ウィンドウを開きます。

Completing and delegating workflow steps via the notification bar works as it does when [participating in workflows](/help/sites-cloud/authoring/workflows/participating.md) from the Notification inbox.

ページが複数のワークフローの対象である場合は、ワークフローの数がワークフローをスクロールできる矢印ボタンと共に通知の右端に表示されます。

![複数のワークフロー通知](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## コンポーネントプレースホルダー {#component-placeholder}

コンポーネントプレースホルダーは、コンポーネントをドロップしたときのコンポーネントの配置場所（現在ポインターを置いているコンポーネントの上）を示します。

* ページに新しいコンポーネントを追加する場合（コンポーネントブラウザーからドラッグ）：

   ![ページに新しいコンポーネントを追加する際のプレースホルダー](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* 既存のコンポーネントを移動する場合：

   ![ページ上の既存のコンポーネントを移動する際のプレースホルダー](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## コンポーネントの挿入 {#inserting-a-component}

### コンポーネントブラウザーからのコンポーネントの挿入 {#inserting-a-component-from-the-components-browser}

[コンポーネントブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)を使用して、新しいコンポーネントを追加できます。[コンポーネントプレースホルダー](#component-placeholder)にコンポーネントの配置先が表示されます。

1. ページが[**編集&#x200B;**モード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)であることを確認します。
1. [コンポーネントブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)を開きます。
1. 必要なコンポーネントを[必要な位置](#component-placeholder)までドラッグします。
1. コンポーネントを[編集](#edit-content)します。

>[!NOTE]
>
>モバイルデバイスでは、コンポーネントブラウザーは画面全体に表示されます。コンポーネントをドラッグすると、ブラウザーが閉じて、コンポーネントを配置できるようにページが再び表示されます。

### 段落システムからのコンポーネントの挿入 {#inserting-a-component-from-the-paragraph-system}

段落システムの「**コンポーネントをここにドラッグ**」ボックスを使用して、新しいコンポーネントを追加できます。

1. ページが[**編集&#x200B;**モード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)であることを確認します。
1. 段落システムから新しいコンポーネントを選択して追加する方法は 2 つあります。

   * 既存のコンポーネントのツールバーまたは「**コンポーネントをここにドラッグ**」ボックスから&#x200B;**コンポーネントを挿入**&#x200B;オプション（+）を選択します。

      ![コンポーネントの挿入](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * If you are on a desktop device you can double-click on the **Drag components here** box.

   * **新規コンポーネントを挿入**&#x200B;ダイアログが表示され、必要なコンポーネントを選択できるようになります。

      ![新規コンポーネントを挿入ダイアログ](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. 選択したコンポーネントがページの下部に追加されます。必要に応じてコンポーネントを[編集](#edit-content)します。

### アセットブラウザーを使用したコンポーネントの挿入 {#inserting-a-component-using-the-assets-browser}

[アセットブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)からアセットをドラッグして、ページに新しいコンポーネントを追加することもできます。この操作により、適切なタイプの新しいコンポーネント（アセットが格納される）が自動的に作成されます。

この動作は使用しているインストール環境で設定できます。See Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance for further details. <!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

前述のいずれかのアセットタイプをドラッグしてコンポーネントを作成するには：

1. ページが[**編集&#x200B;**モード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)であることを確認します。
1. [アセットブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)を開きます。
1. 必要なアセットを必要な位置までドラッグします。[コンポーネントプレースホルダー](#component-placeholder)にコンポーネントの配置先が表示されます。

   アセットタイプに適したコンポーネントが、必要な場所に作成されます。これには選択したアセットが含まれます。

1. 必要に応じて、コンポーネントを[編集](#edit-content)します。

>[!NOTE]
>
>モバイルデバイスでは、アセットブラウザーは画面全体に表示されます。アセットをドラッグすると、ブラウザーが閉じて、アセットを配置できるようにページが再び表示されます。

If when browsing the assets you find that you need to make a quick change to an asset, you can start the asset editor directly from the browser by clicking the edit icon next to the asset&#39;s name. <!--If when browsing the assets you find that you need to make a quick change to an asset, you can start the [asset editor](/help/assets/manage-digital-assets.md) directly from the browser by clicking the edit icon next to the asset's name.-->

![アセット編集ボタン](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## コンポーネントツールバー {#component-toolbar}

コンポーネントを選択すると、ツールバーが開きます。このツールバーからコンポーネントに対して様々なアクションを実行できます。

ユーザーが使用できる実際のアクションは、必要に応じて表示されます。ここではすべてのアクションについては説明していません。

![コンポーネントツールバー](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **編集**

   [コンポーネントのタイプに応じて](/help/sites-cloud/authoring/fundamentals/components.md) 、コンポーネントのコ [ンテンツを編集できます](#edit-content)。 多くの場合、ツールバーが提供されます。

   「![編集」ボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **設定**

   [コンポーネントのタイプに応じて](/help/sites-cloud/authoring/fundamentals/components.md) 、コンポーネントのプロパティを編集および設定できます。 多くの場合、ダイアログが開きます。

   ![設定ボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-configure.png)

* **コピー**

   コンポーネントをクリップボードにコピーします。貼り付け後も、元のコンポーネントは残ります。

   ![コピーボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-copy.png)

* **切り取り**

   コンポーネントをクリップボードにコピーします。貼り付け後、元のコンポーネントは削除されます。

   ![切り取りボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-cut.png)

* **削除**

   確認後に、ページからコンポーネントを削除します。

   ![削除ボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-delete.png)

* **コンポーネントを挿入**

   [新しいコンポーネントを追加](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system)するためのダイアログが開きます。

   ![挿入ボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-insert.png)

* **貼り付け**

   クリップボードにコピーしたコンポーネントをページに貼り付けます。元のコンポーネントが残るかどうかは、コピーするか、切り取るかによって決まります。

   * 同じページ、または別のページに貼り付けることができます。
   * 項目は、貼り付けアクションを選択した項目の上に貼り付けられます。
   * 貼り付けアクションは、クリップボードにコンテンツがある場合にのみ表示されます。
   ![貼り付けボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-paste.png)

   >[!NOTE]
   >
   >切り取り／コピー操作の前に既に開いていた別のページに貼り付ける場合は、ページを更新して、貼り付けたコンテンツを表示する必要があります。

* **グループ**

   複数のコンポーネントを一度に選択できます。デスクトップデバイスで同じ操作をおこなうには、**Control キーを押しながらクリック**&#x200B;するか、または **Command キーを押しながらクリック**&#x200B;します。

   ![グループボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **親**

   これにより、選択したコンポーネントの親コンポーネントを選択できます。

   ![親ボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **レイアウト**

   選択したコンポーネントの[レイアウト](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout)を変更できます。選択したコンポーネントにのみ適用され、ページ全体の[レイアウトモード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)はアクティブ化されません。

   ![レイアウトボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **エクスペリエンスフラグメントバリエーションに変換**

   これを使用すると、選択したコンポーネントから新しい[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)を作成したり、既存のエクスペリエンスフラグメントに追加したりできます。

   ![エクスペリエンスフラグメントに変換ボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## コンテンツの編集 {#edit-content}

コンポーネント内のコンテンツを追加または編集するには、次の 2 つの方法があります。

* [編集用のコンポーネントのダイアログ](#component-edit-dialog)を開きます。
* アセットブラウザーから[アセットをドラッグ＆ドロップ](#drag-and-drop-assets-into-component)して、コンテンツを直接追加します。

### コンポーネントの編集ダイアログ {#component-edit-dialog}

[コンポーネントツールバーの編集（鉛筆）アイコン](#component-toolbar)を使用して、コンポーネントを開いてコンテンツを編集できます。

正確な編集オプションは、コンポーネントによって異なります。一部のコンポーネントでは[フルスクリーンモードでのみすべてのアクションを使用できます](#edit-content-full-screen-mode)。次に例を示します。

* テキストコンポーネント

   ![テキストコンポーネントのツールバー](/help/sites-cloud/authoring/assets/editing-text-component-toolbar.png)

* 画像コンポーネント

   ![画像コンポーネントのツールバー](/help/sites-cloud/authoring/assets/editing-image-component-toolbar.png)

   >[!NOTE]
   >
   >編集は、空の画像コンポーネントでは動作しません。
   >
   >コンポーネントの編集を開始する前に、コンポーネントに画像をドラッグまたはアップロードする必要があります。

* 画像コンポーネント - 全画面

   画像コンポーネント[のフルスクリーンモードに入ると](#edit-content-full-screen-mode)、画像を編集する領域が広くなり、追加の編集オプション（「**マップを起動**」や「**ズームをリセット**」など）が表示されます。また、全画面では切り抜きプリセットを選択できます。

   ![画像コンポーネントのフルスクリーンモード](/help/sites-cloud/authoring/assets/editing-image-component-full-screen.png)

* 複数の基本コンポーネントから構成されるコンポーネントは、まず、必要な編集オプションのセットを確認するように求められます。

### アセットのコンポーネントへのドラッグ＆ドロップ {#drag-and-drop-assets-into-component}

特定のコンポーネントタイプ（画像など）に対して、アセットブラウザからコンポーネントに直接アセットをドラッグ&amp;ドロップして、コンテンツを更新できます。

## Edit Content in Full Screen Mode {#edit-content-full-screen-mode}

次のアイコンを使用して、すべてのコンポーネントで全画面表示モードにアクセス（または終了）できます。

![フルスクリーンボタン](/help/sites-cloud/authoring/assets/editing-full-screen.png)

例えば、**テキスト**&#x200B;コンポーネントの場合は、次のように表示されます。

![フルスクリーンのテキストコンポーネント](/help/sites-cloud/authoring/assets/editing-text-full-screen.png)

>[!NOTE]
>
>一部のコンポーネントでは、フルスクリーンモードに基本のインプレイスエディターよりも多くのオプションを使用できます。

## コンポーネントの移動 {#moving-a-component}

段落コンポーネントを移動するには：

1. タップ＆ホールドまたはクリック＆ホールドによって移動する段落を選択します。
1. 段落を新しい場所にドラッグします。段落を配置できる場所が示されます。目的の場所にドロップします。

   ![コンポーネントの移動](/help/sites-cloud/authoring/assets/editing-moving-component.png)

1. 段落が移動されます。

>[!TIP]
>
>[切り取りと貼り付け](#component-toolbar)を使用して、コンポーネントを移動することもできます。

## コンポーネントのレイアウトの編集 {#edit-component-layout}

コンポーネントを調整するために編集モードから[レイアウトモード](/help/sites-cloud/authoring/features/responsive-layout.md)に繰り返し切り替える代わりに、コンポーネントの&#x200B;**レイアウト**&#x200B;アクションを選択してそのコンポーネントのレイアウトを変更すると、編集モードから切り替える必要がなくなり、時間を節約できます。

1. When in **Edit** mode of the sites console, selecting a component reveals the component&#39;s toolbar.

   ![ページコンポーネントのコンポーネントツールバー](/help/sites-cloud/authoring/assets/editing-layout-toolbar.png)

   Click or tap the **Layout** action to adjust the layout of the component.

   ![コンポーネントツールバーの「レイアウト」ボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

1. レイアウトアクションを選択すると、

   * コンポーネントのサイズ変更ハンドルが表示されます。
   * エミュレーターツールバーが画面の上部に表示されます。
   * 標準の編集アクションの代わりにレイアウトアクションが、コンポーネントツールバーに表示されます。
   ![レイアウトモードのコンポーネント](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   You can now modify the layout of the component as you would in [layout mode](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode).

1. After making the necessary layout changes, click the **Close** button in the component action menu to stop modifying the layout of the component. コンポーネントのツールバーは通常の編集状態に戻ります。

   ![ページコンポーネントのコンポーネントツールバー](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>レイアウトアクションは、選択したコンポーネントの範囲に限定されます。例えば、あるコンポーネントのレイアウトを編集し、別のコンポーネントをクリックすると、新しく選択したコンポーネントの標準編集ツールバー（レイアウトツールバーではなく）が表示され、サイズ変更ハンドルとエミュレータツールバーが非表示になります。
>
>複数のコンポーネントに影響するページの全体のレイアウトを編集する必要がある場合は、[レイアウトモード](/help/sites-cloud/authoring/features/responsive-layout.md)に切り替えます。

## 継承されたコンポーネント {#inherited-components}

継承とは、コンテンツをコンポーネント間で自動的にプッシュできるメカニズムです。 継承されたコンポーネントは、次のような様々なシナリオによって生成されます。

* マルチサイト管理 <!--[Multi site management](/help/sites-administering/msm.md)-->
* [ローンチ](/help/sites-cloud/authoring/launches/overview.md)（ライブコピーをベースとしている場合）

継承はキャンセル（その後再度有効化）できます。コンポーネントに応じて、コンポーネントがライブコピーまたは（ライブコピーに基づく）起動の一部であるページ上にある場合は、コンポーネントツールバーから使用できます。

![継承関係を示すコンポーネントツールバー](/help/sites-cloud/authoring/assets/editing-component-toolbar-inheritance.png)

次に例を示します。

* 継承をキャンセル

   ![継承のキャンセルボタン](/help/sites-cloud/authoring/assets/editing-cancel-inheritance.png)

* 継承を再有効化（既に継承がキャンセルされている場合）

   ![継承を再有効化ボタン](/help/sites-cloud/authoring/assets/editing-reenable-inheritance.png)

* ロールアウトアクションは、Blueprintまたはライブコピーソースでも使用できます

   ![ロールアウトボタン](/help/sites-cloud/authoring/assets/editing-rollout.png)

## ページテンプレートの編集 {#editing-the-page-template}

ページ情報メニューで「テンプレートの編集」 [を選択すると](/help/sites-cloud/authoring/features/templates.md#editing-templates-template-authors) 、テンプ **レートエディターに簡単** に切り替えることができま [](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information)す。

[列表示](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)または[リスト表示](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)でページを選択するときに、ページが基にしているテンプレートを簡単に確認できます。

## ライブコピーステータス {#live-copy-status}

[ライブコピーステータスページモード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)では、ライブコピーのステータスの簡単な概要、および継承される（または継承されない）コンポーネントを示すことができます。

* 緑のボーダー：継承
* ピンクのボーダー：継承がキャンセルされている

次に例を示します。

![ライブコピーステータスの表示例](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## 注釈の追加 {#adding-annotations}

[注釈](/help/sites-cloud/authoring/fundamentals/annotations.md)を使用すると、レビュー担当者や他の作成者がコンテンツに関するフィードバックを提供できます。注釈は、レビューや検証の目的でよく使用されます。

## ページのプレビュー {#previewing-pages}

ページをプレビューするには、以下の 2 つの方法があります。

* [プレビューモード](#preview-mode) - その場ですばやく確認できるプレビュー
* [公開済みとして表示](#view-as-published) - ページを新しいタブに開くフルプレビュー

>[!TIP]
>
>* コンテンツ内のリンクは表示されますが、編集モードでアクセスすることはできません。
>* リンクを使用して移動する場合には、いずれかのプレビューオプションを使用してください。
>* Use the [keyboard shortcut](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M` to switch between preview and the last selected mode.


>[!NOTE]
>
>WCMモードCookieは、両方のプレビューオプションに対して設定されます。

### プレビューモード {#preview-mode}

コンテンツの編集時に、プレビュー[モード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)を使用してページをプレビューすることができます。このモードでは、次の操作を実行できます。

* 各種編集メカニズムを非表示にして公開時にページがどのように表示されるかをすばやく確認できます。
* リンクを使用して移動できます。
* ページコンテンツは更新&#x200B;**されません**。

オーサリング時に、ページエディターの右上にある次のアイコンを使用して、プレビューモードに切り替えることができます。

![「プレビュー」ボタン](/help/sites-cloud/authoring/assets/preview.png)

### 公開済みとして表示 {#view-as-published}

「**公開済みとして表示**」オプションは、[ページ情報](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information)メニューで使用できます。これによりページが新しいタブで開き、コンテンツが更新され、ページがパブリッシュ環境で表示されるとおりに表示されます。

## ページのロック {#locking-a-page}

AEM では、他のユーザーによるコンテンツの変更を防ぐためにページをロックすることができます。ページのロックは、1 つの特定のページで大量の編集作業をおこなう場合や、短期間ページを凍結する必要がある場合に便利です。

ページは次のいずれかの場所からロックできます。

* **サイト**&#x200B;コンソール

   1. [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)でページを選択します。
   1. ロックアイコンを選択します。

      ![ロックボタン](/help/sites-cloud/authoring/assets/lock.png)

* **ページエディター**

   1. **ページ情報**&#x200B;アイコンを選択して、メニューを開きます。
   1. 「**ページをロック**」オプションを選択します。

ロックすると、コンソール表示の情報が更新され、編集時にロック記号がツールバーに表示されます。

![ロックされたページの例](/help/sites-cloud/authoring/assets/editing-locked-page.png)

>[!CAUTION]
>
>ページのロックは、別のユーザーとして実行している場合にも実行できます。ただし、この方法でロックされたページをロック解除できるのは、別のユーザーとして実行したユーザーか、管理者ユーザーです。
>
>実際にページのロック作業をおこなったユーザーに成り代わっても、ページをロック解除できません。
<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## ページのロック解除 {#unlocking-a-page}

Unlocking a page is very similar to [locking the page](#locking-a-page). Once the page is locked the lock options are replaced by unlock actions.

ページ情報メニューには「**ロック解除**」がオプションとして表示され、サイトコンソールのロックアイコンは「**ロック解除**」アイコンに置き換えられます。

![ロック解除ボタン](/help/sites-cloud/authoring/assets/unlock.png)

>[!CAUTION]
>
>ページのロックは、別のユーザーとして実行している場合にも実行できます。ただし、この方法でロックされたページをロック解除できるのは、別のユーザーとして実行したユーザーか、管理者ユーザーです。
>
>実際にページのロック作業をおこなったユーザーに成り代わっても、ページをロック解除できません。
<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## Undoing and Redoing Page Edits {#undoing-and-redoing-page-edits}

次のアイコンを使用して、アクションの取り消しまたはやり直しを行うことができます。これらのアイコンは、ツールバーに適宜表示されます。

![「取り消し」ボタンと「やり直し」ボタン](/help/sites-cloud/authoring/assets/redo.png)

>[!TIP]
>
>* The [keyboard shortcut](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Z` is also available to undo page edit actions.
>* The keyboard shortcut `Ctrl-Y` is also available to redo page edit actions.


>[!NOTE]
>
>ページ編集の取り消しとやり直しによって実行可能なことについて詳しくは、[ページ編集の取り消しとやり直し - 理論](#undoing-and-redoing-page-edits-the-theory)を参照してください。

## ページ編集の取り消しとやり直し - 理論 {#undoing-and-redoing-page-edits-the-theory}

AEM では、ユーザーが実行するアクションの履歴と、それらのアクションを実行した順序が保存されます。そのため、複数のアクションの取り消しは、ユーザーが実行した順序でおこなうことができます。その後、必要に応じて、やり直しを使用して 1 つ以上のアクションを再適用することもできます。

コンテンツページで要素（テキストコンポーネントなど）が選択されている場合、取り消しコマンドとやり直しコマンドは選択した項目に適用されます。

元に戻すコマンドとやり直しコマンドの動作は、他のソフトウェアの動作と似ています。コンテンツに関する意思決定を行う際に、Webページの最新の状態を復元するには、次のコマンドを使用します。 例えば、テキスト段落をページ上の別の場所に移動した場合に、取り消しコマンドを使用して、その段落を元の場所に戻すことができます。前の場所のほうがいい場合は、やり直しコマンドを使用して「取り消しを取り消し」ます。

例えば、次の操作を実行できます。

* 取り消しを使用してからページの編集をおこなっていない限り、アクションをやり直すことができます。
* 最大 20 回の編集アクションを取り消すことができます（デフォルト設定）。
* 様々な[キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)を利用して取り消しとやり直しをおこなうこともできます。

取り消しおよびやり直しは、次のようなページの変更に対して使用できます。

* 段落の追加、編集、削除および移動
* 段落コンテンツのインプレース編集
* ページ内部での項目のコピー、カットおよび貼り付け

>[!NOTE]
>
>* ファイルと画像に対する変更の取り消しおよびやり直しには、特別な権限が必要になります。
>* ファイルや画像への変更の履歴は、少なくとも 10 時間維持されます。この時間を経過すると、変更の取り消しは保証されません。管理者はデフォルトの 10 時間を変更できます。
>* システム管理者は、インスタンスの要件に従って取り消しおよびやり直し機能の様々な面を設定できます。

<!--* Your system administrator can [configure various aspects of the Undo/Redo features](/help/sites-administering/config-undo.md) according to the requirements for your instance.-->
