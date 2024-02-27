---
title: AEM Page Editor
description: AEMページエディターは、コンテンツをオーサリングするための強力なツールです。
source-git-commit: 91ce6a0c880436327f4dd333a2eb3d36a4e89a4d
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 42%

---


# AEM Page Editor {#editing-page-content}

ページが [**Sites** コンソール](/help/sites-cloud/authoring/sites-console/introduction.md) AEMページエディターを使用してページのコンテンツを編集できます。これは、コンテンツをオーサリングするための強力なツールです。

>[!NOTE]
>
>ページの編集時 ( [**Sites** コンソール](/help/sites-cloud/authoring/sites-console/introduction.md) コンソールで、ページの [テンプレート：](/help/sites-cloud/authoring/sites-console/templates.md) このドキュメントで説明するページエディター、または [ユニバーサルエディター。](/help/sites-cloud/authoring/universal-editor/authoring.md)

>[!NOTE]
>
>ページを編集するための適切なアクセス権と権限がアカウントに必要です。 権限がない場合は、システム管理者に問い合わせてください。

## 向き {#orientation}

AEMのページエディターは、主に次の 3 つのセクションで構成されます。

1. [ツールバー](#toolbar)  — ツールバーを使用すると、ページモードをすばやく変更したり、追加のページ設定にアクセスしたりできます。
1. [サイドパネル](#side-panel)  — サイドパネルでは、ページコンポーネントやアセット、その他のオーサリングツールにアクセスできます。
1. [エディター](#editor)  — エディターでは、コンテンツを変更してプレビューできます。

![ページエディターのレイアウト](assets/page-editor-layout.png)

コンテンツは、ページにドラッグ可能な[コンポーネント](/help/sites-cloud/authoring/components-console.md)（コンテンツのタイプに適したもの）を使用して追加できます。コンポーネントはその後、そのまま編集したり、移動や削除をおこなったりすることができます。

### ツールバー {#page-toolbar}

ページツールバーを使用すると、ページ設定に応じて、コンテキストに応じた機能にアクセスできます。

![ページエディターのツールバー](assets/page-editor-toolbar.png)

#### サイドパネル {#side-panel-button}

これにより、 [サイドパネル](/help/sites-cloud/authoring/page-editor/editor-side-panel.md) このツリーには、アセットブラウザ、コンポーネントブラウザ、コンテンツツリーが含まれます。

![サイドパネルの切り替え](assets/page-editor-side-panel-toggle.png)

#### ページ情報 {#page-information}

これにより、ページの詳細や、ページ情報の表示および編集、ページプロパティの表示、ページの公開/非公開など、ページで実行できるアクションを含む詳細なページ情報にアクセスできます。

![ページ情報ボタン](assets/page-editor-page-information-icon.png)

**ページ情報** ドロップダウンメニューを開き、選択したページの最後の編集および最後の公開に関する詳細を表示します。 ページ、そのページのサイト、インスタンスの特性に応じて、追加のアクションを使用できます。

* [プロパティを開く](/help/sites-cloud/authoring/sites-console/page-properties.md)
* [ページをロールアウト](/help/sites-cloud/administering/msm/overview.md#msm-from-the-ui)
* [ワークフローを開始](/help/sites-cloud/authoring/workflows/applying.md#starting-a-workflow-from-the-page-editor)
* [ページをロック](/help/sites-cloud/authoring/page-editor/introduction.md#locking-unlocking)
* [ページを公開](/help/sites-cloud/authoring/sites-console/publishing-pages.md#publishing-pages-1)
* [ページを非公開](/help/sites-cloud/authoring/sites-console/publishing-pages.md#unpublishing-pages)
* [テンプレートを編集](/help/sites-cloud/authoring/sites-console/templates.md)
* [公開済みとして表示](/help/sites-cloud/authoring/page-editor/introduction.md#view-as-published)
* [管理画面で表示](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)
* [ヘルプ](/help/sites-cloud/authoring/basic-handling.md#accessing-help)
* [ローンチを昇格](/help/sites-cloud/authoring/launches/promoting.md)（ページがローンチの場合のみ）

該当する場合、**ページ情報**&#x200B;から分析やレコメンデーションを確認することもできます。

#### エミュレーター {#emulator}

これにより、 [エミュレーターツールバー](/help/sites-cloud/authoring/page-editor/responsive-layout.md#selecting-a-device-to-emulate)：別のデバイスでのページのルックアンドフィールをエミュレートするために使用されます。 これは、レイアウトモードで自動的に有効になります。

![エミュレーターボタン](assets/page-editor-emulator.png)

#### ContextHub {#context-hub}

これにより、 [ContextHub です。](/help/sites-cloud/authoring/personalization/contexthub.md) 次でのみ使用できます。 **プレビュー** モード。

![ContextHub ボタン](assets/page-editor-context-hub.png)

#### ページタイトル {#page-title}

これはページのタイトルで、大文字で情報としてレンダリングされます。

![ページタイトル](assets/page-editor-page-title.png)

#### モードセレクター {#mode-selector}

モードセレクターに現在の [mode](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector) 「 」では、編集、レイアウト、タイムワープ、ターゲット設定など、別のモードを選択できます。

![モードセレクターボタン](assets/page-editor-mode-selector.png)

ページの編集時には様々なモードがあり、異なるアクションを行うことができます。

* [編集](/help/sites-cloud/authoring/page-editor/edit-content.md)  — ページコンテンツの編集時に使用するモード
* [レイアウト](/help/sites-cloud/authoring/page-editor/responsive-layout.md)  — デバイスに応じたレスポンシブレイアウトを作成および編集できます（ページがレイアウトコンテナに基づいている場合）
* [ターゲット設定](/help/sites-cloud/authoring/personalization/targeted-content.md)  — すべてのチャネルでのターゲティングと測定を通じてコンテンツの関連性を高めます
* [タイムワープ](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp)  — 特定の時点でのページの状態の表示
* [ライブコピーステータス](/help/sites-cloud/authoring/page-editor/introduction.md#live-copy-status)  — ライブコピーのステータスと継承される（または継承されない）コンポーネントの概要をすばやく確認できます
* [開発者モード](/help/implementing/developing/tools/developer-mode.md)
* [プレビュー](/help/sites-cloud/authoring/page-editor/introduction.md#previewing-pages)  — パブリッシュ環境で表示されるようにページを表示する、またはコンテンツ内のリンクを使用して移動する
* [注釈](/help/sites-cloud/authoring/page-editor/annotations.md)  — ページで注釈を追加または表示する

>[!NOTE]
>
>* ページの特性によっては、一部のモードを使用できない場合があります。
>* 一部のモードにアクセスするには、適切な権限または特権が必要です。
>* モバイルデバイスでは、スペースの制約により、開発者モードを使用できません。
>* [キーボードショートカット](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)（`Ctrl-Shift-M`）で、**プレビュー**&#x200B;と、現在選択されているモード（**編集モード**、**レイアウトモード**&#x200B;など）を切り替えることができます。

#### プレビュー {#preview}

The **プレビュー** ボタンを有効にする [プレビューモード。](#preview-mode)：公開時に表示されるページを表示します。

![「プレビュー」ボタン](assets/page-editor-preview.png)

#### 注釈 {#annotate}

**注釈** モードを使用すると、 [注釈](/help/sites-cloud/authoring/page-editor/annotations.md) をページに追加します。 最初の注釈を追加後、アイコンは、ページ上の注釈の数を示す数字に切り替わります。

![注釈ボタン](assets/page-editor-annotations.png)

### サイドパネル {#side-panel}

サイドパネルから、3 つの異なるタブにアクセスできます。

* ページに新しいコンテンツを追加するためのコンポーネントブラウザー
* ページに新しいアセットを追加するためのアセットブラウザー
* ページの構造を参照するコンテンツツリー

![ページエディターのサイドパネル](assets/page-editor-side-panel.png)

ドキュメントを参照してください [ページエディターのサイドパネル](/help/sites-cloud/authoring/page-editor/editor-side-panel.md) を参照してください。

### 編集者 {#editor}

エディターでは、ページコンテンツを直接変更できます。 ページは表示されるとおりにレンダリングされ、サイドパネルのアセットまたはコンポーネントブラウザーを使用して新しいコンテンツをドラッグ&amp;ドロップし、コンテンツをインプレースで編集できます。

![ページエディターのエディター](assets/page-editor-editor.png)

## コンテンツの編集 {#editing-content}

これで、ページエディターを理解したので、コンテンツを編集する準備が整いました。

ドキュメントを参照してください [AEM Page Editor を使用したコンテンツの編集](/help/sites-cloud/authoring/page-editor/edit-content.md) を参照してください。

## ステータスの通知 {#status-notification}

ページが [workflow](/help/sites-cloud/authoring/workflows/overview.md) 複数のワークフローに関しては、この情報は、ページの編集時にツールバーの下の通知バーに表示されます。

![ワークフロー通知](assets/page-editor-editing-workflow-notification.png)

>[!NOTE]
>
>ステータスバーは、適切な特権を持つユーザーアカウントにのみ表示されます。

通知には、ページに対して実行されているワークフローが一覧表示されます。ユーザーが現在のワークフローステップに関係している場合は、[ワークフローのステータスに影響する](/help/sites-cloud/authoring/workflows/participating.md)オプションや、ワークフローの詳細を取得するオプションを使用できます。例えば、次のようなものがあります。

* **完了** - **作業項目を完了**&#x200B;ダイアログを開きます
* **委任** - **作業項目を完了**&#x200B;ダイアログを開きます
* **詳細を表示** - ワークフローの&#x200B;**詳細**&#x200B;ウィンドウを開きます

通知バーからのワークフローステップの完了および委任は、通知インボックスから[ワークフローに参加](/help/sites-cloud/authoring/workflows/participating.md)している場合に動作します。

ページが複数のワークフローの対象である場合は、ワークフローの数がワークフローをスクロールできる矢印ボタンと共に通知の右端に表示されます。

![複数のワークフロー通知](assets/page-editor-editing-workflow-notification-multiple.png)

## ライブコピーステータス {#live-copy-status}

The **ライブコピーステータス** ページモードでは、ライブコピーのステータスと継承される（または継承されない）コンポーネントの概要をすばやく確認できます。

* 緑のボーダー：継承
* ピンクのボーダー：継承がキャンセルされている

次に例を示します。

![ライブコピーステータスの表示例](assets/page-editor-editing-live-copy-status.png)

## ページのプレビュー {#previewing-pages}

ページをプレビューするには、以下の 2 つの方法があります。

* [プレビューモード](#preview-mode)  — その場ですばやく確認できるプレビュー
* [公開済みとして表示](#view-as-published)  — 新しいタブでページを開く完全なプレビュー

>[!TIP]
>
>* コンテンツ内のリンクは表示されますが、次の場所ではアクセスできません： **編集** モード。
>* リンクを使用して移動する場合には、いずれかのプレビューオプションを使用してください。
>* プレビューと最後に選択したモードを切り替えるには、[キーボードショートカット](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) `Ctrl-Shift-M` を使用します。

>[!NOTE]
>
>両方のプレビューオプションに WCM Mode Cookie が設定されています。

### プレビューモード {#preview-mode}

コンテンツの編集時に、プレビューモードを使用してページをプレビューできます。 このモードでは、次の操作を実行できます。

* 各種編集メカニズムを非表示にして公開時にページがどのように表示されるかをすばやく確認できます。
* リンクを使用して移動できます。
* ページコンテンツは更新&#x200B;**されません**。

オーサリング時に、ページエディターの右上にある次のアイコンを使用してプレビューモードを使用できます。

![「プレビュー」ボタン](assets/page-editor-preview.png)

### 公開済みとして表示 {#view-as-published}

「**公開済みとして表示**」オプションは、[ページ情報](#page-information)メニューで使用できます。ページが新しいタブで開き、コンテンツが更新され、ページがパブリッシュ環境で表示されるとおりに表示されます。

## ページのロックとロック解除 {#locking-unlocking}

AEMを使用すると、他のユーザーがコンテンツを編集できないようにページをロックできます。 ロックは、1 つの特定のページに多数の編集を加える場合や、短時間ページを固定する必要がある場合に便利です。

1. **ページ情報**&#x200B;アイコンを選択して、メニューを開きます。
1. 「**ページをロック**」オプションを選択します。

ロックすると、ページエディターのツールバーにロック記号が表示されます。

![ロックされたページの例](assets/page-editor-editing-locked-page.png)

ページのロック解除は、 [ページのロック](#locking-a-page). ページがロックされると、ロックオプションはロック解除アクションに置き換えられます。

>[!CAUTION]
>
>* ページのロックは、別のユーザーとして実行している場合にも実行できます。ただし、別のユーザーに成り代わって実行したユーザーのみが、この方法でロックされたページをロック解除することができます。
>* 実際にページのロック作業を行なったユーザーに成り代わっても、ページをロック解除できません。
>* ページをロックしたユーザーが（対応できないため）ページのロックを解除できない場合は、カスタマーサポートに連絡して、ロックを解除するオプションを評価してください。

## ページ編集の取り消しとやり直し {#undoing-and-redoing-page-edits}

次のアイコンを使用して、アクションの取り消しまたはやり直しを行うことができます。これらのアイコンは、ツールバーに適宜表示されます。

![取り消しボタンとやり直しボタン](assets/page-editor-redo.png)

>[!TIP]
>
>* [キーボードショートカット](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) `Ctrl-Z` を使用して、ページの編集アクションを取り消すこともできます。
>* キーボードショートカット `Ctrl-Y` を使用して、ページの編集アクションをやり直すこともできます。

>[!NOTE]
>
>ドキュメントを参照してください [取り消しとやり直しの制限](/help/sites-cloud/authoring/page-editor/undo-redo.md) ページ編集の取り消しとやり直しによって実行できることの詳細。
