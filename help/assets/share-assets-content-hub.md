---
title: ' [!DNL the Content Hub] でのアセットの共有'
description: ' [!DNL the Content Hub] でのアセットの共有'
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: a641933d1049cd07ee8935672c8ef357a5bbf18c
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 44%

---

# コンテンツハブでのアセットの共有 {#search-assets-as-a-link}

選択したアセットへのリンクを作成して、他のユーザーと簡単に共有できるようにします。認証済みの [!DNL Content Hub] ユーザーとして、[!DNL Content Hub] 環境で使用可能な 1 つ以上のアセットを選択し、リンクを生成して、そのリンクを他のプライベートまたはパブリックのユーザーに送信します。

>[!VIDEO](https://video.tv.adobe.com/v/3474920/?captions=jpn&learn=on&enablevpops=on){transcript=true}

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

### AEM Assets Content Hubでのアセットの共有とは

AEM Assets Content Hubでのアセットの共有では、権限のあるユーザーがリンクを生成することで、1 つ以上のアセットまたはコレクション全体を他のユーザーと簡単に共有できます。 このリンクは、プライベートユーザー（ログインする必要があるユーザー）またはパブリックユーザー（ゲストとしてアクセスできるユーザー）に送信でき、受信者は選択したアセットを表示およびダウンロードするための直接アクセス権を付与されます。

### AEM Assets Content Hubを使用してアセットやコレクションを他のユーザーと共有するにはどうすればよいですか？

Content Hubでアセットやコレクションを共有するには、Content Hub ホームページに移動し、1 つ以上のアセットを選択（またはコレクションの「コレクション」タブに移動）して、共有アイコンをクリックします。 共有ダイアログでは、アセットをプレビューし、必要に応じて削除して、タイトルと説明を追加し、リンクにアクセスできるユーザー（プライベートまたはパブリック）を選択し、有効期限を設定してから、「リンクを取得」をクリックして共有可能な URL を生成およびコピーできます。 その後、リンクをチームメンバーや関係者に送信できます。

### AEM Assets Content Hubでアセットを共有する際に使用できるアクセスオプションはどれですか？また、その違いはどのようなものですか？

Content Hubでは、共有リンクに対してプライベートとパブリックの 2 つのアクセスオプションから選択できます。 プライベートリンクでは、受信者はContent Hub環境にログインしてアセットを表示およびダウンロードする必要があり、セキュリティが強化されます。 公開リンクは、リンクを持つユーザーであれば誰でも、ログインの必要なしにアクセスできます。 各リンクタイプには独自の有効期限設定があります（公開リンクの場合は 24 時間から 1 週間、プライベートリンクの場合はカスタム日付など）。

### AEM Assets Content Hubでアセットの公開リンクを生成できるように、管理者が管理する設定はありますか？

はい。管理者は、設定 UI の **コレクションと共有** タブにある **公開リンクを有効にする** 切替スイッチを有効または無効にして、AEM Assets Content Hubでのアセットの公開リンクの生成を管理できます。

### AEM Assets Content Hubで共有アセットリンクの有効期限を設定できますが、これが重要な理由は何ですか？

はい。Content Hubでは、非公開および公開共有リンクの両方に有効期限を設定できます。 公開リンクの場合は、24 時間から最大 1 週間などのプリセットから選択できますが、非公開リンクの場合は、プリセットから選択するか、カスタムの有効期限を設定できます。 リンクの有効期限が切れると、リンクを使用してアセットにアクセスしたりダウンロードしたりすることはできなくなるので、有効期限が重要です。これにより、コンテンツのセキュリティと制御を維持できます。

### AEM Assets Content Hubを使用して作成された共有アセットリンクに対して受信者は何ができますか？また、様々なレンディションをダウンロードするためのオプションはありますか？

共有アセットリンクを受け取った受信者は、ブラウザーで共有アセットリンクを開き、提供されたアセットをプレビュー、選択およびダウンロードできます。 Content Hubでアセットレンディションが有効になっている場合、受信者はダウンロードするレンディション（オリジナルまたは静的など）を選択することができます。 アセットとレンディションが zip ファイルとしてダウンロードされ、アセットのサムネールをクリックして、メタデータを表示できます。 設定された有効期限までリンクは引き続き機能します。




