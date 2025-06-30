---
title: ' [!DNL the Content Hub] でのアセットの共有'
description: ' [!DNL the Content Hub] でのアセットの共有'
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 100%

---

# コンテンツハブでのアセットの共有 {#search-assets-as-a-link}

選択したアセットへのリンクを作成して、他のユーザーと簡単に共有できるようにします。認証済みの [!DNL Content Hub] ユーザーとして、[!DNL Content Hub] 環境で使用可能な 1 つ以上のアセットを選択し、リンクを生成して、そのリンクを他のプライベートまたはパブリックのユーザーに送信します。

## 前提条件 {#prerequisites}

[コンテンツハブユーザー](deploy-content-hub.md#onboard-content-hub-users)は、選択したアセットへのリンクを作成し、他のユーザーとそのリンクを共有できます。

## アセットを共有する {#share-assets}

1 つ以上のアセットをプライベートユーザーまたはパブリックユーザーと共有するには、次の手順を実行します。
1. [!DNL Content Hub] ホームページに移動し、1 つ以上のアセットを選択して、![共有](/help/assets/assets/share.svg) **[!UICONTROL 共有]**&#x200B;をクリックして、**[!UICONTROL アセットを共有]**&#x200B;ダイアログボックスに 1 つの選択したアセットを表示するか、複数の選択したアセットのリストを表示します。また、![コレクション](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL コレクション]**&#x200B;で使用可能なアセットを選択して共有することもできます。
1. **[!UICONTROL アセットを共有]**&#x200B;ダイアログボックスで、アセットを表示するか、使用可能なアセットのリストを確認します。アセットの横にある![選択解除](/help/assets/assets/Close.svg)をクリックして、リストから選択を解除します。
1. **[!UICONTROL 有効期限]**&#x200B;を選択し、「**[!UICONTROL プライベートリンクを生成]**」をクリックして、プライベートユーザーと共有するリンクを生成します。プライベートユーザーが自分の [!DNL Content Hub] 環境にログインして、共有アセットページにアクセスします。
   ![プライベートリンクとパブリックリンク](/help/assets/assets/private-and-public-link.png)
**[!UICONTROL 公開リンク]**&#x200B;切り替えスイッチを有効にし、**[!UICONTROL 有効期限]**&#x200B;を選択して「**[!UICONTROL 公開リンクの生成]**」をクリックして、公開ユーザーと共有するリンクを生成します。公開ユーザーはゲストとして、[!DNL Content Hub] にログインせずに共有アセットページにアクセスします。
   ![プライベートリンクとパブリックリンク](/help/assets/assets/public-and-private-link.png)

   >[!NOTE]
   > 
   > **[!UICONTROL アセットの共有]**&#x200B;ダイアログボックスに&#x200B;**[!UICONTROL 公開リンク]**&#x200B;切替スイッチを表示するには、[設定ページから公開リンク共有を有効にします](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing)。

## プレビューページからアセットを共有する {#share-asset-from-preview-page}

アセットをプレビューしながら共有するには、次の手順を実行します。

1. [!DNL Content Hub] ホームページに移動し、アセットのサムネールをクリックしてアセットをプレビューし、ダイアログボックスの右側のパネルにメニューオプションを表示します。
1. 「![共有](/help/assets/assets/share.svg)」を選択して&#x200B;**[!UICONTROL 共有]**パネルを表示します。
   ![プレビュー中にアセットを共有](/help/assets/assets/share-assets-from-share-panel.png)
1. [アセットの共有](#share-assets)セクションの手順 3 に従って、この **[!UICONTROL 共有]** パネルからアセットリンク（プライベートまたはパブリック）を生成して共有します。

## 共有アセットにアクセス {#access-shared-assets}

リンクから共有アセットページにアクセスし、次の手順を実行します。

* 1 つ以上のアセットを選択し、「![ダウンロード](/help/assets/assets/download-icon.svg) **[!UICONTROL ダウンロード]**」をクリックして、利用可能なダウンロードオプションから **[!UICONTROL オリジナル]**、**[!UICONTROL 静的]** または両方のレンディションを選択します。
  ![](/help/assets/assets/download-shared-assets.png)
* アセットのサムネールをクリックして、アセットのメタデータを表示します。
* 共有アセットページ（[プライベートリンクを使用してアクセス](#share-assets)）でアセットのサムネールをクリックし、![ダウンロード](/help/assets/assets/download-icon.svg)を選択して、アセットの使用可能な動的レンディションを選択およびダウンロードする前に、**[!UICONTROL ダウンロード]**パネルでそれらのレンディションを選択して表示します。
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)





