---
title: デプロイ [!DNL Content Hub]
description: Content Hubをデプロイしてアクティブ化し、様々なタイプの権限（アセットのアップロード、ユーザーのAdobe Express）を持つユーザーにアクセスを提供する方法と、ユーザーに管理者権限を提供する方法について説明します。
role: Admin
source-git-commit: 7224cca950e61bea298f246245bdb221fd8fa22e
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 3%

---


# コンテンツハブのデプロイ {#deploy-content-hub}

![Content Hubのデプロイ ](assets/deploy-content-hub.png)

Content Hubは、組織やビジネスパートナーがオンブランドのコンテンツにアクセスしやすくするために、Experience Manager Assetsas a Cloud Serviceの一部として利用できます。

Experience Manager Assetsのas a Cloud Serviceで承認済みとマークされたアセットは、Content Hubでアセットを配布することができます。

この記事では、必要に応じた権限のバリエーションなど、Content Hubへのアクセスをユーザーに提供するエンドツーエンドのワークフローを説明します。

Content Hubに対する権限には、次のような種類があります。

* [Content Hub ユーザー ](#onboard-content-hub-users): Content Hub ポータルでブランド承認済みアセットにアクセスします。

* [Content Hub管理者 ](#onboard-content-hub-administrator): ブランド承認済みアセットへのアクセス、Content Hubへのアセットのアップロード、画像を編集するためのAdobe Express統合（Adobe Express権限がある場合）に加えて、Content Hubの [ 設定ユーザーインターフェイス ](/help/assets/configure-content-hub-ui-options.md) にアクセスできます。

* [ アセットを追加する権限を持つContent Hub ユーザー ](#onboard-content-hub-users-add-assets):Content Hub ポータルでブランド承認済みアセットにアクセスできるだけでなく、Content Hubにアセットをアップロード ](/help/assets/upload-brand-approved-assets.md) できます [。

* [ アセットを新しいバリエーションに混在させる権限を持つContent Hub ユーザー ](#onboard-content-hub-users-remix-assets):Content Hub ポータルでブランド承認済みAdobe Expressにアクセスできるだけでなく、[Adobe Express統合 ](/help/assets/edit-images-content-hub.md) （アセット権限がある場合）を利用できます。

* [Experience Manager Assets ユーザー ](#experience-manager-assets-users): Experience Manager Assetsでアセットを承認して、それらのアセットをContent Hubで利用できるようにする機能のas a Cloud Service。

## 手順 1:Cloud Managerを使用してContent Hub for Experience Manager Assetsを有効にする {#enable-content-hub}

Content Hub ポータルにアクセスするには、管理者はまずCloud Managerを使用してContent Hub for Experience Manager Assetsas a Cloud Serviceを有効にする必要があります。 以下の手順を実行します。

1. Cloud Managerにログオンします。 ログイン時に適切な組織を選択していることを確認します。 Cloud Managerにすべてのプログラムが一覧表示されます。

1. Experience Manager Assetsas a Cloud Serviceプログラムに移動し、「その他のオプション」アイコン（...）をクリックして「**[!UICONTROL プログラムを編集]**」を選択します。

   ![Cloud Managerでプログラムを編集 ](assets/edit-program-cloud-manager.png)

1. [!UICONTROL  プログラムを編集 ] ダイアログで、「**[!UICONTROL ソリューションとアドオン]** タブを選択します。

1. 「**[!UICONTROL Assets]**」を展開し、「**[!UICONTROL Content Hub]**」を選択します。
   ![Cloud ManagerでContent Hubを選択 ](assets/edit-program-cloud-manager-content-hub.png)

   >[!NOTE]
   >
   >Content Hubを選択した後 **[!UICONTROL アップデート]** が有効になっていない場合は、プログラムの運用開始設定が指定されていることを確認してください。

1. 「**[!UICONTROL 更新]**」をクリックします。

Content HubがExperience Manager Assetsas a Cloud Serviceに対して有効になりました。

>[!NOTE]
>
>最大 250 人のContent Hub ユーザーがContent Hubにアクセスして使用できます。 その他の質問がある場合は、Adobeの担当者にお問い合わせください。


Experience Manager Assetsを初めて使用する場合は、「**[!UICONTROL プログラムを追加]**」をクリックし、プログラムの詳細（プログラム名、実稼動用に設定）を入力して、「**[!UICONTROL 続行]**」をクリックします。 その後、「{ ソリューションとアドオン ]**」タブで]** 0}Assets **[!UICONTROL と]** 2}Content Hub} を選択できます。**[!UICONTROL **[!UICONTROL 

### Admin Console時のContent Hub インスタンスと製品プロファイル{#content-hub-instance-product-profile}

[Cloud Managerを使用してAssetsas a Cloud Service用にContent Hubを有効にする ](#enable-content-hub) を行うと、Admin Console時にAEM Assetsas a Cloud Service内に新しいインスタンスが作成され、サフィックスに `contenthub` が付きます。

![Content Hubの新しいインスタンス ](assets/new-instance-content-hub.png)

Content Hubのインスタンス名には `author` や `publish` はありません。

インスタンス名をクリックして、Content Hub製品プロファイルを表示します。

![Content Hub製品プロファイル ](assets/content-hub-product-profile.png)

## 手順 2:Content Hub管理者をオンボーディングする {#onboard-content-hub-administrator}

Content Hub管理者は、ブランド承認済みアセットへのアクセス、Content Hubへのアセットのアップロード、画像を編集するAdobe Express統合に加えて、Content Hubの [ 設定ユーザーインターフェイス ](/help/assets/configure-content-hub-ui-options.md) にアクセスできます（Adobe Expressの使用権限がある場合）。

Content Hub管理者をオンボーディングするには：

1. [Content Hub ユーザー製品プロファイルにアクセスしてクリックします ](#content-hub-instance-product-profile)。

1. 「**[!UICONTROL ユーザーを追加]**」をクリックして、ユーザーまたはユーザーグループを製品プロファイルに追加します。

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

1. Content Hub製品プロファイルにユーザーを追加した後、Admin Console上の製品のリストでExperience Manager Assets製品名をクリックして、AEM as a Cloud Service製品プロファイルにアクセスします。

1. AEM as a Cloud Service用の実稼動オーサーインスタンスをクリックします。
   ![AEM as a Cloud Serviceの製品プロファイル ](assets/aem-cloud-service-instances.png)

   Admin Consoleには、AEM as a Cloud Service用の 2 つの製品プロファイル（Administrators と Users）が表示されます。
1. 管理者製品プロファイルをクリックし、**[!UICONTROL ユーザーを追加]** をクリックして、ユーザーを製品プロファイルに追加します。
   ![ 管理者製品プロファイル ](assets/aem-cs-admin-product-profile.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

## 手順 3:Content Hub ユーザーのオンボーディング {#onboard-content-hub-users}

Content Hub ユーザーは、ポータルで使用可能なアセットにアクセスできますが、新しいアセットを追加したり、既存のアセットを変更したりすることはできません。

Content Hub ユーザーをオンボーディングするには：

1. [Content Hub ユーザー製品プロファイルにアクセスしてクリックします ](#content-hub-instance-product-profile)。

1. 「**[!UICONTROL ユーザーを追加]**」をクリックして、ユーザーまたはユーザーグループを製品プロファイルに追加します。

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

これで、これらのユーザーは、Content Hub ポータルで使用可能なアセットにアクセスできます。

>[!NOTE]
>
>外部 ID プロバイダーとの同期など、高度なエンタープライズ機能をすべて使用できます。

### Content Hubへのアクセス方法 {#access-content-hub}

Content Hubには、次の方法でアクセスできます。

* 次のリンクを使用してContent Hubにアクセスします。

  `https://experience.adobe.com/#/assets/contenthub`

* `experience.adobe com` にログオンし、「**[!UICONTROL クイックアクセス]**」セクションの {1 ]**Experience Manager Assets Content Hub} をクリックします。**[!UICONTROL 
  ![Content Hub アクセス ](assets/access-content-hub.png)

* `experience.adobe com` にログオンし、製品スイッチャーで使用可能な **[!UICONTROL Experience Manager Assets Content Hub]** をクリックします。
  ![Content Hub アクセス メソッド 3](assets/access-content-hub-alternate.png)

### ユーザーへのメール通知を無効にする {#disable-email-notifications}

管理者が、ユーザーがContent Hub製品プロファイルに追加されたときに送信されるメール通知を無効にする必要がある場合：

製品プロファイル名の横にある検索アイコンをクリックし、「**[!UICONTROL メールでユーザーに通知]**」トグルを無効にします。

![ メール通知を無効にする ](assets/disable-email-notifications.png)


## 手順 4：アセットを追加する権限を持つContent Hub ユーザーをオンボーディングする（オプション） {#onboard-content-hub-users-add-assets}

アセットを追加する権限を持つContent Hub ユーザーは、[ ブランドが承認した新しいアセットをContent Hubにアップロード ](/help/assets/upload-brand-approved-assets.md) できます。

ユーザーを追加する権限でContent Hub ユーザーをオンボーディングするには：

1. [Content Hub製品プロファイルにユーザーを追加した後 ](#onboard-content-hub-users)、Admin Consoleされている製品のリストでAEM as a Cloud Service製品名をクリックして、Experience Manager Assets製品プロファイルにアクセスします。

1. AEM as a Cloud Service用の実稼動オーサーインスタンスをクリックします。
   ![AEM as a Cloud Serviceの製品プロファイル ](assets/aem-cloud-service-instances.png)

   Admin Consoleには、AEM as a Cloud Service用の 2 つの製品プロファイル（Administrators と Users）が表示されます。
1. ユーザー製品プロファイルをクリックし、「**[!UICONTROL ユーザーを追加]**」をクリックして、ユーザーを製品プロファイルに追加します。
   ![ ユーザー製品プロファイル ](assets/aem-cs-user-product-profile.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

## 手順 4：アセットを新しいバリエーションに混在させる権限を持つContent Hub ユーザーをオンボーディングする（オプション） {#onboard-content-hub-users-remix-assets}

アセットを新しいバリエーションにリミックスする権限を持つContent Hub ユーザーは、[Adobe Expressを使用して既存のアセットを変更し、アセットをリポジトリに保存 ](/help/assets/edit-images-content-hub.md) できます。 Adobe Expressを使用したアセットの編集は、ユーザーがAdobe Express権限を持っている場合にのみ使用できます。

アセットを新しいバリエーションに混在させる権限を持つContent Hub ユーザーをオンボーディングするには：

1. [Content Hub製品プロファイルにユーザーを追加した後 ](#onboard-content-hub-users)、Admin Consoleされている製品のリストでAEM as a Cloud Service製品名をクリックして、Experience Manager Assets製品プロファイルにアクセスします。

1. AEM as a Cloud Service用の実稼動オーサーインスタンスをクリックします。
   ![AEM as a Cloud Serviceの製品プロファイル ](assets/aem-cloud-service-instances.png)

   Admin Consoleには、AEM as a Cloud Service用の 2 つの製品プロファイル（Administrators と Users）が表示されます。
1. ユーザー製品プロファイルをクリックし、「**[!UICONTROL ユーザーを追加]**」をクリックして、ユーザーを製品プロファイルに追加します。
   ![ ユーザー製品プロファイル ](assets/aem-cs-user-product-profile.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

## Experience Manager Assets ユーザー {#experience-manager-assets-users}

Experience Manager Assets ユーザーは、Content Hubで使用できるように、AEM as a Cloud Service上のアセットを承認できます。

Experience Manager Assets ユーザーを設定するには：

1. Admin Console時の製品のリストでExperience Manager Assets製品名をクリックして、AEM as a Cloud Service製品プロファイルにアクセスします。

1. AEM as a Cloud Service用の実稼動オーサーインスタンスをクリックします。
   ![AEM as a Cloud Serviceの製品プロファイル ](assets/aem-cloud-service-instances.png)

   Admin Consoleには、AEM as a Cloud Service用の 2 つの製品プロファイル（Administrators と Users）が表示されます。
1. ユーザー製品プロファイルをクリックし、「**[!UICONTROL ユーザーを追加]**」をクリックして、ユーザーを製品プロファイルに追加します。
   ![ ユーザー製品プロファイル ](assets/aem-cs-user-product-profile.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

   >[!NOTE]
   >
   > Experience Manager Assets ユーザーの場合、[Content Hub製品プロファイル ](#onboard-content-hub-users) に追加される必要はありません。



