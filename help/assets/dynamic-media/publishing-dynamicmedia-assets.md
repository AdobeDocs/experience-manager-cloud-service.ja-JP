---
title: Dynamic Media アセットの公開
description: Dynamic Media アセットの公開方法を学習します。
contentOwner: Rick Brough
feature: アセット管理
role: Business Practitioner
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
source-git-commit: d3ee23917eba4a2e4ae1f2bd44f5476d2ff7dce1
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 49%

---

# Dynamic Media アセットの公開 {#publishing-dynamic-media-assets}

Dynamic Media アセットを公開するには、既にアップロード済みのアセットを選択し、「**[!UICONTROL 公開]**」または「**[!UICONTROL クイック公開]**」をタップします。Dynamic Media アセットを公開すると、URL として Web ページに含めることや、Web ページにコードを埋め込むことができます。

また、ユーザーの介入なしに、アップロードしたアセットを即座に公開することもできます。 または、選択してアセットを公開することもできます。[Dynamic Media の設定](config-dm.md)を参照してください。または、フォルダーレベルで&#x200B;**[!UICONTROL 選択的公開]**&#x200B;を使用して、相互に排他的なアセットをDynamic MediaまたはAdobe Experience Managerに選択的に公開することもできます。 [Dynamic Mediaでの選択的公開の操作](/help/assets/dynamic-media/selective-publishing.md)を参照してください。

**[!UICONTROL カード表示]**&#x200B;で、アセット名のすぐ下、アセットが発行されたことを示す日時の左側に、小さな地球アイコンが表示されます。**[!UICONTROL リスト表示]**&#x200B;では、公開されたアセットと公開されていないアセットが「**[!UICONTROL 公開]**」列でわかります。

>[!NOTE]
>
>既にアセットが公開されている場合は、そのアセットを別のフォルダーに移動し、新しい場所から再公開すると、新しく再公開されたアセットと共に、元の公開済みアセットの場所も引き続き使用できます。 ただし、元の公開済みアセットはExperience Managerに対して「失われる」ので、非公開にできません。 したがって、ベストプラクティスとして、アセットを別のフォルダーに移動する前に、アセットを非公開にします。

ビデオアセットをエンコードした後すぐに公開する場合は、エンコードがおこなわれていることを確認します。 ビデオがエンコードされると、システムによってビデオ処理ワークフローが進行中であることが通知されます。 ビデオのエンコーディングが完了すると、ビデオレンディションをプレビューできます。 その時点で、公開エラーが発生することなく、安全にビデオを公開できます。

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)も参照してください。

[WebページへのDynamic Mediaビデオビューアまたは画像ビューアの埋め込み](embed-code.md)も参照してください。

>[!NOTE]
>
>* このURLを使用するには、アセットを公開する必要があります。 アセットが公開されていない場合、URLのコピーおよびWebブラウザーへの貼り付けは機能しません。
>* ライブ配信をするには、画像プリセットおよびビューアプリセットをアクティベートして公開する必要があります。

>



セットまたはアセットの公開について詳しくは、[アセットの公開](/help/assets/manage-digital-assets.md)を参照してください。

## Dynamic Media アセットの HTTP/2 配信 {#http-delivery-of-dynamic-media-assets}

Experience Managerは、HTTP/2を介したすべてのDynamic Mediaコンテンツ（画像とビデオ）の配信をサポートするようになりました。 つまり、画像やビデオの公開済み URL や埋め込みコードは、ホストされるアセットを受け取るアプリケーションとの統合に使用できます。その公開済みアセットは、その後、HTTP/2 プロトコルで配信されます。この配信方法により、ブラウザーとサーバーの通信が向上し、すべての Dynamic Media アセットの応答時間と読み込み時間が短くなります。

[コンテンツのHTTP/2配信に関するよくある質問](/help/assets/dynamic-media/http2faq.md)を参照してください。

<!--this md file used to reside under sites-administering-->
