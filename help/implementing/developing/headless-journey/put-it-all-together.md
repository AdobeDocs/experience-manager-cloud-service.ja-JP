---
title: 組み合わせ方法 — アプリとコンテンツをAEMにヘッドレスで
description: AEMヘッドレス開発者ジャーニーのこの部分では、コンテンツフラグメント、GraphQL呼び出し、REST API呼び出し、アプリケーションを含むAEMプロジェクトを実行し、運用に備える方法を説明します。
hide: true
hidefromtoc: true
index: false
exl-id: 254fb9dd-36c8-43ce-aaea-ceb4d079503d
translation-type: tm+mt
source-git-commit: e8eb9d2c96d24601e50c48f6846a8c8bac8b0252
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 1%

---

# 組み合わせ方法 — アプリとコンテンツをAEMヘッドレス{#put-it-all-together}に配置

>[!CAUTION]
>
>作業中 — このドキュメントの作成は現在進行中で、完全なもの、最終的なもの、または実稼働目的で使用するものとして理解してはなりません。

[AEMヘッドレス開発者ジャーニーのこの部分では、](overview.md)が、Content Fragments、GraphQL呼び出し、REST API呼び出し、アプリケーションを含むAEMプロジェクトを実行し、運用準備を行う方法を学びます。

## {#story-so-far}

以前のドキュメントのAEM headlessジャーニーでは、[AEM AssetsAPIを使用したコンテンツの更新方法](update-your-content.md)で、AEMの既存のheadlessコンテンツを更新する方法を学びました。今後は、次の操作を行う必要があります。

* AEM AssetsHTTP APIについて説明します。

この記事は、これらの基本事項に基づいて構築されているので、独自のAEMヘッドレスプロジェクトを実稼動に備える方法を理解しています。

## 目的 {#objective}

* AEMのローカル開発ワークフローについて理解する
* AEM SDKをインストールして、コンテンツのテストに使用できるローカル開発ランタイムを取得します。
* ローカル開発ランタイムの横で作業する必要がある開発ツールについて説明します。

## ローカル開発ワークフロー{#the-local-development-workflow}

ローカル開発プロジェクトはApache Mavenを基に構築されており、ソース管理にGitを使用しています。 プロジェクトを更新するために、開発者はEclipse、Visual Studio Code、IntelliJなどの望ましい統合開発環境を使用できます。

ヘッドレスアプリケーションで取り込まれるコードまたはコンテンツの更新をテストするには、AEM作成者のローカルインスタンスとパブリッシュインスタンスを含むローカルAEMランタイムにアップデートを展開する必要があります。

ローカルAEMランタイムの各コンポーネント間の違いは必ず書き留めておいてください。最も重要な点は、アップデートをテストすることです。例えば、作成者でコンテンツの更新をテストしたり、発行インスタンスで新しいコードをテストしたりします。

実稼働システムでは、ディスパッチャーとhttp Apacheサーバーは、常にAEM発行インスタンスの前に配置されます。 また、AEMシステムのキャッシュおよびセキュリティサービスを提供するので、ディスパッチャーに対してコードおよびコンテンツの更新をテストすることもお勧めします。

すべてのテストが完了し、正しく機能していることを確認したら、Cloud Managerの中央のGitリポジトリにコードの更新をプッシュする準備が整います。

アップデートは、Cloud Managerにアップロードされた後、Cloud ManagerのCI/CDパイプラインを使用して、AEMにCloud Serviceとしてデプロイできます。


## AEM SDK {#the-aem-sdk}

AEM SDKは、カスタムコードを構築しデプロイするために使用します。 次のアーティファクトが含まれます。

* Quickstart jar — 作成者インスタンスと発行インスタンスの両方を設定するのに使用できる実行可能なjarファイル
* ディスパッチャーツール — WindowsおよびUNIXベースのシステムのディスパッチャーモジュールとその依存関係
* Java API Jar - AEMに対する開発に使用できる、許可されているすべてのJava APIを公開するJava Jar/Maven依存関係
* Javadoc jar - Java API jarのjavadoc

## ローカル開発環境セットアップ{#local-development-environment}

AEMヘッドレスプロジェクトを起動用に準備するには、プロジェクトの構成要素がすべて正常に機能していることを確認する必要があります。

そのためには、コード、コンテンツ、設定をまとめ、ローカル開発環境でテストして、運用に適した状態に保つ必要があります。

ローカル開発環境は、

1. AEMプロジェクト —AEM開発者が作業するすべてのカスタムコード、設定、コンテンツが含まれます。
1. Local AEM Runtime - AEMプロジェクトからコードをデプロイするために使用されるAEM作成者サービスおよび発行サービスのローカルバージョン
1. Local Dispatcher Runtime - Dispatcherモジュールを含むApache httpd Webサーバーのローカルバージョンです。

## 開発ツール {#development-tools}

AEM SDKに加えて、コードとコンテンツをローカルで開発およびテストするための追加ツールが必要になります。

* Java
* Git
* Apache Maven
* Node.jsライブラリ
* 選択したIDE

AEMはJavaアプリケーションなので、AEMをCloud Serviceとして開発するためには、JavaとJava SDKをインストールする必要があります。

Gitは、ソース管理の管理、Cloud Managerの変更をチェックインし、実稼働インスタンスに展開するために使用するツールです。

AEMでは、AEM Mavenプロジェクトアーキタイプから生成されたプロジェクトを作成する際にApache Mavenを使用します。 主要なIDEはすべてMavenの統合サポートを提供します。

Node.jsは、AEMプロジェクトのui.frontendサブプロジェクトのフロントエンドアセットを操作するために使用されるJavaScriptランタイム環境です。 Node.jsはnpmと共に配布され、JavaScriptの依存関係を管理するために使用される、事実上のNode.jsパッケージマネージャーです。

## 次の作業{#what-is-next}

次に、AEMヘッドレス・プロジェクトを実際に稼働させるドキュメント[How to Go Live with Your Headless Application](go-live.md)を見て、AEMのヘッドレス・ジャーニーを続ける必要があります。

## その他のリソース {#additional-resources}

* [ローカル開発環境の設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-dispatcher-runtime) - AEM用の開始開発に必要なツールのインストール方法を学びます。
* [Cloud ServiceSDKとしてのAEM](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)  -AEM SDKを詳しく見る