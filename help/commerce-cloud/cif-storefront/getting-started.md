---
title: AEM Commerce as a Cloud Service の基本を学ぶ
description: Cloud Manager、CI/CD パイプラインおよび Venia 参照用ストアフロントを使用して、Adobe Experience Manager(AEM) コマースプロジェクトをデプロイする方法について説明します。
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Experience Manager as a Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 89%

---


# AEM Commerce as a Cloud Service の基本を学ぶ {#start}

AEM Commerce as a Cloud Service の使用を開始するには、Experience Manager Cloud Service が Commerce Integration Framework（CIF）アドオンによりプロビジョニングされている必要があります。CIF アドオンは、[AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md) 上の追加モジュールです。

>[!TIP]
>
>**Edge Delivery Servicesを検討しましたか？**
>
>Edge Delivery Servicesは、ストアフロントを作成するための、Adobeが推奨するソリューションです。 詳しくは、ドキュメント [&#x200B; 概要 &#x200B;](/help/commerce-cloud/introduction.md) を参照してください。

## オンボーディング {#onboarding}

AEM Commerce as a Cloud Service のオンボーディングは、次の 2 つの手順で構成されます。

1. AEM Commerce as a Cloud Service を有効にし、CIF アドオンをプロビジョニングする
1. AEM Commerce as a Cloud Service をコマースソリューションに接続する

最初のオンボーディング手順はアドビが行います。価格とプロビジョニングの詳細については、セールス担当者にお問い合わせください。

CIF アドオンのプロビジョニングが完了すると、既存の Cloud Manager プログラムに適用されます。Cloud Manager プログラムがない場合は、作成する必要があります。詳しくは、[&#x200B; プログラムの設定 &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/program-setup.html?lang=ja) を参照してください。

2 つ目の手順は、各 AEM as a Cloud Service 環境のセルフサービスです。CIF アドオンの初期プロビジョニングの後で、いくつかの追加の設定を行う必要があります。

## AEM とコマースソリューションの接続 {#solution}

CIF アドオンと [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)をコマースソリューションに接続するには、Cloud Manager の環境変数で GraphQL エンドポイント URL を指定する必要があります。変数名は `COMMERCE_ENDPOINT` です。HTTPS を介した安全な接続を設定する必要があります。

この環境変数は、次の 2 つの場所で使用されます。

* AEM CIF コアコンポーネントと顧客プロジェクトコンポーネントで使用される、共有可能な共通の GraphQl クライアントを介した、AEM からコマースバックエンドへの GraphQL 呼び出し。
* `/api/graphql` で変数が使用可能に設定された各 AEM 環境への GraphQL プロキシ URL の設定。この URL は、AEM Commerce オーサリングツール（CIF アドオン）および CIF クライアントサイドコンポーネントで使用されます。

AEM as a Cloud Service 環境ごとに異なる GraphQL エンドポイント URL を使用できます。この方法で、プロジェクトは AEM ステージング環境をコマースステージングシステムに、また、AEM 本番環境をコマース実稼働システムに接続できます。GraphQL エンドポイントは、公開されている必要があります。プライベート VPN またはローカル接続はサポートされていません。オプションで、認証が必要な追加の CIF 機能を使用するために認証ヘッダーを指定できます。

Adobe Commerce Enterprise／Cloud の場合のみ、CIF アドオンはオプションで AEM 作成者向けのステージング済みカタログデータの使用をサポートします。このデータを使用するには、認証ヘッダーを設定する必要があります。このヘッダーは、セキュリティ上の理由から、AEM オーサーインスタンスでのみ使用できます。AEM パブリッシュインスタンスでは、ステージング済みデータを表示できません。

エンドポイントを設定する方法は 2 つあります。

### Cloud Manager ユーザーインターフェイスを使用（デフォルト） {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/343272?captions=jpn&quality=12&learn=on)

この設定は、環境の詳細ページのダイアログボックスを使用して行うことができます。コマース対応プログラムでこのページを表示すると、エンドポイントが設定されていない場合は、ボタンが表示されます。

![CM 環境情報](/help/commerce-cloud/cif-storefront/assets/commerce-cmui.png)

このボタンをクリックすると、次のダイアログボックスが開きます。

![CM コマースエンドポイント](/help/commerce-cloud/cif-storefront/assets/commerce-cm-endpoint.png)

エンドポイント（オプションで、ステージング済みカタログのサポートの認証ヘッダー）が設定されると、エンドポイントが詳細ページに表示されます。編集アイコンをクリックすると同じダイアログボックスが開き、必要に応じてエンドポイントを編集できます。

![CM 環境情報](/help/commerce-cloud/cif-storefront/assets/commerce-cmui-done.png)

### Adobe I/O CLI を使用  {#adobe-cli}

Adobe I/O CLI を使用して AEM をコマースソリューションに接続するには、次の手順に従います。

1. Cloud Manager プラグインとAdobe I/O CLI を取得します。

   * [Adobe CLI プラグインで &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=ja)2&rbrace;Cloud Manager CLI&rbrace; をダウンロード、設定、使用する方法については [&#128279;](https://github.com/adobe/aio-cli)Adobe I/O Cloud Managerのドキュメント [&#x200B; を参照してください。](https://github.com/adobe/aio-cli-plugin-cloudmanager)

1. Adobe I/O CLI をAEM as a Cloud Service プログラムで認証します。

1. Cloud Managerで `COMMERCE_ENDPOINT` 変数を設定します。

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   * 詳細は、 [CLI ドキュメント](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) を参照してください。

   * コマース GraphQL エンドポイント URL は、コマースの GraphQL サービスを指し、安全な HTTPS 接続を使用する必要があります。例：`https://<yourcommercesystem>/graphql`

1. 認証を必要とするステージング済みカタログ機能を有効にします（オプション）。

   >[!NOTE]
   >
   >この機能は、Adobe Commerce Enterprise または Cloud Edition でのみ使用できます。詳しくは、[トークンベースの認証](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens)を参照してください。

   * Cloud Manager でシークレット変数 `COMMERCE_AUTH_HEADER` を設定します。

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>次のコマンドを使用して、すべての Cloud Manager 変数を一覧表示して再確認できます。 `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

これで、AEM Commerce as a Cloud Service を使用する準備が整い、Cloud Manager を介してプロジェクトをデプロイできます。

## ストアとカタログの設定 {#catalog}

CIF アドオンと [CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、異なるコマースストア（またはストア表示など）に接続された複数の AEM サイト構造で使用できます。デフォルトでは、CIF アドオンは、Adobe Commerce のデフォルトストアとカタログに接続するデフォルト設定でデプロイされます。

この設定は、次の手順に従って、CIF Cloud Service 設定を使用してプロジェクトに合わせて調整できます。

1. AEM で、ツール／Cloud Services／CIF 設定に移動します。

1. 変更するコマース設定を選択します。

1. アクションバーから設定プロパティを開きます。

![CIF Cloud Services の設定](/help/commerce-cloud/cif-storefront/assets/cif-cloud-service-config.png)

次のプロパティを設定できます。

* GraphQL クライアント - コマースバックエンド通信用に設定済みの GraphQL クライアントを選択します。このクライアントは通常、デフォルトのままです。
* ストア表示 - ストア表示の識別子。空の場合は、デフォルトのストア表示が使用されます。
* GraphQL プロキシパス - AEM の GraphQL プロキシが、コマースバックエンドの GraphQL エンドポイントへのリクエストをプロキシするために使用する URL パス。

  >[!NOTE]
  >
  > ほとんどの設定で、デフォルト値 `/api/graphql` は変更できません。この設定を変更するのは、指定された GraphQL プロキシを使用しない高度な設定でのみです。

* カタログ UID のサポートを有効にする - コマースバックエンドの GraphQL 呼び出しで、ID ではなく UID のサポートを有効にします。

  >[!NOTE]
  >
  > UID のサポートは、Adobe Commerce 2.4.2 で導入されました。コマースバックエンドがバージョン 2.4.2 以降の GraphQL スキーマをサポートしている場合にのみ有効にします。

* カタログのルートカテゴリ識別子 - ストアカタログルートの識別子（UID または ID）

  >[!CAUTION]
  >
  > CIF コアコンポーネントバージョン 2.0.0 以降では、`id` のサポートが削除されて `uid` に置き換えられました。プロジェクトで CIF コアコンポーネントバージョン 2.0.0 を使用している場合は、カタログ UID のサポートを有効にし、有効なカテゴリ UID を「カタログルートカテゴリ識別子」として使用する必要があります。

上記の設定は参照用です。プロジェクトは、独自の設定を行う必要があります。

複数の AEM サイト構造を異なるコマースカタログと組み合わせて使用する、より複雑な設定については、チュートリアル「[コマースマルチストアの設定](/help/commerce-cloud/cif-storefront/configuring/multi-store-setup.md)」を参照してください。

## その他のリソース {#additional-resources}

* [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
* [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
* [コマースマルチストアの設定](/help/commerce-cloud/cif-storefront/configuring/multi-store-setup.md)
* [複数のコマースシステムの設定](/help/commerce-cloud/cif-storefront/configuring/multiple-commerce-systems-setup.md)
