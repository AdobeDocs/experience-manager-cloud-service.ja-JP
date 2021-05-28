---
title: AEM Commerce as a Cloud Service - はじめに
description: 実行中の AEM as a Cloud Service 環境にコマース対応の AEM プロジェクトをデプロイする方法を説明します。Adobe Cloud Manager の機能と CI／CD パイプラインを使用すると、実行中の環境に対する Venia 参照ストアフロントを構築できます。
topics: Commerce
feature: コマース統合フレームワーク Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 36%

---

# AEM Commerce as a Cloud Service - はじめに {#start}

AEM Commerce as a Cloud Service の使用を開始するには、Experience Manager Cloud Service が Commerce Integration Framework（CIF）アドオンによりプロビジョニングされている必要があります。CIF アドオンは、[AEM Sites as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html) の追加モジュールです。

## オンボーディング {#onboarding}

AEM Commerce as a Cloud Service のオンボーディングは、次の 2 つの手順で構成されます。

1. AEM Commerce as a Cloud Service を有効にし、CIF アドオンをプロビジョニングする
2. AEM CommerceをコマースソリューションとCloud Serviceとして接続する

最初のオンボーディング手順はアドビがおこないます。価格とプロビジョニングの詳細については、セールス担当者にお問い合わせください。

CIF アドオンのプロビジョニングが完了すると、既存の Cloud Manager プログラムに適用されます。Cloud Manager プログラムがない場合は、新しく作成する必要があります。詳しくは、「[プログラムの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html)」を参照してください。

2 つ目の手順は、各 AEM as a Cloud Service 環境のセルフサービスです。CIF アドオンの初期プロビジョニングの後で、いくつかの追加の設定をおこなう必要があります。

## AEMとコマースソリューションの接続 {#magento}

CIFアドオンと[AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components)をコマースソリューションに接続するには、Cloud Manager環境変数を使用してGraphQLエンドポイントURLを指定する必要があります。 変数名は `COMMERCE_ENDPOINT` です。HTTPS を介した安全な接続を設定する必要があります。

この環境変数は、次の2つの場所で使用されます。

- AEM CIFコアコンポーネントと顧客プロジェクトコンポーネントで使用される、共通の共有可能なGraphQlクライアントを介した、AEMからコマースバックエンドへのGraphQL呼び出し。
- `/api/graphql`で変数が使用可能に設定される各AEM環境にGraphQLプロキシURLを設定します。 これは、AEMコマースオーサリングツール（CIFアドオン）およびCIFクライアント側コンポーネントで使用されます。

AEM as a Cloud Service 環境ごとに異なる GraphQL エンドポイント URL を使用できます。この方法で、プロジェクトはAEMステージング環境をコマースステージングシステムおよびAEM実稼動環境とコマース実稼動システムを接続できます。  GraphQL エンドポイントは、パブリックに使用可能である必要があります。プライベート VPN またはローカル接続はサポートされていません。オプションで、認証が必要な追加のCIF機能を使用するために認証ヘッダーを指定できます。

オプションで、Adobeコマースエンタープライズ/クラウドの場合のみ、CIFアドオンはAEM作成者向けのステージング済みカタログデータの使用をサポートします。 認証トークンを設定する必要があります。 設定された認証トークンは、セキュリティ上の理由から、AEMオーサーインスタンスでのみ使用および使用できます。 AEMパブリッシュインスタンスは、ステージデータを表示できません。

エンドポイントを設定する方法は2つあります。

### Cloud Manager UI経由（デフォルト） {#cm-ui}

これは、環境の詳細ページのダイアログを使用しておこなえます。 コマース対応プログラムでこのページを表示すると、エンドポイントが現在設定されていない場合は、ボタンが表示されます。

![CM環境情報](/help/commerce-cloud/assets/commerce-cmui.png)

このボタンをクリックすると、次のダイアログが開きます。

