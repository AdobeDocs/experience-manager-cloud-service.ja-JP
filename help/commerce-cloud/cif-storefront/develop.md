---
title: AEM Commerce for AEM as a Cloud Service の開発
description: AEM プロジェクトアーキタイプを使用してコマース対応の AEM プロジェクトを生成する方法を説明します。AEM as a Cloud Service SDK でプロジェクトを構築してローカル開発環境にデプロイする方法を説明します。
topics: Commerce, Development
feature: Commerce Integration Framework
version: Experience Manager as a Cloud Service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
role: Admin
index: false
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 74%

---


# AEM Commerce for AEM as a Cloud Service の開発 {#develop}

AEM as a Cloud Service 用の Commerce Integration Framework（CIF）に基づく AEM Commerce プロジェクトの開発は、AEM as a Cloud Service 上の他の AEM プロジェクトと同じルールとベストプラクティスに従います。最初に次の点を確認します。

* [AEM プロジェクトの構造](/help/implementing/developing/introduction/aem-project-content-package-structure.md)
* [AEM as a Cloud Service の SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [AEM as a Cloud Service の開発ガイドライン](/help/implementing/developing/introduction/development-guidelines.md)

## AEM as a Cloud Service SDK を使用したローカル開発 {#local}

>[!VIDEO](https://video.tv.adobe.com/v/347038/?quality=12&learn=on&captions=jpn)

CIF プロジェクトを使用する場合は、ローカル開発環境を使用することをお勧めします。AEM as a Cloud Service 用に提供された CIF アドオンは、ローカル開発にも使用できます。[ ソフトウェア配布ポータル ](/help/implementing/developing/tools/package-manager.md#software-distribution) からダウンロードできます。

CIF アドオンは Sling 機能アーカイブとして提供されます。ソフトウェア配布ポータルで利用できる zip ファイルには、2 つの Sling 機能アーカイブファイルが含まれています。1 つは AEM オーサー用、もう 1 つは AEM パブリッシュインスタンス用です。

>[!TIP]
>
>**AEM as a Cloud Serviceを初めて使用する場合**
>&#x200B;>[AEM as a Cloud Service SDKを使用したローカル開発環境のセットアップに関する詳細なガイド ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=ja) を参照してください。

### 必要なソフトウェア {#required-software}

以下をローカルにインストールしておく必要があります。

* [AEM as a Cloud Service の SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=ja#download-the-aem-as-a-cloud-service-sdk)
* [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
* [Apache Maven](https://maven.apache.org/)（3.3.9 以降）
* [Node.js v10 以降](https://nodejs.org/ja)
* [npm 6 以降](https://www.npmjs.com/)
* [Git](https://git-scm.com/)

### CIF アドオンへのアクセス {#accessing-add-on}

CIF アドオンは、[ ソフトウェア配布ポータルから zip ファイルでダウンロードできます。zip ファイルに ](/help/implementing/developing/tools/package-manager.md)Sling 機能アーカイブ **としてCIF アドオンが含まれているのであれ**、AEM パッケージではありません。 SDK リストには、AEM as a Cloud Serviceライセンスでアクセスできます。

>[!TIP]
>
>常に最新バージョンの CIF アドオンを使用していることを確認してください。

### ローカル設定 {#local-setup}

AEM as a Cloud Service SDKを使用するローカル CIF アドオン開発の場合は、次の手順に従います。

1. 最新のAEM as a Cloud Service SDKを取得します。
1. AEMの.jar を解凍し、`crx-quickstart` フォルダーを作成します。 次のコマンドを実行します。

   ```bash
   java -jar <jar name> -unpack
   ```

1. `crx-quickstart/install` フォルダーを作成します。
1. CIF アドオンの正しい Sling 機能アーカイブファイルを `crx-quickstart/install` フォルダーにコピーします。

   * CIF アドオン zip ファイルには、2 つの Sling 機能アーカイブ `.far` ファイルが含まれています。
   * ローカル AEM as a Cloud Service SDK を実行する方法に応じて、AEM オーサーまたは AEM パブリッシュに対して正しいものを使用してください。

1. Adobe Commerce GraphQL エンドポイントを保持する `COMMERCE_ENDPOINT` という名前のローカル OS 環境変数を作成します。

   * この変数は、AEM でコマースシステムへの接続に使用されます。CIF アドオンには、Commerce GraphQL エンドポイントをローカルで使用できるようにするローカルリバースプロキシが含まれています。 このプロキシは、CIF オーサリングツール（製品コンソールおよびピッカー）で使用され、GraphQL の直接呼び出しを行う CIF クライアントサイドコンポーネントにも使用されます。

   * この変数は、AEM as a Cloud Service 環境に対しても設定する必要があります。変数について詳しくは、[AEM as a Cloud Serviceの OSGi の設定 ](/help/implementing/deploying/configuring-osgi.md#local-development) を参照してください。

   * macOSの下の例：

     ```bash
     export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
     ```

   * Windows での例：

     ```bash
     set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
     ```

1. （オプション）ステージング済みカタログ機能を有効にするには、Adobe Commerce インスタンスの統合トークンを作成する必要があります。[概要](/help/commerce-cloud/cif-storefront/getting-started.md#staging)の手順に従って、トークンを作成します。

   * `COMMERCE_AUTH_HEADER` という名前の OSGi シークレットを次の値に設定します。

     ```xml
     Authorization: Bearer <Access Token>
     ```

   * 秘密鍵について詳しくは、[AEM as a Cloud Serviceの OSGi の設定 ](/help/implementing/deploying/configuring-osgi.md#local-development) を参照してください。

1. AEM as a Cloud Service SDKを開始します。

>[!NOTE]
>
>手順 5 で設定した環境変数と同じターミナルウィンドウで、AEM as a Cloud Service SDK を起動します。別のターミナルウィンドウで起動するか .jar ファイルをダブルクリックして起動する場合、環境変数が表示されていることを確認します。

OSGi コンソールを使用して設定を確認します：`http://localhost:4502/system/console/osgi-installer`。 リストには、機能モデルファイルで定義されたCIF アドオン関連バンドル、コンテンツパッケージ、OSGi 設定が含まれている必要があります。

## プロジェクトのセットアップ {#project}

AEM as a Cloud Service 用の CIF プロジェクトを Bootstrap するには、2 つの方法があります。

### AEM プロジェクトアーキタイプの使用 {#project-archetype}

CIF を使い始めるために事前に設定されたプロジェクトを Bootstrap するには、[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)が主なツールです。CIF コアコンポーネントと必要なすべての設定を、1 つの追加オプションで生成されたプロジェクトに含めることができます。

>[!TIP]
>
>常に最新バージョンの [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype/releases)を使用して、プロジェクトを生成します。

AEM プロジェクトの生成方法については、AEM プロジェクトアーキタイプの「[使用手順](https://github.com/adobe/aem-project-archetype#usage)」を参照してください。プロジェクトに CIF を含めるには、`includeCommerce` オプションを使用します。

次に例を示します。

```bash
mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
 -D archetypeGroupId=com.adobe.aem \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=35 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D includeCommerce=y
```

CIF コアコンポーネントは、提供されている `all` パッケージを含めるか、CIF コンテンツパッケージと関連する OSGi バンドルを個別に使用することで、任意のプロジェクトで使用できます。 CIF コアコンポーネントを手動でプロジェクトに追加するには、次の依存関係を使用します。

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
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

### AEM Venia 参照用ストアの使用 {#venia-reference}

CIF プロジェクトを開始する 2 つ目の方法は、[AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)をコピーして使用する方法です。AEM Venia 参照用ストアは、AEM 用の CIF コアコンポーネントの使用方法を示すサンプルのストアフロントアプリケーションです。これは、ベストプラクティス例として意図されていて、独自機能を開発するための有望な出発点としての役割も果たします。

Venia 参照用ストアを使い始めるには、Git リポジトリをクローンし、必要に応じてプロジェクトをカスタマイズし始めます。

>[!NOTE]
>
>Venia 参照用ストアプロジェクトには、AEM as a Cloud Service 用および AEM 6.5 用の 2 つのビルドプロファイルが含まれています。[project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) を参照して、使用方法を確認してください。

## その他のリソース {#additional-resources}

* [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
* [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
* [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
