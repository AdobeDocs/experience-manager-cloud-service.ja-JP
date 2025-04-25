---
title: コンテンツハブからのアセットのダウンロード
description: コンテンツハブポータルからアセットをダウンロードする方法について説明します。
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: e108d25f3cdc025e0fbe8010854f245f62786baf
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 80%

---

# コンテンツハブからのアセットのダウンロード {#download-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime と Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets と Edge Delivery Services の統合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Dynamic Media Prime と Ultimate の有効化</b></a>
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

<!-- ![Download assets](assets/download-asset.jpg) -->
![アセットのダウンロード](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>コンテンツハブガイドを PDF 形式で利用できるようになりました。ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えてください。
>
>[!BADGE コンテンツハブガイドの PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

コンテンツハブでは、アセットをダウンロードして共有できます。コンテンツハブのユーザーインターフェイスには、承認済みアアセットのみが表示されます。これらのアセットには、画像、ビデオ、またはその他のデジタルコンテンツが含まれる場合があります。コンテンツハブでは、効果的なアセット配布用のアクセシビリティと適応性が強化されます。

コンテンツハブを使用して、1 つまたは複数のアセットとその使用可能なレンディションをダウンロードできます。

[コンテンツハブでの使用可能なレンディションのタイプ](#types-of-renditions)を参照してください。

## アセットとそのレンディションのダウンロード {#download-asset-renditions}

アセットとそのレンディションをダウンロードするには、次の手順を実行します。

1. アセットをクリックして、そのプロパティを表示します。

1. ![ダウンロード](/help/assets/assets/download-icon.svg) をクリックして、ダウンロードプロセスを開始します。ダウンロードパネルには、使用可能なすべてのアセットレンディションがリストされます。

   >[!NOTE]
   >
   >* レンディションは、[設定](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)ユーザーインターフェイスを使用して表示が有効になっている場合にのみ表示されます。
   >* アセットのダウンロード中に、すべての[静的、動的、スマート切り抜きレンディション](#types-of-renditions)をダウンロードできます。

1. 1 つ以上のレンディションを選択し、「**[!UICONTROL ダウンロード]**」をクリックします。

   ![1 つのアセットレンディションをダウンロード](/help/assets/assets/download-single-asset-renditions.png)


ライセンス済みアセットをダウンロードする場合は、「**[!UICONTROL 上記のすべての利用条件を読み、同意しました]**」を選択し、「**[!UICONTROL ダウンロード]**」をクリックします。また、「**[!UICONTROL 利用条件]**」をクリックしてアセットライセンスを表示することもできます。ライセンスのプレビューは、アセットが Assets as a Cloud Service オーサリング環境を使用して承認された場合にのみ表示されます。詳しくは、[コンテンツハブのライセンス済みアセットの管理](/help/assets/manage-licensed-assets-on-content-hub.md)を参照してください。

>[!NOTE]
>
> [Open API を備えた Dynamic Media 機能](/help/assets/dynamic-media-open-apis-overview.md)にアクセスできるユーザーは、動的およびスマート切り抜きレンディションを表示およびダウンロードできます。

## 複数のアセットとそのレンディションのダウンロード {#download-multiple-assets-renditions}

複数のアセットとそのレンディションをダウンロードするには、次の手順を実行します。

1. アセットを選択し、![ダウンロード](/help/assets/assets/download-icon.svg)「**[!UICONTROL ダウンロード]**」をクリックします。[!UICONTROL アセットをダウンロード]画面に、選択したすべてのアセットがリストされます。
1. 「**[!UICONTROL ダウンロード]**」をクリックして、様々なダウンロードオプションから選択し、ダウンロードを開始します。

   * **オリジナル[!UICONTROL をダウンロード]**：選択したアセットを元の形式でダウンロードするには、このオプションを選択します。
   * **静的レンディションのみ[!UICONTROL をダウンロード]**：元のアセットを除く、アセットの使用可能なすべての静的レンディションをダウンロードするには、このオプションを選択します。
   * **オリジナルと静的レンディション[!UICONTROL をダウンロード]**：選択したアセットのオリジナルと静的レンディションの両方をダウンロードするには、このオプションを選択します。

     ![複数のレンディションをダウンロード](/help/assets/assets/download-multiple-renditions.png)

     >[!NOTE]
     >
     >* レンディションは、[設定](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)ユーザーインターフェイスを使用して表示が有効になっている場合にのみ表示されます。
     >* 複数のアセットのダウンロード中にのみ、[静的レンディション](#types-of-renditions)をダウンロードできます。

   選択したアセットのいずれかがライセンス済みアセットである場合は、左側のパネルでアセットのライセンスをクリックしてプレビューを表示して、「**[!UICONTROL 上記のすべての利用条件を読み、同意しました]**」を選択し、「**[!UICONTROL ダウンロード]**」をクリックできます。ライセンスのプレビューは、アセットが Assets as a Cloud Service オーサリング環境を使用して承認された場合にのみ表示されます。詳しくは、[コンテンツハブのライセンス済みアセットの管理](/help/assets/manage-licensed-assets-on-content-hub.md)を参照してください。

   <!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

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


## レンディションのタイプ {#types-of-renditions}

アセットレンディションは、アセットの元のファイルを様々に表現したものです。これらには、サムネイル、web またはモバイル用に最適化されたバージョン、透かし入りまたは DRM で保護されたファイル、さらにはスマート切り抜きなどの動的要素を含めることができます。元のファイルタイプと一致する必要はなく、代わりに、様々なユースケースでアセットを表すために機能します。

詳しくは、[Experience Manager Assets でのレンディションの表示と管理](/help/assets/renditions.md)を参照してください。

[!DNL Experience Manager Assets] では、次のレンディションのタイプをサポートしています。

* [静的レンディション](/help/assets/renditions.md#static-renditions)：静的レンディションは、デジタルアセットの事前生成されたバージョンで、通常はアセットの取り込みまたは変更中に作成されます。これらは、web サムネイル、レスポンシブデザイン用のモバイルに対応した形式、印刷用の高解像度ファイルなど、特定の用途とプラットフォーム用に最適化され、効率化された一貫したエクスペリエンスを提供します。

* [動的レンディション](/help/assets/renditions.md#dynamic-renditions)：動的レンディションは、様々なデバイスの解像度に合わせた画像のサイズ変更や、様々な縦横比に合わせた切り抜きなど、様々なアクションを実行するために、リアルタイムでカスタマイズされたアセットバージョンです。これらのレンディションにより、より広範な要件に合わせて、パーソナライズされ最適化されたエクスペリエンスを提供できます。アセットの動的レンディションは、オーサー環境 [!DNL Adobe Experience Manager Assets] 作成されます。 動的レンディションを有効にするために必要な手順について詳しくは、[ 動的レンディションの有効化 ](#enable-dynamic-media-renditions) を参照してください。

* [スマート切り抜き](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)：スマート切り抜きは、切り抜きプロセス中にアセットの重要な部分にのみ焦点を当てます。Dynamic Media のスマート切り抜きでは、Adobe Sensei を使用した人工知能を活用して目標地点を追跡し、アセットがすべての画面サイズで最適に表示されるようにします。[!DNL Adobe Experience Manager] のスマート切り抜きでは、タイトルと共にアセットレンディションの幅と高さが表示されます。詳しくは、[AEM Assets Dynamic Media でのスマート切り抜きの使用](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use)を参照してください。

  スマート切り抜きレンディションは、[OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) にアクセスできる場合にのみ表示され、ダウンロードできます。 スマート切り抜きレンディションは、画像アセットでのみ使用できます。

  ![レンディションタイプ](/help/assets/assets/renditions-types.png)

### 動的レンディションの有効化 {#enable-dynamic-media-renditions}

動的レンディションを有効にするには：

1. [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) にアクセスできることを確認します。

   OpenAPI 機能で Dynamic Media にアクセスできるようになると、`Approved` としてマークされたすべてのアセットは Dynamic Media を使用して公開配信できます。

1. Content Hubに対してのみアセットを承認する場合は、「[ アセットの承認ターゲット ](/help/assets/approve-assets-content-hub.md#set-approval-target)」を「Content Hub」に設定します。

1. **[!UICONTROL 設定]** ユーザーインターフェイスの **[!UICONTROL レンディション]** タブで使用可能な [ レンディションの可用性を有効にする ](/help/assets/configure-content-hub-ui-options.md#access-configuration-options-content-hub) トグルを有効にします。

1. 既存の画像プリセットを再保存して、Content Hubで使用できるようにします。 OpenAPI を使用して Dynamic Media に新しくオンボーディングした場合にのみ適用されます。

   既存の画像プリセットを再度保存するには、管理者ビューに移動し、**[!UICONTROL ツール]**/**[!UICONTROL Assets]**/ **[!UICONTROL 画像プリセット]** を選択します。 プリセットを選択し、「**[!UICONTROL 編集]**」をクリックしてから、「**[!UICONTROL 保存]** をクリックします。



   >[!NOTE]
   > 
   > 動的レンディションは、画像アセットでのみ使用できます。



