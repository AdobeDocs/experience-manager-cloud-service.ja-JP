---
title: メタデータプロファイル
description: アセットのメタデータプロファイルについて理解します。また、メタデータプロファイルを作成し、フォルダーのアセットに適用する方法も学習します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# メタデータプロファイル {#metadata-profiles}

メタデータプロファイルを使用すると、フォルダー内のアセットに初期設定のメタデータを適用できます。メタデータプロファイルを作成し、フォルダーに適用します。その後フォルダーにアップロードするアセットは、メタデータプロファイルで設定したデフォルトのメタデータを継承します。

<!-- See [Profiles for Processing Metadata, Images, and Videos](processing-profiles.md).

See also [Best Practices for Organizing your Digital Assets for using Processing Profiles](/help/assets/best-practices-for-file-management.md).

-->

## メタデータプロファイルの追加 {#adding-a-metadata-profile}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Metadata Profiles]**, and then tap  **[!UICONTROL Create]**.
1. Enter a title for the Metadata Profile, for example Sample Metadata, and tap **[!UICONTROL Submit]**. メタデータプロファイルの「フォームを編集」が表示されます。
1. Click a component and configure its properties in the **[!UICONTROL Settings]** tab. For example, click the **[!UICONTROL Description]** component and edit its properties.
Edit the following properties for the **[!UICONTROL Description]** component:

   * **[!UICONTROL Field Label]** — メタデータプロパティの表示名。 ユーザーの参照用のみで使用します。
   * **[!UICONTROL Map to Property]** — このプロパティの値は、リポジトリに保存されるアセットノードへの相対パス/名前を提供します。この値は、パスがアセットのノード `./` の下にあることを示しているので、常にで始まる必要があります。

      The value you specify for **[!UICONTROL Map to property]** is stored as a property under the asset&#39;s metadata node. For example, if you specify . `/jcr:content/metadata/dc:desc` aem Assetsは、プロパテ **[!UICONTROL ィにマップの名前として]**、アセットのメタデ `dc:desc` ータノードに値を格納します。

   * **[!UICONTROL デフォルト値]** — このプロパティを使用して、メタデータコンポーネントのデフォルト値を追加します。 For example, if you specify &quot;My description&quot; then this value is assigned to the property `dc:desc` at the asset&#39;s metadata node.

      >[!NOTE]
      >
      >新しいメタデータプロパティにデフォルト値を追加する（にまだ存在しない）。ノー `/jcr:content/metadata` ド)は、初期設定ではアセットのプロパティページにプロパティとその値を表示しません。 アセットのプロパティページに新しいプロパティを表示するには、対応するスキーマフォームを変更します。

1. (Optional) Add more components to the Edit Form from the **[!UICONTROL Build Form]** tab, and configure their properties in the **[!UICONTROL Settings]** tab. The following properties are available from the **[!UICONTROL Build Form]** tab:

| コンポーネント | プロパティ |
|------------------|----------------------------------------------------|
| セクションヘッダー | フィールドラベル、説明 |
| 1 行のテキスト | フィールドラベル、プロパティにマップ、デフォルト値 |
| 複数値テキスト | フィールドラベル、プロパティにマップ、デフォルト値 |
| 番号 | フィールドラベル、プロパティにマップ、デフォルト値 |
| 日付 | フィールドラベル、プロパティにマップ、デフォルト値 |
| 標準タグ | フィールドラベル、プロパティにマップ、デフォルト値、説明 |

1. 「**[!UICONTROL Done]**」をタップします。メタデータプロファイルが、**[!UICONTROL メタデータプロファイル]**&#x200B;ページのプロファイルのリストに追加されます。

## メタデータプロファイルのコピー {#copying-a-metadata-profile}

1. From the **[!UICONTROL Metadata Profiles]** page, select a Metadata Profile to make a copy of it.
1. ツールバー **[!UICONTROL から]** 「コピー」をタップします。
1. **[!UICONTROL メタデータプロファイルをコピー]**&#x200B;ダイアログで、メタデータプロファイルの新しいコピーのタイトルを入力します。
1. 「**[!UICONTROL コピー]**」をタップします。メタデータプロファイルのコピーが、**[!UICONTROL メタデータプロファイル]**&#x200B;ページのプロファイルのリストに表示されます。

## メタデータプロファイルの削除 {#deleting-a-metadata-profile}

1. **[!UICONTROL メタデータプロファイル]**&#x200B;ページで、削除するプロファイルを選択します。
1. Tap **[!UICONTROL Delete Metadata Profiles]** in the toolbar.
1. ダイアログで、「**[!UICONTROL 削除]**」をクリックして、削除操作を確定します。メタデータプロファイルがリストから削除されます。

