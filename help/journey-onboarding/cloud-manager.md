---
title: Cloud Manager へのアクセス
description: プロジェクトリソースを設定するための Cloud Manager へのアクセス方法について説明します。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 41%

---

# Cloud Manager へのアクセス {#cloud-resources}

この部分では、 [オンボーディングジャーニー](overview.md) プロジェクトリソースを設定できるように Cloud Manager にアクセスする方法を学習します。

## 目的 {#objective}

このオンボーディングジャーニーの前の記事では、 [Cloud Manager 製品プロファイルへのチームメンバーの割り当て，](assign-profiles-cloud-manager.md) AEMaaCS チームに適切な役割を付与しました。 次に、チームが使用するプロジェクトリソースを設定できるように Cloud Manager にアクセスする方法を説明します。

このジャーニーの前の手順を完了したので、チームは Cloud Manager にアクセスできます。 Cloud Manager は、プログラムや環境などのプロジェクトリソースを作成および管理するために使用します。

このドキュメントを読んだ後、次の点を理解する必要があります。

* システム管理者が **ビジネスオーナー** の役割は、組織で Cloud Manager にログインしてアクセスする最初の役割である必要があります。
* Cloud Manager へのログイン方法。

## Cloud Manager {#cloud-manager}

Cloud Manager は、AEM as a Cloud Service の必須コンポーネントであり、チームの単一のエントリポイントとして機能します。専用の CI/CD パイプラインを使用してエンタープライズ開発を設定したお客様をサポートします。このパイプラインは、優れたエクスペリエンスを提供するために、徹底的なテストと最高のコード品質を確保するために備わっています。 Cloud Manager は、クラウドのリソースや環境を作成する機能など、セルフサービス方式での作業を開始するために必要なすべてを提供します。

通常、 **ビジネスオーナー** 製品プロファイルは、プログラムや環境などのクラウドリソースを追加します。 このユーザーは、ビジネスニーズと、Cloud Manager の初期設定を完了するユーザーを理解します。

このオンボーディングジャーニーの目的上、システム管理者は自分を既に **ビジネスオーナー** 製品プロファイルおよびは、クラウドリソースを設定します。 実際のプロジェクト要件に応じて、ビジネスオーナーはシステム管理者と同じ場合と同じでない場合があります。

## システム管理者およびビジネスオーナーとして Cloud Manager にアクセス {#access-sysadmin-bo}

割り当てたチームメンバーの前に **ビジネスオーナー** の役割は cloud manager にアクセスし、クラウドリソースの作成を開始できます。システム管理者には、 **ビジネスオーナー** このオンボーディングジャーニーの前の手順と同様に、 Cloud Manager にロールしてログインします。

1. システム管理者が、 **ビジネスオーナー** ロールが割り当てられました。

   * このジャーニーの前の手順に戻ります。 [Cloud Manager 製品プロファイルへのチームメンバーの割り当て](assign-profiles-cloud-manager.md) 割り当てに関する詳細 **ビジネスオーナー** 役割をシステム管理者に割り当てます（まだ割り当てていない場合）。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) から Cloud Manager にログインすると、通常のランディングページが表示されます。

を使用してシステム管理者として正常にサインインする **ビジネスオーナー** ロールを使用する場合、他のユーザーが使用する Cloud Manager を **ビジネスオーナー** 役割。 これについての確認やメッセージは表示されません。ログインするだけで十分です。

を使用してシステム管理者として Cloud Manager にログインするまで、 **ビジネスオーナー** 役割、 **ビジネスオーナー** ロールは、適切なロールが割り当てられている場合でも、Cloud Manager でプログラムを作成できません。

## Cloud Manager に移動 {#navigate-cloud-manager}

を持つ **ビジネスオーナー** の役割には、開始するためのリンクが記載された「ようこそ」の電子メールが届きます。 このメールを使用して Cloud Manager に移動するには、以下の手順に従います。

