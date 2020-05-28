---
title: 実行段階
description: 実行段階
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 15%

---


# 実行 {#execution-phase}

実行フェーズを開始する前に、クラウドサービスにオンボードする必要があります。 また、Cloud ManagerはAEMクラウドサービスにコードをデプロイする唯一のメカニズムなので、十分に理解しておく必要があります。

Cloud Managerを使用すると、組織はクラウド内のAEMを自己管理できます。 このサービスには継続的統合および継続的配信（CI／CD）フレームワークが備わっているので、IT チームや実装パートナーはパフォーマンスやセキュリティを妥協することなくカスタマイズや更新を迅速に配信できます。

詳しくは、次のリソースを参照してください。

* [クラウドサービスとしてのExperience Managerのオンボーディングを参照し](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/onboarding/home.html) 、Experience Managerのクラウドサービスとしてのオンボーディングに関するセルフヘルプリソースを理解してください。

* [GitとAdobe Cloud Managerの統合](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) 」を参照して、単一のGitリポジトリを使用してコードをデプロイする方法を確認してください。

* [クラウドサービス設定としてのAdobe Experience](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/security/ims-support.html#aem-configuration) （管理コンソールでの製品とユーザーアクセスの管理）を参照してください。


## 概要 {#introduction}

クラウドサービスへのトランジションの正確な手順は、購入したシステムと、従うソフトウェア開発のライフサイクル慣行によって異なります。

次の図に、実行フェーズに関する主な手順を示します。

![画像](/help/move-to-cloud-service/assets/exec-image1.png)

## コンテンツ転送 {#content-transfer}

現在のAEMインスタンスからクラウドサービスインスタンスにコンテンツを転送するには、アドビのコンテンツ転送ツールを使用します。

このツールを使用すると、ソースAEMインスタンスからAEMクラウドサービスインスタンスに転送するコンテンツのサブセットを指定できます。

>[!NOTE]
>クラウドサービスを利用する前に、最終的な差分コンテンツ転送のためのコンテンツの固定期間を短縮するために、頻繁に差分コンテンツのトップアップを行うことをお勧めします。

詳しくは、「 [コンテンツ転送ツール](/help/move-to-cloud-service/content-transfer-tool/overview-content-transfer-tool.md) 」を参照してください。

>[!IMPORTANT]
>コンテンツ転送ツールの最小システム要件は、AEM 6.3以降およびJAVA 8です。 AEMより前のバージョンを使用している場合は、コンテンツ転送ツールを使用するには、コンテンツリポジトリをAEM 6.5にアップグレードする必要があります。

## コードリファクタリング {#code-refactor}

AEMでクラウドサービスとしてコードを開発および実行するには、考慮事項の変更が必要です。 コードは回復力が必要であること、特にインスタンスはいつでも停止する可能性があるので注意が必要です。  Cloud Service で実行するコードは、常にクラスター内で実行されていることを認識している必要があります。つまり、常に複数のインスタンスが実行されています。

AEM Mavenプロジェクトに、クラウドサービスとしてのAEMとの互換性を持たせるために、一部の変更が必要になります。 クラウドサービスとしてのAEMでは、AEMに展開するために、 *コンテンツ* と ** コードを個別のパッケージに分離する必要があります。

* `/apps` と `/libs` は AEM の不変領域と見なされます。AEM の起動後（例：実行時）に変更（作成、更新、削除）できないからです。実行時に不変領域を変更しようとすると失敗します。

* リポジトリ内のそれ以外の領域（`/content`、`/conf`、`/var`、`/home`、`/etc`、`/oak:index`、`/system`、`/tmp` など）はすべて可変領域です。つまり、実行時に変更できます。

Refer to [Recommended Package Structure](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure) for more details.

クラウドサービスとしてAEMで開発する場合は、注意が必要な開発ガイドラインがいくつかあります。 詳しくは、「 [AEMをクラウドサービスの開発に関するガイドライン](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) 」を参照してください。

計画段階で、クラウドサービスとの互換性を維持するためにリファクタリングする必要がある領域のリストが必要です。 また、コードをリファクタリングして最適化し、クラウドサービスに移行する方法の詳細については、 [開発ガイドライン](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) （英語）も参照してください。

コードリファクタリングタスクの一部を高速化するために、次のツールを使用できます。

* [アセットワークフローの移行](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [ディスパッチャーコンバーター](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [最新化ツール](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md)

コードをCloud Manager Gitを介してクラウドサービス環境にプッシュする前に、コードをローカルでリファクタリングおよびテストすることをお勧めします。

詳しくは、 [AEM SDK](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) （SDKのドキュメント）を参照してください。

その他のリソースを以下に示します。

* ディスパッチャーSDKのインストールを監視して、ディスパッチャーSDKのインストール方法を理解します。

   > [!VIDEO](https://video.tv.adobe.com/v/30601)

* ディスパッチャーSDKの設定を見て、ディスパッチャーSDKの設定方法を理解してください。

   > [!VIDEO](https://video.tv.adobe.com/v/30602)

* 「 [ローカル開発セットアップ](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) 」ドキュメントを確認し、ローカル開発環境を設定します。


トランジションの遍歴の一環として、アクティブなAEM上での継続的なコード開発を管理し、コードリファクタリングタスクと共に管理するには、Mavenプロジェクトの再構築が完了して、クラウドサービスとしてのAEMとの互換性を維持するまで、コードの停止期間を設定することをお勧めします。

プロジェクトの再構築が完了したら、この新しい構造に基づいて新しいコード開発を再開できます。 これにより、コードのデプロイメントおよびテスト中にCloud Managerのパイプラインエラーが発生することがなくなります。

>[!NOTE]
>コンテンツ転送とコードリファクタリングのタスクは、順番に実行されるわけではありません。 これらのタスクは互いに独立して行うことができます。 ただし、クラウドサービス環境でコンテンツが正しくレンダリングされるようにするには、正しいプロジェクト構造が必要です。

## コードの導入とテストのベストプラクティス {#best-practices}

Cloud Services 用 Cloud Manager のパイプライン実行では、ステージ環境に対するテストの実行をサポートしています。

テストスクリプトの作成方法と推奨範囲を50 %以上にする方法については、 [コード品質テスト](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing) （英語）を参照してください。

また、AEMエンジニアリングのベストプラクティスに基づいて作成されたCloud Managerが実行するカスタムコード品質ルールについて詳しくは、 [「カスタムコード品質ルールについて](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/custom-code-quality-rules.html) 」を参照してください。

Cloud Managerの使用は、クラウドサービス環境にコードをデプロイする唯一のメカニズムです。

次のリソースに従って、Cloud Managerを使用してコードを管理およびデプロイする方法を学習します。

* [環境の管理](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [CI/CD パイプラインの設定](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [コードのデプロイ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)

## Go Live準備のベストプラクティス {#go-live}

クラウドサービスとしてのAEMのGo Liveをスムーズかつ成功に導くために、次の手順を実行することを検討する必要があります。

* コードとコンテンツの固定期間のスケジュール
* 最終コンテンツのトップアップの実行
* 完全なテスト反復
* パフォーマンスとセキュリティテストの実行
* カットオーバー
