---
title: Dynamic Media アセットの公開
description: Dynamic Media アセットの公開方法
contentOwner: Rick Brough
translation-type: tm+mt
source-git-commit: b65ce0af6281f60272322744f0e6f81b7eb6b96a
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 100%

---


# Dynamic Media アセットの公開  {#publishing-dynamic-media-assets}

Dynamic Media アセットを公開するには、既にアップロード済みのアセットを選択し、「**[!UICONTROL 公開]**」または「**[!UICONTROL クイック公開]**」をタップします。Dynamic Media アセットを公開すると、URL として Web ページに含めることや、Web ページにコードを埋め込むことができます。

また、ユーザーの介入なしに、アップロードしたアセットを即座に公開することもできます。または、選択してアセットを公開することもできます。[Dynamic Media の設定を参照してください。](config-dm.md) または、フォルダーレベルで「**[!UICONTROL 選択的公開]**」を使用して、相互に排他的なアセットを Dynamic Media または AEM に選択的に公開することもできます。詳しくは、[Dynamic Media での選択的公開の操作](/help/assets/dynamic-media/selective-publishing.md)を参照してください。

**[!UICONTROL カード表示]**&#x200B;で、アセット名のすぐ下、アセットが発行されたことを示す日時の左側に、小さな地球アイコンが表示されます。**[!UICONTROL リスト表示]**&#x200B;では、公開されたアセットと公開されていないアセットが「**[!UICONTROL 公開]**」列でわかります。

>[!NOTE]
>
>アセットが既に公開されていて、AEM を使用してアセットを別のフォルダーに移動し、その移動先から再公開した場合は、新しく再公開されたアセットに加えて、元の公開済みアセットの場所も使用できる状態のままです。ただし、元の公開済みアセットは AEM からは「消失」しているので、非公開にすることができません。そのため、ベストプラクティスとしては、アセットを別のフォルダーに移動する前に、アセットを非公開にしてください。

ビデオアセットをエンコードした直後に公開する場合は、エンコードが完全に終了していることを確認してください。ビデオのエンコードがまだ完了していない場合は、ビデオ処理ワークフローが実行中であることが通知されます。ビデオのエンコードが完了すると、ビデオレンディションをプレビューできるようになります。その時点で、エラーが発生することなく、安全にビデオを公開できます。

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)も参照してください。

[Web ページへの Dynamic Media ビデオビューアまたは画像ビューアの埋め込み](embed-code.md)も参照してください。

>[!NOTE]
>
>* アセットの URL を使用するためには、そのアセットを公開する必要があります。アセットが公開されていない場合、URL をコピーして Web ブラウザーに貼り付けても機能しません。
>* ライブ配信をするには、画像プリセットおよびビューアプリセットをアクティベートして公開する必要があります。

>



一連のアセットを公開する方法について詳しくは、[アセットの公開](/help/assets/manage-digital-assets.md)を参照してください。

## Dynamic Media アセットの HTTP/2 配信  {#http-delivery-of-dynamic-media-assets}

AEM は現在、HTTP/2 上でのすべての Dynamic Media コンテンツ（画像とビデオ）の配信をサポートしています。つまり、画像やビデオの公開済み URL や埋め込みコードは、ホストされるアセットを受け取るアプリケーションとの統合に使用できます。その公開済みアセットは、その後、HTTP/2 プロトコルで配信されます。この配信方法により、ブラウザーとサーバーの通信が向上し、すべての Dynamic Media アセットの応答時間と読み込み時間が短くなります。

詳しくは、[コンテンツの HTTP/2 配信に関する FAQ](/help/assets/dynamic-media/http2faq.md) を参照してください。
<!--this md file used to reside under sites-administering-->
