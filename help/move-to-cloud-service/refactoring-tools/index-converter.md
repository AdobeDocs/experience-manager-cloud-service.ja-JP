---
title: インデックスコンバータ
description: インデックスコンバータ
translation-type: tm+mt
source-git-commit: fecbd0b4d5cfd8aa970c235c79158bea44403c09
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 6%

---


# インデックスコンバータ{#index-converter}

Index Converterは、Cloud ServiceとしてのAEMへの移行に備えて、顧客のインデックス定義を移行するために開発されたユーティリティです。

## 概要 {#introduction}

Index Converterを使用すると、AEM開発者は、Cloud Service互換のカスタムOakインデックス定義として、既存のカスタムOakインデックス定義をAEMに移行できます。

>[!NOTE]
>インデックスコンバータは、`/apps`または`/oak:index`に存在する&#x200B;*lucene*&#x200B;型カスタムOakインデックス定義のみを変換します。 `nt:base`用に作成された&#x200B;*lucene*&#x200B;型のインデックスは変換しません。

カスタムOakインデックス定義を作成する方法は2つあります。

* `under /apps` （任意のカスタムコンテンツパッケージを使用）
* &lt;a0/のパスの直下`/oak:index`

>[!NOTE]
>Oak定義の定義および作成方法については、[Ensure Oak Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)を参照してください。

## インデックスコンバータの使用{#using-index-converter}

>[!NOTE]
>[AIO CLIプラグインを使用して](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)Index Converterツールを使用することをお勧めしますが、このツールはスタンドアロンで実行することもできます。

**[Gitリソースを参照：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)**&#x200B;を参照してください。

