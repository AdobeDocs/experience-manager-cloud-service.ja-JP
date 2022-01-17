---
title: Cloud Manager 製品プロファイルへのチームメンバーの割り当て
description: ここでは、チームメンバーを Cloud Manager 製品プロファイルに割り当てる方法について説明します
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: ht
source-wordcount: '1440'
ht-degree: 100%

---

# Cloud Manager 製品プロファイルへのチームメンバーの割り当て {#assign-team-members}

[Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=ja) へのログイン方法を理解し、[システム管理者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/system-administrator.html?lang=ja)としての権限を確認したら、チームメンバーを Cloud Manager 製品プロファイルに割り当てる準備が整います。

## 目的 {#objective}

このドキュメントでは、Adobe Admin Console でチームメンバーを Cloud Manager 製品プロファイルに割り当てる方法について説明します。

この節の学習目標は次のとおりです。

* チームメンバーを追加する理由と方法を理解する。
* ビジネスオーナー、デプロイメントマネージャー、開発者という 3 種類の Cloud Manager 製品プロファイルについて理解する。
* ビジネスオーナー、デプロイメントマネージャー、開発者などの Cloud Manager 製品プロファイルにチームメンバーを割り当てる。

## 前提条件 {#prerequisites}

この節を開始する前に、次の前提条件を考慮してください。読者の要件は次のとおりです。

