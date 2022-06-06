---
title: Cloud Manager を使用したクラウドリソースの設定
description: Cloud Manager を使用して独自のクラウドリソースを設定および管理する方法について説明します。
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 0db24518610fccf0d2ea5e0620a0c6a5f8009ea8
workflow-type: ht
source-wordcount: '1369'
ht-degree: 100%

---

# Cloud Manager を使用したクラウドリソースの設定 {#setup-cloud-resources}

Cloud Manager を使用して独自のクラウドリソースを設定および管理する方法について説明します。

## 目的 {#objective}

このドキュメントでは、クラウドリソースの作成方法と誰が作成できるのかについて説明します。この説を読み終えると、以下を理解できます。

* 組織で Cloud Manager に最初にログインしてアクセスするのは、**ビジネスオーナー**&#x200B;の役割を割り振られているシステム管理者である必要があります。
* クラウドプログラムと環境の作成方法。

## はじめに {#introduction}

クラウドリソースの追加は、**ビジネスオーナー**&#x200B;製品プロファイルに割り当てられたチームメンバーが Cloud Manager を使用して行います。通常、このユーザーは、ビジネスニーズを理解し、Cloud Manager の初期設定を完了するユーザーです。

以下の節では、[クラウドサービスプログラム](#create-cloud-service-program)と[環境](#create-cloud-environments)の作成方法について説明します。

### 前提条件 {#prerequisites}

* **ビジネスオーナー**&#x200B;の役割に割り当てられたシステム管理者は、**ビジネスオーナー**&#x200B;の役割を持つ他のユーザーが Cloud Manager にアクセスしてこのドキュメントに記載されている手順を実行しようとする前に、Cloud Manager にログインしている必要があります。

   * このジャーニーについて詳しくは、[Cloud Manager 製品プロファイルへのチームメンバーの割り当て](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md)のドキュメントを参照してください。

* [Cloud Manager に移動してログインする](/help/onboarding/learn-concepts/cloud-manager-introduction.md)方法を理解している必要があります。

* [Cloud Manager の製品プロファイル](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)をよく理解しておく必要があります。

* Cloud Manager の[プログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)と[環境](/help/implementing/cloud-manager/manage-environments.md)の概念を理解しておく必要があります。

## システム管理者およびビジネスオーナーとして Cloud Manager にアクセス {#access-sysadmin-bo}

**ビジネスオーナー**&#x200B;の役割を割り当てたチームメンバーが Cloud Manager にアクセスし、クラウドリソースの作成を開始する前に、システム管理者は、**ビジネスオーナー**&#x200B;の役割を割り当てられ、Cloud Manager にログインする必要があります。

1. システム管理者が、**ビジネスオーナー**&#x200B;の役割を持っていることを確認してください。

   * まだシステム管理者に&#x200B;**ビジネスオーナー**&#x200B;を割り当てていない場合は、この前の手順の [Cloud Manager 製品プロファイルへのチームメンバーの割り当て](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md)に戻り、詳細を参照してください。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) から Cloud Manager にログインすると、通常のランディングページが表示されます。

**ビジネスオーナー**&#x200B;の役割を持つシステム管理者がログインに成功すると、**ビジネスオーナー**&#x200B;の役割を持つ他のユーザーが使用できるように Cloud Manager が初期化されます。これについての確認やメッセージは表示されません。ログインするだけで十分です。

**ビジネスオーナー**&#x200B;の役割を持つシステム管理者が Cloud Manager にログインするまで、**ビジネスオーナー**&#x200B;の役割を持つ他のユーザーは、正しい役割が割り当てられていても、Cloud Manager でプログラムを作成できません。

## Cloud Manager に移動 {#navigate-cloud-manager}

**ビジネスオーナー**&#x200B;の役割を持つユーザーには、開始するためのリンクが記載された、お知らせメールが届きます。このメールを使用して Cloud Manager に移動するには、以下の手順に従います。

1. お知らせメールで、「**使用を開始**」をクリックします（下図を参照）。
   ![メールの例](/help/journey-onboarding/assets/get-started-email.png)

1. Cloud Manager の&#x200B;**プログラムと製品**&#x200B;ページに移動します。

   >[!TIP]
   >
   >[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) から Cloud Manager のログインページに直接移動することもできます。今後の参照用に、このページをブックマークに追加してください。

1. Cloud Manager のランディングページに移動します。詳しくは、[Cloud Manager のプログラムの表示](#viewing-programs)の節を参照してください。

次の手順に従って、Adobe Experience Cloud のホームページから Cloud Manager の&#x200B;**プログラムと製品**&#x200B;ページに移動することもできます。

1. [Adobe Experience Cloud](https://experience.adobe.com) に直接移動し、Adobe ID を使用してログインします。

1. Adobe Experience Cloud のホームページで、「**Experience Manager**」を選択します。

   ![Experience Cloud ホームページ](/help/journey-onboarding/assets/setup-resources2.png)

1. AEM ホームページが表示されます。ここから **Cloud Manager** タイルの「**ローンチ**」をクリックします。

   ![AEM ホームページ](/help/journey-onboarding/assets/setup-resources3.png)

1. 正常にログインすると、Cloud Manager のランディングページが表示されます。詳しくは、[Cloud Manager のプログラムの表示](#viewing-programs)の節を参照してください。

Cloud Manager を使用してプログラムや製品にアクセスする方法はユーザー次第であり、Cloud Manager の使用方法やプログラムの管理方法には影響しません。

>[!NOTE]
>
>[!UICONTROL Cloud Manager] で割り当てられた役割とアプリケーションの状態によっては、[!UICONTROL Cloud Manager] UI の使用中に異なる画面が表示されます。

### プログラムの表示 {#viewing-programs}

Cloud Manager に正常にアクセスすると、表示される内容は、以降の節で説明するように、プログラムの状態によって異なります。

#### プログラムが存在しない場合 {#no-programs}

組織にプログラムが存在しない場合は、最初のプログラムを作成するようにランディングページで指示されます。

![プログラムがありません](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### プログラムが既に存在する場合 {#programs-exist}

組織にプログラムが既に存在する場合は、ランディングページに既存のプログラムが表示され、プログラムを追加するボタンも表示されます。

![プログラムが存在します](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### プログラムが存在し、システム管理者である場合 {#programs-exist-sysadmin}

組織にプログラムが既に存在し、ユーザーがシステム管理者である場合は、ランディングページに「**アクセスを管理**」ボタンと「**プログラムを追加**」オプションが表示されます。

![システム管理者の表示](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## ユーザーの役割の確認 {#verify-user-roles}

Cloud Manager に正常にログインしたら、**ビジネスオーナー**&#x200B;製品プロファイルが割り当てられていることを確認します。

1. ウィンドウの右上からプロファイルを選択します。

   ![ユーザープロファイル](/help/journey-onboarding/assets/setup-resources5.png)

1. 「**ユーザーの役割**」を選択し、ユーザーに割り当てられている役割を表示します。

   ![ユーザーの役割](/help/journey-onboarding/assets/setup-resources6.png)

1. ユーザーが&#x200B;**ビジネスオーナー**&#x200B;の役割を持っていることを確認します。

   ![ユーザーの役割のリスト](/help/journey-onboarding/assets/setup-resources7.png)

Cloud Manager にビジネスオーナーとして正常にログインしました。**ビジネスオーナー**&#x200B;の役割を割り当てられていない場合は、システム管理者にお問い合わせください。

## Cloud Service プログラムの作成 {#create-cloud-service-program}

適切なアクセス権を持っていることが確認できたので、最初のプログラムを作成できます。

1. Cloud Manager のランディングページ [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) に移動してログインします。

1. Cloud Manager のランディングページで、「**プログラムを追加**」をクリックして、プログラムの追加ウィザードを起動します。

   ![ランディングページ](/help/journey-onboarding/assets/setup-resources4.png)

   >[!TIP]
   >
   >プログラムの追加ウィザードの使用方法については、[製品プログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)ドキュメントを参照するか、この[ビデオ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=ja)で AEM as a Cloud プログラムの作成方法とプログラムを作成する前の重要な検討事項を確認してください。


1. クラウドプログラムが正常に作成されたら、 Cloud Manager のランディングページからプログラムに移動して、**概要**&#x200B;ページを開きます。

   ![プログラムの概要](/help/journey-onboarding/assets/setup-resources8.png)

1. 開発者製品プロファイルに割り当てられたメンバーは、Cloud Manager にログインし、Cloud Manager Git リポジトリを管理できます。

   * まだメンバーを割り当てていない場合は、このタイミングで Cloud Manager チームに&#x200B;**開発者**&#x200B;の役割を割り当てるのがよいでしょう。このジャーニーについて詳しくは、[Cloud Manager 製品プロファイルへのチームメンバーの割り当て](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md)のドキュメントを参照してください。

これで、プログラムが正常に作成され、開発者が Cloud Manager Git リポジトリにアクセスできるようになりました。

## クラウド環境の作成 {#create-cloud-environments}

クラウドプログラムを正常に作成したら、クラウド環境を作成します。

1. Cloud Manager のランディングページ [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) に移動して、環境カードから「**追加**」を設定します。

   ![「環境を追加」ボタン](/help/journey-onboarding/assets/setup-resources9.png)

1. 環境を追加ウィザードが起動し、環境の追加手順が示されます。ウィザードに慣れるには、まず開発環境を追加してください。

   >[!TIP]
   >
   >詳細については、[環境の追加](/help/implementing/cloud-manager/manage-environments.md#adding-environments)ドキュメントを参照するか、[このクイックビデオチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=ja)を見て、Cloud Manager 環境とそれをプログラムに追加する方法について確認してください。

1. **開発者**&#x200B;製品プロファイルに割り当てられたメンバーは、Cloud Manager にログインし、Cloud Manager Git リポジトリを管理できます。

これで、プログラムが正常に作成され、開発者が Cloud Manager Git にアクセスできるようになりました。

## 次の手順 {#whats-next}

クラウドリソースが作成され、チームがアクセスする準備が整ったので、システム管理者は、チームメンバーを Adobe Admin Console で AEM as a Cloud Service 製品プロファイルに割り当てて、リソースにアクセスできるようにする必要があります。

次に、[AEM as a Cloud Service 製品プロファイルへのチームメンバーの割り当て](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md)ドキュメントを確認して、チームメンバーに新しい環境へのアクセスに必要な権限を付与する方法について学習し、オンボーディングジャーニーを続行します。

## その他のリソース {#additional-resources}

その他のリソースでは、以下について学習します。

* [プログラムタイプとプログラムの追加](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=ja)
* [環境タイプと環境の追加](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=ja)
* [Cloud Manager Git の管理](/help/implementing/cloud-manager/managing-code/accessing-repos.md)
* [Admin Console からの AEM as a Cloud Service へのアクセスの設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=ja#adobe-ims-users)
