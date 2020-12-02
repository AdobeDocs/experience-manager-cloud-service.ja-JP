---
title: AEM Commerce for AEM as a Cloud Service の開発
description: AEMプロジェクトのアーキタイプを使用して、コマース対応AEMプロジェクトを生成する方法を説明します。 AEMをCloud ServiceSDKとして使用し、ローカル開発環境にプロジェクトを構築してデプロイする方法を説明します。
topics: Commerce, Development
feature: Commerce Integration Framework
version: cloud-service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
translation-type: tm+mt
source-git-commit: 6be2ed60f4e672b99a85b55f833b8ae2f1b952b0
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 89%

---


# AEM Commerce for AEM as a Cloud Service の開発 {#develop}

AEM as a Cloud Service 用の Commerce Integration Framework（CIF）に基づく AEM Commerce プロジェクトの開発は、AEM as a Cloud Service 上の他の AEM プロジェクトと同じルールとベストプラクティスに従います。最初に以下を確認してください。

- [AEM プロジェクトの構造](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [AEM as a Cloud Service の SDK](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [AEM as a Cloud Service の開発ガイドライン](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## AEM as a Cloud Service SDK を使用したローカル開発 {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

CIF プロジェクトを使用する場合は、ローカル開発環境を使用することをお勧めします。AEM as a Cloud Service 環境用に提供された CIF アドオンは、ローカル開発にも使用できます。このファイルは、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html)からダウンロードできます。

CIF アドオンは Sling 機能アーカイブとして提供されます。ソフトウェア配布ポータルで利用できる zip ファイルには、2 つの Sling 機能アーカイブファイルが含まれています。1 つは AEM オーサー用、もう 1 つは AEM パブリッシュインスタンス用です。

**AEM as a Cloud Service は初めてですか？** AEM as a Cloud Service SDK を使用してローカル開発環境をセットアップするための、より詳細な[ガイド](https://docs.adobe.com/content/help/ja-JP/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)を参照してください。

### 必要なソフトウェア

以下をローカルにインストールしておく必要があります。

- [AEM as a Cloud Service の SDK](https://docs.adobe.com/content/help/en/*experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/)（3.3.9 以降）
- [Node.js v10 以降](https://nodejs.org/ja/)
- [npm 6 以降](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### CIF アドオンへのアクセス

CIF アドオンは、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)から zip ファイルとしてダウンロードできます。Zip ファイルには、CIF アドオンが **Sling 機能アーカイブ**&#x200B;として含まれています。これは、AEM パッケージではありません。なお、SDK リストにアクセスできるのは、AEM as a Cloud Service ライセンスのあるユーザーに限られます。

>[!TIP]
>
>常に最新バージョンの CIF アドオンを使用していることを確認してください。

### ローカル設定

AEM as a Cloud Service SDK を使用するローカル CIF アドオン開発の場合は、次の手順に従います。

1. 最新の AEM as a Cloud Service SDK を取得します。
1. AEM.jar を解凍し、`crx-quickstart` フォルダーを作成します。次を実行します。

   ```bash
   java -jar <jar name> -unpack
   ```

1. `crx-quickstart/install` フォルダーの作成
1. CIF アドオンの正しい Sling 機能アーカイブファイルを `crx-quickstart/install` フォルダーにコピーします。

   CIF アドオンの zip ファイルには、2 つの Sling 機能アーカイブ `.far` ファイルが含まれています。ローカル AEM as a Cloud Service SDK を実行する方法に応じて、AEM オーサーまたは AEM パブリッシュに対して正しいものを使用してください。

1. Magento GraphQL エンドポイントを保持する `COMMERCE_ENDPOINT` という名前のローカル OS 環境変数を作成します。

   Mac OS X の例：

   ```bash
   export COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   Windows の例：

   ```bash
   set COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   この変数は、AEM as a Cloud Service 環境に対しても設定する必要があります。

   変数の詳細については、[AEM用のOSGiのCloud Serviceとしての設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development)を参照してください。

1. （オプション）ステージングされたカタログ機能を有効にするには、Magentoインスタンス用の統合トークンを作成する必要があります。 [はじめに](./getting-started.md#staging)の手順に従ってトークンを作成してください。

   `COMMERCE_AUTH_HEADER`という名前のOSGiシークレットを次の値に設定します。

   ```xml
   Authorization: Bearer <Access Token>
   ```

   シークレットの詳細については、[AEM用のOSGiのCloud Serviceとしての設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development)を参照してください。

1. AEM as a Cloud Service SDK を開始します。

1. ローカルの GraphQL プロキシサーバーを開始します。

   Magento GraphQL エンドポイントを CIF アドオンと CIF コンポーネントでローカルに使用できるように、次のコマンドを使用します。GraphQL エンドポイントは、`http://localhost:3002/graphql` で使用できるようになります。
Mac OS X の例：

   ```bash
   npx local-cors-proxy --proxyUrl https://demo.magentosite.cloud --port 3002 --proxyPartial ''
   ```

   Windows の例：

   ```bash
   npx local-cors-proxy --proxyUrl https://demo.magentosite.cloud --port 3002 --proxyPartial '""'
   ```

   引数 `--proxyPartial` は、空の文字列を受け取る必要があります。

   GraphQL クエリツールを `http://localhost:3002/graphql` に向けて数件のクエリをテストし、ローカルの GraphQL プロキシをテストできます。

1. AEM SDK にログインし、ローカルの GraphQL プロキシサーバーを使用するように CIF を設定します。。

   CIF Cloud Service 設定に移動します（ツール／Cloud Services／CIF 設定）。プロジェクトで使用されている設定のプロパティ表示を開きます。

   `GraphQL Proxy Path` プロパティには、ローカルプロキシサーバーエンドポイント `http://localhost:3002/graphql` を使用します。設定を保存します。

>[!NOTE]
>
>手順 8 の設定をプロジェクトリポジトリーにプッシュしないでください。この設定は、ローカル開発の設定にのみ必要です。AEM as a Cloud Service 環境は、オンボーディング中に GraphQL プロキシで既に設定されています。

OSGI コンソールを使用して設定を確認します：`http://localhost:4502/system/console/osgi-installer`。このリストには、機能モデルファイルで定義されている CIF アドオン関連バンドル、コンテンツパッケージ、OSGI 設定が含まれている必要があります。

## プロジェクトのセットアップ {#project}

AEM as a Cloud Service 用の CIF プロジェクトをブートストラップするには、2 つの方法があります。

### AEM プロジェクトアーキタイプの使用

CIF を使い始めるために事前に設定されたプロジェクトをブートストラップするには、[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)が主なツールです。CIF コアコンポーネントと必要なすべての設定を、1 つの追加オプションで生成されたプロジェクトに含めることができます。

>[!TIP]
>
>プロジェクトを生成するには、[AEM プロジェクトアーキタイプ 24 以降](https://github.com/adobe/aem-project-archetype/releases)を使用します。

AEM プロジェクトの生成方法については、AEM プロジェクトのアーキタイプの「[使用手順](https://github.com/adobe/aem-project-archetype#usage)」を参照してください。プロジェクトに CIF を含めるには、`includeCommerce` オプションを使用します。

次に例を示します。

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=24 \
 -D aemVersion=cloud \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

CIF コアコンポーネントは、提供されている `all` パッケージを含めるか、CIF コンテンツパッケージと関連する OSGI バンドルを個別に使用することで、任意のプロジェクトで使用できます。CIF コアコンポーネントを手動でプロジェクトに追加するには、次の依存関係を使用します。

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### AEM Venia 参照用ストアの使用

CIF プロジェクトを開始する 2 つ目の方法は、[AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)をコピーして使用する方法です。AEM Venia 参照用ストアは、AEM 用の CIF コアコンポーネントの使用方法を示すサンプルのストアフロントアプリケーションです。これは、ベストプラクティス例として意図されているとともに、独自機能を開発するための有望な出発点としての役割も果たします。

Venia 参照用ストアを使い始めるには、Git リポジトリーをコピーし、必要に応じてプロジェクトをカスタマイズする開始を作成します。

>[!NOTE]
>
>Venia 参照用ストアプロジェクトには、AEM as a Cloud Service 用および AEM 6.5 用の 2 つのビルドプロファイルが含まれています。[project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) を参照して、使用方法を確認してください。

## その他のリソース

- [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
- [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