* システム管理者であり、[Cloud Manager 製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#cloud-manager-product-profiles)について理解している。
* [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=ja) の基本を理解している。
* チームメンバーの詳細を把握している。システム管理者は、AEM as a Cloud Service へのアクセスを必要とするチームメンバーの名前と電子メールアドレス、役割と責務がわかっている必要があります。

   >[!NOTE]
   >オンボーディングのために、管理者、開発者、コンテンツ作成者など、当面のタスクに参加するユーザーを最初に追加することをお勧めします。すべてのユーザーを追加しなくても、残りのオンボーディングを続行できます。オンボーディングが完了したら、後でユーザーの数を増やすことができます。

## Cloud Manager 製品プロファイルの確認 {#review-product-profiles}

Adobe Admin Console で、Cloud Manager プロファイルのリストを確認できます。

>[!NOTE]
>Admin Console で Cloud Manager 製品プロファイルを確認する前に、使用可能な [Cloud Manager 製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#cloud-manager-product-profiles)を確認しておくことをお勧めします。

Cloud Manager プロファイルのリストを表示するには、次の手順に従います。

1. [Adobe Admin Console](https://adminconsole.adobe.com/) にログインします。**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」を選択します。

   ![](/help/journey-onboarding/assets/assign-team1.png)

   >[!NOTE]
   >Admin Console の使用方法については、Admin Console へのログインを参照してください。


1. すべてのインスタンスのリストから **Cloud Manager** インスタンスを選択して、そこに移動します。

   ![](/help/journey-onboarding/assets/assign-team2.png)

1. 事前設定済みの [Cloud Manager 製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#cloud-manager-product-profiles)のリストが表示されます。

   ![](/help/journey-onboarding/assets/assign-team3.png)


## 「ビジネスオーナー」製品プロファイルへのユーザーの割り当て {#assign-users-business-owner}

これで、ユーザーを追加して、Cloud Manager の「ビジネスオーナー」製品プロファイルに割り当てる準備が整いました。

>[!NOTE]
>割り当てを正常に行うには、AdobeAdmin Console で、製品（この場合は AEM as a Cloud Service）と [Cloud Manager の「ビジネスオーナー」製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#cloud-manager-product-profiles)の両方にユーザーを追加する必要があります。

それには次の手順に従います。

1. Cloud Manager プログラムを管理するユーザーを特定して、「ビジネスオーナー」製品プロファイルに追加します。まずシステム管理者が Cloud Manager にアクセスしてログインする必要があります。最初に、自分自身（システム管理者）を「ビジネスオーナー」製品プロファイルに追加する必要があります。

1. [Admin Console](https://adminconsole.adobe.com/enterprise/overview) の&#x200B;**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」製品を選択します（下図を参照）。

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![](/help/journey-onboarding/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログボックスで、追加するユーザーの電子メール ID を入力します。「ID タイプ」で「Adobe ID」を選択します（チームメンバーの Federated ID がまだセットアップされていない場合）。

   ![](/help/journey-onboarding/assets/assign-team5.png)

1. 製品選択で、「**Adobe Experience Manager as a Cloud Service**」を選択し、「**ビジネスオーナー**」製品プロファイルをユーザーに割り当てます（下図を参照）。

   >[!NOTE]
   >下図で示すように Admin Console で適切なユーザーに適切な役割を確実に割り当てるには、[Cloud Manager 製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#cloud-manager-product-profiles)を参照してください。

   ![](/help/journey-onboarding/assets/assign-team6.png)

   >[!NOTE]
   >ユーザーが Cloud Manager にアクセスできるように、ユーザーを 1 つ以上の製品プロファイルに割り当てます。自分自身（システム管理者）を必ず「ビジネスオーナー」に割り当ててください。

1. 「**保存**」をクリックします。追加したユーザー宛に「ようこそ」の電子メールが送信されます。招待されたユーザーは、「ようこそ」の電子メールに記載されているリンクをクリックし、Adobe ID を使用してログインすることで、Cloud Manager にアクセスできます。

   おめでとうございます。これで、新しく作成された Cloud Manager チーム（「ビジネスオーナー」の役割に割り当てられた自分自身を含む）のセットアップが完了しました。メンバーには、Cloud Manager にログインしてアクセスするための招待メールが届きます。「ビジネスオーナー」の役割を果たすために、Cloud Manager にログインしてクラウドリソースを作成できるようになるまであと一歩です。

## 「デプロイメントマネージャー」製品プロファイルへのユーザーの割り当て {#assign-users-deployment-manager}

1. Cloud Manager プログラムを管理するユーザーを特定して、「デプロイメントマネージャー」製品プロファイルに追加します。まずシステム管理者が Cloud Manager にアクセスしてログインする必要があります。最初に、自分自身（システム管理者）を「ビジネスオーナー」製品プロファイルに追加する必要があります（前の節で説明したとおり）。

1. [Admin Console](https://adminconsole.adobe.com/enterprise/overview) の&#x200B;**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」製品を選択します（下図を参照）。

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![](/help/journey-onboarding/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログボックスで、追加するユーザーの電子メール ID を入力します。「ID タイプ」で「Adobe ID」を選択します（チームメンバーの Federated ID がまだセットアップされていない場合）。

   ![](/help/journey-onboarding/assets/assign-team5.png)

1. 製品選択で、「**Adobe Experience Manager as a Cloud Service**」を選択し、「**デプロイメントマネージャー**」製品プロファイルをユーザーに割り当てます（下図を参照）。

   >[!NOTE]
   >下図のように Admin Console で適切なユーザーに適切な役割を確実に割り当てるには、[Cloud Manager 製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#cloud-manager-product-profiles)を参照してください。

   ![](/help/journey-onboarding/assets/assign-team6.png)

   >[!IMPORTANT]
   >Cloud Manager リソースの作成後、「デプロイメントマネージャー」製品プロファイルにユーザーを追加できます。

## 「開発者」製品プロファイルへのユーザーの割り当て {#assign-users-developer}

1. Cloud Manager プログラムを管理するユーザーを特定して、「開発者」製品プロファイルに追加します。まずシステム管理者が Cloud Manager にアクセスしてログインする必要があります。最初に、自分自身（システム管理者）を「ビジネスオーナー」製品プロファイルに追加する必要があります。

1. [Admin Console](https://adminconsole.adobe.com/enterprise/overview) の&#x200B;**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」製品を選択します（下図を参照）。

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![](/help/journey-onboarding/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログボックスで、追加するユーザーの電子メール ID を入力します。「ID タイプ」で「Adobe ID」を選択します（チームメンバーの Federated ID がまだセットアップされていない場合）。

   >[!NOTE]
   >Adobe Admin Console での ID タイプについて詳しくは、[ID の概要](https://helpx.adobe.com/jp/enterprise/using/identity.html)を参照してください。

   ![](/help/journey-onboarding/assets/assign-team5.png)

1. 製品選択で、「**Adobe Experience Manager as a Cloud Service**」を選択し、「**開発者**」製品プロファイルをユーザーに割り当てます（下図を参照）。

   >[!NOTE]
   >下図のように Admin Console で適切なユーザーに適切な役割を確実に割り当てるには、[Cloud Manager 製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#cloud-manager-product-profiles)を参照してください。

   ![](/help/journey-onboarding/assets/assign-team6.png)


   >[!IMPORTANT]
   >Cloud Manager リソースの作成後、「開発者」製品プロファイルにユーザーを追加できます。

## 次の手順 {#whats-next}

ビジネスオーナー、デプロイメントマネージャー、開発者という 3 種類の Cloud Manager 製品プロファイルについて理解しました。次に、ビジネスオーナー、デプロイメントマネージャー、開発者などの Cloud Manager 製品プロファイルにチームメンバーを割り当てました。これで、次に [Cloud Manager を使用したクラウドリソースのセットアップ](/help/journey-onboarding/sysadmin/setup-cloud-resources-via-cloud-manager.md)のドキュメントを次に参照しながらオンボーディングジャーニーを続行する準備が整いました。このドキュメントで学ぶ内容は次のとおりです。

1. *ビジネスオーナー*&#x200B;の役割に割り当てられたシステム管理者として、Cloud Manager にアクセスしてログインする必要があります。

1. 次に、*ビジネスオーナー*&#x200B;の役割を持つ Cloud Manager ユーザーが、クラウドプログラムやクラウド環境などのクラウドリソースにログインしセットアップします。これにより、エキスパートチームが、AEM as a Cloud Service に早めにアクセスできるようになります。

1. *ビジネスオーナー*&#x200B;がクラウドリソースをセットアップしたら、Cloud Manager 製品プロファイルに正常に追加された&#x200B;*開発者*&#x200B;と&#x200B;*デプロイメントマネージャー*&#x200B;は、Cloud Manager にアクセスし、学習パスの継続方法を把握することができます。

## その他のリソース {#additional-resources}

その他に、次のリソースも参照してください。

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=ja)
* [Cloud Manager 製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#cloud-manager-product-profiles)
* [Admin Console の ID の概要](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
