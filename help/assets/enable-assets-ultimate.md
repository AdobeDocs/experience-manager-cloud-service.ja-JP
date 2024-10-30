---
title: Assets Ultimate の有効化
description: 新規および既存のお客様がAssets Ultimate を有効にする方法を説明します。
feature: Asset Management
role: User, Admin
source-git-commit: 16ce83409044ad54140754112eb4d35b97883b44
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 3%

---

# as a Cloud Service Enable [!DNL Assets] Ultimate {#enable-assets-cloud-service-ultimate}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Asset Cloud Service Ultimate へのアップグレード ](/help/assets/assets/upgrade-assets-cs-ultimate-package-banner.png)

Assets as a Cloud Service Ultimate enables you to perform various key DAM capabilities, such as, asset management and library services, security and rights management, Creative and Experience Cloud connections, UI extensibility, API-driven automation, integrations with Adobe and non-Adobe applications, custom code deployment and many more. [](/help/assets/assets-ultimate-overview.md)

## Enable Assets Ultimate {#enable-assets-ultimate}

New Assets as a Cloud Service customers must first enable Assets Ultimate by creating a new program using Cloud Manager.

次の手順を実行します。

1. As a system administrator, log on to Cloud Manager. Ensure that you select the right organization while logging in.

   >[!NOTE]
   >
   >Ensure that you are added to the appropriate Cloud Manager product profile to add a new program. [](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)

