---
title: Cloud Manager 製品プロファイルへのチームメンバーの割り当て
description: ここでは、チームメンバーを Cloud Manager 製品プロファイルに割り当てる方法について説明します
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: ht
source-wordcount: '1154'
ht-degree: 100%

---

# Cloud Manager 製品プロファイルへのチームメンバーの割り当て {#assign-team-members}

このジャーニーの前のステップの[オンボーディングプロセスの概要](/help/journey-onboarding/sysadmin/get-started-onboarding-journey.md)では、Admin Console へのログイン方法とシステム管理者としての権限について説明しました。Cloud Manager 製品プロファイルにチームメンバーを割り当てる準備が整っています。

## 目的 {#objective}

このドキュメントでは、Adobe Admin Console でチームメンバーを Cloud Manager 製品プロファイルに割り当てる方法について説明します。割り当てが完了すると、チームメンバーは、クラウドリソースへのアクセスを設定できるようになります（このジャーニーの次のステップを参照）。

この節を読むと、次のことができるようになります。

* チームメンバーを追加する理由と方法を理解する。
* **ビジネスオーナー**、**デプロイメントマネージャー**、**開発者**&#x200B;という 3 種類の重要な Cloud Manager 製品プロファイルについて理解する。
* Cloud Manager 製品プロファイルにチームメンバーを割り当てる。

>[!TIP]
>
>オンボーディングのために、管理者、開発者、コンテンツ作成者など、当面のタスクに参加するユーザーを最初に追加することをお勧めします。すべてのユーザーを追加しなくても、オンボーディングプロセスを続行できます。オンボーディングが完了したら、さらにユーザーを追加できます。

## 前提条件 {#prerequisites}

この節を開始する前に、次の前提条件を満たしてください。読者の要件は次のとおりです。

* システム管理者であり、Cloud Manager 製品プロファイルについて理解している。
   * これらの概念に詳しくない場合は、[オンボーディングジャーニーの概要](onboarding-journey-overview.md)に戻ります。
* Adobe Admin Console の基本を理解している。
   * これらの概念に詳しくない場合は、[オンボーディングジャーニーの概要](onboarding-journey-overview.md)に戻ります。
* チームメンバー（AEM as a Cloud Service へのアクセスが必要になる）について下記のような詳細を把握している。
   * 氏名
   * 電子メールアドレス
   * 役割と責務

## Cloud Manager 製品プロファイルの確認 {#review-product-profiles}

Adobe Admin Console で、Cloud Manager プロファイルのリストを確認できます。

