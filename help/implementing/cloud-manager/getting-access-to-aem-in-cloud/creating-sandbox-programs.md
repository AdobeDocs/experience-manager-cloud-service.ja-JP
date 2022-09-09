---
title: サンドボックスプログラムの作成
description: Cloud Manager を使用して、トレーニング、デモ、POC などの実稼動以外の用途に使用する独自のサンドボックスプログラムを作成する方法を説明します。
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
source-git-commit: cf6941759dfc1e50928009490c7c518a89ed093e
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 100%

---

# サンドボックスプログラムの作成 {#create-sandbox-program}

サンドボックスプログラムは、通常、トレーニング、デモの実行、イネーブルメント、POC またはドキュメントの目的にかなうように作成されるもので、ライブトラフィックを実行するためのものではありません。

プログラムの種類について詳しくは、[プログラムとプログラムの種類について](program-types.md)のドキュメントを参照してください。

## サンドボックスプログラムの作成 {#create}

サンドボックスプログラムを作成するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. Cloud Manager のランディングページで、画面の右上隅にある「**プログラムを追加**」をクリックします。

   ![Cloud Manager ランディングページ](assets/first_timelogin1.png)

1. プログラム作成ウィザードで、「**サンドボックスを設定する**」を選択し、プログラム名を入力して、「**作成**」をクリックします。

   ![指定タイプのプログラムの作成](assets/create-sandbox.png)

ランディングページに新しいサンドボックスプログラムカードが表示され、セットアッププロセスの進行に応じてステータスインジケーターも表示されます。

![概要ページからのサンドボックスの作成](assets/program-create-setupdemo2.png)

## サンドボックスへのアクセス {#access}

サンドボックスのセットアップの詳細を表示できるほか、環境が使用可能になったら、プログラムの概要ページを表示して環境にアクセスできます。

1. Cloud Manager ランディングページで、新しく作成したプログラムの省略記号ボタンをクリックします。

   ![プログラムの概要へのアクセス](assets/program-overview-sandbox.png)

1. プロジェクト作成手順が完了したら、Git リポジトリを使用できるように、「**リポジトリ情報にアクセス**」リンクをクリックします。

   ![プログラム設定](assets/create-program4.png)

   >[!TIP]
   >
   >Git リポジトリへのアクセスと管理について詳しくは、[Git へのアクセス](/help/implementing/cloud-manager/managing-code/accessing-repos.md)のドキュメントを参照してください。

1. 開発環境が作成されたら、「**AEM にアクセス**」リンクをクリックして、AEM にログインします。

   ![「AEM にアクセス」リンク](assets/create-program-5.png)

1. 実稼動以外のパイプラインによる開発環境へのデプロイメントが完了したら、ウィザードに従って、AEM 開発環境にアクセスしたり、開発環境にコードをデプロイしたりできます。

   ![サンドボックスのデプロイ](assets/create-program-setup-deploy.png)

別のプログラムに切り替えたり、概要ページに戻って別のプログラムを作成したりする必要がある場合は、いつでも画面の左上のプログラム名をクリックして「**移動先**」オプションを表示します。

![](assets/create-program-a1.png) に移動します。
