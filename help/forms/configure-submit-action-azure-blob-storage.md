---
Title: How to connect AEM Adaptive Forms with Azure Blob Storage?
Description: Learn how to create an Azure Blob Storage Configuration in AEM Forms and use it within your Adaptive Forms for efficient data storage.
keywords: AEM Formsとの Azure Blob ストレージ統合、Azure ストレージへのデータの送信、AEM Formsでの Azure ストレージ設定の作成、アダプティブForms送信アクションでの Azure Blob ストレージの使用
feature: Adaptive Forms, Core Components
source-git-commit: 8784c0bcd05eeae41a472faa5ecad03cbdd8a9b6
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 66%

---


# アダプティブフォームを Azure Blob ストレージに送信する

「**[!UICONTROL Azure Blob Storage に送信]**」送信アクションは、アダプティブフォームを Microsoft Azure Portal に接続します。フォームデータ、ファイル、添付ファイル、またはレコードのドキュメントを、接続された Azure Storage コンテナに送信できます。

AEM as a Cloud Serviceには、フォーム送信を処理するための標準の様々な送信アクションが用意されています。 これらのオプションについて詳しくは、 [アダプティブフォーム送信アクション](/help/forms/configure-submit-actions-core-components.md) 記事。

## メリット

AEM Formsとの Azure Blob Storage 統合の利点の一部を次に示します。

* これにより、アダプティブフォームのデータ、ファイル、添付ファイル、レコードのドキュメントを Azure Storage コンテナに送信するプロセスを合理化できます。
* アダプティブフォーム送信の一元化された整理されたストレージに Azure Blob ストレージを使用します。

## AEM FormsとMicrosoft® Azure Blob Storage の接続

アダプティブForms送信アクションで Azure Blob ストレージを使用するには：

1. [Azure Blob Storage コンテナの作成](#create-a-azure-blob-storage-container-create-azure-configuration)：AEM Forms を Azure Storage コンテナに接続します。
2. [アダプティブフォームでの Azure ストレージ設定の使用](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af)：アダプティブフォームを、設定済みの Azure ストレージコンテナに接続します。

### Azure Blob Storage コンテナの作成 {#create-azure-configuration}

AEM Forms を Azure ストレージコンテナに接続するには、次の手順に従います。
1. **AEM Forms オーサー**&#x200B;インスタンス／**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Azure ストレージ]**&#x200B;に移動します。
1. **[!UICONTROL Azure ストレージ]**&#x200B;を選択すると、**[!UICONTROL Azure ストレージブラウザー]**&#x200B;にリダイレクトされます。
1. **設定コンテナ**&#x200B;を選択します。設定は、選択した設定コンテナに保存されます。
1. 「**[!UICONTROL 作成]**」をクリックします。Azure ストレージ設定の作成ウィザードが表示されます。

   ![Azure ストレージ設定](/help/forms/assets/azure-storage-configuration.png)

1. 「**[!UICONTROL タイトル]**」、「**[!UICONTROL Azure ストレージアカウント]**」および「**[!UICONTROL Azure アクセスキー]**」を指定します。

   * `Azure Storage Account` の名前と `Azure Access key` は、Microsoft Azure Portal のストレージアカウントから取得できます。

1. 「**[!UICONTROL 保存]**」をクリックします。

アダプティブフォームの送信アクションに、この Azure ストレージコンテナ設定を使用できるようになりました。

### アダプティブフォームでの Azure ストレージ設定の使用 {#use-azure-storage-configuartion-in-af}

アダプティブフォームで作成した Azure ストレージコンテナ設定を使用して、データや生成済みレコードのドキュメントを Azure ストレージコンテナに保存できます。 アダプティブフォームで Azure ストレージコンテナ設定を使用するには、次の手順を実行します。
1. [アダプティブフォーム](/help/forms/creating-adaptive-form-core-components.md)を作成します。

   >[!NOTE]
   >
   > * OneDrive ストレージを作成したアダプティブ フォームと同じ[!UICONTROL 設定コンテナ]を選択します。
   > * [!UICONTROL 設定コンテナ]が選択されていない場合、グローバルな[!UICONTROL ストレージ設定]フォルダーが送信アクションのプロパティウィンドウに表示されます。

1. 「**送信アクション**」を「**[!UICONTROL Azure Blob Storage に送信]**」として選択します。
   ![Azure Blob Storage GIF](/help/forms/assets/azure-submit-video.gif)

1. データを保存する場所に「**[!UICONTROL ストレージ設定]**」を選択します。
1. 「**[!UICONTROL 保存]**」をクリックして、送信設定を保存します。

フォームを送信すると、データは指定された Azure ストレージコンテナ設定に保存されます。
データを保存するフォルダー構造は `/configuration_container/form_name/year/month/date/submission_id/data` です。

## 関連記事

{{af-submit-action}}