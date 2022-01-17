---
title: Cloud Manager を使用したクラウドリソースの設定
description: このページでは、Cloud Manager を使用してクラウドリソースを設定する方法について説明します
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: ht
source-wordcount: '1428'
ht-degree: 100%

---

# Cloud Manager を使用したクラウドリソースの設定 {#setup-cloud-resources}

ビジネスオーナーの役割に割り当てられたシステム管理者が、Cloud Manager にアクセスしてログインする。その後、ビジネスオーナー製品プロファイルに割り当てられたチームメンバーは、Cloud Manager にログインし、クラウドプログラムと環境を作成して、エキスパートチームが作業を開始できるようにする必要があります。

## 目的 {#objective}

このドキュメントでは、クラウドリソースの作成方法と作成者について説明します。

この節を読むと、次の内容を理解できます。

* ビジネスオーナーの役割に割り当てられたシステム管理者は、Cloud Manager にアクセスしてログインする最初のユーザーである必要がある。
* クラウドプログラムと環境の作成方法。

## はじめに {#introduction}

クラウドリソースの追加は、Cloud Manager ビジネスオーナー製品プロファイルに割り当てられたチームメンバーが Cloud Manager を使用して行います。通常、このユーザーは、ビジネスニーズを理解し、Cloud Manager の初期設定を完了するユーザーです。

