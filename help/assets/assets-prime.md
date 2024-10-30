---
title: Assets Prime
description: 主なメリット、ユーザータイプ、権限など、Assets Prime の主な側面について説明します。
feature: Asset Management
role: User, Admin
source-git-commit: f033efd954ea7f9d27a891bfb9c0226e9d9c1432
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 3%

---

# [!DNL Assets]as a Cloud Service素数  {#assets-prime}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![AEM Assets Prime のバナー画像 ](/help/assets/assets/aem-assets-prime-package-banner.png)

Assetsas a Cloud Serviceプライムには、次のような様々な主要機能を実行できる軽量の DAM が含まれています。

* **アセット管理およびライブラリサービス**&#x200B;：ユーザーが一元的なリポジトリでブランドのデジタルアセットを取り込み、保存、カタログ化、制御、管理、制御できるツールです

* **検索、検出、Collaboration**：豊富なカスタマーエクスペリエンスを実現するために必要なアセットを参照、検出、共有、共同作業できるツールです。

* **セキュリティとRights Management**：コンプライアンス、一貫性、ブランドの整合性を確保するためのアクセス、権限、権限、セキュリティを管理するツールです。

* **Creative Cloud連携**: マーケティングチームやクリエイティブチームがデジタルアセットの更新や最終決定を行う際に、シンプルなアクセス、コメント、レビュー、注釈で共同作業できるようにするツールです。

* **Experience Cloud接続**：他のExperience Cloudアプリケーションおよびサービスからのデジタルアセットへのネイティブアクセスをサポートするツールです。

* **拡張オプションのない配布ポータルエクスペリエンス（Content Hub）**：拡張された関係者に対してブランドの承認済みデジタルアセットへのアクセスを拡張して、使用状況とブランドの一貫性を確保するツール。

* **Adobe**：他の統合アプリケーションおよびAdobe以外のアプリケーションとの統合。

* **Dynamic Media（アドオン）**：画像、ビデオ、その他の新しいコンテンツを変換して配信するツールで、あらゆるデバイス向けのリッチでインタラクティブなマルチメディアエクスペリエンスを大規模に実現します。

ただし、DAM ニーズが拡大し、UI 拡張機能、API 駆動自動化、カスタムコードのデプロイメントなど、より多くの機能が必要になると、[Assets Ultimate](/help/assets/assets-ultimate-overview.md) へのアップグレードを検討する必要があります。

この記事では、Assetsas a Cloud Serviceプライムを有効にするためのエンドツーエンドのワークフローについて説明します。

## Assetsas a Cloud Serviceプライムの有効化{#enable-assets-prime}

Cloud Managerを使用して新しいプログラムを作成する際に、Assets Prime を有効にします。 次の手順を実行します。

1. システム管理者として、Cloud Managerにログオンします。 ログイン時に適切な組織を選択していることを確認します。

   >[!NOTE]
   >
   >新しいプログラムを追加するには、適切なCloud Manager製品プロファイルに追加されていることを確認します。 詳しくは、[Cloud Managerでの役割ベースの権限 ](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) を参照してください。

1. [ 新しいプログラムを作成します ](/help/journey-onboarding/create-program.md)。

   新しいプログラムを作成する際に、「**[!UICONTROL ソリューションとアドオン]**」タブで「**[!UICONTROL Assets Prime]**」を選択します。 また、**[!UICONTROL Assets Prime を展開し]****[!UICONTROL Content Hub} を選択して]** アセット配布に対して [Content Hub](/help/assets/product-overview.md) を有効にすることもできます。

   ![AEM Assets Ultimate](assets/aem-assets-prime.png)


1. **[!UICONTROL 作成]** をクリックして、プログラムを作成します。

1. プログラムカードをクリックし、「**[!UICONTROL 環境を追加]**」をクリックします。

1. 環境名を指定し、地域を定義して、「**[!UICONTROL 保存]**」をクリックして環境を作成します。

   ![Assets Prime への環境の追加 ](assets/aem-assets-prime-add-environment.png)

>[!NOTE]
>
>Assets Prime では、実稼動環境のみを作成できます。 実稼動環境が正常に作成されると、環境を追加するオプションは使用できなくなります。

Assets Prime がExperience Manager Assetsas a Cloud Serviceに対して有効になりました。

![AEM Assetsプライムは使用できます ](assets/aem-assets-prime-setup-complete.png)

システム管理者はAEM管理者として自動的に権限が付与され、製品プロファイルを管理するためのAdmin Consoleに移動するためのメールが届きます。


Admin Console上のAEM as a Cloud Service インスタンスは、次の製品プロファイルで構成されます。

* AEM管理者

* AEM ユーザー

