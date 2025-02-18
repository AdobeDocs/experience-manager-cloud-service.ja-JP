---
title: Cloud Manager 製品プロファイルへのチームメンバーの割り当て
description: このページでは、チームメンバーを Cloud Manager 製品プロファイルに割り当てる方法を説明します
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '1520'
ht-degree: 100%

---


# Cloud Manager 製品プロファイルへのチームメンバーの割り当て {#assign-team-members}

[オンボーディングジャーニー](overview.md)のこの部分では、チームメンバーを Cloud Manager 製品プロファイルに割り当てる方法を説明します。

## 目的 {#objective}

このジャーニーの前のステップ、[Admin Console へのアクセス](admin-console.md)では、Admin Console にログインして、システム管理者としての自身の権限を確認する方法を学びました。これで、チームメンバーが Cloud Manager にアクセスできるようにする準備が整いました。これを行うには、製品プロファイルを割り当てます。

アドビソリューションに対するアクセス権をユーザーに付与する場合、必ずしも完全なアクセス権を付与する必要はありません。製品プロファイルを使用すると、ソリューションごとに独自のユーザー権限を設定できます。製品プロファイルを割り当てるには、Admin Console を使用します。

最初のステップは、Cloud Manager へのアクセス権をユーザーに付与することです。Cloud Manager を使用すると、エンタープライズ開発体制を設定し、CI/CD パイプラインを専用に構築することができます。これらが備わっていることにより、徹底したテストと最高のコード品質を確実に実現し、優れたエクスペリエンスを提供することができます。

このドキュメントを読み終えると、次のことが可能になります。

* 製品プロファイルを理解する。
* Cloud Manager を理解する。
* **ビジネスオーナー**、**デプロイメントマネージャー**、**開発者**&#x200B;という 3 種類の重要な Cloud Manager 製品プロファイルを理解する。
* Cloud Manager 製品プロファイルにチームメンバーを割り当てることができる。

## 前提条件 {#prerequisites}

チームメンバーを製品プロファイルに割り当てるには、AEM as a Cloud Service にアクセスする必要があるチームメンバーについて、次のような詳細が必要です。

* 氏名
* メールアドレス
* 役割と責務

>[!TIP]
>
>オンボーディングのために、管理者、開発者、コンテンツ作成者など、当面のタスクに携わるユーザーを最初に追加することをお勧めします。
>
>すべてのユーザーを追加しなくても、オンボーディングプロセスを続行できます。オンボーディングが完了したら、さらにユーザーを追加できます。

## 製品プロファイル {#product-profiles}

アドビソリューションに対するアクセス権をユーザーに付与する場合、必ずしも完全なアクセス権を付与する必要はありません。製品プロファイルを使用すると、各ソリューションは一連の独自のユーザー権限を持つことができます。これらの権限は、Admin Console を使用して設定します。

例えば、このジャーニーの後半では、Admin Console を使用して AEM 管理者と AEM 作成者に製品プロファイルを割り当てて、AEM ソリューションへのアクセス権をユーザーに付与します。

ただし、次のステップでは、チームメンバーが最初に Cloud Manager にアクセスできるように製品プロファイルを付与します。

## Cloud Manager {#cloud-manager}

システム管理者は、AEM as a Cloud Service プロジェクトを成功させるには、AEM を使用してすばらしいコンテンツを作成することだけでなく、AEM コンテンツを提供するために独自のカスタムコードやアプリケーションを開発してデプロイすることにも依存することを知っています。

Cloud Manager は、AEM as a Cloud Service の不可欠な部分であり、コードをデプロイするための CI/CD パイプラインの管理、コードリポジトリの管理、環境の管理に使用されます。

チームのメンバーは、何らかの操作を行う前に、必要な製品プロファイルを付与して Cloud Manager にオンボーディングする必要があります。次のステップでは、Cloud Manager 製品プロファイルを Admin Console を使用して見つける場所と、製品プロファイルをチームメンバーに割り当てる方法を示します。

## Cloud Manager 製品プロファイルの確認 {#review-product-profiles}

 Admin Console で、Cloud Manager プロファイルのリストを確認できます。

