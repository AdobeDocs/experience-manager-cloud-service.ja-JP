---
title: インデックスコンバータ
description: インデックスコンバータ
translation-type: tm+mt
source-git-commit: 21bd9392d913369a5e8e0ebd9badbbe30fd4bba3
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 5%

---


# インデックスコンバータ{#index-converter}

Index Converterは、Cloud ServiceとしてのAEMへの移行に備えて、顧客のインデックス定義を移行するために開発されたユーティリティです。

## 概要 {#introduction}

Index Converterを使用すると、AEM開発者は、Cloud Service互換のカスタムOakインデックス定義として、既存のカスタムOakインデックス定義をAEMに移行できます。

>[!NOTE]
>インデックスコンバータは、`/apps`または`/oak:index`の下に存在する&#x200B;*lucene*&#x200B;型カスタムOakインデックス定義のみを変換します。 `nt:base`用に作成された&#x200B;*lucene*&#x200B;型のインデックスは変換しません。

## インデックスコンバータの使用{#using-index-converter}

**[Gitリソースを参照：aem-cs-source-migration-index-converter](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;を参照してください。

