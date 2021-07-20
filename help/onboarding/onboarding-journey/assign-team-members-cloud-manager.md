---
title: 'Cloud Manager製品プロファイルへのチームメンバーの割り当て '
description: このページでは、チームメンバーをCloud Manager製品プロファイルに割り当てる方法について説明します
hide: true
hidefromtoc: true
index: false
source-git-commit: 8b30fc9494e152aa742cf17c02f982f5c9479473
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 1%

---


# Cloud Manager製品プロファイルへのチームメンバーの割り当て {#assign-team-members}

Admin Consoleへのログイン方法を学習し、システム管理者としての権限を確認したら、チームメンバーをCloud Manager製品プロファイルに割り当てる準備が整いました。

## 目的 {#objective}

このドキュメントでは、チームメンバーをCloud Manager製品プロファイルに割り当てる方法について概要をAdmin Consoleします。

この節を読むと、次のことが可能になります。

* チームメンバーを追加する必要がある理由と方法を理解します。
* ビジネスオーナー、デプロイメントマネージャー、開発者など、3種類のCloud Manager製品プロファイルについて説明します。
* チームメンバーをCloud Manager製品プロファイル（ビジネスオーナー、デプロイメントマネージャー、開発者）に割り当てます。

## Cloud Manager製品プロファイルの確認 {#review-product-profiles}

Admin Consoleから、Cloud Managerのプロファイルのリストを確認できます。

>[!NOTE]
>Admin ConsoleからCloud Manager製品プロファイルを確認する前に、利用可能なCloud Manager製品プロファイルを確認することをお勧めします。

次の手順に従って、Cloud Managerプロファイルのリストを表示します。

1. Adobe Admin Consoleにログインします。 **概要**&#x200B;ページで、「製品とサービス」カードからAdobe Experience Manager as a Cloud Serviceを選択します。

   >[!NOTE]
   >Admin Consoleの使用方法については、Admin Consoleへのログインを参照してください。


1. すべてのインスタンスのリストを含むテーブルからCloud Managerインスタンスに移動します。 事前設定済みのCloud Manager製品プロファイルのリストが表示されます。


## ユーザーをビジネスオーナー製品プロファイルに割り当てる {#assign-users-business-owner}

これで、ユーザーを追加して、Cloud Managerビジネスオーナー製品プロファイルに割り当てる準備が整いました。

これを正しくおこなうには、AdobeAdmin Consoleから、ユーザーを製品(この場合はCloud ServiceとしてAEM)とCloud Managerビジネスオーナー製品プロファイルの両方に追加する必要があります。

以下の手順で、手順を説明します。

1. Cloud Managerプログラムを管理するユーザーを特定し、ビジネスオーナー製品プロファイルに追加します。 Cloud Managerにアクセスしてログインするのは、システム管理者が最初におこなう必要があります。 最初に、自分自身（システム管理者）をビジネスオーナー製品プロファイルに追加する必要があります。

1. Admin Consoleの概要ページで、次に示すように、製品およびサービスカードからCloud Service製品としてAdobe Experience Managerを選択します。

1. 上部ナビゲーションから「ユーザー」タブを選択し、「ユーザーを追加」を選択します。

1. ユーザーを追加ダイアログボックスで、追加するユーザーの電子メールIDを入力します。 「IDタイプ」で、チームメンバーのFederated IDがまだ設定されていない場合は「 Adobe ID 」を選択します。

1. 「製品」選択で、「Adobe Experience Manager as aCloud Service」を選択し、以下に示すように、「ビジネスオーナー」製品プロファイルをユーザーに割り当てます。 以下に示すように、適切なユーザーにAdmin Consoleで適切な役割が割り当てられていることを確認するには、 Cloud Manager製品プロファイルを参照してください。

1. ユーザーがCloud Managerにアクセスできるように、少なくとも1つの製品プロファイルにユーザーを割り当てます。 自分（システム管理者）を「ビジネスオーナー」に割り当てることを忘れないでください。

1. 「保存」をクリックします。追加したユーザー宛に「ようこそ」の電子メールが送信されます。招待されたユーザーは、「ようこそ」の電子メールに記載されているリンクをクリックし、Adobe IDを使用してログインすることで、Cloud Managerにアクセスできます。