1. Adobe Admin Console（[adminconsole.adobe.com](https://adminconsole.adobe.com/)）にログインして、**概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」を選択します。

   ![AEM as a Cloud Service 製品](/help/journey-onboarding/assets/assign-team1.png)

1. すべてのインスタンスのリストから **Cloud Manager** インスタンスを選択して、そこに移動します。

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. 事前設定済みの Cloud Manager 製品プロファイルのリストを表示できます。

   ![製品プロファイル](/help/journey-onboarding/assets/assign-team3.png)

オンボーディングの初期プロセスの一環として割り当てる必要のある、最も重要なプロファイルは次のとおりです。

* **ビジネスオーナー** - これらのユーザーは、それぞれ別個のプログラムを管理します。
* **デプロイメントマネージャー** - これらのユーザーは、リポジトリから実行中の AEM 環境にコードをデプロイします。
* **開発者** - これらのユーザーは、カスタム AEM アプリケーションを開発し、コードをリポジトリにコミットします。

これらの役割とその作業内容を理解したら、チームメンバーのリストを確認して、誰がどのプロファイルを必要としているかを判断します。ユーザーはチーム内で複数の役割を持つことができ、多くの場合は複数のプロファイルも必要になることに注意してください。

## ビジネスオーナー製品プロファイルの割り当て {#assign-business-owner}

これで、ユーザーを追加して、**ビジネスオーナー**&#x200B;製品プロファイルに割り当てる準備が整いました。

1. Cloud Manager プログラムを管理する必要があるユーザーを特定します。これらは&#x200B;**ビジネスオーナー**&#x200B;になります。

1. Admin Console（`[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)`）にログインして、**概要**&#x200B;ページで&#x200B;**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」製品を選択します。

   ![製品とサービス](/help/journey-onboarding/assets/assign-team1.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![ユーザーを追加](/help/journey-onboarding/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログで、追加するユーザーのメール ID を入力します。

   * チームメンバーの Federated ID がまだセットアップされていない場合は、「**ID タイプ**」として「**Adobe ID**」を選択します。

   ![ユーザー詳細の追加](/help/journey-onboarding/assets/assign-team5.png)

1. 「**製品またはユーザーグループを選択**」見出しの下の「＋」ボタンをクリックして製品の選択を開始し、「**Adobe Experience Manager as a Cloud Service**」を選択して&#x200B;**ビジネスオーナー**&#x200B;製品プロファイルをユーザーに割り当てます。

   * ユーザーが Cloud Manager にアクセスできるように、すべてのユーザーを 1 つ以上の製品プロファイルに割り当てます。
   * システム管理者は必ず自分自身を&#x200B;**ビジネスオーナー**&#x200B;の役割に割り当ててください。

   ![ユーザーの割り当て](/help/journey-onboarding/assets/assign-team6.png)

1. 「**保存**」をクリックすると、追加したユーザー宛にウェルカムメールが送信されます。招待されたユーザーは、ウェルカムメールに記載されているリンクをクリックし、Adobe ID を使用してログインすることで、Cloud Manager にアクセスできます。

1. チームに属するユーザーに対して、上記の手順を繰り返します。

**ビジネスオーナー**&#x200B;が割り当てられ、Cloud Manager にアクセスできるようになりました。 システム管理者は自分自身を&#x200B;**ビジネスオーナー**&#x200B;のプロファイルにも忘れずに割り当ててください。

## デプロイメントマネージャー製品プロファイルの割り当て {#assign-deployment-manager}

1. コードをデプロイする必要があるユーザーを特定します。

1. Admin Console（`[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)`）にログインして、**概要**&#x200B;ページで&#x200B;**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」製品を選択します。

   ![製品とサービス](/help/journey-onboarding/assets/assign-team1.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![ユーザーを追加](/help/journey-onboarding/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログで、追加するユーザーのメール ID を入力します。

   * チームメンバーの Federated ID がまだセットアップされていない場合は、「**ID タイプ**」として「**Adobe ID**」を選択します。

   ![ID の入力](/help/journey-onboarding/assets/assign-team5.png)

1. 「**製品またはユーザーグループを選択**」見出しの下の「＋」ボタンをクリックして製品の選択を開始し、「**Adobe Experience Manager as a Cloud Service**」を選択して&#x200B;**デプロイメントマネージャー**&#x200B;製品プロファイルをユーザーに割り当てます。

   ![プロファイルの割り当て](/help/journey-onboarding/assets/assign-team6.png)

**デプロイメントマネージャー**&#x200B;が割り当てられ、Cloud Manager にアクセスできるようになりました。 システム管理者は、今後の担務に応じて、自分自身を&#x200B;**デプロイメントマネージャー**&#x200B;のプロファイルに割り当てる必要がある場合とない場合があります。

## 開発者製品プロファイルの割り当て {#assign-developer}

1. AEM アプリケーションを開発してコードを管理する必要があるユーザーを特定します。

1. Admin Console（`[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)`）にログインして、**概要**&#x200B;ページで&#x200B;**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」製品を選択します。

   ![製品とサービス](/help/journey-onboarding/assets/assign-team1.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

   ![ユーザーを追加](/help/journey-onboarding/assets/assign-team4.png)

1. **チームにユーザーを追加**&#x200B;ダイアログで、追加するユーザーのメール ID を入力します。

   * チームメンバーの Federated ID がまだセットアップされていない場合は、「**ID タイプ**」として「**Adobe ID**」を選択します。

   ![ユーザー ID の追加](/help/journey-onboarding/assets/assign-team5.png)

1. 「**製品またはユーザーグループを選択**」見出しの下の「＋」ボタンをクリックして製品の選択を開始し、「**Adobe Experience Manager as a Cloud Service**」を選択して&#x200B;**開発者**&#x200B;製品プロファイルをユーザーに割り当てます。

   ![プロファイルの割り当て](/help/journey-onboarding/assets/assign-team6.png).

**開発者**&#x200B;が割り当てられ、Cloud Manager にアクセスできるようになりました。 システム管理者は、今後の担務に応じて、自分自身を&#x200B;**開発者**&#x200B;のプロファイルに割り当てる必要がある場合とない場合があります。

## 次のステップ {#whats-next}

おめでとうございます。これで、新しく構築された Cloud Manager チーム（**ビジネスオーナー**&#x200B;のプロファイルに割り当てられた自分自身を含む）の設定が完了しました。**ビジネスオーナー**&#x200B;の役割で Cloud Manager にログインしてクラウドリソースを作成できるようになるまであと少しです。

オンボーディングジャーニーのこのパートでは、Admin Console でチームメンバーをプロファイルに割り当てる方法について説明しました。その結果、以下を習得しました。

* 製品プロファイルを理解する。
* Cloud Manager を理解する。
* **ビジネスオーナー**、**デプロイメントマネージャー**、**開発者**&#x200B;という 3 種類の重要な Cloud Manager 製品プロファイルを理解する。
* Cloud Manager 製品プロファイルにチームメンバーを割り当てることができる。

これで、オンボーディングジャーニーを続ける準備が整いました。次は、[Cloud Manager へのアクセス](cloud-manager.md)のドキュメントを確認します。このドキュメントでは、Cloud Manager にアクセスしてプロジェクトリソースを作成する方法を説明します。

## その他のリソース {#additional-resources}

前述のように、オンボーディングジャーニーを続行することをお勧めします。このジャーニーの特定のトピックの詳細を調べる場合に参考になる追加のリソースです。

* [Cloud Manager の概要](/help/onboarding/cloud-manager-introduction.md) - Cloud Manager、Cloud Manager プログラム、環境について説明します。
* [Cloud Manager 製品プロファイル](/help/onboarding/aem-cs-team-product-profiles.md) - AEM as a Cloud Service のチームおよび製品プロファイルについて説明します。
* [Adobe Admin Console の ID タイプ](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/identity.ug.html) - アドビの ID 管理システムは、管理者がアプリケーションやサービスへのユーザーのアクセス権を作成および管理するのに役立ちます。アドビでは、ユーザーを認証および承認するために、これらの ID タイプまたはアカウントを提供しています。

