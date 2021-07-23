---
title: Cloud Managerを使用したクラウドリソースの設定
description: このページでは、Cloud Managerを使用してクラウドリソースを設定する方法について説明します
hide: true
hidefromtoc: true
index: false
source-git-commit: 730dcb038a3080ff736a83963811aaf39d270845
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 2%

---

# Cloud Managerを使用したクラウドリソースの設定 {#setup-cloud-resources}

*ビジネスオーナー*&#x200B;の役割に割り当てられたシステム管理者は、Cloud Managerにアクセスしてログインする必要があります。 その後、*ビジネスオーナー*&#x200B;製品プロファイルに割り当てられたチームメンバーは、Cloud Managerにログインし、クラウドプログラムと環境を作成して、エキスパートチームが作業を開始できるようにする必要があります。

## 目的 {#objective}

このドキュメントでは、クラウドリソースの作成方法と実行者について説明します。

この節を読むと、次の内容を理解できます。

* *ビジネスオーナー*&#x200B;の役割に割り当てられたシステム管理者は、Cloud Managerにアクセスしてログインする最初のユーザーである必要があります。
* クラウドプログラムと環境の作成方法。

## はじめに {#introduction}

クラウドリソースの追加は、Cloud Managerビジネスオーナー製品プロファイルに割り当てられたチームメンバーがCloud Managerを通じておこないます。 通常、このユーザーは、ビジネスニーズを理解し、Cloud Managerの初期設定を完了するユーザーです。

以下の節では、[クラウドサービスプログラム](#create-cloud-service-program)と[環境](#create-cloud-environments)の作成方法について説明します。

### 前提条件 {#prerequisites}

* *ビジネスオーナー*&#x200B;の役割に割り当てられたシステム管理者は、Cloud Managerにアクセスしてログインする必要があります。

* [Cloud Managerに移動してログインする方法を理解します。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=en)

* [Cloud Managerの製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)について理解してください。

* プログラムの作成に関する考慮事項を理解します。 詳しくは、このビデオをご覧ください。

* Cloud Managerの[プログラム](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html?lang=en)と[環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=ja)の概念を理解します。

## Cloud Manager への移動 {#navigate-cloud-manager}

1. *ビジネスオーナー*&#x200B;ユーザーは、開始場所からお知らせメールを受け取るか、見つからない場合は[Adobe Experience Cloud](https://experience.adobe.com/#/@ccs/home)に直接アクセスし、Adobe IDを使用してログインします。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources1.png)

1. Adobe Experience Cloudのホームページで、「**Experience Manager**」を選択します。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources2.png)

1. これにより、AEMホームページが表示されます。 ここから、 **Cloud Manager**&#x200B;を起動します。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources3.png)

1. 次の図に示すように、Cloud Managerのランディングページが表示されます。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources4.png)

1. ビジネスオーナー製品プロファイルが割り当てられていることを確認します。 これをおこなうには、次に示すように、右上からプロファイルを選択します。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources5.png)

1. 「**ユーザーの役割**」を選択し、ビジネスオーナーに割り当てられていることを確認します。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources6.png)

1. これにより、ビジネスオーナーとしてのユーザーの役割が確認されます。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources7.png)

   お疲れ様でした。Cloud Managerにビジネスオーナーとして正常にログインしました。

## 作成Cloud Service {#create-cloud-service-program}

Cloud Managerからクラウドサービスプログラムを作成するには、以下の手順に従います。

