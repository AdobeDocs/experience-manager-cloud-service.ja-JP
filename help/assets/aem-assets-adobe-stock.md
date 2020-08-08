---
title: の [!DNL Adobe Stock] 管理セット [!DNL Adobe Experience Manager Assets]。
description: 内部から、検索、取得、ライセンス、 [!DNL Adobe Stock] 管理の各セットを検索します [!DNL Adobe Experience Manager]。 ライセンス済みのアセットを他のデジタルアセットと同様に使用します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 453a8459e042f57820c10fb90f30c2016aa0f5d0
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 24%

---


# ア [!DNL Adobe Stock] セットの使用 [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] サービスは、あらゆるクリエイティブプロジェクトに使用できる、適切にキュレーションされ、著作権使用料が不要で質の高い何百万点もの写真、ベクター、イラスト、ビデオ、テンプレートおよび 3D アセットを提供します。[!DNL Experience Manager] で保存されたアセットは、インター [!DNL Adobe Stock] フェイス上ですばやく検索、プレビュー、ライセンス認証でき [!DNL Experience Manager][!DNL Experience Manager] ます。

## 統合 [!DNL Experience Manager] および [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.

### IMS 設定の作成 {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. 「**[!UICONTROL 作成]**」をクリックし、**[!UICONTROL クラウドソリューション]**／**[!UICONTROL Adobe Stock]** を選択します。
1. 既存の証明書を再使用するか、「**[!UICONTROL 新しい証明書を作成]**」を選択します。
1. 「**[!UICONTROL 証明書を作成]**」をクリックします。証明書を作成したら、公開鍵をダウンロードします。「**[!UICONTROL 次へ]**」をクリックします。
1. Add the downloaded public key to your [!DNL Adobe Developer Console] service account. 「**[!UICONTROL 次へ]**」をクリックします。間もなく値を指定する場合は、 [!UICONTROL AdobeIMSテクニカルアカウント設定] 画面を開いたままにします。
1. Adobe [開発者コンソールにアクセスします](https://console.adobe.io)。 アカウントに、統合が必要な組織の管理者権限があることを確認します。
1. 「 **[!UICONTROL 新しいプロジェクトを]** 作成 **[!UICONTROL 」をクリックし、「]** API」をクリックします。 使用可能なAPIのリストから **[!UICONTROL Adobe Stockを選択します]** 。 「 [!UICONTROL OAUTH 2.0 Web]」を選択します。 表示される様々な値を設定およびコピーします。
1. In [!DNL Experience Manager] provide the values in the fields titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. これらの値について詳しくは、 [JWT認証クイック開始](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)（英語）を参照してください。

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### 設定 [!DNL Adobe Stock] の作成 [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. 「**[!UICONTROL 作成]**」をクリックして設定を作成し、その設定を既存の IMS 設定に関連付けます。環境パラメーターとして「`PROD`」を選択します。
1. 「**[!UICONTROL ライセンスが必要なアセットのパス]**」フィールドの場所をそのまま残します。Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. すべての必須プロパティを追加して作成を完了します。「**[!UICONTROL 保存して閉じる]**」をクリックします。
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>複数の [!DNL Adobe Stock] 設定がある場合は、ユーザ環境設定パネルで目的の設定を選択します。 Experience Managerホームページからパネルにアクセスするには、ユーザーアイコンをクリックし、 **[!UICONTROL ユーザー環境設定]** / **[!UICONTROL Stock設定]**)をクリックします。

## Use and manage [!DNL Adobe Stock] assets in [!DNL Experience Manager] {#usemanage}

Using this capability, organizations can allow its users to work using [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets]. From within the [!DNL Experience Manager] user interface, users can search [!DNL Adobe Stock] assets and license the required assets.

Once an [!DNL Adobe Stock] asset is licensed in [!DNL Experience Manager], it can be used and managed like a typical asset. In [!DNL Experience Manager], the users can search and preview the assets; copy and publish the assets; share the assets on [!DNL Brand Portal]; access and use the assets via [!DNL Experience Manager] desktop app; and so on.

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

### アセットの検索 {#find-assets}

Your [!DNL Experience Manager] users, can search for assets in both, [!DNL Experience Manager] and [!DNL Adobe Stock]. When the search location is not limited to [!DNL Adobe Stock], the search results from [!DNL Experience Manager] and [!DNL Adobe Stock] are displayed.

