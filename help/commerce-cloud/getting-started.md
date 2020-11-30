---
title: AEM Commerce as a Cloud Service - はじめに
description: コマース対応のAEMプロジェクトを実行中のAEMにクラウドサービス環境としてデプロイする方法を説明します。 Adobeクラウドマネージャーの機能とCI/CDパイプラインを使用して、実行中の環境に対するVeniaリファレンスストアフロントを構築します。
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
translation-type: tm+mt
source-git-commit: b3abefb2953080443e220a248dd4484d23c09a0e
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 93%

---


# AEM Commerce as a Cloud Service - はじめに {#start}

AEM Commerce as a Cloud Service の使用を開始するには、Experience Manager Cloud Service が Commerce Integration Framework（CIF）アドオンによりプロビジョニングされている必要があります。CIF アドオンは、[AEM Sites as a Cloud Service](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/sites/home.html) の追加モジュールです。

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

## オンボーディング {#onboarding}

AEM Commerce as a Cloud Service のオンボーディングは、次の 2 つの手順で構成されます。

1. AEM Commerce as a Cloud Service を有効にし、CIF アドオンをプロビジョニングする
2. AEM Commerce as a Cloud Service を Magento 環境に接続する

最初の手順はアドビがおこないます。プロビジョニングプロセスの一部として、IMS 組織、Magento 環境の GraphQL エンドポイント URL などの情報を入力する必要があります。価格とプロビジョニングの詳細については、セールス担当者にお問い合わせください。

CIF アドオンのプロビジョニングが完了すると、既存の Cloud Manager プログラムに適用されます。Cloud Manager プログラムがない場合は、新しく作成する必要があります。詳しくは、「[プログラムの設定](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-manager/using/getting-started/setting-up-program.html)」を参照してください。

2 つ目の手順は、各 AEM as a Cloud Service 環境のセルフサービスです。CIF アドオンの初期プロビジョニングの後で、いくつかの追加の設定をおこなう必要があります。

## AEM Commerce と Magento の接続 {#magento}

CIF アドオンと [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)を Magento 環境に接続するには、Cloud Manager の環境変数で Magento の GraphQL エンドポイント URL を指定する必要があります。変数名は `COMMERCE_ENDPOINT` です。HTTPS を介した安全な接続を設定する必要があります。AEM as a Cloud Service 環境ごとに異なる Magento GraphQL エンドポイント URL を使用できます。この方法で、プロジェクトは AEM ステージング環境を Magento ステージングシステムに、また、AEM 実稼働環境を Magento 実稼働システムに接続できます。Magento GraphQL エンドポイントは、パブリックに使用可能である必要があります。プライベート VPN またはローカル接続はサポートされていません。

AEM Commerce を Magento と接続するには、次の手順に従います。

1. Cloud Manager プラグインと Adobe I/O CLI を取得します。

   [Cloud Manager CLI プラグイン](https://github.com/adobe/aio-cli-plugin-cloudmanager)で [Adobe I/O CLI](https://github.com/adobe/aio-cli) をダウンロード、設定、使用する方法については、[Adobe Cloud Manager のドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)を参照してください。

2. CLI を AEM as a Cloud Service で認証します。

3. Cloud Manager で `COMMERCE_ENDPOINT` 変数を設定します。

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   詳細は、[CLI ドキュメント](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)を参照してください。

   Magento GraphQL エンドポイント URL は、Magento の GraphQL サービスを指し、安全な HTTPS 接続を使用する必要があります。例：`https://demo.magentosite.cloud/graphql`

>[!TIP]
>
>次のコマンドを使用して、すべての Cloud Manager 変数を一覧表示して再確認できます。 `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!NOTE]
>
>また、[Cloud Manager API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) を使用して Cloud Manager 変数を設定することもできます。

これで、AEM Commerce as a Cloud Service を使用する準備が整い、Cloud Manager を介してプロジェクトをデプロイできます。

## サードパーティコマースシステムとの統合 {#integrations}

サードパーティのコマース統合の場合、AEM Commerce as a Cloud Service および CIF コアコンポーネントをコマースシステムと接続するには、[API マッピングレイヤー](architecture/third-party.md)が必要です。この API マッピングレイヤーは、通常、Adobe I/O Runtime にデプロイされます。利用可能な統合や Adobe I/O Runtime へのアクセスについては、セールス担当者にお問い合わせください。
