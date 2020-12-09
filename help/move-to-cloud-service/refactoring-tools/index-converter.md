---
title: インデックスコンバータ
description: インデックスコンバータ
translation-type: tm+mt
source-git-commit: 3fe19282f9e96d503f4e8be05553c6f48a6f19b6
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 9%

---


# インデックスコンバータ{#index-converter}

Index Converterは、Cloud ServiceとしてAEMに移行する際に、お客様のインデックス定義を移行するために開発されたユーティリティです。

## 概要 {#introduction}

Index Converterを使用すると、AEM開発者は、Cloud Service互換のカスタムOakインデックス定義として、既存のカスタムOakインデックス定義をAEMに移行できます。

>[!NOTE]
>インデックスコンバータは、`/apps`または`/oak:index`に存在する&#x200B;*lucene*&#x200B;型カスタムOakインデックス定義のみを変換します。 `nt:base`用に作成された&#x200B;*lucene*&#x200B;型のインデックスは変換しません。

カスタムOakインデックス定義を作成する方法は2つあります。

* `under /apps` （任意のカスタムコンテンツパッケージを使用）
* &lt;a0/のパスの直下`/oak:index`

[Ensure Oak Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)を使用した場合は、Cloud ServiceとしてAEMで定義がサポートされていないことを確認してください。したがって、まずOak Index Definitionsに変換し、次のガイドラインに従ってAEMと互換性のあるカスタムOak Index Definitionsに移行する必要があります。

* 「ignore」プロパティが`true`に設定されている場合は、「Ensure Definition」を無視するか、スキップします。
* `jcr:primaryType`を`oak:QueryIndexDefinition`に更新
* OSGi設定で説明されているように無視するプロパティを削除します
* Remove subtree `/facets/jcr:content` from Ensure Definition

## インデックスコンバータの使用{#using-index-converter}

* Adobe I/OCLI経由：`aio-cli-plugin-aem-cloud-service-migration`経由でIndex Converterを使用することをお勧めします(AEMはAdobe I/OCLIのCloud Serviceコードリファクタリングプラグインとして使用します)。

   プラグインをインストールして使用する方法について詳しくは、**[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** を参照してください。

* スタンドアロンユーティリティとして、Index Converterは、スタンドアロンユーティリティとして実行することもできます。

   **[Gitリソースを参照：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)**&#x200B;を参照して、このツールの使用方法を確認してください。



