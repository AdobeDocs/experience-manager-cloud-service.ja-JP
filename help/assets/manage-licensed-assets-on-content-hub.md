---
title: Content Hubでのライセンス取得済みAssetsの管理
description: アセットメタデータフォームへの「ライセンス」フィールドの追加、アセットフォルダーへの「ライセンス」メタデータプロパティの適用、使用するライセンスを持つアセットの承認について説明します。
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 2%

---

# Content Hubでのライセンス取得済みAssetsの管理 {#manage-licensed-assets-on-content-hub}

>[!AVAILABILITY]
>
>Content Hub ガイドがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE Content Hub ガイドのPDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

管理者は、メタデータフォームを編集してアセットライセンスフィールドを含め、AEM オーサー環境のアセットプロパティに表示されるようにします。 その後、アセットとそのライセンスを承認して、アセットのライセンスを取得しContent Hubで使用できるようにします。

次の手順を実行します。

1. メタデータフォームを編集して新しいテキストフィールドを追加し、ライセンスの詳細を含めます。 テキストフィールドをプロパティ `dc:license` マッピングします。 メタデータフォームにフィールドを追加し、プロパティを定義する方法について詳しくは、[ メタデータFormsの設定 ](/help/assets/metadata-assets-view.md#metadata-forms) を参照してください。
   ![ZIP 抽出](/help/assets/assets/metadata-form-edit.png)
1. 手順 1 で取り込んだ設定を適用するには、メタデータフォームをアセットフォルダーに適用します。 メタデータフォームをアセットフォルダーに割り当てる方法について詳しくは、[ メタデータフォームをフォルダーに割り当て ](/help/assets/metadata-assets-view.md#metadata-forms) を参照してください。
1. [ライセンス済みPDFを承認](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. アセットを選択し、「**詳細** をクリックしてそのプロパティを表示します。 手順 1 で追加した「ライセンス」フィールドで、手順 3 で承認された、または既に前に承認されたアセットライセンスの絶対パスを定義します。 Content Hubの絶対パスは、次の標準パターンに従います。`/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)` 例：/content/dam/teamA/projects/documents/file1.pdf
   ![ 絶対パス ](/help/assets/assets/absolute-path.png)
1. アセットを承認してContent Hubで使用できるようにし、「**保存**」をクリックします。 アセットの承認方法について詳しくは、[ アセットステータスの設定 ](/help/assets/manage-organize-assets-view.md#set-asset-status) を参照してください。
