---
title: CI／CD パイプライン
description: Cloud Manager の CI／CD パイプラインと、CI／CD パイプラインを使用してコードを効率的にデプロイする方法について説明します。
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 76%

---


# Cloud Manager CI／CD パイプライン {#intro-cicd}

Cloud Manager の CI／CD パイプラインと、CI／CD パイプラインを使用してコードを効率的にデプロイする方法について説明します。

## はじめに {#introduction}

Cloud Manager の CI／CD パイプラインは、ソースリポジトリーからコードを作成して環境にデプロイするためのメカニズムです。パイプラインは、ソースコードリポジトリからのプル要求（コード変更）や、リリースケイデンスに合わせた定期的なスケジュールで、イベントによってトリガーできます。

パイプラインを設定するには、以下を行う必要があります。

* パイプラインを開始するトリガーの定義
* 実稼動デプロイメントを制御するパラメーターの定義
* パフォーマンステストパラメーターの設定

Cloud Manager には、次の 2 種類のパイプラインが用意されています。

* [実稼動パイプライン](#prod-pipeline)
* [実稼動以外のパイプライン](#non-prod-pipeline)

![パイプラインのタイプ](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## ビデオの概要 {#video}

パイプラインタイプの概要については、この短いビデオを視聴してください。

>[!VIDEO](https://video.tv.adobe.com/v/342363)

## 実稼動パイプライン {#prod-pipeline}

実稼動パイプラインは、ソースコードを実稼動用にデプロイするための調整された一連のステップで構成される専用のパイプラインです。これらのステップには、ビルド、パッケージ化、テスト、検証およびデプロイがあり、最初はすべてステージング環境で行われます。したがって、実稼働パイプラインは、実稼働環境とステージング環境のセットを作成した場合にのみ追加できます。

>[!TIP]
>
>詳しくは、 [実稼動パイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) を参照してください。

## 実稼動以外のパイプライン {#non-prod-pipeline}

実稼動以外のパイプラインは、主にコード品質スキャンの実行や開発環境へのソースコードのデプロイに役立ちます。

>[!TIP]
>
>詳しくは、 [実稼動以外のパイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) を参照してください。

## コードのソース {#code-sources}

実稼働パイプラインと実稼動以外のパイプラインに加えて、デプロイするコードのタイプによってパイプラインを区別することもできます。

* **[フルスタックパイプライン](#full-stack-pipeline)** - 1 つ以上の AEM サーバーアプリケーションを含んだバックエンドおよびフロンエンドコードビルドと HTTPD／Dispatcher 設定を同時にデプロイします。
* **[フロントエンドパイプライン](#front-end)** - 1 つ以上のクライアントサイド UI アプリケーションを含んだフロントエンドコードビルドをデプロイします。
* **[Web 階層設定パイプライン](#web-tier-config-pipelines)** - HTTPD／Dispatcher 設定をデプロイします。

これらについては、この後このドキュメントで詳しく説明します。

### Cloud Manager の CI／CD パイプラインについて {#understand-pipelines}

Cloud Manager で使用できるすべてのパイプラインとその用途を次の表にまとめます。

| パイプラインタイプ | デプロイメントまたはコード品質 | ソースコード | 目的 | 備考 |
|--- |--- |--- |---|---|
| 実稼動または非実稼動 | デプロイメント | フルスタック | バックエンドおよびフロンエンドコードビルドと HTTPD／Dispatcher 設定を同時にデプロイ | フロントエンドコードを AEM サーバーコードと同時にデプロイする必要がある場合。<br>フロントエンドパイプラインまたは web 階層設定パイプラインがまだ導入されていない場合。 |
| 実稼動または非実稼動 | デプロイメント | フロントエンド | 1 つ以上のクライアントサイド UI アプリケーションを含んだフロントエンドコードビルドをデプロイ | 複数の同時フロントエンドパイプラインをサポート<br>フルスタックデプロイメントよりはるかに高速 |
| 実稼動または非実稼動 | デプロイメント | Web 階層設定 | HTTPD／Dispatcher 設定をデプロイ | 数分でデプロイ |
| 実稼動以外 | コード品質 | フルスタック | デプロイメントなしでフルスタックコードに対してコード品質スキャンを実行 | 複数のパイプラインをサポート |
| 実稼動以外 | コード品質 | フロントエンド | デプロイメントなしでフロントエンドコードに対してコード品質スキャンを実行 | 複数のパイプラインをサポート |
| 実稼動以外 | コード品質 | Web 階層設定 | デプロイメントなしで Dispatcher 設定に対してコード品質スキャンを実行 | 複数のパイプラインをサポート |

従来の単一のフロントエンドリポジトリーまたは独立したフロントエンドリポジトリーをセットアップした Cloud Manager パイプライン設定を次の図に示します。

![Cloud Manager パイプライン設定](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## フルスタックパイプライン {#full-stack-pipeline}

フルスタックパイプラインでは、バックエンドコード、フロントエンドコードおよび web 階層設定を、すべて同時に AEM ランタイムにデプロイします。

* バックエンドコード — Java コード、OSGi 設定、repoinit、可変コンテンツなどの不変コンテンツ
* フロントエンドコード - JavaScript、CSS、フォントなどのアプリケーション UI リソース
* Web 階層設定 - HTTPD／Dispatcher 設定

フルスタックパイプラインとは、すべてのことを一度に行う「スーパー」パイプラインのことですが、その一方で、フロントエンドパイプラインと web 階層設定パイプラインをそれぞれ使用して、フロントエンドコードまたは Dispatcher 設定に限定してデプロイすることもできます。

フルスタックパイプラインパッケージフロントエンドコード (JavaScript/CSS) を [AEMクライアントライブラリ](/help/implementing/developing/introduction/clientlibs.md).

フルスタックパイプラインは、[web 階層設定パイプライン](#web-tier-config-pipelines)が設定されていない場合、web 階層設定をデプロイする場合があります。

次の制限が適用されます。

* ユーザーは、 **デプロイメントマネージャー** パイプラインを設定または実行するためのロール。
* フルスタックパイプラインは、常に 1 つの環境に 1 つしか存在できません。

また、 [web 層設定パイプライン。](#web-tier-config-pipelines)

* 環境のフルスタックパイプラインは、対応する web 階層設定パイプラインが存在する場合、Dispatcher 設定を無視します。
* 環境に対応する web 階層設定パイプラインが存在しない場合、ユーザーは、Dispatcher 設定を含めるまたは無視するようにフルスタックパイプラインを設定できます。

フルスタックパイプラインは、コード品質パイプラインとすることも、デプロイメントパイプラインとすることもできます。

## フロントエンドパイプライン {#front-end}

フロントエンドコードは、静的ファイルとして機能する任意のコードです。これは AEM から提供される UI コードとは別個のもので、サイトテーマ、顧客定義の SPA、SPA、その他のソリューションなどが含まれる可能性があります。

フロントエンドパイプラインは、バックエンド開発と同期せずにフロントエンドコードのデプロイメントを速めることができるので、チームが設計および開発プロセスを効率化するのに役立ちます。この専用パイプラインは、JavaScript と CSS をテーマとして AEM 配布レイヤーにデプロイして、AEM により配信されるページから参照できる新しいテーマバージョンを作成します。

>[!IMPORTANT]
>
>AEM版である必要があります `2021.10.5933.20211012T154732Z ` またはAEM Sitesがフロントエンドパイプラインの使用を有効にしている場合は、

>[!NOTE]
>
>**デプロイメントマネージャー**&#x200B;の役割を持つユーザーは、複数のフロントエンドパイプラインを同時に作成および実行できます。
>
>ただし、プログラムごとに（すべてのタイプで）最大 300 パイプラインの制限があります。

フロントエンドパイプラインは、コード品質パイプラインとすることも、デプロイメントパイプラインとすることもできます。

### フロントエンドパイプラインを設定する前に {#before-start}

フロントエンドパイプラインを設定する前に、 [AEMクイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md) を参照してください。 このジャーニーはフロントエンド開発の効率化に役立つほか、AEM のバックエンドに関する知識がなくても、このジャーニーを参考にサイトをすばやくカスタマイズできます。

### フロントエンドパイプラインの設定 {#configure-front-end}

フロントエンドパイプラインの設定方法については、以下を参照してください。

* [実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### フロントエンドパイプラインを使用したサイトの開発 {#developing-with-front-end-pipeline}

フロントエンドパイプラインを使用すると、フロントエンド開発者の作業の独立性が高まるほか、開発プロセスを速めることができます。

詳しくは、 [フロントエンドパイプラインを使用したサイトの開発](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) このプロセスの仕組みと、このプロセスを最大限に活用するために考慮すべきいくつかの検討事項について説明します。

### フルスタックパイプラインの設定 {#configure-full-stack}

フルスタックパイプラインの設定方法については、次のドキュメントを参照してください。

* [実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)


## Web 階層設定パイプライン {#web-tier-config-pipelines}

Web 階層設定パイプラインを使用すると、HTTPD／Dispatcher 設定を他のコード変更から切り離して、この設定のみを AEM ランタイムにデプロイできます。これは効率化されたパイプラインで、Dispatcher 設定変更のみをデプロイしたい場合に、ほんの数分で行うことができます。

>[!TIP]
>
>Web 階層設定パイプラインでは、web 設定の保存先をフルスタックパイプラインの場合と同じ元の場所にするか別の場所にするかを、プロジェクトへの適合性に応じて選択することができます。

次の制限が適用されます。

* AEM版である必要があります `2021.12.6151.20211217T120950Z` Web 層設定パイプラインを使用する場合と、それ以降の場合があります。
* 必ず [dispatcher ツールの柔軟なモードのオプトイン](/help/implementing/dispatcher/disp-overview.md#validation-debug) web 層設定パイプラインを使用する場合。
* ユーザーは、 **デプロイメントマネージャー** パイプラインを設定または実行するためのロール。
* Web 階層設定パイプラインは、常に 1 つの環境に 1 つしか存在できません。
* 対応するフルスタックパイプラインの実行中は、web 階層設定パイプラインを設定できません。
* Web 層構造は、ドキュメントで定義されている柔軟モード構造に従う必要があります [クラウド内の Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug).

さらに、 [フルスタックパイプライン](#full-stack-pipeline) は、Web 層パイプラインを導入する際に動作します。

* Web 階層設定パイプラインが環境に設定されていない場合、ユーザーは、対応するフルスタックパイプラインを設定する際に、実行時およびデプロイメント時に Dispatcher 設定を含めるか無視するかを選択することができます。
* Web 階層設定パイプラインが環境に既に設定されている場合、それに対応するフルスタックパイプライン（存在する場合）では、実行時およびデプロイメント時に Dispatcher 設定が無視されます。
* Web 層設定パイプラインを削除すると、対応するフルスタックパイプラインがリセットされ、実行中に Dispatcher 設定がデプロイされます。

Web 階層設定パイプラインは、コード品質タイプでもデプロイメントタイプでもかまいません。

### Web 階層設定パイプラインの設定 {#configure-web-tier-config-pipelines}

Web 層設定パイプラインの設定方法については、次のドキュメントを参照してください。

* [実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)