## Apply a metadata profile to folders {#applying-a-metadata-profile-to-folders}

フォルダーにメタデータプロファイルを割り当てると、サブフォルダーは自動的に親フォルダーのプロファイルを継承します。つまり、フォルダーに適用できるのは 1 つのメタデータプロファイルのみとなります。そのため、アセットをアップロード、保存、使用およびアーカイブする場所のフォルダー構造については入念に検討してください。

フォルダーに異なるメタデータプロファイルを割り当てた場合、新しいプロファイルが以前のプロファイルよりも優先されます。以前に存在していたフォルダーのアセットは変更されずに維持されます。新しいプロファイルは、その後にフォルダーに追加されるアセットに対して適用されます。

プロファイルが割り当てられているフォルダーは、ユーザーインターフェイスでカード名にプロファイルの名前が表示されます。

特定のフォルダーまたはすべてのアセットにグローバルにメタデータプロファイルを適用できます。

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### Apply metadata profiles to specific folders {#applying-metadata-profiles-to-specific-folders}

**[!UICONTROL ツール]**&#x200B;メニュー内から、またはフォルダー内にいる場合は「**[!UICONTROL プロパティ]**」から、メタデータプロファイルをフォルダーに適用できます。このセクションでは、メタデータプロファイルをフォルダーに適用する両方の方法について説明します。

既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

You can reprocess assets in a folder that already has an existing video profile that you later changed. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### Apply metadata profiles to folders from Profiles user interface {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. 1 つまたは複数のフォルダーに適用するメタデータプロファイルを選択します。
1. Tap **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and tap **[!UICONTROL Done]**. 既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

#### Apply metadata profiles to folders from Properties {#applying-metadata-profiles-to-folders-from-properties}

1. In the left rail, tap **[!UICONTROL Assets]** then navigate to the folder that you want to apply a metadata profile to.
1. On the folder, tap or click the check mark to select it and then tap or click **Properties**.
1. Select the **[!UICONTROL Metadata Profiles]** tab and select the profile from the drop-down menu and tap **Save]**. 既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

### Apply a metadata profile globally {#applying-a-metadata-profile-globally}

特定のフォルダーにプロファイルを適用できるだけでなく、グローバルにプロファイルを適用することもできます。これにより、AEM アセットにアップロードされている、すべてのフォルダー内にあるすべてのコンテンツに、選択したプロファイルを適用できます。

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**メタデータプロファイルをグローバルに適用するには、次のいずれかの操作を行います**

* 適切なプロフ `https://<AEM server>/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` ァイルに移動して適用し、「保存」をタッ **プします**。

* Navigate to CRXDE Lite to the following node: `/content/dam/jcr:content`. プロパティを追加し、「す `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` べて保存」 **をタップしま**&#x200B;す。

## フォルダーからのメタデータプロファイルの削除 {#removing-a-metadata-profile-from-folders}

フォルダーからメタデータプロファイルを削除すると、サブフォルダーは自動的に親フォルダーのプロファイルの削除状態を継承します。ただし、フォルダー内で実行されたファイルの処理はそのまま維持されます。

You can remove a metadata profile from a folder from within the **Tools** menu or if you are in the folder, from the **Properties**. このセクションでは、メタデータプロファイルをフォルダーから削除する両方の方法について説明します。

### プロファイルユーザーインターフェイスを使用したフォルダーからのメタデータプロファイルの削除 {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Tap or click the AEM logo and navigate to **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. 1 つまたは複数のフォルダーから削除するメタデータプロファイルを選択します。
1. Tap **[!UICONTROL Remove Metadata Profile from Folder(s)]** and select the folder or multiple folders you want use to remove a profile from and tap **[!UICONTROL Done]**.

   名前がフォルダー名の下に表示されなくなっていることで、メタデータプロファイルがフォルダーに適用されていないことを確認できます。

### 「プロパティ」を使用したフォルダーからのメタデータプロファイルの削除{#removing-metadata-profiles-from-folders-via-properties}

1. Tap the AEM logo and navigate **[!UICONTROL Assets]** and then to the folder that you want to remove an metadata profile from.
1. On the folder, tap the check mark to select it and then tap **[!UICONTROL Properties]**.
1. 「**[!UICONTROL メタデータプロファイル]**」タブを選択し、ドロップダウンメニューから「**[!UICONTROL なし]**」を選択して、「**[!UICONTROL 保存]**」をクリックします。既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。
