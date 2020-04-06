---
title: Brand Portalへのアセット、フォルダーおよびコレクションの公開
seo-title: Brand Portalへのアセット、フォルダおよびコレクションの公開
description: アセット、フォルダーおよびコレクションをBrand Portalに公開したり非公開にする方法について説明します。
seo-description: アセット、フォルダーおよびコレクションをBrand Portalに公開したり非公開にする方法について説明します。
uuid: null
contentOwner: Vishabh Gupta
products: SG_EXPERIENCEMANAGER/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: null
translation-type: tm+mt
source-git-commit: 7a98b0f77177612bf81d904e8b0fb3645baf1435

---


# Brand Portalへのアセット、フォルダーおよびコレクションの公開 {#publish-aem-assets-to-brand-portal}

Adobe Experience Manager(AEM)Assets管理者は、AEM Assets Brand Portalインスタンスにアセット、フォルダーおよびコレクションを公開できます。 また、アセットまたはフォルダの公開ワークフローを後日にスケジュールすることもできます。 公開すると、Brand Portalユーザーはアセット、フォルダーおよびコレクションにアクセスし、他のユーザーにさらに配布できます。

ただし、最初にBrand PortalでAEM Assetsを設定する必要があります。 For details, see [Configure AEM Assets with Brand Portal](configure-aem-assets-with-brand-portal.md).

AEM Assetsで元のアセット、フォルダーまたはコレクションに対して後で変更を加えた場合、AEM Assetsから再公開するまで、変更はBrand Portalに反映されません。 この機能を使用すると、作業中の変更がBrand Portalで使用できなくなります。 Brand Portalでは、管理者が発行した承認済みの変更のみを利用できます。

