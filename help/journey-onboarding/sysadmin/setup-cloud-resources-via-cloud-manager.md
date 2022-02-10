---
title: Cloud Manager を使用したクラウドリソースのセットアップ
description: Cloud Manager を使用して独自のクラウドリソースを設定および管理する方法について説明します。
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 19%

---

# Cloud Manager を使用したクラウドリソースのセットアップ {#setup-cloud-resources}

Cloud Manager を使用して独自のクラウドリソースを設定および管理する方法について説明します。

## 目的 {#objective}

このドキュメントでは、クラウドリソースの作成方法と作成者について説明します。 この説を読み終えると、以下を理解できます。

* システム管理者が **ビジネスオーナー** の役割は、組織で Cloud Manager にログインしてアクセスする最初の役割である必要があります。
* クラウドプログラムと環境の作成方法。

## はじめに {#introduction}

クラウドリソースの追加は、Cloud Manager を通じて、 **ビジネスオーナー** 製品プロファイル。 通常、このユーザーは、ビジネスニーズを理解し、Cloud Manager の初期設定を完了するユーザーです。

以下の節では、 [クラウドサービスプログラム](#create-cloud-service-program) および [環境。](#create-cloud-environments)

### 前提条件 {#prerequisites}

* システム管理者が **ビジネスオーナー** の役割は、Cloud Manager にログインしておく必要があります。 **ビジネスオーナー** ロールは、このドキュメントで説明されている手順を実行するために Cloud Manager にアクセスしようとします。

   * に戻る [Cloud Manager 製品プロファイルへのチームメンバーの割り当て](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) このジャーニーのドキュメントを参照してください。

* 次の方法を理解する必要があります。 [Cloud Manager に移動してログインします。](/help/onboarding/learn-concepts/cloud-manager-introduction.md)

* 君は～をよく知っているべきだ。 [Cloud Manager 製品プロファイル。](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)

* Cloud Manager の概念を理解する必要があります [プログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/understand-program-types.md) および [環境。](/help/implementing/cloud-manager/manage-environments.md)

## システム管理者およびビジネスオーナーとして Cloud Manager にアクセス {#access-sysadmin-bo}

割り当てたチームメンバーの前に **ビジネスオーナー** の役割は cloud manager にアクセスし、クラウドリソースの作成を開始できます。システム管理者には、 **ビジネスオーナー** ロールを作成し、Cloud Manager にログインします。

1. システム管理者が、 **ビジネスオーナー** ロールが割り当てられました。

   * このジャーニーの前の手順に戻ります。 [Cloud Manager 製品プロファイルへのチームメンバーの割り当て](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) 割り当てに関する詳細 **ビジネスオーナー** の役割をシステム管理者に割り当てます（まだ割り当てていない場合）。

1. で Cloud Manager にログインする [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 通常のランディングページが表示されます。

を使用してシステム管理者として正常にサインインする **ビジネスオーナー** ロールを使用する場合、他のユーザーが使用する Cloud Manager を **ビジネスオーナー** 役割。 このメッセージやメッセージの確認はお送りしません。 サインインで十分です。

を使用して Cloud Manager にシステム管理者としてログインするまで、 **ビジネスオーナー** 役割、 **ビジネスオーナー** ロールは、適切なロールが割り当てられている場合でも、Cloud Manager でプログラムを作成できません。

## Cloud Manager への移動 {#navigate-cloud-manager}

ユーザーの **ビジネスオーナー** の役割には、開始するためのリンクが記載された「ようこそ」の電子メールが届きます。 このようこそメールを使用して Cloud Manager に移動するには、以下の手順に従います。

1. お知らせメールで、「**使用を開始**」をクリックします（下図を参照）。
   ![電子メールの例](/help/journey-onboarding/assets/get-started-email.png)

1. Cloud Manager の&#x200B;**プログラムと製品**&#x200B;ページに移動します。

   >[!TIP]
   >
   >また、次の場所から Cloud Manager のログインページに直接移動することもできます。 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). 今後の参照用に、このページをブックマークに追加してください。

1. Cloud Manager のランディングページに移動します。詳しくは、[Cloud Manager のプログラムの表示](#viewing-programs)の節を参照してください。

また、Cloud Manager の **プログラムと製品** 次の手順に従って、Adobe Experience Cloudホームページからページを開きます。

1. [Adobe Experience Cloud](https://experience.adobe.com) に直接移動し、Adobe ID を使用してログインします。

1. Adobe Experience Cloud のホームページで、「**Experience Manager**」を選択します。

   ![Experience Cloudホームページ](/help/journey-onboarding/assets/setup-resources2.png)

1. AEM ホームページが表示されます。ここから、 **起動** の **Cloud Manager** タイル。

   ![AEMホームページ](/help/journey-onboarding/assets/setup-resources3.png)

1. 正常にログインすると、Cloud Manager のランディングページが表示されます。詳しくは、[Cloud Manager のプログラムの表示](#viewing-programs)の節を参照してください。

Cloud Manager を使用してプログラムや製品にアクセスする方法はユーザー次第で、Cloud Manager の使用方法やプログラムの管理方法には影響しません。

>[!NOTE]
>
>[!UICONTROL Cloud Manager] で割り当てられた役割とアプリケーションの状態によっては、[!UICONTROL Cloud Manager] UI の使用中に異なる画面が表示されます。

### プログラムの表示 {#viewing-programs}

Cloud Manager に正常にアクセスすると、表示される内容は、以降の節で説明するように、プログラムの状態によって異なります。

#### プログラムが存在しない場合 {#no-programs}

組織にプログラムが存在しない場合は、最初のプログラムを作成するようにランディングページに指示されます。

![プログラムがありません](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### プログラムが既に存在する場合 {#programs-exist}

組織にプログラムが既に存在する場合は、ランディングページに既存のプログラムが表示され、追加のプログラムを追加するボタンも表示されます。

![プログラムが存在します](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### プログラムが存在し、システム管理者である場合 {#programs-exist-sysadmin}

組織にプログラムが既に存在し、システム管理者である場合は、ランディングページが表示されます **アクセスを管理** ～と一緒に **プログラムの追加** オプション。

![システム管理者ビュー](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## ユーザーの役割の確認 {#verify-user-roles}

Cloud Manager に正常にログインすると、 **ビジネスオーナー** 製品プロファイル。

1. ウィンドウの右上からプロファイルを選択します。

   ![ユーザープロファイル](/help/journey-onboarding/assets/setup-resources5.png)

1. 選択 **ユーザーの役割** ：ユーザーに割り当てられているロールを表示します。

   ![ユーザーの役割](/help/journey-onboarding/assets/setup-resources6.png)

1. ユーザーが **ビジネスオーナー** 役割。

   ![ユーザーの役割のリスト](/help/journey-onboarding/assets/setup-resources7.png)

Cloud Manager にビジネスオーナーとして正常にログインしました。まだ **ビジネスオーナー** の役割については、システム管理者にお問い合わせください。

## Cloud Serviceプログラムの作成 {#create-cloud-service-program}

これで、適切なアクセス権が確保されたので、最初のプログラムを作成できます。

1. Cloud Manager ランディングページ ( ) に移動します。 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) にログインし、

1. Cloud Manager のランディングページで、 **プログラムの追加** をクリックして、プログラムの追加ウィザードを起動します。

   ![ランディングページ](/help/journey-onboarding/assets/setup-resources4.png)

   >[!TIP]
   >
   >プログラムの追加ウィザードの使用方法に関する詳細な手順については、このドキュメントを参照してください [実稼働プログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-program.md) またはこれをご覧ください [ビデオ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) AEM as a Cloud プログラムを作成する方法と、プログラムを作成する前に重要な考慮事項について学ぶには、以下を参照してください。


1. クラウドプログラムが正常に作成されたら、 Cloud Manager のランディングページからプログラムに移動して、 **概要** ページを開きます。

   ![プログラムの概要](/help/journey-onboarding/assets/setup-resources8.png)

1. デベロッパー製品プロファイルに割り当てられたメンバーは、 Cloud Manager にログインして、Cloud Manager の Git リポジトリを管理できます。

   * まだメンバーを割り当てていない場合は、今すぐ、 **開発者** の役割が Cloud Manager チームに割り当てられていることを確認します。 に戻る [Cloud Manager 製品プロファイルへのチームメンバーの割り当て](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) このジャーニーのドキュメントを参照してください。

これで、プログラムが正常に作成され、Cloud Manager の Git リポジトリを開発者が使用できるようになりました。

## クラウド環境の作成 {#create-cloud-environments}

クラウドプログラムを正常に作成したら、クラウド環境を作成します。

1. Cloud Manager ランディングページ ( ) に移動します。 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) を選択し、 **追加** を設定します。

   ![環境を追加ボタン](/help/journey-onboarding/assets/setup-resources9.png)

1. 環境を追加ウィザードが起動し、環境の追加手順が示されます。 ウィザードに慣れるには、まず開発環境を追加してください。

   >[!TIP]
   >
   >ドキュメントを参照します。 [環境の追加](/help/implementing/cloud-manager/manage-environments.md#adding-environments) 多くを学ぶ、または見る [このクイックビデオチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) Cloud Manager 環境と、それらをプログラムに追加する方法について説明します。

1. に割り当てられたメンバー **開発者** 製品プロファイルは、 Cloud Manager にログインして Cloud Manager の Git リポジトリーを管理できます。

これで、プログラムが正常に作成され、開発者が Cloud Manager の Git にアクセスできるようになりました。

## 次の手順 {#whats-next}

クラウドリソースが作成され、チームからアクセスする準備が整ったので、システム管理者は、チームメンバーをAdobe Admin Consoleのas a Cloud Serviceの製品プロファイルに割り当てて、それらのリソースにアクセスする必要があります。

次にドキュメントを確認して、オンボーディングジャーニーを続行する必要があります [チームメンバーのAEMas a Cloud Service製品プロファイルへの割り当て](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md) ここでは、チームメンバーに新しい環境へのアクセスに必要な権限を付与する方法について説明します。

## その他のリソース {#additional-resources}

その他のリソースでは、以下について学習します。

* [プログラムタイプとプログラムの追加](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html)
* [環境タイプと環境の追加](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html)
* [Cloud Manager Git の管理](/help/implementing/cloud-manager/managing-code/accessing-repos.md)
* [Admin Console からの AEM as a Cloud Service へのアクセスの設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#adobe-ims-users)
