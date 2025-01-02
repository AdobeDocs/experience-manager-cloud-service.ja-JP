---
title: コンテンツハブからのアセットのダウンロード
description: コンテンツハブポータルからアセットをダウンロードする方法について説明します。
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 28424cb184d0378669498c78e571961227f6539a
workflow-type: ht
source-wordcount: '439'
ht-degree: 100%

---

# コンテンツハブからのアセットのダウンロード {#download-assets}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Download assets](assets/download-asset.jpg) -->
![アセットのダウンロード](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>コンテンツハブガイドを PDF 形式で利用できるようになりました。ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えてください。
>
>[!BADGE コンテンツハブガイドの PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

コンテンツハブでは、アセットをダウンロードして共有できます。コンテンツハブのユーザーインターフェイスには、承認済みアアセットのみが表示されます。これらのアセットには、画像、ビデオ、またはその他のデジタルコンテンツが含まれる場合があります。コンテンツハブでは、効果的なアセット配布用のアクセシビリティと適応性が強化されます。

コンテンツハブを使用して、1 つまたは複数のアセットとその使用可能なレンディションをダウンロードできます。

## アセットとそのレンディションのダウンロード {#download-asset-renditions}

アセットとそのレンディションをダウンロードするには、次の手順を実行します。

1. アセットをクリックして、そのプロパティを表示します。

1. ![ダウンロード](/help/assets/assets/download-icon.svg) をクリックして、ダウンロードプロセスを開始します。ダウンロードパネルには、使用可能なすべてのアセットレンディション（オリジナルとその他のレンディション）がリストされます。

   >[!NOTE]
   >
   レンディションは、[設定](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)ユーザーインターフェイスを使用して表示が有効になっている場合にのみ表示されます。

1. レンディションを選択し、「**[!UICONTROL ダウンロード]**」をクリックします。

   ![1 つのアセットレンディションをダウンロード](/help/assets/assets/download-single-asset-renditions.png)


ライセンス済みアセットをダウンロードする場合は、「**[!UICONTROL 上記のすべての利用条件を読み、同意しました]**」を選択し、「**[!UICONTROL ダウンロード]**」をクリックします。また、「**[!UICONTROL 利用条件]**」をクリックしてアセットライセンスを表示することもできます。ライセンスのプレビューは、アセットが Assets as a Cloud Service オーサリング環境を使用して承認された場合にのみ表示されます。詳しくは、[コンテンツハブのライセンス済みアセットの管理](/help/assets/manage-licensed-assets-on-content-hub.md)を参照してください。

## 複数のアセットとそのレンディションのダウンロード {#download-multiple-assets-renditions}

複数のアセットとそのレンディションをダウンロードするには、次の手順を実行します。

1. アセットを選択し、![ダウンロード](/help/assets/assets/download-icon.svg)「**[!UICONTROL ダウンロード]**」をクリックします。[!UICONTROL アセットをダウンロード]画面に、選択したすべてのアセットがリストされます。
1. 「**[!UICONTROL ダウンロード]**」をクリックして、様々なダウンロードオプションから選択し、ダウンロードを開始します。

   * **オリジナル[!UICONTROL をダウンロード]**：選択したアセットを元の形式でダウンロードするには、このオプションを選択します。
   * **レンディションのみ[!UICONTROL をダウンロード]**：元のアセットを除く、アセットの使用可能なすべてのレンディションをダウンロードするには、このオプションを選択します。
   * **オリジナルとすべてのレンディション[!UICONTROL をダウンロード]**：選択したアセットのオリジナルとレンディションの両方をダウンロードするには、このオプションを選択します。

     ![複数のレンディションをダウンロード](/help/assets/assets/download-multiple-renditions.png)

     >[!NOTE]
     >
     レンディションは、[設定](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)ユーザーインターフェイスを使用して表示が有効になっている場合にのみ表示されます。

   選択したアセットのいずれかがライセンス済みアセットである場合は、左側のパネルでアセットのライセンスをクリックしてプレビューを表示して、「**[!UICONTROL 上記のすべての利用条件を読み、同意しました]**」を選択し、「**[!UICONTROL ダウンロード]**」をクリックできます。ライセンスのプレビューは、アセットが Assets as a Cloud Service オーサリング環境を使用して承認された場合にのみ表示されます。詳しくは、[コンテンツハブのライセンス済みアセットの管理](/help/assets/manage-licensed-assets-on-content-hub.md)を参照してください。

   ![複数ライセンスをダウンロード](/help/assets/assets/download-multiple-license.png)

<!--1. On the Content Hub homepage, select the asset and click **Download**. The **Download assets** dialog box displays a license or list of licenses associated with the selected assets in the left pane. 
1. Click a license in the left pane to see its PDF in the middle pane and the associated assets with it in the right pane. The license PDF preview is displayed only if the license is approved in your Assets as a Cloud Service environment. [Approve the license PDFs](/help/assets/approve-assets-content-hub.md) of the selected assets to see their previews.
1. Optional: Click ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the dialog box.
1. Select **I have read and accept all the terms and conditions mentioned above.** 
1. Click **Download** to download the selected assets.-->

<!---This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the preview of the associated assets to the license in the right. Reviewed licenses are highlighted in light blue.


The dialog box that displays depends on whether the download list includes expired assets or only non-expired assets. <br/>
**Download expired assets dialog box:** This dialog box displays the expired assets' preview along with their expiry date in the left pane. The expired assets' count out of total selected displays in the right pane. Click **Proceed with all assets** to download expired assets with other assets (if present). The Download assets dialog box displays. See the [Download assets dialog box](#Download-asset-dialog-box) to proceed further.
    
    >[!NOTE]
    >
    >[Enable the download option for expired assets](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub) to download them. Only expired assets that have enabled downloading are available for download.

   <a id="Download-asset-dialog-box"></a> **Download assets dialog box:** This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the associated assets' preview and their count in the right pane. Reviewed licenses are highlighted in light blue.

    >[!NOTE]
    >
    > The **Download Asset dialog box** previews licensing terms and conditions only for approved licenses. [Approve the assets' licenses](/help/assets/approve-assets-content-hub.md) before downloading them to preview their licensing terms in the **Download Asset dialog box**.

1. Click  ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the download dialog box. 

1. Accept the terms and conditions and then click **Download** to download assets associated with the available licenses in the left pane.-->
<!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

<!---
### Download non-licensed Assets {#download-non-licensed-assets}

 To download non-licensed assets, select the assets and click ![download](/help/assets/assets/download-icon.svg) from the top rail.-->







