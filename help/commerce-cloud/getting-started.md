---
title: Cloud ServiceとしてのAEMコマースの使用の手引き
description: Cloud ServiceとしてのAEMコマースの使用の手引き
translation-type: tm+mt
source-git-commit: 170a6f4f3aa07b9aa917014b7a682ead9ed595c1
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 6%

---


# Cloud ServiceとしてのAEMコマースの使用の手引き {#start}

AEMコマースをCloud Serviceとして使用し始めるには、Experience Manager Cloud ServiceがCommerce Integration Framework (CIF)アドオンを使用してプロビジョニングされている必要があります。 CIFアドオンは、Cloud Serviceとしての [AEM Sitesの上に追加のモジュール](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/sites/home.html)。

## 使用開始 {#onboarding}

AEMコマースのCloud Serviceとしてのオンボーディングは、次の2つの手順で構成されます。

1. Cloud ServiceとしてのAEMコマースを有効にし、CIFアドオンをプロビジョニングする
2. AEM CommerceをCloud ServiceとしてMagento環境に接続する

最初のステップはAdobeが行います。 IMS組織、Magento環境のGraphQLエンドポイントURLなどの情報を入力する必要があります。 をプロビジョニングプロセスの一部として追加します。 価格とプロビジョニングの詳細については、セールス担当者にお問い合わせください。

CIFアドオンのプロビジョニングが完了すると、既存のCloud Managerプログラムに適用されます。 Cloud Managerのプログラムがない場合は、新しいCloud Managerを作成する必要があります。 詳しくは、「プログラムの [設定](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/setting-up-program.html)」を参照してください。

2つ目のステップは、各AEMに対するCloud Service環境としてのセルフサービスです。 CIFアドオンの初期プロビジョニングの後に行う必要がある追加の設定がいくつかあります。

## AEMコマースとMagentoの接続 {#magento}

CIFアドオンとAEM CIFコアコンポーネント [](https://github.com/adobe/aem-core-cif-components) ( CIF)をMagento環境に接続するには、Cloud Managerの環境変数を使用してMagentoのGraphQLエンドポイントURLを指定する必要があります。 変数名はで `COMMERCE_ENDPOINT`す。 HTTPSを介した安全な接続を設定する必要があります。
AEMごとに異なるMagentoGraphQLエンドポイントURLをCloud Service環境として使用できます。 この方法で、プロジェクトはAEMステージング環境をMagentoステージングシステムとAEM実稼働環境をMagento実稼働システムに接続できます。 そのMagentoGraphQLエンドポイントは、パブリックに使用可能である必要があります。プライベートVPNまたはローカル接続はサポートされていません。

AEM CommerceをMagentoと接続するには、次の手順に従います。

1. Cloud Managerプラグインを使用してAdobeI/O CLIを取得する

   Cloud Manager CLIプラグインを使用して [AdobeI/O CLI](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)[(](https://github.com/adobe/aio-cli) AdobeCloud Manager)をダウンロード、セットアップ、使用する方法については、 [Cloud Managerのドキュメントを参照してください](https://github.com/adobe/aio-cli-plugin-cloudmanager)。

2. CLIをCloud ServiceプログラムとしてAEMで認証する

3. Cloud Managerでの `COMMERCE_ENDPOINT` 変数の設定

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   詳細は、 [CLIドキュメント](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) を参照してください。

   MagentoGraphQLエンドポイントURLは、MagentoのGraphQlサービスを指し、安全なHTTPS接続を使用する必要があります。 例：`https://demo.magentosite.cloud/graphql`

>[!TIP]
>
>次のコマンドを使用して、すべてのCloud Manager変数を重複チェックできます。 `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!Note]
>
>また、 [Cloud Manager API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) (Cloud Manager API)を使用してCloud Manager変数を設定することもできます。

これで、AEM CommerceをCloud Serviceとして使用する準備が整い、Cloud Managerを介してプロジェクトをデプロイできます。

## 3rd party commerce integrations {#integrations}

サードパーティのコマース統合の場合、AEM CommerceをCloud Serviceとして接続し、CIFコアコンポーネントをコマースシステムと接続するには、 [APIマッピングレイヤー](architecture/third-party.md) が必要です。 このAPIマッピングレイヤーは、通常、Adobe I/O Runtimeにデプロイされます。 利用可能な統合やAdobe I/O Runtimeへのアクセスについては、セールス担当者にお問い合わせください。