以下の節では、[クラウドサービスプログラム](#create-cloud-service-program)と[環境](#create-cloud-environments)の作成方法について説明します。

### 前提条件 {#prerequisites}

* ビジネスオーナーの役割に割り当てられたシステム管理者が、Cloud Manager にアクセスしてログインする。

* [Cloud Manager に移動してログインする](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=ja)方法を理解している。

* [Cloud Manager の製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#cloud-manager-product-profiles)を理解している。

* Cloud Manager の[プログラム](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html?lang=ja)と[環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=ja)の概念を理解している。

## Cloud Manager への移動 {#navigate-cloud-manager}

作業を開始するためのリンクが記載された「ようこそ」電子メールがビジネスオーナーユーザーに届きます。リンクが見つからない場合は、Adobe ID を使用してログインすることで、[Cloud Manager](https://my.cloudmanager.adobe.com/) に直接アクセスします。

Cloud Manager にアクセスするには、次の手順に従います。

1. お知らせメールで、「**使用を開始**」をクリックします（下図を参照）。
   ![](/help/journey-onboarding/assets/get-started-email.png)

1. Cloud Manager の&#x200B;**プログラムと製品**&#x200B;ページに移動します。

   >[!IMPORTANT]
   >または、[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) から Cloud Manager の&#39;ログインページに直接移動することもできます。今後 Cloud Manager のランディングページに直接移動する際に役立つように、このページをブックマークに追加してください。

1. Cloud Manager のランディングページに移動します。詳しくは、[Cloud Manager のプログラムの表示](#viewing-programs)の節を参照してください。

さらに、Adobe Experience Cloud のホームページから Cloud Manager の「**プログラムと製品**」ページに移動できます。次の手順に従います。

1. [Adobe Experience Cloud](https://experience.adobe.com) に直接移動し、Adobe ID を使用してログインします。

1. Adobe Experience Cloud のホームページで、「**Experience Manager**」を選択します。

   ![](/help/journey-onboarding/assets/setup-resources2.png)

1. AEM ホームページが表示されます。ここから、 **Cloud Manager** を起動します。

   ![](/help/journey-onboarding/assets/setup-resources3.png)

1. 正常にログインすると、Cloud Manager のランディングページが表示されます。詳しくは、[Cloud Manager のプログラムの表示](#viewing-programs)の節を参照してください。

   >[!NOTE]
   >[!UICONTROL Cloud Manager] で割り当てられた役割とアプリケーションの状態によっては、[!UICONTROL Cloud Manager] UI の使用中に異なる画面が表示されます。

### Cloud Manager のランディングページでのプログラムの表示 {#viewing-programs}

正常にログインすると、Cloud Manager のランディングページが表示されます。次に示す 3 つのオプションのいずれかが表示されます。

#### Cloud Manager にプログラムが存在しません {#no-programs}

組織にプログラムが存在しない場合は、最初のプログラムを作成するようにランディングページで指示されます（下図を参照）。


![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### プログラムは既に Cloud Manager に存在します {#programs-exist}

組織にプログラムが既に存在する場合は、別のプログラムを追加するようにランディングページで指示され、既存のプログラムがすべてランディングページに表示されます（下図を参照）。

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### プログラムが存在しユーザーがシステム管理者です {#programs-exist-sysadmin}

組織にプログラムが既に存在し、ユーザーがシステム管理者である場合は、次の図に示すように、ランディングページに「**アクセスを管理**」ボタンと「**プログラムを追加**」オプションが表示されます。

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## ユーザーの役割の確認 {#verify-user-roles}

Cloud Manager に正常にログインしたら、以下の手順に従って、ビジネスオーナー製品プロファイルが割り当てられていることを確認します。

1. 右上のプロファイルを選択します（下図を参照）。

   ![](/help/journey-onboarding/assets/setup-resources5.png)

1. 「**ユーザーの役割**」を選択し、ビジネスオーナーに割り当てられていることを確認します。

   ![](/help/journey-onboarding/assets/setup-resources6.png)

1. これで、ビジネスオーナーとしてのユーザーの役割を確認できました。

   ![](/help/journey-onboarding/assets/setup-resources7.png)

   お疲れ様でした。Cloud Manager にビジネスオーナーとして正常にログインしました。

## クラウドサービスプログラムの作成 {#create-cloud-service-program}

Cloud Manager からクラウドサービスプログラムを作成するには、以下の手順に従います。

1. 次に示すように、Cloud Manager ランディングページに移動します。

   >[!NOTE]
   >この手順を正常に完了するには、 Cloud Manager ビジネスオーナー製品プロファイルに割り当てられているチームメンバーである必要があります。

   ここから、「**プログラムの追加**」をクリックして、「プログラムの追加」ウィザードを起動します。

   ![](/help/journey-onboarding/assets/setup-resources4.png)

   >[!NOTE]
   >AEM as a Cloud プログラムの作成方法と、プログラムを作成する前の重要な検討事項については、[ビデオ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=ja)をご覧ください。

   >[!IMPORTANT]
   >プログラムの追加ウィザードの使い方に関する詳しい手順については、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/production-programs/creating-production-program.html?lang=ja)を参照してください。
   >
   >* 作成後はプログラム名を変更できないのでご注意ください。プログラムに付ける名前に関して明確にしておくことをお勧めします。
   >* プログラム名を変更する必要がある場合は、Adobe サポートまたは Adobe 担当者にお問い合わせください。実質的にプログラムを削除することになるので、一からやり直す必要があり、チームの作業が失われる可能性があります。


1. クラウドプログラムが正常に作成されたら、プログラムに移動して、以下に示すように、プログラムの&#x200B;**概要**&#x200B;ページを確認できます。

   ![](/help/journey-onboarding/assets/setup-resources8.png)

   >[!NOTE]
   >開発者メンバーを Cloud Manager チームにまだ追加していない場合は、ここで追加するとよいでしょう。「開発者製品プロファイルへのユーザーの追加」を参照し、その手順に従います。

1. デベロッパー製品プロファイルに割り当てられたメンバーは、Cloud Manager にログインし、[Cloud Manager Git を管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=ja)できます。

   お疲れさまでした。プログラムが正常に作成され、デベロッパーが Cloud Manager Git にアクセスできるようになりました。


## クラウド環境の作成 {#create-cloud-environments}

クラウドプログラムを正常に作成したら、クラウド環境を作成します。

Cloud Manager からクラウド環境を作成するには、次の手順に従います。

1. Cloud Manager の&#x200B;**概要**&#x200B;ページに移動し、環境カードから「**追加**」を選択します。

   ![](/help/journey-onboarding/assets/setup-resources9.png)

   >[!IMPORTANT]
   >この手順を正常に完了するには、ビジネスオーナーまたはデプロイメントマネージャーの役割を持つ Cloud Manager ユーザーがログインする必要があります。

   さらに、[ビデオ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=ja)のクイックチュートリアルでは、Cloud Manager 環境と、それらの環境をプログラムに追加する方法についても説明しています。

1. 環境の追加ウィザードが起動し、環境の追加を指示します。ウィザードに慣れるには、まず開発環境を追加してください。詳しくは、[環境の追加](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=ja#adding-environments)を参照してください。

   >[!NOTE]
   >開発者メンバーを Cloud Manager チームにまだ追加していない場合は、ここで追加するとよいでしょう。「開発者製品プロファイルへのユーザーの追加」を参照し、その手順に従います。

1. デベロッパー製品プロファイルに割り当てられたメンバーは、Cloud Manager にログインし、[Cloud Manager Git を管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=ja)できます。

   お疲れさまでした。プログラムが正常に作成され、開発者が Cloud Manager Git にアクセスできるようになりました。

   おめでとうございます。これで、クラウドプログラム環境が作成され、デベロッパーがチームに追加されました。

## 次の手順 {#whats-next}

Cloud Manager を管理する権限では不十分なので、チームメンバーにインスタンスに対する権限を付与する必要があります。システム管理者は、クラウドリソースが作成され、チームがアクセスする準備が整ったら、Adobe Admin Console でチームメンバーを AEM as a Cloud Service 製品プロファイルに割り当てる必要があります。

>[!NOTE]
>AEM as a Cloud Service ユーザーにアクセス権を付与するには、`AEM Users` または `AEM Administrators` のいずれかの製品プロファイルに属している必要があります。詳しくは、](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=ja#managing-products-and-user-access-in-admin-console)Admin Console での製品とユーザーアクセスの管理[を参照してください。

[AEM as a Cloud Service 製品プロファイルへのチームメンバーの割り当て](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md)のドキュメントを次に確認して、オンボーディングジャーニーを続けてください。


## その他のリソース {#additional-resources}

その他のリソースでは、以下について学習します。

* [プログラムタイプとプログラムの追加](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=ja)
* [環境タイプと環境の追加](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=ja)
* [Cloud Manager Git の管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=ja)
* [Admin Console からの AEM as a Cloud Service へのアクセスの設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=ja#adobe-ims-users)
