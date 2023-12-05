---
title: 機能テスト
description: コードの品質と信頼性を確保するために、AEM as a Cloud Service デプロイメントプロセスに組み込まれている 3 種類の機能テストについて説明します。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 9%

---


# はじめに {#functional-testing-introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="機能テスト"
>abstract="コードの品質と信頼性を確保するために、AEM as a Cloud Service デプロイメントプロセスに組み込まれている 3 種類の機能テストについて説明します。"

で使用できる品質ゲートについて説明します。 [AEMas a Cloud Serviceデプロイメントプロセス](/help/implementing/cloud-manager/deploy-code.md)、組み込まれている様々な種類の機能テスト、投稿方法、および全体的なテスト戦略のコンテキストでそれらを最大限に活用する方法。

## 概要

次の図は、テスト戦略全体のコンテキストで使用可能なパイプラインの概要と、 [AEMas a Cloud Serviceデプロイメントプロセス](/help/implementing/cloud-manager/deploy-code.md).

![AEM Cloud Serviceデプロイメントの品質ゲート](assets/functional-testing/quality-gates-compact.svg)

## 目的

AEM Cloud Serviceデプロイメントパイプラインの目的は、開発およびAEM製品リリースのライフサイクルの様々な段階で、堅牢で安全なデプロイメントを容易にすることです。 これらのパイプラインには、様々なレベルで複数の品質ゲートが組み込まれており、AEMアプリケーションの変更とAEM製品のアップデートの両方に対するデプロイメントの整合性と安全性を確保できます。

Adobeには、いくつかの組み込みの品質ゲートが用意されていますが、実装と設定に対してユーザーが介入する必要がある場合もあります。 これらの品質ゲートは汎用性が高く、ライフサイクルの様々な段階で適用でき、独自の開発設定および CI/CD プロセスに統合できるものもあります。

組み込みの品質ゲートでは主に、AEMアプリケーションのコンテキスト内でAEM製品の機能を検証します。 一方、設定したカスタム品質ゲートは、アプリケーションの重要な機能とユーザーインタラクションが意図したとおりに実行されることを検証するように設計されています。 これら 2 つの品質ゲートをまとめて連携させ、コードの変更とAEM製品のアップデートの両方に対する堅牢で安全な自動デプロイメントを実現します。

これらの品質ゲートは、テスト戦略全体の包括的なテストフレームワークではないことに注意する必要があります。 AEM製品は、AEM Cloud Service のデプロイメントプロセスに入る前に、広範なテストがおこなわれます。 同様に、アプリケーションは、デプロイメントフェーズに達する前に、既に高品質である必要があります。 このアプローチは、品質ゲートが完全なテストレジメンの代わりとなるのではなく、デプロイメントプロセスを保護する主な目的に焦点を当てるようにします。

## 品質ゲート

次の図は、使用可能な品質ゲートと、テスト戦略全体でのその使用状況および [AEMas a Cloud Serviceデプロイメントプロセス](/help/implementing/cloud-manager/deploy-code.md).

![AEM Cloud Serviceデプロイメントの品質ゲート](assets/functional-testing/quality-gates-overview.svg)

### お客様が提供する品質ゲートの概要

|                               | 単体テスト | カスタム<br/> 機能テスト | カスタム<br/> UI テスト | 顧客<br/> 検証 | 手動<br/> テスト |
|:------------------------------|:---------------------:|:-----------------------------------:|:-----------------------------------:|:-------------------------:|:-------------------:|
| **実稼動パイプライン** | はい<br/>ブロック<br/> | はい<br/>ブロック<br/>60m タイムアウト | はい<br/>ブロック<br/>60m タイムアウト | いいえ | 不可 |
| **実稼動以外のパイプライン** | はい<br/>ブロック<br/> | オプトイン<br/>ブロック<br/>60m タイムアウト | オプトイン<br/>ブロック<br/>60m タイムアウト | いいえ | 不可 |
| **Adobe内部検証** | はい<br/>ブロック<br/> | はい<br/>ブロック<br/>60m タイムアウト | はい<br/>ブロック<br/>60m タイムアウト | いいえ | 不可 |
| **顧客 CI/CD** | はい | はい | はい | はい | はい |
| **お客様のローカル開発者** | はい | はい | はい | はい | はい |

### 単体テスト

すべてのテスト戦略の基盤となる、AEMアプリケーションの単体テストを実施することをお勧めします。 高速で頻繁に実行し、早く、迅速にフィードバックを提供することを目的としています。 これらは、開発者ワークフロー、独自の CI/CD、AEM Cloud Service デプロイメントパイプラインに緊密に統合されています。

