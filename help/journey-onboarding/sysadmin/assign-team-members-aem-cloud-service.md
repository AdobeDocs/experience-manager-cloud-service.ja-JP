---
title: 'チームメンバーを製品プロファイルとしてAEMに割り当てるCloud Service '
description: このページでは、チームメンバーをAEM as a Cloud Service製品プロファイルに割り当てる方法について説明します
index: false
role: Admin, User, Developer
source-git-commit: a9eacc44c6be9101fae131c6fb6b95612efeac53
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 2%

---


# チームメンバーを製品プロファイルとしてAEMに割り当てるCloud Service {#assign-team-members-cloud-service}

## 目的 {#objective}

このドキュメントでは、チームメンバーをCloud Service製品プロファイルとしてAEMに割り当てるためにシステム管理者が実行する必要がある手順と、AEM作成者がAEMを使用してジャーニーを開始できるようにすることが重要な理由を説明します。

この節を読むと、次の内容を理解できます。

* チームメンバーが製品プロファイルとしてAEMに割り当てられる理由と方法。
* チームメンバーをAEM User製品プロファイルに追加する方法。
* チームメンバーをAEM Administrators製品プロファイルに追加する方法。


## はじめに {#introduction}

AEM as aCloud Serviceユーザーに対するアクセス権を付与するには、次の2つの製品プロファイルのいずれかに属している必要があります。 `AEM Users`または`AEM Administrators`。 Cloud Managerを管理する権限では不十分なので、チームメンバーにAEMインスタンスに対する権限を付与する必要があります。

>[!NOTE]
>システム管理者がAEMユーザー製品プロファイルに割り当てたすべてのユーザーは、Cloud Managerに（読み取り専用）アクセスできます。

## 前提条件 {#prerequisites}

この節を読む前に、次の前提条件を検討する必要があります。

* [AEM as aCloud Service製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)について
* [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)について
* Cloud Managerの製品プロファイルが必要に応じてチームメンバーに割り当てられ、クラウドリソースが設定されている
* チームメンバーの詳細：システム管理者は、AEM as aCloud Serviceへのアクセスが必要なチームメンバーの名前と電子メールアドレス、役割と責任を持っている必要があります。

   >[!NOTE]
   >オンボーディングを目的として、最初に管理者、開発者、コンテンツ作成者など、即時タスクに参加するユーザーを追加することをお勧めします。 すべてのユーザーを追加することなく、残りのオンボーディングを続行できます。 オンボーディングが完了したら、後でより多くのユーザーに拡大できます。


   >[!IMPORTANT]
   >AEM as aCloud Service製品プロファイルにチームメンバーを割り当てる手順を確認する前に、次の2つの手順に従ってください。
   >
   >1. [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)にログインします。 詳しくは、「Admin Consoleへのログイン」を参照してください。
   >
   >1. [AEM as aCloud Service製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)を確認します。


以下の手順に従って、Adobe Admin ConsoleのCloud Managerプロファイルのリストを表示します。

1. [Adobe Admin Console](https://adminconsole.adobe.com/)にログインします。 **概要**&#x200B;ページで、**Cloud Serviceとサービス**&#x200B;カードから&#x200B;**Adobe Experience Managerを製品**&#x200B;として選択します。

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. 次の図に示すように、インスタンス（開発環境のオーサーインスタンス）に移動して選択します。

   ![](/help/journey-onboarding/assets/cloud-profiles-1.png)


1. ユーザーの役割に基づいてCloud Serviceに割り当てる必要がある製品プロファイルとして、AEMのリストが表示されます。

   >[!NOTE]
   >これらについて詳しくは、[AEM as aCloud Service製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)を参照してください。

   ![](/help/journey-onboarding/assets/cloud-profiles-2.png)


## AEMユーザーまたはAEM管理者製品プロファイルへのチームメンバーの追加 {#add-team-members}

AEM as aCloud Serviceインスタンスへのアクセス権を付与するには、ユーザーが2つの製品プロファイル`AEM Users`または`AEM Administrators`のいずれかに属している必要があります。

>[!NOTE]
>インスタンスに対する権限を付与されている必要があります。Cloud Managerを管理する権限では不十分です。 詳細情報を参照してください。

以下の手順に従う必要があるのは、システム管理者で、ビジネスオーナーの役割も果たします。

1. Cloud Managerからプログラムに移動し、次に示すように、目的の環境のコンテキストから「**アクセスを管理**」ボタンを選択します。

   ![](/help/journey-onboarding/assets/add-team1.png)

1. 新しいタブで、環境のオーサーインスタンスにアクセスできるAdobe Admin Consoleに移動します。 **AEM Administrators**&#x200B;または&#x200B;**AEM Users**&#x200B;を、この個人が付与する必要がある権限に基づいて選択します。 [AEM as aCloud Service製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)の詳細をご覧ください。

   ![](/help/journey-onboarding/assets/add-team2.png)

1. `AEM Administrator`または`AEM User`を選択し、以下に示すように「**ユーザーを追加**」をクリックし、必要な詳細を送信してチームメンバーの追加を完了します。

   ![](/help/journey-onboarding/assets/add-team3.png)

   追加したユーザーは、AEM as a User Authorサービスにアクセスできます。

   >[!NOTE]
   >アクセス権を必要とするチームメンバーの情報を持っている場合は、開発、ステージング、実稼動を含むすべての環境に対して、これらの手順を繰り返します。


## 次の作業 {#whats-next}

これで、AEMにCloud Service製品プロファイルとして割り当てたCloud Serviceは、作成者にアクセスする方法と、AEM as a Usitorのページのオーサリングについて理解する方法を学ぶ準備が整いました。 次に、[AEM Users](/help/journey-onboarding/sysadmin/learning-path-aem-users.md)または[Developers and Deployment Manager](/help/journey-onboarding/sysadmin/learning-path-developers-deploymentmanagers.md)の学習パスを確認して、パスに従う必要があります。

## その他のリソース {#additional-resources}

* [Admin Console での製品とユーザーアクセスの管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#managing-products-and-user-access-in-admin-console)
* [AEMへのアクセスの設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)
* [ページのオーサリングのクイックスタートガイド](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=en)