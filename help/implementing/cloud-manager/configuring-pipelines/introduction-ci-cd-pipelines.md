---
title: CI／CD パイプライン
description: Cloud Manager の CI/CD パイプラインと、それらを使用してコードを効率的にデプロイする方法について説明します。
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 7%

---

# Cloud Manager CI/CD パイプライン {#intro-cicd}

Cloud Manager の CI/CD パイプラインと、それらを使用してコードを効率的にデプロイする方法について説明します。

## はじめに {#introduction}

Cloud Manager の CI/CD パイプラインは、ソースリポジトリからコードを構築し、環境にデプロイするメカニズムです。 パイプラインは、ソースコードリポジトリからのプル要求（コード変更など）や、リリースケイデンスに合わせた定期的なスケジュールで、イベントによってトリガーできます。

パイプラインを設定するには、次の操作をおこなう必要があります。

* パイプラインを開始するトリガーを定義します。
* 実稼動デプロイメントを制御するパラメーターを定義します。
* パフォーマンステストのパラメーターを設定します。

Cloud Manager には、次の 2 種類のパイプラインが用意されています。

* [実稼動パイプライン](#prod-pipeline)
* [実稼動以外のパイプライン](#non-prod-pipeline)

![パイプラインのタイプ](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## 実稼動パイプライン {#prod-pipeline}

実稼動パイプラインは、実稼動用にソースコードをデプロイするために調整された一連の手順を含む、専用のパイプラインです。 手順には、最初のビルド、パッケージ化、テスト、検証およびすべてのステージング環境へのデプロイが含まれます。 したがって、実稼動パイプラインは、一連の実稼動環境とステージング環境を作成した場合にのみ追加できます。

>[!TIP]
>
>ドキュメントを参照します。 [実稼動パイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) を参照してください。

## 実稼動以外のパイプライン {#non-prod-pipeline}

非実稼動パイプラインは、主にコード品質スキャンの実行や、ソースコードの開発環境へのデプロイを目的としています。

>[!TIP]
>
>ドキュメントを参照します。 [実稼動以外のパイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) を参照してください。

## コードソース {#code-sources}

パイプラインは、実稼動環境と非実稼動環境に加えて、デプロイするコードのタイプで区別できます。

* **[フルスタックパイプライン](#full-stack-pipeline)** - 1 つ以上のAEMサーバーアプリケーションを含むバックエンドとフロントエンドのコードビルドを、HTTPD/Dispatcher 設定と共に同時にデプロイします
* **[フロントエンドパイプライン](#front-end)** - 1 つ以上のクライアント側 UI アプリケーションを含むフロントエンドコードビルドをデプロイする
* **[Web 層設定パイプライン](#web-tier-config-pipelines)** - HTTPD/Dispatcher 設定をデプロイします

詳しくは、このドキュメントで後述します。

### Cloud Manager の CI／CD パイプラインについて {#understand-pipelines}

次の表に、Cloud Manager で使用可能なすべてのパイプラインとその使用状況をまとめます。

| パイプラインタイプ | デプロイメントまたはコード品質 | ソースコード | 目的 | 備考 |
|--- |--- |--- |---|---|
| 実稼動または非実稼動 | デプロイメント | フルスタック | HTTPD/Dispatcher 設定と共に、バックエンドとフロントエンドのコードビルドを同時にデプロイします | フロントエンドコードをAEMサーバーコードと同時にデプロイする必要がある場合。<br>フロントエンドパイプラインまたは Web 層設定パイプラインがまだ採用されていない場合。 |
| 実稼動または非実稼動 | デプロイメント | フロントエンド | 1 つ以上のクライアント側 UI アプリケーションを含むフロントエンドコードビルドをデプロイします | 複数の同時フロントエンドパイプラインをサポート<br>フルスタックデプロイメントよりもはるかに高速 |
| 実稼動または非実稼動 | デプロイメント | Web 階層設定 | HTTPD/Dispatcher 設定をデプロイします | 数分でデプロイ |
| 実稼動以外 | コード品質 | フルスタック | デプロイメントなしでフルスタックコードでコード品質スキャンを実行します | 複数のパイプラインをサポート |
| 実稼動以外 | コード品質 | フロントエンド | デプロイメントを使用せずに、フロントエンドコードでコード品質スキャンを実行します | 複数のパイプラインをサポート |
| 実稼動以外 | コード品質 | Web 階層設定 | デプロイメントを使用せずに、Dispatcher 設定でコード品質スキャンを実行します | 複数のパイプラインをサポート |

次の図は、従来の単一のフロントエンドリポジトリ、または独立したフロントエンドリポジトリでの Cloud Manager のパイプライン設定を示しています。

![Cloud Manager パイプライン設定](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## フルスタックパイプライン {#full-stack-pipeline}

フルスタックパイプラインは、バックエンドコード、フロントエンドコード、Web 層の設定をAEM Runtime に同時にデプロイします。

* バックエンドコード — Java コード、OSGi 設定、repoinit、可変コンテンツなどの不変コンテンツ
* フロントエンドコード — JavaScript、CSS、フォントなどのアプリケーション UI リソース
* Web 層設定 — HTTPD/Dispatcher 設定

フルスタックパイプラインは「uber」パイプラインを表し、すべてを一度に実行します。また、フロントエンドパイプラインと Web 層設定パイプラインを介して、それぞれフロントエンドコードまたは Dispatcher 設定をデプロイするオプションをユーザーに提供します。

フルスタックパイプラインパッケージフロントエンドコード (JavaScript/CSS) を [AEMクライアントライブラリ。](/help/implementing/developing/introduction/clientlibs.md)

フルスタックパイプラインでは、 [web 層設定パイプライン](#web-tier-config-pipelines) が設定されていません。

次の制限が適用されます。

* ユーザーは、 **デプロイメントマネージャー** の役割を使用して、パイプラインを設定または実行できます。
* いつでも、環境ごとに 1 つのフルスタックパイプラインしか存在できません。

また、 [web 層設定パイプライン。](#web-tier-config-pipelines)

* 対応する Web 層設定パイプラインが存在する場合、環境のフルスタックパイプラインは Dispatcher 設定を無視します。
* 環境に対応する Web 層設定パイプラインが存在しない場合、ユーザーはフルスタックパイプラインに Dispatcher 設定を含めるか無視するかを設定できます。

フルスタックパイプラインには、コード品質のパイプラインまたはデプロイメントを使用できます。

## フロントエンドパイプライン {#front-end}

フロントエンドコードは、静的ファイルとして提供される任意のコードです。 AEMが提供する UI コードとは別のもので、サイトテーマ、顧客定義SPA、Firefly SPA、その他のソリューションを含めることができます。

フロントエンドパイプラインは、バックエンド開発の非同期的なフロントエンドコードの迅速なデプロイを可能にし、チームが設計と開発プロセスを合理化するのに役立ちます。 この専用パイプラインは、JavaScript と CSS をテーマとしてAEM配布レイヤーにデプロイするので、AEMが配信するページから参照できる新しいテーマバージョンが作成されます。

>[!IMPORTANT]
>
>AEM版である必要があります `2021.10.5933.20211012T154732Z ` AEM Sitesがフロントエンドパイプラインの活用を有効にしている場合は、以降で利用できます。

>[!NOTE]
>
>ユーザーが **デプロイメントマネージャー** の役割は、複数のフロントエンドパイプラインを同時に作成および実行できます。
>
>ただし、プログラムごとに（すべてのタイプで）最大 300 パイプラインの制限があります。これには、フロントエンドコード品質またはフロントエンドデプロイメントパイプラインが含まれます。

フロントエンドパイプラインには、コード品質のパイプラインやデプロイメントを使用できます。

### フロントエンドパイプラインを設定する前に {#before-start}

フロントエンドパイプラインを設定する前に、 [AEMクイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md) を参照してください。 このジャーニーは、フロントエンド開発を合理化し、バックエンドのAEMに関する知識を持たずに、すばやくサイトをカスタマイズできるようにします。

### フロントエンドパイプラインの設定 {#configure-front-end}

フロントエンドパイプラインの設定方法については、次のドキュメントを参照してください。

* [実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### フロントエンドパイプラインを使用したサイトの開発 {#developing-with-front-end-pipeline}

フロントエンドパイプラインを使用すると、フロントエンド開発者により多くの独立性が与えられ、開発プロセスを高速化できます。

ドキュメントを参照してください [フロントエンドパイプラインを使用したサイトの開発](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) このプロセスの機能と、このプロセスを最大限に活用するために考慮すべきいくつかの検討事項について説明します。

### フルスタックパイプラインの設定 {#configure-full-stack}

フルスタックパイプラインの設定方法については、次のドキュメントを参照してください。

* [実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)


## Web 層設定パイプライン {#web-tier-config-pipelines}

Web 層設定パイプラインを使用すると、HTTPD/Dispatcher 設定を他のコード変更と分離して、AEMランタイムに排他的にデプロイできます。 Dispatcher 設定の変更のみをデプロイするユーザーを提供する、合理化されたパイプラインです。これは、数分で迅速にデプロイする方法です。

>[!TIP]
>
>Web 層設定パイプラインを使用すると、Web 設定をフルスタックパイプラインと同じソースの場所に保存するか、プロジェクトに適した構造に応じて別の場所に保存するかを選択できます。

次の制限が適用されます。

* AEM版である必要があります `2021.12.6151.20211217T120950Z` Web 層設定パイプラインを利用する場合と、それ以降の場合があります。
* 必ず [dispatcher ツールの柔軟なモードのオプトイン](/help/implementing/dispatcher/disp-overview.md#validation-debug) web 層設定パイプラインを活用する。
* ユーザーは、 **デプロイメントマネージャー** の役割を使用して、パイプラインを設定または実行できます。
* 環境ごとに、1 つの Web 層設定パイプラインのみを使用できます。
* 対応するフルスタックパイプラインが実行中の場合、ユーザーは Web 層設定パイプラインを設定できません。
* Web 層構造は、ドキュメントで定義されている柔軟モード構造に従う必要があります [クラウド内の Dispatcher。](/help/implementing/dispatcher/disp-overview.md#validation-debug)

さらに、 [フルスタックパイプライン](#full-stack-pipeline) Web 層パイプラインを導入する際にが動作します。

* Web 層設定パイプラインが環境用に設定されていない場合、ユーザーは、実行およびデプロイ時に Dispatcher 設定を含めるか無視するように、対応するフルスタックパイプラインを設定する際に選択をおこなうことができます。
* ある環境に対して Web 層設定パイプラインを設定すると、対応するフルスタックパイプライン（存在する場合）では、実行とデプロイメント中に Dispatcher 設定が無視されます。
* Web 層設定パイプラインを削除すると、対応するフルスタックパイプラインがリセットされ、実行中に Dispatcher 設定がデプロイされます。

Web 層設定パイプラインは、コード品質のタイプまたはデプロイメントのタイプにすることができます。

### Web 層設定パイプラインの設定 {#configure-web-tier-config-pipelines}

Web 層設定パイプラインの設定方法については、次のドキュメントを参照してください。

* [実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)
