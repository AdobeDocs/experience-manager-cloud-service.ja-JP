---
title: Cloud Manager へのアクセス
description: プロジェクトリソースを設定するための Cloud Manager へのアクセス方法について説明します。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
feature: Onboarding
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '1040'
ht-degree: 100%

---

# Cloud Manager へのアクセス {#cloud-resources}

[オンボーディングジャーニー](overview.md)のこのパートでは、プロジェクトリソースを設定する Cloud Manager へのアクセス方法について説明します。

## 目的 {#objective}

オンボーディングジャーニーの前の記事 [Cloud Manager 製品プロファイルへのチームメンバーの割り当て](assign-profiles-cloud-manager.md)では、AEMaaCS チームに適切な役割を付与しました。ここでは、チームが使用するプロジェクトリソースを設定するための Cloud Manager にアクセスする方法について説明します。

ジャーニーの前の手順を完了したので、チームは Cloud Manager にアクセスできます。Cloud Manager を使用すると、プログラムや環境などのプロジェクトリソースの作成と管理を行えます。

このドキュメントを読むと、次の点を理解できるようになります。

* **ビジネスオーナー**&#x200B;の役割を割り当てられたシステム管理者が、組織で最初に Cloud Manager にログオンしてアクセスする必要があること。
* Cloud Manager へのログイン方法。

## Cloud Manager {#cloud-manager}

Cloud Manager は、AEM as a Cloud Service に不可欠なコンポーネントであり、チームにとって単一のエントリポイントとして機能します。専用の CI/CD パイプラインを構築して、お客様のエンタープライズ開発体制をサポートします。このパイプラインは、徹底したテストと最高のコード品質を確保し、優れたエクスペリエンスを提供するために備わっています。Cloud Manager は、クラウドのリソースや環境を作成する機能など、セルフサービス方式での作業を開始するために必要なものを提供します。

通常、**ビジネスオーナー**&#x200B;の製品プロファイルに割り当てられたグループメンバーは、プログラムや環境などのクラウドリソースの追加を担当します。この担当者は、ビジネスニーズを理解し、Cloud Manager の初期設定を実施します。

このオンボーディングジャーニーの目的上、システム管理者は既に&#x200B;**ビジネスオーナー**&#x200B;の製品プロファイルに割り当てられており、クラウドリソースを設定できます。実際のプロジェクト要件に応じて、ビジネスオーナーはシステム管理者と同一人物の場合も別の人物の場合もあります。

## システム管理者およびビジネスオーナーとして Cloud Manager にアクセス {#access-sysadmin-bo}

**ビジネスオーナー**&#x200B;の役割に割り当てたチームメンバーが Cloud Manager にアクセスし、クラウドリソースの作成を開始できるようにするには、システム管理者に&#x200B;**ビジネスオーナー**&#x200B;の役割を割り当てる必要があります。また、このオンボーディングジャーニーの前の手順と同様に、Cloud Manager にログインする必要があります。

1. システム管理者として、**ビジネスオーナー**&#x200B;の役割が割り当てられていることを確認します。

   * このジャーニーの前の手順の [Cloud Manager 製品プロファイルへのチームメンバーの割り当て](assign-profiles-cloud-manager.md)に戻り、システム管理者に&#x200B;**ビジネスオーナー**&#x200B;の役割を割り当てる方法の詳細を参照してください。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) から Cloud Manager にログインすると、通常のランディングページが表示されます。

**ビジネスオーナー**&#x200B;の役割を持つシステム管理者がログインに成功すると、**ビジネスオーナー**&#x200B;の役割を持つ他のユーザーが使用できるように Cloud Manager が初期化されます。確認メッセージなどのメッセージは表示されません。ログインするだけで十分です。

**ビジネスオーナー**&#x200B;の役割を持つシステム管理者が Cloud Manager にログインするまで、**ビジネスオーナー**&#x200B;の役割を持つ他のユーザーは、Cloud Manager でプログラムを作成できません。このルールは、正しい役割が割り当てられている場合でも適用されます。

## Cloud Manager に移動 {#navigate-cloud-manager}

**ビジネスオーナー**&#x200B;の役割を持つユーザーには、開始するためのリンクが記載されたウェルカムメールが届きます。このウェルカムメールを使用して Cloud Manager に移動するには、以下の手順に従います。

