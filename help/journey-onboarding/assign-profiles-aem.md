---
title: AEM 製品プロファイルの割り当て
description: クラウドリソースを設定したら、AEM 製品プロファイルを使用して、AEM 自体へのアクセス権をチームに付与します。
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '878'
ht-degree: 100%

---

# AEM 製品プロファイルの割り当て {#assign-profiles-aem}

>[!CONTEXTUALHELP]
>id="assets_user_entitlements"
>title="AEM 製品プロファイルの割り当て"
>abstract="Experience Manager Assets を使用する資格が付与されていません。システム管理者にお問い合わせください。"

[オンボーディングジャーニー](overview.md)のこのパートでは、AEM 製品プロファイルを使用して AEM へのアクセス権をチームに付与する方法を説明します。

## 目的 {#objective}

オンボーディングジャーニーの前のドキュメント[環境の作成](create-environments.md)を読んでクラウドリソースを設定したら、AEM 製品プロファイルを使用して、AEM 自体へのアクセス権をチームに付与します。これを行うには、システム管理者が AEM 製品プロファイルを割り当てます。

このドキュメントを読むと、次の点を理解できるようになります。

* AEM 製品プロファイルとは何か。
* チームメンバーを「AEM ユーザー」製品プロファイルに追加する方法
* チームメンバーを「AEM 管理者」製品プロファイルに追加する方法

## AEM 製品プロファイル {#aem-product-profiles}

AEM を使用するには、チームメンバーが 1 つまたは複数の AEM 製品プロファイルに割り当てられている必要があります。 Cloud Manager にアクセスする権限では不十分です。 ユーザーは、次の 2 つの製品プロファイルのいずれかに属している必要があります。

* `AEM Users` - このグループには、コンテンツのオーサリング作業を日々行う通常のユーザーが含まれます。
* `AEM Administrators` - このグループには、高度な機能や AEM を担当するユーザーが含まれます。

>[!NOTE]
>
>AEM as a Cloud Service の製品プロファイルに割り当てられたすべてのユーザーは、**Cloud Manager ユーザー**&#x200B;の役割を介して Cloud Manager に読み取り専用でアクセスできます。
>
>**Cloud Manager** ユーザーの役割のみを持つユーザーは、Cloud Manager にログインし、プログラムメニューオプションを使用して AEM オーサー環境（存在する場合）に移動できます。**Cloud Manager ユーザー**の役割では、プログラムの詳細にアクセスするのに十分ではありません。 そのようなアクセスが必要な場合は、システム管理者から追加の役割を付与してもらう必要があります。
>Cloud Manager ユーザーの役割について詳しくは、[下記のその他のリソース](#additional-resources)のセクションを参照してください。

>[!CAUTION]
>
>AEM 管理者または AEM ユーザーという名前の製品プロファイルは、編集または削除しないでください。これらのプロファイル名を編集すると、AEM クラウドインスタンスへのログインが中断する場合があります。

## 前提条件 {#prerequisites}

このセクションを読む前に、AEM を使用するチームに関する次の情報を入手する必要があります。

* 氏名
* メールアドレス
* 役割と責務

>[!TIP]
>
>オンボーディングを目的に、管理者、開発者、コンテンツ作成者など、当面のタスクに携わるユーザーを最初に追加することをお勧めします。すべてのユーザーを追加しなくても、残りのオンボーディングを続行できます。オンボーディングが完了したら、後でユーザーの数を増やすことができます。

## AEM 製品プロファイルの表示 {#view-profiles}

次の手順に従って、Admin Console で AEM 製品プロファイルを表示します。

1. [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) で Admin Console にログインします。

1. **概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」を選択します。

   ![製品とサービスカード](/help/journey-onboarding/assets/assign-team1.png)

1. インスタンスに移動して選択します。

   ![インスタンスの選択](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. 役割に基づいてユーザーに割り当てる必要がある AEM as a Cloud Service 製品プロファイルのリストが表示されます。

   ![製品プロファイル](/help/journey-onboarding/assets/cloud-profiles-2.png)

## 製品プロファイルへのチームメンバーの追加 {#add-team-members}

使用可能なプロファイルについて理解できたので、必要に応じてチームメンバーに割り当てることができます。

これらのタスクを実行するには、**ビジネスオーナー** Cloud Manager 製品プロファイルを持つシステム管理者である必要があります。

1. Cloud Manager のプログラムに移動し、対象となる環境のコンテキストから「**アクセスを管理**」ボタンを選択します。

   ![アクセスの管理](/help/journey-onboarding/assets/add-team1.png)

1. 新しいタブで Admin Console が表示されます。ここから、環境のオーサーインスタンスにアクセスできます。そのユーザーに付与すべき権限に応じて、「**AEM 管理者**」または「**AEM ユーザー**」を選択します。

   ![アクセス権限の割り当て](/help/journey-onboarding/assets/add-team2.png)

1. 「`AEM Administrator`」または「`AEM User`」を選択し、「**ユーザーを追加**」（以下を参照）をクリックして、チームメンバーの追加に必要な詳細を送信します。

   ![チームメンバーの追加](/help/journey-onboarding/assets/add-team3.png)

1. アクセスを必要とするチームメンバーの情報があれば、開発、ステージ、実稼動などのすべての環境で、これらの手順を繰り返します。

これで、追加したユーザーは、AEM as a Cloud Service のオーサーサービスにアクセスできるようになりました。

## ジャーニーの終了 {#the-end}

これで完了です。これで、AEM as a Cloud Service の製品プロファイルに割り当てたユーザーが、AEM オーサリング環境にアクセスし、AEM as a Cloud Service でコンテンツの作成を開始する準備が整いました。同様に、開発者は Cloud Manager にアクセスし、Git を使用してカスタムアプリケーションコードを保存し、デプロイできるようになりました。つまり、オンボーディングジャーニーは完了し、ユーザーは AEMaaCS を使用できるようになりました。

ただし、作成者と開発者がシステムをどのように使用しているかをより深く理解したい場合は、このオンボーディングジャーニーの次の 2 つのオプションのパートに進んでください。

* [開発者およびデプロイメントマネージャーのタスク](developers.md) - 開発者が Git にアクセスしてカスタムコードを保存し、Cloud Manager パイプラインを使用してデプロイする方法をを説明します。
* [AEM ユーザーのタスク](aem-users.md) - コンテンツの作成を開始できる AEM 環境にアクセスする方法をを説明します。

## その他のリソース {#additional-resources}

オンボーディングジャーニーのコンテンツの範囲を超えてさらに詳しく知りたい場合に役立つ、追加のオプションリソースを次に示します。

* [AEM as a Cloud Service のチームおよび製品プロファイル](/help/onboarding/aem-cs-team-product-profiles.md) - ライセンス取得済みのアドビソリューションに対するアクセスを AEM as a Cloud Service のチームおよび製品プロファイルで許可および制限する方法について説明します。
* [Admin Console での製品とユーザーアクセスの管理](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) - Admin Console を使用してユーザーアクセスを管理する方法について説明します。
* [AEM へのアクセスの設定のウォークスルー](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=ja) - Admin Console で Adobe IMS ユーザー、ユーザーグループ、製品プロファイルを設定する方法については、こちらの簡潔なウォークスルーを参照してください。

