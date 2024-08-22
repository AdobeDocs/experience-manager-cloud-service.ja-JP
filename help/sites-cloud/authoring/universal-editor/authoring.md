---
title: ユニバーサルエディターを使用したコンテンツのオーサリング
description: コンテンツ作成者がユニバーサルエディターを使用してコンテンツを作成する際に、簡単で直感的な方法を説明します。
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: eecbc48a77e92b064be9fcdbe547fb330f8d40e0
workflow-type: ht
source-wordcount: '1297'
ht-degree: 100%

---


# ユニバーサルエディターを使用したコンテンツのオーサリング {#authoring}

コンテンツ作成者がユニバーサルエディターを使用してコンテンツを作成する際に、簡単で直感的な方法を説明します。

## はじめに {#introduction}

ユニバーサルエディターを使用すると、あらゆる実装、あらゆるコンテンツ、あらゆる側面を編集できるため、優れたエクスペリエンスを提供し、コンテンツベロシティを向上させ、最新のデベロッパーエクスペリエンスを提供できます。

これを行うために、ユニバーサルエディターはコンテンツ作成者に、最小限のトレーニングで簡単にコンテンツの編集を開始できる直感的な UI を提供します。このドキュメントでは、ユニバーサルエディターのオーサリングエクスペリエンスについて説明します。

>[!NOTE]
>
>このドキュメントは、ユニバーサルエディターへのアクセスと操作の方法を、ユーザーが既に理解していることを前提としています。そうでない場合は、[ユニバーサルエディターへのアクセスと操作](/help/sites-cloud/authoring/universal-editor/navigation.md)ドキュメントを参照してください。

>[!TIP]
>
>ユニバーサルエディターについて詳しくは、[ユニバーサルエディターの概要](/help/implementing/universal-editor/introduction.md)ドキュメントを参照してください。

## コンテンツの編集 {#editing-content}

コンテンツの編集はシンプルで直感的です。エディターでコンテンツにマウスカーソルを重ねると、編集可能なコンテンツが薄い青色のアウトラインでハイライト表示されます。

![編集可能コンテンツが青いボックスでハイライト表示される](assets/editable-content.png)

>[!TIP]
>
>デフォルトでは、コンテンツをタップまたはクリックすると、そのコンテンツが編集用に選択されます。リンクをたどってコンテンツを移動する場合は、[プレビューモード](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode)に切り替えます。

選択したコンテンツに応じて、異なるインプレース編集オプションが設定されている場合や、[プロパティパネル](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)にコンテンツの追加情報やオプションが表示される場合があります。

### プレーンテキストの編集 {#edit-plain-text}

コンポーネントをダブルクリックまたはダブルタップすると、その場でテキストを編集できます。

![コンテンツを編集](assets/editing-content.png)

薄い青色のアウトラインは、選択を示す濃い青色のアウトラインに変わり、カーソルが表示されます。変更を行ったら、Enter キーまたは Return キーを押すか、テキストボックスの外側を選択して、変更を保存します。

テキストコンポーネントを選択すると、その詳細がプロパティパネルに表示されます。[](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)パネル内のテキストを編集することもできます。

![プロパティパネルでのテキストの編集](assets/ue-editing-text-component-rail.png)

また、テキストの詳細はプロパティパネルで確認できます。フォーカスがプロパティパネルの編集されたフィールドを離れると、変更は自動的に保存されます。

### リッチテキストの編集 {#edit-rich-text}

コンポーネントをダブルクリックまたはダブルタップすると、その場でテキストを編集できます。

![リッチテキストコンポーネントの編集](assets/rich-text-editing.png)

利便性のために、テキストの書式設定オプションと詳細は、2 か所で利用できます。

#### コンテキストメニュー {#context-menu}

コンテキストメニューは、リッチテキストブロック上で開き、コンテキスト内の基本的な書式設定オプションを提供します。スペースの都合上、一部のオプションが省略記号ボタンの後ろに隠れている場合があります。

![リッチテキストコンテキストメニュー](assets/rich-text-context-menu.png)

編集されたフィールドからフォーカスが離れると、変更は自動的に保存されます。

#### プロパティパネル {#properties-rail}

[プロパティパネル](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)には、選択したテキストの項目が表示されます。エントリをタップすると、テキストを編集するための大きいキャンバスを表示するダイアログが開きます。

![リッチテキスト編集ダイアログ](assets/rich-text-canvas.png)

変更を破棄または保存するには、それぞれ「**キャンセル**」または「**完了**」をタップまたはクリックします。

### メディアの編集 {#edit-media}

詳細は、[プロパティパネル](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)で確認できます。

![メディアの編集](assets/ue-edit-media.png)

