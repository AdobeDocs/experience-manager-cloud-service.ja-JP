---
title: Use the Rich Text Editor in [!DNL Adobe Experience Manager] to author content.
description: Use the [!DNL Experience Manager] Rich Text Editor to author content.
translation-type: tm+mt
source-git-commit: 5437329c55bd7da6d8b966a7f01c9e57ff1feb59
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 42%

---


# リッチテキストエディターを使用したコンテンツのオーサリング {#use-rich-text-editor-to-author-content}

リッチテキストエディタ(RTE)は、テキストコンテンツを追加する基本的な文書パーツ [!DNL Adobe Experience Manager]です。 また、オーサリングを可能にする他の多くのコンポーネントはRTEに基づいています。 Experience Manager開発者はRTEをカスタマイズでき、管理者は作成者が使用するRTEを設定できます。

## インプレース編集 {#in-place-editing}

テキストベースのコンポーネントを1回クリックして選択すると、 [コンポーネントツールバーが表示され](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)ます。

![コンポーネントツールバー](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

もう一度クリックするか、重複のクリックが遅いコンポーネントを最初に選択すると、インプレイス編集が開きます。 編集モードには、ツールバーが含まれます。 コンテンツを編集し、基本的な書式設定を変更できます。

![RTE を使用したインプレース編集](/help/sites-cloud/authoring/assets/rte-in-place-editing.png)

通常、ツールバーには次のオプションがあります。

* **形式**：テキストを太字や斜体にしたり、テキストに下線を引いたりします。
* **リスト**：箇条書き記号または番号付きリストを作成し、インデントを設定します。
* **ハイパーリンク**：リンクを作成します。
* **リンク解除**：ハイパーリンクを削除します。
* **フルスクリーン**: エディターをフルスクリーンモードで開きます。
* **閉じる**：編集を停止します。
* **保存**：変更を保存します。

## フルスクリーン編集 {#full-screen-editing}

For text-based components, click the full-screen mode ![RTE full screen button](/help/sites-cloud/authoring/assets/editing-full-screen.png) from the [toolbar](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) to open the rich text editor and hides the rest of the page content.

フルスクリーンモードでは、オーサリングに使用できる設定済みオプションがすべて表示されます。使用できるオプションは、設定によって異なります。 <!--Full screen mode displays all the configured options that you can use for authoring. The availability of options [depends on the configuration](/help/sites-administering/rich-text-editor.md).-->

![フルスクリーンモードの RTE](/help/sites-cloud/authoring/assets/rte-full-screen.png)

リッチテキストエディターのその他のオプションを次に示します。

* **アンカー**：テキストにアンカーを作成し、後でそのアンカーへのリンクや参照が作成できます。
* **テキストを左揃え**.
* **テキストを中央揃え**.
* **テキストを右揃え**.

「最小化」をクリックしてフルスクリーンモードを閉じます。

>[!Tip]
>
>Copying nested lists from [!DNL Microsoft Word] into the RTE can give inconsistent results. 代わりに、テキストとして貼り付け、手動で調整をおこないます。

>[!MORELIKETHIS]
>
>* [リッチテキストエディターの設定](/help/implementing/developing/extending/rich-text-editor.md)

