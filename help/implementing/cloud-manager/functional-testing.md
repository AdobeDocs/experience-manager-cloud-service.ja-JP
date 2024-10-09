---
title: 機能テスト
description: コードの品質と信頼性を確保するために、AEM as a Cloud Service デプロイメントプロセスに組み込まれている 3 種類の機能テストについて説明します。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 7a370ee0ab77046d128ae260af2575d50e655254
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 59%

---


# はじめに {#functional-testing-introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="機能テスト"
>abstract="コードの品質と信頼性を確保するために、AEM as a Cloud Service デプロイメントプロセスに組み込まれている 3 種類の機能テストについて説明します。"

[AEM as a Cloud Service デプロイメントプロセスで使用できる品質ゲート ](/help/implementing/cloud-manager/deploy-code.md) および様々なタイプの組み込み機能テストについて説明します。 包括的なテスト戦略のフレームワーク内で、使用をコントリビューションおよび最適化する方法について説明します。

## 概要

次の図は、テスト戦略全体のコンテキストで使用可能なパイプラインの概要と、[AEM as a Cloud Service デプロイメントプロセス](/help/implementing/cloud-manager/deploy-code.md)を示しています。

![AEM Cloud Service デプロイメントの品質ゲート](assets/functional-testing/quality-gates-compact.svg)

## 目的

AEM Cloud Service デプロイメントパイプラインの目的は、開発および AEM 製品リリースのライフサイクルの様々な段階で、堅牢で安全なデプロイメントを容易にすることです。これらのパイプラインには、様々なレベルで複数の品質ゲートが組み込まれており、AEM アプリケーションの変更と AEM 製品のアップデートの両方に対するデプロイメントの整合性と安全性を確保できます。

Adobeには、いくつかの組み込みの品質ゲートが用意されていますが、実装と設定に対してユーザーが介入する必要がある場合もあります。これらの品質ゲートは汎用性が高く、様々なライフサイクル段階で適用され、開発セットアップや CI/CD プロセスに直接統合されます。

組み込みの品質ゲートでは、AEMアプリケーションのコンテキスト内でAEM製品の機能を主に検証します。一方、設定したカスタム品質ゲートは、アプリケーションの重要な機能とユーザーインタラクションが意図したとおりに実行されることを検証するように設計されています。これら 2 つの品質ゲートをまとめて連携させ、コードの変更と AEM 製品のアップデートの両方に対する堅牢で安全な自動デプロイメントを実現します。

これらの品質ゲートは、テスト戦略全体の包括的なテストフレームワークではないことに注意する必要があります。AEM 製品は、AEM Cloud Service のデプロイメントプロセスに入る前に、広範なテストが行われます。同様に、アプリケーションは、デプロイメントフェーズに達する前に、既に高品質である必要があります。このアプローチは、品質ゲートが完全なテスト計画の代わりとなるのではなく、デプロイメントプロセスを保護する主要目的に焦点を当てるようにします。

## 品質ゲート

次の図は、使用可能な品質ゲートの詳細図、テスト戦略全体でのその使用状況、および [AEM as a Cloud Service デプロイメントプロセス](/help/implementing/cloud-manager/deploy-code.md)を示します。

![AEM Cloud Service デプロイメントの品質ゲート](assets/functional-testing/quality-gates-overview.svg)

### お客様が提供する品質ゲートの概要

|                               | 単体テスト | カスタム<br/> 機能テスト | カスタム<br/> UI テスト | 顧客<br/> 検証 | 手動<br/> テスト |
|:------------------------------|:---------------------:|:-----------------------------------:|:-----------------------------------:|:-------------------------:|:-------------------:|
| **実稼動パイプライン** | あり<br/>ブロック<br/> | あり<br/>ブロック<br/>60m タイムアウト | あり<br/>ブロック<br/>30m タイムアウト | 不可 | 不可 |
| **実稼動以外のパイプライン** | あり<br/>ブロック<br/> | オプトイン<br/>ブロック<br/>60m タイムアウト | オプトイン<br/>ブロック<br/>30m タイムアウト | 不可 | 不可 |
| **Adobe 内部検証** | あり<br/>ブロック<br/> | あり<br/>ブロック<br/>60m タイムアウト | あり<br/>ブロック<br/>30m タイムアウト | 不可 | 不可 |
| **顧客の CI/CD** | はい | はい | はい | はい | はい |
| **顧客のローカル開発者** | はい | はい | はい | はい | はい |

### 単体テスト

すべてのテスト戦略の基盤となる、AEM アプリケーションの単体テストを実施することをお勧めします。このテストは、高速かつ頻繁な実行と早期の迅速なフィードバックの提供を目的としており、開発者ワークフロー、独自の CI/CD、AEM Cloud Service デプロイメントパイプラインに緊密に統合されています。

また、JUnit を使用して実装され、Maven で実行されます。AEMの単体テストと概要の例については ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/using#unit-tests) AEM プロジェクトアーキタイプの [ コアモジュールを参照してください。

### コード品質

この品質ゲートは標準で設定され、AEM アプリケーションコードで静的コード分析を実行します。

詳しくは、[コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md)および[カスタムコード品質ルール](/help/implementing/cloud-manager/custom-code-quality-rules.md)を参照してください。

### 製品テスト

製品機能テストは、オーサリングタスクやレプリケーションタスクなど、AEMのコア機能に対する安定した HTTP 統合テスト（IT）です。 アドビでは、これらを標準で提供、保守しています。これは、カスタムアプリケーションコードが AEM 製品のコア機能を破壊した場合に、カスタムアプリケーションコードに対する変更がデプロイされるのを防ぐためのものです。

