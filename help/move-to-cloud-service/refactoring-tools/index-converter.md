---
title: インデックスコンバーター
description: インデックスコンバーター
exl-id: e6a3ec6d-cc02-4f5b-8b1d-ea481d6884ca
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '279'
ht-degree: 100%

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

AEM as a Cloud Service では Ensure 定義がサポートされていないことに注意してください。そのため、[Ensure Oak インデックス](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)を使用した場合は、まず Oak インデックス定義に変換した後、次のガイドラインに従って、AEM as a Cloud Service と互換性のあるカスタム Oak インデックス定義に移行する必要があります。

* ignore プロパティが `true` に設定されている場合は、Ensure 定義を無視するかスキップします。
* `jcr:primaryType` を `oak:QueryIndexDefinition` に更新します。
* OSGi 設定に従って、無視するプロパティをすべて削除します。
* Ensure 定義からサブツリー `/facets/jcr:content` を削除します。

## インデックスコンバーターの使用 {#using-index-converter}

* Adobe I/O CLI を経由：`aio-cli-plugin-aem-cloud-service-migration`（AEM as a Cloud Service の Adobe I/O CLI 用コードリファクタリングプラグイン）を介してインデックスコンバーターを使用することをお勧めします。

   このプラグインをインストールして使用する方法については、**[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** を参照してください。

* スタンドアロンユーティリティとして：インデックスコンバーターは、スタンドアロンユーティリティとして実行することもできます。

   このツールの使用方法については、**[Git リソース：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** を参照してください。
