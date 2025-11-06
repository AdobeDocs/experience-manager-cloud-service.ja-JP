---
title: CI/CD パイプラインの概要
description: Cloud Manager の CI/CD パイプラインと、CI/CD パイプラインを使用してコードを効率的にデプロイする方法について説明します。
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1546'
ht-degree: 96%

---


# Cloud Manager CI/CD パイプライン {#intro-cicd}

Cloud Manager の CI/CD パイプライン（継続的統合／継続的配信）と、CI/CD パイプラインを使用してコードを効率的にデプロイする方法について説明します。

## CI/CD パイプラインの概要 {#introduction}

Cloud Manager の CI／CD パイプラインは、ソースリポジトリーからコードを作成して環境にデプロイするためのメカニズムです。パイプラインは、Git などのソースコードリポジトリからのプルリクエスト（つまり、コード変更）などのイベントでトリガーできます。または、リリース頻度に合わせた定期的なスケジュールでトリガーすることもできます。

パイプラインを設定するには、次の操作を行う必要があります。

* パイプラインを開始するトリガーの定義。
* 実稼動デプロイメントを制御するパラメーターの定義。
* パフォーマンステストパラメーターの設定

Cloud Manager には、次の 2 種類のパイプラインが用意されています。

* [実稼動パイプライン](#prod-pipeline)
* [実稼動以外のパイプライン](#non-prod-pipeline)

![パイプラインのタイプ](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## 実稼動パイプライン {#prod-pipeline}

実稼動パイプラインは、ソースコードを実稼動用にデプロイするための調整された一連のステップで構成される専用のパイプラインです。これらのステップには、ビルド、パッケージ化、テスト、検証およびデプロイがあり、最初はすべてステージング環境で行われます。したがって、実稼動パイプラインは、実稼動環境とステージング環境のセットを作成した場合にのみ追加できます。

>[!TIP]
>
>詳しくは、[実稼動パイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)を参照してください。

## 実稼動以外のパイプライン {#non-prod-pipeline}

実稼動以外のパイプラインは、主にコード品質スキャンの実行や開発環境へのソースコードのデプロイに役立ちます。

>[!TIP]
>
>詳しくは、[実稼動以外のパイプライン](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)を参照してください。

## コードのソース {#code-sources}

パイプラインは、本番環境と本番以外の環境に加えて、デプロイするコードのタイプによっても異なる場合があります。

* **[フルスタックパイプライン](#full-stack-pipeline)** - 1 つ以上の AEM サーバーアプリケーションを含んだバックエンドおよびフロンエンドコードビルドを HTTPD／Dispatcher 設定と共に同時にデプロイします。
* **[設定パイプライン](#config-deployment-pipeline)** - ログ転送やパージ関連のメンテナンスタスクなどの機能の設定をすばやくデプロイできます。また、Web アプリケーションファイアウォール（WAF）ルールを含むトラフィックフィルタールールなど、様々な CDN（コンテンツ配信ネットワーク）設定も含まれます。さらに、リクエストと応答の変換、接触チャネルセレクター、クライアントサイドリダイレクト、エラーページ、CDN キー、パージ API キー、基本認証を管理できます。詳しくは、[設定パイプラインの使用](/help/operations/config-pipeline.md)を参照してください。
* **[フロントエンドパイプライン](#front-end)** - 1 つ以上のクライアントサイドユーザーインターフェイスアプリケーションを含んだフロントエンドコードビルドをデプロイします。
* **[Web 階層設定パイプライン](#web-tier-config-pipelines)** - HTTPD／Dispatcher 設定をデプロイします。

これらのパイプラインタイプについて詳しくは、このドキュメントの後半で説明します。

### Cloud Manager の CI/CD パイプラインについて {#understand-pipelines}

Cloud Manager で使用できるパイプラインとその用途を次の表にまとめます。

| パイプラインタイプ | デプロイメントまたはコード品質 | ソースコード | 目的 | メモ |
| --- | --- | --- | --- | ---|
| 実稼動または実稼動以外 | デプロイメント | フルスタック | バックエンドおよびフロンエンドコードビルドと HTTPD／Dispatcher 設定を同時にデプロイ | フロントエンドコードを AEM サーバーコードと同時にデプロイする必要がある場合に使用されます。フロントエンドパイプラインまたは web 階層設定パイプラインがまだ導入されていない場合に使用されます。 |
| 実稼動または実稼動以外 | デプロイメント | フロントエンド | 1 つ以上のクライアントサイド UI アプリケーションを含んだフロントエンドコードビルドをデプロイ | 複数の同時フロントエンドパイプラインをサポート<br>フルスタックデプロイメントよりはるかに高速。 |
| 実稼動または実稼動以外 | デプロイメント | Web 階層設定 | HTTPD／Dispatcher 設定をデプロイ | 数分でデプロイ |
| 実稼動または実稼動以外 | デプロイメント | Config | CDN、ログ転送、パージメンテナンスタスクに関連する[多くの機能の設定](/help/operations/config-pipeline.md)をデプロイ | 数分でデプロイ |
| 実稼動以外 | コード品質 | フルスタック | デプロイメントなしでフルスタックコードに対してコード品質スキャンを実行 | 複数のパイプラインをサポート |
| 実稼動以外 | コード品質 | フロントエンド | デプロイメントなしでフロントエンドコードに対してコード品質スキャンを実行 | 複数のパイプラインをサポート |
| 実稼動以外 | コード品質 | Web 階層設定 | デプロイメントなしで Dispatcher 設定に対してコード品質スキャンを実行 | 複数のパイプラインをサポート |

従来の単一のフロントエンドリポジトリーまたは独立したフロントエンドリポジトリーをセットアップした Cloud Manager パイプライン設定を次の図に示します。

![Cloud Manager パイプライン設定](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## フルスタックパイプライン {#full-stack-pipeline}

フルスタックパイプラインでは、バックエンドコード、フロントエンドコードおよび web 階層設定を、すべて同時に AEM ランタイムにデプロイします。

* バックエンドコード - Java コード、OSGi 設定、repoinit などの不変コンテンツと可変コンテンツ
* フロントエンドコード - JavaScript、CSS、フォントなどのアプリケーション UI リソース
* Web 階層設定 - HTTPD／Dispatcher 設定

フルスタックパイプラインは、「uber」パイプラインを表します。すべてを同時に処理できる一方、ユーザーがフロントエンドコードと Dispatcher の設定を個別にデプロイすることもできます。このデプロイメントは、フロントエンドパイプラインと web 階層設定パイプラインをそれぞれ通じて行われます。

フルスタックパイプラインでは、フロントエンドコード（JavaScript／CSS）を [AEM クライアントライブラリ](/help/implementing/developing/introduction/clientlibs.md)としてパッケージ化します。

フルスタックパイプラインは、[web 階層設定パイプライン](#web-tier-config-pipelines)が設定されていない場合、web 階層設定をデプロイする場合があります。

次の制限が適用されます。

* パイプラインを設定または実行するには、ユーザーが&#x200B;**デプロイメントマネージャー**&#x200B;の役割でログインしている必要があります。
* フルスタックパイプラインは、常に 1 つの環境に 1 つしか存在できません。

さらに、[web 階層設定パイプライン](#web-tier-config-pipelines)の導入を選択した場合は、フルスタックパイプラインがどのように動作するかを認識しておいてください。

* 環境のフルスタックパイプラインは、対応する web 階層設定パイプラインが存在する場合、Dispatcher 設定を無視します。
* 環境に対応する web 階層設定パイプラインが存在しない場合、ユーザーは、Dispatcher 設定を含めるまたは無視するようにフルスタックパイプラインを設定できます。

フルスタックパイプラインは、コード品質パイプラインとすることも、デプロイメントパイプラインとすることもできます。

### 実稼動以外のパイプラインの設定 {#configure-full-stack}

[実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code)を参照してください。
[実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)を参照してください。

## パイプラインの設定 {#config-deployment-pipeline}

設定パイプラインを使用すると、ログ転送、パージ関連のメンテナンスタスク、トラフィックフィルタールール（WAF（Web アプリケーションファイアウォール）ルールなど）を含む様々な CDN 設定の設定をすばやくデプロイできます。さらに、リクエストと応答の変換、オリジンセレクター、クライアントサイドリダイレクト、エラーページ、顧客管理 CDN キー、パージ API キー、基本認証を管理できます。

サポートされている機能の包括的なリストと、リポジトリ内の設定を適切にデプロイするために設定を管理する方法については、[設定パイプラインの使用](/help/operations/config-pipeline.md)を参照してください。

>[!NOTE]
>
>Edge Delivery設定パイプラインには、開発環境、ステージング環境および実稼動環境は分離されません。 AEM as a Cloud Serviceでは、変更は開発層、ステージ層、実稼動層を通じて進みます。 これに対し、Edge Delivery設定パイプラインは、Cloud Managerに登録されたすべてのEdge Delivery Sites ドメインに設定を直接適用します。 詳しくは、[Edge Delivery パイプラインの追加 &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md) を参照してください。


### 設定パイプラインの設定 {#configure-config-deployment}

[実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment)を参照してください。
[実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)を参照してください。

## フロントエンドパイプライン {#front-end}

フロントエンドコードは、静的ファイルとして機能する任意のコードです。これは AEM から提供される UI コードとは別個のもので、サイトテーマ、顧客定義の SPA、SPA、その他のソリューションなどが含まれる可能性があります。

フロントエンドパイプラインは、バックエンド開発と同期せずにフロントエンドコードのデプロイメントを速めることができるので、チームが設計および開発プロセスを効率化するのに役立ちます。この専用パイプラインは、JavaScript と CSS をテーマとして AEM 配布レイヤーにデプロイして、AEM により配信されるページから参照できる新しいテーマバージョンを作成します。

>[!NOTE]
>
>**デプロイメントマネージャー**&#x200B;の役割を持つユーザーは、複数のフロントエンドパイプラインを同時に作成および実行できます。
>
>ただし、プログラムごとに（すべてのタイプで）最大 300 パイプラインの制限があります。

フロントエンドパイプラインは、コード品質パイプラインとすることも、デプロイメントパイプラインとすることもできます。

### フロントエンドパイプラインを設定する前に {#before-start}

フロントエンドパイプラインを設定する前に、[AEM クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md)を参照して、使いやすい AEM クイックサイト作成ツールの包括的ガイドを確認してください。このジャーニーはフロントエンド開発の効率化に役立つほか、AEM のバックエンドに関する知識がなくても、このジャーニーを参考にサイトをすばやくカスタマイズできます。

### フロントエンドパイプラインの設定 {#configure-front-end}

[実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)を参照してください。
[実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)を参照してください。

### フロントエンドパイプラインを使用したサイトの開発 {#developing-with-front-end-pipeline}

フロントエンドパイプラインを使用すると、フロントエンド開発者の作業の独立性が高まるほか、開発プロセスを速めることができます。

このプロセスの仕組みや、このプロセスの可能性を最大限に引き出すために知っておきたいいくつかの考慮事項については、[フロントエンドパイプラインを使用したサイトの開発](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)を参照してください。

## Web 階層設定パイプライン {#web-tier-config-pipelines}

Web 階層設定パイプラインを使用すると、HTTPD／Dispatcher 設定を他のコード変更から切り離して、この設定のみを AEM ランタイムにデプロイできます。これは効率化されたパイプラインで、Dispatcher 設定変更のみをデプロイしたい場合に、ほんの数分で行うことができます。

>[!TIP]
>
>Web 階層設定パイプラインを使用すると、プロジェクト構造に最適なものに応じて、フルスタックパイプラインと同じソースの場所または別のソースの場所に web 設定を保存できます。

次の制限が適用されます。

* Web 階層設定パイプラインを使用するには、AEM バージョン `2021.12.6151.20211217T120950Z` 以降を使用する必要があります。
* Web 階層設定パイプラインを使用するには、[Dispatcher ツールのフレキシブルモードをオプトイン](/help/implementing/dispatcher/disp-overview.md#validation-debug)する必要があります。
* パイプラインを設定または実行するには、ユーザーが&#x200B;**デプロイメントマネージャー**&#x200B;の役割でログインしている必要があります。
* Web 階層設定パイプラインは、常に 1 つの環境に 1 つしか存在できません。
* 対応するフルスタックパイプラインの実行中は、web 階層設定パイプラインを設定できません。
* Web 階層構造は、[クラウド内の Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) のドキュメントで定義されているフレキシブルモード構造に準拠している必要があります。

さらに、web 階層設定パイプラインを導入した場合に[フルスタックパイプライン](#full-stack-pipeline)がどのように動作するかを認識しておいてください。

* Web 階層設定パイプラインが環境に設定されていない場合、ユーザーは、フルスタックパイプラインの設定時に、Dispatcher 設定を含めるか無視するかを選択できます。この選択は、実行時およびデプロイメント時に行われます。
* Web 階層設定パイプラインが環境に設定されると、対応するフルスタックパイプライン（存在する場合）では実行時およびデプロイメント時に Dispatcher 設定が無視されます。
* Web 階層設定パイプラインが削除されたら、それに対応するフルスタックパイプラインは、実行時に Dispatcher 設定をデプロイするようにリセットされます。

Web 階層設定パイプラインのタイプは、`Code quality` または `Deployment` のいずれかになります。

### Web 階層パイプラインの設定 {#configure-web-tier}

[実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment)を参照してください。
[実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)を参照してください。

## パイプラインタイプの概要ビデオ {#video}

パイプラインタイプの概要については、次のビデオ（2 分 26 秒）を参照してください。

>[!VIDEO](https://video.tv.adobe.com/v/342363)
