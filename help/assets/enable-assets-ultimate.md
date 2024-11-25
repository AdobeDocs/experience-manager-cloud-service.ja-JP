---
title: Assets Ultimate の有効化
description: 新規および既存のお客様に対して Assets Ultimate を有効にする方法について説明します。
feature: Asset Management
role: User, Admin
source-git-commit: 16ce83409044ad54140754112eb4d35b97883b44
workflow-type: ht
source-wordcount: '1420'
ht-degree: 100%

---

# [!DNL Assets] as a Cloud Service Ultimate の有効化 {#enable-assets-cloud-service-ultimate}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Asset Cloud Service Ultimate へのアップグレード](/help/assets/assets/upgrade-assets-cs-ultimate-package-banner.png)

Assets as a Cloud Service Ultimate を使用すると、アセット管理とライブラリサービス、セキュリティと権限管理、Creative Cloud と Experience Cloud の接続、UI の拡張性、API 駆動型の自動化、アドビアプリケーションとアドビ以外のアプリケーションとの統合、カスタムコードのデプロイメントなど、様々な主要な DAM 機能を実行できます。完全なリストについては、[Assets as a Cloud Service Ultimate の概要](/help/assets/assets-ultimate-overview.md)を参照してください。

## Assets Ultimate の有効化 {#enable-assets-ultimate}

新規の Assets as a Cloud Service のお客様は、まず Cloud Manager を使用して新しいプログラムを作成し、Assets Ultimate を有効にする必要があります。

次の手順を実行します。

1. システム管理者として、Cloud Manager にログオンします。ログイン時に正しい組織を選択していることを確認します。

   >[!NOTE]
   >
   >新しいプログラムを追加するには、適切な Cloud Manager 製品プロファイルに追加されていることを確認します。詳しくは、[Cloud Manager での役割に基づく権限](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)を参照してください。

