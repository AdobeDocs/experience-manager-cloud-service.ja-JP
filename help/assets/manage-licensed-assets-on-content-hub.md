---
title: コンテンツハブでのライセンス済みアセットの管理
description: アセットメタデータフォームへのライセンスフィールドの追加、アセットフォルダーへのライセンスメタデータプロパティの適用、使用するライセンスを持つアセットの承認について説明します。
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: a641933d1049cd07ee8935672c8ef357a5bbf18c
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 41%

---

# コンテンツハブでのライセンス済みアセットの管理 {#manage-licensed-assets-on-content-hub}

管理者として、メタデータフォームを編集してアセットライセンスフィールドを含め、AEM オーサー環境のアセットプロパティに表示されるようにします。その後、アセットとそのライセンスを承認して、アセットのライセンスを付与し、コンテンツハブで使用できます。

次の手順を実行します。

1. メタデータフォームを編集して、ライセンスの詳細を含める新しいテキストフィールドを含めます。テキストフィールドを `dc:license` プロパティにマッピングします。メタデータフォームにフィールドを追加してプロパティを定義する方法について詳しくは、[メタデータフォームの設定](/help/assets/metadata-assets-view.md#metadata-forms)を参照してください。
   ![ZIP 抽出](/help/assets/assets/metadata-form-edit.png)
1. メタデータフォームをアセットフォルダーに適用して、手順 1 で組み込んだ設定を適用します。メタデータフォームをアセットフォルダーに割り当てる方法について詳しくは、[フォルダーへのメタデータフォームの割り当て](/help/assets/metadata-assets-view.md#metadata-forms)を参照してください。
1. [ライセンス済み PDF の承認](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. アセットを選択し、「**詳細**」をクリックしてそのプロパティを表示します。手順 1 で追加したライセンスフィールドに、手順 3 で承認済みまたは既に以前に承認済みのアセットライセンスの絶対パスを定義します。コンテンツハブの絶対パスは、`/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)` の標準パターンに従います。例：/content/dam/teamA/projects/documents/file1.pdf
   ![絶対パス](/help/assets/assets/absolute-path.png)
1. アセットを承認して、コンテンツハブで使用できるようにし、「**保存**」をクリックします。アセットの承認方法について詳しくは、[アセットステータスの設定](/help/assets/manage-organize-assets-view.md#set-asset-status)を参照してください。

## よくある質問 {#faqs-manage-licensed-assets-content-hub}

### AEM Assets Content Hubでライセンス済みアセットを管理する目的は何ですか？

Content Hubでライセンス済みアセットを管理すると、管理者は、有効なライセンスを持つ承認済みアセットのみを使用でき、AEM オーサー環境内でコンプライアンスと適切なメタデータトラッキングを維持できます。

### Experience Manager as a Cloud Serviceでアセットのプロパティにライセンスフィールドを追加するにはどうすればよいですか？

アセットのプロパティにライセンスフィールドを追加するには、メタデータフォームを編集して、ライ `dc:license` ンスフィールドにマッピングする新しいテキストフィールドを含めます。 このフィールドは、AEM Assets オーサー環境のアセットプロパティに表示されます。

### アセットフォルダーにメタデータフォームを適用して、アセットのプロパティに「ライセンス」フィールドを含める方法

メタデータフォームを編集し、ライセンスフィールドを含めます。 このメタデータフォームを目的のアセットフォルダーに適用して、そのフォルダー内のすべてのアセットに新しい設定が確実に組み込まれるようにします。

### アセットのライセンス詳細を指定するには

ライセンスの詳細を指定するには、アセットを選択し、「**詳細**」をクリックしてプロパティを表示し、メタデータフォームに追加された「ライセンス」フィールドに、承認済みアセットライセンスの絶対パスを入力します。

### アセットライセンスのContent Hub絶対パスに必要な形式は何ですか？

Content Hubの絶対パスは、/content/dam/（DAM リポジトリー内のアセットのフォルダー階層）/（asset_name）のようなパターンになります。（file_extension）。 （例：`/content/dam/teamA/projects/documents/file1.pdf`）。

### AEM Assets Content Hubで使用できるように、アセットとそのライセンスの両方を承認することが重要なのはなぜですか？

アセットとそのライセンスの両方を承認すると、適切にライセンスを取得され承認されたアセットのみがAEM Assets Content Hubで利用できるようになり、コンプライアンスと適切な使用権限を維持できます。

### ライセンスの承認後にAEM Assets Content Hubでアセットを使用できるようにする方法を教えてください。

アセットのプロパティでライセンスパスを定義したら、アセットを承認して「保存」をクリックします。 これにより、ライセンスが必要なアセットがAEM Assets Content Hubで使用できるようになります。

### Content Hubでライセンスされたアセットを管理する責任者

管理者は、メタデータフォームの編集、アセットフォルダーへの割り当て、Content Hubでのアセットとライセンスの両方の承認を行います。
