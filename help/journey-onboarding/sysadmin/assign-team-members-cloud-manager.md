---
title: Cloud Manager 製品プロファイルへのチームメンバーの割り当て
description: ここでは、チームメンバーを Cloud Manager 製品プロファイルに割り当てる方法について説明します
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 25%

---

# Cloud Manager 製品プロファイルへのチームメンバーの割り当て {#assign-team-members}

このジャーニーの前の手順では、 [オンボーディングプロセスの概要](/help/journey-onboarding/sysadmin/get-started-onboarding-journey.md)では、Admin Consoleにログインし、自分の権限をシステム管理者として表示する方法を学習しました。 これで、チームメンバーを Cloud Manager 製品プロファイルに割り当てる準備が整いました。

## 目的 {#objective}

このドキュメントでは、Adobe Admin Console でチームメンバーを Cloud Manager 製品プロファイルに割り当てる方法について説明します。割り当てられたメンバーは、このジャーニーの次の手順で説明するように、クラウドリソースにアクセスできます。

この節の学習目標は次のとおりです。

* チームメンバーを追加する理由と方法を理解する。
* 次の 3 つの重要な Cloud Manager 製品プロファイルについて説明します。 **ビジネスオーナー**, **デプロイメントマネージャー**、および **開発者**.
* Cloud Manager 製品プロファイルにチームメンバーを割り当てます。

>[!TIP]
>
>オンボーディングの目的で、Adobeは最初に、管理者、開発者、コンテンツ作成者など、即時タスクに参加するユーザーを追加することをお勧めします。 すべてのユーザーを追加せずに、オンボーディングプロセスを続行できます。 オンボーディングが完了したら、ユーザーを追加できます。

## 前提条件 {#prerequisites}

この節を開始する前に、次の前提条件を満たす必要があります。 読者の要件は次のとおりです。

* システム管理者であり、Cloud Manager 製品プロファイルについて理解している。
   * に戻る [オンボーディングジャーニーの概要](onboarding-journey-overview.md) これらの概念に詳しくない場合は、を参照してください。
* Adobe Admin Console の基本を理解している。
   * に戻る [オンボーディングジャーニーの概要](onboarding-journey-overview.md) これらの概念に詳しくない場合は、を参照してください。
