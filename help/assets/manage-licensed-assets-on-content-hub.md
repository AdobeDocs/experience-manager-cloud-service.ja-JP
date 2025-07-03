---
title: コンテンツハブでのライセンス済みアセットの管理
description: アセットメタデータフォームへのライセンスフィールドの追加、アセットフォルダーへのライセンスメタデータプロパティの適用、使用するライセンスを持つアセットの承認について説明します。
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: ht
source-wordcount: '251'
ht-degree: 100%

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
