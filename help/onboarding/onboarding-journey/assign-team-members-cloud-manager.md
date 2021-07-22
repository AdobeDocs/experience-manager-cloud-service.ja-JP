---
title: 'Cloud Manager製品プロファイルへのチームメンバーの割り当て '
description: このページでは、チームメンバーをCloud Manager製品プロファイルに割り当てる方法について説明します
hide: true
hidefromtoc: true
index: false
source-git-commit: 21fae2eff51e46ee026cebe135c8a16625ed8f10
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 2%

---


# Cloud Manager製品プロファイルへのチームメンバーの割り当て {#assign-team-members}

[Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)へのログイン方法を学習し、[システム管理者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/system-administrator.html?lang=en)として権限を確認したら、Cloud Manager製品プロファイルにチームメンバーを割り当てる準備が整いました。

## 目的 {#objective}

このドキュメントでは、チームメンバーをCloud Manager製品プロファイルに割り当てる方法について概要をAdmin Consoleします。

この節を読むと、次のことが可能になります。

* チームメンバーを追加する必要がある理由と方法を理解します。
* ビジネスオーナー、デプロイメントマネージャー、開発者など、3種類のCloud Manager製品プロファイルについて説明します。
* チームメンバーをCloud Manager製品プロファイル（ビジネスオーナー、デプロイメントマネージャー、開発者など）に割り当てます。

## 前提条件 {#prerequisites}

この節を開始する前に、次の前提条件を考慮する必要があります。 次の条件を満たす必要があります。

* システム管理者で、[Cloud Manager製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)について理解している必要があります。
* [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)の基本を理解します。
* チームメンバーの詳細を入力する必要があります。 システム管理者は、AEM as aCloud Serviceへのアクセスを必要とするチームメンバーの名前と電子メールアドレス、役割と責任を持っている必要があります。

   >[!NOTE]
   >オンボーディングを目的として、最初に管理者、開発者、コンテンツ作成者など、即時タスクに参加するユーザーを追加することをお勧めします。 すべてのユーザーを追加することなく、残りのオンボーディングを続行できます。 オンボーディングが完了したら、後でより多くのユーザーに拡大できます。

## Cloud Manager製品プロファイルの確認 {#review-product-profiles}

Admin Consoleから、Cloud Managerのプロファイルのリストを確認できます。

>[!NOTE]
>Admin ConsoleのCloud Manager製品プロファイルを確認する前に、利用可能な[Cloud Manager製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)を確認することをお勧めします。

次の手順に従って、Cloud Managerプロファイルのリストを表示します。

