---
title: Cloud Manager 製品プロファイルへのチームメンバーの割り当て
description: このページでは、チームメンバーを Cloud Manager 製品プロファイルに割り当てる方法について説明します
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 42%

---


# Cloud Manager 製品プロファイルへのチームメンバーの割り当て {#assign-team-members}

この部分では、 [オンボーディングジャーニー](overview.md) チームメンバーを Cloud Manager 製品プロファイルに割り当てる方法について説明します。

## 目的 {#objective}

このジャーニーの前の手順では、 [Admin Consoleへのアクセス](admin-console.md) ここで、Admin Consoleにログインし、システム管理者としての権限を確認する方法を学習しました。 これで、チームメンバーに Cloud Manager へのアクセスを許可する準備が整いました。 これをおこなうには、製品プロファイルを割り当てます。

ユーザーにAdobeソリューションへのアクセス権を付与する場合、必ずしもユーザーにフルアクセス権を付与する必要はありません。 製品プロファイルを使用すると、各ソリューションに独自のユーザー権限セットを設定できます。 製品プロファイルの割り当てには、Admin Consoleを使用します。

最初の手順は、ユーザーに Cloud Manager へのアクセス権を付与することです。 Cloud Manager は、エンタープライズ開発の設定と専用に構築された CI/CD パイプラインをサポートします。これは、高度なテストと最高のコード品質を確実に実現し、優れたエクスペリエンスを提供するために備わっています。

読み終えると、次のことが習得できます。

* 製品プロファイルの概要
* Cloud Manager とは何かを理解します。
* 次の 3 つの重要な Cloud Manager 製品プロファイルを把握します。 **ビジネスオーナー**, **デプロイメントマネージャー**、および **開発者**.
* Cloud Manager 製品プロファイルにチームメンバーを割り当てることができる。

## 前提条件 {#prerequisites}

チームメンバーを製品プロファイルに割り当てるには、チームメンバーに関する詳細が必要です。チームメンバーは、次の情報を含め、AEMas a Cloud Serviceにアクセスする必要があります。

* 氏名
* 電子メールアドレス
* 役割と責務

>[!TIP]
>
>オンボーディングの目的で、Adobeは、管理者、開発者、コンテンツ作成者など、即時タスクに参加するユーザーを最初に追加することをお勧めします。
>
>すべてのユーザーを追加しなくても、オンボーディングプロセスを続行できます。オンボーディングが完了したら、さらにユーザーを追加できます。

## 製品プロファイル {#product-profiles}

ユーザーにAdobeソリューションへのアクセス権を付与する場合、必ずしもユーザーにフルアクセス権を付与する必要はありません。 製品プロファイルを使用すると、各ソリューションは、製品を使用して設定された、独自のユーザー権限を持つことができます。Admin Console

例えば、このジャーニーの後半で、Admin Consoleを使用して、AEM管理者とAEM作成者用の製品プロファイルを割り当て、AEMソリューションへのアクセス権をユーザーに付与します。

ただし、次の手順では、チームメンバーが最初に Cloud Manager にアクセスできるように製品プロファイルを付与します。

## Cloud Manager {#cloud-manager}

システム管理者は、AEMas a Cloud Serviceプロジェクトを成功させるには、AEMを使用した驚くべきコンテンツの作成だけでなく、AEMコンテンツを提供するための独自のカスタムコードやアプリケーションの開発とデプロイメントにも依存することを知っています。

Cloud Manager はAEMas a Cloud Serviceの不可欠な要素で、コードデプロイメント用の CI/CD パイプラインの管理、コードリポジトリの管理、環境の管理に使用されます。

チームが他の操作をおこなう前に、必要な製品プロファイルを付与して Cloud Manager に転送する必要があります。 次の手順では、Admin Consoleを使用して Cloud Manager 製品プロファイルを見つける場所と、それらをチームメンバーに割り当てる方法を示します。

