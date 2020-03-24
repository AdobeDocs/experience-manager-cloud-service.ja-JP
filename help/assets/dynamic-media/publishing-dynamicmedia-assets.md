---
title: Dynamic Media アセットの公開
description: Dynamic Media アセットの公開方法
translation-type: tm+mt
source-git-commit: c8f8598e3e476af529a87b056e66ddb619a2da0a

---


# Dynamic Media アセットの公開 {#publishing-dynamic-media-assets}

You publish your Dynamic Media assets by selecting the assets and tapping **[!UICONTROL Publish]**. ダイナミックメディアアセットは、公開後、URL経由でWebページに含めたり、埋め込んだりすることができます。

また、ユーザの介入なしで、アップロードしたアセットを即座に公開することもできます。 または、選択してアセットを公開することもできます。 See [Configuring Dynamic Media](config-dm.md).

**[!UICONTROL カード表示]**&#x200B;では、小さい地球のアイコンがアセット名のすぐ下に表示され、アセットが公開されていることを示します。**[!UICONTROL リスト表示]**&#x200B;では、公開されたアセットと公開されていないアセットを「**[!UICONTROL 公開]**」列で確認できます。

>[!NOTE]
>
>アセットが既に公開済みの場合は、AEMを使用してアセットを別のフォルダーに移動し、新しい場所から再公開すると、元の公開済みアセットの場所と新しく再公開したアセットが引き続き使用できます。ただし、元の公開済みアセットはAEMに対して「失われる」ので、非公開にすることはできません。したがって、ベストプラクティスとして、アセットを別のフォルダに移動する前に、まずアセットの公開を取り消すことをお勧めします。

ビデオアセットをエンコードした直後に公開する場合は、エンコードが完了していることを確認します。ビデオのエンコードが進行中の場合、ビデオ処理ワークフローが進行中であることがシステムから通知されます。ビデオのエンコーディングが完了したら、ビデオのレンディションをプレビューできる必要があります。この時点で、投稿エラーを発生させずにビデオを投稿しても問題はありません。

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

See [HTTP/2 delivery of content frequently asked questions](/help/assets/dynamic-media/http2faq.md) to learn more.
<!--this md file used to reside under sites-administering-->
