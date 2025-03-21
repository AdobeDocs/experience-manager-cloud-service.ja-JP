---
title: メタデータプロファイル
description: アセットのメタデータプロファイルについて説明します。また、メタデータプロファイルを作成し、フォルダーのアセットに適用する方法も説明します。
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: eef90c6a-b354-4342-8b97-21d067ae2979
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 98%

---

# メタデータプロファイル {#metadata-profiles}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-config.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

メタデータプロファイルを使用すると、フォルダー内のアセットにデフォルトのメタデータを適用できます。メタデータプロファイルを作成し、フォルダーに適用します。後からフォルダーにアップロードしたすべてのアセットは、メタデータプロファイルで設定したデフォルトのメタデータを継承します。

プロファイルがフォルダーに割り当てられることは、Experience Manager Assets でのプロファイルの使用に関する重要な概念です。プロファイル内では、メタデータプロファイルの形式で、ビデオプロファイルまたはイメージプロファイルと共に設定されています。これらの設定は、フォルダーのコンテンツを（そのサブフォルダーコンテンツを含めて）処理します。そのため、ファイルおよびフォルダーの命名方法、サブフォルダーの配置およびこれらのフォルダー内にあるファイルの処理方法は、プロファイルによるこれらのアセットの処理方法に大きな影響を与えます。
ファイルおよびフォルダーの一貫した適切な命名戦略と優れたメタデータプラクティスを使用することで、デジタルアセットコレクションを最大限に活用して、適切なファイルを適切なプロファイルによって処理することができます。

## メタデータプロファイルの追加 {#adding-a-metadata-profile}

1. **[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL メタデータプロファイル]**&#x200B;に移動し、「**[!UICONTROL 作成]**」をクリックします。
1. メタデータプロファイルのタイトル（「サンプルメタデータ」など）を入力し、「**[!UICONTROL 送信]**」を選択します。メタデータプロファイルの「フォームを編集」が表示されます。
1. コンポーネントをクリックし、「**[!UICONTROL 設定]**」タブでプロパティを設定します。例えば、「**[!UICONTROL 説明]**」コンポーネントをクリックして、そのプロパティを編集します。
**[!UICONTROL 説明]**&#x200B;コンポーネントについて、次のプロパティを編集します。

   * **[!UICONTROL フィールドラベル]** - メタデータプロパティの表示名。ユーザーの参照用のみで使用します。
   * **[!UICONTROL プロパティにマッピング]**：このプロパティの値は、リポジトリに保存されているアセットノードへの相対パスまたは名前を提供します。この値は、パスがアセットのノードの下にあることを示すので、常に「`./`」から開始する必要があります。

     「**[!UICONTROL プロパティにマッピング]**」に指定する値は、アセットのメタデータノードの下のプロパティとして格納されます。例えば、次のように指定するとします。「**[!UICONTROL プロパティにマッピング]**」の名前として .`/jcr:content/metadata/dc:desc` を指定すると、[!DNL Adobe Experience Manager Assets] はアセットの metadata ノードに値 `dc:desc` を格納します。

   * **[!UICONTROL デフォルト値]** - メタデータコンポーネントのデフォルト値を追加するには、このプロパティを使用します。例えば、「My description」と指定すると、この値がアセットのメタデータノードの `dc:desc` プロパティに割り当てられます。

     >[!NOTE]
     >
     >（`/jcr:content/metadata` ノードに存在していない）新しいメタデータプロパティにデフォルト値を追加しても、プロパティとその値は、アセットのプロパティページにデフォルトでは表示されません。[!UICONTROL プロパティ]ページに新しいプロパティを表示するには、対応するスキーマフォームを変更します。

1. （オプション）「**[!UICONTROL フォームを作成]**」タブから、「フォームを編集」にコンポーネントを追加し、「**[!UICONTROL 設定]**」タブでプロパティを設定します。「**[!UICONTROL フォームを作成]**」タブでは、次のプロパティを使用できます。

| コンポーネント | プロパティ |
|------------------|----------------------------------------------------|
| セクションヘッダー | フィールドラベル、説明 |
| 1 行のテキスト | フィールドラベル、プロパティにマッピング、デフォルト値 |
| 複数値テキスト | フィールドラベル、プロパティにマッピング、デフォルト値 |
| 数値 | フィールドラベル、プロパティにマッピング、デフォルト値 |
| 日付 | フィールドラベル、プロパティにマッピング、デフォルト値 |
| 標準タグ | フィールドラベル、プロパティにマッピング、デフォルト値、説明 |

1. 「**[!UICONTROL 完了]**」をクリックします。メタデータプロファイルが、**[!UICONTROL メタデータプロファイル]**&#x200B;ページのプロファイルのリストに追加されます。

## メタデータプロファイルのコピー {#copying-a-metadata-profile}

1. **[!UICONTROL メタデータプロファイル]**&#x200B;ページで、コピーを作成するメタデータプロファイルを選択します。
1. ツールバーの「**[!UICONTROL コピー]**」をクリックします。
1. **[!UICONTROL メタデータプロファイルをコピー]**&#x200B;ダイアログで、メタデータプロファイルの新しいコピーのタイトルを入力します。
1. 「**[!UICONTROL コピー]**」をクリックします。メタデータプロファイルのコピーが、**[!UICONTROL メタデータプロファイル]**&#x200B;ページのプロファイルのリストに表示されます。

## メタデータプロファイルの削除 {#deleting-a-metadata-profile}

1. **[!UICONTROL メタデータプロファイル]**&#x200B;ページで、削除するプロファイルを選択します。
1. ツールバーの「**[!UICONTROL メタデータプロファイルを削除]**」をクリックします。
1. ダイアログで、「**[!UICONTROL 削除]**」をクリックして、削除操作を確定します。メタデータプロファイルがリストから削除されます。

