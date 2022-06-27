---
title: WorkfrontとExperience Manager Assetsの間でのアセットメタデータマッピングの設定
description: Adobe Workfrontと Assetas a Cloud Serviceアプリケーションの間で、アセットメタデータフィールドをマッピングします。 メタデータフィールドのマッピングの結果、WorkfrontからExperience Manager Assetsにアセットを送信する際に、マッピングされたアセットメタデータをExperience Manager Assetsで表示できます。
source-git-commit: 212ecb5330de739b2e479d36462953ce33697c1c
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 10%

---

# Adobe WorkfrontとExperience Manager Assetsの間でのアセットメタデータマッピングの設定 {#asset-metadata-mapping-workfront-aem-assets}

アセットメタデータフィールドは、Adobe Workfrontと Assetas a Cloud Serviceアプリケーションの間でExperience Managerをマッピングできます。 メタデータフィールドのマッピングの結果、WorkfrontからExperience Manager Assetsにアセットを送信する際に、マッピングされたアセットメタデータをExperience Manager Assetsで表示できます。

例えば、画像をExperience Manager Assetsに送信する際に、画像の名前、説明、画像が属するプロジェクトのメタデータフィールドをWorkfrontで保持する必要がある場合は、これらのフィールドを設定してExperience Manager Assetsプロパティにマッピングします。

**ユースケース**

画像 `add-users-workfront.png` が `Metadata Syncs` プロジェクトをAdobe Workfrontアプリケーションで使用します。 次のメタデータを使用して、その画像をExperience Manager Assetsas a Cloud Serviceに送信する必要があります。

* プロジェクト名

* Document Name

* ドキュメントの説明

## 前提条件 {#prerequisites}

* WorkfrontおよびExperience Manager Assetsas a Cloud Serviceアプリケーションへの管理者アクセス

* 統合 [WorkfrontおよびExperience Manager Assetsas a Cloud Serviceアプリケーション](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus).

## Workfrontでのメタデータマッピングの設定 {#set-up-metadata-mapping}

Workfrontの「プロジェクト名」、「ドキュメント名」および「ドキュメントの説明」フィールドのメタデータマッピングを設定するには、次の手順に従います。

1. メインメニューアイコンをクリックします。 ![メニューを表示](assets/show-menu.svg) Adobe Workfrontアプリケーションの右上隅にある「 」をクリックし、 **[!UICONTROL 設定]**.

1. 選択 **[!UICONTROL ドキュメント]** 左のパネルで、「 **[!UICONTROL Experience Manager Assets]**.

1. Experience Manager Assets統合を選択し、 **[!UICONTROL 編集]**.

1. クリック **[!UICONTROL メタデータ]**. 内 **[!UICONTROL Assets]** タブ、マップ [!UICONTROL プロジェクト] > [!UICONTROL 名前] Workfrontフィールドから `wm:projectName` Experience Manager Assetsフィールド。 完全一致が見つからない場合、Adobeでは、WorkfrontとExperience Manager Assetsのフィールドをマッピングするうえで最適な一致を探すことをお勧めします。 様々なデータタイプのフィールドをマッピングするのを避けることができます。 例えば、日付のWorkfrontフィールドを説明の Assets フィールドにマッピングするとします。
1. を [!UICONTROL 文書] > [!UICONTROL 名前] Workfrontフィールドから `wm:documentName` Experience Manager Assetsフィールド。

   ![Workfrontでのマッピング](assets/workfront-metadata-mapping.png)

1. を [!UICONTROL 文書] > [!UICONTROL 説明] Workfrontフィールドから `dc:description` Experience Manager Assetsフィールド。

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## WorkfrontからExperience Manager Assetsに画像を送信 {#send-image-workfront-assets}

WorkfrontからExperience Manager Assetsに画像を送信するには：

1. メインメニューアイコンをクリックします。 ![メニューを表示](assets/show-menu.svg) Adobe Workfrontアプリケーションの右上隅にある「 」をクリックし、 **[!UICONTROL プロジェクト]**.

1. クリック **[!UICONTROL 新規プロジェクト]** をクリックして、新しいプロジェクトを作成します。

1. クリック **[!UICONTROL ドキュメント]** 「 」オプションが左側のウィンドウに表示されている場合は、ドラッグして、Experience Manager Assetsに送信する必要のある画像を選択します。

1. クリック **[!UICONTROL 送信先]**」で、「 Experience Manager Assets Essentials 統合名」を選択します。

   ![AEMに送信](assets/send-to-aem.png)

1. アセットの保存先フォルダーを選択し、「 **[!UICONTROL フォルダーを選択]**.

1. 「**[!UICONTROL 保存]**」をクリックします。

## アセットメタデータマッピングのExperience Manageras a Cloud Service {#metadata-mapping-aem}

