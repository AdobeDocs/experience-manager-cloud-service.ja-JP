---
title: 実稼動プログラムの作成
description: Cloud Manager を使用して、ライブトラフィックをホストする独自の実稼動プログラムを作成する方法について説明します。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
source-git-commit: 79d3ec7f5ede84fd989b7d5440739ec9560a547f
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 88%

---


# 実稼動プログラムの作成 {#create-production-program}

実稼動プログラムの対象ユーザーは、AEM と Cloud Manager に精通し、ライブトラフィックをホストするためにコードをデプロイする目的でコードの作成、ビルドおよびテストを開始する準備が整っているユーザーです。

プログラムの種類について詳しくは、[プログラムとプログラムの種類について](program-types.md)のドキュメントを参照してください。

## 実稼動プログラムの作成 {#create}

実稼動プログラムを作成するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 次の日： **[マイプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 画面、タップまたはクリック **プログラムの追加** をクリックします。

   ![Cloud Manager ランディングページ](assets/log-in.png)

1. プログラムを作成ウィザードで「**実稼動用に設定**」を選択して、実稼動プログラムを作成し、プログラム名を指定します。

   ![プログラム作成ウィザード](assets/create-production-program.png)

1. オプションとして、画像ファイルを&#x200B;**プログラム画像を追加**&#x200B;のターゲットにドラッグ＆ドロップするか、ファイルブラウザーからクリックして画像を選択することで、プログラムに画像を追加できます。「**続行**」を選択します。

1. 必要な権限がある場合は、**セキュリティ**&#x200B;タブが表示され、実稼動プログラム用に **HIPAA** および／または **WAF-DDOS 保護**&#x200B;をアクティベートするオプションが提供されます。作成するプログラムに必要な場合は、該当するオプションをオンにしてから、**続行**&#x200B;を選択します。

   * プログラムの作成後に HIPAA を有効または無効にすることはできません。
      * アドビの HIPAA 対応ソリューションの実装について詳しくは、[こちら](https://www.adobe.com/go/hipaa-ready)を参照してください。
   * 有効化すると、WAF-DDOS 保護は、[実稼動以外のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)で設定できます。

   ![セキュリティオプション](assets/create-production-program-security.png)

1. 「**ソリューションとアドオン**」タブで、プログラムに含めるソリューションを選択します。

   * 利用可能な様々なソリューションに対して 1 つ以上のプログラムが必要かどうかが不明な場合は、最も興味のあるプログラムを選択します。後で[プログラムを編集](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)することで、追加のソリューションをアクティブ化することができます。プログラム設定の推奨事項について詳しくは、[実稼動プログラムの概要ドキュメント](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)を参照してください。
   * 以前に「**セキュリティの強化を有効にする**」を選択した場合は、HIPAA 資格が使用可能なソリューションのみを選択できます。

   ![ソリューションを選択](assets/setup-prod-select.png)

1. ソリューション名の前の山形記号をクリックすると、オプションのアドオンが表示されます。例えば、**Sites** で **Commerce** アドオンオプションを選択できます。

   ![アドオンを選択](assets/setup-prod-commerce.png)

1. ソリューションやアドオンを選択してから、「**続行**」をクリックします。

1. 「**開始日**」タブで、実稼動プログラムの運用開始予定日を入力します。

   ![運用開始予定日の定義](assets/setup-go-live.png)

   * この日付はいつでも編集できます。
   * この日付は、情報提供のみを目的とし、Go Live ウィジェットを [**プログラムの概要** ページ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview) AEMas a Cloud Serviceのベストプラクティスドキュメントへの製品内リンクをタイムリーに提供し、Go Live の成功とスムーズな運用を実現するジャーニーに合わせます。

1. 「**作成**」をクリックします。

プログラムが Cloud Manager により作成され、ランディングページに表示されて選択可能になります。

![Cloud Manager の概要](assets/navigate-cm.png)

## プログラムへのアクセス {#accessing}

1. ランディングページにプログラムカードが表示されたら、省略記号（...）ボタンを選択して、使用可能なメニューオプションを表示します。

   ![プログラムの概要](assets/program-overview.png)

1. 「**プログラムの概要**」を選択して、Cloud Manager の&#x200B;**概要**&#x200B;ページに移動します。

1. 概要ページのメインコールトゥアクションカードのガイドに従って、環境、実稼動以外のパイプライン、そして最終的に実稼動パイプラインを作成できます。

   ![プログラムの概要](assets/set-up-prod5.png)

別のプログラムに切り替えたり、概要ページに戻って別のプログラムを作成したりする必要がある場合は、いつでも画面の左上のプログラム名をクリックして「**移動先**」オプションを表示します。

![](assets/create-program-a1.png) に移動します。

>[!NOTE]
>
>[サンドボックスプログラム](introduction-sandbox-programs.md#auto-creation)とは異なり、実稼動プログラムでは、Cloud Manager の適切な役割を持つユーザーがセルフサービス UI を使用してプロジェクトを作成し環境を追加する必要があります。
