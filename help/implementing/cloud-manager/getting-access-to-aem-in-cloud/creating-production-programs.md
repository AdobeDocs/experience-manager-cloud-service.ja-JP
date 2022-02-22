---
title: '実稼働プログラムの作成 '
description: Cloud Manager を使用して、ライブトラフィックをホストする独自の実稼動プログラムを作成する方法について説明します。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
source-git-commit: cf6941759dfc1e50928009490c7c518a89ed093e
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 2%

---


# 実稼働プログラムの作成 {#create-production-program}

実稼働プログラムは、AEMと Cloud Manager に詳しく、コードの記述、構築、テストを開始し、ライブトラフィックをホストするためにコードをデプロイする準備が整っているユーザーを対象としています。

プログラムの種類について詳しくは、ドキュメントを参照してください [プログラムとプログラムの種類について](program-types.md)

## ビデオTutorials {#video-tutorials}

Cloud Manager でのプログラムの作成方法を学ぶには、次の 2 つのチュートリアルビデオをご覧ください。 [ドキュメントに記載された手順に従います。](#create)

>[!VIDEO](https://video.tv.adobe.com/v/334953)

>[!VIDEO](https://video.tv.adobe.com/v/334954)

## 実稼動プログラムの作成 {#create}

実稼動プログラムを作成するには、次の手順に従います。

1. Cloud Manager( ) にログインします。 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 適切な組織を選択します。

1. クリック **プログラムの追加** 画面の右上隅から。

   ![Cloud Manager ランディングページ](assets/first_timelogin1.png)

1. 選択 **実稼動用に設定** （「プログラムの作成」ウィザード）をクリックし、実稼働用プログラムを作成します。 デフォルトのプログラム名を受け入れるか、選択前に編集することができます **作成**.

   ![プログラムウィザードの作成](assets/create-prod1.png)

1. 次のタブで、プログラムに含めるソリューションを選択します。

   ![ソリューションを選択](assets/setup-prod-select.png)

1. ソリューション名の前の山形記号をクリックすると、「 **コマース** 以下のアドオンオプション **サイト**.

   ![アドオンを選択](assets/setup-prod-commerce.png)

1. ソリューションとアドオンを選択した状態で、 **作成**.

プログラムは Cloud Manager で作成され、ランディングページに表示されて選択可能になります。

![Cloud Manager の概要](assets/navigate-cm.png)

## プログラムにアクセス {#acessing}

1. ランディングページにプログラムカードが表示されたら、省略記号ボタンを選択して、使用可能なメニューオプションを表示します。

   ![プログラムの概要](assets/program-overview.png)

1. 選択 **プログラムの概要** Cloud Manager の **概要** ページ。

1. 概要ページのメインのコールトゥアクションカードでは、環境、非実稼動パイプライン、最後に実稼動パイプラインの作成手順をガイドします。

   ![プログラムの概要](assets/set-up-prod5.png)

別のプログラムに切り替えたり、概要ページに戻って別のプログラムを作成する必要がある場合は、画面の左上にあるプログラム名をクリックすると、 **に移動します。** オプション。

![](assets/create-program-a1.png) に移動します。

>[!NOTE]
>
>とは異なる [サンドボックスプログラム](introduction-sandbox-programs.md#auto-creation) 実稼動プログラムでは、適切な Cloud Manager の役割を持つユーザーがプロジェクトを作成し、セルフサービス UI を使用して環境を追加する必要があります。
