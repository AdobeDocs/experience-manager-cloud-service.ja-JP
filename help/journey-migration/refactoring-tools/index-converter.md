---
title: インデックスコンバーター
description: AEM as a Cloud Service への移行に備えて、インデックス定義を移行する方法を説明します。
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '272'
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

[Oak インデックスを確認](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)を使用した場合、AEM as a Cloud Service では定義を確認がサポートされません。そのため、まず Oak インデックス定義に変換し、次のガイドラインに従って、AEM as a Cloud Service と互換性のあるカスタム Oak インデックス定義に移行する必要があります。

* ignore プロパティが `true` に設定されている場合は、Ensure 定義を無視するかスキップします。
* `jcr:primaryType` を `oak:QueryIndexDefinition` に更新します。
* OSGi 設定に従って、無視するプロパティをすべて削除します。
* Ensure 定義からサブツリー `/facets/jcr:content` を削除します。

## インデックスコンバーターの使用 {#using-index-converter}

* Adobe I/O CLI を経由：`aio-cli-plugin-aem-cloud-service-migration`（AEM as a Cloud Service の Adobe I/O CLI 用コードリファクタリングプラグイン）を介してインデックスコンバーターを使用することをお勧めします。

  プラグインをインストールして使用する方法について詳しくは、**[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** を参照してください。

* スタンドアロンユーティリティとして：インデックスコンバーターは、スタンドアロンユーティリティとして実行することもできます。

  このツールの使用方法については、**[Git リソース：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** を参照してください。