![CMコマースエンドポイント](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

エンドポイント（オプションで、ステージングされたカタログのサポートの認証トークン）が設定されると、エンドポイントが詳細ページに表示されます。 「編集」アイコンをクリックすると同じダイアログが開き、必要に応じてエンドポイントを変更できます。

![CM環境情報](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Adobe I/OCLI {#adobe-cli}を使用

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

AEMをAdobe I/OCLIを介してコマースソリューションに接続するには、次の手順に従います。

1. Cloud Manager プラグインと Adobe I/O CLI を取得します。

   [Cloud Manager CLIAdobe I/O](https://github.com/adobe/aio-cli-plugin-cloudmanager)を使用して[AdobeCLI](https://github.com/adobe/aio-cli)をダウンロード、設定、使用する方法については、[Cloud Managerのドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=ja)を参照してください。

2. Adobe I/OCLIをAEM as aでCloud Service

3. Cloud Manager で `COMMERCE_ENDPOINT` 変数を設定します。

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   詳細は、[CLI ドキュメント](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)を参照してください。

   コマースGraphQLエンドポイントURLは、コマースのGraphQlサービスを指し、安全なHTTPS接続を使用する必要があります。 例：`https://demo.magentosite.cloud/graphql`

4. 認証を必要とするステージング済みカタログ機能を有効にする（オプション）

   >[!NOTE]
   >
   >この機能は、Commerce EnterpriseまたはCloud EditionAdobeでのみ使用できます。 詳しくは、[トークンベースの認証](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens)を参照してください。

   Cloud Manager でシークレット変数 `COMMERCE_AUTH_HEADER` を設定します。

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>次のコマンドを使用して、すべての Cloud Manager 変数を一覧表示して再確認できます。 `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

これで、AEM Commerce as a Cloud Service を使用する準備が整い、Cloud Manager を介してプロジェクトをデプロイできます。

## ストアとカタログの設定 {#catalog}

CIFアドオンと[CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、異なるコマースストア（またはストアビューなど）に接続された複数のAEMサイト構造で使用できます。デフォルトでは、CIFアドオンは、Adobeコマースのデフォルトのストアとカタログ(Magento)に接続するデフォルト設定でデプロイされます。

この設定は、次の手順に従って、CIFCloud Service設定を使用してプロジェクトに合わせて調整できます。

1. AEMで、ツール/Cloud Services/CIF設定に移動します。

2. 変更するコマース設定を選択します

3. アクションバーから設定プロパティを開く

![CIFCloud Servicesの設定](/help/commerce-cloud/assets/cif-cloud-service-config.png)

次のプロパティを設定できます。

- GraphQLクライアント — コマースバックエンド通信用に設定済みのGraphQLクライアントを選択します。 これは通常、デフォルトのままになります。
- ストア表示 — (Magento)ストア表示の識別子。 空の場合は、デフォルトのストア表示が使用されます。
- GraphQLプロキシパス — AEMのURLパスGraphQLプロキシは、コマースバックエンドGraphQLエンドポイントに要求をプロキシするために使用します。
   >[!NOTE]
   >
   > ほとんどの設定では、デフォルト値`/api/graphql`は変更できません。 指定されたGraphQLプロキシを使用しない高度な設定のみが、この設定を変更する必要があります。
- カタログUIDのサポートを有効にする — コマースバックエンドのGraphQL呼び出しで、IDではなくUIDのサポートを有効にします。
   >[!NOTE]
   >
   > UIDのサポートは、Adobeコマース(Magento)2.4.2で導入されました。コマースバックエンドがバージョン2.4.2以降のGraphQLスキーマをサポートしている場合にのみ有効にします。
- カタログのルートカテゴリ識別子 — ストアカタログルートの識別子（UIDまたはID）

上記の設定は参照用です。 プロジェクトは、独自の設定を提供する必要があります。

複数のAEMサイト構造を異なるコマースカタログと組み合わせて使用する、より複雑な設定については、『コマースマルチストアの設定](configuring/multi-store-setup.md)』チュートリアルを参照してください。[

## その他のリソース {#additional-resources}

- [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
- [コマースマルチストアの設定](configuring/multi-store-setup.md)