実装には JUnit を使用し、Maven で実行され、公式の [AEM テストクライアント ](https://github.com/adobe/aem-testing-clients) に依存します。 製品テストスイートは
[オープンソースプロジェクト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)として維持され、ベストプラクティスに従っているため、テスト実装の出発点として適しています。

### カスタム機能テスト

顧客機能テストは、製品テストと同様に、JUnit で実装された HTTP 統合テスト（IT）であり、Maven を使用して実行され、公式の [AEM テストクライアント ](https://github.com/adobe/aem-testing-clients) 上に構築されます。

>[!NOTE]
>
>カスタム機能テストは、AEM アプリケーションの変更のデプロイメントおよびAEM製品のプッシュアップデートに使用される、実稼動パイプラインと実稼動以外（オプトイン）のパイプラインの両方で実行されます。 アプリケーションが適切に機能し、リリースの安全性を高める上で重要な役割を果たします。 顧客機能テストはそれぞれの内部プレリリース検証パイプラインで実行され、早期にフィードバックを得ることができます。

効率的なパイプラインの実行を維持するために、Adobeは主な機能と主要なユーザーインタラクションフローに重点を置き、約 15 分以内の機能的なテストランタイムを目指しています。 この時間を超える完全な機能テストスイートは、開発プロセス中に一般的な顧客検証パイプラインの一部として実行する必要があります。

例については、[オープンソースの製品テスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)または [AEM プロジェクトアーキタイプの it.tests モジュール](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests)を参照してください。

詳しくは、[Java 機能テスト](/help/implementing/cloud-manager/java-functional-testing.md)を参照してください。

### カスタム UI テスト

Adobeでは、お客様固有の開発に対するリスク制御を最大限に高めるために、重要な UI テストをAEM as a Cloud Serviceに取り込むことをお勧めします。 制限はあるが、顧客体験に与える影響を最大化することに焦点を当てる。

テストは、可能な限り揮発性に設計された Docker イメージにパッケージ化されます（Cypress、Selenium、Java およびJavaScriptをサポート）。 カスタム機能テストと同様に、同じ特性と目的に従います。

>[!NOTE]
>
>カスタム UI テストは、AEM アプリケーションの変更デプロイメントとAEM製品のプッシュアップデートに使用される、実稼動パイプラインと実稼動以外（オプトイン）のパイプラインの両方で実行されます。 これらは、アプリケーションの適切な機能を確保し、リリースの安全性を高めるために不可欠です。 また、顧客 UI テストは、各顧客の内部プレリリース検証パイプラインで実行され、早期にフィードバックを得るのに役立ちます。
>
>Selenium 以外のコンテナでは、[UI テストの節](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)で示した環境変数に基づいて HTTP プロキシを使用してテストを実行する必要があります。

パイプラインの実行を効率的に行うために、Adobeでは、主な機能と主なユーザーインタラクションフローに焦点を当てることをお勧めします。 この品質ゲートを超える完全な UI テストスイートは、一般的な顧客検証パイプラインの一部として実行する必要があります。 お客様の開発プロセスに組み込みます。

例として、[オープンソースのサンプルテスト](https://github.com/adobe/aem-test-samples/tree/aem-cloud/)または [AEMプロジェクトアーキタイプの ui.tests モジュール](/help/implementing/cloud-manager/ui-testing.md)を参照してください。

詳しくは、[カスタム UI テスト](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)を参照してください。

### エクスペリエンス監査

エクスペリエンス監査品質ゲートが、顧客の web ページに対して [Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) 監査を実行中です。

この品質ゲートは、AEM の標準で提供されていますが、デプロイメントパイプラインをブロックしていません。デフォルトでは、パブリッシュインスタンスのルートページ（`/`）に対して監査が実行されます。監査対象と見なされる最大 25 個のカスタムパスを設定して貢献できます。

詳しくは、[エクスペリエンス監査テスト](/help/implementing/cloud-manager/experience-audit-dashboard.md)を参照してください。

### 顧客の検証

顧客検証の品質ゲートは、顧客独自のテスト戦略と作業のプレースホルダーです。このテスト戦略と作業は、顧客のアプリケーションの変更が AEM クラウドデプロイメントパイプラインに到達する前に実行されます。

ここでは、好みのツールとフレームワークを選択できます。顧客機能テストとカスタム UI テストとは異なり、AEM as a Cloud Serviceに関連する制限はありません。 そのため、Adobeでは、長期間実行する機能テストと UI テストをここで実行することをお勧めします。

任意のツールやフレームワークを選ぶことができますが、Adobeでは、HTTP ベースの統合と UI テストを、カスタムの機能ゲートや UI テスト品質ゲートで使用されるツールやフレームワークに合わせることをお勧めします。 さらに、Adobeでは、AEM クラウド環境を緊密にミラーリングするために、[ 迅速な開発環境（RDE） ](/help/implementing/developing/introduction/rapid-development-environments.md) をローカルテスト戦略に組み込むことをお勧めします。

### 手動テスト

手動テストの品質ゲートは、手動テストを行うお客様向けのプレースホルダーです。AEMのクラウドパイプラインは手動でのテストをサポートしていないので、ローカルのテスト方法に組み込む必要があります。

手動テストの場合、追加の AEM Cloud Service 開発環境と統合すると便利です。
