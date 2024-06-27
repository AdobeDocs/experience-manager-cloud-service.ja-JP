---
title: デプロイ [!DNL Content Hub]
description: Content Hubをデプロイしてアクティブ化し、様々なタイプの権限（アセットのアップロード、ユーザーのAdobe Express）を持つユーザーにアクセスを提供する方法と、ユーザーに管理者権限を提供する方法について説明します。
role: Admin
source-git-commit: 56af07a198e1350282f5d3f771c1c29db318b90e
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 3%

---


# Content Hubのデプロイ {#deploy-content-hub}

![Content Hubのデプロイ](assets/deploy-content-hub.png)

Content Hubは、組織やビジネスパートナーがオンブランドのコンテンツにアクセスしやすくするために、Experience Manager Assetsas a Cloud Serviceの一部として利用できます。

Experience Manager Assetsのas a Cloud Serviceで承認済みとマークされたアセットは、Content Hubでアセットを配布することができます。

この記事では、必要に応じた権限のバリエーションなど、Content Hubへのアクセスをユーザーに提供するエンドツーエンドのワークフローを説明します。

Content Hubに対する権限には、次のような種類があります。

* [アセットコンシューマー](#onboard-content-hub-consumer-users):Content Hub ポータルでブランド承認済みアセットにアクセスします。

* [管理者](#onboard-content-hub-administrator)：へのアクセス [設定ユーザーインターフェイス](/help/assets/configure-content-hub-ui-options.md) 送信権限を持つ Asset Consumer に加えて、Content Hubでも可能です。

* [送信権限を持つアセットコンシューマー](#onboard-content-hub-consumer-users-submission-rights)：次の機能 [Content Hubへのアセットのアップロード](/help/assets/upload-brand-approved-assets.md) および [Adobe Expressの統合](/help/assets/edit-images-content-hub.md) Content Hub ポータルでブランド承認済みアセットにアクセスするほか、

* [アセットディストリビューター](#content-hub-asset-distributors):Experience Manager Assetsas a Cloud Service上のアセットを承認して、それらのアセットをContent Hubで使用できるようにする機能。

## 手順 1:Cloud Managerを使用してContent Hub for Experience Manager Assetsを有効にする {#enable-content-hub}

Content Hub ポータルにアクセスするには、管理者はまずCloud Managerを使用してContent Hub for Experience Manager Assetsas a Cloud Serviceを有効にする必要があります。 以下の手順を実行します。

1. Cloud Managerにログオンします。 ログイン時に適切な組織を選択していることを確認します。 Cloud Managerにすべてのプログラムが一覧表示されます。

1. Experience Manager Assetsas a Cloud Serviceプログラムに移動し、「その他のオプション」アイコン（...）をクリックして選択します。 **[!UICONTROL プログラムを編集]**.

   ![Cloud Managerでプログラムを編集](assets/edit-program-cloud-manager.png)

1. 日 [!UICONTROL プログラムを編集] ダイアログで、 **[!UICONTROL ソリューションとアドオン]** タブ。

1. を展開 **[!UICONTROL Assets]** を選択して、 **[!UICONTROL Content Hub]**.
   ![Cloud ManagerでContent Hubを選択します。](assets/edit-program-cloud-manager-content-hub.png)

1. 「**[!UICONTROL 更新]**」をクリックします。

Content HubがExperience Manager Assetsas a Cloud Serviceに対して有効になりました。

Experience Manager Assetsを初めて使用する場合は、 **[!UICONTROL プログラムを追加]** 次に、プログラムの詳細（プログラム名、実稼動用に設定）を入力し、をクリックします **[!UICONTROL 続行]**. 次に、以下を選択できます **[!UICONTROL Assets]** および **[!UICONTROL Content Hub]** が含まれる **[!UICONTROL ソリューションとアドオン]** タブ。

### Admin Console時のContent Hub インスタンスと製品プロファイル{#content-hub-instance-product-profile}

後 [Cloud Managerを使用してAssetsas a Cloud Service用にContent Hubを有効化](#enable-content-hub)にAdmin Consoleされ、AEM Assetsのas a Cloud Service内に新しいインスタンスが作成されます `contenthub` 接尾辞として

![Content Hubの新しいインスタンス](assets/new-instance-content-hub.png)

はありません `author` または `publish` Content Hubのインスタンス名で指定します。

インスタンス名をクリックして、Content Hub製品プロファイルを表示します。

![Content Hub製品プロファイル](assets/content-hub-product-profile.png)

## 手順 2:Content Hub管理者をオンボーディングする {#onboard-content-hub-administrator}

Content Hub管理者は、Content Hubにアセットを追加できるほか、 [設定オプション](/help/assets/configure-content-hub-ui-options.md) （組織内の他のユーザー用）。

Content Hub管理者をオンボーディングするには：

1. [Content Hub ユーザー製品プロファイルにアクセスしてクリックします。](#content-hub-instance-product-profile).

1. クリック **[!UICONTROL ユーザーを追加]** 製品プロファイルにユーザーまたはユーザーグループを追加するには、次の手順を実行します。

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

1. Content Hub製品プロファイルにユーザーを追加した後、Admin Console上の製品のリストでExperience Manager Assets製品名をクリックして、AEM as a Cloud Service製品プロファイルにアクセスします。

1. AEM as a Cloud Service用の実稼動オーサーインスタンスをクリックします。
   ![AEM as a Cloud Serviceの製品プロファイル](assets/aem-cloud-service-instances.png)

   Admin Consoleには、AEM as a Cloud Service用の 2 つの製品プロファイル（Administrators と Users）が表示されます。
1. 「管理者」製品プロファイルをクリックし、 **[!UICONTROL ユーザーを追加]** 製品プロファイルにユーザーを追加する場合
   ![管理者製品プロファイル](assets/aem-cs-admin-product-profile.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

## 手順 3:Content Hub asset consumer ユーザーをオンボーディングする {#onboard-content-hub-consumer-users}

Content Hub コンシューマーユーザーは、ポータルで利用可能なアセットにアクセスできますが、新しいアセットを追加したり、既存のアセットを変更したりすることはできません。

コンシューマーユーザーをContent Hubにオンボーディングするには：

1. [Content Hub ユーザー製品プロファイルにアクセスしてクリックします。](#content-hub-instance-product-profile).

1. クリック **[!UICONTROL ユーザーを追加]** 製品プロファイルにユーザーまたはユーザーグループを追加するには、次の手順を実行します。

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

これで、これらのユーザーは、Content Hub ポータルで使用可能なアセットにアクセスできます。

>[!NOTE]
>
>外部 ID プロバイダーとの同期など、高度なエンタープライズ機能をすべて使用できます。

Admin Consoleを使用して適切なユーザーを追加した後、次のリンクを使用してContent Hubにアクセスできます。

`https://experience.adobe.com/#/assets/contenthub`

### ユーザーへのメール通知を無効にする {#disable-email-notifications}

管理者が、ユーザーがContent Hub製品プロファイルに追加されたときに送信されるメール通知を無効にする必要がある場合：

製品プロファイル名の横にある検索アイコンをクリックし、を無効にします **[!UICONTROL メールでユーザーに通知する]** 切り替えます。

![メール通知を無効にする](assets/disable-email-notifications.png)


## 手順 4：送信権限を持つContent Hub asset consumer ユーザーのオンボーディング（オプション） {#onboard-content-hub-consumer-users-submission-rights}

送信権限を持つContent Hub asset consumer ユーザーは、次のことができます。

* [ブランドが承認した新しいアセットのContent Hubへのアップロード](/help/assets/upload-brand-approved-assets.md).

* [Adobe Expressを使用して既存のアセットを変更し、アセットをリポジトリに保存します](/help/assets/edit-images-content-hub.md). Adobe Expressを使用したアセットの編集は、ユーザーがAdobe Express権限を持っている場合にのみ使用できます。

送信権限を使用してContent Hub コンシューマーユーザーをオンボードするには：

1. [Content Hub製品プロファイルにユーザーを追加した後](#onboard-content-hub-consumer-users)で、Admin Console時の製品のリストでAEM as a Cloud Service製品名をクリックして、Experience Manager Assets製品プロファイルにアクセスします。

1. AEM as a Cloud Service用の実稼動オーサーインスタンスをクリックします。
   ![AEM as a Cloud Serviceの製品プロファイル](assets/aem-cloud-service-instances.png)

   Admin Consoleには、AEM as a Cloud Service用の 2 つの製品プロファイル（Administrators と Users）が表示されます。
1. ユーザー製品プロファイルをクリックし、 **[!UICONTROL ユーザーを追加]** 製品プロファイルにユーザーを追加する場合
   ![ユーザー製品プロファイル](assets/aem-cs-user-product-profile.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

## Content Hub アセットディストリビューター {#content-hub-asset-distributors}

アセットディストリビューターは、AEM as a Cloud Service上のアセットを承認して、Content Hub上で使用できるようにします。

アセット配布者の役割を設定するには：

1. Admin Console時の製品のリストでExperience Manager Assets製品名をクリックして、AEM as a Cloud Service製品プロファイルにアクセスします。

1. AEM as a Cloud Service用の実稼動オーサーインスタンスをクリックします。
   ![AEM as a Cloud Serviceの製品プロファイル](assets/aem-cloud-service-instances.png)

   Admin Consoleには、AEM as a Cloud Service用の 2 つの製品プロファイル（Administrators と Users）が表示されます。
1. ユーザー製品プロファイルをクリックし、 **[!UICONTROL ユーザーを追加]** 製品プロファイルにユーザーを追加する場合
   ![ユーザー製品プロファイル](assets/aem-cs-user-product-profile.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

   >[!NOTE]
   >
   > に追加する必要はありません [Content Hub製品プロファイル](#onboard-content-hub-consumer-users) （アセット配布の役割）。



