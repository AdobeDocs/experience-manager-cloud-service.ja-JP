---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] のアセットセレクター'
description: アセットセレクターを使用して、アプリケーション内のアセットのメタデータとレンディションを検索および取得します。
role: Admin,User
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: ht
source-wordcount: '479'
ht-degree: 100%

---


# アセットセレクターのコレクション {#asset-selector-collections}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

コレクションとは、アセットセレクター内のアセット、フォルダーまたはその他のコレクションのセットです。コレクションを使用して、ユーザー間でアセットを共有します。フォルダーとは異なり、1 つのコレクションに異なる複数の場所のアセットを含めることができます。

アセットセレクターのマイクロフロントエンドコレクションは、読み取り専用モードで標準で使用できます。アクセス権を持つ [!DNL Experience Manager Assets] リポジトリからアセットとコレクションを直接取得します。

>[!NOTE]
>
>[!DNL Experience Manager Assets] の [imsOrg](/help/assets/asset-selector-properties.md) およびコレクションに対するアクセス権があることを確認します。

アセットセレクターのマイクロフロントエンドコレクションは、読み取り専用モードで標準で使用できます。アクセス権を持つ Experience Manager Assets リポジトリからアセットとコレクションを直接取得し、Experience Manager Assets リポジトリからパブリックフォルダーとプライベートフォルダーのプロパティを継承します。詳しくは、[アセットビューでのパブリックまたはプライベートコレクションの作成](/help/assets/manage-collections-assets-view.md#create-collection)を参照してください。

アセットセレクターのコレクションは、パネル表示とモーダル表示の両方で表示できます。

![パネル表示のコレクション](assets/collections-rail-modal-view.png)

<!--
Additionally, you can [customize](/help/assets/asset-selector-customization.md) the `featureSet` property to enable or disable collections in Asset Selector. See [enable or disable Collections tab](#enable-disable-collections-tab).-->

さらに、「コレクション」タブでアセットの選択をカスタマイズすることもできます。これを行うには、`handleSelection` を使用してカスタマイズできます。[オブジェクトスキーマを使用したアセット選択の処理](/help/assets/asset-selector-customization.md#handling-selection)を参照してください。

## コレクションの表示 {#view-collections}

アセットセレクターを使用すると、コレクションを ![リスト表示](assets/do-not-localize/list-view.png) リスト表示または ![グリッド表示](assets/do-not-localize/grid-view.png) グリッド表示で表示できます。[アセットセレクターでの表示のタイプ](overview-asset-selector.md#types-of-view)を参照してください。

## アセットのコンポーネントへのドラッグ＆ドロップ {#collection-drag-and-drop}

オーサー環境の [!DNL Assets as a Cloud Service] ビューから、アセットをコレクションに直接ドラッグ＆ドロップできます。これを行うには、アセットを「アセット」タブからアセットセレクターアプリケーションの「コレクション」作業領域にドラッグして、リッチアプリケーションを作成します。

>[!NOTE]
>
>* アセットのドラッグ＆ドロップは、パネル表示でのみ可能です。
>* ドラッグ＆ドロップできるのはファイル（アセット）のみで、フォルダーはドラッグ＆ドロップできません。

一方、直接[コレクション内のアセットのドラッグ＆ドロップを有効または無効](asset-selector-customization.md#enable-disable-drag-and-drop)にすることもできます。

## コレクション内のアセットの選択を無効にする {#disable-selection-collection}

「選択を無効にする」は、アセットやフォルダーを非表示にしたり、選択できないようにしたりするために使用します。カードやアセットから選択チェックボックスを非表示にし、選択されないようにします。[選択を無効にする](/help/assets/asset-selector-customization.md#disable-selection)を参照してください。

## 「コレクション」タブを有効または無効にする {#enable-disable-collections-tab}

アセットセレクターを使用すると、要件とユーザビリティに応じてコンポーネントをカスタマイズできます。アセットセレクターの「コレクション」タブを有効または無効にするには、次の方法で `featureSet` プロパティを使用します。

* **「コレクション」タブを有効にする：**「コレクション」タブを有効にするには、`collections` を配列の値として指定する必要があります。デフォルトでは、「コレクション」タブはすべてのユーザーに対して標準で有効になります。例えば、`featureSet:["collections"]` のように指定します。
* **「コレクション」タブを無効にする：**「コレクション」タブを無効にするには、空の配列をその値として指定する必要があります。例えば、`featureSet:[ ]` のように指定します。

>[!MORELIKETHIS]
>
>* [アセットセレクターのカスタマイズ](/help/assets/asset-selector-customization.md)
>* [アセットセレクターと様々なアプリケーションの統合](/help/assets/integrate-asset-selector.md)
>* [アセットセレクターのプロパティ](/help/assets/asset-selector-properties.md)

