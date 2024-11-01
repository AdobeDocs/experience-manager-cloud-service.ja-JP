---
title: Content Hubでのライセンス取得済みAssetsの管理
description: 様々なメタデータの管理および編集方法について
source-git-commit: 541d5819e19c67eb3f961e41000106178bff66de
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---


# Content Hubでのライセンス取得済みAssetsの管理 {#manage-licensed-assets-on-content-hub}

管理者は、メタデータフォームを編集してアセットライセンスフィールドを含め、AEM オーサー環境のアセットプロパティに表示されるようにします。 その後、アセットとそのライセンスを承認して、アセットのライセンスを取得しContent Hubで使用できるようにします。

次の手順を実行します。

1. メタデータフォームを編集して新しいテキストフィールドを追加し、ライセンスの詳細を含めます。 テキストフィールドをプロパティ `dc:license` マッピングします。 メタデータフォームにフィールドを追加し、プロパティを定義する方法について詳しくは、[ メタデータFormsの設定 ](/help/assets/metadata-assets-view.md#metadata-forms) を参照してください。
   ![ZIP 抽出](/help/assets/assets/metadata-form-edit.png)
1. 手順 1 で取り込んだ設定を適用するには、メタデータフォームをアセットフォルダーに適用します。 メタデータフォームをアセットフォルダーに割り当てる方法について詳しくは、[ メタデータフォームをフォルダーに割り当て ](/help/assets/metadata-assets-view.md#metadata-forms) を参照してください。
1. [ライセンス済みPDFを承認](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. アセットを選択し、「**詳細** をクリックしてそのプロパティを表示します。 手順 1 で追加した「ライセンス」フィールドで、手順 3 で承認された、または既に承認済みのアセットライセンスの絶対パスを定義します。 Content Hubの絶対パスは、次の標準パターンに従います。`/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)` 例：/content/dam/teamA/projects/documents/file1.pdf
   ![ 絶対パス ](/help/assets/assets/absolute-path.png)