1. [新しいプログラムを作成](/help/journey-onboarding/create-program.md)し、それに[環境を追加](/help/journey-onboarding//create-environments.md)します。

   新しいプログラムの作成中に、「**[!UICONTROL ソリューションとアドオン]**」タブで「**[!UICONTROL Assets Ultimate]**」を選択します。また、**[!UICONTROL Assets Ultimate]** を展開し、「**[!UICONTROL コンテンツハブ]**」を選択して、アセット配布用の[コンテンツハブ](/help/assets/product-overview.md)を有効にすることもできます。

   ![AEM Assets Ultimate](assets/aem-assets-ultimate-solutions.png)

1. 「**[!UICONTROL 作成]**」をクリックしてプログラムを作成します。これで、Assets Ultimate が Experience Manager Assets as a Cloud Service で有効になります。

システム管理者は、Assets Ultimate で AEM 管理者としての資格が自動的に付与され、使用可能な製品プロファイルを管理するために Admin Console に移動するためのメールを受信します。

Admin Console 上の AEM as a Cloud Service インスタンスは、次の製品プロファイルで構成されます。

* AEM 管理者

* AEM ユーザー

* [AEM Assets 共同作業者ユーザー](#onboard-collaborator-users)

* [AEM Assets パワーユーザー](#onboard-power-users)

  ![AEM Assets 製品プロファイル](assets/aem-assets-product-profiles.png)

Assets as a Cloud Service 用のコンテンツハブを有効にしている場合は、Admin Console の AEM Assets as a Cloud Service 内に、サフィックスとして `delivery` が付いた新しいインスタンスが作成されます。

![コンテンツハブの新しいインスタンス](assets/new-instance-content-hub.png)

>[!NOTE]
>
>2024年8月14日（PT）より前にコンテンツハブをプロビジョニングした場合、新しいインスタンスはサフィックスとして `contenthub` を付けて作成されます。

コンテンツハブのインスタンス名には、`author` または `publish` がありません。

インスタンス名をクリックすると、`AEM Assets Limited Users` コンテンツハブ製品プロファイルが表示されます。

![コンテンツハブ製品プロファイル](assets/content-hub-product-profile.png)

この製品プロファイルへのユーザーまたはユーザーグループの追加を開始して、コンテンツハブへのアクセス権を付与できます。

>[!NOTE]
>
>2024年8月14日（PT）より前にコンテンツハブをプロビジョニングした場合、コンテンツハブ製品プロファイルには、`delivery` の代わりに、`Limited Users` の後に `contenthub` と表示されます。

## 既存のお客様に対する Assets Ultimate の有効化 {#enable-assets-ultimate-existing-customers}

既存の Assets as a Cloud Service のお客様は、2 つの簡単な手順を実行して Assets Ultimate にアップグレードできます。Cloud Manager で Assets as a Cloud Service プログラムに移動し、Assets Ultimate クレジットの可用性に基づいてプログラムカードでアップグレードステータスを確認できます。Assets Ultimate へのアップグレードに十分なクレジットがある場合は、次の画像に示すように、ステータスが `Assets license upgrade required` と表示されます。

![Assets Ultimate への AEM Assets のアップグレード](assets/aem-assets-upgrade-status-ultimate.png)

既存のお客様が Assets Ultimate の新しいライセンスを購入した場合は、アップグレードステータスが `Assets license upgrade available` と表示されます。

### アップグレードの前提条件 {#prerequisites-assets-upgrade}

すべての環境を最新の AEM as a Cloud Service リリースバージョンまたは最低でも `2024.10.18175` リリースバージョンにアップグレードする必要があります。最小要件を満たしていない場合は、アドビ担当者に連絡して、必要な AEM リリースバージョンに切り替えてください。

### Assets Ultimate にアップグレード {#upgrade-assets-ultimate}

次の手順を実行します。

1. AEM リリースバージョンの最小要件に切り替えた後、プログラム名をクリックします。次の画像に示すように、「**[!UICONTROL 環境]**」セクションのすぐ上にアップグレードカードが表示されます。

   ![Assets Ultimate への AEM Assets のアップグレード](assets/aem-assets-upgrade-card.png)

1. 「**[!UICONTROL 製品プロファイルを追加]**」をクリックします。Cloud Manager には、プログラムで使用可能なすべての環境または個別の環境に新しい製品プロファイルを追加するオプションが表示されます。

   ![AEM Assets アップグレードオプション](assets/aem-assets-upgrade-options.png)

1. 「**[!UICONTROL すべての環境]**」をクリックしてプログラム内のすべての環境に新しい製品プロファイルを追加するか、「**[!UICONTROL 個別の環境]**」をクリックして新しい製品プロファイルを選択した環境に追加します。

   「**[!UICONTROL 個別の環境]**」をクリックすると、プログラムで使用可能なすべての環境のリストが表示されます。

1. 環境に対応するその他のオプションアイコンをクリックし、「**[!UICONTROL 製品プロファイルを追加]**」を選択して、選択した環境に新しい製品プロファイルを追加します。

   ![AEM Assets で個別の環境を選択](assets/aem-assets-individual-environments.png)

   また、「**[!UICONTROL 環境]**」セクションに移動し、環境に対応するその他のオプションアイコンをクリックし、「**[!UICONTROL 製品プロファイルを追加]**」を選択して、選択した環境に製品プロファイルを追加することもできます。

   新しい製品プロファイルが追加されている間は、環境のステータスに `Adding Product Profiles` と表示され、プロセスが完了すると `Running` と表示されます。

   次の手順を実行する前に、プログラムで使用可能なすべての環境に、個別に、またはすべての環境にまとめて製品プロファイルを追加する必要があります。

1. 「**[!UICONTROL アップグレード]**」をクリックします。「**[!UICONTROL アップグレード]**」オプションは、使用可能なすべての環境に製品プロファイルを追加した場合にのみ表示されます。

   ![アップグレードプロセスの最後の手順](assets/aem-assets-upgrade-button.png)

   アップグレードプロセスが完了し、Assets as a Cloud Service が Assets Ultimate に正常にアップグレードされました。プログラムのステータスには `Assets Ultimate` と表示されます。

   ![アップグレード後のプログラムステータス](assets/program-status-post-upgrade.png)

これで、Admin Console 上の AEM as a Cloud Service インスタンスは、次の製品プロファイルで構成されます。

* AEM 管理者

* AEM ユーザー

* [AEM Assets 共同作業者ユーザー](#onboard-collaborator-users)

* [AEM Assets パワーユーザー](#onboard-power-users)

![AEM Assets 製品プロファイル](assets/aem-assets-product-profiles.png)

コンテンツハブを有効にする必要がある場合は、Cloud Manager のプログラム名のその他オプション（…）アイコンをクリックし、「**[!UICONTROL プログラムを編集]**」を選択します。**[!UICONTROL Assets Ultimate]** を展開し、「**[!UICONTROL コンテンツハブ]**」をクリックします。この手順により、Assets Ultimate のコンテンツハブが有効になります。Admin Console の AEM Assets as a Cloud Service 内に、サフィックスとして `delivery` が付いた新しいインスタンスが作成されます。

![コンテンツハブの新しいインスタンス](assets/new-instance-content-hub.png)

>[!NOTE]
>
>2024年8月14日（PT）より前にコンテンツハブをプロビジョニングした場合、新しいインスタンスはサフィックスとして `contenthub` を付けて作成されます。

コンテンツハブのインスタンス名には、`author` または `publish` がありません。

インスタンス名をクリックすると、`AEM Assets Limited Users` コンテンツハブ製品プロファイルが表示されます。

![コンテンツハブ製品プロファイル](assets/content-hub-product-profile.png)

この製品プロファイルへのユーザーまたはユーザーグループの追加を開始して、コンテンツハブへのアクセス権を付与できます。

>[!NOTE]
>
>2024年8月14日（PT）より前にコンテンツハブをプロビジョニングした場合、コンテンツハブ製品プロファイルには、`delivery` ではなく、`Limited Users` の後に `contenthub` が表示されます。

## AEM Assets 共同作業者ユーザーのオンボード {#onboard-collaborator-users}

AEM Assets 共同作業者ユーザーは、他のアドビ製品やアドビ以外のアプリケーションで組織が使用できる Assets の統合を通じて Experience Manager のアセットを操作することや、組み込みの Adobe Express および Firefly を使用してプロフェッショナルがデザインしたテンプレート、ブランドキット、Adobe Stock アセットなどを活用したアセットを作成および編集することや、AEM Assets コンテンツハブポータルを使用して組織の承認済みアセットにアクセスして活用できます。

共同作業者ユーザーをオンボードするには：

1. Admin Console の製品のリストで AEM as a Cloud Service 製品名をクリックして、Experience Manager Assets 製品プロファイルにアクセスします。

1. AEM as a Cloud Service の実稼動オーサーインスタンスをクリックします。
   ![AEM as a Cloud Service の製品プロファイル](assets/aem-cloud-service-instances.png)

1. 共同作業者ユーザーの製品プロファイルをクリックし、「**[!UICONTROL ユーザーを追加]**」をクリックして、製品プロファイルにユーザーまたはユーザーグループを追加します。
   ![ユーザー製品プロファイル](assets/aem-assets-collaborator-user-permissions.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

また、次の画像に示すように、共同作業者ユーザーに割り当てられたサービスにアクセスして表示することもできます。

![共同作業者ユーザー向けサービス](assets/aem-assets-collaborator-users.png)

`Adobe Express` および `AEM Assets Collaborator Users` サービスは、デフォルトで有効になっています。

>[!NOTE]
>
>必要に応じて、切替スイッチをオフ／オンにして使用可能なサービスを有効または無効にすることができますが、アドビでは、製品プロファイルに対して有効になっているデフォルトのサービスを使用することをお勧めします。


## AEM Assets パワーユーザーのオンボード {#onboard-power-users}

AEM Assets パワーユーザーは、アセット、権限、メタデータ、デジタルアセットに関する全体的なガバナンスと自動化の管理を含むすべての AEM Assets 機能にアクセスすることや、他のアドビアプリケーションやアドビ以外のアプリケーションで組織が使用できる Assets の統合を通じて Experience Manager のアセットを操作することや、組み込みの Adobe Express および Firefly を使用してプロフェッショナルがデザインしたテンプレート、ブランドキット、Adobe Stock アセットなどを活用したアセットを作成および編集することや、AEM Assets コンテンツハブポータルを使用して組織の承認済みアセットにアクセスして活用できます。

パワーユーザーをオンボードするには：

1. Admin Console の製品のリストで AEM as a Cloud Service 製品名をクリックして、Experience Manager Assets 製品プロファイルにアクセスします。

1. AEM as a Cloud Service の実稼動オーサーインスタンスをクリックします。
   ![AEM as a Cloud Service の製品プロファイル](assets/aem-cloud-service-instances.png)

1. パワーユーザーの製品プロファイルをクリックし、「**[!UICONTROL ユーザーを追加]**」をクリックして、製品プロファイルにユーザーまたはユーザーグループを追加します。
   ![ユーザー製品プロファイル](assets/aem-assets-power-user-permissions.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

また、次の画像に示すように、パワーユーザーに割り当てられたサービスにアクセスして表示することもできます。

![パワーユーザー向けサービス](assets/aem-assets-power-users.png)

`Adobe Express` および `AEM Assets Power Users` サービスは、デフォルトで有効になっています。

>[!NOTE]
>
>必要に応じて、切替スイッチをオフ／オンにして使用可能なサービスを有効または無効にすることができますが、アドビでは、製品プロファイルに対して有効になっているデフォルトのサービスを使用することをお勧めします。
