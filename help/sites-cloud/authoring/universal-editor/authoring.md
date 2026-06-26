---
title: ユニバーサルエディターを使用したコンテンツのオーサリング
description: コンテンツ作成者がユニバーサルエディターを使用してコンテンツを作成する際に、簡単で直感的な方法を説明します。
badgeSaas: label="AEM Sites" type="Positive" tooltip="AEM Sitesに適用）。"
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 152b867e74ac87763f7249fa7e50986b257736b3
workflow-type: tm+mt
source-wordcount: '3165'
ht-degree: 63%

---


# ユニバーサルエディターを使用したコンテンツのオーサリング {#authoring}

コンテンツ作成者がユニバーサルエディターを使用してコンテンツを作成する際に、簡単で直感的な方法を説明します。

## はじめに {#introduction}

ユニバーサルエディターを使用すると、実装におけるあらゆるコンテンツの様々な側面を編集できるので、優れたエクスペリエンスを提供し、コンテンツベロシティを向上させることができます。

これを行うために、ユニバーサルエディターはコンテンツ作成者に、最小限のトレーニングで簡単にコンテンツの編集を開始できる直感的な UI を提供します。 このドキュメントでは、ユニバーサルエディターのオーサリングエクスペリエンスについて説明します。

>[!NOTE]
>
>このドキュメントは、ユニバーサルエディターへのアクセスと操作の方法を、ユーザーが既に理解していることを前提としています。 まだの場合は、[&#x200B; ユニバーサルエディターへのアクセスとナビゲーション &#x200B;](/help/sites-cloud/authoring/universal-editor/navigation.md)を参照してください。

>[!TIP]
>
>ユニバーサルエディターの詳細については、[&#x200B; ユニバーサルエディターの概要を参照してください。](/help/implementing/universal-editor/introduction.md)

## コンテンツの編集 {#editing-content}

コンテンツの編集はシンプルで直感的です。 エディターでコンテンツにマウスポインターを置くと、編集可能なコンテンツが、薄い水色のアウトラインとバッジでハイライト表示されます。

![編集可能なコンテンツは、明るい青のボックスで強調表示されます](assets/editable-content.png)

ハイライト表示されたコンテンツをタップまたはクリックすると、薄い水色のアウトラインが濃い青色のアウトラインになり、バッジが表示されます。

![選択したコンテンツは、濃い青色のボックスで強調表示されます](assets/selected-content.png)

>[!TIP]
>
>デフォルトでは、コンテンツをタップまたはクリックすると、そのコンテンツが編集用に選択されます。 リンクをたどってコンテンツを移動する場合は、[プレビューモード](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode)に切り替えます。

選択したコンテンツに応じて、インプレース編集オプションと、[&#x200B; プロパティパネルのコンテンツに関する追加情報とオプションが異なる場合があります。](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)

### コンテキストメニュー {#context-menu}

編集可能なコンテンツはすべて、コンテンツの種類にバッジが付いています。

このバッジをクリックすると、編集アクションを含むコンテキストメニューにすばやくアクセスできます。 選択されていない編集可能な項目を右クリックすると、自動的に選択され、コンテキストメニューも開きます。

![編集可能なバッジオプション &#x200B;](assets/editable-badge.png)

### プレーンテキストの編集 {#edit-plain-text}

コンポーネントをダブルクリックまたはダブルタップすると、その場でテキストを編集できます。

![コンテンツを編集](assets/editing-content.png)

薄い水色のアウトラインが濃い青色のアウトラインに変わり、選択範囲が示され、カーソルが表示されます。 変更を行ったら、Enter キーまたは Return キーを押すか、テキストボックスの外側を選択して、変更を保存します。

テキストコンポーネントを選択すると、その詳細が[&#x200B; プロパティパネルに表示されます。](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail) パネルのテキストを編集することもできます。

![プロパティパネルでのテキストの編集](assets/ue-editing-text-component-rail.png)

また、テキストの詳細はプロパティパネルで確認できます。 フォーカスがプロパティパネルの編集されたフィールドを離れると、変更は自動的に保存されます。

### リッチテキストの編集 {#edit-rich-text}

コンポーネントをダブルクリックまたはダブルタップすると、その場でテキストを編集できます。

![リッチテキストコンポーネントの編集](assets/rich-text-editing.png)

利便性のために、テキストの書式設定オプションと詳細は、2 か所で利用できます。

#### リッチテキストコンテキストメニュー {#rich-text-context-menu}

リッチテキストブロックの上にコンテキストメニューが表示され、コンテキスト内の基本的な書式設定オプションが表示されます。 スペースの都合上、一部のオプションが省略記号ボタンの後ろに隠れている場合があります。

![リッチテキストコンテキストメニュー](assets/rich-text-context-menu.png)

編集されたフィールドからフォーカスが離れると、変更は自動的に保存されます。

#### プロパティパネル {#properties-rail}

[&#x200B; プロパティパネル &#x200B;](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)には、選択したリッチテキストコンポーネントのエントリが表示されます。

![&#x200B; プロパティパネルのリッチテキストコンポーネント &#x200B;](assets/rich-text-properties-panel.png)

#### モーダルエディター {#modal-editor}

[&#x200B; プロパティパネル &#x200B;](#properties-rail)のエントリをタップすると、モーダルエディターが開き、大きなキャンバスを使用してリッチテキストを編集できます。

![リッチテキスト編集ダイアログ](assets/rich-text-canvas.png)

「**キャンセル**」または「**完了**」をタップまたはクリックして、それぞれ変更を破棄または保存します。 Esc キーを押して変更を保存し、ダイアログを閉じることもできます。

#### リッチテキスト書式設定オプション {#formatting-options}

ユニバーサルエディターのリッチテキストエディター（RTE）を使用すると、作成者は標準のテキストフォーマットを適用できます。 次のオプションを使用できます。

* **段落スタイル**
   * 段落、h1 ～ h6、コード
* **太字**
* **斜体**
* **下線**
* **取り消し線**
* **テキストカラー**
   * カラーを選択したり、16進値を指定したりできるカラーパレットを開きます
   * モーダルエディターでのみ使用でき、インコンテクストでは使用できません
* **上付き文字**
* **下付き文字**
* **箇条書き**
   * tab キーを使用してインデントし、shift + tab キーを使用してインデントします。
* **順序付きリスト**
   * tab キーを使用してインデントし、shift + tab キーを使用してインデントします。
* **リンク**
   * URLを指定するか、コンテンツブラウザーを使用して、AEM内のパスを選択します。
* **リンク解除**
   * 選択したテキストからリンクを削除します。
* **画像**
   * URLを指定するか、[Content Advisor](/help/assets/integrate-adobe-non-adobe-applications.md)を使用して、AEMからアセットを選択します。
* **テーブル**
   * ドロップダウンを使用して、選択した数の列と行の新しいテーブルを挿入するか、新しい列/行を挿入して削除します。
* **調整**
   * **左揃え**
   * **中央揃え**
   * **右揃え**
   * **ジャスティフィケーションの整列**
* **右から左へ**
* **左から右**
* **インデント**
* **アウトデント**
* **テキストとしてペースト**
   * ユニバーサルエディターにペーストする前に、クリップボードのテキストから書式を削除します。
* **特殊文字**
   * テキストに特殊文字を挿入します。
* **すべての書式を削除**
   * 選択したテキストからすべての書式設定オプションを削除します。

バックエンドによっては、デフォルトで使用できるオプションが異なる場合があります。 RTEは、作成者のニーズに応じて、オプションを非表示にしたり、追加のオプションを表示したりするように設定できます。 詳しくは、「[&#x200B; ユニバーサルエディターのRTEの設定](/help/implementing/universal-editor/configure-rte.md)」のドキュメントを参照してください。

### メディアの編集 {#edit-media}

詳細は、[プロパティパネル](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)で確認できます。

![メディアの編集](assets/ue-edit-media.png)

1. プロパティパネルで、選択した画像のプレビューをタップまたはクリックします。
1. [&#x200B; コンテンツアドバイザー](/help/assets/integrate-adobe-non-adobe-applications.md) ウィンドウが開き、アセットを選択できます。
1. 選択して、新しいアセットを選択します。
1. 「**選択**」を選択して、アセットが置き換えられたプロパティパネルに戻ります。

変更はコンテンツに自動的に保存されます。

### コンテンツフラグメントの編集 {#edit-content-fragment}

[&#x200B; コンテンツフラグメント &#x200B;](/help/sites-cloud/administering/content-fragments/overview.md)を選択した場合、[&#x200B; プロパティパネルでその詳細を編集できます。](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)

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

   ![コンテナに追加するコンポーネントの選択](assets/ue-add-component.png)

1. 次のいずれかを実行できます。

   * プロパティパネルで「**追加**」アイコンを選択します。

     ![追加アイコンの選択](assets/add-icon.png)

   * コンテキストメニューで「**追加**」オプションを選択します。

     ![&#x200B; コンテキストメニューから追加](assets/add-from-context-menu.png)

1. コンポーネントピッカーダイアログが開きます。
   * 左側の列を使用して、カテゴリ別にコンポーネントをフィルタリングするか、検索を使用して名前でフィルタリングします。
   * 右側の列のコンポーネント名をクリックして、コンテナに挿入します。
   * コンテナ内で使用できるコンポーネントが1つしかない場合は、自動的に挿入されます。
   * ピッカーの外側をクリックして、コンポーネントの挿入をキャンセルします。

   ![&#x200B; コンポーネントピッカー](assets/component-picker.png)

コンポーネントがコンテナに挿入され、エディターで編集できます。

>[!TIP]
>
>ホットキー `a` を使用して、選択したコンテナにコンポーネントを追加します。

### コンテナ内のコンポーネントの複製 {#duplicating-components}

1. [コンテンツツリー](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)またはエディターを使用して、コンテナ内のコンポーネントを選択します。

1. 次のいずれかを実行できます。

   * プロパティパネルで「**重複**」アイコンを選択します。

     ![コンテナに追加するコンポーネントの選択](assets/ue-duplicate-component.png)

   * コンテキストメニューから「**重複**」オプションを選択します。

     ![&#x200B; コンテキストメニューから複製](assets/duplicate-from-context-menu.png)

コンポーネントが複製され、選択したコンポーネントの下に挿入されます。

### コンテナからのコンポーネントの削除 {#deleting-components}

1. [&#x200B; コンテンツツリー](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)またはエディターで、コンテナ内のコンポーネントを選択します。
1. 次のいずれかを実行できます。
   * プロパティパネルで「**削除**」アイコンを選択します。

     ![コンポーネントの削除](assets/ue-delete-component.png)
   * コンテキストメニューで「**削除**」オプションを選択します。
     ![&#x200B; コンテキストメニューから削除](assets/delete-from-context-menu.png)

選択したコンポーネントが削除されました。

>[!TIP]
>
>ホットキー `Shift+Backspace` を使用して、選択したコンポーネントをコンテナから削除します。

### コンポーネントの並べ替えと移動 {#reordering-components}

ドラッグ&amp;ドロップ、コンテキストメニュー、コンテンツツリーを使用して、コンポーネントを移動したり、並べ替えたりできます。

>[!NOTE]
>
>選択したコンポーネントがターゲットコンテナの[コンポーネントフィルター](/help/implementing/universal-editor/filtering.md)で許可されている場合にのみ、コンテナ間でコンポーネントを移動できます。

#### ドラッグ&amp;ドロップでコンポーネントを移動 {#drag-and-drop-move}

1. 移動するコンポーネントをクリックしてドラッグします。
   * 宛先にマウスポインターを置くと、コンポーネントを青い横線でドロップすると、エディターに配置される場所が表示されます。
     ![&#x200B; コンポーネントをドラッグ&amp;ドロップして移動します](assets/drag-and-drop-component-move.png)
1. コンポーネントをドロップして再配置します。

#### コンテキストメニューでのコンポーネントの移動 {#move-context-menu}

1. コンポーネントを右クリックするか、選択したコンポーネントのバッジをクリックして、[&#x200B; コンテキストメニューを開きます。](#context-menu)
1. 目的の移動オプションを選択します。
   * 最上位に移動
   * 上に移動
   * 下に移動
   * 最下位に移動
     ![&#x200B; コンテキストメニューのオプションを移動](assets/move-options-in-conext-menu.png)

コンポーネントは、エディターとコンテンツツリーの両方で移動します。

>[!TIP]
>
>ホットキー`Command-U`または`Shift-Command-U`を使用して、それぞれ上または上に移動します。
> ホットキー`Command-J`または`Shift-Command-J`を使用して、それぞれ下または下に移動します。

>[!NOTE]
>
>コンテキストメニューオプションは、コンテナ内のコンポーネントのみを移動できます。 コンテナ間でコンポーネントを移動する場合は、[&#x200B; コンテンツツリーを使用します。](#reorder-content-tree)

#### コンテンツツリーでのコンポーネントの移動 {#reorder-content-tree}

1. [コンテンツツリーモード](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)でない場合はそれに切り替えます。
1. コンテンツツリーまたはエディターでコンテナコンポーネントを選択します。
1. コンテナの山形アイコンを選択して、コンテンツツリーでコンテンツを展開します。
1. コンテナ内のコンポーネントの横にあるハンドルアイコンをドラッグすると、それらを並べ替えることができます。 コンポーネントをドラッグして、コンテナ内で並べ替えます。

   ![コンポーネントの並べ替え](assets/ue-reordering-components.png)

1. ドラッグしたコンポーネントがコンテンツツリー内でグレー表示され、挿入ポイントは青い線で表されます。 コンポーネントをリリースして、新しい場所に配置します。

コンポーネントは、コンテンツツリーおよびエディターの両方で並べ替えられます。

### 取り消しとやり直し {#undo-redo}

エディターで最後に行った編集を取り消すまたはやり直すには、「取り消し」ボタンまたは「やり直し」ボタンを選択します。

![取り消しアイコン](assets/undo.png)
![やり直しアイコン &#x200B;](assets/redo.png)

* コンテキスト内での編集、プロパティパネルを使用した編集、ブロックの追加、複製、移動、削除に対して、取り消しとやり直しを実行できます。
* 取り消しとやり直しは、現在のブラウザーセッションに限定されます。

>[!TIP]
>
>取り消すには `Command-Z`、やり直すには `Shift-Command-Z` のホットキーを使用します。

### コピー＆ぺースト {#copy-paste}

[コンテナ](/help/implementing/universal-editor/field-types.md#container)内にあるコンポーネントをコピー＆ペーストできます。 これは、ターゲットコンテナに[個のフィルターが設定されていないか、コンポーネントをペーストできるフィルターがある場合にのみ可能です。](/help/implementing/universal-editor/filtering.md)

コピー&amp;ペーストは、同じブラウザータブ、またはタブが既に開いている場合は、ブラウザータブ間で行うことができます。 アイテムをコピーしてから、新しいブラウザータブを開いて貼り付けることはできません。

![&#x200B; コピーアイコン](assets/copy.png)
![&#x200B; アイコンを貼り付け](assets/paste.png)

1. エディター内またはコンテンツツリーでコンポーネントを選択します。
1. 次のいずれかを実行できます。
   * [&#x200B; プロパティパネルの&#x200B;**コピー** アイコンをクリックします。](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-panel)
     ![&#x200B; パネルからコピー](assets/copy-from-panel.png)
   * コンテキストメニューで「**コピー**」オプションを選択します。
     ![&#x200B; コンテキストメニューからコピー](assets/copy-from-context-menu.png)
1. コピーしたコンポーネントをペーストした&#x200B;_後_&#x200B;のコンポーネントを選択します。
1. 次のいずれかを実行できます。
   * プロパティパネルで「**貼り付け**」をタップまたはクリックします。
     ![&#x200B; パネルからの貼り付け](assets/paste-from-panel.png)
   * コンテキストメニューで「**貼り付け**」を選択します。
     ![&#x200B; コンテキストメニューからの貼り付け](assets/paste-from-context-menu.png)

コピーしたコンポーネントは、選択したコンポーネントの&#x200B;_後_&#x200B;にペーストされます。

>[!TIP]
>
>コピーするには `Command-C`、ペーストするには `Command-V` のホットキーを使用します。

## コンテンツのプレビュー {#previewing-content}

コンテンツの編集が完了したら、他のページのコンテンツでコンテンツがどのように表示されるかを確認するためにコンテンツ内を移動したい場合がよくあります。 [プレビューモード](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode)でリンクをクリックして、読者と同じようにコンテンツ内を移動できます。 コンテンツは、公開されるときと同じように、エディターでレンダリングされます。

プレビューモードでは、コンテンツをタップまたはクリックすると、コンテンツの読者に対するように反応します。 編集するコンテンツを選択する場合は、[プレビューモード](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode)から切り替えます。

## コンポーネントの継承の編集 {#inheritance}

継承とは、一方を変更するともう一方も自動的に変更されるようにコンテンツをリンクできるメカニズムです。

ユニバーサルエディターを使用すると、コンテンツを更新するだけで、コンテンツの継承をキャンセルできます。 エディターでは、そのページの作成者が行ったすべての変更の継承を自動的に無効にし、ブループリントから更新を同期した際に変更済みのコンテンツが保持されるようにします。

**AEM マルチサイト管理（MSM）拡張機能**&#x200B;がプログラムに対して有効な場合は、ユニバーサルエディター内で個々のコンポーネントの継承ステータスを表示および変更する[追加のツールバーオプション](#inheritance-extension)があります。

ユニバーサルエディターを使用した継承の仕組みについて詳しくは、「[&#x200B; ユニバーサルエディターでのコンテンツの継承」を参照してください。](/help/sites-cloud/authoring/universal-editor/inheritance.md)

## オプションのツールバー機能 {#toolbar-options}

ページとコンテンツをさらに管理するのに役立つ追加機能が、ユニバーサルエディターの拡張機能として使用できます。 [ユニバーサルエディターのツールバー](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar)にコンテンツ作成者が表示する前に、[これらの拡張機能は、管理者がプログラムで有効にする必要があります](/help/implementing/universal-editor/extending.md)。

### 継承 {#inheritance-extension}

**AEM マルチサイト管理（MSM）拡張機能**&#x200B;では、選択したコンポーネントの現在の継承ステータスが表示され、[継承を解除または復元](/help/sites-cloud/authoring/universal-editor/inheritance.md)できます。

ユニバーサルエディターツールバーの&#x200B;**インストール済み継承**&#x200B;アイコンは、選択したコンポーネントの継承が引き続きアクティブであることを示します。

![インストール済み継承アイコン](assets/inheritance-installed-icon.png)

選択したコンポーネントの継承を解除するには、アイコンをタップまたはクリックします。 コンポーネントを編集すると、継承は自動的に解除されます。

**解除済み継承**&#x200B;アイコンは、選択したコンポーネントの継承が解除済みであることを示します。

![解除済み継承アイコン](assets/inheritance-broken-icon.png)

アイコンをタップまたはクリックすると、選択したコンポーネントの継承が復元されます。 継承済みコンテンツを表示するには、ページをリロードしてコンテンツを更新する必要があります。

この拡張機能を有効にする方法について詳しくは、[Extension Manager ドキュメント](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)を参照してください。

>[!NOTE]
>
>**インストール済み継承**&#x200B;アイコンと&#x200B;**解除済み継承**&#x200B;アイコンは、コンポーネントを選択し、ページがブループリントに基づいている場合にのみ表示されます。

>[!NOTE]
>
>**AEM マルチサイト管理（MSM）拡張機能**&#x200B;はページに対してのみ機能し、コンテンツフラグメントには機能しません。

### ページプロパティへのアクセス {#page-properties}

**ページプロパティ** ボタンを使用すると、現在編集中のページの[AEM ページプロパティウィンドウ &#x200B;](/help/sites-cloud/authoring/sites-console/page-properties.md)にすばやくアクセスできます。

![ページプロパティアイコン](assets/page-properties-icon.png)

ユニバーサルエディターツールバーの&#x200B;**ページプロパティ**&#x200B;アイコンをタップまたはクリックすると、新しいブラウザータブでページのページプロパティが開きます。

>[!NOTE]
>
>* 「**AEM ページプロパティ**」ボタンは、コンテンツフラグメントではなく、ページでのみ機能します。
>* ボタンは、リモートページがプロトコル [&#128279;](/help/implementing/universal-editor/component-definition.md#plugins) `aem`または`xwalk`との接続を持ち、一意のページパスを現在の編集可能な状態から解決できる場合にのみ表示されます。

### サイト管理者で開く {#sites-console}

「**サイト管理で開く**」ボタンを使用すると、AEM[&#128279;](/help/sites-cloud/authoring/sites-console/introduction.md)の サイトコンソール（`/content/experience-fragments` パスの[&#x200B; エクスペリエンスフラグメントコンソール &#x200B;](/help/sites-cloud/authoring/fragments/experience-fragments.md)）にすばやくアクセスし、現在編集中のページがコンテンツ構造のどこにあるかを確認できます。 これにより、サイトツリーを移動したり、コンソールでページレベルのアクションを実行したりできます。

![サイト管理者で開くアイコン](assets/open-in-site-admin-icon.png)

アイコンをタップまたはクリックすると、新しいブラウザータブで Sites コンソールが開き、現在エディターにあるページに移動します。

DAM パス （`/content/dam`）の場合、このボタンは非表示になり、現在の編集可能ファイルから一意のAEM ページを決定できない場合は非表示になります。

### ページのロックとロック解除 {#locking-pages}

**AEM ページロック拡張機能**&#x200B;を使用すると、エディターのページの現在のロック状態が表示され、[ページをロックまたはロック解除](/help/sites-cloud/authoring/sites-console/managing-pages.md#locking-a-page)できます。

ユニバーサルエディターツールバーの&#x200B;**ロック解除済み**&#x200B;アイコンは、エディターのページが現在ロックされていないことを示します。

![ロック解除済みアイコン](assets/unlocked-icon.png)

アイコンをタップまたはクリックすると、ページがロックされます。

ユニバーサルエディターツールバーの&#x200B;**ロック済み**&#x200B;アイコンは、エディターのページが現在ロックされていることを示します。 アイコンにポインターを合わせると、ページをロックしたユーザーを示すツールチップが表示されます。

![ロック済みアイコン](assets/locked-icon.png)

ユーザーがページをロックした場合は、アイコンをタップまたはクリックしてページのロックを解除します。

この拡張機能を有効にする方法について詳しくは、[Extension Manager ドキュメント](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)を参照してください。

>[!NOTE]
>
>**AEM ページロック拡張機能**&#x200B;はページに対してのみ機能し、コンテンツフラグメントには機能しません。

### ワークフロー {#workflows}

**AEM ワークフロー拡張機能**&#x200B;を使用すると、現在エディターにあるページで[ワークフローを開始](/help/sites-cloud/authoring/workflows/overview.md)できます。

![ワークフローアイコン](assets/workflows-icon.png)

ユニバーサルエディターツールバーの&#x200B;**ワークフロー**&#x200B;アイコンをタップまたはクリックして、**ワークフローを開始**&#x200B;モーダルを開きます。 ウィンドウには、ワークフローを適用できるコンテンツのリストが表示されます。

![ワークフローを開始モーダル](assets/start-a-workflow.png)

1. **ワークフローモデル**&#x200B;ドロップダウンで、適用するワークフローを選択します。
1. 「**名前**」フィールドのワークフローに説明を入力します。
1. **ワークフローに含めるコンテンツ**&#x200B;リストで、チェックボックスを使用して、ワークフローに含めるコンテンツを定義します。
1. **ワークフローを開始**&#x200B;をタップまたはクリックしてワークフローを開始し、「**閉じる**」をタップまたはクリックして中止します。

この拡張機能を有効にする方法について詳しくは、[Extension Manager ドキュメント](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)を参照してください。

### 開発者ログイン {#developer-login}

**AEM ユニバーサルエディター開発者ログイン拡張機能**&#x200B;は、ローカルで開発する開発者にとって便利で、テスト目的でローカルの AEM SDK に対する認証を行うことができます。

![開発者ログインアイコン](assets/developer-login-icon.png)

ユニバーサルエディターツールバーの&#x200B;**開発者ログオン**&#x200B;アイコンをタップまたはクリックして、ローカルの AEM SDK にサインインするためのローカルログイン資格情報を入力します。

![開発者ログインモーダル](assets/developer-login.png)

この拡張機能を有効にする方法について詳しくは、[Extension Manager ドキュメント](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)を参照してください。

## オプションのプロパティパネルの機能 {#properties-panel-options}

ページのコンテンツをさらに管理するのに役立つ追加機能が、ユニバーサルエディターの拡張機能として使用できます。 これらの拡張機能が[ユニバーサルエディターのプロパティパネル](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail)でコンテンツ作成者に表示されるには、[管理者がプログラムでこれらの拡張機能を有効にする必要があります](/help/implementing/universal-editor/extending.md)。

### バリエーションを生成 {#generate-variations}

**バリエーションを生成**&#x200B;拡張機能を使用すると、生成 AI を使用して、プロパティパネルでコンテンツのバリエーションを直接作成できます。

![「バリエーションを生成」アイコン](assets/generate-variations-icon.png)

ユニバーサルエディターのプロパティパネルにある「**バリエーションを生成**」アイコンをタップまたはクリックして、レコメンデーションを受け取り、バリエーションを作成します。 バリエーションの生成の仕組みについて詳しくは、[バリエーションを生成 - AEM エディターに統合済み](/help/generative-ai/generate-variations-integrated-editor.md)ドキュメントを参照してください。

この拡張機能を有効にする方法について詳しくは、[Extension Manager ドキュメント](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)を参照してください。

## その他のリソース {#additional-resources}

ユニバーサルエディターを使用してコンテンツを公開する方法については、このドキュメントを参照してください。

* [ユニバーサルエディターを使用したコンテンツの公開](publishing.md) - ユニバーサルエディターでのコンテンツの公開方法と、アプリでの公開済みコンテンツの処理方法について説明します。

ユニバーサルエディターの技術的な詳細について詳しくは、次の開発者向けドキュメントを参照してください。

* [ユニバーサルエディターの概要](/help/implementing/universal-editor/introduction.md) - ユニバーサルエディターを使用して、実装おけるあらゆるコンテンツの様々な側面を編集できるようにして、優れたエクスペリエンスを実現し、コンテンツベロシティを向上させる方法について説明します。
* [AEM のユニバーサルエディターの概要](/help/implementing/universal-editor/getting-started.md) - ユニバーサルエディターへのアクセス権を取得する方法と、これを使用するために最初の AEM アプリのインストルメントを開始する方法について説明します。
* [ユニバーサルエディターのアーキテクチャ](/help/implementing/universal-editor/architecture.md) - ユニバーサルエディターのアーキテクチャと、そのサービスとレイヤー間でのデータのフローについて説明します。
* [属性とタイプ](/help/implementing/universal-editor/attributes-types.md) - ユニバーサルエディターで必要なデータ属性とデータ型について説明します。
* [ユニバーサルエディターの認証](/help/implementing/universal-editor/authentication.md) - ユニバーサルエディターの認証方法について説明します。

