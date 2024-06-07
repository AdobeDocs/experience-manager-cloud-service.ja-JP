---
title: GitHub チェック注釈
description: GitHub がプライベートリポジトリの注釈 PR をチェックして、役立つフィードバックを提供する方法を説明します。
exl-id: 15178de8-8a8a-4300-8510-88875ad0fc8c
source-git-commit: f7348d388918a31d255babcfb64b3dc547153d62
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# GitHub チェック注釈 {#github-annotations}

GitHub がプライベートリポジトリの注釈 PR をチェックして、役立つフィードバックを提供する方法を説明します。

## 概要 {#overview}

を使用している場合 [プライベートリポジトリー](private-repositories.md) cloud Manager プログラムでは、プルリクエストのたびに GitHub でのチェックが自動的に実行されます。 これらには、コードの問題をできるだけ早く理解するのに役立つ有用な情報が注釈として付けられています。

![GitHub チェック注釈の例](assets/github-check-annotations.png)

[コード品質](/help/implementing/cloud-manager/code-quality-testing.md) によって検出された問題 [SonarQube](/help/implementing/cloud-manager/custom-code-quality-rules.md) 明確にリストされています。

![コード問題注釈の例](assets/github-check-annotations-example.png)

イシューと正確なコード行が表示され、それをクリックして関連するコードを表示できます。 これらの注釈は、プルリクエストで変更された問題だけでなく、すべてのコード問題に対して提供されます。

![コード問題注釈の例](assets/github-check-annotations-example-code.png)

すべての注釈付き行は、次の行に集約されます **変更されたファイル** github プルリクエストでタブに移動します。 プルリクエストで変更されなかったファイルの注釈は、独自のセクションに表示されます。

![「変更されたファイル」タブの注釈の例](assets/github-check-annotations-files-changed.png)

## コード品質パイプライン {#code-quality-pipelines}

この [コード品質](/help/implementing/cloud-manager/code-quality-testing.md) 結果は、の下部にある Cloud Manager によって自動的にトリガーされるパイプラインにも表示されます。 **チェック** タブ。 からもアクセスできます **詳細** プルリクエストのチェック。

![注釈の例](assets/github-check-annotations-code-quality.png)

![注釈の例](assets/github-check-annotations-code-quality-2.png)

また、CSV 形式でイシューを視覚化することもできます。 これは、次の方法で取得できます。 [cloud Manager でパイプライン実行の詳細を表示する。](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)
