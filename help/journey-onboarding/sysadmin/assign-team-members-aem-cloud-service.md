---
title: AEM as a Cloud Service 製品プロファイルへのチームメンバーの割り当て
description: ここでは、チームメンバーを AEM as a Cloud Service 製品プロファイルに割り当てる方法について説明します
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: ht
source-wordcount: '833'
ht-degree: 100%

---

# AEM as a Cloud Service 製品プロファイルへのチームメンバーの割り当て {#assign-team-members-cloud-service}

## 目的 {#objective}

このドキュメントでは、システム管理者がチームメンバーを AEM as a Cloud Service 製品プロファイルに割り当てるために必要な手順と、AEM 作成者が AEM のジャーニーを開始できるようにすることが重要な理由を説明します。

この説を読み終えると、以下を理解できます。

* チームメンバーを AEM as a Cloud Service 製品プロファイルに割り当てる理由と方法
* チームメンバーを「AEM ユーザー」製品プロファイルに追加する方法
* チームメンバーを「AEM 管理者」製品プロファイルに追加する方法


## はじめに {#introduction}

ユーザーが AEM as a Cloud Service へのアクセス権を付与されるには、`AEM Users` または `AEM Administrators` のどちらかの製品プロファイルに属している必要があります。Cloud Manager を管理する権限では不十分なので、チームメンバーに AEM インスタンスに対する権限を付与する必要があります。

>[!NOTE]
>システム管理者によって「AEM ユーザー」製品プロファイルに割り当てられたユーザーは誰でも、Cloud Manager に（読み取り専用で）アクセスできます。

## 前提条件 {#prerequisites}

この節を読む前に、次の前提条件を確認してください。

* [AEM as a Cloud Service 製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#aem-product-profiles)について理解している
* [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=ja) について理解している
* Cloud Manager 製品プロファイルが必要に応じてチームメンバーに割り当てられており、クラウドリソースがセットアップされている
* チームメンバーの詳細：システム管理者は、AEM as a Cloud Service へのアクセスを必要とするチームメンバーの名前と電子メールアドレス、役割と責務がわかっている

   >[!NOTE]
   >オンボーディングのために、管理者、開発者、コンテンツ作成者など、当面のタスクに参加するユーザーを最初に追加することをお勧めします。すべてのユーザーを追加しなくても、残りのオンボーディングを続行できます。オンボーディングが完了したら、後でユーザーの数を増やすことができます。


   >[!IMPORTANT]
   >AEM as a Cloud Service 製品プロファイルにチームメンバーを割り当てる手順を確認する前に、必ず次の 2 つの手順に従ってください。
   >
   >1. [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=ja) にログインします。詳しくは、「Admin Console へのログイン」を参照してください。
   >
   >1. [AEM as a Cloud Service 製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#aem-product-profiles)を確認します。


Adobe Admin Console で Cloud Manager プロファイルのリストを表示するには、次の手順に従います。

1. [Adobe Admin Console](https://adminconsole.adobe.com/) にログインします。**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」を選択します。

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. インスタンス（開発環境のオーサーインスタンス）に移動して選択します（下図を参照）。

   ![](/help/journey-onboarding/assets/cloud-profiles-1.png)


1. 役割に基づいてユーザーに割り当てる必要がある AEM as a Cloud Service 製品プロファイルのリストが表示されます。

   >[!NOTE]
   >詳しくは、[AEM as a Cloud Service 製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#aem-product-profiles)を参照してください。

   ![](/help/journey-onboarding/assets/cloud-profiles-2.png)


## 「AEM ユーザー」または「AEM 管理者」製品プロファイルへのチームメンバーの追加 {#add-team-members}

AEM as a Cloud Service へのアクセス権が付与されるには、インスタンスは「`AEM Users`」または「`AEM Administrators`」のどちらかの製品プロファイルに属している必要があります。

>[!NOTE]
>インスタンスに対する権限を付与される必要があります。Cloud Manager を管理する権限では不十分です。詳細情報を参照してください。

以下の手順は、「ビジネスオーナー」の役割も兼務しているシステム管理者が実行する必要があります。

1. Cloud Manager のプログラムに移動し、対象となる環境のコンテキストから「**アクセスを管理**」ボタンを選択します（下図を参照）。

   ![](/help/journey-onboarding/assets/add-team1.png)

1. 新しいタブで Adobe Admin Console が表示されます。ここから、環境のオーサーインスタンスにアクセスできます。ユーザーに付与すべき権限に基づいて、「**AEM 管理者**」または「**AEM ユーザー**」を選択します。詳しくは、[AEM as a Cloud Service 製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#aem-product-profiles)を参照してください。

   ![](/help/journey-onboarding/assets/add-team2.png)

1. 「`AEM Administrator`」または「`AEM User`」を選択し、「**ユーザーを追加**」（下図を参照）をクリックして、チームメンバーの追加に必要な詳細を送信します。

   ![](/help/journey-onboarding/assets/add-team3.png)

   追加したユーザーは、AEM as a Cloud Service のオーサーサービスにアクセスできるようになります。

   >[!NOTE]
   >アクセスを必要とするチームメンバーの情報があれば、開発、ステージ、実稼動などのすべての環境で、上記の手順を繰り返すことができます。


## 次の手順 {#whats-next}

これで、AEM as a Cloud Service の製品プロファイルに割り当てたユーザーは、オーサリングサービスにアクセスする方法を学び、AEM as a Cloud Service でのページのオーサリングに慣れることができます。次は、[AEM ユーザーの学習パス](/help/journey-onboarding/sysadmin/learning-path-aem-users.md)または[開発者およびデプロイメントマネージャーの学習パス](/help/journey-onboarding/sysadmin/learning-path-developers-deploymentmanagers.md)のドキュメントを確認して、そのパスに従ってください。

## その他のリソース {#additional-resources}

* [Admin Console での製品とユーザーアクセスの管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=ja#managing-products-and-user-access-in-admin-console)
* [AEM へのアクセスの設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=ja)
* [ページのオーサリングのクイックスタートガイド](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=ja)
