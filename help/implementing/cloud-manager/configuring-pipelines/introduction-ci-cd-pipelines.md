---
title: CI／CD パイプライン
description: Cloud Managerの CI/CD パイプラインと、CI/CD パイプラインを使用してコードを効率的にデプロイする方法について説明します。
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 40%

---


# Cloud Manager CI／CD パイプライン {#intro-cicd}

Cloud Managerの CI/CD （Continuous Integration/Continuous Delivery）パイプラインと、それらを使用してコードを効率的にデプロイする方法について説明します。

## はじめに {#introduction}

Cloud Manager の CI／CD パイプラインは、ソースリポジトリーからコードを作成して環境にデプロイするためのメカニズムです。イベントは、Git などのソースコードリポジトリからのプルリクエスト（つまりコード変更）などのパイプラインをトリガーにします。 または、リリース頻度に合わせて定期的にトリガーすることもできます。

パイプラインを設定するには、以下を行う必要があります。

* パイプラインを開始するトリガーを定義します
* 実稼動デプロイメントを制御するパラメーターの定義
* パフォーマンステストパラメーターの設定

Cloud Manager には、次の 2 種類のパイプラインが用意されています。

* [実稼動パイプライン](#prod-pipeline)
* [実稼動以外のパイプライン](#non-prod-pipeline)

![パイプラインのタイプ](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## 実稼動パイプライン {#prod-pipeline}

実稼動パイプラインは、ソースコードを実稼動用にデプロイするための調整された一連のステップで構成される専用のパイプラインです。これらのステップには、ビルド、パッケージ化、テスト、検証およびデプロイがあり、最初はすべてステージング環境で行われます。したがって、実稼動パイプラインは、実稼動環境とステージング環境のセットを作成した場合にのみ追加できます。

>[!TIP]
>
>[ 実稼動パイプラインの設定 ](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) を参照してください。

## 実稼動以外のパイプライン {#non-prod-pipeline}

実稼動以外のパイプラインは、主にコード品質スキャンの実行や開発環境へのソースコードのデプロイに役立ちます。

>[!TIP]
>
>[ 実稼動以外のパイプラインの設定 ](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) を参照してください。

## コードソース {#code-sources}

パイプラインは、実稼動環境と非実稼動環境に加えて、デプロイするコードのタイプによっても異なる場合があります。

* **[フルスタックパイプライン](#full-stack-pipeline)** - 1 つ以上のAEM サーバーアプリケーションを含んだバックエンドおよびフロンエンドコードビルドと HTTPD/Dispatcher設定を同時にデプロイします。
* **[設定パイプライン](#config-deployment-pipeline)** - ログ転送やパージ関連のメンテナンスタスクなどの機能の設定をすばやくデプロイできます。 また、Web アプリケーションファイアウォール（WAF）ルールなどのトラフィックフィルタールールなど、様々な CDN （コンテンツ配信ネットワーク）設定も含まれています。 さらに、リクエストと応答の変換、オリジンセレクター、クライアントサイドのリダイレクト、エラーページ、CDN キー、API キーのパージ、基本認証を管理できます。 詳しくは [ 設定パイプラインの使用 ](/help/operations/config-pipeline.md) を参照してください。
* **[フロントエンドパイプライン](#front-end)** - 1 つ以上のクライアントサイド UI アプリケーションを含んだフロントエンドコードビルドをデプロイします。
* **[Web 階層設定パイプライン](#web-tier-config-pipelines)** - HTTPD/Dispatcher設定をデプロイします。

これらのパイプラインタイプについては、このドキュメントで後ほど詳しく説明します。

### Cloud Managerの CI/CD パイプラインについて {#understand-pipelines}

Cloud Manager で使用できるパイプラインとその用途を次の表にまとめます。

| パイプラインタイプ | デプロイメントまたはコード品質 | Source コード | 目的 | 備考 |
| --- | --- | --- | --- | ---|
| 実稼動または非実稼動 | デプロイメント | フルスタック | バックエンドおよびフロンエンドコードビルドと HTTPD／Dispatcher 設定を同時にデプロイ | フロントエンドコードをAEM サーバーコードと同時にデプロイする必要がある場合に使用します。 フロントエンドパイプラインまたは web 階層設定パイプラインがまだ採用されていない場合に使用します。 |
| 実稼動または非実稼動 | デプロイメント | フロントエンド | 1 つ以上のクライアントサイド UI アプリケーションを含んだフロントエンドコードビルドをデプロイ | 複数の同時フロントエンドパイプラインをサポート <br> フルスタックデプロイメントよりはるかに高速。 |
| 実稼動または非実稼動 | デプロイメント | Web 階層設定 | HTTPD／Dispatcher 設定をデプロイ | 数分でデプロイ |
| 実稼動または非実稼動 | デプロイメント | Config | CDN、ログ転送、パージメンテナンスタスクに関連する[多くの機能の設定](/help/operations/config-pipeline.md)をデプロイ | 数分でデプロイ |
| 実稼動以外 | コード品質 | フルスタック | デプロイメントなしでフルスタックコードに対してコード品質スキャンを実行 | 複数のパイプラインをサポート |
| 実稼動以外 | コード品質 | フロントエンド | デプロイメントなしでフロントエンドコードに対してコード品質スキャンを実行 | 複数のパイプラインをサポート |
| 実稼動以外 | コード品質 | Web 階層設定 | デプロイメントなしでDispatcher設定に対してコード品質スキャンを実行 | 複数のパイプラインをサポート |

従来の単一のフロントエンドリポジトリーまたは独立したフロントエンドリポジトリーをセットアップした Cloud Manager パイプライン設定を次の図に示します。

![Cloud Manager パイプライン設定](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## フルスタックパイプライン {#full-stack-pipeline}

フルスタックパイプラインでは、バックエンドコード、フロントエンドコードおよび web 階層設定を、すべて同時にAEM ランタイムにデプロイします。

* バックエンドコード - Java コード、OSGi 設定、repoinit などの不変コンテンツと可変コンテンツ
* フロントエンドコード - JavaScript、CSS、フォントなどのアプリケーション UI リソース
* Web 階層設定 - HTTPD／Dispatcher 設定

フルスタックパイプラインは「uber」パイプラインを表します。 すべてを同時に処理できる一方、フロントエンドコードとDispatcherの設定を別々にデプロイすることもできます。 このデプロイメントは、フロントエンドパイプラインと web 階層設定パイプラインをそれぞれ通じて行われます。

フルスタックパイプラインでは、フロントエンドコード（JavaScript／CSS）を [AEM クライアントライブラリ](/help/implementing/developing/introduction/clientlibs.md)としてパッケージ化します。

フルスタックパイプラインは、[web 階層設定パイプライン](#web-tier-config-pipelines)が設定されていない場合、web 階層設定をデプロイする場合があります。

次の制限が適用されます。

* パイプラインを設定または実行するには、ユーザーが&#x200B;**デプロイメントマネージャー**&#x200B;の役割でログインしている必要があります。
* フルスタックパイプラインは、常に 1 つの環境に 1 つしか存在できません。

さらに、[web 階層設定パイプライン](#web-tier-config-pipelines)の導入を選択した場合は、フルスタックパイプラインがどのように動作するかを認識しておいてください。

* 環境のフルスタックパイプラインは、対応する web 階層設定パイプラインが存在する場合、Dispatcher設定を無視します
* 環境に対応する web 階層設定パイプラインが存在しない場合、ユーザーは、Dispatcher 設定を含めるまたは無視するようにフルスタックパイプラインを設定できます。

フルスタックパイプラインは、コード品質パイプラインとすることも、デプロイメントパイプラインとすることもできます。

### フルスタックパイプラインの設定 {#configure-full-stack}

[ 実稼動パイプラインの追加 ](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code) を参照してください。
[ 実稼動以外のパイプラインを追加 ](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code) を参照してください。

## 設定パイプライン {#config-deployment-pipeline}

設定パイプラインを使用すると、ログ転送、パージ関連のメンテナンスタスク、様々な CDN 設定（トラフィックフィルタールール（WAF（Web Application Firewall）ルールなど）を含む）の設定をすばやくデプロイできます。 さらに、リクエストと応答の変換、オリジンセレクター、クライアントサイドのリダイレクト、エラーページ、顧客が管理する CDN キー、API キーのパージ、基本認証を管理できます。

サポートされる機能の包括的なリストと、リポジトリの設定を適切にデプロイするために管理する方法については、[ 設定パイプラインの使用 ](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) を参照してください。

### 設定パイプライン {#configure-config-deployment}

[ 実稼動パイプラインの追加 ](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment) を参照してください。
[ 実稼動以外のパイプラインを追加 ](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment) を参照してください。

## フロントエンドパイプライン {#front-end}

フロントエンドコードは、静的ファイルとして機能する任意のコードです。これは AEM から提供される UI コードとは別個のもので、サイトテーマ、顧客定義の SPA、SPA、その他のソリューションなどが含まれる可能性があります。

フロントエンドパイプラインは、バックエンド開発と同期せずにフロントエンドコードのデプロイメントを迅速に行えるようにすることで、チームが設計および開発プロセスを合理化するのに役立ちます。 この専用パイプラインは、JavaScriptと CSS をテーマとしてAEM配布レイヤーにデプロイして、新しいテーマバージョンを作成します。このバージョンは、AEMによって配信されるページから参照できます。

>[!NOTE]
>
>**デプロイメントマネージャー**&#x200B;の役割を持つユーザーは、複数のフロントエンドパイプラインを同時に作成および実行できます。
>
>ただし、プログラムごとに（すべてのタイプで）最大 300 パイプラインの制限があります。

フロントエンドパイプラインは、コード品質パイプラインとすることも、デプロイメントパイプラインとすることもできます。

### フロントエンドパイプラインを設定する前に {#before-start}

フロントエンドパイプラインを設定する前に、[AEM クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md)を参照して、使いやすい AEM クイックサイト作成ツールの包括的ガイドを確認してください。このジャーニーはフロントエンド開発の効率化に役立つほか、AEMのバックエンドに関する知識がなくても、このジャーニーを参考にサイトをすばやくカスタマイズできます。

### フロントエンドパイプラインの設定 {#configure-front-end}

[ 実稼動パイプラインの追加 ](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline) を参照してください。
[ 実稼動以外のパイプラインを追加 ](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline) を参照してください。

### フロントエンドパイプラインを使用したサイトの開発 {#developing-with-front-end-pipeline}

フロントエンドパイプラインを使用すると、フロントエンド開発者の作業の独立性が高まるほか、開発プロセスを速めることができます。

このプロセスの仕組みと、このプロセスの可能性を最大限に引き出すために知っておくべきいくつかの考慮事項については、[ フロントエンドパイプラインを使用したサイトの開発 ](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) を参照してください。

## Web 階層設定パイプライン {#web-tier-config-pipelines}

Web 階層設定パイプラインを使用すると、HTTPD/Dispatcher設定を排他的にAEM ランタイムにデプロイし、他のコード変更から切り離すことができます。 これは効率化されたパイプラインで、Dispatcher設定の変更のみをデプロイしたい場合に、ほんの数分で行うことができます。

>[!TIP]
>
>Web 階層設定パイプラインを使用すると、プロジェクト構造に最適なものを基に、web 設定をフルスタックパイプラインと同じ場所または別の場所に保存できます。

次の制限が適用されます。

* Web 階層設定パイプラインを使用するには、AEM バージョン `2021.12.6151.20211217T120950Z` 以降を使用します。
* [Dispatcher ツールのフレキシブルモードをオプトイン ](/help/implementing/dispatcher/disp-overview.md#validation-debug) して、web 階層設定パイプラインを使用します。
* パイプラインを設定または実行するには、ユーザーが&#x200B;**デプロイメントマネージャー**&#x200B;の役割でログインしている必要があります。
* Web 階層設定パイプラインは、常に 1 つの環境に 1 つしか存在できません。
* 対応するフルスタックパイプラインの実行中は、web 階層設定パイプラインを設定できません。
* Web 階層構造は、[クラウド内の Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) のドキュメントで定義されているフレキシブルモード構造に準拠している必要があります。

さらに、web 階層設定パイプラインを導入した場合に[フルスタックパイプライン](#full-stack-pipeline)がどのように動作するかを認識しておいてください。

* Web 階層設定パイプラインが環境に対して設定されていない場合、ユーザーは、フルスタックパイプラインの設定時に、Dispatcher設定を含めるか無視するかを選択できます。 この選択は、実行時やデプロイメント時に行われます。
* Web 階層設定パイプラインが環境に設定されると、それに対応するフルスタックパイプライン（存在する場合）では、実行中およびデプロイメント中にDispatcher設定が無視されます。
* Web 階層設定パイプラインが削除されたら、それに対応するフルスタックパイプラインは、実行時に Dispatcher 設定をデプロイするようにリセットされます。

Web 階層設定パイプラインのタイプは、`Code quality` または `Deployment` にできます。

### Web 階層設定パイプライン {#configure-web-tier}

[ 実稼動パイプラインの追加 ](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment) を参照してください。
[ 実稼動以外のパイプラインを追加 ](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment) を参照してください。

## パイプラインタイプの概要に関するビデオ {#video}

パイプラインタイプの概要については、次のビデオ（2 分 26 秒）を参照してください。

>[!VIDEO](https://video.tv.adobe.com/v/342363)
