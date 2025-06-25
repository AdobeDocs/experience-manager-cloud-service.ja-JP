---
title: ' [!DNL AEM Assets]  と  [!DNL Figma] の統合'
description: ' [!DNL AEM Assets]  と  [!DNL Figma]  を統合して、デザインワークフロー内の組織のアセットにアクセスして使用する方法  [!DNL Figma]  説明します。'
hide: false
role: User
exl-id: 530561ca-497b-4331-a014-72c561e1ca84
source-git-commit: 41fc6cc1c852c25215a804c2d1f9c5872a46e0a4
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 11%

---

# [!DNL AEM Assets] と [!DNL Figma] の統合{#integrate-aem-assets-with-figma}

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

[!DNL AEM Assets] は、[!DNL Figma] とネイティブに統合されているので、デザイナーは [!DNL Figma] ユーザーインターフェイス内から [!DNL AEM Assets] に保存されているアセットに直接アクセスできます。 [!DNL AEM Assets] で管理されているコンテンツを [!DNL Figma] キャンバスに配置してから、新しいコンテンツや編集したコンテンツを [!DNL AEM Assets] リポジトリに保存することができます。

## 開始する前に{#prerequisites-for-aem-assets-and-figma-integration}

* 最低限必要なAEMのリリースバージョンは `19149` です。

* [!DNL AEM Assets] を [!DNL Figma] と統合するには、有効な [!DNL AEM Assets] ライセンスと [!DNL Figma] ライセンスが必要です。

## [!UICONTROL Adobe Experience Manager（AEM）Assets コネクタへのアクセス ]{#access-aem-assets-connector}

次の手順を実行して、[!UICONTROL Adobe Experience Manager（AEM）Assets コネクタ ] にアクセスします。

1. [!DNL Figma] ホームページで、キャンバスの下部にあるツールバーの **[!UICONTROL アクション]** をクリックし、ダイアログボックスで使用できる検索バーで [!DNL Adobe Experience Manager (AEM) Assets Connector] を検索します。
1. 「[!DNL Adobe Experience Manager (AEM) Assets Connector]」を選択すると、[!DNL Adobe Experience Manager (AEM) Assets Connector] パネルが表示されます。 このパネルを使用して [ [!DNL AEM]  アセットをキャンバスに読み込み ](#import-aem-assets-into-figma-workflow) す  [!DNL Figma] 。
   ![ アクション ](/help/assets/assets/actions-on-figma.png)
または、[!DNL Figma] のコミュニティで使用可能な [[!DNL Adobe Experience Manager (AEM) Assets Connector]](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector) にアクセスして、「**[!UICONTROL 次のウィンドウで開く…]**」をクリックし、最近のファイルを選択するか、新しいファイルを作成します。次に、「**[!UICONTROL 実行]**」をクリックして、[!DNL Adobe Experience Manager (AEM) Assets Connector] パネルにアクセスします。
   ![plugin-page-on-figma-community](/help/assets/assets/plugin-page-on-figma-community.png)

>[!NOTE]
>
> [!DNL AEM] 環境にログインした後に **[!UICONTROL ネットワークエラー]** メッセージが表示された場合は、[Adobe サポートにお問い合わせください ](https://helpx.adobe.com/jp/contact.html)。

## [!DNL AEM] アセットのキャンバスへ [!DNL Figma] 読み込み{#import-aem-assets-into-figma-workflow}

[!DNL Figma] デザインインターフェイス内の [1}Adobe Experience Manager（AEM）Assets Connector] パネルにアクセス ](#access-aem-assets-connector) て、次の手順を実行します。[!UICONTROL 

1. [!UICONTROL Adobe Experience Manager（AEM）Assets コネクタ ] パネルでアセットを検索します。 詳しくは、[ アセットセレクターの使用 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector#using-asset-selector) を参照してください。

1. アセットをキャンバスにドラッグ&amp;ドロップするか、アセットを選択して **[!UICONTROL 選択]** をクリックして、アセットをキャンバスに移動します。

1. フォルダーパスの ![3 つのドット ](/help/assets/assets/three-dots.svg) をクリックすると、現在の階層内のすべての親フォルダーと子フォルダーが表示されます。 その場所に移動するフォルダーを選択します。
   ![3 ドット ](/help/assets/assets/assets-folder-structure.png)

Figma デザインの準備が整ったら、[ アセットをAEM Assets リポジトリに書き出す ](#export-figma-design-to-aem-assets-folder) ことができます。

## リポジトリへのアセット [!DNL AEM Assets] 書き出し{#export-figma-design-to-aem-assets-folder}

[!DNL Figma] デザインインターフェイス内の [[!UICONTROL Adobe Experience Manager （AEM）Assets Connector] パネルにアクセス ](#access-aem-assets-connector) て次の手順を実行し、デザインを [!DNL AEM Assets] リポジトリにエクスポートします。

1. [!DNL Figma] デザインを保存する宛先フォルダーに移動します。 既にフォルダー内にいる場合は、フォルダーパスの「その他のオプション」（![3 つのドット ](/help/assets/assets/three-dots.svg)）をクリックして、別の宛先フォルダーを選択します。
1. オプション：キャンバス上のアセットをグループ化し、フォルダーにアップロードする 1 つのユニットとして選択します。
1. ![ ファイルのアップロード ](/help/assets/assets/upload-icon.svg)**[!UICONTROL アップロード]** をクリックして、**[!UICONTROL アセットをアップロード]** ダイアログボックスを表示します。
1. ダイアログボックスで、ファイル名を指定し、ファイル形式を選択し、**[!UICONTROL 選択した項目]** または **[!UICONTROL ページ]** を選択して、**[!UICONTROL アップロード]** をクリックして、選択したアセットまたはデザイン全体を宛先フォルダーにアップロードします。
   ![figma デザインをアップロード ](/help/assets/assets/upload-figma-design.png)

## 重要な注意点{#Limitations-of-using-aem-assets-into-figma}

この統合には現在、次のような制限があります。

* [!DNL AEM] アセットを Figma に読み込む場合、サポートされる形式は **JPEG**、**PNG** です。
* [!DNL Figma] から [!DNL AEM Assets] にデザインを書き出す場合、サポートされている形式は **PNG**、**PDF**、**JPG**、**SVG** です。

