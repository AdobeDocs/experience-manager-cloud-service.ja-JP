---
title: Cloud Manager へのアクセス
description: プロジェクトリソースを設定するための Cloud Manager へのアクセス方法について説明します。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 5c9dbaa25f0142afdae8b09dc18d1e1aaaf4c1fb
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 53%

---

# Cloud Manager へのアクセス {#cloud-resources}

この部分では、 [オンボーディングジャーニー](overview.md) Cloud Manager にアクセスしてプロジェクトリソースを設定する方法を学びます。

## 目的 {#objective}

オンボーディングジャーニーの前の記事 [Cloud Manager 製品プロファイルへのチームメンバーの割り当て](assign-profiles-cloud-manager.md)では、AEMaaCS チームに適切な役割を付与しました。次に、チームが使用するプロジェクトリソースを設定できるように Cloud Manager にアクセスする方法を説明します。

ジャーニーの前の手順を完了したので、チームは Cloud Manager にアクセスできます。Cloud Manager を使用すると、プログラムや環境などのプロジェクトリソースの作成と管理を行えます。

このドキュメントを読むと、次の内容を理解できるようになります。

* システム管理者が **ビジネスオーナー** の役割は、組織で Cloud Manager にログオンしてアクセスする最初の役割である必要があります。
* Cloud Manager へのログイン方法。

## Cloud Manager {#cloud-manager}

Cloud Manager は、AEM as a Cloud Service に不可欠なコンポーネントであり、チームにとって単一のエントリポイントとして機能します。専用の CI/CD パイプラインを構築して、お客様のエンタープライズ開発体制をサポートします。このパイプラインは、徹底したテストと最高のコード品質を確保し、優れたエクスペリエンスを提供するために備わっています。Cloud Manager は、クラウドのリソースや環境を作成する機能など、セルフサービス方式での作業を開始するために必要なものを提供します。

通常、**ビジネスオーナー**&#x200B;の製品プロファイルに割り当てられたグループメンバーは、プログラムや環境などのクラウドリソースの追加を担当します。この担当者は、ビジネスニーズを理解し、Cloud Manager の初期設定を実施します。

このオンボーディングジャーニーの目的上、システム管理者は自分を既に **ビジネスオーナー** 製品プロファイルを作成し、クラウドリソースを設定できます。 実際のプロジェクト要件に応じて、ビジネスオーナーはシステム管理者と同じ場合と同じでない場合があります。

## システム管理者およびビジネスオーナーとして Cloud Manager にアクセス {#access-sysadmin-bo}

割り当てたチームメンバーの前に **ビジネスオーナー** の役割は cloud manager にアクセスし、クラウドリソースの作成を開始できます。システム管理者には、 **ビジネスオーナー** 役割。 また、このオンボーディングジャーニーの前の手順と同様に、Cloud Manager にログインする必要があります。

1. システム管理者として、**ビジネスオーナー**&#x200B;の役割が割り当てられていることを確認します。

   * このジャーニーの前の手順に戻ります。 [Cloud Manager 製品プロファイルへのチームメンバーの割り当て](assign-profiles-cloud-manager.md) 割り当てに関する詳細 **ビジネスオーナー** の役割をシステム管理者に割り当てます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) から Cloud Manager にログインすると、通常のランディングページが表示されます。

**ビジネスオーナー**&#x200B;の役割を持つシステム管理者がログインに成功すると、**ビジネスオーナー**&#x200B;の役割を持つ他のユーザーが使用できるように Cloud Manager が初期化されます。確認メッセージやメッセージは表示されません。 サインインだけで十分です。

を使用してシステム管理者として Cloud Manager にログインするまで、 **ビジネスオーナー** 役割、 **ビジネスオーナー** ロールは、Cloud Manager でプログラムを作成できません。 このルールは、正しい役割が割り当てられている場合でも当てはまります。

## Cloud Manager に移動 {#navigate-cloud-manager}

を持つ **ビジネスオーナー** 役割には、開始用のリンクが記載された「ようこそ」の電子メールが届きます。 このメールを使用して Cloud Manager に移動するには、以下の手順に従います。

1. ようこそメールで、 **はじめに**（下の図を参照）。
   ![メールの例](/help/journey-onboarding/assets/get-started-email.png)

