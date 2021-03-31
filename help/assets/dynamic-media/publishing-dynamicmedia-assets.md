---
title: Dynamic Media アセットの公開
description: Dynamic Media アセットの公開方法を学習します。
contentOwner: Rick Brough
feature: アセット管理
topic: 業務担当者
role: 業務担当者
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 59%

---


# Dynamic Media アセットの公開 {#publishing-dynamic-media-assets}

Dynamic Media アセットを公開するには、既にアップロード済みのアセットを選択し、「**[!UICONTROL 公開]**」または「**[!UICONTROL クイック公開]**」をタップします。Dynamic Media アセットを公開すると、URL として Web ページに含めることや、Web ページにコードを埋め込むことができます。

また、ユーザーの介入なしに、アップロードしたアセットを即座に公開することもできます。または、選択してアセットを公開することもできます。[Dynamic Media の設定を参照してください。](config-dm.md) または、フォルダーレベルで **[!UICONTROL 選択的発行を使用して、相互に排他的なDynamic MediaまたはAdobe Experience Managerに選択的にアセットを]** 発行することもできます。詳しくは、[Dynamic Media での選択的公開の操作](/help/assets/dynamic-media/selective-publishing.md)を参照してください。

**[!UICONTROL カード表示]**&#x200B;で、アセット名のすぐ下、アセットが発行されたことを示す日時の左側に、小さな地球アイコンが表示されます。**[!UICONTROL リスト表示]**&#x200B;では、公開されたアセットと公開されていないアセットが「**[!UICONTROL 公開]**」列でわかります。

>[!NOTE]
>
>既にアセットが公開されている場合は、アセットを別のフォルダに移動し、新しい場所から再公開すると、元の公開済みアセットの場所と新しく再公開したアセットは引き続き使用できます。 ただし、元の公開済みアセットはExperience Managerに対して「失われる」ので、非公開にすることはできません。 したがって、ベストプラクティスとして、アセットを別のフォルダーに移動する前に、アセットを非公開にします。

ビデオアセットのエンコード後すぐに公開する場合は、エンコードが完了していることを確認します。 ビデオをエンコードすると、ビデオ処理ワークフローが進行中であることが通知されます。 ビデオのエンコーディングが完了したら、ビデオレンディションをプレビューできます。 その時点で、公開エラーが発生することなく、安全にビデオを公開できます。

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)も参照してください。

[Web ページへの Dynamic Media ビデオビューアまたは画像ビューアの埋め込み](embed-code.md)も参照してください。

>[!NOTE]
>
>* このURLを使用するには、アセットを公開する必要があります。 アセットが公開されていない場合、URLをコピーしてWebブラウザーに貼り付けることはできません。
>* ライブ配信をするには、画像プリセットおよびビューアプリセットをアクティベートして公開する必要があります。

>



一連のアセットを公開する方法について詳しくは、[アセットの公開](/help/assets/manage-digital-assets.md)を参照してください。

## Dynamic Media アセットの HTTP/2 配信  {#http-delivery-of-dynamic-media-assets}

Experience Managerで、HTTP/2を介したすべてのDynamic Mediaコンテンツ（画像およびビデオ）の配信がサポートされるようになりました。 つまり、画像やビデオの公開済み URL や埋め込みコードは、ホストされるアセットを受け取るアプリケーションとの統合に使用できます。その公開済みアセットは、その後、HTTP/2 プロトコルで配信されます。この配信方法により、ブラウザーとサーバーの通信が向上し、すべての Dynamic Media アセットの応答時間と読み込み時間が短くなります。

「[HTTP/2配信の内容に関するよくある質問](/help/assets/dynamic-media/http2faq.md)」を参照してください。

<!--this md file used to reside under sites-administering-->
