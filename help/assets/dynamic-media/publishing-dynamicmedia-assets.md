---
title: Dynamic Media アセットの公開
description: Dynamic Media アセットの公開方法
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Dynamic Media アセットの公開 {#publishing-dynamic-media-assets}

You publish your Dynamic Media assets by selecting the assets and tapping **[!UICONTROL Publish]**. 動的メディアアセットは、公開後、URL経由でWebページに含めたり、埋め込みを使用してWebページに含めたりできます。

また、ユーザの介入なしで、アップロードしたアセットを即座に公開することもできます。 See [Configuring Dynamic Media](config-dm.md).

In the **[!UICONTROL Card View]**, a small globe icon appears directly below an asset&#39;s name to indicate that it is published. In the **[!UICONTROL List View]**, a **[!UICONTROL Published]** column indicates which assets are published or which are not.

>[!NOTE]
>
>アセットが既に公開されている場合は、AEMを使用してアセットを別のフォルダに移動し、新しい場所から再公開すると、元の公開済みアセットの場所と新しく再公開したアセットを引き続き使用できます。ただし、元の公開済みアセットはAEMに対して「失われる」ので、非公開にすることはできません。したがって、ベストプラクティスとして、アセットを別のフォルダーに移動する前に、アセットの公開を取り消す必要があります。

ビデオアセットをエンコードした直後に公開する場合は、エンコードが完全に完了していることを確認します。ビデオがエンコードされている間は、ビデオ処理ワークフローが進行中であることが通知されます。ビデオのエンコーディングが完了すると、ビデオのレンディションをプレビューできるようになります。この時点で、公開エラーが発生することなくビデオを公開しても安全です。

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)も参照してください。

[Web ページへのビデオビューアの埋め込み](embed-code.md)も参照してください。

>[!NOTE]
>
>* アセットの URL を使用するためには、そのアセットを公開する必要があります。アセットが公開されていない場合、URL をコピーして Web ブラウザーに貼り付けても機能しません。
>* ライブ配信をするには、画像プリセットおよびビューアプリセットをアクティベートして公開する必要があります。
>



一連のアセットを公開する方法について詳しくは、[アセットの公開](/help/assets/manage-digital-assets.md)を参照してください。

## Dynamic Media アセットの HTTP/2 配信 {#http-delivery-of-dynamic-media-assets}

AEM は現在、HTTP/2 上でのすべての Dynamic Media コンテンツ（画像とビデオ）の配信をサポートしています。つまり、画像やビデオの公開済み URL や埋め込みコードは、ホストされるアセットを受け取るアプリケーションとの統合に使用できます。その公開済みアセットは、その後、HTTP/2 プロトコルで配信されます。この配信方法により、ブラウザーとサーバーの通信が向上し、すべての Dynamic Media アセットの応答時間と読み込み時間が短くなります。

See [HTTP/2 delivery of content frequently asked questions](/help/assets/dynamic-media/scene7-http2faq.md) to learn more.
<!--this md file used to reside under sites-administering-->
