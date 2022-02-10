---
title: オンボーディングプロセスの概要
description: このページでは、オンボーディングジャーニーの概要について説明します
feature: Onboarding
role: Admin, User, Developer
exl-id: a02ff46f-1319-4c0c-8ecc-d8d2d4276229
source-git-commit: a8649f639eb173cdc1869a27c8f2d4b6b8026fb1
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 100%

---

# オンボーディングプロセスの概要 {#getting-started}

オンボーディングとは、指定された[システム管理者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/system-administrator.html?lang=ja)が組織の AEM as a Cloud Service を設定するプロセスです。これには、クラウドリソースの初期プロビジョニングや、ユーザーを職務に基づいて役割に割り当てる作業が含まれます。その結果、各メンバーがログインして AEM as a Cloud Service リソースにアクセスできるようになります。

## 目的 {#objective}

このドキュメントでは、システム管理者にオンボーディングジャーニーの最初の手順について説明します。

この節を読むと、次のことができるようになります。

* Admin Console にアクセスしてログインする。
* Admin Console でシステム管理者としての権限を確認する。

>[!NOTE]
>オンボーディングプロセスを開始する前に、必ず Adobe Admin Console について学んでください。Adobe Admin Console は、Adobe の製品ライセンスとユーザーを一元管理するための場所です。システム管理者が Adobe Admin Console にログインして、ユーザーの追加や削除などを行えます。詳しくは、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=ja)を参照してください。

## AEM as a Cloud Service のオンボーディング {#onboarding-process}

契約段階から Cloud Manager を使用した環境のセットアップまで、AEM as a Cloud Service へのオンボーディングについて説明します。

>[!VIDEO](https://video.tv.adobe.com/v/336959/?quality=12&learn=on)

## Admin Console へのログイン {#steps-admin-console}

次の手順に従って、Admin Console に移動し、Admin Console でシステム管理者の役割を確認します。

>[!NOTE]
>次の手順を正しく完了するには、システム管理者である必要があります。

1. 次の図に示すように、「ようこそ」メールから「**開始**」をクリックして、Admin Console に移動するか、[こちら](https://adminconsole.adobe.com)から直接 Admin Console に移動します。

   >[!NOTE]
   >システム管理者は、複数のメールを受信します。アクセス権を付与された組織名に関する情報を提供するお知らせメールを探し、「**開始**」をクリックします。メールが見つからない場合は、[Admin Console](https://adminconsole.adobe.com/) に直接移動します。

   ![](/help/journey-onboarding/assets/get-started-email.png)

1. [Adobe ID を使用してログインします。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/adobe-id.html?lang=ja)ログインに成功すると、次に示すように、Adobe Admin Console の&#x200B;**概要**&#x200B;ページが表示されます。

   ![](/help/journey-onboarding/assets/get-started1.png)

   >[!NOTE]
   >複数の組織にアクセスできる場合は、正しい組織にログインしていることを確認してください。組織を変更するには、右上隅の組織名をクリックし、アクセスする必要がある組織を選択します（下図を参照）。

   ![](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. **ユーザー**&#x200B;カードから「**管理者**」を選択し、Adobe Admin Console 経由のシステム管理者であることを確認します。

   ![](/help/journey-onboarding/assets/get-started2.png)

1. **ユーザー**&#x200B;カードで「**管理者**」をクリックすると、Adobe ID のメールアドレス、ユーザー名、名、姓を入力して検索できます。

   ![](/help/journey-onboarding/assets/get-started3.png)

1. 検索で電子メールレコードが正常に見つかる必要があります。さらに、「**管理者の役割**」列が「**システム**」と表示される必要があります（下図を参照）。これにより、ユーザーがシステム管理者であることを確認できます。これにより、ユーザーの役割がシステム管理者であることを確認できます。

   ![](/help/journey-onboarding/assets/get-started4.png)

   システム管理者として Admin Console に正常にログインし、次の手順に進む準備が整いました。

## 次の手順 {#whats-next}

これで、Admin Console にログインし、システム管理者としてプロファイルを確認したので、次に [Cloud Manager 製品プロファイルへのチームメンバーの割り当て](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md)のドキュメントを参照しながら、オンボーディングジャーニーを続けてください。

## その他のリソース {#additional-resources}

* [Admin Console](/help/onboarding/learn-concepts/admin-console.md)
* [システム管理者](/help/onboarding/learn-concepts/system-administrator.md)