1. お知らせメールで、「**使用を開始**」をクリックします（下図を参照）。
   ![メールの例](/help/journey-onboarding/assets/get-started-email.png)

1. Cloud Manager の&#x200B;**プログラムと製品**&#x200B;ページに移動します。

   >[!TIP]
   >
   >`[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)` から Cloud Manager のログインページに直接移動することもできます。今後の参照用に、このページをブックマークに追加してください。

1. Cloud Manager のランディングページが表示されるようになります。

または、 Cloud Manager の **プログラムと製品** 次の手順に従って、Adobe Experience Cloudホームページからページを開きます。

1. [Adobe Experience Cloud](https://experience.adobe.com) に直接移動し、Adobe ID を使用してログインします。

1. Adobe Experience Cloud のホームページで、「**Experience Manager**」を選択します。

   ![Experience Cloud ホームページ](/help/journey-onboarding/assets/setup-resources2.png)

1. AEM ホームページが表示されます。ここから **Cloud Manager** タイルの「**ローンチ**」をクリックします。

   ![AEM ホームページ](/help/journey-onboarding/assets/setup-resources3.png)

1. 正常にログインすると、Cloud Manager のランディングページが表示されます。詳しくは、[Cloud Manager のプログラムの表示](#viewing-programs)の節を参照してください。

Cloud Manager を使用してプログラムや製品にアクセスする方法はユーザー次第であり、Cloud Manager の使用方法やプログラムの管理方法には影響しません。

>[!NOTE]
>
>Cloud Manager で割り当てられた役割とアプリケーションの状態に応じて、Cloud Manager UI の使用中に異なる画面が表示されます。

## プログラムの表示 {#viewing-programs}

Cloud Manager に正常にアクセスすると、表示される内容は、以降の節で説明するように、プログラムの状態によって異なります。

### プログラムが存在しない場合 {#no-programs}

組織にプログラムが存在しない場合は、最初のプログラムを作成するようにランディングページで指示されます。

![プログラムがありません](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### プログラムが既に存在する場合 {#programs-exist}

組織にプログラムが既に存在する場合は、ランディングページに既存のプログラムが表示され、プログラムを追加するボタンも表示されます。

![プログラムが存在します](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### プログラムが存在し、システム管理者である場合 {#programs-exist-sysadmin}

組織にプログラムが既に存在し、システム管理者である場合は、ランディングページが表示されます **アクセスを管理** ～と一緒に **プログラムの追加** オプション。

![システム管理者の表示](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## ユーザーの役割の確認 {#verify-user-roles}

Cloud Manager に正常にログインしたら、**ビジネスオーナー**&#x200B;製品プロファイルが割り当てられていることを確認します。

1. ウィンドウの右上からプロファイルを選択します。

   ![ユーザープロファイル](/help/journey-onboarding/assets/setup-resources5.png)

1. 「**ユーザーの役割**」を選択し、ユーザーに割り当てられている役割を表示します。

   ![ユーザーの役割](/help/journey-onboarding/assets/setup-resources6.png)

1. ダイアログで、ユーザーが **ビジネスオーナー** 役割。

   ![ユーザーの役割のリスト](/help/journey-onboarding/assets/setup-resources7.png)

Cloud Manager にビジネスオーナーとして正常にログインしました。**ビジネスオーナー**&#x200B;の役割を割り当てられていない場合は、システム管理者にお問い合わせください。

## 次の手順 {#whats-next}

これで、システム管理者として Cloud Manager にアクセスできるので、最初のプログラムを作成する準備が整いました。

次にドキュメントを確認して、オンボーディングジャーニーを続行する必要があります [プログラムの作成](create-program.md) その方法を学ぶ場所

## その他のリソース {#additional-resources}

その他に、次のリソースも参照してください。

* [Cloud Manager の概要](/help/onboarding/cloud-manager-introduction.md) - Cloud Manager、Cloud Manager プログラム、環境について説明します。
