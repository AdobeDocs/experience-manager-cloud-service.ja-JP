---
title: AEM Commerce as a Cloud Service - はじめに
description: Cloud Manager、CI/CD パイプラインおよび Venia 参照用ストアフロントを使用して、Adobe Experience Manager(AEM) コマースプロジェクトをデプロイする方法について説明します。
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 42%

---

# AEM Commerce as a Cloud Service - はじめに {#start}

Adobe Experience Manager(AEM)Commerceas a Cloud Serviceの使用を開始するには、Experience Manager Cloud ServiceにCommerce integration framework(CIF) アドオンがプロビジョニングされている必要があります。 CIFアドオンは、 [AEM Sitesas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/home.html).

## オンボーディング {#onboarding}

AEM Commerce as a Cloud Service のオンボーディングは、次の 2 つの手順で構成されます。

1. AEM Commerce as a Cloud Service を有効にし、CIF アドオンをプロビジョニングする
2. AEM Commerce as a Cloud Service をコマースソリューションに接続する

最初のオンボーディング手順はアドビが行います。価格とプロビジョニングの詳細については、セールス担当者にお問い合わせください。

CIFアドオンのプロビジョニングが完了すると、既存の Cloud Manager プログラムに適用されます。 Cloud Manager プログラムがない場合は、作成する必要があります。 詳しくは、 [プログラムの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/program-setup.html?lang=ja).

2 つ目の手順は、各 AEM as a Cloud Service 環境のセルフサービスです。CIFアドオンの初期プロビジョニング後に、いくつかの追加の設定をおこなう必要があります。

## AEM とコマースソリューションの接続 {#solution}

CIFアドオンと [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components) コマースソリューションでは、Cloud Manager 環境変数を使用してGraphQLエンドポイントの URL を指定する必要があります。 変数名は `COMMERCE_ENDPOINT` です。HTTPS を介した安全な接続を設定する必要があります。

この環境変数は、次の 2 つの場所で使用されます。

- AEM CIFコアコンポーネントおよび顧客プロジェクトコンポーネントで使用される、共有可能な GraphQl クライアントを介して、AEMからコマースバックエンドに対するGraphQL呼び出し。
- 変数が使用可能な各AEM環境でGraphQLプロキシ URL を設定します。 `/api/graphql`. この URL は、AEMコマースオーサリングツール (CIFアドオン ) およびCIFクライアント側コンポーネントで使用されます。

AEM as a Cloud Service 環境ごとに異なる GraphQL エンドポイント URL を使用できます。この方法で、プロジェクトは AEM ステージング環境をコマースステージングシステムに、また、AEM 実稼働環境をコマース実稼働システムに接続できます。GraphQL エンドポイントは、公開されている必要があります。プライベート VPN またはローカル接続はサポートされていません。オプションで、認証を必要とする追加のCIF機能を使用するために認証ヘッダーを提供できます。

オプションで、Adobe Commerce Enterprise/Cloud の場合のみ、CIFアドオンはAEM作成者向けのステージング済みカタログデータの使用をサポートします。 このデータを使用するには、認証ヘッダーを設定する必要があります。 このヘッダーは、セキュリティ上の理由から、AEMオーサーインスタンスでのみ使用および使用できます。 AEMパブリッシュインスタンスは、ステージ済みデータを表示できません。

エンドポイントを設定する方法は 2 つあります。

### Cloud Manager ユーザーインターフェイスを介する（デフォルト） {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

この設定は、環境の詳細ページのダイアログボックスを使用しておこなうことができます。 コマース対応プログラムでこのページを表示すると、エンドポイントが現在設定されていない場合は、ボタンが表示されます。

![CM 環境情報](/help/commerce-cloud/assets/commerce-cmui.png)

このボタンをクリックすると、次のダイアログボックスが開きます。

