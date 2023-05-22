---
title: 機能テスト
description: コードの品質と信頼性を確保するために、AEM as a Cloud Service デプロイメントプロセスに組み込まれている 3 種類の機能テストについて説明します。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 7d15440159a8e24314753acd5b37fcd2c5e8ec4c
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 83%

---


# 機能テスト {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="機能テスト"
>abstract="コードの品質と信頼性を確保するために、AEM as a Cloud Service デプロイメントプロセスに組み込まれている 3 種類の機能テストについて説明します。"

コードの品質と信頼性を確保するために、[AEM as a Cloud Service デプロイメントプロセス](/help/implementing/cloud-manager/deploy-code.md)に組み込まれている 3 種類の機能テストについて説明します。

## 範囲

Cloud Manager パイプラインの機能テスト手順の目的は、アプリケーションの基本的な機能が期待どおりに動作していることを確認することです。

このテスト段階は、コードを実稼動環境にデプロイする前の、自動テストの最後のレベルです。

機能テストは、置き換えるのではなく、Cloud Manager でのパイプライン実行外で実行される単体テスト、統合テスト、機能テストなど、他のテスト戦略を補完し拡張する必要があります。

## 概要 {#overview}

AEM as a Cloud Service には 3 種類の機能テストがあります。

* [製品機能テスト](#product-functional-testing)
* [カスタム機能テスト](#custom-functional-testing)
* [カスタム UI テスト](#custom-ui-testing)

すべての機能テストについて、[デプロイメントプロセス](/help/implementing/cloud-manager/deploy-code.md)の一環としてビルド概要画面の「**ビルドログをダウンロード**」ボタンを使用して、テストの詳細な結果を `.zip` ファイル形式でダウンロードできます。

これらのログには、実際の AEM ランタイムプロセスのログは含まれていません。これらのログへのアクセスについて詳しくは、[ログへのアクセスと管理](/help/implementing/cloud-manager/manage-logs.md) を参照してください。

製品機能テストとサンプルのカスタム機能テストは、どちらも [AEM テストクライアント](https://github.com/adobe/aem-testing-clients)に基づいています。

### 製品機能テスト {#product-functional-testing}

製品機能テストは、オーサリングタスクやレプリケーションタスクなど、AEM のコア機能の安定した HTTP 統合テスト（IT）のセットです。これらのテストは、アドビで管理され、コア機能に障害が発生した場合に、カスタムアプリケーションコードに対する変更がデプロイされるのを防ぐことを目的としています。

* [製品機能テスト](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)：製品機能テストは、新しいコードを Cloud Manager にデプロイするたびに自動的に実行され、省略することはできません。
* [実稼動以外のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)：製品機能テストは、実稼動以外のパイプラインを実行する際に、オプションで実行するように選択できます。

製品機能テストは、オープンソースプロジェクトとして維持されます。詳しくは、GitHub の[製品機能テスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)を参照してください。

### カスタム機能テスト {#custom-functional-testing}

製品機能テストはアドビで定義されますが、独自のアプリケーション用に独自の品質テストを作成することもできます。これは、アプリケーションの品質を確保するために、[実稼働パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)またはオプションで[実稼働以外のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)の一部としてカスタム機能テストとして実行されます。

カスタム機能テストは、カスタムコードのデプロイメントとプッシュアップグレードの両方で実行されます。そのため、AEM コードの変更によってアプリケーションコードが機能しなくなることを防ぐ適切な機能テストを作成することが特に重要になります。カスタム機能テストステップは常に存在し、スキップできません。

詳しくは、 [Java 機能テスト](/help/implementing/cloud-manager/java-functional-testing.md) を参照してください。


### カスタム UI テスト {#custom-ui-testing}

カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプション機能です。UI テストは、Docker イメージにパッケージ化された Selenium ベースのテストです。幅広い言語とフレームワーク（Java、Maven、Node、WebDriver.io、Selenium 上に構築されたその他のフレームワークとテクノロジーなど）を選択できるようにします。

詳しくは、 [カスタム UI テスト](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) を参照してください。