* [AEM Assets Collaborator Users](#onboard-collaborator-users)

* [AEM Assets パワーユーザー](#onboard-power-users)


![AEM Assets製品プロファイル ](assets/aem-assets-product-profiles.png)

ユーザーまたはユーザーグループのAEM Assets Collaborator Users およびAEM Assets Power Users 製品プロファイルへの追加を開始できます。 詳しくは、[AEM Assets Collaborator ユーザーのオンボーディング ](#onboard-collaborator-users) および [AEM Assets Power ユーザーのオンボーディング ](#onboard-power-users) を参照してください。

Assetsのas a Cloud ServiceのContent Hubを有効にした場合は、Admin Console時にAEM Assetsのas a Cloud Service内に新しいインスタンスが作成され、サフィックスに `delivery` が付きます。

![Content Hubの新しいインスタンス ](assets/new-instance-content-hub.png)

>[!NOTE]
>
>2024 年 8 月 14 日（PT）より前にContent Hubをプロビジョニングしている場合、新しいインスタンスは `contenthub` をサフィックスとして使用して作成されます。

Content Hubのインスタンス名には `author` や `publish` はありません。

インスタンス名をクリックして、`AEM Assets Limited Users` Content Hub製品プロファイルを表示します。

![Content Hub製品プロファイル ](assets/content-hub-product-profile.png)

この製品プロファイルにユーザーまたはユーザーグループを追加して、Content Hubへのアクセス権を付与できます。

>[!NOTE]
>
>2024 年 8 月 14 日（PT）より前にContent Hubをプロビジョニングしている場合、Content Hub製品プロファイルには `delivery` ではなく `Limited Users` の後に記載さ `contenthub` ています。

## AEM Assets Collaborator ユーザーのオンボーディング {#onboard-collaborator-users}

AEM Assets Collaborator ユーザーは、他のAdobeAdobeや非製品アプリケーションで使用可能なAssetsを統合して Experience Manager のアセットを操作したり、プロフェッショナルが設計したテンプレート、ブランドキット、Adobe Stock アセットなどを活用した組み込みのAdobe ExpressとFireflyを使用してアセットを作成および編集したり、AEM Assets Content Hub ポータルを使用して承認済みアセットにアクセスおよび活用したりできます。

Collaborator ユーザーをオンボードするには、次の手順に従います。

1. Admin Console時の製品のリストでExperience Manager Assets製品名をクリックして、AEM as a Cloud Service製品プロファイルにアクセスします。

1. AEM as a Cloud Service用の実稼動オーサーインスタンスをクリックします。
   ![AEM as a Cloud Serviceの製品プロファイル ](assets/aem-cloud-service-instances.png)

1. 「共同作業者ユーザー」製品プロファイルをクリックし、「**[!UICONTROL ユーザーを追加]**」をクリックして、製品プロファイルにユーザーを追加します。
   ![ ユーザー製品プロファイル ](assets/aem-assets-collaborator-user-permissions.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

次の図に示すように、コラボレータ・ユーザーに割り当てられたサービスにアクセスして表示することもできます。

![ コラボレータ・ユーザー向けサービス ](assets/aem-assets-collaborator-users.png)

`Adobe Express` サービスと `AEM Assets Collaborator Users` サービスは、デフォルトで有効になっています。 必要に応じて、切り替えのオン/オフを切り替えることができますが、Adobeは製品プロファイルに対して有効になっているデフォルトサービスを使用することをお勧めします。

## AEM Assetsのパワーユーザーをオンボードする {#onboard-power-users}

AEM Assets Power ユーザーは、デジタルアセットに関するアセット、権限、メタデータ、全体的なガバナンスと自動化など、すべてのAEM Assets機能にアクセスできます。また、他のAdobeアプリケーションや非Adobeアプリケーションで使用できるAssetsと統合することで、AEM AssetsContent Hubのアセットを操作できます。さらに、専門的に設計されたテンプレート、ブランドキット、Adobe Stock アセットなどを活用した組み込みのAdobe ExpressとFireflyを使用して、アセットを作成および編集できます。

パワー・ユーザーをオンボードするには、次の手順に従います。

1. Admin Console時の製品のリストでExperience Manager Assets製品名をクリックして、AEM as a Cloud Service製品プロファイルにアクセスします。

1. AEM as a Cloud Service用の実稼動オーサーインスタンスをクリックします。
   ![AEM as a Cloud Serviceの製品プロファイル ](assets/aem-cloud-service-instances.png)

1. 「パワーユーザー」製品プロファイルをクリックし、「**[!UICONTROL ユーザーを追加]**」をクリックして、ユーザーを製品プロファイルに追加します。
   ![ ユーザー製品プロファイル ](assets/aem-assets-power-user-permissions.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。

また、次の図に示すように、パワーユーザーに割り当てられたサービスにアクセスして表示することもできます。

![ パワーユーザー向けサービス ](assets/aem-assets-power-users.png)

`Adobe Express` サービスと `AEM Assets Power Users` サービスは、デフォルトで有効になっています。 必要に応じて、切り替えのオン/オフを切り替えることができますが、Adobeは製品プロファイルに対して有効になっているデフォルトサービスを使用することをお勧めします。
