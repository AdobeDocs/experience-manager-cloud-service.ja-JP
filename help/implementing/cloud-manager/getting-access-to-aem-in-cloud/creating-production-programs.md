---
title: '実稼動プログラムの作成 '
description: Cloud Manager を使用して、ライブトラフィックをホストする独自の実稼動プログラムを作成する方法について説明します。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
source-git-commit: cf6941759dfc1e50928009490c7c518a89ed093e
workflow-type: ht
source-wordcount: '362'
ht-degree: 100%

---


# 実稼動プログラムの作成 {#create-production-program}

実稼動プログラムの対象ユーザーは、AEM と Cloud Manager に精通し、ライブトラフィックをホストするためにコードをデプロイする目的でコードの作成、ビルドおよびテストを開始する準備が整っているユーザーです。

プログラムの種類について詳しくは、[プログラムとプログラムの種類について](program-types.md)のドキュメントを参照してください。

## ビデオチュートリアル {#video-tutorials}

Cloud Manager でプログラムを作成する方法については、次の 2 つのチュートリアルビデオをご覧ください。または[手順に関するドキュメント](#create)を参照してください。

>[!VIDEO](https://video.tv.adobe.com/v/334953)

>[!VIDEO](https://video.tv.adobe.com/v/334954)

## 実稼動プログラムの作成 {#create}

実稼動プログラムを作成するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 画面の右上隅にある「**プログラムを追加**」クリックします。

   ![Cloud Manager ランディングページ](assets/first_timelogin1.png)

1. プログラムの作成ウィザードで「**本番用にセットアップ**」を選択して、実稼動プログラムを作成します。デフォルトのプログラム名をそのまま使用するか編集してから、「**作成**」を選択します。

   ![プログラムの作成ウィザード](assets/create-prod1.png)

1. 次のタブで、プログラムに含めるソリューションを選択します。

   ![ソリューションの選択](assets/setup-prod-select.png)

1. ソリューション名の前にある山形アイコンをクリックすると、オプションのアドオンが表示されます（**Sites** の下の **Commerce** アドオンオプションなど）。

   ![アドオンを選択](assets/setup-prod-commerce.png)

1. ソリューションとアドオンを選択して、「**作成**」をクリックします。

プログラムが Cloud Manager により作成され、ランディングページに表示されて選択可能になります。

![Cloud Manager の概要](assets/navigate-cm.png)

## プログラムへのアクセス {#acessing}

1. ランディングページにプログラムカードが表示されたら、省略記号ボタンを選択して、使用可能なメニューオプションを表示します。

   ![プログラムの概要](assets/program-overview.png)

1. 「**プログラムの概要**」を選択して、Cloud Manager の&#x200B;**概要**&#x200B;ページに移動します。

1. 概要ページのメインコールトゥアクションカードのガイドに従って、環境、実稼動以外のパイプライン、そして最終的に実稼動パイプラインを作成できます。

   ![プログラムの概要](assets/set-up-prod5.png)

別のプログラムに切り替えたり、概要ページに戻って別のプログラムを作成したりする必要がある場合は、いつでも画面の左上のプログラム名をクリックして「**移動先**」オプションを表示します。

![](assets/create-program-a1.png) に移動します。

>[!NOTE]
>
>[サンドボックスプログラム](introduction-sandbox-programs.md#auto-creation)とは異なり、実稼動プログラムでは、Cloud Manager の適切な役割を持つユーザーがセルフサービス UI を使用してプロジェクトを作成し環境を追加する必要があります。
