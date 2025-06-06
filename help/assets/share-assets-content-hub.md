---
title: ' [!DNL the Content Hub] でのアセットの共有'
description: ' [!DNL the Content Hub] でのアセットの共有'
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 0e66b355d09e2fd2c4c8a5ddacc9b2d033b41bf2
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 19%

---

# コンテンツハブでのアセットの共有 {#search-assets-as-a-link}

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

![アセットの共有のバナー画像](assets/share-assets-banner.png)

>[!AVAILABILITY]
>
>コンテンツハブガイドを PDF 形式で利用できるようになりました。ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えてください。
>
>[!BADGE コンテンツハブガイドの PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

選択したアセットへのリンクを作成して、他のユーザーと簡単に共有できるようにします。 認証済みの [!DNL Content Hub] ユーザーとして、[!DNL Content Hub] 環境で使用可能な 1 つ以上のアセットを選択し、リンクを生成して、他のプライベートまたはパブリックのユーザーに送信します。

## 前提条件 {#prerequisites}

[Content Hub ユーザー ](deploy-content-hub.md#onboard-content-hub-users) 選択したアセットへのリンクを作成し、他のユーザーと共有できます。

## アセットを共有する {#share-assets}

1 つ以上のアセットをプライベートユーザーまたはパブリックユーザーと共有するには、次の手順を実行します。
1. [!DNL Content Hub] ホームページに移動し、1 つ以上のアセットを選択して、![ 共有 ](/help/assets/assets/share.svg) **[!UICONTROL 共有]** をクリックして、**[!UICONTROL アセットを共有]** ダイアログボックスに 1 つの選択したアセットを表示するか、複数の選択したアセットのリストを表示します。
また、![collections](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL Collections]** で使用可能なアセットを選択して共有することもできます。
1. **[!UICONTROL アセットを共有]** ダイアログボックスで、アセットを表示するか、使用可能なアセットのリストを確認します。 アセットの横にある ![ 選択解除 ](/help/assets/assets/Close.svg) をクリックして、リストから選択を解除します。
1. **[!UICONTROL 有効期限]** を選択し、「**[!UICONTROL プライベートリンクを生成]**」をクリックして、プライベートユーザーと共有するリンクを生成します。 プライベートユーザーが自分の [!DNL Content Hub] 環境にログインして、共有アセットページにアクセスします。
   ![ プライベートリンクとパブリックリンク ](/help/assets/assets/private-and-public-link.png)
**[!UICONTROL 公開リンク]** 切り替えスイッチを有効にし、**[!UICONTROL 有効期限]** を選択して **[!UICONTROL 公開リンクを生成]** をクリックして、公開ユーザーと共有するリンクを生成します。 公開ユーザーはゲストとして、[!DNL Content Hub] にログインせずに共有アセットページにアクセスします。
   ![ プライベートリンクとパブリックリンク ](/help/assets/assets/public-and-private-link.png)

   >[!NOTE]
   > 
   > [ アセットを共有 ](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing) ダイアログボックスに **[!UICONTROL 公開リンク]** を表示するには、**[!UICONTROL 設定ページから公開リンク共有を有効にする]** を有効にします。

## プレビューページからのアセットの共有 {#share-asset-from-preview-page}

アセットをプレビューしながら共有するには、次の手順を実行します。

1. [!DNL Content Hub] ホームページに移動し、アセットのサムネールをクリックしてアセットをプレビューし、ダイアログボックスの右側のパネルにメニューオプションを表示します。
1. ![ 共有 ](/help/assets/assets/share.svg) を選択して **[!UICONTROL 共有]** パネルを表示します。
   ![ プレビュー中にアセットを共有 ](/help/assets/assets/share-assets-from-share-panel.png)
1. [ アセットを共有 ](#share-assets) セクションの手順 3 に従って、この **[!UICONTROL 共有]** パネルからアセットリンク（プライベートまたはパブリック）を生成して共有します。

## 共有アセットにアクセス {#access-shared-assets}

リンクから共有アセットページにアクセスし、次の手順を実行します。

* 1 つ以上のアセットを選択し、「![ ダウンロード ](/help/assets/assets/download-icon.svg)**[!UICONTROL ダウンロード]**」をクリックして、利用可能なダウンロードオプションから **[!UICONTROL オリジナル]**、**[!UICONTROL 静的]** または両方のレンディションを選択します。
  ![](/help/assets/assets/download-shared-assets.png)
* アセットのサムネールをクリックして、アセットのメタデータを表示します。
* 共有アセットページ（[ プライベートリンクを使用してアクセス ](#share-assets)）でアセットのサムネールをクリックし、![ ダウンロード ](/help/assets/assets/download-icon.svg) を選択して、アセットを選択およびダウンロードする前に、**[!UICONTROL ダウンロード]** パネルでアセットの使用可能な動的レンディションを選択して表示します。
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)





