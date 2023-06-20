---
title: ページのコンテンツの編集
description: ページを作成したら、コンテンツを編集して、必要な更新を行うことができます
exl-id: 8af0f621-14e8-4605-a51a-a3be21f19092
source-git-commit: 635f4c990c27a7646d97ebd08b453c71133f01b3
workflow-type: tm+mt
source-wordcount: '3004'
ht-degree: 60%

---

# ページのコンテンツの編集 {#editing-page-content}

ページが作成されたら（新規またはローンチまたはライブコピーの一部として）、コンテンツを編集して、必要な更新をおこなうことができます。

コンテンツを追加するには、 [コンポーネント](/help/sites-cloud/authoring/features/components-console.md) （コンテンツタイプに適した）ページにドラッグできます。 コンポーネントはその後、そのまま編集したり、移動や削除をおこなったりすることができます。

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
>ページやテンプレートが適切に設定されていると、編集中に[レスポンシブレイアウト](/help/sites-cloud/authoring/features/responsive-layout.md)を使用できます。

>[!TIP]
>
>**編集**&#x200B;モードでは、コンテンツのリンクは表示されますが、**アクセスできません**。コンテンツのリンクを使用して移動する場合は、[プレビューモード](#previewing-pages)を使用します。

## ページツールバー {#page-toolbar}

ページツールバーを使用すると、ページ設定に応じた適切な機能にアクセスできます。

![ページツールバー](/help/sites-cloud/authoring/assets/editing-page-toolbar.png)

ツールバーを使用すると、多数のオプションにアクセスできます。 現在のコンテキストと設定によっては、一部のオプションを使用できない場合があります。

