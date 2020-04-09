---
title: プログラムの作成 — クラウドサービス
description: プログラムの作成 — クラウドサービス
translation-type: tm+mt
source-git-commit: b30d9e37bb7de46aa252aa7030ab0c2de8610431

---


# プログラムの作成 {#create-a-program}

クラウドネイティブソリューションは、必要な権限と、セルフサービスモデルに関するプログラムの作成機能をユーザーに提供します。

プログラム作成ウィザードは、特定の顧客または組織が使用できるプログラムの範囲内で、ユーザーの目標に応じて詳細を送信するように求めます。

Cloud Managerへの初回アクセスのイベント、またはテナントにプログラムが存在しない場合は、「最初のプログラムを作成 **」画面が表示されます** 。 ユーザーが *Esc* を選択するか、ダイアログボックスの外をクリックすると、次の画面が表示されます。

![](assets/create-program1.png)


## 作成ウィザードのプログラム {#using-create-program-wizard}

特定の顧客/組織が使用できる範囲内でプログラムを作成するユーザーの目標に応じて、プログラム作成ウィザードによって、1つ以上の詳細を送信するように求められます。

![](assets/create-program-2.png)

>[!NOTE]
>If a program already exists, then you will see **Add Program** on the top right of the landing page, as shown in the figure below.

![](assets/create-program-add.png)

## デモプログラム {#create-demo-program}

>[!NOTE]
>デモプログラムは、Cloud Manager UIのサンドボックスプログラムに似ています。

次の手順に従って、サンドボックスプログラムを作成します。

1. プログラムの作成ウィザードで、「デ **モの設定」を選択します**。 「作成」を選択する前にプログラム名が送信 **されます**。

   ![](assets/create-program-setupdemo.png)

1. ランディングページ上に新しいSandboxプログラムカードが表示され、その上にマウスポインターを置いてCloud Managerアイコンを選択し、Cloud Managerの概要ページに移動できます。 カードは、新しく作成されたサンドボックスプログラムの自動セットアップの状態をユーザーに通知します。 ユーザーには進行状況が表示されます。

   ![](assets/program-create-setupdemo2.png)

1. プログラムの設定とプロジェクトの作成手順が完了すると、次の図に示すように、 **Git** （Gitを管理）リンクにアクセスできます。

   ![](assets/create-program4.png)

   >[!NOTE]
   >
   >Cloud Manager UIのセルフサービスGitアカウント管理を使用したGitリポジトリへのアクセスと管理の詳細については、Gitへのアクセスを参照 [してください](/help/implementing/cloud-manager/accessing-git.md)。


1. 開発環境を作成すると、次の図に示すよ **うにAEM** Linkにアクセスできます。

   ![](assets/create-program-5.png)

1. 開発への非実稼働パイプラインのデプロイが完了すると、ウィザードに従って、AEM（開発時）にアクセスするか、開発環境にコードをデプロイします。

   ![](assets/create-program-setup-deploy.png)

   >[!NOTE]
   >次に示すように、Cloud Managerの概要ページでプログラムの編集、切り替え、追加を行うこともできます。

   ![](assets/create-program-a1.png)



## 正規プログラム {#create-regular-program}

通常の *プログラムは* 、AEMとCloud Managerに精通しており、本番環境に導入する目的でコードの作成、構築、テストを開始する準備が整っているユーザーを対象としています。

次の手順に従って、正規プログラムを作成します。

1. 通常の **プログラムを作成するには** 、「実稼働用に設定」を選択します。 ユーザーは、デフォルトのプログラム名を受け入れるか、「続行」を選択する前に編集 **できま**&#x200B;す。

   ![](assets/set-up-prod1.png)

1. 上の画面の後に表示される画面のプログラムに含めるソリューションを選択します。



   >[!NOTE]
   >
   >次の画面は、複数のソリューションを購入した顧客のセグメントに対してのみ表示されます。 1つのソリューションのみを購入したお客様の場合、下のソリューション選択画面は表示されません。

   ![](assets/set-up-prod2.png)

1. Once you have selected the solutions, click **Create**.

   ![](assets/set-up-prod3.png)

1. ランディングページにプログラムカードが表示されたら、その上にマウスポインターを置いてCloud Managerアイコンを選択し、Cloud Managerの概要ページに移 **動します** 。

   ![](assets/set-up-prod4.png)

1. メインの誘い文句（CTA：コールトゥアクション）カードは、環境の作成、非実稼働パイプラインの作成、最後に実稼働パイプラインの作成をユーザーに指示します。
   ![](assets/set-up-prod5.png)


   >[!NOTE]
   >
   >A regular program does not have **Auto-setup** feature.





