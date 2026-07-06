---
title: ' [!DNL the Content Hub] でのアセットの共有'
description: ' [!DNL the Content Hub] でのアセットの共有'
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 230ca753bd5f3d5b26b30a962a526dc0edfc9bd4
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 46%

---

# コンテンツハブでのアセットの共有 {#search-assets-as-a-link}

選択したアセットへのリンクを作成して、他のユーザーと簡単に共有できるようにします。 認証済みの [!DNL Content Hub] ユーザーとして、[!DNL Content Hub] 環境で使用可能な 1 つ以上のアセットを選択し、リンクを生成して、そのリンクを他のプライベートまたはパブリックのユーザーに送信します。

>[!VIDEO](https://video.tv.adobe.com/v/3474920/?captions=jpn&learn=on&enablevpops=on){transcript=true}

## 前提条件 {#prerequisites}

[コンテンツハブユーザー](deploy-content-hub.md#onboard-content-hub-users)は、選択したアセットへのリンクを作成し、他のユーザーとそのリンクを共有できます。

## アセットを共有する {#share-assets}

1 つ以上のアセットをプライベートユーザーまたはパブリックユーザーと共有するには、次の手順を実行します。

1. [!DNL Content Hub] ホームページに移動し、1 つ以上のアセットを選択して、![共有](/help/assets/assets/share.svg) **[!UICONTROL 共有]**&#x200B;をクリックして、**[!UICONTROL アセットを共有]**&#x200B;ダイアログボックスに 1 つの選択したアセットを表示するか、複数の選択したアセットのリストを表示します。

   また、![コレクション](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL コレクション]**&#x200B;で使用可能なアセットを選択して共有することもできます。

1. **[!UICONTROL アセットを共有]**&#x200B;ダイアログボックスで、アセットを表示するか、使用可能なアセットのリストを確認します。 アセットの横にある![選択解除](/help/assets/assets/Close.svg)をクリックして、リストから選択を削除します。

1. 選択したアセットのセットを定義するタイトルとオプションの説明を指定します。

1. **[!UICONTROL 有効期限]**&#x200B;を選択します。

1. **[!UICONTROL アクセスできるユーザー]**&#x200B;ドロップダウンでアクセスオプションを選択し、「**[!UICONTROL リンクを取得]**」をクリックして、選択したユーザーと共有するリンクを生成します。 プライベートユーザーは、自分の [!DNL Content Hub] 環境にログインして、共有アセットページにアクセスする必要があります。 一方、公開ユーザーはゲストとして、[!DNL Content Hub] にログインせずに共有アセットページにアクセスできます。

<!--1. Select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Get Link]** to generate a link to share with private users. Private users sign in to their [!DNL Content Hub] environment to access the shared assets page.-->

![プライベートリンクとパブリックリンク](/help/assets/assets/shared-link-for-assets.png)

<!--Enable the **[!UICONTROL Public Link]** toggle, select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Generate Public Link]** to generate a link to share with public users. Public users, as guests, access the shared assets page without signing in to [!DNL Content Hub].-->

>[!NOTE]
> 
> **[!UICONTROL アセットの共有]**&#x200B;ダイアログボックスに&#x200B;**[!UICONTROL 公開リンク]**&#x200B;切替スイッチを表示するには、[設定ページから公開リンク共有を有効にします](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing)。

## プレビューページからアセットを共有する {#share-asset-from-preview-page}

アセットをプレビューしながら共有するには、次の手順を実行します。

1. [!DNL Content Hub] ホームページに移動し、アセットのサムネールをクリックしてアセットをプレビューし、ダイアログボックスの右側のパネルにメニューオプションを表示します。
1. 「![共有](/help/assets/assets/share.svg)」を選択して&#x200B;**[!UICONTROL 共有]**&#x200B;パネルを表示します。
   ![プレビュー中にアセットを共有](/help/assets/assets/share-link-asset-preview.png)