1. [Adobe Admin Console](https://adminconsole.adobe.com/)にログインします。 **概要**&#x200B;ページで、**Cloud Serviceとサービス**&#x200B;カードから&#x200B;**Adobe Experience Managerを製品**&#x200B;として選択します。

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

   >[!NOTE]
   >Admin Consoleの使用方法については、Admin Consoleへのログインを参照してください。


1. すべてのインスタンスのリストを含むテーブルから&#x200B;**Cloud Manager**&#x200B;インスタンスに移動します。

   ![](/help/onboarding/onboarding-journey/assets/assign-team2.png)

1. 事前設定済みの[Cloud Manager製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)のリストが表示されます。

   ![](/help/onboarding/onboarding-journey/assets/assign-team3.png)


## ビジネスオーナー製品プロファイルへのユーザーの割り当て {#assign-users-business-owner}

これで、ユーザーを追加して、Cloud Managerビジネスオーナー製品プロファイルに割り当てる準備が整いました。

>[!NOTE]
>これを正しくおこなうには、AdobeAdmin Consoleから、ユーザーを製品(この場合はCloud ServiceとしてAEM)と[Cloud Managerビジネスオーナー製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)の両方に追加する必要があります。

以下の手順で、手順を説明します。

1. Cloud Managerプログラムを管理するユーザーを特定し、ビジネスオーナー製品プロファイルに追加します。 Cloud Managerにアクセスしてログインするのは、システム管理者が最初におこなう必要があります。 最初に、自分自身（システム管理者）をビジネスオーナー製品プロファイルに追加する必要があります。

1. [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **概要**&#x200B;ページで、以下に示すように、**Cloud Serviceとして** Adobe Experience Managerを選択します。**製品とサービス**&#x200B;カード

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. 上部のナビゲーションから「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログボックスに、追加するユーザーの電子メールIDを入力します。 「IDタイプ」で、チームメンバーのFederated IDがまだ設定されていない場合は「 Adobe ID 」を選択します。

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. 製品選択で、**Adobe Experience ManagerをCloud Service**&#x200B;として選択し、以下に示すように、**ビジネスオーナー**&#x200B;の製品プロファイルをユーザーに割り当てます。

   >[!NOTE]
   >[Cloud Manager製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)を参照して、以下に示すように、適切なAdmin Consoleに適切な役割が割り当てられていることを確認します。

   ![](/help/onboarding/onboarding-journey/assets/assign-team6.png)

   >[!NOTE]
   >ユーザーがCloud Managerにアクセスできるように、少なくとも1つの製品プロファイルにユーザーを割り当てます。 自分（システム管理者）を必ずビジネスオーナーに割り当ててください。

1. 「**保存**」をクリックします。追加したユーザー宛に「ようこそ」の電子メールが送信されます。招待されたユーザーは、「ようこそ」の電子メールに記載されているリンクをクリックし、Adobe IDを使用してログインすることで、Cloud Managerにアクセスできます。

おめでとうございます。これで、「ビジネスオーナー」の役割に割り当てられた自分自身を含む、新しく作成されたCloud Managerチームが設定されました。 メンバーには、Cloud Managerにログインしてアクセスするよう勧めるお知らせメールが届きます。 ビジネスオーナーの役割では、Cloud Managerにログインしてクラウドリソースを作成できるようになるのは、1ステップの距離にすぎません。

## Deployment Manager製品プロファイルへのユーザーの割り当て {#assign-users-deployment-manager}

1. Cloud Managerプログラムを管理するユーザーを特定し、Deployment Manager製品プロファイルに追加します。 Cloud Managerにアクセスしてログインするのは、システム管理者が最初におこなう必要があります。 最初に、自分自身（システム管理者）をビジネスオーナー製品プロファイルに追加する必要があります。

1. [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **概要**&#x200B;ページで、以下に示すように、**Cloud Serviceとして** Adobe Experience Managerを選択します。**製品とサービス**&#x200B;カード

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. 上部のナビゲーションから「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログボックスに、追加するユーザーの電子メールIDを入力します。 「IDタイプ」で、チームメンバーのFederated IDがまだ設定されていない場合は「 Adobe ID 」を選択します。

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. 製品選択で、Cloud Serviceとして&#x200B;**Adobe Experience Manager**&#x200B;を選択し、以下に示すように、**Deployment Manager**&#x200B;製品プロファイルをユーザーに割り当てます。

   >[!NOTE]
   >[Cloud Manager製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)を参照して、以下に示すように、適切なAdmin Consoleに適切な役割が割り当てられていることを確認します。

   ![](/help/onboarding/onboarding-journey/assets/assign-team6.png)

   >[!IMPORTANT]
   >ユーザーは、Cloud Managerリソースの作成後にDeployment Manager製品プロファイルに追加できます。

## 開発者製品プロファイルへのユーザーの割り当て {#assign-users-developer}

1. Cloud Managerプログラムを管理するユーザーを特定し、開発者製品プロファイルに追加します。 Cloud Managerにアクセスしてログインするのは、システム管理者が最初におこなう必要があります。 最初に、自分自身（システム管理者）をビジネスオーナー製品プロファイルに追加する必要があります。

1. [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **概要**&#x200B;ページで、以下に示すように、**Cloud Serviceとして** Adobe Experience Managerを選択します。**製品とサービス**&#x200B;カード

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. 上部のナビゲーションから「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログボックスに、追加するユーザーの電子メールIDを入力します。 「IDタイプ」で、チームメンバーのFederated IDがまだ設定されていない場合は「 Adobe ID 」を選択します。

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. 製品選択で、**Adobe Experience ManagerをCloud Service**&#x200B;として選択し、以下に示すように、**Developer**&#x200B;製品プロファイルをユーザーに割り当てます。

   >[!NOTE]
   >[Cloud Manager製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)を参照して、以下に示すように、適切なAdmin Consoleに適切な役割が割り当てられていることを確認します。

   ![](/help/onboarding/onboarding-journey/assets/assign-team6.png).


   >[!IMPORTANT]
   >ユーザーは、Cloud Managerリソースの作成後に開発者製品プロファイルに追加できます。

## 次の作業 {#whats-next}

*ビジネスオーナー*&#x200B;の役割に割り当てられたシステム管理者は、Cloud Managerにアクセスしてログインする必要があります。
>[!NOTE]
>Cloud Managerにログインしてアクセスする方法については、 [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=en)への移動を参照してください。

ビジネスオーナーロールのCloud Managerユーザーは、プログラムと環境を含むクラウドリソースにログインし、設定できます。 これにより、エキスパートチームができるだけ早くAEMにCloud Serviceとしてアクセスできるようになります。
ビジネスオーナーがクラウドリソースを設定したら、Cloud Manager製品プロファイルに正常に追加された開発者とデプロイメントマネージャーは、Cloud Managerにアクセスし、学習パスを続行する方法を把握できます。

## その他のリソース {#additional-resources}

その他のリソースでは、以下について学習します。

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Cloud Manager製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Admin ConsoleIDの概要](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