1. ウェルカムメールで、「**入門**」をクリックします（下図を参照）。
   ![メールの例](/help/journey-onboarding/assets/get-started-email.png)

1. Cloud Manager の&#x200B;**プログラムと製品**&#x200B;ページに移動します。

   >[!TIP]
   >
   >`[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)` から Cloud Manager のログインページに直接移動することもできます。今後の参照用に、このページをブックマークに追加してください。

1. Cloud Manager のランディングページが表示されるようになります。

または、次の手順に従って、Adobe Experience Cloud のホームページから Cloud Manager の&#x200B;**プログラムと製品**&#x200B;ページに移動することもできます。

1. [Adobe Experience Cloud](https://experience.adobe.com) に直接移動し、Adobe ID を使用してログインします。

1. Adobe Experience Cloud ホームページで「**Experience Manager**」を選択して、AEM ホームページを開きます。

   ![Experience Cloud ホームページ](/help/journey-onboarding/assets/setup-resources2.png)

1. **Cloud Manager** タイルで、「**起動する**」を選択します。

   ![AEM ホームページ](/help/journey-onboarding/assets/setup-resources3.png)

1. 正常にログオンすると、Cloud Manager ランディングページが表示されるようになります。詳しくは、[Cloud Manager のプログラムの表示](#viewing-programs)を参照してください。

Cloud Manager を使用してプログラムや製品にアクセスする方法はユーザー次第であり、Cloud Manager の使用方法やプログラムの管理方法には影響しません。

>[!NOTE]
>
>Cloud Manager で割り当てられた役割やアプリケーションの状態に応じて、Cloud Manager ユーザーインターフェイスの使用中に表示される画面が変わります。

## プログラムの表示 {#viewing-programs}

Cloud Manager に正常にアクセスすると、表示される内容は、以降のセクションで詳しく説明するように、プログラムの状態によって異なります。

### プログラムが存在しない場合 {#no-programs}

組織にプログラムが存在しない場合は、最初のプログラムを作成するようにランディングページで指示されます。

![プログラムがありません](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### プログラムが既に存在する場合 {#programs-exist}

組織にプログラムが既に存在する場合は、ランディングページに既存のプログラムが表示され、プログラムを追加するボタンも表示されます。

![プログラムが存在します](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### プログラムが存在し、システム管理者である場合 {#programs-exist-sysadmin}

組織にプログラムが存在し、ユーザーがシステム管理者である場合は、ランディングページに「**アクセスを管理**」ボタンと「**プログラムを追加**」オプションが表示されます。

![システム管理者の表示](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## ユーザーの役割の確認 {#verify-user-roles}

Cloud Manager に正常にログインしたら、**ビジネスオーナー**&#x200B;製品プロファイルが割り当てられていることを確認します。

1. ウィンドウの右上からプロファイルを選択します。

1. ユーザーに割り当てられているロールを表示するには、「**ユーザーの役割**」を選択します。

   ![ユーザーの役割](/help/journey-onboarding/assets/setup-resources6.png)

1. ダイアログで、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;の役割を持っていることを確認する必要があります。

   ![ユーザーの役割のリスト](/help/journey-onboarding/assets/setup-resources7.png)

Cloud Manager にビジネスオーナーとして正常にログインしました。**ビジネスオーナー**&#x200B;の役割を割り当てられていない場合は、システム管理者にお問い合わせください。

## 次のステップ {#whats-next}

これで、システム管理者として Cloud Manager にアクセスできるので、最初のプログラムを作成する準備が整いました。

オンボーディングジャーニーを続け、次は[プログラムの作成](create-program.md)ドキュメントを確認して、プログラムの作成方法を学びます。

## その他のリソース {#additional-resources}

オンボーディングジャーニーのコンテンツの範囲を超えてさらに詳しく知りたい場合に役立つ、追加のオプションリソースを次に示します。

* [Cloud Manager の概要](/help/onboarding/cloud-manager-introduction.md) - 
Cloud Manager、Cloud Manager プログラム、環境について説明します。
* [AEM as a Cloud Service のチームおよび製品プロファイル](/help/onboarding/aem-cs-team-product-profiles.md) - ライセンス取得済みのアドビソリューションに対するアクセスを AEM as a Cloud Service のチームおよび製品プロファイルで許可および制限する方法について説明します。
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
