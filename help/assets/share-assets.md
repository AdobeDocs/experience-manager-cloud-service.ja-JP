---
title: アセット、フォルダーおよびコレクションの配布と共有
description: リンクとして共有、ダウンロード、経由 [!DNL Brand Portal], [!DNL desktop app], and [!DNL Asset Link]などの方法を使用して、デジタルアセットを配布します。
contentOwner: AG
feature: アセット管理、共同作業、アセット分布
role: User,Admin
exl-id: 14e897cc-75c2-42bd-8563-1f5dd23642a0
source-git-commit: 00bea8b6a32bab358dae6a8c30aa807cf4586d84
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 95%

---

# Adobe [!DNL Experience Manager] で管理されるアセットの共有と配布  {#share-assets-from-aem}

[!DNL Adobe Experience Manager Assets] では、アセット、フォルダー、コレクションを組織内や外部（パートナーやベンダーなど）のメンバーと共有できます。Adobe [!DNL Experience Manager Assets] as a [!DNL Cloud Service] のアセットを共有するには、次の方法を使用します。

* [リンクとして共有](#sharelink).
* [アセットをダウンロードし、個別に共有します。](/help/assets/download-assets-from-aem.md)
* [[!DNL Experience Manager]  デスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=ja)を使用して共有します。
* [[!DNL Adobe Asset Link] を使用して共有します](https://www.adobe.com/jp/creativecloud/business/enterprise/adobe-asset-link.html)。
* [[!DNL Brand Portal] を使用して共有します](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=ja)。

## アセットをリンクとして共有 {#sharelink}

ユーザーと共有するアセットの URL を生成するには、リンク共有ダイアログを使用します。`/var/dam/share` の場所への管理者特権または読み取り権限を持つユーザーが、共有されたリンクを表示することができます。リンクによるアセットの共有は、外部の関係者が [!DNL Assets] にログインすることなくリソースを利用するための便利な方法です。

![リンク共有ダイアログ](assets/link-share-dialog.png)

>[!NOTE]
>
>* リンクとして共有するフォルダーやアセットに対する編集の ACL 権限が必要です。
>* ユーザーとリンクを共有する前に、[送信電子メール](/help/implementing/developing/introduction/development-guidelines.md#sending-email)を有効にします。 そうでない場合は、エラーが発生します。


1. [!DNL Assets] のユーザーインターフェイスで、リンクとして共有するアセットを選択します。
1. ツールバーの「**[!UICONTROL リンクを共有]**」をクリックします。「**[!UICONTROL リンクを共有]**」フィールドにアセットリンクが自動的に作成されます。このリンクをコピーしてユーザーと共有します。リンクのデフォルトの有効期間は 1 日です。

   >[!NOTE]
   >
   >共有アセットが別の場所に移動されると、そのリンクは機能しなくなります。リンクを再作成し、ユーザーと再共有します。

<!--
## Share assets as a link {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to AEM Assets.

>[!NOTE]
>
>* You need Edit ACL permission on the folder or the asset that you want to share as a link.
>* Before you share a link with users, ensure that Day CQ Mail Service is configured. Otherwise, an error occurs.

1. In the Assets user interface, select the asset to share as a link.
1. From the toolbar, click/tap the **[!UICONTROL Share Link]**.

   An asset link is auto-created in the **[!UICONTROL Share Link]** field. Copy this link and share it with the users. The default expiration time for the link is one day.

   Alternatively, proceed to perform steps 3-7 of this procedure to add email recipients, configure the expiration time for the link, and send it from the dialog.

   >[!NOTE]
   >
   >If a shared asset is moved to a different location, its link stops working. Re-create the link and re-share with the users.

1. From the web console, open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against each:

    * local
    * author
    * publish

   For the local and author properties, provide the URL for the local and author instance respectively. Both local and author properties have the same value if you run a single AEM author instance. For publish, provide the URL for the publish instance.

1. In the email address box of the **[!UICONTROL Link Sharing]** dialog, type the email ID of the user you want to share the link with. You can also share the link with multiple users.

   If the user is a member of your organization, select the user's email ID from the suggested email IDs that appear in the list below the typing area. For an external user, type the complete email ID and then select it from the list.

   To enable emails to be sent out to users, configure the SMTP server details in [Day CQ Mail Service](/help/assets/configure-asset-sharing.md#configmailservice).

   >[!NOTE]
   >
   >If you enter an email ID of a user that is not a member of your organization, the words "External User" are prefixed with the email ID of the user.

1. In the **[!UICONTROL Subject]** box, enter a subject for the asset you want to share.
1. In the **[!UICONTROL Message]** box, enter an optional message.
1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link using the date picker. By default, the expiration date is set for a week from the date you share the link.
1. To let users download the original image along with the renditions, select **[!UICONTROL Allow download of original file]**.

   >[!NOTE]
   >
   >By default, users can only download the renditions of the asset that you share as a link.

1. Click **[!UICONTROL Share]**. A message confirms that the link is shared with the users through an email.
1. To view the shared asset, click/tap the link in the email that is sent to the user. The shared asset is displayed in the **[!UICONTROL Adobe Marketing Cloud]** page.

   To toggle to the list view, click/tap the layout icon in the toolbar.

1. To generate a preview of the asset, click/tap the shared asset. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click/tap **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click/tap **[!UICONTROL Parent Folder]** to return to the parent folder.

   >[!NOTE]
   >
   >AEM supports generating the preview of assets of these MIME types: JPG, PNG, GIF, BMP, INDD, PDF, and PPT. You can only download the assets of the other MIME types.

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. To view the assets you shared as links, go to the Assets user interface and click/tap the GlobalNav icon. Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

A message confirms that you unshared the asset. In addition, the entry for the asset is removed from the list.
-->

## アセットのダウンロードと共有 {#download-and-share-assets}

ユーザーは、必要なアセットをダウンロードして、[!DNL Experience Manager] の外部で共有することができます。詳しくは、[アセットの検索方法](/help/assets/search-assets.md)、[アセットのダウンロード方法](/help/assets/download-assets-from-aem.md)、[コレクションのダウンロード方法](manage-collections.md#download-a-collection)を参照してください。

## クリエイティブプロフェッショナルとのアセットの共有 {#share-with-creatives}

マーケティング担当者や事業部門のユーザーは、次のいずれかを使用して、承認済みアセットをクリエイティブプロフェッショナルと容易に共有できます。

* **Adobe Experience Manager デスクトップアプリケーション**：このアプリケーションは Windows と Mac で動作します。[AEM デスクトップアプリケーションの概要](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)を参照してください。承認済みのデスクトップユーザーが共有アセットに容易にアクセスできる方法については、[アセットの参照、検索、プレビュー](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja#browse-search-preview-assets)を参照してください。デスクトップユーザーは、アセットを作成し、新しい画像をアップロードするなどして、AEM ユーザーである相手とアセットを共有することができます。詳しくは、[デスクトップアプリケーションを使用したアセットのアップロード方法](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja#upload-and-add-new-assets-to-aem)を参照してください。

* **Adobe Asset Link**：クリエイティブプロフェッショナルは、[!DNL Adobe InDesign]、[!DNL Adobe Illustrator]、[!DNL Adobe Photoshop] 内から直接アセットを検索および使用できます。

## アセット共有の設定 {#configure-sharing}

アセットを共有する様々なオプションには、特定の設定が必要で、特定の前提条件があります。

### アセットリンク共有の設定 {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

ユーザーと共有するアセットの URL を生成するには、リンク共有ダイアログを使用します。`/var/dam/share` の場所への管理者特権または読み取り権限を持つユーザーが、共有されたリンクを表示することができます。リンクによるアセットの共有は、外部の関係者が [!DNL Assets] にログインすることなくリソースを利用するための便利な方法です。

>[!NOTE]
>
> オーサーインスタンスから外部エンティティへのリンクを共有する場合は、`GET` リクエストに対する次の URL のみ公開するようにします。オーサーインスタンスの安全性を確保するために、その他の URL はブロックします。
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


<!--
## Configure Day CQ mail service {#configmailservice}

Before you can share assets as links, configure the email service.

1. Click or tap the AEM logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service]** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password

1. Click/tap **[!UICONTROL Save]**.
-->

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.
### Configure maximum data size {#maxdatasize}

When you download assets from the link shared using the Link Sharing feature, AEM compresses the asset hierarchy from the repository and then returns the asset in a ZIP file. However, in the absence of limits to the amount of data that can be compressed in a ZIP file, huge amounts of data is subjected to compression, which causes out of memory errors in JVM. To secure the system from a potential denial of service attack due to this situation, you can configure the maximum size of the downloaded files. If uncompressed size of the asset exceeds the configured value, asset download requests are rejected. The default value is 100 MB.

1. Click/Tap the AEM logo and then go to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the web console, locate the **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configuration.
1. Open the configuration in edit mode, and modify the value of the **[!UICONTROL Max Content Size (uncompressed)]** parameter.
1. Save the changes.
-->

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### デスクトップアクションのデスクトップアプリでの有効化 {#desktop-actions}

ブラウザーの [!DNL Assets] ユーザーインターフェイスから、アセットの場所を参照したり、アセットをチェックアウトしてデスクトップアプリケーションで編集用に開いたりできます。これらのオプションはデスクトップアクションと呼ばれます。これを有効にするには、[ [!DNL Assets] Web インターフェイスでのデスクトップアクションの有効化](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja#desktopactions-v2)を参照してください。

![デスクトップアプリで作業する際の、デスクトップアクションのショートカットとしての有効化](assets/enable_desktop_actions.png)

### [!DNL Adobe Asset Link] の使用設定  {#configure-asset-link}

Adobe Asset Link を使用すると、コンテンツ作成プロセスでのクリエイターとマーケターのコラボレーションを効率化できます。[!DNL Adobe Experience Manager Assets] を [!DNL Creative Cloud] デスクトップアプリケーションである [!DNL Adobe InDesign]、[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator] と接続します。[!DNL Adobe Asset Link] パネルを使用すると、[!DNL Assets] に保存されているコンテンツに対して、クリエイターが最もなじみのあるクリエイティブアプリケーションからアクセスして変更を加えることができます。

[ [!DNL Adobe Asset Link] と併用できるように [!DNL Assets] を設定する方法](https://helpx.adobe.com/jp/enterprise/using/configure-aem-assets-for-asset-link.html)を参照してください。

## ベストプラクティスとトラブルシューティング {#bestpractices}

* 名前に空白を含むアセットフォルダーまたはコレクションは共有されない可能性があります。
* ユーザーが共有アセットをダウンロードできない場合は、AEM 管理者に[ダウンロード制限](#maxdatasize)を確認してください。
* リンク共有を使用して共有されているビデオをプレビューするには、リポジトリー内でそのビデオノードの場所 `/jcr:content/renditions` に静的ビデオレンディションが必要です。プレビューは、[!DNL Dynamic Media] レンディションの有無には依存しません。
* リンク共有を介してビデオアセットをダウンロードする場合、ダウンロードされたアーカイブに [!DNL Dynamic Media] レンディションは含まれません。

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your AEM administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!-- TBD: Add content or link about how to share using Brand Portal when it is available on [!DNL Cloud Service].
-->
