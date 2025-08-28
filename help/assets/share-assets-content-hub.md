---
title: ' [!DNL the Content Hub] でのアセットの共有'
description: ' [!DNL the Content Hub] でのアセットの共有'
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: a6d995eddd714c356eadc6c1b668887bdfd011cd
workflow-type: ht
source-wordcount: '409'
ht-degree: 100%

---

# コンテンツハブでのアセットの共有 {#search-assets-as-a-link}

選択したアセットへのリンクを作成して、他のユーザーと簡単に共有できるようにします。認証済みの [!DNL Content Hub] ユーザーとして、[!DNL Content Hub] 環境で使用可能な 1 つ以上のアセットを選択し、リンクを生成して、そのリンクを他のプライベートまたはパブリックのユーザーに送信します。

## 前提条件 {#prerequisites}

[コンテンツハブユーザー](deploy-content-hub.md#onboard-content-hub-users)は、選択したアセットへのリンクを作成し、他のユーザーとそのリンクを共有できます。

## アセットを共有する {#share-assets}

1 つ以上のアセットをプライベートユーザーまたはパブリックユーザーと共有するには、次の手順を実行します。

1. [!DNL Content Hub] ホームページに移動し、1 つ以上のアセットを選択して、![共有](/help/assets/assets/share.svg) **[!UICONTROL 共有]**&#x200B;をクリックして、**[!UICONTROL アセットを共有]**&#x200B;ダイアログボックスに 1 つの選択したアセットを表示するか、複数の選択したアセットのリストを表示します。

   また、![コレクション](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL コレクション]**&#x200B;で使用可能なアセットを選択して共有することもできます。

1. **[!UICONTROL アセットを共有]**&#x200B;ダイアログボックスで、アセットを表示するか、使用可能なアセットのリストを確認します。アセットの横にある![選択解除](/help/assets/assets/Close.svg)をクリックして、リストから選択を削除します。

1. 選択したアセットのセットを定義するタイトルとオプションの説明を指定します。

1. **[!UICONTROL 有効期限]**&#x200B;を選択します。

1. **[!UICONTROL アクセスできるユーザー]**&#x200B;ドロップダウンでアクセスオプションを選択し、「**[!UICONTROL リンクを取得]**」をクリックして、選択したユーザーと共有するリンクを生成します。プライベートユーザーは、自分の [!DNL Content Hub] 環境にログインして、共有アセットページにアクセスする必要があります。一方、公開ユーザーはゲストとして、[!DNL Content Hub] にログインせずに共有アセットページにアクセスできます。

<!--1. Select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Get Link]** to generate a link to share with private users. Private users sign in to their [!DNL Content Hub] environment to access the shared assets page.-->

![プライベートリンクとパブリックリンク](/help/assets/assets/shared-link-for-assets.png)

<!--Enable the **[!UICONTROL Public Link]** toggle, select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Generate Public Link]** to generate a link to share with public users. Public users, as guests, access the shared assets page without signing in to [!DNL Content Hub].-->

>[!NOTE]
> 
> **[!UICONTROL アセットの共有]**&#x200B;ダイアログボックスに&#x200B;**[!UICONTROL 公開リンク]**&#x200B;切替スイッチを表示するには、[設定ページから公開リンク共有を有効にします](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing)。

## プレビューページからアセットを共有する {#share-asset-from-preview-page}

アセットをプレビューしながら共有するには、次の手順を実行します。

1. [!DNL Content Hub] ホームページに移動し、アセットのサムネールをクリックしてアセットをプレビューし、ダイアログボックスの右側のパネルにメニューオプションを表示します。
1. 「![共有](/help/assets/assets/share.svg)」を選択して&#x200B;**[!UICONTROL 共有]**パネルを表示します。
   ![プレビュー中にアセットを共有](/help/assets/assets/share-link-asset-preview.png)
1. [アセットの共有](#share-assets)の節の手順 3～5 に従って、この&#x200B;**[!UICONTROL 共有]**&#x200B;パネルからアセットリンク（プライベートまたはパブリック）を生成して共有します。

## 共有アセットにアクセス {#access-shared-assets}

リンクから共有アセットページにアクセスし、次の手順を実行します。

* 1 つ以上のアセットを選択し、「![ダウンロード](/help/assets/assets/download-icon.svg) **[!UICONTROL ダウンロード]**」をクリックして、利用可能なダウンロードオプションから **[!UICONTROL オリジナル]**、**[!UICONTROL 静的]** または両方のレンディションを選択します。
  ![](/help/assets/assets/download-shared-assets.png)
* アセットのサムネールをクリックして、アセットのメタデータを表示します。
* 共有アセットページ（[プライベートリンクを使用してアクセス](#share-assets)）でアセットのサムネールをクリックし、![ダウンロード](/help/assets/assets/download-icon.svg)を選択して、アセットの使用可能な動的レンディションを選択およびダウンロードする前に、**[!UICONTROL ダウンロード]**パネルでそれらのレンディションを選択して表示します。
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)


