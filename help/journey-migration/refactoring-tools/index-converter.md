---
title: インデックスコンバーター
description: インデックスコンバーター
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
source-git-commit: 92c123817a654d0103d0f7b8e457489d9e82c2ce
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 70%

---

# インデックスコンバーター {#index-converter}

インデックスコンバーターは、AEM as a Cloud Service への移行に備えて顧客のインデックス定義を移行するために開発されたユーティリティです。

## はじめに {#introduction}

インデックスコンバーターを使用すると、AEM 開発者は既存のカスタム Oak インデックス定義を AEM as a Cloud Service 互換のカスタム Oak インデックス定義に移行できます。

>[!NOTE]
>インデックスコンバーターでは、`/apps` または `/oak:index` 下に存在する *lucene* 型カスタム Oak インデックス定義のみ変換します。`nt:base` 用に作成された *lucene* 型インデックスは変換しません。

カスタム Oak インデックス定義の作成方法は次の 2 とおりあります。

* `under /apps`（任意のカスタムコンテンツパッケージを使用）
* `/oak:index` パスの直下

If [Oak インデックスの確認](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) を使用していた場合は、定義がAEM as a Cloud Serviceでサポートされていないことを確認します。 そのため、まず Oak インデックス定義に変換し、次に、次のガイドラインに従って、AEMas a Cloud Serviceと互換性のある Custom Oak Index Definitions に移行する必要があります。

* ignore プロパティが `true` に設定されている場合は、Ensure 定義を無視するかスキップします。
* `jcr:primaryType` を `oak:QueryIndexDefinition` に更新します。
* OSGi 設定に従って、無視するプロパティをすべて削除します。
* Ensure 定義からサブツリー `/facets/jcr:content` を削除します。

## インデックスコンバーターの使用 {#using-index-converter}

* Adobe I/OCLI:インデックスコンバーターは、 `aio-cli-plugin-aem-cloud-service-migration` (Adobe I/OCLI 用のAEMas a Cloud Serviceコードリファクタリングプラグイン )。

  このプラグインをインストールして使用する方法については、**[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** を参照してください。

* スタンドアロンユーティリティとして：インデックスコンバーターは、スタンドアロンユーティリティとして実行することもできます。

  このツールの使用方法については、**[Git リソース：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** を参照してください。
