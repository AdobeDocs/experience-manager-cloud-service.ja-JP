---
title: AEM製品プロファイルの割り当て
description: クラウドリソースを設定したら、AEM製品プロファイルを使用して、チームにAEM自体へのアクセス権を付与する必要があります。
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 22%

---

# AEM製品プロファイルの割り当て {#assign-profiles-aem}

この部分では、 [オンボーディングジャーニー](overview.md) AEM製品プロファイルを使用して、AEMへのチームアクセスを許可する方法を学習します。

## 目的 {#objective}

このオンボーディングジャーニーの前のドキュメントを読んだら、 [環境の作成](create-environments.md) お使いのクラウドリソースを設定するには、AEM製品プロファイルを使用して、チームにAEM自体へのアクセス権を付与する必要があります。 システム管理者は、AEM製品プロファイルを割り当てることでこれをおこないます。

このドキュメントを読んだ後、次の点を理解する必要があります。

* AEM製品プロファイルの概要。
* チームメンバーを「AEM ユーザー」製品プロファイルに追加する方法
* チームメンバーを「AEM 管理者」製品プロファイルに追加する方法

## AEM製品プロファイル {#aem-product-profiles}

AEMを使用するには、チームメンバーが少なくとも 1 つのAEM製品プロファイルに割り当てられている必要があります。 Cloud Manager にアクセスする権限では不十分です。 ユーザーは、次の 2 つの製品プロファイルのいずれかに属している必要があります。

* `AEM Users`  — このグループには、毎日のコンテンツオーサリングタスクを実行する通常のユーザーが含まれます。
* `AEM Administrators`  — このグループには、高度な機能またはAEMを担当するユーザーが含まれます。

AEM製品プロファイルに割り当てられたすべてのユーザーは、Cloud Manager に対する読み取り専用アクセス権も取得します。 Cloud Manager への書き込みアクセス権は、他の製品プロファイルを通じて付与できます。

## 前提条件 {#prerequisites}

この節を読む前に、AEMを使用するチームに関する次の情報を入手する必要があります。

* 氏名
* 電子メールアドレス
* 役割と責務

>[!TIP]
>
>オンボーディングのために、管理者、開発者、コンテンツ作成者など、当面のタスクに参加するユーザーを最初に追加することをお勧めします。すべてのユーザーを追加しなくても、残りのオンボーディングを続行できます。オンボーディングが完了したら、後でユーザーの数を増やすことができます。

## AEM製品プロファイルの表示 {#view-profiles}

次の手順に従って、Admin ConsoleからAEM製品プロファイルを表示します。

1. 次の場所でAdmin Consoleにログイン [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. **概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」を選択します。

   ![製品およびサービスカード](/help/journey-onboarding/assets/assign-team1.png)

1. インスタンスに移動して選択します。

   ![インスタンスを選択](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. ユーザーの役割に基づいてユーザーに割り当てることができるAEMas a Cloud Service製品プロファイルのリストが表示されます。

   ![製品プロファイル](/help/journey-onboarding/assets/cloud-profiles-2.png)

## 製品プロファイルへのチームメンバーの追加 {#add-team-members}

これで、使用可能なプロファイルについて理解できたので、必要に応じてチームメンバーに割り当てることができます。

これらのタスクを実行するには、 **ビジネスオーナー** Cloud Manager 製品プロファイル。

1. Cloud Manager からプログラムに移動し、 **アクセスを管理** ボタンをクリックします。

   ![アクセスを管理](/help/journey-onboarding/assets/add-team1.png)

1. 新しいタブで、Admin Consoleに移動します。このタブから、環境のオーサーインスタンスにアクセスできます。 選択 **AEM Administrators** または **AEM Users** 個人に与える必要がある権限に基づいて、個人が与える必要があります。

   ![アクセスの割り当て](/help/journey-onboarding/assets/add-team2.png)

1. 「`AEM Administrator`」または「`AEM User`」を選択し、「**ユーザーを追加**」（下図を参照）をクリックして、チームメンバーの追加に必要な詳細を送信します。

   ![チームメンバーを追加](/help/journey-onboarding/assets/add-team3.png)

1. アクセス権を必要とするチームメンバーの情報を持っている場合、開発、ステージング、実稼動を含むすべての環境に対して、これらの手順を繰り返します。

追加したユーザーは、AEM as a Cloud Service のオーサーサービスにアクセスできるようになります。

## ジャーニーの終了 {#the-end}

おめでとうございます。これで、AEMas a Cloud Serviceの製品プロファイルに割り当てたユーザーが、AEMオーサリング環境にアクセスし、AEMas a Cloud Serviceのを使用してコンテンツの作成を開始する準備が整いました。 同様に、開発者は Cloud Manager にアクセスして Git を使用してカスタムアプリケーションコードを保存し、デプロイできるようになりました。 この意味で、オンボーディングジャーニーは完了し、ユーザーは AEMaaCS を使用できるようになります。

ただし、作成者と開発者がシステムをどのように使用しているかをより深く理解したい場合は、このオンボーディングジャーニーの次の 2 つのオプション部分を使用し続けることができます。

* [開発者およびデプロイメントマネージャーのタスク](developers.md)  — 開発者が Git にアクセスしてカスタムコードを保存し、Cloud Manager パイプラインを使用してデプロイする方法を学ぶ場所です。
* [AEM User Tasks](aem-users.md)  — コンテンツの作成を開始できるAEM環境へのアクセス方法の参照先。

## その他のリソース {#additional-resources}

* [Admin Console での製品とユーザーアクセスの管理](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console)  — ユーザーアクセスを管理するAdmin Consoleの使用方法を説明します。
* [AEMウォークスルーへのアクセスの設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=ja) -Admin Console内でのAdobe IMSユーザー、ユーザーグループ、製品プロファイルの設定については、簡潔なウォークスルーをご覧ください。

