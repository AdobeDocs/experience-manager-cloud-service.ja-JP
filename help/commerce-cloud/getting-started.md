---
title: AEM Commerce as a Cloud Service - はじめに
description: 実行中の AEM as a Cloud Service 環境にコマース対応の AEM プロジェクトをデプロイする方法を説明します。Adobe Cloud Manager の機能と CI／CD パイプラインを使用すると、実行中の環境に対する Venia 参照ストアフロントを構築できます。
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: d85352b93b9c793a716841523677eb710bb4577c
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 87%

---

# AEM Commerce as a Cloud Service - はじめに {#start}

AEM Commerce as a Cloud Service の使用を開始するには、Experience Manager Cloud Service が Commerce Integration Framework（CIF）アドオンによりプロビジョニングされている必要があります。CIF アドオンは、[AEM Sites as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html?lang=ja) の追加モジュールです。

## オンボーディング {#onboarding}

AEM Commerce as a Cloud Service のオンボーディングは、次の 2 つの手順で構成されます。

1. AEM Commerce as a Cloud Service を有効にし、CIF アドオンをプロビジョニングする
2. AEM Commerce as a Cloud Service をコマースソリューションに接続する

最初のオンボーディング手順はアドビがおこないます。価格とプロビジョニングの詳細については、セールス担当者にお問い合わせください。

CIF アドオンのプロビジョニングが完了すると、既存の Cloud Manager プログラムに適用されます。Cloud Manager プログラムがない場合は、新しく作成する必要があります。詳しくは、「[プログラムの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?lang=ja)」を参照してください。

2 つ目の手順は、各 AEM as a Cloud Service 環境のセルフサービスです。CIF アドオンの初期プロビジョニングの後で、いくつかの追加の設定をおこなう必要があります。

## AEM とコマースソリューションの接続 {#solution}

CIF アドオンと [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)をコマースソリューションに接続するには、Cloud Manager の環境変数で GraphQL エンドポイント URL を指定する必要があります。変数名は `COMMERCE_ENDPOINT` です。HTTPS を介した安全な接続を設定する必要があります。

この環境変数は、次の 2 つの場所で使用されます。

- AEM CIF コアコンポーネントと顧客プロジェクトコンポーネントで使用される、共有可能な共通の GraphQl クライアントを介した、AEM からコマースバックエンドへの GraphQL 呼び出し。
- `/api/graphql` で変数が使用可能に設定された各 AEM 環境への GraphQL プロキシ URL の設定。これは、AEM コマースオーサリングツール（CIF アドオン）および CIF クライアントサイドコンポーネントで使用されます。

AEM as a Cloud Service 環境ごとに異なる GraphQL エンドポイント URL を使用できます。この方法で、プロジェクトは AEM ステージング環境をコマースステージングシステムに、また、AEM 実稼働環境をコマース実稼働システムに接続できます。GraphQL エンドポイントは、公開されている必要があります。プライベート VPN またはローカル接続はサポートされていません。オプションで、認証が必要な追加の CIF 機能を使用するために認証ヘッダーを指定できます。

オプションで、Adobe Commerce Enterprise/Cloud のみで、CIF アドオンはAEM作成者向けのステージング済みカタログデータの使用をサポートします。 認証ヘッダーを設定する必要があります。 このヘッダーは、セキュリティ上の理由から、AEMオーサーインスタンスでのみ使用および使用できます。 AEM パブリッシュインスタンスでは、ステージング済みデータを表示できません。

エンドポイントを設定する方法は 2 つあります。

### Cloud Manager UI 経由（デフォルト） {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

これは、「環境の詳細」ページのダイアログを使用しておこなうことができます。コマース対応プログラムでこのページを表示すると、エンドポイントが設定されていない場合は、ボタンが表示されます。

![CM 環境情報](/help/commerce-cloud/assets/commerce-cmui.png)

このボタンをクリックすると、次のダイアログが開きます。

