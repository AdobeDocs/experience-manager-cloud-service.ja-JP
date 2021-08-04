---
title: Cloud Manager への移動
description: このページでは、Cloud Manager ランディングページへの移動方法について説明します
exl-id: 9cf25d1d-a351-4ea0-b2e9-1df6ca4915b7
source-git-commit: 149776bdd7acce3e00710e50600d9bd1d7cc6b9b
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 80%

---

# Cloud Manager への移動 {#cloud-manager}

Cloud Manager は、AEM as a Cloud Service の重要な部分です。Cloud Manager を使用すると、組織がクラウド内の Experience Manager を自己管理できます。このサービスには継続的統合および継続的配信（CI／CD）フレームワークが備わっているので、IT チームや実装パートナーはパフォーマンスやセキュリティを妥協することなくカスタマイズや更新を迅速に配信できます。ユーザーインターフェイスを使用して、CI／CD パイプラインを設定および開始できます。

Cloud Manager へのアクセスがシステム管理者から許可されると、[Adobe Experience Cloud](https://experience.adobe.com) のホームページに移動するための電子メールが届きます。

>[!NOTE]
>ユーザーとして追加され、システム管理者によって 1 つ以上の Cloud Manager 役割（Admin Console 内の製品プロファイル）を割り当てられる必要があります。

1. お知らせメールで、「**使用を開始**」をクリックします（下図を参照）。
   ![](/help/onboarding/what-is-required/assets/get-started-email.png)


   >[!IMPORTANT]
   >または、[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)からCloud Managerのログインページに直接移動することもできます。 今後Cloud Managerのランディングページに直接移動する際に役立つように、このページをブックマークに追加してください。

さらに、Adobe Experience CloudのホームページからCloud Managerの「**プログラムと製品**」ページに移動することもできます。 次の手順に従います。

1. [Adobe Experience Cloud](https://experience.adobe.com)に直接移動し、Adobe IDを使用してログインします。

1. **Experience Manager** を選択します。
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/landing-page1.png)

1. Cloud Manager カードの「**Launch**」をクリックします。
[!UICONTROL Cloud Manager] に正常にログインすると、ユーザーインターフェイス（UI）を使用する準備が整います。
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/landing-page2.png)

1. 正常にログインすると、Cloud Manager のランディングページが表示されます。


## Cloud Manager ランディングページ {#cloud-manager-landing}

正常にログインすると、Cloud Manager のランディングページが表示されます。

>[!NOTE]
>[!UICONTROL Cloud Manager] で割り当てられた役割とアプリケーションの状態によっては、[!UICONTROL Cloud Manager] UI の使用中に異なる画面が表示されます。

次に示す 3 つのオプションのいずれかが表示されます。

* **Cloud Manager にプログラムが存在しません**

   組織にプログラムが存在しない場合は、最初のプログラムを作成するようにランディングページで指示されます（下図を参照）。

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

* **プログラムは既に Cloud Manager に存在します**

   組織にプログラムが既に存在する場合は、別のプログラムを追加するようにランディングページで指示され、既存のプログラムがすべてランディングページに表示されます（下図を参照）。

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

* **プログラムが存在しユーザーがシステム管理者です**

   組織にプログラムが既に存在し、ユーザーがシステム管理者である場合は、次の図に示すように、ランディングページに「**アクセスを管理**」ボタンと「**プログラムを追加**」オプションが表示されます。

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

ここから、Cloud Manager のビジネスオーナーの役割など、適切な権限を持つユーザーが、「**プログラムを追加**」を選択して[プログラムを追加](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/production-programs/creating-production-program.html?lang=ja#getting-access)ウィザードを起動できます。

Cloud Managerでプログラムを追加する方法については、次の作成を参照してください。

* [実稼動プログラム](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/production-programs/creating-production-program.html?lang=en)
* [サンドボックスプログラム](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sandbox-programs/creating-sandbox-program.html?lang=en)