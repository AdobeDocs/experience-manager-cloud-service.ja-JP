---
title: Dynamic Media Classic を使用した CDN キャッシュの無効化
description: 「CDN(コンテンツ配信ネットワーク)キャッシュコンテンツを無効にして、キャッシュの期限が切れるのを待たずに、Dynamic Mediaから配信されるアセットをすばやく更新する方法を説明します。」
feature: アセット管理，Dynamic Mediaクラシック
topic: 開業医
translation-type: tm+mt
source-git-commit: 80a59a02067d478713aa7dcdb436ad1345d89c1a
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 46%

---


# Dynamic Media Classic を使用した CDN キャッシュの無効化 {#invalidating-your-cdn-cached-content}

Dynamic Mediaアセットは、高速配信を実現するために、CDN(コンテンツ配信ネットワーク)によってキャッシュされます。 ただし、アセットを更新する場合は、その変更をすぐに有効にする必要があります。 CDNキャッシュコンテンツを無効にすると、キャッシュの期限が切れるのを待たずに、Dynamic Mediaから配信されるアセットをすばやく更新できます。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience ManagerDynamic Mediaにバンドルされている標準搭載のCDNを使用する必要があります。 この機能では、その他のカスタムCDNはサポートされません。

>[!IMPORTANT]
>
>これらの手順は、AEM 6.5、Service Pack 5 以前の Dynamic Media にのみ適用されます。<!-- If you are using Dynamic Media in AEM as a Cloud Service, [use the new steps found here](/help/assets/invalidate-cdn-cache-dynamic-media.md). -->

[Dynamic Media Classic のキャッシュの概要](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)も参照してください。

**Dynamic Media Classic を使用して CDN キャッシュを無効にするには：**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、アカウントにログインします。

   資格情報とログインの詳細は、プロビジョニング時にAdobeから提供されました。 この情報をお持ちでない場合は、テクニカルサポートにお問い合わせください。

1. **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。
1. アプリケーションの一般設定ページで、「サーバー」グループ見出しの下にある「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスを見つけます。

1. CDN（コンテンツ配信ネットワーク）のキャッシュの無効化に使用するテンプレートを指定します。

   例えば、次の例にあるように、特定の画像 ID ではなく、`<ID>` を参照する画像 URL（画像プリセットまたは画像の修飾子を含む）を入力するとします。

   `https://server.com/is/image/Company/<ID>?$product$`

   テンプレートに`<ID>`のみが含まれる場合、Dynamic Mediaは`https://<server>/is/image`に入力します。`<server>`は「一般設定」で定義された公開サーバ名で、&lt;ID>は無効にするように選択されたアセットです。

1. ページ右下隅の「**[!UICONTROL 閉じる]**」をタップします。
1. Dynamic Mediaクラシック(Scene7)UIで、1つまたは複数のアセットを選択し、**[!UICONTROL ファイル/CDNを無効にする]**&#x200B;をタップします。 作成したテンプレートから生成された1つ以上のURLのリストと、選択したアセットが表示されます。 このリストに使用されているのは、アプリケーションの一般設定の「公開先サーバー名」にリストされているサーバー URL です。

   例えば、前の手順で設定した CDN 無効化テンプレートを使用して、`Backpack_B` という名前の画像アセットを 1 つだけ選択したとします。**[!UICONTROL ファイル/CDNを無効にする]**&#x200B;をタップすると、CDN無効化ユーザーインターフェイスで次のURLが生成されます。

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 「URLリスト」ボックスで、「**[!UICONTROL 継続]**」をタップして、特定のURLのキャッシュをクリアします。 URLは、編集することも、「URLリスト」ボックスに入力または貼り付けてURLを追加することもできます。事前にCDN無効化テンプレートを設定する必要はありません。

   「**[!UICONTROL 続行]**」をタップすると、キャッシュをクリアするのにかかる推定時間を示すインジケーターが表示されます。

   複数のアセットを選択した場合は、**[!UICONTROL ファイル/CDNを無効にする]**&#x200B;をタップすると、保存された&#x200B;**[!UICONTROL テンプレートURL]**&#x200B;で各アセットが参照されます。 したがって、**[!UICONTROL CDN無効化テンプレート]**&#x200B;を定義して、製品の詳細や検索結果など、Webサイトで参照されている各URL画像プリセットを参照できます。 これにより、キャッシュの無効化の対象として 1 つ以上の画像を選択したときに、それらの URL が自動的にインターフェイスに入力されます。

   >[!NOTE]
   >
   >アセットを選択し、**[!UICONTROL ファイル/CDNを無効にする]**&#x200B;をタップすると、Dynamic MediaはCDNを無効にするテンプレートを使用して、CDNから無効にするURLを自動的に作成します。 「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスに何も入力していないと、空白の URL リストが返されます。CDN におけるキャッシュは、アセットベースではありません。URL ベースです。したがって、Web サイト上での完全な URL を認識しておく必要があります。URL を特定した後は、上記の手順で、それらの URL を「**[!UICONTROL CDN 無効化テンプレート]**」テキストボックスに追加できます。これにより、アセットを選択し、ワンステップで URL を無効化することができます。
   >
   >もう 1 つのオプションとして、完全な URL を **[!UICONTROL CDN 無効化]**&#x200B;リストに追加する方法があります。この方法に従う場合は、**[!UICONTROL ファイル／CDN を無効にする]**&#x200B;オプションに進む前に Dynamic Media Classic でアセットを選択する必要はありません。