![CM コマースエンドポイント](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

エンドポイントと、オプションでステージング済みカタログサポートの認証ヘッダーを設定したら、エンドポイントが詳細ページに表示されます。 編集アイコンをクリックすると同じダイアログが開き、必要に応じてエンドポイントを変更できます。

![CM 環境情報](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Adobe I/O CLI 経由  {#adobe-cli}

AEM を Adobe I/O CLI を介してコマースソリューションに接続するには、次の手順に従います。

1. Cloud Manager プラグインと Adobe I/O CLI を取得します。

   [Cloud Manager CLI プラグイン](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=ja)で [Adobe I/O CLI](https://github.com/adobe/aio-cli) をダウンロード、設定、使用する方法については、[Adobe Cloud Manager のドキュメント](https://github.com/adobe/aio-cli-plugin-cloudmanager)を参照してください。

2. Adobe I/O CLI を AEM as a Cloud Service で認証します。

3. Cloud Manager で `COMMERCE_ENDPOINT` 変数を設定します。

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   詳細は、[CLI ドキュメント](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)を参照してください。

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

これで、AEM Commerce as a Cloud Service を使用する準備が整い、Cloud Manager を介してプロジェクトをデプロイできます。

## ストアとカタログの設定 {#catalog}

CIF アドオンと [CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components) は、異なるコマースストア（またはストア表示など）に接続された複数のAEMサイト構造で使用できます。デフォルトでは、CIF アドオンは、Adobe Commerceのデフォルトのストアおよびカタログに接続するデフォルトの設定でデプロイされます。

この設定は、次の手順に従って、CIF Cloud Service 設定を使用してプロジェクトに合わせて調整できます。

1. AEM で、ツール／Cloud Services／CIF 設定に移動します。

2. 変更するコマース設定を選択します。

3. アクションバーから設定プロパティを開きます。

![CIF Cloud Services の設定](/help/commerce-cloud/assets/cif-cloud-service-config.png)

次のプロパティを設定できます。

- GraphQL クライアント - コマースバックエンド通信用に設定済みの GraphQL クライアントを選択します。これは通常、デフォルトのままです。
- ストア表示 — ストア表示の識別子。 空の場合は、デフォルトのストア表示が使用されます。
- GraphQL プロキシパス - AEM の GraphQL プロキシが、コマースバックエンドの GraphQL エンドポイントへのリクエストをプロキシするために使用する URL パス。
   >[!NOTE]
   >
   > ほとんどの設定で、デフォルト値 `/api/graphql` は変更できません。この設定を変更するのは、指定された GraphQL プロキシを使用しない高度な設定でのみです。
- カタログ UID のサポートを有効にする - コマースバックエンドの GraphQL 呼び出しで、ID ではなく UID のサポートを有効にします。
   >[!NOTE]
   >
   > Adobe Commerce 2.4.2 で UID のサポートが導入されました。コマースバックエンドがバージョン 2.4.2 以降の GraphQL スキーマをサポートしている場合にのみ、これを有効にしてください。
- カタログのルートカテゴリ識別子 - ストアカタログルートの識別子（UID または ID）
   >[!CAUTION]
   >
   > CIF コアコンポーネントバージョン 2.0.0 以降では、`id` のサポートが削除されて `uid` に置き換えられました。プロジェクトで CIF コアコンポーネントバージョン 2.0.0 を使用している場合は、カタログ UID のサポートを有効にし、有効なカテゴリ UID を「カタログルートカテゴリ識別子」として使用する必要があります。

上記の設定は参照用です。プロジェクトは、独自の設定を行う必要があります。

複数の AEM サイト構造を異なるコマースカタログと組み合わせて使用する、より複雑な設定については、チュートリアル「[コマースマルチストアの設定](configuring/multi-store-setup.md)」を参照してください。

## その他のリソース {#additional-resources}

- [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
- [コマースマルチストアの設定](configuring/multi-store-setup.md)