JUnit を使用して実装され、Maven で実行されます。 詳しくは、 [AEMプロジェクトアーキタイプのコアモジュール](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/core.html#unit-tests) AEMの単体テストの例と導入方法を参照してください。

### コード品質

この品質ゲートは標準で設定され、AEMアプリケーションコードで静的コード分析を実行します。

詳しくは、 [コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md) および [カスタムコード品質ルール](/help/implementing/cloud-manager/custom-code-quality-rules.md) を参照してください。

### 製品テスト

製品機能テストは、オーサリングタスクやレプリケーションタスクなど、AEM のコア機能の安定した HTTP 統合テスト（IT）のセットです。Adobeは標準で提供し、維持します。 これは、カスタムアプリケーションコードがAEM製品のコア機能を壊した場合に、カスタムアプリケーションコードに対する変更がデプロイされるのを防ぐためのものです。

これらは Junit を使用して実装され、Maven を使用して実行され、公式の [AEM Testing Clients](https://github.com/adobe/aem-testing-clients). 製品テストスイートは、 [オープンソースプロジェクト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)は、ベストプラクティスに従っており、テストの実装の出発点として適しています。

### カスタム機能テスト

製品テストと同様に、お客様の機能テストは HTTP 統合テスト (IT) であり、Junit を使用して実装され、Maven を使用して実行され、公式の [AEM Testing Clients](https://github.com/adobe/aem-testing-clients).

>[!NOTE]
>
>カスタム機能テストは、AEMアプリケーションのデプロイメント変更やAEM製品プッシュアップデートで使用される実稼動および非実稼動（オプトイン）パイプラインで実行されるので、アプリケーションの適切な機能を確保し、リリースの安全性を高める重要な役割を果たします。 また、お客様の機能テストは、各顧客の内部プレリリース検証パイプラインでも実行され、早期のフィードバックが得られます。

パイプラインの実行を効率的に保つために、主な機能と主なユーザーインタラクションフローに焦点を当てることをお勧めします。 機能テストの実行時間は、15 分以下にすることをお勧めします。 この品質ゲートに収まらない完全な機能テストスイートは、顧客の開発フロー中に、一般的な顧客検証パイプラインの一部として実行することをお勧めします。

詳しくは、 [オープンソース製品テスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) または [AEM Projects アーキタイプの it.tests モジュール](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/ittests.html) 例：

詳しくは、[Java 機能テスト](/help/implementing/cloud-manager/java-functional-testing.md)を参照してください。

### カスタム UI テスト

お客様固有の開発に対するリスク制御を最大限に高めるために、Adobeは、重要な UI テストを AEMCS に取り込むことを強く推奨します。 これらは、数が少なく抑えられ、顧客体験に最も大きな影響を与えるように意図されています。

テストは Docker イメージでパッケージ化され、可能な限り揮発性が高く設計されています（Cypress、Selenium、Java、JavaScript をサポート）。 カスタム機能テストと同じ特性と目的に従います。

>[!NOTE]
>
>カスタム UI テストは、AEMアプリケーションによって使用される実稼動および非実稼動（オプトイン）パイプラインで実行され、デプロイメントやAEM製品プッシュの更新が変更されるので、アプリケーションの適切な機能を確保し、リリースの安全性を高める重要な貢献となります。 また、顧客 UI テストは、各顧客の内部プレリリース検証パイプラインで実行され、早期のフィードバックが提供されます。

パイプラインの実行を効率的におこなうために、主な機能と主なユーザーインタラクションフローに注力することをお勧めします。 この品質ゲートに収まらない完全な UI テストスイートは、顧客の開発フロー中に、一般的な顧客検証パイプラインの一部として実行することをお勧めします。

詳しくは、 [オープンソースのサンプルテスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/) または [AEMプロジェクトアーキタイプの ui.tests モジュール](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uitests.html) 例：

詳しくは、[カスタム UI テスト](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)を参照してください。

### エクスペリエンス監査

エクスペリエンス監査品質ゲートが実行中です [Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) 顧客の web ページに対する監査。

この品質ゲートは、AEMの標準で提供されていますが、デプロイメントパイプラインをブロックしていません。 デフォルトでは、ルートページ (`/`) をクリックします。 監査対象と見なされる最大 25 個のカスタムパスを設定して、投稿できます。

詳しくは、 [エクスペリエンス監査テスト](/help/implementing/cloud-manager/experience-audit-testing.md) を参照してください。

### 顧客の検証

顧客検証の品質ゲートは、顧客のアプリケーションの変更がAEMクラウドデプロイメントパイプラインに到達する前に実行される、顧客独自のテスト戦略と作業のプレースホルダーです。

ここで、好みのツールとフレームワークを選択できます。 顧客機能テストやカスタム UI テストとは異なり、AEMに関するas a Cloud Service的な制限はないので、長時間実行される機能および UI テストをここで実行することをお勧めします。

任意のツールとフレームワークを自由に選択できますが、HTTP ベースの統合テストと UI テストは、カスタム機能テストおよびカスタム UI テスト品質ゲートで利用可能なツールとフレームワークと連携させることをお勧めします。 統合をお勧めします [迅速な開発環境 (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) ローカルテスト戦略で、AEMクラウド環境にできる限り近い場所でテストする必要があります。

### 手動テスト

手動テストの品質ゲートは、手動テストをおこなうお客様向けのプレースホルダーです。 AEMクラウドパイプラインは手動テストをサポートしていないので、独自のローカルテスト戦略の一環として実行する必要があります。

手動テストの場合、追加のAEM Cloud Service開発環境と統合すると便利です。