* [Brand Portal へのアセットの公開](#publish-assets-to-bp)
* [Brand Portal へのフォルダーの公開](#publish-folders-to-brand-portal)
* [Brand Portal へのコレクションの公開](#publish-collections-to-brand-portal)

>[!NOTE]
>
>AEM オーサーが過剰なリソースを占有しないように、できればピーク時を避け、時間をずらして公開することをお勧めします。


## Brand Portal へのアセットの公開 {#publish-assets-to-bp}

AEM AssetsからBrand Portalにアセットを公開する手順を次に示します。

1. アセットコンソールで、親フォルダを開き、公開するすべてのアセットを選択し、ツールバーの「クイック公 **[!UICONTROL 開]** 」オプションをクリックします。


   ![publish2bp-2](assets/publish2bp.png)

1. アセットを公開する方法は2つあります。
   * [今すぐ公開](#publish-to-bp-now) （アセットを今すぐ公開）
   * [後で公開](#publish-to-bp-now) （アセットの公開をスケジュール）

### アセットを今すぐ公開 {#publish-to-bp-now}

選択したアセットを Brand Portal に公開するには、次のいずれかを実行します。

* From the toolbar, select **[!UICONTROL Quick Publish]**. From the menu, click **[!UICONTROL Publish to Brand Portal]**.

* From the toolbar, select **[!UICONTROL Manage Publication]**.

   1. From **[!UICONTROL Action]**, select **[!UICONTROL Publish to Brand Portal]**, and from **[!UICONTROL Scheduling]**, select **[!UICONTROL Now]**. 「**[!UICONTROL 次へ]**」をクリックします。

   2. 「スコープ」での選択を **[!UICONTROL 確認し]**、「ブランドポー **[!UICONTROL タルに投稿」をクリックします]**。

アセットが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portalインターフェイスにログインして、公開済みアセットを表示します。

### アセットを後で公開 {#publish-to-bp-later}

アセットを Brand Portal に公開するスケジュールを未来の日時で設定するには、次のようにします。

1. 公開のスケジュールを設定するアセットを選択し、上部のツ **[!UICONTROL ールバーから]** 「パブリケーションの管理」を選択します。

1. On **[!UICONTROL Manage Publication]** page, select **[!UICONTROL Publish to Brand Portal]** from **[!UICONTROL Action]**, and select **[!UICONTROL Later]** from **[!UICONTROL Scheduling]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Select an **Activation date** and specify time. 「**次へ**」をクリックします。

1. Specify a **[!UICONTROL Workflow title]** in **[!UICONTROL Workflows]**. Click **[!UICONTROL Publish Later]**.

   ![publishworkflow](assets/publishworkflow.png)

Brand Portalインターフェイスにログインして、公開済みのアセットが使用可能であることを確認します。

![bp_landing_page](assets/bp_landing_page.png)

<!--

End - Publish assets to Brand Portal
Start- Publish folders to Brand Portal
-->


## Brand Portal へのフォルダーの公開{#publish-folders-to-brand-portal}

アセットフォルダは、直ちに公開または非公開にしたり、後でスケジュールしたりできます。

### Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal-1}

1. アセットコンソールで、公開するフォルダを選択し、ツールバーの「クイッ **[!UICONTROL ク公開]** 」オプションをクリックします。

   ![publish2bp](assets/publish2bp.png)

1. **フォルダーを今すぐ公開**

   選択したフォルダーを Brand Portal に公開するには、次のいずれかを実行します。

   * From the toolbar, select **[!UICONTROL Quick Publish]**. メニューから「**[!UICONTROL Brand Portal に発行]**」を選択します。

   * From the toolbar, select **[!UICONTROL Manage Publication]**.

      1. 「アクシ **[!UICONTROL ョン]**」から「ブラ **[!UICONTROL ンドポータルに投稿」を選択します]**。 「スケジ **[!UICONTROL ュール]**」から「今すぐ **[!UICONTROL 」を選択します]**。 「**[!UICONTROL 次へ]**」をクリックします。
      1. 「スコープ」での選択を確 **[!UICONTROL 認し]** 、「ブランドポ **[!UICONTROL ータルに投稿」をクリックします]**。
   フォルダーが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portalインターフェイスにログインして、公開済みフォルダを表示します。

1. **フォルダーを後で公開**

   アセットフォルダの公開を後日にスケジュールする場合。

   1. 公開のスケジュールを設定するフォルダを選択し、上部のツ **[!UICONTROL ールバーから]** [パブリケーションの管理]を選択します。
   1. From **[!UICONTROL Action]**, select **[!UICONTROL Publish to Brand Portal]**, and from **[!UICONTROL Scheduling]** select **[!UICONTROL Later]**.

      ![publishlatebp](assets/publishlaterbp.png)

   1. Select an **[!UICONTROL Activation date]** and specify time. 「**[!UICONTROL 次へ]**」をクリックします。
   1. Confirm your selection in **[!UICONTROL Scope]**. 「**[!UICONTROL 次へ]**」をクリックします。
   1. Specify a Workflow title under **[!UICONTROL Workflows]**. Click **[!UICONTROL Publish Later]**.

      ![manageschedulepub](assets/manageschedulepub.png)

### Brand Portal へのフォルダーの公開の取り消し {#unpublish-folders-from-brand-portal}

AEM Assetsインスタンスから非公開にすることで、Brand Portalに公開されたアセットフォルダーを削除できます。 元のフォルダーの公開を取り消すと、そのコピーはBrand Portalユーザーには使用できなくなります。

アセットフォルダーをBrand Portalから直ちに非公開にしたり、後で公開するようにスケジュールしたりできます。

Brand Portal へのアセットフォルダーの公開を取り消すには、次のようにします。

1. AEM Assetsコンソールから、非公開にするフォルダーを選択します。

   ![publish2bp-1](assets/publish2bp.png)

1. From the toolbar, Click **[!UICONTROL Manage Publication]**.

1. **Brand Portal への公開を今すぐ取り消し**

   選択したフォルダーをBrand Portalから直ちに非公開にするには：

   1. From the toolbar, select **Manage Publication**.
   1. From **Action**, select **Unpublish from Brand Portal**, and from **Scheduling**, select **Now**. 「**次へ」をクリックします。**
   1. 「スコープ」での選択を確 **認し** 、「Brand Portalか **ら非公開」をクリックします**。
   ![非公開の確認](assets/confirm-unpublish.png)

1. **後でBrand Portalから非公開にする**

   Brand Portalから後日にフォルダーの非公開をスケジュールするには：

   1. From the toolbar, select **Manage Publication**.
   1. From **Action**, select **Unpublish from Brand Portal**, and from **Scheduling** select **Later**.
   1. Select an **Activation date** and specify the time. 「**次へ**」をクリックします。
   1. 「スコープ」での選択を確 **認し** 、「次へ」をクリ **ックします**。
   1. Specify a **Workflow title** in **Workflows**. Click **Unpublish Later.**

      ![unpublishworkflows](assets/unpublishworkflows.png)


<!--
End - Publish folders to Brand Portal
Start- Publish Collections to Brand Portal

-->

## Brand Portal へのコレクションの公開 {#publish-collections-to-brand-portal}

AEM Assetsインスタンスからコレクションを公開または非公開できます。

>[!NOTE]
>
>コンテンツフラグメントは Brand Portal に公開できません。Therefore, if you select content fragment(s) in AEM Asset, then **[!UICONTROL Publish to Brand Portal]** action is not available.
>
>コンテンツフラグメントを含むコレクションがAEM AssetsからBrand Portalに公開される場合、コンテンツフラグメントを除くフォルダーのすべてのコンテンツがBrand Portalインターフェイスに複製されます。

### コレクションの公開 {#publish-a-collection-to-brand-portal}

AEM AssetsからBrand Portalにコレクションを公開する手順を次に示します。

1. AEM Assets UIで、「AEM logo」をクリックします。
1. From **Navigation** page, go to **[!UICONTROL Assets]** > **[!UICONTROL Collections]**.
1. From the **Collections** console, select the collections that you want to publish to Brand Portal.

   ![select_collection](assets/select_collection.png)

1. From the toolbar, click **[!UICONTROL Publish to Brand Portal]**.
1. In the confirmation dialog, click **[!UICONTROL Publish]**.
1. 確認メッセージを閉じます。

   管理者としてBrand Portalにログインします。 The published collection is available in the **[!UICONTROL Collections]** console.

   ![公開コレクション](assets/published_collection.png)

## コレクションを非公開にする {#unpublish-collections}

AEM Assetsインスタンスから公開を取り消すことで、Brand Portalに公開されたコレクションを削除できます。 元のコレクションの公開を取り消すと、そのコピーはBrand Portalユーザーは使用できなくなります。

コレクションの公開を取り消す手順は次のとおりです。

1. AEM Assetsインスタンスのコレクションコンソールから、非公開にするコレクションを選択します。

   ![select_collection-1](assets/select_collection-1.png)

1. From the toolbar, click **[!UICONTROL Remove from Brand Portal]** icon.
1. In the dialog, click **[!UICONTROL Unpublish]**.
1. 確認メッセージを閉じます。コレクションがBrand Portalインターフェイスから削除されます。

エンドユーザ [ーへのアセット、フォルダ](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) 、コレクションの配布について詳しくは、Brand Portalのドキュメントを参照してください。

<!--

End - Publish Collections to Brand Portal

-->

