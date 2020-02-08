---
title: CDN にキャッシュされたコンテンツの無効化
description: コンテンツ配信ネットワーク（CDN）にキャッシュされたコンテンツを無効にすることで、Dynamic Media で配信されるアセットをすばやく更新できます。キャッシュが期限切れになるのを待つ必要はありません。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# CDN にキャッシュされたコンテンツの無効化 {#invalidating-your-cdn-cached-content}

CDN を使用して Dynamic Media アセットをキャッシュすることで、高速配信が可能になります。ただし、アセットを更新する場合は、その変更をすぐに有効にする必要がある場合があります。 コンテンツ配信ネットワーク（CDN）にキャッシュされたコンテンツを無効にすることで、Dynamic Media で配信されるアセットをすばやく更新できます。キャッシュが期限切れになるのを待つ必要はありません。

ダイナミックメ [ディアクラシック(Scene7)のキャッシュの概要も参照してください](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)。

**CDN にキャッシュされたコンテンツを無効化するには、次の手順を実行します。**

1. 次のページから、Dynamic Media Classic（Scene7）アカウントにログオンします。

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   資格情報とログオンは、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、テクニカルサポートにお問い合わせください。

1. **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。
1. On the Application General Settings page, under the Servers group heading, locate the **[!UICONTROL CDN Invalidation Template]** text box.

1. CDN（コンテンツ配信ネットワーク）のキャッシュの無効化に使用するテンプレートを指定します。

   For example, suppose you enter an image URL (including image presets or modifiers) referencing `<ID>`, instead of a specific image ID as in the following example:

   `https://server.com/is/image/Company/<ID>?$product$`

   If the Template just contains `<ID>`, then Dynamic Media fills in `https://<server>/is/image` where `<server>` is the Publish Server Name that is defined in General Settings and &lt;ID> is the asset(s) selected to be invalidated.

1. ページの右下隅にある「**[!UICONTROL 閉じる]**」をクリックします。
1. Dynamic Media Classic（Scene7）の UI で、1 つ以上のアセットを選択し、**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;をクリックします。作成したテンプレートから生成された 1 つ以上の URL と、選択したアセット（またはアセット群）からなるリストが表示されます。このリストに使用されているのは、アプリケーションの全般設定の「公開先サーバー名」にリストされているサーバー URL です。

   例えば、前の手順で設定した CDN 無効化テンプレートを使用して、`Backpack_B` という名前の画像アセットを 1 つだけ選択したとします。**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;をクリックすると、CDN 無効化のユーザーインターフェイスには、次のように生成された URL が表示されます。

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. URL リストボックスで「**[!UICONTROL 続行]**」をクリックして、特定の URL ごとのキャッシュを消去します。URL リストボックスでは、URL を入力または貼り付けることによって、URL を編集したり、追加したりできます。事前に CDN 無効化テンプレートを設定する必要はありません。

   「**[!UICONTROL 続行]**」をクリックすると、キャッシュの消去にかかる時間の概算を示すインジケーターが表示されます。

   If you selected multiple assets, then clicked **[!UICONTROL File > Invalidate CDN]**, each asset is referenced in the saved **[!UICONTROL Template URL]**. Therefore, you can define a **[!UICONTROL CDN Invalidate Template]** referencing each URL image preset that is referenced on your website (such as product detail, search results, and so forth). これにより、キャッシュの無効化の対象として 1 つ以上の画像を選択したときに、それらの URL が自動的にインターフェイスに入力されます。

   >[!NOTE]
   >
   >アセットを選択して&#x200B;**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;をクリックすると、Dynamic Media が CDN 無効化テンプレートを使用して、コンテンツ配信ネットワーク（CDN）内の無効化する URL 群を自動的に作成します。If there is nothing in the **[!UICONTROL CDN Invalidate Template]** text box, then you get a blank URL list. CDN におけるキャッシュは、アセットベースではありません。URL ベースです。したがって、Web サイト上での完全な URL を認識しておく必要があります。After you determine those URLs, you can add them to the **[!UICONTROL Invalidate CDN Template]** text box earlier in the steps. これにより、アセットを選択し、ワンステップで URL を無効化することができます。
   >
   >Another option is to add complete URLs to the **[!UICONTROL Invalidate CDN]** list. この方法に従う場合は、**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;オプションに進む前に Dynamic Media Classic でアセットを選択する必要はありません。