1. 次に示すように、 Cloud Managerランディングページに移動します。

   >[!NOTE]
   >この手順を正常に完了するには、 Cloud Managerビジネスオーナー製品プロファイルに割り当てられているチームメンバーである必要があります。

   ここから、「**プログラムの追加**」をクリックして、「プログラムの追加」ウィザードを起動します。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources4.png)

   >[!NOTE]
   >AEM as a Cloudプログラムの作成方法と、プログラムを作成する前の重要な考慮事項については、[ビデオ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)をご覧ください。

   >[!IMPORTANT]
   >プログラムの追加ウィザードの使い方に関する詳しい手順については、[ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/production-programs/creating-production-program.html?lang=en)を参照してください。
   >
   >* 作成後はプログラム名を変更できないことに注意してください。 プログラムに与えたい名前を確認することをお勧めします。
   >* プログラム名を変更する必要がある場合は、Adobeサポートに問い合わせるか、またはAdobe担当者に問い合わせます。 これらは、プログラムを効果的に削除するのに役立ちます。 チームが行った作業が失われる可能性があるので、再びやり直す必要があります。


1. クラウドプログラムが正常に作成されたら、プログラムに移動して、以下に示すように、プログラムの&#x200B;**概要**&#x200B;ページを確認できます。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources8.png)

   >[!NOTE]
   >まだおこなっていない場合は、今すぐ開発者メンバーをCloud Managerチームに追加してください。 開発者製品プロファイルへのユーザーの追加を参照し、概要の手順に従います。

1. デベロッパー製品プロファイルに割り当てられたメンバーは、Cloud Managerにログインし、[Cloud Manager Gitを管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en)できます。

   お疲れさまでした。 プログラムが正常に作成され、開発者がCloud Manager Gitにアクセスできるようになりました。


## クラウド環境の作成 {#create-cloud-environments}

クラウドプログラムを正常に作成したら、クラウド環境を作成します。

Cloud Managerからクラウド環境を作成するには、次の手順に従います。

1. Cloud Managerの&#x200B;**概要**&#x200B;ページに移動し、環境カードから「**追加**」を選択します。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources9.png)

   >[!IMPORTANT]
   >この手順を正常に完了するには、ビジネスオーナーまたはデプロイメントマネージャーの役割を持つCloud Managerユーザーがログインする必要があります。

   さらに、 [ビデオ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en)のクイックチュートリアルでは、Cloud Manager環境と、それらの環境をプログラムに追加する方法についても説明しています。

1. これにより、環境の追加ウィザードが起動し、環境の追加を指示します。 最初に開発環境を追加して、使い慣れてください。 詳しくは、[環境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=ja#adding-environments)の追加を参照してください。

   >[!NOTE]
   >まだおこなっていない場合は、今すぐ開発者メンバーをCloud Managerチームに追加してください。 開発者製品プロファイルへのユーザーの追加を参照し、概要の手順に従います。

1. デベロッパー製品プロファイルに割り当てられたメンバーは、Cloud Managerにログインし、[Cloud Manager Gitを管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en)できます。

   お疲れさまでした。 プログラムが正常に作成され、開発者がCloud Manager Gitにアクセスできるようになりました。

   おめでとうございます。これで、クラウドプログラム環境が作成され、開発者がチームに追加されました。

## 次の作業 {#whats-next}

Cloud Managerを管理する権限では不十分なので、チームメンバーにインスタンスに対する権限を付与する必要があります。 クラウドリソースが作成され、チームからアクセスする準備が整ったので、システム管理者は、Admin ConsoleのCloud Service製品プロファイルとしてチームメンバーをAEMに割り当てる必要があります。

次に、「チームメンバーのAEM as a Team Product Profilesへの割り当て」ドキュメントを確認して、オンボーディングジャーニーを続行する必要があります。

>[!NOTE]
>AEM as aCloud Serviceユーザーに対するアクセス権を付与するには、2つの製品プロファイル「AEM Users」または「AEM Administrators」のいずれかに属している必要があります。 詳細情報を参照してください。

## その他のリソース {#additional-resources}

その他のリソースでは、以下について学習します。

* [プログラムタイプとプログラムの追加](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)
* [環境タイプと環境の追加](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en)
* [Cloud Manager Gitの管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en)
* [Admin ConsoleからのAEM as aCloud Serviceへのアクセスの設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=en#adobe-ims-users)
