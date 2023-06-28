---
title: 機能テスト
description: コードの品質と信頼性を確保するために、AEM as a Cloud Service デプロイメントプロセスに組み込まれている 3 種類の機能テストについて説明します。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 56%

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

すべての機能テストで、テストの詳細な結果は、 `.zip` ファイルを **ビルドログをダウンロード** ボタンを [配置プロセス](/help/implementing/cloud-manager/deploy-code.md).

これらのログには、実際の AEM ランタイムプロセスのログは含まれていません。これらのログにアクセスするには、 [ログへのアクセスと管理](/help/implementing/cloud-manager/manage-logs.md) を参照してください。

製品機能テストとサンプルのカスタム機能テストは、どちらも [AEM テストクライアント](https://github.com/adobe/aem-testing-clients)に基づいています。

### 製品機能テスト {#product-functional-testing}

製品機能テストは、オーサリングタスクやレプリケーションタスクなど、AEM のコア機能の安定した HTTP 統合テスト（IT）のセットです。これらのテストは、アドビで管理され、コア機能に障害が発生した場合に、カスタムアプリケーションコードに対する変更がデプロイされるのを防ぐことを目的としています。

* [製品機能テスト](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)：製品機能テストは、新しいコードを Cloud Manager にデプロイするたびに自動的に実行され、省略することはできません。
* [実稼動以外のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)：製品機能テストは、実稼動以外のパイプラインを実行する際に、オプションで実行するように選択できます。

製品機能テストは、オープンソースプロジェクトとして維持されます。詳しくは、 [製品機能テスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) 詳しくは、 GitHub を参照してください。

### カスタム機能テスト {#custom-functional-testing}

製品機能テストはアドビで定義されますが、独自のアプリケーション用に独自の品質テストを作成することもできます。これは、 [実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) または [非実稼動パイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) を使用して、アプリケーションの品質を確保します。

カスタム機能テストは、カスタムコードのデプロイメントとプッシュアップグレードの両方で実行されるので、AEMコードの変更によってアプリケーションコードが破損するのを防ぐ、適切な機能テストを作成することが特に重要です。 カスタム機能テストステップは常に存在し、スキップできません。

詳しくは、 [Java 機能テスト](/help/implementing/cloud-manager/java-functional-testing.md) を参照してください。


### カスタム UI テスト {#custom-ui-testing}

カスタム UI テストは、アプリケーションの UI テストを作成して自動的に実行できるオプション機能です。UI テストは、Java や Maven、Node や WebDriver.io などの幅広い言語とフレームワーク、または Selenium に基づいて構築されたその他のフレームワークとテクノロジーを可能にする、Docker イメージにパッケージ化された Selenium ベースのテストです。

詳しくは、 [カスタム UI テスト](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) を参照してください。

