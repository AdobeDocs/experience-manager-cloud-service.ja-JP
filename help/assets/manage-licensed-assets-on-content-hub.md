---
title: コンテンツハブでのライセンス済みアセットの管理
description: アセットメタデータフォームへのライセンスフィールドの追加、アセットフォルダーへのライセンスメタデータプロパティの適用、使用するライセンスを持つアセットの承認について説明します。
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: 230ca753bd5f3d5b26b30a962a526dc0edfc9bd4
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 44%

---

# コンテンツハブでのライセンス済みアセットの管理 {#manage-licensed-assets-on-content-hub}

管理者として、メタデータフォームを編集してアセットライセンスフィールドを含め、AEM オーサー環境のアセットプロパティに表示されるようにします。 その後、アセットとそのライセンスを承認して、アセットのライセンスを付与し、コンテンツハブで使用できます。

次の手順を実行します。

1. メタデータフォームを編集して、ライセンスの詳細を含める新しいテキストフィールドを含めます。 テキストフィールドを `dc:license` プロパティにマッピングします。 メタデータフォームにフィールドを追加してプロパティを定義する方法について詳しくは、[メタデータフォームの設定](/help/assets/metadata-assets-view.md#metadata-forms)を参照してください。   ![ZIP 抽出](/help/assets/assets/metadata-form-edit.png)
1. メタデータフォームをアセットフォルダーに適用して、手順 1 で組み込んだ設定を適用します。 メタデータフォームをアセットフォルダーに割り当てる方法について詳しくは、[フォルダーへのメタデータフォームの割り当て](/help/assets/metadata-assets-view.md#metadata-forms)を参照してください。
1. [ライセンス済み PDF の承認](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. アセットを選択し、「**詳細**」をクリックしてそのプロパティを表示します。 手順 1 で追加したライセンスフィールドに、手順 3 で承認済みまたは既に以前に承認済みのアセットライセンスの絶対パスを定義します。 コンテンツハブの絶対パスは、`/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)` の標準パターンに従います。 例：/content/dam/teamA/projects/documents/file1.pdf   ![絶対パス](/help/assets/assets/absolute-path.png)
1. アセットを承認して、コンテンツハブで使用できるようにし、「**保存**」をクリックします。 アセットの承認方法について詳しくは、[アセットステータスの設定](/help/assets/manage-organize-assets-view.md#set-asset-status)を参照してください。

## よくある質問 {#faqs-manage-licensed-assets-content-hub}

### AEM Assets Content Hubでライセンス済みアセットを管理する目的は何ですか？

AEM Assets Content Hubでライセンス済みアセットを管理することで、管理者は有効なライセンスを持つ承認済みアセットのみを使用できるようにし、コンプライアンスとAEM オーサー環境内での適切なメタデータトラッキングを維持できます。

### Experience Manager as a Cloud Serviceのアセットプロパティにライセンスフィールドを追加するにはどうすればよいですか？

AEM Assets ビューで、メタデータフォームを編集して、`dc:license` プロパティにマッピングされた新しいテキストフィールドを含めることで、アセットプロパティにライセンスフィールドを追加できます。 このフィールドは、AEM Assets オーサー環境のアセットプロパティに表示されます。

### AEM Assetsのアセットプロパティにライセンスフィールドを含めるために、メタデータフォームをアセットフォルダーに適用する方法を教えてください。

AEM Assets ビューで、メタデータフォームを編集して、ライセンスフィールドを含めます。 このメタデータフォームを目的のアセットフォルダーに適用し、そのフォルダー内のすべてのアセットに新しい設定が組み込まれるようにします。

### AEM Assets ビューでアセットのライセンスの詳細を指定するにはどうすればよいですか？

ライセンスの詳細を指定するには、アセットを選択し、**詳細**&#x200B;をクリックしてプロパティを表示し、メタデータフォームに追加されたライセンスフィールドに承認済みアセットライセンスの絶対パスを入力します。

### アセットライセンスのAEM Assets Content Hub絶対パスに必要なフォーマットは何ですか？

Content Hubの絶対パスは、/content/dam/（DAM リポジトリ内のアセットのフォルダー階層）/（asset_name）。（file_extension）というパターンに従う必要があります。 （例：`/content/dam/teamA/projects/documents/file1.pdf`）。

### AEM Assets Content Hubでアセットを使用できるようにするために、アセットとそのライセンスの両方を承認することが重要なのはなぜですか？

アセットとライセンスの両方を承認することで、AEM Assets Content Hubでは適切なライセンスが付与されたアセットのみが使用できるようになり、コンプライアンスと適切な使用権限を維持できます。

### ライセンス承認後にAEM Assets Content Hubでアセットを使用できるようにするにはどうすればよいですか？

アセットのプロパティでライセンスパスを定義したら、アセットを承認し、「保存」をクリックします。 これにより、AEM Assets Content Hubでライセンス済みアセットを使用できるようになります。

### AEM Assets Content Hubでライセンスされたアセットを管理する責任は誰ですか？

管理者は、メタデータフォームの編集、アセットフォルダーへの割り当て、AEM Assets Content Hubでのアセットとライセンスの両方の承認を担当します。


**関連情報**

* [アセットを翻訳](/help/assets/translate-assets.md)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](/help/assets/file-format-support.md)
* [アセットを検索](/help/assets/search-assets.md)
* [接続されたアセット](/help/assets/use-assets-across-connected-assets-instances.md)
* [アセットレポート](/help/assets/asset-reports.md)
* [メタデータスキーマ](/help/assets/metadata-schemas.md)
* [アセットをダウンロード](/help/assets/download-assets-from-aem.md)
* [メタデータを管理](/help/assets/manage-metadata.md)
* [Dynamic Media テンプレートの管理](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [レポートの管理](/help/assets/manage-reports-assets-view.md)
* [検索ファセット](/help/assets/search-facets.md)
* [コレクションを管理](/help/assets/manage-collections.md)
* [メタデータの一括読み込み](/help/assets/metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
