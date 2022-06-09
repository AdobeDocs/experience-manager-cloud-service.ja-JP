---
title: '実稼動プログラムの作成 '
description: Cloud Manager を使用して、ライブトラフィックをホストする独自の実稼動プログラムを作成する方法について説明します。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
source-git-commit: 3557ddbc76ff21bcfe4ac0338f116b02b5135f2c
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 74%

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

1. プログラムの作成ウィザードで「**本番用にセットアップ**」を選択して、実稼動プログラムを作成します。既定のプログラム名を受け入れるか、クリックする前に編集することができます **続行**.

   ![プログラムの作成ウィザード](assets/create-prod1.png)

1. の **ソリューションとアドオン** 「 」タブで、プログラムに含めるソリューションを選択します。

   ![ソリューションを選択](assets/setup-prod-select.png)

1. ソリューション名の前にある山形アイコンをクリックすると、オプションのアドオンが表示されます（**Sites** の下の **Commerce** アドオンオプションなど）。

   ![アドオンを選択](assets/setup-prod-commerce.png)

1. ソリューションとアドオンを選択した状態で、 **続行**.

1. の **Go-Live 日** 「 」タブで、実稼動プログラムを運用開始する予定の日付を入力します。

   ![計画開始日の定義](assets/setup-go-live.png)

   * この日付はいつでも編集できます。
   * この日付は、情報提供のみを目的とし、プログラムの概要ページの Go Live ウィジェットをトリガーし、AEMas a Cloud Serviceのベストプラクティスドキュメントへの製品内リンクをタイムリーに提供し、Go Live エクスペリエンスの成功とスムーズ化を実現します。

1. 「**作成**」をクリックします。

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