![CM コマースエンドポイント](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

エンドポイントと、オプションでステージング済みカタログサポートの認証ヘッダーを設定すると、エンドポイントが詳細ページに表示されます。 必要に応じて、編集アイコンをクリックして、エンドポイントを編集できるのと同じダイアログボックスを開きます。

![CM 環境情報](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Adobe I/OCLI  {#adobe-cli}

CLI を使用してAEMをコマースソリューションにAdobe I/Oするには、次の手順に従います。

1. Cloud Manager プラグインと Adobe I/O CLI を取得します。

   次を確認します。 [AdobeCloud Manager のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=ja) のダウンロード、設定、使用方法 [Adobe I/OCLI](https://github.com/adobe/aio-cli) と [Cloud Manager CLI プラグイン](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Adobe I/O CLI を AEM as a Cloud Service で認証します。

3. Cloud Manager で `COMMERCE_ENDPOINT` 変数を設定します。

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   詳細は、 [CLI ドキュメント](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) を参照してください。

   コマース GraphQL エンドポイント URL は、コマースの GraphQL サービスを指し、安全な HTTPS 接続を使用する必要があります。例：`https://<yourcommercesystem>/graphql`

4. 認証を必要とするステージング済みカタログ機能を有効にする（オプション）

   >[!NOTE]
   >
   >この機能は、Adobe Commerce Enterprise または Cloud Edition でのみ使用できます。詳しくは、[トークンベースの認証](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens)を参照してください。

   Cloud Manager でシークレット変数 `COMMERCE_AUTH_HEADER` を設定します。

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>次のコマンドを使用して、すべての Cloud Manager 変数を一覧表示して再確認できます。 `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

これで、AEM Commerce をas a Cloud Service的に使用する準備が整い、Cloud Manager を介してプロジェクトをデプロイできます。

## ストアとカタログの設定 {#catalog}

CIFのアドオンと [CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components) は、異なるコマースストア（またはストア表示回数など）に接続された複数のAEMサイト構造で使用できます。 デフォルトでは、CIFアドオンは、Adobe Commerceのデフォルトのストアおよびカタログに接続するデフォルトの設定でデプロイされます。

この設定は、次の手順に従って、CIFCloud Service設定を使用して、プロジェクトに合わせて調整できます。

1. AEMで、ツール/Cloud Service/CIF Configuration に移動します。

2. 変更するコマース設定を選択します。

3. アクションバーのを使用して、設定プロパティを開きます。

![CIF Cloud Services の設定](/help/commerce-cloud/assets/cif-cloud-service-config.png)

次のプロパティを設定できます。

- GraphQL クライアント - コマースバックエンド通信用に設定済みの GraphQL クライアントを選択します。このクライアントは通常、デフォルトの状態に保たれます。
- ストア表示 - ストア表示の識別子。空の場合は、デフォルトのストア表示が使用されます。
- GraphQL プロキシパス - AEM の GraphQL プロキシが、コマースバックエンドの GraphQL エンドポイントへのリクエストをプロキシするために使用する URL パス。
  >[!NOTE]
  >
  > ほとんどの設定では、デフォルト値 `/api/graphql` は変更できません。 この設定を変更するのは、指定された GraphQL プロキシを使用しない高度な設定でのみです。
- カタログ UID のサポートを有効にする - コマースバックエンドの GraphQL 呼び出しで、ID ではなく UID のサポートを有効にします。
  >[!NOTE]
  >
  > UID のサポートは、Adobe Commerce 2.4.2 で導入されました。コマースバックエンドがバージョン 2.4.2 以降のGraphQLスキーマをサポートしている場合にのみ、UID を有効にします。
- カタログのルートカテゴリ識別子 - ストアカタログルートの識別子（UID または ID）
  >[!CAUTION]
  >
  > CIF コアコンポーネントバージョン 2.0.0 以降では、`id` のサポートが削除されて `uid` に置き換えられました。プロジェクトで CIF コアコンポーネントバージョン 2.0.0 を使用している場合は、カタログ UID のサポートを有効にし、有効なカテゴリ UID を「カタログルートカテゴリ識別子」として使用する必要があります。

上記の設定は参照用です。プロジェクトは、独自の設定を行う必要があります。

より複雑な設定では、複数のAEMサイト構造を異なるコマースカタログと組み合わせて使用します。詳しくは、 [コマースマルチストアの設定](configuring/multi-store-setup.md) チュートリアル

## その他のリソース {#additional-resources}

- [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
- [コマースマルチストアの設定](configuring/multi-store-setup.md)
- [複数のコマースシステムの設定](configuring/multiple-commerce-systems-setup.md)

