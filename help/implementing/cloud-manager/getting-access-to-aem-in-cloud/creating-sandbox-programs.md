---
title: サンドボックスプログラムの作成
description: Cloud Manager を使用して、トレーニング、デモ、POC などの実稼動以外の用途に使用する独自のサンドボックスプログラムを作成する方法を説明します。
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: ht
source-wordcount: '434'
ht-degree: 100%

---

# サンドボックスプログラムの作成 {#create-sandbox-program}

サンドボックスプログラムは、通常、トレーニング、デモの実行、イネーブルメント、POC またはドキュメントの目的にかなうように作成されるもので、ライブトラフィックを実行するためのものではありません。

プログラムの種類について詳しくは、[プログラムとプログラムの種類について](program-types.md)のドキュメントを参照してください。

## サンドボックスプログラムの作成 {#create}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログオンし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、画面の右上隅付近に表示される「**プログラムを追加**」をタップまたはクリックします。

   ![Cloud Manager ランディングページ](assets/log-in.png)

1. プログラムの作成ウィザードで、「**サンドボックスを設定**」を選択し、プログラム名を入力します。

   ![指定タイプのプログラムの作成](assets/create-sandbox.png)

1. オプションとして、画像ファイルを&#x200B;**プログラム画像を追加**&#x200B;のターゲットにドラッグ＆ドロップするか、ファイルブラウザーからクリックして画像を選択することで、プログラムに画像を追加できます。「**続行**」を選択します。

   * 画像は、プログラムの概要ウィンドウのタイルとしてのみ機能し、プログラムを識別するのに役立ちます。

1. **サンドボックスの設定**&#x200B;ダイアログボックスで、**ソリューションとアドオン**&#x200B;テーブルのオプションにチェックを入れて、サンドボックスプログラムで有効にするソリューションを選択します。

   * ソリューション名の横にある山形括弧を使用して、ソリューションにオプションで追加できるアドオンを表示します。

   * **サイト**&#x200B;ソリューションおよび&#x200B;**アセット**&#x200B;ソリューションは、常にサンドボックスプログラムに含まれ、選択を解除することはできません。

   ![サンドボックス用のソリューションとアドオンを選択](assets/sandbox-solutions-add-ons.png)

1. サンドボックスプログラムのソリューションとアドオンを選択したら、「**作成**」をクリックします。

ランディングページに新しいサンドボックスプログラムカードが表示され、セットアッププロセスの進行に応じてステータスインジケーターも表示されます。

![概要ページからのサンドボックスの作成](assets/sandbox-setup.png)

## サンドボックスアクセス {#access}

サンドボックスのセットアップの詳細を表示できるほか、環境が使用可能になったら、プログラムの概要ページを表示して環境にアクセスできます。

1. Cloud Manager ランディングページで、作成したプログラムの省略記号ボタンをクリックします。

   ![プログラムの概要へのアクセス](assets/program-overview-sandbox.png)

1. プロジェクト作成手順が完了したら、Git リポジトリを使用できるように、「**リポジトリ情報にアクセス**」リンクにアクセスします。

   ![プログラム設定](assets/create-program4.png)

   >[!TIP]
   >
   >Git リポジトリへのアクセスと管理について詳しくは、[Git へのアクセス](/help/implementing/cloud-manager/managing-code/accessing-repos.md)を参照してください。

1. 開発環境が作成されたら、「**AEM にアクセス**」リンクをクリックして、AEM にログインします。

   ![「AEM にアクセス」リンク](assets/create-program5.png)

1. 実稼動以外のパイプラインによる開発環境へのデプロイメントが完了したら、コールトゥアクションのウィザードに従って、AEM 開発環境にアクセスしたり、開発環境にコードをデプロイしたりできます。

   ![サンドボックスのデプロイ](assets/create-program-setup-deploy.png)

>[!TIP]
>
>Cloud Manager の操作方法と&#x200B;**マイプログラム**&#x200B;コンソールについて詳しくは、[Cloud Manager UI の操作](/help/implementing/cloud-manager/navigation.md)を参照してください。