* **サイドパネルを切り替え**

  これにより、サイドパネルが開く（または閉じる）ので、 [アセットブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser), [コンポーネントブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)、および [コンテンツツリー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree).

  ![サイドパネルの切り替え](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **ページ情報**

  次にアクセスできる [ページ情報](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) ページ上で実行できるページの詳細やアクションを含むメニュー（ページ情報の表示と編集、ページプロパティの表示、ページの公開/非公開を含む）。

  ![ページ情報ボタン](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **エミュレーター**

  を切り替えます。 [エミュレーターツールバー](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate)：別のデバイスでのページのルックアンドフィールをエミュレートするために使用されます。 これは、レイアウトモードで自動的に切り替えられます。

  ![エミュレーターボタン](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

  [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md) を開きます。プレビューモードでのみ使用できます。

  ![ContextHub ボタン](/help/sites-cloud/authoring/assets/context-hub.png)

* **ページタイトル**

  これは単なる情報です。

  ![ページタイトル](/help/sites-cloud/authoring/assets/page-title.png)

* **モードセレクター**

  現在の [mode](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) また、編集、レイアウト、タイムワープ、ターゲット設定など、別のモードを選択することもできます。

  ![モードセレクターボタン](/help/sites-cloud/authoring/assets/mode-selector.png)

* **プレビュー**

  有効 [プレビューモード](#preview-mode). 公開時に表示されるページが表示されます。

  ![「プレビュー」ボタン](/help/sites-cloud/authoring/assets/preview.png)

* **注釈**

  次を追加できます： [注釈](/help/sites-cloud/authoring/fundamentals/annotations.md) をページに追加します。 最初の注釈の後、アイコンはページ上の注釈の数を示す番号に切り替わります。

  ![注釈ボタン](/help/sites-cloud/authoring/assets/annotations.png)

### ステータスの通知 {#status-notification}

ページが 1 つまたは複数の[ワークフロー](/help/sites-cloud/authoring/workflows/overview.md)の一部である場合、この情報はページの編集時に画面の上部にある通知バーに表示されます。

![ワークフロー通知](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>ステータスバーは、適切な特権を持つユーザーアカウントにのみ表示されます。

通知には、ページに対して実行されているワークフローが一覧表示されます。 ユーザーが現在のワークフローステップに関与している場合は、次のオプションを選択します。 [ワークフローのステータスに影響を与える](/help/sites-cloud/authoring/workflows/participating.md) また、ワークフローに関する詳細情報も次のように表示されます。

* **完了** - **作業項目を完了**&#x200B;ダイアログを開きます
* **委任** - **作業項目を完了**&#x200B;ダイアログを開きます
* **詳細を表示** - ワークフローの&#x200B;**詳細**&#x200B;ウィンドウを開きます

通知バーからのワークフローステップの完了および委任は、通知インボックスから[ワークフローに参加](/help/sites-cloud/authoring/workflows/participating.md)している場合に動作します。

ページが複数のワークフローの対象である場合は、ワークフローの数がワークフローをスクロールできる矢印ボタンと共に通知の右端に表示されます。

![複数のワークフロー通知](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## コンポーネントプレースホルダー {#component-placeholder}

コンポーネントプレースホルダーは、コンポーネントをドロップしたときの位置（現在カーソルを合わせているコンポーネントの上）を示すインジケーターです。

* 新しいコンポーネントをページに追加する場合（コンポーネントブラウザーからドラッグ）:

  ![ページに新しいコンポーネントを追加する際のプレースホルダー](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* 既存のコンポーネントを移動する場合：

  ![ページ上の既存のコンポーネントを移動する際のプレースホルダー](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## コンポーネントの挿入 {#inserting-a-component}

### コンポーネントブラウザーからのコンポーネントの挿入 {#inserting-a-component-from-the-components-browser}

新しいコンポーネントを追加するには、 [コンポーネントブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). この [コンポーネントプレースホルダー](#component-placeholder) コンポーネントの配置場所が表示されます。

1. ページが&#x200B;[**編集**&#x200B;モード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)であることを確認します。
1. [コンポーネントブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)を開きます。
1. 必要なコンポーネントを[必要な位置](#component-placeholder)までドラッグします。
1. コンポーネントを[編集](#edit-content)します。

>[!NOTE]
>
>モバイルデバイスでは、コンポーネントブラウザーが画面全体に表示されます。 コンポーネントのドラッグを開始すると、ブラウザーが閉じてページが再度表示され、コンポーネントを配置できます。

### 段落システムからのコンポーネントの挿入 {#inserting-a-component-from-the-paragraph-system}

段落システムの「**コンポーネントをここにドラッグ**」ボックスを使用して、新しいコンポーネントを追加できます。

1. ページが&#x200B;[**編集**&#x200B;モード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)であることを確認します。
1. 段落システムから新しいコンポーネントを選択して追加する方法は 2 つあります。

   * を選択します。 **コンポーネントを挿入** オプション (+) を既存のコンポーネントのツールバーまたは **ここにコンポーネントをドラッグ** ボックス

     ![コンポーネントの挿入](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * デスクトップデバイスを使用している場合は、「**コンポーネントをここにドラッグ**」ボックスをダブルクリックします。

   * **新規コンポーネントを挿入**&#x200B;ダイアログが表示され、必要なコンポーネントを選択できるようになります。

     ![新規コンポーネントを挿入ダイアログ](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. 選択したコンポーネントがページの下部に追加されます。 [編集](#edit-content) 必要に応じて、コンポーネントを選択します。

### アセットブラウザーを使用したコンポーネントの挿入 {#inserting-a-component-using-the-assets-browser}

また、ページに新しいコンポーネントを追加するには、 [アセットブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser). これにより、適切なタイプ（およびアセットを含む）の新しいコンポーネントが自動的に作成されます。

この動作は使用しているインストール環境で設定できます。詳しくは、「アセットをドラッグするとコンポーネントインスタンスが作成されるように段落システムを設定」を参照してください。<!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

前述のいずれかのアセットタイプをドラッグしてコンポーネントを作成するには：

1. ページが&#x200B;[**編集**&#x200B;モード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)であることを確認します。
1. を開きます。 [アセットブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
1. 必要なアセットを必要な位置までドラッグします。 この [コンポーネントプレースホルダー](#component-placeholder) コンポーネントの配置場所が表示されます。

   アセットタイプに適したコンポーネントが必要な場所に作成され、選択したアセットが格納されます。

1. [編集](#edit-content) 必要に応じて、コンポーネントを選択します。

>[!NOTE]
>
>モバイルデバイスでは、アセットブラウザーが画面全体に表示されます。 アセットのドラッグを開始すると、ブラウザーが閉じてページが再度表示され、アセットを配置できます。

アセットを参照したときに、アセットをすばやく変更する必要があることに気づいた場合は、 [アセットエディター](/help/assets/manage-digital-assets.md) ブラウザーから直接アセット名の横にある編集アイコンをクリックします。

![アセット編集ボタン](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## コンポーネントツールバー {#component-toolbar}

コンポーネントを選択すると、ツールバーが開きます。このツールバーからコンポーネントに対して様々なアクションを実行できます。

ユーザーが使用できる実際のアクションは、必要に応じて表示されます。ここでは、すべてのアクションについて説明するわけではありません。

![コンポーネントツールバー](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **編集**

  [コンポーネントタイプに応じて異なる](/help/sites-cloud/authoring/fundamentals/components.md)を設定すると、 [コンポーネントのコンテンツを編集](#edit-content). 多くの場合、ツールバーが用意されています。

  ![「編集」ボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **設定**

  [コンポーネントタイプに応じて異なる](/help/sites-cloud/authoring/fundamentals/components.md)を使用すると、コンポーネントのプロパティを編集および設定できます。 多くの場合、ダイアログが開きます。

  ![設定ボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-configure.png)

* **コピー**

  これにより、コンポーネントがクリップボードにコピーされます。 貼り付け操作の後も、元のコンポーネントは保持されます。

  ![コピーボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-copy.png)

* **切り取り**

  これにより、コンポーネントがクリップボードにコピーされます。 貼り付け操作の後、元のコンポーネントは削除されます。

  ![切り取りボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-cut.png)

* **削除**

  これにより、確認を含むページからコンポーネントが削除されます。

  ![削除ボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-delete.png)

* **コンポーネントの挿入**

  これにより、次のダイアログが開きます。 [新しいコンポーネントを追加](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system).

  ![挿入ボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-insert.png)

* **貼り付け**

  これにより、コンポーネントがクリップボードからページに貼り付けられます。 オリジナルが残るかどうかは、コピーを使用したか切り取ったかによって異なります。

   * 同じページまたは別のページに貼り付けることができます。
   * 貼り付けられた項目は、貼り付けアクションを選択した項目の上に貼り付けられます。
   * 貼り付けアクションは、クリップボードにコンテンツがある場合にのみ表示されます。

  ![貼り付けボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-paste.png)

  >[!NOTE]
  >
  >切り取り/コピー操作の前に開いていた別のページに貼り付ける場合は、ページを更新して、貼り付けたコンテンツを表示する必要があります。

* **グループ**

  これにより、複数のコンポーネントを一度に選択できます。 デスクトップデバイスで同じ操作をおこなうには、**Ctrl キーを押しながらクリック**&#x200B;するか、または **Command キーを押しながらクリック**&#x200B;します。

  ![グループボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **親**

  選択したコンポーネントの親コンポーネントを選択できます。

  ![親ボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **レイアウト**

  これにより、 [レイアウト](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout) 選択したコンポーネントの。 これは、選択したコンポーネントにのみ適用され、 [レイアウトモード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) ページ全体に対して

  ![レイアウトボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **エクスペリエンスフラグメントバリエーションに変換**

  これを使用すると、選択したコンポーネントから新しい[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)を作成したり、既存のエクスペリエンスフラグメントに追加したりできます。

  ![エクスペリエンスフラグメントへの変換ボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## コンテンツの編集 {#edit-content}

コンポーネント内のコンテンツを追加または編集するには、次の 2 つの方法があります。

* を開きます。 [編集用のコンポーネントダイアログ](#component-edit-dialog).
* [アセットをドラッグ&amp;ドロップ](#drag-and-drop-assets-into-component) アセットブラウザーからコンテンツを直接追加します。

### コンポーネント編集ダイアログ {#component-edit-dialog}

[コンポーネントツールバーの編集（鉛筆）アイコン](#component-toolbar)を使用して、コンポーネントを開いてコンテンツを編集できます。

正確な編集オプションは、コンポーネントによって異なります。一部のコンポーネントでは[全画面表示モードでのみすべてのアクションを使用できます](#edit-content-full-screen-mode)。次に例を示します。

* テキストコンポーネント

  ![テキストコンポーネントのツールバー](/help/sites-cloud/authoring/assets/editing-text-component-toolbar.png)

* 画像コンポーネント

  ![画像コンポーネントのツールバー](/help/sites-cloud/authoring/assets/editing-image-component-toolbar.png)

  >[!NOTE]
  >
  >編集は、空の画像コンポーネントでは動作しません。
  >
  >画像を編集するには、まず、画像をコンポーネントにドラッグまたはアップロードする必要があります。

* 画像コンポーネント — 全画面表示

  画像コンポーネント[の全画面表示モードに入ると](#edit-content-full-screen-mode)、画像を編集する領域が広くなり、追加の編集オプション（「**マップを起動**」や「**ズームをリセット**」など）が表示されます。また、全画面表示では切り抜きプリセットを選択できます。

  ![画像コンポーネントの全画面表示モード](/help/sites-cloud/authoring/assets/editing-image-component-full-screen.png)

* 複数の基本コンポーネントで構成されるコンポーネントでは、最初に、必要な編集オプションセットを確認するメッセージが表示されます。

### アセットのコンポーネントへのドラッグ＆ドロップ {#drag-and-drop-assets-into-component}

特定のコンポーネントタイプ（画像など）では、アセットをアセットブラウザーから直接コンポーネントにドラッグ＆ドロップして、コンテンツを更新することができます。

## 全画面表示モードでのコンテンツの編集 {#edit-content-full-screen-mode}

次のアイコンを使用して、すべてのコンポーネントで全画面表示モードにアクセス（または終了）できます。

![全画面表示ボタン](/help/sites-cloud/authoring/assets/editing-full-screen.png)

例えば、**テキスト**&#x200B;コンポーネントの場合は、次のように表示されます。

![全画面表示のテキストコンポーネント](/help/sites-cloud/authoring/assets/editing-text-full-screen.png)

>[!NOTE]
>
>一部のコンポーネントでは、全画面表示モードにすると、基本のインプレースエディターより多くのオプションが表示されます。

## コンポーネントの移動 {#moving-a-component}

段落コンポーネントを移動するには：

1. タップ&amp;ホールドまたはクリック&amp;ホールドで移動する段落を選択します。
1. 段落を新しい場所にドラッグします。 AEMは、段落を預ける場所を示します。 目的の場所にドロップします。

   ![コンポーネントの移動](/help/sites-cloud/authoring/assets/editing-moving-component.png)

1. 段落が移動します。

>[!TIP]
>
>[切り取りと貼り付け](#component-toolbar)を使用して、コンポーネントを移動することもできます。

## コンポーネントのレイアウトの編集 {#edit-component-layout}

コンポーネントを調整するために編集モードから[レイアウトモード](/help/sites-cloud/authoring/features/responsive-layout.md)に繰り返し切り替える代わりに、コンポーネントの&#x200B;**レイアウト**&#x200B;アクションを選択してそのコンポーネントのレイアウトを変更すると、編集モードから切り替える必要がなくなり、時間を節約できます。

1. サイトコンソールの&#x200B;**編集**&#x200B;モードでコンポーネントを選択すると、コンポーネントのツールバーが表示されます。

   ![ページコンポーネントのコンポーネントツールバー](/help/sites-cloud/authoring/assets/editing-layout-toolbar.png)

   コンポーネントのレイアウトを調整するには、**レイアウト**&#x200B;アクションをクリックまたはタップします。

   ![コンポーネントツールバーのレイアウトボタン](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

1. 「Layout」アクションを選択したら、次の操作を実行します。

   * コンポーネントのサイズ変更ハンドルが表示されます。
   * 画面の上部にエミュレーターツールバーが表示されます。
   * 標準の編集アクションの代わりにレイアウトアクションがコンポーネントツールバーに表示されます。

   ![レイアウトモードのコンポーネント](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   [レイアウトモード](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode)と同様に、コンポーネントのレイアウトを変更できるようになりました。

1. 必要なレイアウトの変更を加えて、コンポーネントのアクションメニューの「**閉じる**」ボタンをクリックすると、コンポーネントのレイアウトの変更が終わります。コンポーネントのツールバーは通常の編集状態に戻ります。

   ![ページコンポーネントのコンポーネントツールバー](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>レイアウトアクションは、選択したコンポーネントの範囲に限定されます。例えば、あるコンポーネントのレイアウトを編集してから別のコンポーネントをクリックすると、新しく選択したコンポーネントに（レイアウトツールバーではなく）標準の編集ツールバーが表示され、サイズ変更ハンドルとエミュレーターツールバーが表示されなくなります。
>
>複数のコンポーネントに影響するページの全体のレイアウトを編集する必要がある場合は、[レイアウトモード](/help/sites-cloud/authoring/features/responsive-layout.md)に切り替えます。

## 継承されたコンポーネント {#inherited-components}

継承とは、コンポーネントからコンポーネントへコンテンツを自動的にプッシュできるメカニズムです。継承されたコンポーネントは、次のような様々なシナリオによって生成されます。

* [マルチサイト管理](/help/sites-cloud/administering/msm/overview.md)
* [ローンチ](/help/sites-cloud/authoring/launches/overview.md)（ライブコピーをベースとしている場合）

継承はキャンセル（その後再度有効化）できます。ライブコピーまたは（ライブコピーに基づいた）ローンチの一部であるページにコンポーネントがある場合は、コンポーネントに応じて、コンポーネントツールバーからこの機能を使用できます。

![継承関係を示すコンポーネントツールバー](/help/sites-cloud/authoring/assets/editing-component-toolbar-inheritance.png)

次に例を示します。

* 継承をキャンセル

  ![継承のキャンセルボタン](/help/sites-cloud/authoring/assets/editing-cancel-inheritance.png)

* 継承を再度有効にする（既に継承がキャンセルされている場合）

  ![継承再有効化ボタン](/help/sites-cloud/authoring/assets/editing-reenable-inheritance.png)

* ブループリントまたはライブコピーのソースでは、ロールアウトアクションも使用できます。

  ![ロールアウトボタン](/help/sites-cloud/authoring/assets/editing-rollout.png)

## ページテンプレートの編集 {#editing-the-page-template}

[ページ情報メニュー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information)で「**テンプレートを編集**」を選択すると、[テンプレートエディター](/help/sites-cloud/authoring/features/templates.md#editing-templates-template-authors)に容易に切り替えることができます。

[列表示](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)または[リスト表示](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)でページを選択するときに、ページが基にしているテンプレートを簡単に確認できます。

## ライブコピーステータス {#live-copy-status}

この [ライブコピーステータスページモード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) ライブコピーのステータスと継承される（または継承されない）コンポーネントの概要を簡単に確認できます。

* 緑の境界線：継承
* ピンクの境界線：継承がキャンセルされました

次に例を示します。

![ライブコピーステータスの表示例](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## 注釈の追加 {#adding-annotations}

[注釈](/help/sites-cloud/authoring/fundamentals/annotations.md) レビュー担当者や他の作成者がコンテンツに関するフィードバックを提供することを許可します。 多くの場合、レビューや検証の目的で使用されます。

## ページのプレビュー {#previewing-pages}

ページをプレビューするには、以下の 2 つの方法があります。

* [プレビューモード](#preview-mode) - その場ですばやく確認できるプレビュー
* [公開済みとして表示](#view-as-published)  — ページを新しいタブで開く完全なプレビュー

>[!TIP]
>
>* コンテンツ内のリンクは表示されますが、編集モードではアクセスできません。
>* リンクを使用して移動する場合には、いずれかのプレビューオプションを使用してください。
>* プレビューと最後に選択したモードを切り替えるには、[キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M` を使用します。

>[!NOTE]
>
>両方のプレビューオプションに WCM Mode Cookie が設定されています。

### プレビューモード {#preview-mode}

コンテンツの編集時に、プレビューを使用してページをプレビューできます [mode](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes). このモード：

* 各種編集メカニズムを非表示にして公開時にページがどのように表示されるかをすばやく確認できます。
* リンクを使用して移動できます。
* 実行 **not** ページコンテンツを更新します。

オーサリング時には、ページエディターの右上にある次のアイコンを使用してプレビューモードを使用できます。

![「プレビュー」ボタン](/help/sites-cloud/authoring/assets/preview.png)

### 公開済みとして表示 {#view-as-published}

この **公開済みとして表示** オプションは、 [ページ情報](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) メニュー これにより、新しいタブでページが開き、コンテンツが更新され、ページがパブリッシュ環境で表示されるとおりに表示されます。

## ページのロック {#locking-a-page}

AEM では、他のユーザーによるコンテンツの変更を防ぐためにページをロックすることができます。ページのロックは、1 つの特定のページで大量の編集作業をおこなう場合や、短期間ページを凍結する必要がある場合に便利です。

ページは次のいずれかからロックできます。

* **サイト** コンソール

   1. を含むページを選択します。 [選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
   1. ロックアイコンを選択します。

      ![「ロック」ボタン](/help/sites-cloud/authoring/assets/lock.png)

* **ページエディター**

   1. を選択します。 **ページ情報** アイコンをクリックしてメニューを開きます。
   1. を選択します。 **ページをロック** オプション。

ロックすると、コンソール表示の情報が更新され、編集時にロック記号がツールバーに表示されます。

![ロックされたページの例](/help/sites-cloud/authoring/assets/editing-locked-page.png)

>[!CAUTION]
>
>ページのロックは、別のユーザーとして実行している場合にも実行できます。ただし、この方法でロックされたページを（顧客によって）ロック解除できるのは、別のユーザーとして実行したユーザーのみです。
>
>実際にページのロック作業を行なったユーザーに成り代わっても、ページをロック解除できません。
>
>ページをロックしたユーザーが（居ないため）ページのロックを解除できない場合は、カスタマー サポートに連絡して、ロックを解除するオプションを評価してください。

## ページのロック解除 {#unlocking-a-page}

ページのロック解除は、[ページのロック](#locking-a-page)とよく似ています。ページがロックされると、ロックオプションはロック解除アクションに置き換えられます。

ページ情報メニューには「**ロック解除**」がオプションとして表示され、サイトコンソールのロックアイコンは「**ロック解除**」アイコンに置き換えられます。

![ロック解除ボタン](/help/sites-cloud/authoring/assets/unlock.png)

>[!CAUTION]
>
>ページのロックは、別のユーザーとして実行している場合にも実行できます。ただし、別のユーザーに成り代わって実行したユーザーのみが、この方法でロックされたページをロック解除することができます。
>
>実際にページのロック作業を行なったユーザーに成り代わっても、ページをロック解除できません。
>
>ページをロックしたユーザーが（居ないため）ページのロックを解除できない場合は、カスタマー サポートに連絡して、ロックを解除するオプションを評価してください。

<!--
>[!CAUTION]
>
>Locking a page can be performed when impersonating a user. However a page locked in this way can only then be unlocked by the user who was impersonated, or by a user with admin rights (a member of AEM Administrator IMS profile).
>
>Pages can not be unlocked by impersonating the user who locked the page.
-->

<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## ページ編集の取り消しとやり直し {#undoing-and-redoing-page-edits}

次のアイコンを使用して、アクションの取り消しまたはやり直しを行うことができます。これらのアイコンは、ツールバーに適宜表示されます。

![取り消しボタンとやり直しボタン](/help/sites-cloud/authoring/assets/redo.png)

>[!TIP]
>
>* [キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Z` を使用して、ページの編集アクションを取り消すこともできます。
>* キーボードショートカット `Ctrl-Y` を使用して、ページの編集アクションをやり直すこともできます。

>[!NOTE]
>
>ページ編集の取り消しとやり直しによって実行可能なことについて詳しくは、[ページ編集の取り消しとやり直し - 理論](#undoing-and-redoing-page-edits-the-theory)を参照してください。

## ページ編集の取り消しとやり直し - 理論 {#undoing-and-redoing-page-edits-the-theory}

AEM では、ユーザーが実行するアクションの履歴と、それらのアクションを実行した順序が保存されます。そのため、複数のアクションの取り消しは、ユーザーが実行した順序でおこなうことができます。その後、必要に応じて、やり直しを使用して 1 つ以上のアクションを再適用することもできます。

コンテンツページで要素（テキストコンポーネントなど）が選択されている場合、取り消しコマンドとやり直しコマンドは選択した項目に適用されます。

取り消しコマンドとやり直しコマンドの動作は、他のソフトウェアの場合と同様です。これらのコマンドを使用すると、コンテンツに関する決定をおこなう中で、Web ページの最新の状態に復元できます。例えば、テキスト段落をページ上の別の場所に移動した場合に、取り消しコマンドを使用して、その段落を元の場所に戻すことができます。その後、前の位置の方が良いと判断した場合は、やり直しコマンドを使用して「元に戻す」操作を元に戻します。

例えば、次のことができます。

* 取り消しを使用してからページの編集を行っていない限り、操作をやり直します。
* 最大 20 個の編集アクションを取り消します（デフォルト設定）。
* また、 [キーボードショートカット](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) 元に戻す/やり直しの場合。

取り消しとやり直しは、次のタイプのページの変更に対して使用できます。

* 段落の追加、編集、削除および移動
* 段落コンテンツのインプレース編集
* ページ内の項目のコピー、切り取り、貼り付け

>[!NOTE]
>
>* ファイルと画像に対する変更の取り消しおよびやり直しには、特別な権限が必要になります。
>* ファイルおよび画像に対する変更の履歴は、少なくとも 10 時間保持されます。 ただし、これ以降は、変更の取り消しは保証されません。 管理者は、デフォルトの 10 時間を変更できます。
>* システム管理者は、インスタンスの要件に従って取り消しおよびやり直し機能の様々な面を設定できます。
<!--* Your system administrator can [configure various aspects of the Undo/Redo features](/help/sites-administering/config-undo.md) according to the requirements for your instance.-->