おめでとうございます。これで、「ビジネスオーナー」の役割に割り当てられた自分自身を含む、新しく作成されたCloud Managerチームが設定されました。 メンバーには、Cloud Managerにログインしてアクセスするよう勧めるお知らせメールが届きます。 ビジネスオーナーの役割では、Cloud Managerにログインしてクラウドリソースを作成できるようになるのは、1ステップの距離にすぎません。

## Deployment Manager製品プロファイルへのユーザーの割り当て {#assign-users-deployment-manager}

1. Cloud Managerプログラムを管理するユーザーを特定し、ビジネスオーナー製品プロファイルに追加します。 Cloud Managerにアクセスしてログインするのは、システム管理者が最初におこなう必要があります。 最初に、自分自身（システム管理者）をビジネスオーナー製品プロファイルに追加する必要があります。

1. Admin Consoleの概要ページで、次に示すように、製品およびサービスカードからCloud Service製品としてAdobe Experience Managerを選択します。

1. 上部ナビゲーションから「ユーザー」タブを選択し、「ユーザーを追加」を選択します。

1. ユーザーを追加ダイアログボックスで、追加するユーザーの電子メールIDを入力します。 「IDタイプ」で、チームメンバーのFederated IDがまだ設定されていない場合は「 Adobe ID 」を選択します。

1. 製品選択で、「Adobe Experience Manager as aCloud Service」を選択し、以下に示すように、製品プロファイル「Deployment Manager」をユーザーに割り当てます。 以下に示すように、適切なユーザーにAdmin Consoleで適切な役割が割り当てられていることを確認するには、 Cloud Manager製品プロファイルを参照してください。

   >[!NOTE]
   >ユーザーは、Cloud Managerリソースの作成後にDeployment Manager製品プロファイルに追加できます。

## 開発者製品プロファイルへのユーザーの割り当て {#assign-users-developer}

1. Cloud Managerプログラムを管理するユーザーを特定し、ビジネスオーナー製品プロファイルに追加します。 Cloud Managerにアクセスしてログインするのは、システム管理者が最初におこなう必要があります。 最初に、自分自身（システム管理者）をビジネスオーナー製品プロファイルに追加する必要があります。

1. Admin Consoleの概要ページで、次に示すように、製品およびサービスカードからCloud Service製品としてAdobe Experience Managerを選択します。

1. 上部ナビゲーションから「ユーザー」タブを選択し、「ユーザーを追加」を選択します。

1. ユーザーを追加ダイアログボックスで、追加するユーザーの電子メールIDを入力します。 「IDタイプ」で、チームメンバーのFederated IDがまだ設定されていない場合は「 Adobe ID 」を選択します。

1. 製品選択で、「Adobe Experience Manager as aCloud Service」を選択し、以下に示すように、製品プロファイル「開発者」をユーザーに割り当てます。 以下に示すように、適切なユーザーにAdmin Consoleで適切な役割が割り当てられていることを確認するには、 Cloud Manager製品プロファイルを参照してください。

   >[!NOTE]
   >ユーザーは、Cloud Managerリソースの作成後に開発者製品プロファイルに追加できます。

## 次の作業 {#whats-next}

*ビジネスオーナー*&#x200B;の役割に割り当てられたシステム管理者は、Cloud Managerにアクセスしてログインする必要があります。
>[!NOTE]
>Cloud Managerにログインしてアクセスする方法については、 Cloud Managerへの移動を参照してください。

ビジネスオーナーロールのCloud Managerユーザーは、プログラムと環境を含むクラウドリソースにログインし、設定できます。 これにより、エキスパートチームができるだけ早くAEMにCloud Serviceとしてアクセスできるようになります。
ビジネスオーナーがクラウドリソースを設定したら、Cloud Manager製品プロファイルに正常に追加された開発者とデプロイメントマネージャーは、Cloud Managerにアクセスし、学習パスを続行する方法を把握できます。

## その他のリソース {#additional-resources}

その他のリソースでは、以下について学習します。

* Cloud Manager
* Cloud Manager製品プロファイル
* Admin ConsoleIDの概要
