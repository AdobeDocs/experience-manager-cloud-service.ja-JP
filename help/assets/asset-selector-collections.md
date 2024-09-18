---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] のアセットセレクター'
description: アセットセレクターを使用して、アプリケーション内のアセットのメタデータとレンディションを検索および取得します。
role: Admin,User
source-git-commit: 5c76b28726403a6b011a55add190e6e3a6d7a390
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 15%

---


# アセットセレクターコレクション {#asset-selector-collections}

コレクションとは、アセットセレクター内のアセット、フォルダーまたはその他のコレクションのセットです。 コレクションを使用して、ユーザー間でアセットを共有します。フォルダーとは異なり、1 つのコレクションに異なる複数の場所のアセットを含めることができます。

アセットセレクターのマイクロフロントエンドコレクションは、すぐに使用できる読み取り専用モードです。 アクセス権のある [!DNL Experience Manager Assets] リポジトリからアセットやコレクションを直接取得します。

>[!NOTE]
>
>[!DNL Experience Manager Assets] [imsOrg](/help/assets/asset-selector-properties.md) およびコレクションにアクセスする権限があることを確認します。

アセットセレクターのマイクロフロントエンドコレクションは、すぐに使用できる読み取り専用モードです。 アクセス可能なExperience Manager Assets リポジトリからアセットとコレクションを直接取得し、Experience Manager Assets リポジトリからパブリックおよびプライベートフォルダーのプロパティを継承します。 詳しくは、[Assets ビューでのパブリックまたはプライベートコレクションの作成 ](/help/assets/manage-collections-assets-view.md#create-collection) を参照してください。

アセットセレクターでは、パネルビューとモーダルビューの両方でコレクションを表示できます。

![ パネルビューのコレクション ](assets/collections-rail-modal-view.png)

<!--
Additionally, you can [customize](/help/assets/asset-selector-customization.md) the `featureSet` property to enable or disable collections in Asset Selector. See [enable or disable Collections tab](#enable-disable-collections-tab).-->

また、「コレクション」タブで、アセットの選択をカスタマイズすることもできます。 それには、`handleSelection` を使用してカスタマイズできます。 [ オブジェクトスキーマを使用したAssetsの選択処理 ](/help/assets/asset-selector-customization.md#handling-selection) を参照してください。

## コレクションの表示 {#view-collections}

アセットセレクターを使用すると、コレクションを ![ リスト表示 ](assets/do-not-localize/list-view.png) リスト表示または ![ グリッド表示 ](assets/do-not-localize/grid-view.png) グリッド表示で表示できます。 [ アセットセレクターでの表示のタイプ ](overview-asset-selector.md#types-of-view) を参照してください。

## アセットをコレクションにドラッグ&amp;ドロップ {#collection-drag-and-drop}

オーサー環境の [!DNL Assets as a Cloud Service] ビューから直接コレクションにアセットをドラッグ&amp;ドロップできます。 これをおこなうには、「Assets」タブからアセットセレクターアプリケーションの「コレクション」ワークエリアにアセットをドラッグして、リッチアプリケーションを作成します。

>[!NOTE]
>
>* アセットのドラッグ&amp;ドロップは、パネルビューでのみ可能です。
>* ドラッグ&amp;ドロップできるのはファイル（アセット）のみです。フォルダーはドラッグ&amp;ドロップできません。

一方、コレクション内のアセットのドラッグ&amp;ドロップを直接 [ 有効または無効 ](asset-selector-customization.md#enable-disable-drag-and-drop) にすることもできます。

## コレクション内のアセット選択の無効化 {#disable-selection-collection}

「選択を無効にする」は、アセットやフォルダーを非表示にしたり、選択できないようにしたりするために使用します。カードやアセットから選択チェックボックスを非表示にし、選択されないようにします。[ 選択を無効にする ](/help/assets/asset-selector-customization.md#disable-selection) を参照してください。

## 「コレクション」タブを有効または無効にする {#enable-disable-collections-tab}

アセットセレクターを使用すると、要件と操作性に応じてコンポーネントをカスタマイズできます。 アセットセレクターの「コレクション」タブを有効または無効にするには、次 `featureSet` 方法でプロパティを使用します。

* **「コレクション」タブを有効にする：** 「コレクション」タブを有効にするには、配列の値として `collections` を指定する必要があります。 デフォルトでは、「コレクション」タブは、すべてのユーザーに対して初期設定の状態で有効になっています。 例えば、`featureSet:["collections"]` のように指定します。
* **「コレクション」タブを無効にする：** 「コレクション」タブを無効にするには、値として空の配列を指定する必要があります。 例えば、`featureSet:[ ]` のように指定します。

>[!MORELIKETHIS]
>
>* [ アセットセレクターのカスタマイズ ](/help/assets/asset-selector-customization.md)
>* [ アセットセレクターと様々なアプリケーションの統合 ](/help/assets/integrate-asset-selector.md)
>* [ アセットセレクターのプロパティ ](/help/assets/asset-selector-properties.md)