## Cloud Manager 製品プロファイルの確認 {#review-product-profiles}

このAdmin Consoleを使用して、Cloud Manager のプロファイルのリストを表示できます。

1. Adobe Admin Console（[adminconsole.adobe.com](https://adminconsole.adobe.com/)）にログインして、**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」を選択します。

   ![AEM as a Cloud Service 製品](/help/journey-onboarding/assets/assign-team1.png)

1. すべてのインスタンスのリストから **Cloud Manager** インスタンスを選択して、そこに移動します。

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. 事前設定済みの Cloud Manager 製品プロファイルのリストが表示されます。

   ![製品プロファイル](/help/journey-onboarding/assets/assign-team3.png)

初期オンボーディングプロセスの一環として割り当てる最も重要なプロファイルは次のとおりです。

* **ビジネスオーナー**  — これらのユーザーは様々なプログラムを管理します。
* **デプロイメントマネージャー**  — これらのユーザーは、リポジトリーから実行中のAEM環境にコードをデプロイします。
* **開発者**  — これらのユーザーは、カスタムAEMアプリケーションを開発し、コードをリポジトリにコミットします。

これらの役割とその役割を理解し、チームメンバーのリストを確認して、誰がどのプロファイルを必要とするかを判断します。 ユーザーはチーム内で複数の役割を持つことができ、多くの場合は複数のプロファイルも必要になることに注意してください。

## ビジネスオーナー製品プロファイルの割り当て {#assign-business-owner}

これで、ユーザーを追加して、**ビジネスオーナー**&#x200B;製品プロファイルに割り当てる準備が整いました。

1. Cloud Manager プログラムを管理する必要があるユーザーを特定します。 これらは、 **事業主**.

1. Admin Console（`[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)`）にログインして、**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」製品を選択します。

   ![製品とサービス](/help/journey-onboarding/assets/assign-team1.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![ユーザーを追加](/help/journey-onboarding/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログで、追加するユーザーの電子メール ID を入力します。

   * チームメンバーの Federated ID がまだセットアップされていない場合は、「**ID タイプ**」として「**Adobe ID**」を選択します。

   ![ユーザー詳細の追加](/help/journey-onboarding/assets/assign-team5.png)

1. 「**製品またはユーザーグループを選択**」見出しの下の「＋」ボタンをクリックして製品の選択を開始し、「**Adobe Experience Manager as a Cloud Service**」を選択して&#x200B;**ビジネスオーナー**&#x200B;製品プロファイルをユーザーに割り当てます。

   * ユーザーが Cloud Manager にアクセスできるように、すべてのユーザーを 1 つ以上の製品プロファイルに割り当てます。
   * システム管理者として自分を **ビジネスオーナー** 役割。

   ![ユーザーの割り当て](/help/journey-onboarding/assets/assign-team6.png)

1. 「**保存**」をクリックすると、追加したユーザー宛に「ようこそ」の電子メールが送信されます。招待されたユーザーは、「ようこそ」の電子メールに記載されているリンクをクリックし、Adobe ID を使用してログインすることで、Cloud Manager にアクセスできます。

1. チームに属するユーザーに対して、上記の手順を繰り返します。

お使いの **ビジネスオーナー**&#x200B;が割り当てられ、Cloud Manager にアクセスできるようになりました。 システム管理者としての自分を **ビジネスオーナー** プロファイル。

## デプロイメントマネージャー製品プロファイルの割り当て {#assign-deployment-manager}

1. コードのデプロイが必要なユーザーを特定します。

1. Admin Console（`[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)`）にログインして、**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」製品を選択します。

   ![製品とサービス](/help/journey-onboarding/assets/assign-team1.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![ユーザーを追加](/help/journey-onboarding/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログで、追加するユーザーの電子メール ID を入力します。

   * チームメンバーの Federated ID がまだセットアップされていない場合は、「**ID タイプ**」として「**Adobe ID**」を選択します。

   ![ID の入力](/help/journey-onboarding/assets/assign-team5.png)

1. 「**製品またはユーザーグループを選択**」見出しの下の「＋」ボタンをクリックして製品の選択を開始し、「**Adobe Experience Manager as a Cloud Service**」を選択して&#x200B;**デプロイメントマネージャー**&#x200B;製品プロファイルをユーザーに割り当てます。

   ![プロファイルの割り当て](/help/journey-onboarding/assets/assign-team6.png)

お使いの **デプロイメントマネージャー**&#x200B;が割り当てられ、Cloud Manager にアクセスできるようになりました。 今後の責任に応じて、システム管理者としての自分自身を **デプロイメントマネージャー** プロファイル。

## 開発者製品プロファイルの割り当て {#assign-developer}

1. AEMアプリケーションの開発とコードの管理を必要とするユーザーを特定します。

1. Admin Console（`[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)`）にログインして、**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」製品を選択します。

   ![製品とサービス](/help/journey-onboarding/assets/assign-team1.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![ユーザーを追加](/help/journey-onboarding/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログで、追加するユーザーの電子メール ID を入力します。

   * チームメンバーの Federated ID がまだセットアップされていない場合は、「**ID タイプ**」として「**Adobe ID**」を選択します。

   ![ユーザー ID の追加](/help/journey-onboarding/assets/assign-team5.png)

1. 「**製品またはユーザーグループを選択**」見出しの下の「＋」ボタンをクリックして製品の選択を開始し、「**Adobe Experience Manager as a Cloud Service**」を選択して&#x200B;**開発者**&#x200B;製品プロファイルをユーザーに割り当てます。

   ![プロファイルの割り当て](/help/journey-onboarding/assets/assign-team6.png).

お使いの **開発者**&#x200B;が割り当てられ、Cloud Manager にアクセスできるようになりました。 今後の責任に応じて、システム管理者としての自分自身を **開発者** プロファイル。

## 次の手順 {#whats-next}

おめでとうございます。新しく作成された Cloud Manager チーム ( 自分が **ビジネスオーナー** プロファイル ) が設定されていることを確認します。 **ビジネスオーナー**&#x200B;の役割で Cloud Manager にログインしてクラウドリソースを作成できるようになるまであと少しです。

オンボーディングジャーニーのこの部分では、Admin Console内のプロファイルにチームメンバーを割り当てる方法について学びました。 その結果、以下を習得しました。

* 製品プロファイルの概要
* Cloud Manager とは何かを理解します。
* 次の 3 つの重要な Cloud Manager 製品プロファイルを把握します。 **ビジネスオーナー**, **デプロイメントマネージャー**、および **開発者**.
* Cloud Manager 製品プロファイルにチームメンバーを割り当てることができる。

これで、次にドキュメントを確認して、オンボーディングジャーニーを続行する準備が整いました [Cloud Manager にアクセスする](cloud-manager.md) ここでは、Cloud Manager にアクセスしてプロジェクトリソースを作成する方法について説明します。

## その他のリソース {#additional-resources}

前述したようにオンボーディングジャーニーを続行することをお勧めします。以下は、このジャーニーで説明している特定のトピックの詳細を調べる場合に参考になる追加のリソースです。

* [Cloud Manager の概要](/help/onboarding/cloud-manager-introduction.md) - Cloud Manager、Cloud Manager プログラム、環境について説明します。
* [Cloud Manager 製品プロファイル](/help/onboarding/aem-cs-team-product-profiles.md) - AEMのas a Cloud Serviceのチームおよび製品プロファイルについて説明します。
* [Adobe Admin Consoleの ID タイプ](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/identity.ug.html) -Adobeの id 管理システムは、管理者がアプリケーションやサービスへのユーザーのアクセスを作成および管理するのに役立ちます。 Adobeは、ユーザーの認証と承認をおこなうために、これらの ID タイプまたはアカウントを提供します。

