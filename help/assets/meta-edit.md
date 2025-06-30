---
title: メタデータの編集と追加
description: ' [!DNL Experience Manager Assets]  のアセットメタデータを編集する様々な方法について説明します。'
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 100%

---

# メタデータの編集と追加 {#how-to-edit-or-add-metadata}

メタデータは、検索可能なアセットに関する追加情報です。画像をアップロードすると自動的に抽出されます。既存のメタデータを編集したり、新しいメタデータプロパティを既存のフィールドに追加（例えば、メタデータフィールドが空白の場合など）したりすることができます。

どの企業でも、メタデータの語彙を制御して信頼性を確保する必要があります。そのため、[!DNL Experience Manager Assets] では、新しいメタデータプロパティをオンデマンドで追加することはできません。作成者は、アセットの新しいメタデータフィールドを追加することはできませんが、開発者は追加できます。[アセットの新しいメタデータプロパティの作成](meta-edit.md#editing-metadata-schema)を参照してください。

## アセットのメタデータの編集 {#editing-metadata-for-an-asset}

メタデータを編集するには、次の手順に従います。

1. 次のいずれかの操作をおこないます。

   * Assets UI でアセットを選択し、ツールバーの「**[!UICONTROL プロパティを表示]**」アイコンを選択します。
   * アセットのサムネールから、「**[!UICONTROL プロパティを表示]**」クイックアクションを選択します。
   * アセットページから、ツールバーの「**[!UICONTROL プロパティを表示]**」を選択します。

   アセットページに、アセットのメタデータが表示されます。このメタデータは、Experience Manager Assets にアップロードされた（取り込まれた）ときに、自動的に抽出されたものです。

1. 必要に応じて、様々なタブの下でメタデータの編集を終えたら、ツールバーの「**[!UICONTROL 保存]**」を選択して、変更内容を保存します。「**[!UICONTROL 閉じる]**」を選択して、Assets web インターフェイスに戻ります。

   >[!NOTE]
   >
   >テキストフィールドが空の場合、現在設定されているメタデータはありません。フィールドに値を入力して保存すると、そのメタデータプロパティを追加できます。

アセットのメタデータへの変更内容は、XMP データの一部として元のバイナリに書き戻されます。この操作は、Experience Manager のメタデータ書き戻しワークフローで実行されます。既存のプロパティ（`dc:title` など）への変更は上書きされ、作成されたプロパティ（`cq:tags` などのカスタムプロパティを含む）はスキーマとともに追加されます。

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## メタデータスキーマの編集 {#editing-metadata-schema}

メタデータスキーマの編集方法について詳しくは、[メタデータスキーマフォームの編集](metadata-schemas.md#edit-metadata-schema-forms)を参照してください。

## Experience Manager でのカスタム名前空間の登録 {#registering-a-custom-namespace-within-aem}

Experience Manager 内で独自の名前空間を追加できます。cq、jcr、sling など事前に定義された名前空間があるように、リポジトリメタデータと xml 処理用の名前空間を設定できます。

1. ノードタイプ管理ページ（*https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*）に移動します。
1. ページ上部の「**[!UICONTROL 名前空間]**」を選択します。ウィンドウに名前空間管理ページが表示されます。

1. 名前空間を追加するには、下部にある「**[!UICONTROL 新規]**」を選択します。
1. XML 名前空間規則に従って、カスタム名前空間を指定（URI 形式の id と、その id に関連付けられている接頭辞を指定）したら、「**[!UICONTROL 保存]**」を選択します。

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
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
