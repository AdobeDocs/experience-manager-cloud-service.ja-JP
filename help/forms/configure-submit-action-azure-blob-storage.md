---
title: Azure Blob Storage に AEM アダプティブフォームを接続する方法
description: AEM Forms で Azure Blob Storage 設定を作成し、アダプティブフォーム内で使用して、効率的なデータストレージを実現する方法について説明します。
keywords: AEM Forms との Azure Blob Storage の統合、Azure ストレージへのデータの送信、AEM Forms での Azure ストレージ設定の作成、アダプティブフォーム送信アクションでの Azure Blob Storage の使用
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
exl-id: 0c9f8f85-c4e9-4c79-bd0b-abdcac99a2d4
role: User, Developer
source-git-commit: 44a8d5d5fdd2919d6d170638c7b5819c898dcefe
workflow-type: ht
source-wordcount: '818'
ht-degree: 100%

---

# Azure Blob Storage にアダプティブフォームを送信する

**[!UICONTROL Azure Blob Storage に送信]**&#x200B;の送信アクションは、アダプティブフォームを Microsoft® Azure Portal に接続します。フォームデータ、ファイル、添付ファイルまたはレコードのドキュメントを、接続された Azure ストレージコンテナに送信できます。

AEM as a Cloud Service では、フォーム送信を処理するための様々な送信アクションが標準で提供されます。これらのオプションについて詳しくは、[アダプティブフォーム送信アクション](/help/forms/aem-forms-submit-action.md)の記事を参照してください。

## メリット

AEM Forms との Azure Blob Storage の統合のメリットの一部を次に示します。

* アダプティブフォームのデータ、ファイル、添付ファイルおよびレコードのドキュメントを Azure ストレージコンテナに送信するプロセスを効率化するのに役立ちます。
* アダプティブフォーム送信の一元化された、整理されたストレージに Azure Blob Storage を使用します。

## Microsoft® Azure Blob Storage との AEM Forms の接続

アダプティブフォーム送信アクションで Azure Blob Storage を使用するには、次の手順に従います。

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
<!--

    >[!NOTE]
    >
    > The URL for **[!UICONTROL Azure Blob Endpoint]** is automatically appended to the textbox when a value is entered for **[!UICONTROL Azure Storage Account]**. You can update the Azure Blob End Point URL with your custom domain. Steps to update URL for **[!UICONTROL Azure Blob End Point]**:
    > 1. [Enable the AEM Advance Networking VPN support](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=ja)
    > 1. [Enable dedicated egress IP link](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=ja)
    > 1. [Map custom domain to azure blob storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal)
-->

1. 「**[!UICONTROL 保存]**」をクリックします。

アダプティブフォームの送信アクションに、この Azure ストレージコンテナ設定を使用できるようになりました。

### アダプティブフォームでの Azure ストレージ設定の使用 {#use-azure-storage-configuartion-in-af}

アダプティブフォームで作成した Azure ストレージコンテナ設定を使用して、データや生成済みレコードのドキュメントを Azure ストレージコンテナに保存できます。

>[!NOTE]
>
> * OneDrive ストレージを作成したアダプティブ フォームと同じ[!UICONTROL 設定コンテナ]を選択します。
> * [!UICONTROL 設定コンテナ]が選択されていない場合、グローバルな[!UICONTROL ストレージ設定]フォルダーが送信アクションのプロパティウィンドウに表示されます。

>[!BEGINTABS]

>[!TAB 基盤コンポーネント]

基盤コンポーネントに基づくアダプティブフォームで Azure ストレージコンテナ設定を使用するには、次の手順を実行します。

1. 編集用にアダプティブフォームを開き、アダプティブフォームのコンテナプロパティの「**[!UICONTROL 送信]**」セクションに移動します。
1. **[!UICONTROL 送信アクション]**&#x200B;ドロップダウンリストから、「**[!UICONTROL Azure Blob Storage に送信]**」を選択します。

   ![Azure Blob Storage GIF](/help/forms/assets/submit-to-azure-blob-fc.png){width=50%,height=50%}

   Azure Blob Storage にレコードのドキュメント（DoR）を保存することもできます。

1. データを保存する場所に「**[!UICONTROL ストレージ設定]**」を選択します。
1. 「**[!UICONTROL 保存]**」をクリックして、送信設定を保存します。

フォームを送信すると、データは指定された Azure ストレージコンテナ設定に保存されます。
データを保存するフォルダー構造は `/configuration_container/form_name/year/month/date/submission_id/data` です。

>[!TAB コアコンポーネント]

コアコンポーネントに基づくアダプティブフォームで Azure ストレージコンテナ設定を使用するには、次の手順を実行します。

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブをクリックします。
1. **[!UICONTROL 送信アクション]**&#x200B;ドロップダウンリストから、「**[!UICONTROL Azure Blob Storage に送信]**」を選択します。

   ![Azure Blob Storage GIF](/help/forms/assets/azure-submit-video.gif)

   Azure Blob Storage にレコードのドキュメント（DoR）を保存することもできます。

1. データを保存する場所に「**[!UICONTROL ストレージ設定]**」を選択します。
1. 「**[!UICONTROL 保存]**」をクリックして、送信設定を保存します。

フォームを送信すると、データは指定された Azure ストレージコンテナ設定に保存されます。
データを保存するフォルダー構造は `/configuration_container/form_name/year/month/date/submission_id/data` です。

>[!TAB ユニバーサルエディター]

ユニバーサルエディターでオーサリングされたアダプティブフォームで Azure ストレージコンテナ設定を使用するには、次の手順を実行します。

1. アダプティブフォームを編集用に開きます。
1. エディターで&#x200B;**フォームプロパティを編集**拡張機能をクリックします。
**フォームプロパティ**&#x200B;ダイアログが表示されます。

   >[!NOTE]
   >
   > * ユニバーサルエディターインターフェイスに **フォームプロパティを編集** アイコンが表示されない場合は、Extension Manager で&#x200B;**フォームプロパティを編集**&#x200B;拡張機能を有効にします。
   > * ユニバーサルエディターで拡張機能を有効または無効にする方法については、[Extension Manager 機能のハイライト](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)の記事を参照してください。

1. 「**送信**」タブをクリックし、「**[!UICONTROL Azure Blob Storage に送信]**」送信アクションを選択します。
   ![Azure Blob Storage](/help/forms/assets/azure-blob-storage-ue.png)

   「**添付ファイルを元の名前で保存**」を選択した場合、添付ファイルは元のファイル名を使用してフォルダーに保存されます。Azure Blob Storage にレコードのドキュメント（DoR）を保存することもできます。

1. データを保存する場所に「**[!UICONTROL ストレージ設定]**」を選択します。
1. 「**[!UICONTROL 保存して閉じる]**」をクリックして、送信設定を保存します。

フォームを送信すると、データは指定された Azure ストレージコンテナ設定に保存されます。
データを保存するフォルダー構造は `/configuration_container/form_name/year/month/date/submission_id/data` です。

>[!ENDTABS]

## 関連記事

{{af-submit-action}}
