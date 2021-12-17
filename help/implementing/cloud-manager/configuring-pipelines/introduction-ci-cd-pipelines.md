---
title: CI/CD パイプライン
description: このページでは、Cloud Manager CI/CD パイプラインについて説明します
index: true
source-git-commit: 3d48bd507305e7a1d3efa2b61123afdae1f52ced
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 3%

---


# Cloud Manager CI/CD パイプライン {#intro-cicd}

## はじめに {#introduction}

Cloud Manager の CI/CD パイプラインは、ソースコードリポジトリからのプルリクエスト、コード変更、リリースケイデンスに合わせた定期的なスケジュールなど、何らかのイベントでトリガーできます。

>[!NOTE]
>パイプラインを設定するには、次の操作を行う必要があります。
>* パイプラインを開始するトリガーを定義する
>* 実稼動デプロイメントを制御するパラメーターの定義
>* パフォーマンステストパラメーターの設定


Cloud Manager には、次の 2 種類のパイプラインがあります。

* [実稼動パイプライン](#prod-pipeline)
* [実稼動以外のパイプライン](#non-prod-pipeline)

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)


## 実稼動パイプライン {#prod-pipeline}

実稼動パイプラインは、調整された一連の手順を含む目的で構築されたパイプラインで、ソースコードを実稼動環境に送り込みます。 手順には、最初にすべてのステージ環境に構築、パッケージ化、テスト、検証、デプロイが含まれます。 言うまでもなく、実稼動パイプラインは、実稼動およびステージ環境セットを作成した場合にのみ追加できます。

参照： [実稼動パイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) を参照してください。


## 実稼動以外のパイプライン {#non-prod-pipeline}

非実稼動パイプラインは、コード品質スキャンの実行や、ソースコードの開発環境へのデプロイを目的としています。

参照： [実稼動以外のパイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) を参照してください。

## Cloud Manager の CI/CD パイプラインについて {#understand-pipelines}

Cloud Manager 内のすべてのパイプラインとその使用方法を次の表にまとめます。

| パイプラインタイプ | デプロイメントまたはコード品質 | ソースコード | 使用するタイミング | 使用する必要があるタイミングや理由 |
|--- |--- |--- |---|---|
| 実稼動または非実稼動 | デプロイメント | フロントエンド | 迅速な導入。<br>環境ごとに複数のフロントエンドパイプラインを設定し、同時に実行できます。<br>フロントエンドパイプラインのビルドは、ビルドをストレージにプッシュします。 html ページが提供されると、CDN がこのストレージを接触チャネルとして使用して提供するフロントエンドコード静的ファイルを参照する場合があります。 | 1 つ以上のクライアント側 UI アプリケーションを含むフロントエンドコードを排他的にデプロイする。 フロントエンドコードは、静的ファイルとして機能する任意のコードです。 これは、AEMが提供する UI コードとは別のものです。 Sites テーマ、顧客定義SPA、Firefly SPA、その他のソリューションが含まれます。<br>AEMバージョン2021.10.5933.20211012T154732Z 上にある必要があります<br>Sites を有効にする必要があります。 |
| 実稼動または非実稼動 | デプロイメント | フルスタック | フロントエンドパイプラインがまだ採用されていない場合。<br>フロントエンドコードをAEM Server コードと同時にデプロイする必要がある場合。 | 1 つ以上のAEMサーバーアプリケーションを同時に含むAEM Server コード（不変コンテンツ、Java コード、OSGi 設定、HTTPD/dispatcher 設定、repoinit、可変コンテンツ、フォント）をデプロイするには、次の手順を実行します。 |
| 実稼動以外 | コード品質 | フロントエンド | Cloud Manager を評価するよう設定する必要があります。 デプロイメントをおこなわずにビルドを成功させ、コードの品質を確保できます。<br>複数のパイプラインを設定および実行できます。 | フロントエンドコードでコード品質スキャンを実行します。 |
| 実稼動以外 | コード品質 | フルスタック | Cloud Manager を評価するよう設定する必要があります。 デプロイメントをおこなわずにビルドを成功させ、コードの品質を確保できます。<br>複数のパイプラインを設定および実行できます。 | フルスタックコードでコード品質スキャンを実行します。 |


次の図に、従来の単一のフロントエンドリポジトリまたは独立したフロントエンドリポジトリを設定した Cloud Manager パイプライン設定を示します。

![](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Cloud Manager フロントエンドパイプライン {#front-end}

フロントエンドパイプラインは、フロントエンドコードをデプロイするための高速フロントエンドパイプラインを有効にし、チームが設計と開発のプロセスを合理化するのに役立ちます。 この差別化されたパイプラインは、JavaScript と CSS をテーマとしてAEM配布レイヤーにデプロイするので、AEMランタイムから配信されるページから参照できる新しいテーマバージョンが作成されます。 フロントエンドコードは、静的ファイルとして機能する任意のコードです。 これは、AEMが提供する UI コードとは別のものです。 Sites テーマ、顧客定義SPA、Firefly SPA、その他のソリューションが含まれます。

>[!IMPORTANT]
>AEM版である必要があります `2021.10.5933.20211012T154732Z ` を使用して、フロントエンドパイプラインを活用します。

>[!NOTE]
>デプロイメントマネージャーの役割としてログインしたユーザーは、複数のフロントエンドパイプラインを同時に作成および実行できます。 ただし、プログラムあたり最大 300 個のパイプライン（すべてのタイプ）が制限されます。

フロントエンドコード品質またはフロントエンドデプロイメントパイプラインのいずれかを指定できます。

### フロントエンドパイプラインを設定する前に {#before-start}

フロントエンドパイプラインの設定を開始する前に、 [AEMクイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md) 使いやすいAEM Quick Site Creation ツールを使用してエンドツーエンドのワークフローを実現する このドキュメントサイトは、AEMサイトのフロントエンド開発を合理化し、AEMのバックエンドに関する知識を持たずに、すばやくサイトをカスタマイズするのに役立ちます。

### フロントエンドパイプラインの設定 {#configure-front-end}

フロントエンドパイプラインの設定方法については、次を参照してください。

* [実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### フロントエンドパイプラインを使用したサイトの開発 {#developing-with-front-end-pipeline}

フロントエンドパイプラインを使用すると、フロントエンド開発者により多くの独立性が与えられ、開発プロセスは大幅な速度を得ることができます。

参照： [このドキュメント](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) このプロセスの機能と、このプロセスを最大限に活用するために考慮すべきいくつかの検討事項について説明します。

## フルスタックパイプライン {#full-stack-pipeline}

フルスタックパイプラインでは、バックエンド、フロントエンド、HTTPD/Dispatcher 設定を同時にデプロイするオプションをユーザーに提供します。  AEMクライアントライブラリとしてパッケージ化されたフロントエンドコード (JavaScript/CSS) を含む、AEMランタイムにコードとコンテンツをデプロイします。 Web 層パイプラインが構成されていない場合は、Web 層の構成をデプロイする可能性があります。 これは「uber」パイプラインを表しますが、フロントエンドパイプラインと Web 層設定パイプラインを介して、フロントエンドコードまたは Dispatcher 設定を排他的にデプロイするオプションをユーザーに提供します。
フルスタックタイプ（コード品質）またはフルスタックタイプ（デプロイメントパイプライン）を使用できます。

次の制限が適用されます。

1. パイプラインを設定または実行するには、ユーザーがデプロイメントマネージャーとしてログインする必要があります。

1. 環境ごとにフルスタックパイプラインはいつでも 1 つしか存在できません。

1. ユーザーは、環境のフルスタックパイプラインを Dispatcher 設定を無視するか無視しないかを設定できます。その環境に対応する Web 層設定パイプラインが存在しない場合。

1. 環境のフルスタックパイプラインは、その環境に対応する Web 層設定パイプラインが存在する場合、Dispatcher 設定を無視します。


### フルスタックパイプラインの設定 {#configure-full-stack}

フルスタックパイプラインの設定方法については、以下を参照してください。

* [実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)