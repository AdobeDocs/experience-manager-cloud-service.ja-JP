---
title: ' [!DNL Adobe Experience Manager]  のリッチテキストエディターを使用して、コンテンツを作成します。'
description: ' [!DNL Experience Manager]  リッチテキストエディターを使用したコンテンツのオーサリング'
translation-type: tm+mt
source-git-commit: 5a90db8791dd92cceb811b9ed2beda3ecb4a974d
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 100%

---


# リッチテキストエディターを使用したコンテンツのオーサリング {#use-rich-text-editor-to-author-content}

リッチテキストエディター（RTE）は、[!DNL Adobe Experience Manager] にテキストコンテンツを追加するための基本的な構成要素です。また、オーサリングを可能にするその他の多くのコンポーネントは RTE に基づいています。Experience Manager 開発者は RTE をカスタマイズでき、管理者は作成者が使用する RTE を設定できます。

## インプレース編集 {#in-place-editing}

テキストベースのコンポーネントを 1 回クリックして選択すると、[コンポーネントツールバー](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)が表示されます。

![コンポーネントツールバー](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

もう一度クリックするか、最初にコンポーネントをゆっくりダブルクリックして選択すると、インプレース編集が開きます。編集モードには、ツールバーが含まれます。ここで、コンテンツの編集や、基本的な書式変更ができます。

![RTE を使用したインプレース編集](/help/sites-cloud/authoring/assets/rte-in-place-editing.png)

通常、ツールバーには次のオプションがあります。

* **形式**：テキストを太字や斜体にしたり、テキストに下線を引いたりします。
* **リスト**：箇条書き記号または番号付きリストを作成し、インデントを設定します。
* **ハイパーリンク**：リンクを作成します。
* **リンク解除**：ハイパーリンクを削除します。
* **全画面表示**：エディターをフルスクリーンモードで開きます。
* **閉じる**：編集を停止します。
* **保存**：変更を保存します。

## フルスクリーン編集 {#full-screen-editing}

テキストベースのコンポーネントの場合は、[ツールバー](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar)のフルスクリーンモード ![RTE 全画面表示ボタン](/help/sites-cloud/authoring/assets/editing-full-screen.png)をクリックしてリッチテキストエディターを開き、ページコンテンツの残りを非表示にします。

フルスクリーンモードでは、オーサリングに使用できる設定済みオプションがすべて表示されます。使用できるオプションは、設定によって異なります。 <!--Full screen mode displays all the configured options that you can use for authoring. The availability of options [depends on the configuration](/help/sites-administering/rich-text-editor.md).-->

![フルスクリーンモードの RTE](/help/sites-cloud/authoring/assets/rte-full-screen.png)

さらなるリッチテキストエディターオプションを次に示します。

* **アンカー**：テキストにアンカーを作成し、後でそのアンカーへのリンクや参照が作成できます。
* **テキストを左揃え**。
* **テキストを中央揃え**。
* **テキストを右揃え**。

「最小化」をクリックしてフルスクリーンモードを閉じます。

>[!TIP]
>
>ネストされたリストを [!DNL Microsoft Word] から RTE にコピーすると、結果に一貫性がなくなる可能性があります。代わりに、テキスト形式で貼り付け、手動で調整してください。

>[!MORELIKETHIS]
>
>* [リッチテキストエディターの設定](/help/implementing/developing/extending/rich-text-editor.md)