## フォルダーへのメタデータプロファイルの適用 {#applying-a-metadata-profile-to-folders}

フォルダーにメタデータプロファイルを割り当てると、サブフォルダーは自動的に親フォルダーのプロファイルを継承します。サブフォルダーに別のプロファイルが適用されると、継承は停止します。1 つのフォルダーに割り当てることができるメタデータプロファイルは 1 つだけです。したがって、アセットをアップロード、保存、使用およびアーカイブする場合のフォルダー構造については慎重に検討してください。

フォルダーに別のメタデータプロファイルを割り当てた場合、新しいプロファイルで以前のプロファイルが上書きされます。既存のフォルダーアセットはそのまま変わりません。新しいプロファイルは、変更後にフォルダーに追加されるアセットに適用されます。特定のフォルダーまたはすべてのアセットにグローバルにメタデータプロファイルを適用できます。

プロファイルが割り当てられているフォルダーは、ユーザーインターフェイスでカード名にプロファイルの名前が表示されます。

後で変更した既存のメタデータプロファイルが存在するフォルダー内のアセットを再処理できます。<!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### 特定のフォルダーへのメタデータプロファイルの適用 {#applying-metadata-profiles-to-specific-folders}

**[!UICONTROL ツール]**&#x200B;メニュー内から、またはフォルダー内にいる場合は「**[!UICONTROL プロパティ]**」から、メタデータプロファイルをフォルダーに適用できます。この節では、メタデータプロファイルをフォルダーに適用する両方の方法について説明します。

既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

後で変更した既存のビデオプロファイルが存在するフォルダー内のアセットを再処理できます。<!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### プロファイルユーザーインターフェイスからのフォルダーへのメタデータプロファイルの適用 {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. **[!UICONTROL ツール／アセット／メタデータプロファイル]**&#x200B;に移動します。
1. 1 つまたは複数のフォルダーに適用するメタデータプロファイルを選択します。
1. 「**[!UICONTROL メタデータプロファイルをフォルダーに適用]**」をクリックし、新たにアップロードしたアセットを受け取る 1 つ以上のフォルダーを選択して、「**[!UICONTROL 完了]**」をクリックします。既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

#### 「プロパティ」からのフォルダーへのメタデータプロファイルの適用  {#applying-metadata-profiles-to-folders-from-properties}

1. 左パネルで、「**[!UICONTROL アセット]**」をクリックし、メタデータプロファイルを適用するフォルダーに移動します。
1. チェックマークを選択して対象のフォルダーを選択し、「**プロパティ**」をクリックします。
1. 「**[!UICONTROL メタデータプロファイル]**」タブを選択し、ドロップダウンメニューからプロファイルを選択して、「**[!UICONTROL 保存]**」をクリックします。既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

### メタデータプロファイルのグローバルな適用 {#applying-a-metadata-profile-globally}

特定のフォルダーにプロファイルを適用できるだけでなく、グローバルにプロファイルを適用することもできます。これにより、[!DNL Experience Manager Assets] にアップロードされている、任意のフォルダー内にある任意のコンテンツに、選択したプロファイルを適用できます。

後で変更した既存のメタデータプロファイルが存在するフォルダー内のアセットを再処理できます。<!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**メタデータプロファイルをグローバルに適用するには、次のいずれかを行います。**

* `https://[aem_server]/mnt/overlay/dam/gui/content/assets/v2/foldersharewizard.html/content/dam` に移動して適切なプロファイル適用し、「**[!UICONTROL 保存]**」をクリックします。

* CRXDE Lite で、`/content/dam/jcr:content` ノードに移動します。`metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` プロパティを追加します。「**すべて保存**」をクリックします。

## フォルダーからのメタデータプロファイルの削除 {#removing-a-metadata-profile-from-folders}

フォルダーからメタデータプロファイルを削除すると、サブフォルダーは自動的に親フォルダーのプロファイルの削除状態を継承します。ただし、フォルダー内で実行されたファイルの処理はそのまま維持されます。

**ツール**&#x200B;メニュー内で、またはフォルダー内にいる場合は「**プロパティ**」で、メタデータプロファイルをフォルダーから削除できます。この節では、メタデータプロファイルをフォルダーから削除する両方の方法について説明します。

### プロファイルユーザーインターフェイスを使用したフォルダーからのメタデータプロファイルの削除 {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Experience Manager のロゴをクリックし、**[!UICONTROL ツール／Assets／メタデータプロファイル]**&#x200B;に移動します。
1. 1 つ以上のフォルダーから削除するメタデータプロファイルを選択します。
1. 「**[!UICONTROL フォルダーからメタデータプロファイルを削除]**」をクリックし、プロファイルを削除する 1 つ以上のフォルダーを選択して、「**[!UICONTROL 完了]**」をクリックします。

   名前がフォルダー名の下に表示されなくなっていることで、メタデータプロファイルがフォルダーに適用されていないことを確認できます。

### 「プロパティ」を使用したフォルダーからのメタデータプロファイルの削除  {#removing-metadata-profiles-from-folders-via-properties}

1. Experience Manager のロゴをクリックして「**[!UICONTROL アセット]**」に移動した後、メタデータプロファイルを削除するフォルダーに移動します。
1. チェックマークをクリックして対象のフォルダーを選択し、「**[!UICONTROL プロパティ]**」をクリックします。
1. 「**[!UICONTROL メタデータプロファイル]**」タブを選択し、ドロップダウンメニューから「**[!UICONTROL なし]**」を選択して、「**[!UICONTROL 保存]**」をクリックします。既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

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
