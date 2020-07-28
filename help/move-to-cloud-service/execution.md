---
title: 実行段階
description: 実行段階
translation-type: tm+mt
source-git-commit: 0dd05c1f6dc197daf154d4df6e6661e00455b233
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 100%

---


# 実行 {#execution-phase}

実行段階を開始する前に、Cloud Service にオンボーディングする必要があります。また、Cloud Manager に習熟しておく必要もあります。Cloud Manager は AEM Cloud Service にコードをデプロイするための唯一のメカニズムだからです。

Cloud Manager を使用すると、組織がクラウド内の AEM を自己管理できます。このサービスには継続的統合および継続的配信（CI／CD）フレームワークが備わっているので、IT チームや実装パートナーはパフォーマンスやセキュリティを妥協することなくカスタマイズや更新を迅速に配信できます。

詳しくは、以下のリソースを参照してください。

* [Adobe Experience Manager as a Cloud Service のオンボーディング](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/onboarding/home.html)：Adobe Experience Manager as a Cloud Service のオンボーディングに関するセルフヘルプリソースについて

* [Git と Adobe Cloud Manager の統合](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html)：1 つの Git リポジトリを使用してコードをデプロイする方法について

* [Adobe Experience Manager as a Cloud Service の設定](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/security/ims-support.html#aem-configuration)：Admin Console での製品とユーザーアクセスの管理


## 概要 {#introduction}

Cloud Service への移行の正確な手順は、購入したシステムと準拠するソフトウェア開発ライフサイクル手法によって異なります。

実行段階に必要になる主なステップを次の図に示します。

![画像](/help/move-to-cloud-service/assets/exec-image1.png)

## コンテンツ転送 {#content-transfer}

現在の AEM インスタンスから Cloud Service インスタンスにコンテンツを転送するには、アドビのコンテンツ転送ツールを使用します。

このツールを使用すると、ソース AEM インスタンスから AEM Cloud Service インスタンスに転送するコンテンツサブセットを指定できます。

>[!NOTE]
>差分コンテンツ追加を頻繁におこなって、Cloud Service での運用を開始する前におこなう最後の差分コンテンツ転送に必要なコンテンツフリーズ期間を短縮することをお勧めします。

詳しくは、[コンテンツ転送ツール](/help/move-to-cloud-service/content-transfer-tool/overview-content-transfer-tool.md)を参照してください。

>[!IMPORTANT]
>コンテンツ転送ツールに必要なシステム構成は、AEM 6.3 以降と Java 8 です。使用している AEM のバージョンがこれより古い場合、コンテンツ転送ツールを使用するには、コンテンツリポジトリを AEM 6.5 にアップグレードする必要があります。

## コードリファクタリング {#code-refactor}

AEM as a Cloud Service でコードを開発および実行するには、考え方を変える必要があります。インスタンスはいつ停止するかわからないので、コードには特に回復力が必要である点に留意してください。Cloud Service で実行するコードは、常にクラスター内で実行されていることを認識している必要があります。つまり、常に複数のインスタンスが実行されています。

AEM as a Cloud Service に対応するために、AEM Maven プロジェクトに変更がいくつか必要になります。AEM as a Cloud Service では、AEM にデプロイするために、*コンテンツ*&#x200B;と&#x200B;*コード*&#x200B;を別個のパッケージに分離する必要があります。

* `/apps` と `/libs` は AEM の不変領域と見なされます。AEM の起動後（例：実行時）に変更（作成、更新、削除）できないからです。実行時に不変領域を変更しようとすると失敗します。

* リポジトリ内のそれ以外の領域（`/content`、`/conf`、`/var`、`/home`、`/etc`、`/oak:index`、`/system`、`/tmp` など）はすべて可変領域です。つまり、実行時に変更できます。

詳しくは、[推奨されるパッケージ構造](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure)を参照してください。

AEM as a Cloud Service で開発する際に留意する必要がある開発ガイドラインがさらにいくつかあります。詳しくは、[AEM as a Cloud Service の開発ガイドライン](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/development-guidelines.html)を参照してください。

Cloud Service に対応するためにリファクタリングする必要がある領域のリストを計画段階で作成する必要があります。また、Cloud Service に移行するためにコードをリファクタリングし最適化する方法について詳しくは、[開発ガイドライン](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/development-guidelines.html)を参照してください。

コードリファクタリングタスクの一部を高速化するために、次のツールを使用できます。

* [アセットワークフロー移行](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [Dispatcher コンバーター](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [AEM Modernization Tools](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md)

Cloud Manager Git を介して Cloud Service 環境にコードをプッシュする前に、コードをリファクタリングしローカルでテストすることをお勧めします。

詳しくは、[AEM SDK](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) のドキュメントを参照してください。

その他のリソースを以下に示します。

* Dispatcher SDKのインストール方法については、「Install Dispatcher SDK」（Dispatcher SDK のインストール）を視聴してください。

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* Dispatcher SDKの設定方法については、「Configure Dispatcher SDK」（Dispatcher SDK の設定）を視聴してください。

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

* ローカル開発環境を設定するには、[Local Development Environment Set up](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)（ローカル開発環境のセットアップ）を参照してください。


移行プロセスの一環として、アクティブな AEM 上で進行中のコード開発を、コードリファクタリングタスクと共に管理するには、AEM as a Cloud Service に対応するための Maven プロジェクトの再構築が完了するまで、コードの凍結期間を予定しておくことをお勧めします。

プロジェクトの再構築が完了したら、この新しい構造に基づいて新しいコード開発を再開できます。これにより、コードのデプロイメントおよびテスト中に発生する Cloud Manager パイプラインのエラーを減らすことができます。

>[!NOTE]
>コンテンツ転送タスクとコードリファクタリングタスクは、順番に実行しなくてもかまいません。これらのタスクは互いに独立に実行することができます。ただし、Cloud Service 環境でコンテンツが正常にレンダリングされるようにするには、正しいプロジェクト構造が必要です。

## コードのデプロイメントとテストのベストプラクティス {#best-practices}

Cloud Services 用 Cloud Manager のパイプライン実行では、ステージ環境に対するテストの実行をサポートしています。

テストスクリプトの作成と 50 %以上の推奨コードカバレッジについては、[コード品質テスト](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing)を参照してください。

さらに、AEM エンジニアリングのベストプラクティスに基づいて作成され Cloud Manager で実行されるカスタムコード品質ルールについて詳しくは、[カスタムコード品質ルールについて](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/using-cloud-manager/custom-code-quality-rules.html)を参照してください。

Cloud Manager を使用する以外に、Cloud Service 環境にコードをデプロイする手段はありません。

Cloud Manager を使用してコードを管理およびデプロイする方法については、次のリソースを参照してください。

* [環境の管理](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [CI/CD パイプラインの設定](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [コードのデプロイ](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)

## 運用開始準備のベストプラクティス {#go-live}

AEM as a Cloud Service 上でうまくスムーズに運用を開始できるようにするには、次の手順を実行することを検討してください。

* コードとコンテンツの凍結期間のスケジュール設定
* 最終コンテンツ追加の実行
* 反復テストの完了
* パフォーマンステストとセキュリティテストの実行
* カットオーバー
