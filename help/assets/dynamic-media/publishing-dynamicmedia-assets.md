---
title: Dynamic Media アセットを公開
description: Dynamic Mediaビデオおよび画像アセットを公開し、URL を使用して Web ページに含めたり、Web ページにコードを埋め込んだりできるようにする方法について説明します。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
source-git-commit: 0e452bd94d75609ecc3c20ab6b56ded968ed0a70
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 100%

---

# Dynamic Media アセットの公開 {#publishing-dynamic-media-assets}

Dynamic Media アセットを公開するには、既にアップロード済みのアセットを選択し、「**[!UICONTROL 公開]**」または「**[!UICONTROL クイック公開]**」を選択します。Dynamic Media アセットを公開すると、URL として Web ページに含めることや、Web ページにコードを埋め込むことができます。

また、ユーザーの介入なしに、アップロードしたアセットを即座に公開することもできます。または、選択してアセットを公開することもできます。[Dynamic Media の設定](config-dm.md)を参照してください。または、フォルダーレベルで「**[!UICONTROL 選択的公開]**」を使用して、相互に排他的なアセットを Dynamic Media または Adobe Experience Manager に選択的に公開することもできます。詳しくは、[Dynamic Media での選択的公開の操作](/help/assets/dynamic-media/selective-publishing.md)を参照してください。

**[!UICONTROL カード表示]**&#x200B;で、アセット名のすぐ下、アセットが発行されたことを示す日時の左側に、小さな地球アイコンが表示されます。**[!UICONTROL リスト表示]**&#x200B;では、公開されたアセットと公開されていないアセットが「**[!UICONTROL 公開]**」列でわかります。

>[!NOTE]
>
>アセットが既に公開されていて、アセットを別のフォルダーに移動し、その移動先から再公開する場合は、新しく再公開されたアセットに加えて、元の公開済みアセットの場所も使用可能な状態のままです。ただし、最初に公開したアセットは Experience Manager からは「消失」しているので、非公開にすることができません。そのため、ベストプラクティスとしては、アセットを別のフォルダーに移動する前に、アセットを非公開にしてください。

ビデオアセットをエンコードした直後に公開する場合は、エンコードが完了していることを確認してください。ビデオのエンコードが完了していない場合は、ビデオ処理ワークフローが実行中であることが通知されます。ビデオのエンコードが完了すると、ビデオレンディションをプレビューできます。その時点で、公開エラーが発生することなく、安全にビデオを公開できます。

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)も参照してください。

[Web ページへの Dynamic Media ビデオビューアまたは画像ビューアの埋め込み](embed-code.md)も参照してください。

>[!NOTE]
>
>* アセットの URL を使用するには、そのアセットを公開する必要があります。アセットが公開されていない場合、URL をコピーして Web ブラウザーに貼り付けても機能しません。
>* ライブ配信をするには、画像プリセットおよびビューアプリセットをアクティベートして公開する必要があります。
>

一連のアセットを公開する方法について詳しくは、[アセットの公開](/help/assets/manage-digital-assets.md)を参照してください。

## Dynamic Media アセットの HTTP/2 配信 {#http-delivery-of-dynamic-media-assets}

Experience Manager では、HTTP/2 上でのすべての Dynamic Media コンテンツ（画像とビデオ）の配信をサポートするようになりました。つまり、画像やビデオの公開済み URL または埋め込みコードを、ホストされているアセットを受け入れる任意のアプリケーションと統合できるようになります。その公開済みアセットは、HTTP/2 プロトコルを使用して配信されます。この配信方法を使用すると、ブラウザーとサーバーの通信方法が改善され、すべてのDynamic Mediaアセットの応答時間と読み込み時間が向上します。

詳しくは、[コンテンツの HTTP/2 配信に関する FAQ](/help/assets/dynamic-media/http2faq.md) を参照してください。

<!--this md file used to reside under sites-administering-->