1. プロパティパネルで、選択した画像のプレビューをタップまたはクリックします。
1. [アセットセレクター](/help/assets/asset-selector.md#using-asset-selector)ウィンドウが開き、アセットを選択できます。
1. 選択して、新しいアセットを選択します。
1. 「**選択**」を選択して、アセットが置き換えられたプロパティパネルに戻ります。

変更はコンテンツに自動的に保存されます。

### コンテンツフラグメントの編集 {#edit-content-fragment}

[コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/overview.md)を選択した場合、詳細は、[プロパティパネル](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)で編集できます。

![コンテンツフラグメントの編集](assets/ue-edit-cf.png)

選択したコンテンツフラグメントのコンテンツモデルで定義されたフィールドが、プロパティパネルに表示され編集可能になります。

コンテンツフラグメントに関連するフィールドを選択した場合、コンポーネントパネルにコンテンツフラグメントが読み込まれ、フィールドが自動的にスクロールされます。

フォーカスがプロパティパネルの編集されたフィールドを離れると、変更は自動的に保存されます。

代わりにコンテンツフラグメントを[コンテンツフラグメントエディター](/help/sites-cloud/administering/content-fragments/authoring.md)で編集する場合は、プロパティパネルの [**CF エディターで開く**&#x200B;ボタン](/help/sites-cloud/authoring/universal-editor/navigation.md#edit)をタップまたはクリックします。

>[!TIP]
>
>コンテンツフラグメントエディターで選択したコンテンツフラグメントを編集するには、ホットキー `e` を使用します。

ワークフローのニーズに応じて、コンテンツフラグメントをユニバーサルエディターで編集することも、コンテンツフラグメントエディターで直接編集することもできます。

>[!NOTE]
>
>ユニバーサルエディターでは、[モデルに基づいてコンテンツフラグメントフィールドを検証](/help/assets/content-fragments/content-fragments-models.md#validation)し、正規表現パターンや一意性制約などのデータ整合性ルールを適用できます。
>
>これにより、コンテンツを公開する前に、特定のビジネス要件が満たされます。

### コンテナへのコンポーネントの追加 {#adding-components}

1. [コンテンツツリー](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)またはエディターでコンテナコンポーネントを選択します。
1. 次に、プロパティパネルで追加アイコンを選択します。

   ![コンテナに追加するコンポーネントの選択](assets/ue-add-component.png)

コンポーネントがコンテナに挿入され、エディターで編集できます。

>[!TIP]
>
>ホットキー `a` を使用して、選択したコンテナにコンポーネントを追加します。

### コンテナからのコンポーネントの削除 {#deleting-components}

1. [コンテンツツリー](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)またはエディターでコンテナコンポーネントを選択します。
1. コンテナの山形アイコンを選択して、コンテンツツリーでコンテンツを展開します。
1. 次に、コンテンツツリーで、コンテナ内のコンポーネントを選択します。
1. プロパティパネルで削除アイコンを選択します。

   ![コンポーネントの削除](assets/ue-delete-component.png)

選択したコンポーネントが削除されました。

>[!TIP]
>
>ホットキー `Shift+Backspace` を使用して、選択したコンポーネントをコンテナから削除します。

### コンテナ内のコンポーネントの並べ替え {#reordering-components}

1. [コンテンツツリーモード](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)でない場合はそれに切り替えます。
1. コンテンツツリーまたはエディターでコンテナコンポーネントを選択します。
1. コンテナの山形アイコンを選択して、コンテンツツリーでコンテンツを展開します。
1. コンテナ内のコンポーネントの横にあるハンドルアイコンをドラッグすると、それらを並べ替えることができます。コンポーネントをドラッグして、コンテナ内で並べ替えます。

   ![コンポーネントの並べ替え](assets/ue-reordering-components.png)

1. ドラッグしたコンポーネントがコンテンツツリー内で灰色に変わり、挿入ポイントは青い線で表されます。コンポーネントをリリースして、新しい場所に配置します。

コンポーネントは、コンテンツツリーおよびエディターの両方で並べ替えられます

## コンテンツのプレビュー {#previewing-content}

コンテンツの編集が完了したら、他のページのコンテンツでコンテンツがどのように表示されるかを確認するためにコンテンツ内を移動したい場合がよくあります。[プレビューモード](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode)でリンクをクリックして、読者と同じようにコンテンツ内を移動できます。コンテンツは、公開されるときと同じように、エディターでレンダリングされます。

プレビューモードでは、コンテンツをタップまたはクリックすると、コンテンツの読者に対するように反応します。編集するコンテンツを選択する場合は、[プレビューモード](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode)から切り替えます。

## その他のリソース {#additional-resources}

ユニバーサルエディターを使用してコンテンツを公開する方法については、このドキュメントを参照してください。

* [ユニバーサルエディターを使用したコンテンツの公開](publishing.md) - ユニバーサルエディターでのコンテンツの公開方法と、アプリでの公開済みコンテンツの処理方法について説明します。

ユニバーサルエディターの技術的な詳細について詳しくは、次の開発者向けドキュメントを参照してください。

* [ユニバーサルエディターの概要](/help/implementing/universal-editor/introduction.md) - ユニバーサルエディターを使用して、優れたエクスペリエンスを提供し、コンテンツベロシティを向上させ、最新のデベロッパーエクスペリエンスを提供するために、あらゆる実装、あらゆるコンテンツ、あらゆる側面の編集を可能にする方法を説明します。
* [AEM のユニバーサルエディターの概要](/help/implementing/universal-editor/getting-started.md) - ユニバーサルエディターへのアクセス権を取得する方法と、これを使用するために最初の AEM アプリのインストルメントを開始する方法について説明します。
* [ユニバーサルエディターのアーキテクチャ](/help/implementing/universal-editor/architecture.md) - ユニバーサルエディターのアーキテクチャと、そのサービスとレイヤー間でのデータのフローについて説明します。
* [属性とタイプ](/help/implementing/universal-editor/attributes-types.md) - ユニバーサルエディターで必要なデータ属性とデータ型について説明します。
* [ユニバーサルエディターの認証](/help/implementing/universal-editor/authentication.md) - ユニバーサルエディターの認証方法について説明します。

## コンポーネントの継承の編集 {#inheritance}

継承とは、一方を変更するともう一方も自動的に変更されるようにコンテンツをリンクできるメカニズムです。

ユニバーサルエディターを使用すると、コンテンツを更新するだけで、コンテンツの継承をキャンセルできます。エディターでは、そのページの作成者が行ったすべての変更の継承を自動的に無効にし、ブループリントから更新を同期した際に変更済みのコンテンツが保持されるようにします。

ユニバーサルエディターを使用した継承の仕組みについて詳しくは、[ユニバーサルエディターでのコンテンツの継承](/help/sites-cloud/authoring/universal-editor/inheritance.md)ドキュメントを参照してください。