* To search for [!DNL Adobe Stock] assets, click **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* およ [!DNL Adobe Stock] びにまたがるアセットを検索するには、「検索 [!DNL Experience Manager Assets]![](assets/do-not-localize/search_icon.png)」をクリックします。

また、 アセットを選択するには、検索バーに「`Location: Adobe Stock`」と入力します。[!DNL Adobe Stock][!DNL Experience Manager] は、検索されたアセットに対する高度なフィルタリング機能を備えており、サポートされているアセットのタイプや画像の向き、ライセンスの状態などのフィルターを使用して、必要なアセットをすばやく見つけることができます。

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] アセットは、ユーザーがアセット [!DNL Experience Manager] または [ライセンスを](/help/assets/aem-assets-adobe-stock.md#saveassets) 保存してアセットを保存した後にのみ、リポジトリに取得および保存され [](/help/assets/aem-assets-adobe-stock.md#licenseassets)ます。 Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![検索結果でExperience Managerの検索フィルターとAdobe Stockアセットが強調表示される](assets/aem-search-filters2.jpg)

*図：検索結果でアセット[!DNL Experience Manager]を検索し、ハイライト[!DNL Adobe Stock]表示したフィルター。*

### 必要なアセットの保存と表示 {#saveassets}

Select an asset that you want to save in [!DNL Experience Manager]. Click [!UICONTROL Save] in the toolbar at the top and provide the name and location of the asset. ライセンスが不要なアセットはローカルに透かし付きで保存されます。

Next time when you search for assets, the saved assets are highlighted with a badge, to indicate that such assets are available in [!DNL Experience Manager Assets].

>[!NOTE]
>
>最近追加されたアセットには、ライセンスが許諾されていることを示すバッジではなく、新しいアセットであることを示すバッジが表示されます。

### アセットのライセンス取得 {#licenseassets}

Users can license [!DNL Adobe Stock] assets by using the quota of their [!DNL Adobe Stock] enterprise plan. When you license an asset, it is saved without a watermark and is available for searching and using in [!DNL Experience Manager Assets].

![Experience ManagerアセットのAdobe Stockアセットをライセンス認証し、保存するためのダイアログ](assets/aem-stock_licenseandsave.jpg)

*図：でア[!DNL Adobe Stock]セットのライセンスを取得して保存するダイアログ[!DNL Experience Manager Assets]。*

### メタデータおよびアセットプロパティへのアクセス {#access-metadata-and-asset-properties}

Users can access and preview the metadata, including the [!DNL Adobe Stock] metadata properties for the assets saved in [!DNL Experience Manager], and add **[!UICONTROL License References]** for an asset. However, the updates to license reference are not synced between [!DNL Experience Manager] and [!DNL Adobe Stock] website.

ユーザーは、ライセンスを許諾されたアセットとライセンスを許諾されていないアセットの両方を表示できます。

![保存されているアセットのメタデータとライセンス参照の表示、アクセス](assets/metadata_properties.jpg)

*図：保存されたアセットの表示およびアクセスメタデータとライセンス参照。*

## 既知の制限事項 {#known-limitations}

* **編集画像の警告が表示されない**:画像のライセンスを取得する場合、ユーザは画像が「編集上のみ使用」かどうかを確認できません。 管理者は誤用を防ぐために、Admin Console から編集用アセットへのアクセスをオフにできます。

* **間違ったライセンスの種類が表示される**:アセットに対して、に正しくないライセンスタイプが表示され [!DNL Experience Manager] る可能性があります。 Users can log into the [!DNL Adobe Stock] website to see the license type.

* **参照フィールドとメタデータは同期されません**:ユーザがライセンス参照フィールドを更新すると、そのライセンス参照情報は [!DNL Experience Manager][!DNL Adobe Stock] Webサイト上では更新されません。 Similarly, if the user updates the reference fields on the [!DNL Adobe Stock] website, the updates are not synchronized in [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Experience ManagerアセットでのAdobe Stockアセットの使用に関するビデオチュートリアル](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [Adobe Stock エンタープライズプランのヘルプ](https://helpx.adobe.com/jp/enterprise/using/adobe-stock-enterprise.html)
>* [Adobe Stock の FAQ](https://helpx.adobe.com/jp/stock/faq.html)