* AEM as a Cloud Serviceにアクセスする必要のあるチームメンバーの詳細 (
   * 名前
   * 電子メールアドレス
   * 役割と責務

## Cloud Manager 製品プロファイルの確認 {#review-product-profiles}

Adobe Admin Consoleから、Cloud Manager のプロファイルのリストを表示できます。

1. Adobe Admin Console( ) にログインします。 [adminconsole.adobe.com](https://adminconsole.adobe.com/) そして **概要** ページ、選択 **Adobe Experience Manager as a Cloud Service** から **製品とサービス** カード。

   ![AEM as a product](/help/journey-onboarding/assets/assign-team1.png)

1. すべてのインスタンスのリストから **Cloud Manager** インスタンスを選択して、そこに移動します。

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. 事前設定済みの Cloud Manager 製品プロファイルのリストが表示されます。

   ![製品プロファイル](/help/journey-onboarding/assets/assign-team3.png)

## 「ビジネスオーナー」製品プロファイルへのユーザーの割り当て {#assign-users-business-owner}

これで、ユーザーを追加して **ビジネスオーナー** 製品プロファイル。

1. Cloud Manager プログラムを管理するユーザーを特定して、「ビジネスオーナー」製品プロファイルに追加します。

1. 次の場所にあるAdmin Consoleにログインします。 [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) そして **概要** ページ、選択 **Adobe Experience Manager as a Cloud Service** 製品 **製品とサービス** カード。

   ![製品とサービス](/help/journey-onboarding/assets/assign-team1.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![ユーザーを追加](/help/journey-onboarding/assets/assign-team4.png)

1. 内 **チームにユーザーを追加する** ダイアログで、追加するユーザーの電子メール ID を入力します。

   * チームメンバーの Federated ID が設定されていない場合は、 **Adobe ID** の **ID Type**.

   ![ユーザーの詳細を追加](/help/journey-onboarding/assets/assign-team5.png)

1. の下のプラスボタンをクリックします。 **製品またはユーザーグループを選択** 製品選択を開始し、「 」を選択する見出し **Adobe Experience Manager as a Cloud Service** および割り当て **ビジネスオーナー** ユーザーに対する製品プロファイル。

   * 各ユーザーを少なくとも 1 つの製品プロファイルに割り当てて、ユーザーが Cloud Manager にアクセスできるようにします。
   * 自分をシステム管理者として、必ず **ビジネスオーナー** 役割。

   ![ユーザーの割り当て](/help/journey-onboarding/assets/assign-team6.png)

1. クリック **保存** 追加したユーザー宛に「ようこそ」の電子メールが送信されます。 招待されたユーザーは、「ようこそ」の電子メールに記載されているリンクをクリックし、Adobe ID を使用してログインすることで、Cloud Manager にアクセスできます。

1. チームのユーザーに対して、これらの手順を繰り返します。

新しく作成された Cloud Manager チーム ( 自分が **ビジネスオーナー** ロール ) が設定されています。 の役割で **ビジネスオーナー**&#x200B;を使用すると、Cloud Manager にログインしてクラウドリソースを作成できるようになるので、1 ステップの距離ができます。

## 「デプロイメントマネージャー」製品プロファイルへのユーザーの割り当て {#assign-users-deployment-manager}

1. Cloud Manager プログラムを管理するユーザーを特定して、「デプロイメントマネージャー」製品プロファイルに追加します。

1. 次の場所にあるAdmin Consoleにログインします。 [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) そして **概要** ページ選択 **Adobe Experience Manager as a Cloud Service** 製品 **製品とサービス** カード。

   ![製品とサービス](/help/journey-onboarding/assets/assign-team1.png)

1. を選択します。 **ユーザー** 上部のナビゲーションから「 」タブを選択し、「 」を選択します。 **ユーザーを追加**.

   ![ユーザーを追加](/help/journey-onboarding/assets/assign-team4.png)

1. 内 **チームにユーザーを追加する** ダイアログで、追加するユーザーの電子メール ID を入力します。

   * チームメンバーの Federated ID が設定されていない場合は、 **Adobe ID** の **ID Type**.

   ![ID を入力](/help/journey-onboarding/assets/assign-team5.png)

1. の下のプラスボタンをクリックします。 **製品またはユーザーグループを選択** 製品選択を開始し、「 」を選択する見出し **Adobe Experience Manager as a Cloud Service** および割り当て **デプロイメントマネージャー** ユーザーに対する製品プロファイル。

   ![プロファイルを割り当て](/help/journey-onboarding/assets/assign-team6.png).

## 「開発者」製品プロファイルへのユーザーの割り当て {#assign-users-developer}

1. Cloud Manager プログラムを管理するユーザーを特定します。

1. 次の場所にあるAdmin Consoleにログインします。 [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) そして **概要** ページ選択 **Adobe Experience Manager as a Cloud Service** 製品 **製品とサービス** カード。

   ![製品とサービス](/help/journey-onboarding/assets/assign-team1.png)

1. を選択します。 **ユーザー** 上部のナビゲーションから「 」タブを選択し、「 」を選択します。 **ユーザーを追加**.

   ![ユーザーを追加](/help/journey-onboarding/assets/assign-team4.png)

1. In **チームにユーザーを追加する** ダイアログで、追加するユーザーの電子メール ID を入力します。

   * チームメンバーの Federated ID が設定されていない場合は、 **Adobe ID** の **ID Type**.

   ![ユーザー ID を追加](/help/journey-onboarding/assets/assign-team5.png)

1. の下のプラスボタンをクリックします。 **製品またはユーザーグループを選択** 製品選択を開始し、「 」を選択する見出し **Adobe Experience Manager as a Cloud Service** および割り当て **開発者** ユーザーに対する製品プロファイル。

   ![プロファイルを割り当て](/help/journey-onboarding/assets/assign-team6.png).

## 次の手順 {#whats-next}

オンボーディングジャーニーのこの部分では、チームメンバーをAdmin Console内の役割に割り当てる方法について学びました。 その結果、以下を達成できました。

* チームメンバーを追加する理由と方法を理解する。
* 次の 3 つの重要な Cloud Manager 製品プロファイルについて説明します。 **ビジネスオーナー**, **デプロイメントマネージャー**、および **開発者**.
* Cloud Manager 製品プロファイルにチームメンバーを割り当てることができます。

これで、次に [Cloud Manager を使用したクラウドリソースのセットアップ](/help/journey-onboarding/sysadmin/setup-cloud-resources-via-cloud-manager.md)のドキュメントを次に参照しながらオンボーディングジャーニーを続行する準備が整いました。このドキュメントで学ぶ内容は次のとおりです。

1. 他のビジネスオーナーがプログラムを作成するには、システム管理者が **ビジネスオーナー** の役割では、最初に Cloud Manager にアクセスしてログインする必要があります。
1. を使用して **ビジネスオーナー** の役割は、クラウドプログラムや環境を含むクラウドリソースにログインし、設定できます。
1. を使用して **開発者** および **デプロイメントマネージャー** の役割は Cloud Manager にアクセスできます。

## その他のリソース {#additional-resources}

前述のように、オンボーディングジャーニーを続行することをお勧めします。 このジャーニーの特定のトピックについて詳しく知りたい場合は、これらのリソースを追加します。

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=ja)
* [Cloud Manager 製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#cloud-manager-product-profiles)
* [Admin Console の ID の概要](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