後 [Adobe Workfrontでのアセットメタデータマッピングの設定](#set-up-metadata-mapping)を使用する場合、Experience Manager Assets as a Cloud Serviceアプリケーションで同じマッピングを使用して、画像に適したメタデータの結果を表示する必要があります。

メタデータのマッピングは、Experience Manager Assetsのメタデータスキーマを使用して実行されます。 新しく追加したメタデータスキーマフォームまたは既存のメタデータスキーマフォームを編集できます。メタデータスキーマフォームには、タブとタブ内のフォーム項目が含まれています。これらのフォーム項目を CRX リポジトリーのメタデータノード内のフィールドにマップしたり、フォーム項目を設定したりできます。タブまたはフォーム項目をメタデータスキーマフォームに追加できます。詳しくは、 [メタデータスキーマ](metadata-schemas.md).

Experience Manager Assets as a Cloud Serviceで新しいメタデータフォームを使用してメタデータマッピングを設定するには：

1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。

1. ツールバーから「**[!UICONTROL 作成]**」をクリックします。ダイアログで、スキーマフォームのタイトルを入力し、「**[!UICONTROL 作成]**」をクリックして、フォーム作成プロセスを完了します。

1. スキーマフォームを選択し、 **[!UICONTROL 編集]**.

1. （オプション）メタデータスキーマフォームエディターで、 `+` をクリックして、Workfrontフィールド用の新しいタブを作成します。

1. 次をクリック： **[!UICONTROL フォームを作成]** タブをクリックし、 **[!UICONTROL 1 行のテキスト]** コンポーネントをフォームに追加します。 フォームのコンポーネントをクリックします。 内 **[!UICONTROL フォームを作成]** タブ：

   1. 指定 `Project Name` 内 **[!UICONTROL フィールドラベル]** フィールドに入力します。

   1. 指定 `./jcr:content/metadata/wm:projectName` 内 **[!UICONTROL プロパティにマッピング]** フィールドに入力します。 ガイドラインとして、次のテンプレートを使用して Experience Manager Assets のフィールドマッピングを定義します。
      `./jcr:content/metadata/<mapping defined for the field in workfront>`

      Workfrontでマッピングを設定する際に、マッピングをおこないました `wm:projectName` 「Experience Manager Assets」フィールドから「プロジェクト/Workfrontに名前を付ける」フィールドに移動します。

      `wm` は名前空間名を参照し、 `projectName` は、プロパティのタイトルを指します。 以下を使用： `namespace:propertyTitle` 形式を使用して、メタデータフィールドのマッピングを定義します。

      ![AEMに送信](assets/metadata-schema-mapping.png)

1. 次をクリック： **[!UICONTROL フォームを作成]** タブをクリックし、 **[!UICONTROL 1 行のテキスト]** コンポーネントをフォームに追加します。 フォームのコンポーネントをクリックします。 内 **[!UICONTROL フォームを作成]** タブ：

   1. 指定 `Document Name` 内 **[!UICONTROL フィールドラベル]** フィールドに入力します。

   1. 指定 `./jcr:content/metadata/wm:documentName` 内 **[!UICONTROL プロパティにマッピング]** フィールドに入力します。
Workfrontでマッピングを設定する際に、マッピングをおこないました `wm:documentName` 「Experience Manager Assets」フィールドから「ドキュメント/Workfrontに名前を付ける」フィールドに移動します。

1. 次をクリック： **[!UICONTROL フォームを作成]** タブをクリックし、 **[!UICONTROL 複数行テキスト]** コンポーネントをフォームに追加します。 フォームのコンポーネントをクリックします。 内 **[!UICONTROL フォームを作成]** タブ：

   1. 指定 `Document Description` 内 **[!UICONTROL フィールドラベル]** フィールドに入力します。

   1. 指定 `./jcr:content/metadata/dc:description` 内 **[!UICONTROL プロパティにマッピング]** フィールドに入力します。
Workfrontでマッピングを設定する際に、マッピングをおこないました `dc:description` 「Experience Manager Assets」フィールドから「ドキュメント/説明Workfront」フィールドに移動します。

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## 画像フォルダーへのメタデータ設定の適用 {#apply-metadata-settings-image-folder}

as a Cloud ServiceのExperience Managerでメタデータ設定を行った後、 [Workfrontアプリケーションから送信された画像を含むフォルダー](#send-image-workfront-assets).

画像フォルダーにメタデータ設定を適用するには：

1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。

1. 使用可能なリストからメタデータスキーマを選択し、「 **[!UICONTROL フォルダーに適用]**.

1. 保存先フォルダを選択 [画像はAdobe Workfrontアプリケーションから送信されます](#send-image-workfront-assets) をクリックし、 **[!UICONTROL 適用]**.

Experience Manager Assetsの画像に移動して、その画像に関連付けられているメタデータを表示できます。 画像を選択し、 **[!UICONTROL プロパティ]** をクリックして、画像のメタデータを表示します。