1. Adobe Admin Console（[adminconsole.adobe.com](https://adminconsole.adobe.com/)）にログインして、**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」を選択します。

   ![AEM as a Cloud Service 製品](/help/journey-onboarding/assets/assign-team1.png)

1. すべてのインスタンスのリストから **Cloud Manager** インスタンスを選択して、そこに移動します。

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. 事前設定済みの Cloud Manager 製品プロファイルのリストが表示されます。

   ![製品プロファイル](/help/journey-onboarding/assets/assign-team3.png)

## 「ビジネスオーナー」製品プロファイルへのユーザーの割り当て {#assign-users-business-owner}

これで、ユーザーを追加して、**ビジネスオーナー**&#x200B;製品プロファイルに割り当てる準備が整いました。

1. Cloud Manager プログラムを管理するユーザーを特定して、「ビジネスオーナー」製品プロファイルに追加します。

1. Admin Console（[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)）にログインして、**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」製品を選択します。

   ![製品とサービス](/help/journey-onboarding/assets/assign-team1.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![ユーザーを追加](/help/journey-onboarding/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログで、追加するユーザーの電子メール ID を入力します。

   * チームメンバーの Federated ID がまだセットアップされていない場合は、「**ID タイプ**」として「**Adobe ID**」を選択します。

   ![ユーザー詳細の追加](/help/journey-onboarding/assets/assign-team5.png)

1. 「**製品またはユーザーグループを選択**」見出しの下の「＋」ボタンをクリックして製品の選択を開始し、「**Adobe Experience Manager as a Cloud Service**」を選択して&#x200B;**ビジネスオーナー**&#x200B;製品プロファイルをユーザーに割り当てます。

   * ユーザーが Cloud Manager にアクセスできるように、すべてのユーザーを 1 つ以上の製品プロファイルに割り当てます。
   * 自分自身（システム管理者）は必ず&#x200B;**ビジネスオーナー**&#x200B;の役割に割り当ててください。

   ![ユーザーの割り当て](/help/journey-onboarding/assets/assign-team6.png)

1. 「**保存**」をクリックすると、追加したユーザー宛に「ようこそ」の電子メールが送信されます。招待されたユーザーは、「ようこそ」の電子メールに記載されているリンクをクリックし、Adobe ID を使用してログインすることで、Cloud Manager にアクセスできます。

1. チームに属するユーザーに対して、上記の手順を繰り返します。

これで、新しく作成された Cloud Manager チーム（**ビジネスオーナー**&#x200B;の役割に割り当てられた自分自身を含む）のセットアップが完了しました。**ビジネスオーナー**&#x200B;の役割で Cloud Manager にログインしてクラウドリソースを作成できるようになるまであと少しです。

## 「デプロイメントマネージャー」製品プロファイルへのユーザーの割り当て {#assign-users-deployment-manager}

1. Cloud Manager プログラムを管理するユーザーを特定して、「デプロイメントマネージャー」製品プロファイルに追加します。

1. Admin Console（[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)）にログインして、**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」製品を選択します。

   ![製品とサービス](/help/journey-onboarding/assets/assign-team1.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![ユーザーを追加](/help/journey-onboarding/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログで、追加するユーザーの電子メール ID を入力します。

   * チームメンバーの Federated ID がまだセットアップされていない場合は、「**ID タイプ**」として「**Adobe ID**」を選択します。

   ![ID の入力](/help/journey-onboarding/assets/assign-team5.png)

1. 「**製品またはユーザーグループを選択**」見出しの下の「＋」ボタンをクリックして製品の選択を開始し、「**Adobe Experience Manager as a Cloud Service**」を選択して&#x200B;**デプロイメントマネージャー**&#x200B;製品プロファイルをユーザーに割り当てます。

   ![プロファイルの割り当て](/help/journey-onboarding/assets/assign-team6.png).

## 「開発者」製品プロファイルへのユーザーの割り当て {#assign-users-developer}

1. Cloud Manager プログラムを管理するユーザー（複数可）を特定します。

1. Admin Console（[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)）にログインして、**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」製品を選択します。

   ![製品とサービス](/help/journey-onboarding/assets/assign-team1.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![ユーザーを追加](/help/journey-onboarding/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログで、追加するユーザーの電子メール ID を入力します。

   * チームメンバーの Federated ID がまだセットアップされていない場合は、「**ID タイプ**」として「**Adobe ID**」を選択します。

   ![ユーザー ID の追加](/help/journey-onboarding/assets/assign-team5.png)

1. 「**製品またはユーザーグループを選択**」見出しの下の「＋」ボタンをクリックして製品の選択を開始し、「**Adobe Experience Manager as a Cloud Service**」を選択して&#x200B;**開発者**&#x200B;製品プロファイルをユーザーに割り当てます。

   ![プロファイルの割り当て](/help/journey-onboarding/assets/assign-team6.png).

## 次の手順 {#whats-next}

オンボーディングジャーニーのこのステップでは、Admin Console でチームメンバーを役割に割り当てる方法について説明しました。その結果、以下を達成できました。

* チームメンバーを追加する理由と方法を理解する。
* **ビジネスオーナー**、**デプロイメントマネージャー**、**開発者**&#x200B;という 3 種類の重要な Cloud Manager 製品プロファイルを理解する。
* Cloud Manager 製品プロファイルにチームメンバーを割り当てることができる。

これで、次に [Cloud Manager を使用したクラウドリソースのセットアップ](/help/journey-onboarding/sysadmin/setup-cloud-resources-via-cloud-manager.md)のドキュメントを参照しながらオンボーディングジャーニーを続行する準備が整いました。このドキュメントで学ぶ内容は次のとおりです。

1. 他のビジネスオーナーがプログラムを作成する場合は、まず、**ビジネスオーナー**&#x200B;の役割に割り当てられたシステム管理者が Cloud Manager にログインしてアクセスする必要があります。
1. **ビジネスオーナー**&#x200B;の役割を持つユーザーがクラウドプログラムやクラウド環境などのクラウドリソースにログインしセットアップする方法。
1. **開発者**&#x200B;や&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーが Cloud Manager にアクセスする方法。

## その他のリソース {#additional-resources}

前述したようにオンボーディングジャーニーを続行することをお勧めします。以下は、このジャーニーで説明している特定のトピックの詳細を調べる場合に参考になる追加のリソースです。

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=ja)
* [Cloud Manager 製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=ja#cloud-manager-product-profiles)
* [Admin Console の ID の概要](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