1. [](/help/journey-onboarding/create-program.md)[](/help/journey-onboarding//create-environments.md)

   ****************[](/help/assets/product-overview.md)

   ![](assets/aem-assets-ultimate-solutions.png)

1. **[!UICONTROL 作成]** をクリックして、プログラムを作成します。 Assets Ultimate がExperience Manager Assetsas a Cloud Serviceに対して有効になりました。

システム管理者は、Assets Ultimate 上のAEM管理者として自動的に権限が付与され、利用可能な製品プロファイルを管理するためのAdmin Consoleに移動するためのメールが届きます。

Admin Console上のAEM as a Cloud Service インスタンスは、次の製品プロファイルで構成されます。

* AEM管理者

* AEM ユーザー

* [AEM Assets Collaborator Users](#onboard-collaborator-users)

* [AEM Assets パワーユーザー](#onboard-power-users)

  ![AEM Assets製品プロファイル ](assets/aem-assets-product-profiles.png)

Assetsのas a Cloud ServiceのContent Hubを有効にした場合は、Admin Console時にAEM Assetsのas a Cloud Service内に新しいインスタンスが作成され、サフィックスに `delivery` が付きます。

![Content Hubの新しいインスタンス ](assets/new-instance-content-hub.png)

>[!NOTE]
>
>2024 年 8 月 14 日（PT）より前にContent Hubをプロビジョニングしている場合、新しいインスタンスは `contenthub` をサフィックスとして使用して作成されます。

`author``publish`

`AEM Assets Limited Users`

![Content Hub製品プロファイル ](assets/content-hub-product-profile.png)

この製品プロファイルにユーザーまたはユーザーグループを追加して、Content Hubへのアクセス権を付与できます。

>[!NOTE]
>
>2024 年 8 月 14 日（PT）より前にContent Hubをプロビジョニングしている場合、Content Hub製品プロファイルには `delivery` ではなく `Limited Users` の後に記載さ `contenthub` ています。

## Enable Assets Ultimate for existing customers {#enable-assets-ultimate-existing-customers}

Existing Assets as a Cloud Service customers can upgrade to Assets Ultimate by executing two simple steps. You can navigate to the Assets as a Cloud Service program in Cloud Manager and see upgrade status on the Program card based on the availability of Assets Ultimate credits. `Assets license upgrade required`

![](assets/aem-assets-upgrade-status-ultimate.png)

`Assets license upgrade available`

### Prerequisites for upgrade {#prerequisites-assets-upgrade}

すべての環境を、最新のAEM as a Cloud Service リリースバージョンまたは最小の `2024.10.18175` リリースバージョンにアップグレードする必要があります。 最小要件を満たしていない場合は、Adobe担当者に連絡して、必要なAEM リリースバージョンに切り替えてください。

### Assets Ultimate にアップグレード {#upgrade-assets-ultimate}

次の手順を実行します。

1. AEM リリースバージョンの最小要件に切り替えたら、プログラム名をクリックします。 次の画像に示すように、「**[!UICONTROL 環境]**」セクションのすぐ上にアップグレードカードが表示されます。

   ![Assets Ultimate へのAEM Assetsのアップグレード ](assets/aem-assets-upgrade-card.png)

1. **** Cloud Manager displays options to add new product profiles to all environments available in the program or individual environments.

   ![](assets/aem-assets-upgrade-options.png)

1. ********

   ****

1. ****

   ![](assets/aem-assets-individual-environments.png)

   ********

   `Adding Product Profiles``Running`

   You must add product profiles to all environments available in the program, individually or all environments together, before executing the next step.

1. ****「**[!UICONTROL アップグレード]**」オプションは、使用可能なすべての環境に製品プロファイルを追加した場合にのみ表示されます。

   ![ アップグレードプロセスの最後の手順 ](assets/aem-assets-upgrade-button.png)

   アップグレードプロセスが完了し、Assetsas a Cloud ServiceをAssets Ultimate に正常にアップグレードしました。 プログラムのステータスが「`Assets Ultimate`」と表示されます。

   ![ アップグレード後のプログラムステータス ](assets/program-status-post-upgrade.png)

Your AEM as a Cloud Service instance on Admin Console now comprises the following product profiles:

* AEM管理者

* AEM ユーザー

* [AEM Assets Collaborator Users](#onboard-collaborator-users)

* [AEM Assets パワーユーザー](#onboard-power-users)

![AEM Assets製品プロファイル ](assets/aem-assets-product-profiles.png)

Content Hubを有効にする必要がある場合は、Cloud Managerのプログラム名にある詳細オプション （...）アイコンをクリックし、「**[!UICONTROL プログラムを編集]**」を選択します。 ******** This step enables the Content Hub for Assets Ultimate. `delivery`

![](assets/new-instance-content-hub.png)

>[!NOTE]
>
>`contenthub`

`author``publish`

`AEM Assets Limited Users`

![](assets/content-hub-product-profile.png)

You can start adding users or user groups to this product profile to provide them access to Content Hub.

>[!NOTE]
>
>`contenthub``Limited Users``delivery`

## Onboard AEM Assets Collaborator users {#onboard-collaborator-users}

AEM Assets Collaborator users can work with assets from Experience manager via integrations of Assets available to your organization in other Adobe products and non-Adobe applications, create and edit assets using built-in Adobe Express and Firefly leveraging professionally designed templates, brand kits, Adobe Stock assets, and so on, and access and leverage approved assets from your organization using AEM Assets Content Hub portal.

Collaborator ユーザーをオンボードするには、次の手順に従います。

1. Admin Console時の製品のリストでExperience Manager Assets製品名をクリックして、AEM as a Cloud Service製品プロファイルにアクセスします。

1. AEM as a Cloud Service用の実稼動オーサーインスタンスをクリックします。
   ![AEM as a Cloud Serviceの製品プロファイル ](assets/aem-cloud-service-instances.png)

1. 「共同作業者ユーザー」製品プロファイルをクリックし、「**[!UICONTROL ユーザーを追加]**」をクリックして、製品プロファイルにユーザーまたはユーザーグループを追加します。
   ![](assets/aem-assets-collaborator-user-permissions.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

次の図に示すように、コラボレータ・ユーザーに割り当てられたサービスにアクセスして表示することもできます。

![ コラボレータ・ユーザー向けサービス ](assets/aem-assets-collaborator-users.png)

`Adobe Express` サービスと `AEM Assets Collaborator Users` サービスは、デフォルトで有効になっています。

>[!NOTE]
>
>必要に応じて、切り替えのオンとオフを切り替えて、使用可能なサービスを有効または無効にすることができますが、Adobeでは、製品プロファイルに対して有効になっているデフォルトのサービスを使用することをお勧めします。


## Onboard AEM Assets Power users {#onboard-power-users}

AEM Assets Power users can access all AEM Assets capabilities including managing assets, permissions, metadata and the overall governance and automation around digital assets, work with assets from Experience manager via integrations of Assets available to your organization in other Adobe and non-Adobe applications, create and edit assets using built-in Adobe Express and Firefly leveraging professionally designed templates, brand kits, Adobe Stock assets, and so on, and access and leverage approved assets from your organization using AEM Assets Content Hub portal.

To onboard Power users:

1. Admin Console時の製品のリストでExperience Manager Assets製品名をクリックして、AEM as a Cloud Service製品プロファイルにアクセスします。

1. AEM as a Cloud Service用の実稼動オーサーインスタンスをクリックします。
   ![AEM as a Cloud Serviceの製品プロファイル ](assets/aem-cloud-service-instances.png)

1. ****
   ![ ユーザー製品プロファイル ](assets/aem-assets-power-user-permissions.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

また、次の図に示すように、パワーユーザーに割り当てられたサービスにアクセスして表示することもできます。

![ パワーユーザー向けサービス ](assets/aem-assets-power-users.png)

`Adobe Express` サービスと `AEM Assets Power Users` サービスは、デフォルトで有効になっています。

>[!NOTE]
>
>必要に応じて、切り替えのオンとオフを切り替えて、使用可能なサービスを有効または無効にすることができますが、Adobeでは、製品プロファイルに対して有効になっているデフォルトのサービスを使用することをお勧めします。
