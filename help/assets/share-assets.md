---
title: アセット、フォルダー、コレクションをリンクとして共有
description: この記事では、Experience Manager Assets内のアセット、フォルダーおよびコレクションをハイパーリンクとして共有する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Experience Managerで管理されるアセットの共有と配布 {#share-assets-from-aem}

Adobe Experience Manager (AEM)Assetsを使用すると、アセット、フォルダーおよびコレクションを組織のメンバーや、パートナーやベンダーなどの外部エンティティと共有できます。 次の方法を使用して、Experience Manager Assetsのアセットをクラウドサービスとして共有できます。

* リンクとして共有
* アセットのダウンロード
* AEMデスクトップアプリで共有
* Adobe Assetリンクを使用して共有
* （今後の機能）ブランドポータルを使用した共有

## アセットをリンクとして共有 {#sharelink}

ユーザーと共有するアセットの URL を生成するには、リンク共有ダイアログを使用します。Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. リンクを使用したアセットの共有は、AEM Assetsに最初にログインしなくても、外部のユーザーがリソースを利用できるようにする便利な方法です。

>[!NOTE]
>
>* リンクとして共有するフォルダーまたはアセットに対するACLの編集権限が必要です。
>* リンクをユーザーと共有する前に、Day CQ Mail Service が設定されていることを確認してください。そうしないと、エラーが発生します。


1. Assets のユーザーインターフェイスで、リンクとして共有するアセットを選択します。
1. From the toolbar, click/tap the **[!UICONTROL Share Link]**.

   An asset link is auto-created in the **[!UICONTROL Share Link]** field. このリンクをコピーしてユーザーと共有します。リンクのデフォルトの有効期間は 1 日です。

   または、この手順の 3～7 に進んで電子メールの受信者を追加し、リンクの有効期限を設定して、ダイアログから送信することもできます。

   >[!NOTE]
   >
   >共有アセットが別の場所に移動されると、そのリンクは機能しなくなります。リンクを再作成し、ユーザーと再共有します。

1. From the web console, open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against each:

   * local
   * author
   * publish
   local プロパティと author プロパティには、それぞれローカルインスタンスとオーサーインスタンスの URL を指定します。単一の AEM オーサーインスタンスを実行している場合、local プロパティと author プロパティの値は同じになります。publish には、パブリッシュインスタンスの URL を指定します。

1. **[!UICONTROL リンク共有]**&#x200B;ダイアログの電子メールアドレスボックスに、リンクを共有するユーザーの電子メール ID を入力します。このリンクを複数のユーザーと共有することもできます。

   ユーザーが組織内のメンバーの場合は、入力領域の下のリストに表示される電子メール ID の候補から、ユーザーの電子メール ID を選択します。外部ユーザーの場合は、完全な電子メール ID を入力してリストから選択します。

   ユーザーへの電子メールの送信を有効にするには、[Day CQ Mail Service](/help/assets/configure-asset-sharing.md#configmailservice) で SMTP サーバーの詳細を設定します。

   >[!NOTE]
   >
   >組織内のメンバーではないユーザーの電子メール ID を入力した場合、ユーザーの電子メール ID に「外部ユーザー」というプレフィックスが付けられます。

1. 「**[!UICONTROL 件名]**」ボックスに、共有するアセットの件名を入力します。
1. 「**[!UICONTROL メッセージ]**」ボックスに、オプションでメッセージを入力します。
1. 「**[!UICONTROL 有効期限]**」フィールドに、日付選択を使用してリンクの有効期限の日付と時間を指定します。デフォルトでは、有効期限日はリンクを共有した日から 1 週間後に設定されます。
1. ユーザーが元の画像をレンディションと共にダウンロードすることを許可するには、「**[!UICONTROL 元のファイルのダウンロードを許可]**」を選択します。

   >[!NOTE]
   >
   >デフォルトでは、ユーザーはリンクとして共有されているアセットのレンディションのみをダウンロードできます。

1. 「**[!UICONTROL 共有]**」をクリックします。リンクが電子メールでユーザーと共有されていることを確認するメッセージが表示されます。
1. 共有アセットを表示するには、ユーザーに送信された電子メールのリンクをクリックまたはタップします。共有アセットが **[!UICONTROL Adobe Marketing Cloud]** ページに表示されます。

   リスト表示に切り替えるには、ツールバーのレイアウトアイコンをクリックまたはタップします。

1. アセットのプレビューを生成するには、共有アセットをクリックまたはタップします。To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click/tap **[!UICONTROL Back]** in the toolbar. フォルダーを共有している場合は、「**[!UICONTROL 親フォルダー]**」をクリックまたはタップして親フォルダーに戻ります。

   >[!NOTE]
   >
   >AEM は、これらの MIME タイプ（JPG、PNG、GIF、BMP、INDD、PDF、および PPT）のアセットのプレビューの生成をサポートしています。他の MIME タイプのアセットのみをダウンロードできます。

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. リンクとして共有したアセットを表示するには、Assets の UI に移動し、グローバルナビゲーションアイコンをクリックまたはタップします。Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. ナビゲーションウィンドウで、「**[!UICONTROL 共有リンク]**」を選択して共有アセットのリストを表示します。
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

アセットを共有しないことを確認するメッセージが表示されます。また、このアセットの項目がリストから削除されます。

## アセットのダウンロードと共有 {#download-and-share-assets}

ユーザーは、一部のアセットをダウンロードして、Experience Managerの外部で共有できます。 詳しくは、アセットの検索方法、ア [セットのダウンロード方法](/help/assets/search-assets.md)、コ [レクションのダウンロード方法を](/help/assets/download-assets-from-aem.md)[参照してください。](manage-collections.md#download-a-collection)

## クリエイティブプロフェッショナルとのアセットの共有 {#share-with-creatives}

マーケターや基幹業務ユーザーは、承認されたアセットをクリエイティブプロフェッショナルと簡単に共有できます。

* **AEMデスクトップアプリ**:アプリケーションはWindowsとMacで機能します。 デスクトップア [プリの概要を参照してください](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html)。 承認されたデスクトップユーザーが共有アセットに簡単にアクセスできる方法については、アセットの参照、 [検索およびプレビューを参照してくださ](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets)い。 デスクトップユーザーは、新しいアセットを作成し、例えば、新しい画像をアップロードすることで、AEMユーザーである相手とアセットを共有できます。 詳しくは、デスクト [ップアプリを使用したアセットのアップロードを参照してくださ](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)い。

* **Adobe Asset Link**:クリエイティブプロフェッショナルは、Adobe inDesign、Adobe IllustratorおよびAdobe Photoshop内から直接アセットを検索して使用できます。

### ベストプラクティスとトラブルシューティング {#bestpractices}

* 名前に空白が含まれるアセットフォルダーまたはコレクションは、共有できない場合があります。
* ユーザーが共有アセットをダウンロードできない場合は、AEM 管理者に[ダウンロード制限](/help/assets/configure-asset-sharing.md#maxdatasize)を確認してください。
* 共有アセットへのリンクを含むメールを送信できない場合、または他のユーザーがお客様からのメールを受信できない場合、AEM 管理者に[メールサービス](/help/assets/configure-asset-sharing.md#configmailservice)が構成されているかどうかを確認してください。
* リンク共有機能を使用してアセットを共有できない場合は、適切な権限を持っていることを確認してください。[アセットの共有](#sharelink)を参照してください。

<!--
Add content or link about how to share using BP, DA, AAL, etc.
-->