1. [アセットの共有](#share-assets)の節の手順 3～5 に従って、この&#x200B;**[!UICONTROL 共有]**&#x200B;パネルからアセットリンク（プライベートまたはパブリック）を生成して共有します。

## 共有アセットにアクセス {#access-shared-assets}

リンクから共有アセットページにアクセスし、次の手順を実行します。

* 1 つ以上のアセットを選択し、「![ダウンロード](/help/assets/assets/download-icon.svg) **[!UICONTROL ダウンロード]**」をクリックして、利用可能なダウンロードオプションから **[!UICONTROL オリジナル]**、**[!UICONTROL 静的]** または両方のレンディションを選択します。
  ![](/help/assets/assets/download-shared-assets.png)
* アセットのサムネールをクリックして、アセットのメタデータを表示します。
* 共有アセットページ（[プライベートリンクを使用してアクセス](#share-assets)）でアセットのサムネールをクリックし、![ダウンロード](/help/assets/assets/download-icon.svg)を選択して、アセットの使用可能な動的レンディションを選択およびダウンロードする前に、**[!UICONTROL ダウンロード]**&#x200B;パネルでそれらのレンディションを選択して表示します。
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)

## よくある質問 {#faqs-share-assets-content-hub}

### AEM Assets Content Hubでのアセットの共有とはどういう意味ですか？

AEM Assets Content Hubでのアセットの共有リンクを生成することで、許可されたユーザーは1つ以上のアセットやコレクション全体を他のユーザーと簡単に共有できます。 このリンクは、プライベートユーザー（ログインする必要がある）またはパブリックユーザー（ゲストとしてアクセスできるユーザー）に送信でき、受信者が選択したアセットを表示およびダウンロードするための直接アクセス権を付与します。

### AEM Assets Content Hubを使用して、アセットやコレクションを他のユーザーと共有するにはどうすればよいですか？

AEM Assets Content Hubでアセットまたはコレクションを共有するには、Content Hub ホームページに移動し、1つ以上のアセットを選択し（またはコレクションの「コレクション」タブに移動）、「共有」アイコンをクリックします。 共有ダイアログでは、アセットのプレビュー、必要に応じた削除、タイトルと説明の追加、リンク（プライベートまたはパブリック）にアクセスできるユーザーの選択、有効期限の設定、リンクを取得をクリックして共有可能なURLを生成およびコピーできます。 リンクは、チームメンバーまたは関係者に送信できます。

### AEM Assets Content Hubでアセットを共有する際に使用できるアクセスオプションと、その違いについて教えてください。

Content Hubでは、共有リンクに対してプライベートリンクとパブリックリンクの2つのアクセスオプションを選択できます。 プライベートリンクでは、アセットを表示およびダウンロードするために受信者がContent Hub環境にログインする必要があり、セキュリティが強化されます。 公開リンクは、ログインを必要とせずに、リンクを持つ誰でもアクセスできます。 各リンクタイプには、公開リンクの場合は24時間から1週間、プライベートリンクの場合はカスタム日付など、独自の有効期限の設定が用意されています。

### AEM Assets Content Hubでアセットの公開リンクを生成できるように、管理者が管理する設定はありますか？

はい。管理者は、AEM Assets Content Hubのアセットの公開リンクの生成を管理するために、Configuration UIの「**コレクションと共有**」タブで使用できる「**公開リンクを有効にする**」トグルを有効または無効にできます。

### AEM Assets Content Hubで共有アセットリンクの有効期限を設定できますか？なぜこれが重要なのですか？

はい。AEM Assets Content Hubでは、プライベートリンクと公開リンクの両方に有効期限を設定できます。 公開リンクの場合は、24時間から1週間までのプリセットから選択できます。非公開リンクの場合は、プリセットから選択するか、カスタム有効期限を設定できます。 有効期限は、リンクの有効期限が切れると、アセットへのアクセスやダウンロードに使用できなくなり、コンテンツのセキュリティと制御の維持に役立つため、重要です。

### AEM Assets Content Hubを使用して作成された共有アセットリンクで、受信者は何ができますか？また、異なるレンディションをダウンロードするためのオプションはありますか？

共有アセットリンクを受け取った受信者は、ブラウザーで共有アセットを開いて、提供されたアセットをプレビュー、選択、ダウンロードできます。 AEM Assets Content Hubでアセットレンディションが有効になっている場合、受信者は、ダウンロードするレンディション（元のアセットや静的アセットなど）を選択できます。 アセットとレンディションはzip ファイルとしてダウンロードされ、アセットのサムネールをクリックするとメタデータを表示できます。 リンクは、設定された有効期限まで機能し続けます。


**関連情報**

* [アセットを翻訳](/help/assets/translate-assets.md)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](/help/assets/file-format-support.md)
* [アセットを検索](/help/assets/search-assets.md)
* [接続されたアセット](/help/assets/use-assets-across-connected-assets-instances.md)
* [アセットレポート](/help/assets/asset-reports.md)
* [メタデータスキーマ](/help/assets/metadata-schemas.md)
* [アセットをダウンロード](/help/assets/download-assets-from-aem.md)
* [メタデータを管理](/help/assets/manage-metadata.md)
* [Dynamic Media テンプレートの管理](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [レポートの管理](/help/assets/manage-reports-assets-view.md)
* [検索ファセット](/help/assets/search-facets.md)
* [コレクションを管理](/help/assets/manage-collections.md)
* [メタデータの一括読み込み](/help/assets/metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)