---
title: メタデータの編集と追加
description: ' [!DNL Experience Manager Assets]  のアセットメタデータを編集する様々な方法について説明します。'
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 65%

---

# メタデータの編集と追加 {#how-to-edit-or-add-metadata}

メタデータは、検索可能なアセットに関する追加情報です。画像をアップロードすると自動的に抽出されます。既存のメタデータを編集したり、新しいメタデータプロパティを既存のフィールドに追加（例えば、メタデータフィールドが空白の場合など）したりすることができます。

メタデータの語彙を制御し、信頼性を確保する必要があるので、 [!DNL Experience Manager Assets] では、新しいメタデータプロパティをオンデマンドで追加することはできません。 作成者は、アセットの新しいメタデータフィールドを追加することはできませんが、開発者は追加できます。[アセットの新しいメタデータプロパティの作成](meta-edit.md#editing-metadata-schema)を参照してください。

## アセットのメタデータの編集 {#editing-metadata-for-an-asset}

メタデータを編集するには、次の手順に従います。

1. 次のいずれかの操作をおこないます。

   * Assets UI から、アセットを選択し、 **[!UICONTROL プロパティを表示]** アイコンをクリックします。
   * アセットのサムネールから、「**[!UICONTROL プロパティを表示]**」クイックアクションを選択します。
   * アセットページで、「 」を選択します。 **[!UICONTROL プロパティを表示]** をクリックします。

   アセットページにアセットのメタデータが表示されます。 このメタデータは、Experience Manager Assets にアップロードされた（取り込まれた）ときに、自動的に抽出されたものです。

1. 必要に応じて、様々なタブでメタデータを編集し、完了したら、「 」を選択します。 **[!UICONTROL 保存]** ツールバーから変更を保存します。 選択 **[!UICONTROL 閉じる]** をクリックして、Assets Web インターフェイスに戻ります。

   >[!NOTE]
   >
   >テキストフィールドが空の場合、現在設定されているメタデータはありません。フィールドに値を入力して保存すると、そのメタデータプロパティを追加できます。

アセットのメタデータへの変更内容は、XMP データの一部として元のバイナリに書き戻されます。この操作は、Experience Manager のメタデータ書き戻しワークフローで実行されます。既存のプロパティに対して行われた変更 ( 例： `dc:title`) が上書きされ、新しく作成されたプロパティ ( `cq:tags`) は、スキーマと共に追加されます。

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## メタデータスキーマの編集 {#editing-metadata-schema}

メタデータスキーマの編集方法について詳しくは、[メタデータスキーマフォームの編集](metadata-schemas.md#edit-metadata-schema-forms)を参照してください。

## Experience Manager でのカスタム名前空間の登録 {#registering-a-custom-namespace-within-aem}

Experience Manager 内で独自の名前空間を追加できます。cq、jcr、sling など事前に定義された名前空間があるように、リポジトリメタデータと xml 処理用の名前空間を設定できます。

1. ノードタイプ管理ページ（*https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*）に移動します。
1. 選択 **[!UICONTROL 名前空間]** をクリックします。 ウィンドウに名前空間管理ページが表示されます。

1. 名前空間を追加するには、「 **[!UICONTROL 新規]** 下に
1. XML 名前空間規則に従ってカスタム名前空間を指定し（URI 形式の id と、その id に関連付けられているプレフィックスを指定）、を選択します。 **[!UICONTROL 保存]**.

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [メタデータを管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)
