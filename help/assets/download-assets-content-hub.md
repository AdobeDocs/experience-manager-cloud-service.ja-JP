---
title: Content Hub からのアセットのダウンロード
description: 1 つまたは複数のアセットとそのレンディションを Content Hub ポータルからダウンロードする方法について説明します。
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 37b5404f0814abb3605a26e7933cc3a01ebcf96e
workflow-type: ht
source-wordcount: '831'
ht-degree: 100%

---

# Content Hub からのアセットのダウンロード {#download-assets}

[!DNL Content Hub] では、アセットをダウンロードして共有できます。[!DNL Content Hub] のユーザーインターフェイスには、承認済みアアセットのみが表示されます。これらのアセットには、画像、ビデオ、またはその他のデジタルコンテンツが含まれる場合があります。[!DNL Content Hub] では、効果的なアセット配布用のアクセシビリティと適応性が強化されます。

[!DNL Content Hub] を使用して、1 つまたは複数のアセットとその使用可能なレンディションをダウンロードできます。

[Content Hub での使用可能なレンディションのタイプ](#types-of-renditions)を参照してください。

## 1 つ以上のアセットとそのレンディションのダウンロード {#download-asset-renditions}

1 つ以上のアセットとそのレンディションをダウンロードするには、次の手順を実行します。

1. アセットをダウンロードするには、アセットカードで使用可能な「![ダウンロード](/help/assets/assets/download-icon.svg)」を選択し、アセットのプレビューを表示します。次に、使用可能なレンディションを選択し、ダイアログボックスの「**[!UICONTROL ダウンロード]**」オプションをクリックして、選択したレンディションを ZIP ファイルとしてダウンロードします。ダイアログボックスに（ライセンス済みアセットの）アセットライセンスが表示された場合は、ライセンス条件に同意し、「**[!UICONTROL ダウンロード]**」をクリックします。
   ![](/help/assets/assets/download-an-asset-CH-from-asset-card.png)

   または、アセットのサムネイルをクリックして「![ダウンロード](/help/assets/assets/download-icon.svg)」を選択し、ダイアログボックスで使用可能なレンディションを選択して表示してからダウンロードすることもできます。

1. 複数のアセットをダウンロードするには、アセットを選択し、![ダウンロード](/help/assets/assets/download-icon.svg) **[!UICONTROL ダウンロード]** をクリックして、**[!UICONTROL アセットをダウンロード]**&#x200B;ダイアログボックスで選択したアセットのリストを確認します。アセットの横にある「![選択解除](/help/assets/assets/Close.svg)」をクリックして、リストから選択を解除します。1 つ以上のレンディションを選択し、「**[!UICONTROL ダウンロード]**」をクリックして、単一の ZIP ファイルとしてダウンロードします。**[!UICONTROL スマート切り抜き]**&#x200B;および&#x200B;**[!UICONTROL 静的レンディション]**を選択すると、選択した各アセットの使用可能なすべての静的およびスマート切り抜きレンディションがダウンロードされます。
   ![複数のアセットのダウンロード](/help/assets/assets/download-multiple-assets-CH.png)
ダウンロードの進行中も [!DNL Content Hub] を引き続き使用できます。Content Hub は、ダウンロードプロセス中にワークフローを中断しません。
   ![複数のアセットのダウンロード](/help/assets/assets/download-assets-notification-ch.png)
**[!UICONTROL アセットをダウンロード]**&#x200B;ダイアログボックスにアセットライセンスが表示されている場合、左側のウィンドウ（「[!UICONTROL T&amp;C ドキュメント]」セクション）から各ライセンスを選択してライセンスをプレビューし、ダイアログボックスの中央のウィンドウに、ライセンスに関連付けられた選択したアセットを表示します。各ライセンスを確認したら、レンディションを選択し、「**[!UICONTROL 上記の利用条件を読んで同意しました]**」をクリックし、「**[!UICONTROL ダウンロード]**」を選択してダウンロードします。
   ![複数のアセットのダウンロード](/help/assets/assets/download-multiple-licensed-assets-CH.png)

   >[!NOTE]
   >
   >* レンディションは、[[!UICONTROL 設定]](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)ユーザーインターフェイスを使用して表示が有効になっている場合にのみ表示されます。
   >* [[!DNL Dynamic Media with Open API capabilities]](/help/assets/dynamic-media-open-apis-overview.md) へのアクセス権を持つユーザーは、動的およびスマート切り抜きレンディションを表示およびダウンロードできます。
   >* ライセンスのプレビューは、アセットが [!DNL Assets as a Cloud Service] オーサリング環境を使用して承認された場合にのみ表示されます。詳しくは、[コンテンツハブのライセンス済みアセットの管理](/help/assets/manage-licensed-assets-on-content-hub.md)を参照してください。

<!--

## Download an asset and its renditions {#download-asset-renditions} 

To download an asset and its renditions, execute the following steps: 

1. Click the asset to view its properties.

1. Click ![download](/help/assets/assets/download-icon.svg) to see the list of available asset renditions in the **[!UICONTROL Download]** panel.

   >[!NOTE]
   >
   >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
   >* You can download all [static, dynamic, and smart crop renditions](#types-of-renditions) while downloading an asset.

1. Select one or more renditions and click **[!UICONTROL Download]** to download the selected renditions as a zip file. 
While downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** before clicking **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

   ![Download single asset renditions](/help/assets/assets/download-single-asset-renditions.png)


If you are downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

>[!NOTE]
>
> The users with access to [Dynamic Media with Open API capabilities](/help/assets/dynamic-media-open-apis-overview.md) can view and download dynamic and smart crop renditions.

## Download multiple assets and their renditions {#download-multiple-assets-renditions} 

To download multiple assets and their renditions, execute the following steps: 

1. Select the assets and click ![download](/help/assets/assets/download-icon.svg) **[!UICONTROL Download]**. The [!UICONTROL Download assets] screen displays listing all the selected assets. 
1. Click **[!UICONTROL Download]** to select from the various download options to begin download:

    * **Download [!UICONTROL Originals]**: Select this option to download the selected assets in the original form.
    * **Download [!UICONTROL Static Renditions only]**: Select this option to download all available static renditions of assets except the original assets.
    * **Download [!UICONTROL Originals & Static Renditions]**: Select this option to download both original and static renditions of the selected assets. 

      ![Download multiple renditions](/help/assets/assets/download-multiple-renditions.png)

      >[!NOTE]
      >
      >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
      >* You can only download [static renditions](#types-of-renditions) while downloading multiple assets.

    If any of the selected asset is a licensed asset, click the license of the asset in left pane to see its preview, which enables you to select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

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

詳しくは、[ [!DNL Experience Manager Assets]](/help/assets/renditions.md) でのレンディションの表示と管理を参照してください。

[!DNL Experience Manager Assets] では、次のレンディションのタイプをサポートしています。

* [静的レンディション](/help/assets/renditions.md#static-renditions)：静的レンディションは、デジタルアセットの事前生成されたバージョンで、通常はアセットの取り込みまたは変更中に作成されます。これらは、web サムネイル、レスポンシブデザイン用のモバイルに対応した形式、印刷用の高解像度ファイルなど、特定の用途とプラットフォーム用に最適化され、効率化された一貫したエクスペリエンスを提供します。

* [動的レンディション](/help/assets/renditions.md#dynamic-renditions)：動的レンディションは、様々なデバイスの解像度に合わせた画像のサイズ変更や、様々な縦横比に合わせた切り抜きなど、様々なアクションを実行するために、リアルタイムでカスタマイズされたアセットバージョンです。これらのレンディションにより、より広範な要件に合わせて、パーソナライズおよび最適化されたエクスペリエンスを提供できます。アセットの動的レンディションは、[!DNL Adobe Experience Manager Assets] オーサー環境で作成されます。動的レンディションを有効にするために必要な手順について詳しくは、[動的レンディションの有効化](#enable-dynamic-media-renditions)を参照してください。

* [スマート切り抜き](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)：スマート切り抜きは、切り抜きプロセス中にアセットの重要な部分にのみ焦点を当てます。Dynamic Media のスマート切り抜きでは、Adobe Sensei を使用した人工知能を活用して目標地点を追跡し、アセットがすべての画面サイズで最適に表示されるようにします。[!DNL Adobe Experience Manager] のスマート切り抜きでは、タイトルと共にアセットレンディションの幅と高さが表示されます。詳しくは、[AEM Assets Dynamic Media でのスマート切り抜きの使用](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use)を参照してください。

  スマート切り抜きレンディションは、[OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) にアクセスできる場合にのみ表示され、ダウンロードできます。スマート切り抜きレンディションは、画像アセットに対してのみ使用できます。

  ![レンディションタイプ](/help/assets/assets/renditions-types.png)

  >[!NOTE]
  > 
  > ダウンロードパネルには、カスタムの静的レンディションのみが表示されます。デフォルトの `cq5dam.*` サムネールは、コンテンツハブには表示されません。

### 動的レンディションの有効化 {#enable-dynamic-media-renditions}

動的レンディションを有効にするには：

1. [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) にアクセスできることを確認します。

   OpenAPI 機能を備えた Dynamic Media にアクセスできると、`Approved` としてマークされたすべてのアセットを Dynamic Media を使用して公開配信できます。

1. コンテンツハブのアセットのみを承認するには、[アセットの承認ターゲット](/help/assets/approve-assets-content-hub.md#set-approval-target)をコンテンツハブに設定します。

1. [設定](/help/assets/configure-content-hub-ui-options.md#access-configuration-options-content-hub)ユーザーインターフェイスの「**[!UICONTROL レンディション]**」タブにある「**[!UICONTROL レンディションの可用性を有効にする]**」切替スイッチを有効にします。

1. 既存の画像プリセットを再保存して、コンテンツハブで使用できるようにします。これは、OpenAPI を備えた Dynamic Media に新しくオンボードした場合にのみ適用されます。

   既存の画像プリセットを再保存するには、管理ビューに移動し、**[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL 画像プリセット]**&#x200B;を選択します。プリセットを選択し、「**[!UICONTROL 編集]**」をクリックして、「**[!UICONTROL 保存]**」をクリックします。



   >[!NOTE]
   > 
   > 動的レンディションは、画像アセットに対してのみ使用できます。



