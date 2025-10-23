---
title: Cloud Manager へのアクセス
description: プロジェクトリソースを設定するための Cloud Manager へのアクセス方法について説明します。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
feature: Onboarding
source-git-commit: 858a9c4b61fd3a80a257313e48816b067ca77175
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 94%

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

   前の手順の [Cloud Manager 製品プロファイルへのチームメンバーの割り当て](assign-profiles-cloud-manager.md)に戻り、システム管理者に&#x200B;**ビジネスオーナー**&#x200B;の役割を割り当てる方法の詳細を参照してください。

1. [experience.adobe.com](https://experience.adobe.com) でCloud Managerにログインします。
1. クイックアクセスのグループ化で、「**Experience Manager**」をクリックします。
1. 左側のサイドパネルで、「**Cloud Manager**」をクリックします。

   ![コンソール上の Cloud Manager](/help/journey-onboarding/assets/consol-cloud-manager.png)

**ビジネスオーナー** の役割を持つシステム管理者は、最初にCloud Managerにログインする必要があります。 この最初のログインでは、**ビジネスオーナー** の役割を持つ他のユーザーがプログラムを作成できます。確認は表示されません。

<!--
By successfully signing in as a system administrator with the **Business Owner** role, you use Cloud Manager for use by the other users with the **Business Owner** role. You do not receive a confirmation or any message. Simply signing in is sufficient.

Until you sign in to Cloud Manager as a system administrator with the **Business Owner** role, other users with the **Business Owner** role cannot create programs in Cloud Manager. This rule is true even if they are assigned the correct roles. -->

## Cloud Manager に移動 {#navigate-cloud-manager}

1. [experience.adobe.com/experiencemanager](https://experience.adobe.com/experiencemanager) に移動します。
1. 左側のサイドパネルで、「**Cloud Manager**」をクリックします。

>[!NOTE]
>
>Cloud Manager で割り当てられた役割やアプリケーションの状態に応じて、Cloud Manager ユーザーインターフェイスの使用中に表示される画面が変わります。

<!--
Users with the **Business Owner** role receive a welcome email with a link to get started. Follow the steps below to navigate to Cloud Manager using this welcome email.

1. From your welcome email, click **Get started**, as shown in the figure below.
    ![Email example](/help/journey-onboarding/assets/get-started-email.png)

1. Navigate to Cloud Manager's **Programs & Products** page.

   >[!TIP]
   >
   >You can also navigate directly to Cloud Manager's login page from `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Bookmark this page for future reference.

1. You are directed to Cloud Manager's landing page. -->

<!-- OLD
Alternatively, you can navigate to Cloud Manager's **Programs and Products** page from the Adobe Experience Cloud home page using these steps.

1. Navigate directly to [Adobe Experience Cloud](https://experience.adobe.com) and login using your Adobe ID.

1. From the Adobe Experience Cloud home page, select **Experience Manager** to open the AEM home page.

   ![Experience Cloud homepage](/help/journey-onboarding/assets/setup-resources2.png)

1. On the **Cloud Manager** tile, select **Launch**.

   ![AEM home page](/help/journey-onboarding/assets/setup-resources3.png)

1. After successfully logging on, you are directed to the Cloud Manager landing page. See [Viewing Cloud Manager's Programs](#viewing-programs) for more details.

How you access your programs and products via Cloud Manager is up to you and has no effect on how you use Cloud Manager or how you manage your programs.

>[!NOTE]
>
>Depending on the roles assigned in Cloud Manager and the state of the application, you see different screens while using the Cloud Manager user interface. -->

## プログラムの表示 {#viewing-programs}

Cloud Manager に正常にアクセスすると、表示される内容は、以降のセクションで詳しく説明するように、プログラムの状態によって異なります。

### プログラムが存在しない場合 {#no-programs}

組織にプログラムが存在しない場合は、最初のプログラムを作成するようにランディングページで指示されます。

![プログラムがありません](/help/journey-onboarding/assets/cloud-manager-programs-do-not-exist.png)

### プログラムが既に存在する場合 {#programs-exist}

組織にプログラムが既に存在する場合は、ランディングページに既存のプログラムが表示され、プログラムを追加するボタンも表示されます。

![プログラムが存在します](/help/journey-onboarding/assets/cloud-manager-programs-exist.png)

### プログラムが存在し、システム管理者である場合 {#programs-exist-sysadmin}

組織にプログラムが存在し、ユーザーがシステム管理者である場合は、ランディングページに「**アクセスを管理**」ボタンと「**プログラムを追加**」オプションが表示されます。

![システム管理者の表示](/help/journey-onboarding/assets/cloud-manager-programs-as-sysadmin.png)

## ユーザーの役割の確認 {#verify-user-roles}

Cloud Manager に正常にログインしたら、**ビジネスオーナー**&#x200B;製品プロファイルが割り当てられていることを確認します。

1. ページの右上隅付近にある&#x200B;**アカウント**&#x200B;アイコンをクリックします。

1. 「**ユーザーの役割**」をクリックします。

   ![ユーザーの役割](/help/journey-onboarding/assets/cloud-manager-user-roles.png)

1. **ユーザーの役割**&#x200B;ダイアログボックスで、ユーザーに&#x200B;**ビジネスオーナー**&#x200B;の役割があることを確認します。

   ![ユーザーの役割のリスト](/help/journey-onboarding/assets/cloud-manager-user-roles-business-owner.png)

Cloud Manager にビジネスオーナーとして正常にログインしました。**ビジネスオーナー**&#x200B;の役割を割り当てられていない場合は、システム管理者にお問い合わせください。

## 次の手順 {#whats-next}

これで、システム管理者として Cloud Manager にアクセスできるので、最初のプログラムを作成する準備が整いました。

オンボーディングジャーニーを続け、次は[プログラムの作成](create-program.md)ドキュメントを確認して、プログラムの作成方法を学びます。

## その他のリソース {#additional-resources}

オンボーディングジャーニーのコンテンツの範囲を超えた情報について詳しくは、次の追加のオプションリソースを参照してください。

* [Cloud Manager の概要](/help/onboarding/cloud-manager-introduction.md) - 
Cloud Manager、Cloud Manager プログラム、環境について説明します。
* [AEM as a Cloud Service のチームおよび製品プロファイル](/help/onboarding/aem-cs-team-product-profiles.md) - ライセンス取得済みのアドビソリューションに対するアクセスを AEM as a Cloud Service のチームおよび製品プロファイルで許可および制限する方法について説明します。
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
