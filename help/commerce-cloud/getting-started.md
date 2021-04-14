---
title: AEM Commerce as a Cloud Service - はじめに
description: 実行中の AEM as a Cloud Service 環境にコマース対応の AEM プロジェクトをデプロイする方法を説明します。Adobe Cloud Manager の機能と CI／CD パイプラインを使用すると、実行中の環境に対する Venia 参照ストアフロントを構築できます。
topics: Commerce
feature: Commerce Integration Framework、Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
translation-type: tm+mt
source-git-commit: e34592d24c8f6c17e6959db1d5c513feaf6381c8
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 68%

---

# AEM Commerce as a Cloud Service - はじめに {#start}

AEM Commerce as a Cloud Service の使用を開始するには、Experience Manager Cloud Service が Commerce Integration Framework（CIF）アドオンによりプロビジョニングされている必要があります。CIF アドオンは、[AEM Sites as a Cloud Service](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/sites/home.html) の追加モジュールです。

## オンボーディング {#onboarding}

AEM Commerce as a Cloud Service のオンボーディングは、次の 2 つの手順で構成されます。

1. AEM Commerce as a Cloud Service を有効にし、CIF アドオンをプロビジョニングする
2. AEM CommerceをCloud Serviceとしてコマースソリューションに接続

最初のオンボーディングステップはAdobeが行います。 価格とプロビジョニングの詳細については、セールス担当者にお問い合わせください。

CIF アドオンのプロビジョニングが完了すると、既存の Cloud Manager プログラムに適用されます。Cloud Manager プログラムがない場合は、新しく作成する必要があります。詳しくは、「[プログラムの設定](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-manager/using/getting-started/setting-up-program.html)」を参照してください。

2 つ目の手順は、各 AEM as a Cloud Service 環境のセルフサービスです。CIF アドオンの初期プロビジョニングの後で、いくつかの追加の設定をおこなう必要があります。

## AEMとコマースソリューションの接続{#magento}

CIFアドオンと[AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components)をコマースソリューションに接続するには、Cloud Manager環境変数を使用してGraphQLエンドポイントURLを指定する必要があります。 変数名は `COMMERCE_ENDPOINT` です。HTTPS を介した安全な接続を設定する必要があります。AEM as a Cloud Service 環境ごとに異なる GraphQL エンドポイント URL を使用できます。この方法で、プロジェクトはAEMステージング環境をコマースステージングシステムおよびAEM実稼働環境とコマース実稼働システムに接続できます。  GraphQL エンドポイントは、パブリックに使用可能である必要があります。プライベート VPN またはローカル接続はサポートされていません。必要に応じて、認証が必要な追加のCIF機能を使用するために、認証ヘッダーを提供できます。

エンドポイントを設定する方法は2つあります。

### 1) Cloud Manager UI（デフォルト）を使用

これは、環境の詳細ページのダイアログを使用して行うことができます。 コマース対応プログラムでこのページを表示すると、エンドポイントが現在設定されていない場合はボタンが表示されます。

![エコフレンドリーバッジの最終実装](/help/commerce-cloud/assets/commerce-cmui.png)

このボタンをクリックすると、次のダイアログが開きます。

![エコフレンドリーバッジの最終実装](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

エンドポイント（およびオプションでトークン）が設定されると、エンドポイントが詳細ページに表示されます。 編集アイコンをクリックすると、同じダイアログが開き、必要に応じてエンドポイントを変更できます。

![エコフレンドリーバッジの最終実装](/help/commerce-cloud/assets/commerce-cmui-done.png)

### 2)Adobe I/OCLIを使用

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Adobe I/OCLIを使用してAEMをコマースソリューションに接続するには、次の手順に従います。

1. Cloud Manager プラグインと Adobe I/O CLI を取得します。

   [Cloud Manager CLI プラグイン](https://github.com/adobe/aio-cli-plugin-cloudmanager)で [Adobe I/O CLI](https://github.com/adobe/aio-cli) をダウンロード、設定、使用する方法については、[Adobe Cloud Manager のドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)を参照してください。

2. Adobe I/OCLIをCloud ServiceプログラムとしてAEMで認証する

3. Cloud Manager で `COMMERCE_ENDPOINT` 変数を設定します。

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   詳細は、[CLI ドキュメント](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)を参照してください。

   コマースGraphQLエンドポイントURLは、コマースのGraphQlサービスを指し、安全なHTTPS接続を使用する必要があります。 例：`https://demo.magentosite.cloud/graphql`

>[!TIP]
>
>次のコマンドを使用して、すべての Cloud Manager 変数を一覧表示して再確認できます。 `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

これで、AEM Commerce as a Cloud Service を使用する準備が整い、Cloud Manager を介してプロジェクトをデプロイできます。

## 認証を必要とする機能を有効にする（オプション） {#staging}

>[!NOTE]
>
>この機能は、Magento Enterprise Edition または Magento Cloud でのみ使用できます。

1. Magento にログインし、統合トークンを作成します。詳しくは、[トークンベースの認証](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens)を参照してください。統合トークンから `Content -> Staging` リソースに&#x200B;*のみ*&#x200B;アクセスできることを確認してください。`Access Token` 値をコピーします。

1. Cloud Manager でシークレット変数 `COMMERCE_AUTH_HEADER` を設定します。

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

   Cloud Manager 用の Adobe I/O CLI を設定する方法については、[AEM Commerce と Magento の接続](#magento)を参照してください。

## サードパーティコマースシステムとの統合 {#integrations}

サードパーティのコマース統合の場合、AEM Commerce as a Cloud Service および CIF コアコンポーネントをコマースシステムと接続するには、[API マッピングレイヤー](architecture/third-party.md)が必要です。この API マッピングレイヤーは、通常、Adobe I/O Runtime にデプロイされます。利用可能な統合や Adobe I/O Runtime へのアクセスについては、セールス担当者にお問い合わせください。