1. Cloud Manager の **プログラムと製品** ページ。

   >[!TIP]
   >
   >`[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)` から Cloud Manager のログインページに直接移動することもできます。今後の参照用に、このページをブックマークに追加してください。

1. Cloud Manager のランディングページに誘導されます。

または、次の手順に従って、Adobe Experience Cloud のホームページから Cloud Manager の&#x200B;**プログラムと製品**&#x200B;ページに移動することもできます。

1. [Adobe Experience Cloud](https://experience.adobe.com) に直接移動し、Adobe ID を使用してログインします。

1. Adobe Experience Cloudホームページで、「 」を選択します。 **Experience Manager** をクリックしてAEMホームページを開きます。

   ![Experience Cloud ホームページ](/help/journey-onboarding/assets/setup-resources2.png)

1. の **Cloud Manager** タイル、選択 **起動**.

   ![AEM ホームページ](/help/journey-onboarding/assets/setup-resources3.png)

1. 正常にログオンすると、Cloud Manager ランディングページに移動します。 詳しくは、 [Cloud Manager のプログラムの表示](#viewing-programs) を参照してください。

Cloud Manager を使用してプログラムや製品にアクセスする方法はユーザー次第であり、Cloud Manager の使用方法やプログラムの管理方法には影響しません。

>[!NOTE]
>
>Cloud Manager で割り当てられた役割とアプリケーションの状態に応じて、Cloud Manager ユーザーインターフェイスを使用している間に異なる画面が表示されます。

## プログラムの表示 {#viewing-programs}

Cloud Manager に正常にアクセスした後に表示される内容は、以降の節で説明するように、プログラムの状態によって異なります。

### プログラムが存在しない場合 {#no-programs}

組織にプログラムが存在しない場合は、最初のプログラムを作成するようにランディングページで指示されます。

![プログラムがありません](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### プログラムが既に存在する場合 {#programs-exist}

組織内にプログラムが存在する場合、ランディングページには既存のプログラムが表示され、さらにプログラムを追加するためのボタンも表示されます。

![プログラムが存在します](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### プログラムが存在し、システム管理者である場合 {#programs-exist-sysadmin}

組織にプログラムが存在し、システム管理者である場合は、ランディングページが表示されます **アクセスを管理** ～と一緒に **プログラムの追加** オプション。

![システム管理者の表示](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## ユーザーの役割の確認 {#verify-user-roles}

Cloud Manager に正常にログインしたら、**ビジネスオーナー**&#x200B;製品プロファイルが割り当てられていることを確認します。

1. ウィンドウの右上からプロファイルを選択します。

   ![ユーザープロファイル](/help/journey-onboarding/assets/setup-resources5.png)

1. ユーザーに割り当てられているロールを表示するには、「 」を選択します **ユーザーの役割**.

   ![ユーザーの役割](/help/journey-onboarding/assets/setup-resources6.png)

1. ダイアログで、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;の役割を持っていることを確認する必要があります。

   ![ユーザーの役割のリスト](/help/journey-onboarding/assets/setup-resources7.png)

Cloud Manager にビジネスオーナーとして正常にログインしました。**ビジネスオーナー**&#x200B;の役割を割り当てられていない場合は、システム管理者にお問い合わせください。

## 次の手順 {#whats-next}

これで、システム管理者として Cloud Manager にアクセスできるので、最初のプログラムを作成する準備が整いました。

次にドキュメントを確認して、オンボーディングジャーニーを続行します [プログラムの作成](create-program.md) その方法を学ぶ場所

## その他のリソース {#additional-resources}

オンボーディングジャーニーのコンテンツの範囲を超えたい場合の追加のオプションリソースを次に示します。

* [Cloud Manager の概要](/help/onboarding/cloud-manager-introduction.md) - Cloud Manager、Cloud Manager プログラム、環境について説明します。
* [AEM as a Cloud Service のチームおよび製品プロファイル](/help/onboarding/aem-cs-team-product-profiles.md) - ライセンス取得済みのアドビソリューションに対するアクセスを AEM as a Cloud Service のチームおよび製品プロファイルで許可および制限する方法について説明します。
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
