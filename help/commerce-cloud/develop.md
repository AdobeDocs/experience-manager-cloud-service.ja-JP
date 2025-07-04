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
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 100%

---

# AEM Commerce for AEM as a Cloud Service の開発 {#develop}

AEM as a Cloud Service 用の Commerce Integration Framework（CIF）に基づく AEM Commerce プロジェクトの開発は、AEM as a Cloud Service 上の他の AEM プロジェクトと同じルールとベストプラクティスに従います。最初に次の点を確認します。

- [AEM プロジェクトの構造](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=ja)
- [AEM as a Cloud Service の SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=ja)
- [AEM as a Cloud Service の開発ガイドライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=ja)

## AEM as a Cloud Service SDK を使用したローカル開発 {#local}

>[!VIDEO](https://video.tv.adobe.com/v/347038/?quality=12&learn=on&captions=jpn)

CIF プロジェクトを使用する場合は、ローカル開発環境を使用することをお勧めします。AEM as a Cloud Service 用に提供された CIF アドオンは、ローカル開発にも使用できます。このファイルは、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)からダウンロードできます。

CIF アドオンは Sling 機能アーカイブとして提供されます。ソフトウェア配布ポータルで利用できる zip ファイルには、2 つの Sling 機能アーカイブファイルが含まれています。1 つは AEM オーサー用、もう 1 つは AEM パブリッシュインスタンス用です。

**AEM as a Cloud Service は初めてですか？** AEM as a Cloud Service SDK を使用してローカル開発環境をセットアップするための、より詳細な[ガイド](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=ja)を参照してください。

### 必要なソフトウェア

以下をローカルにインストールしておく必要があります。

- [AEM as a Cloud Service の SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=ja#download-the-aem-as-a-cloud-service-sdk)
- [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/)（3.3.9 以降）
- [Node.js v10 以降](https://nodejs.org/ja)
- [npm 6 以降](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### CIF アドオンへのアクセス

CIF アドオンは、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)から zip ファイルとしてダウンロードできます。Zip ファイルには、CIF アドオンが **Sling 機能アーカイブ**&#x200B;として含まれています。これは、AEM パッケージではありません。SDK リストには、AEM as a Cloud Serviceライセンスでアクセスできます。

>[!TIP]
>
>常に最新バージョンの CIF アドオンを使用していることを確認してください。

### ローカル設定

AEM as a Cloud Service SDK を使用するローカル CIF アドオン開発の場合は、次の手順に従います。

1. 最新の AEM as a Cloud Service SDK を取得します。
1. AEM .jar を解凍して `crx-quickstart` フォルダーを作成し、次を実行します。

   ```bash
   java -jar <jar name> -unpack
   ```

1. `crx-quickstart/install` フォルダーの作成
1. CIF アドオンの正しい Sling 機能アーカイブファイルを `crx-quickstart/install` フォルダーにコピーします。

   CIF アドオンの zip ファイルには、2 つの Sling 機能アーカイブ `.far` ファイルが含まれています。ローカル AEM as a Cloud Service SDK を実行する方法に応じて、AEM オーサーまたは AEM パブリッシュに対して正しいものを使用してください。

1. Adobe Commerce GraphQL エンドポイントを保持する `COMMERCE_ENDPOINT` という名前のローカル OS 環境変数を作成します。

   例：macOS X

   ```bash
   export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   Windows の例：

   ```bash
   set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   この変数は、AEM でコマースシステムへの接続に使用されます。また、CIF アドオンには、Commerce GraphQL エンドポイントをローカルで使用できるようにするローカルリバースプロキシが含まれています。このプロキシは、CIF オーサリングツール（製品コンソールおよびピッカー）で使用され、GraphQL の直接呼び出しを行う CIF クライアントサイドコンポーネントにも使用されます。

   この変数は、AEM as a Cloud Service 環境に対しても設定する必要があります。変数について詳しくは、[AEM as a Cloud Service の OSGi の設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=ja#local-development)を参照してください。

1. （オプション）ステージング済みカタログ機能を有効にするには、Adobe Commerce インスタンスの統合トークンを作成する必要があります。[概要](./getting-started.md#staging)の手順に従って、トークンを作成します。

   `COMMERCE_AUTH_HEADER` という名前の OSGi シークレットを次の値に設定します。

   ```xml
   Authorization: Bearer <Access Token>
   ```

   シークレットについて詳しくは、[AEM as a Cloud Service の OSGi の設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=ja#local-development)を参照してください。

1. AEM as a Cloud Service SDK を開始します。

>[!NOTE]
>
>手順 5 で設定した環境変数と同じターミナルウィンドウで、AEM as a Cloud Service SDK を起動します。別のターミナルウィンドウで起動するか .jar ファイルをダブルクリックして起動する場合、環境変数が表示されていることを確認します。

OSGI コンソールを使用して設定を確認します：`http://localhost:4502/system/console/osgi-installer`。このリストには、機能モデルファイルで定義されている CIF アドオン関連バンドル、コンテンツパッケージ、OSGI 設定が含まれている必要があります。

## プロジェクトのセットアップ {#project}

AEM as a Cloud Service 用の CIF プロジェクトを Bootstrap するには、2 つの方法があります。

### AEM プロジェクトアーキタイプの使用

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

### AEM Venia 参照用ストアの使用

CIF プロジェクトを開始する 2 つ目の方法は、[AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)をコピーして使用する方法です。AEM Venia 参照用ストアは、AEM 用の CIF コアコンポーネントの使用方法を示すサンプルのストアフロントアプリケーションです。これは、ベストプラクティス例として意図されていて、独自機能を開発するための有望な出発点としての役割も果たします。

Venia 参照用ストアを使い始めるには、Git リポジトリをクローンし、必要に応じてプロジェクトをカスタマイズし始めます。

>[!NOTE]
>
>Venia 参照用ストアプロジェクトには、AEM as a Cloud Service 用および AEM 6.5 用の 2 つのビルドプロファイルが含まれています。[project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) を参照して、使用方法を確認してください。

## その他のリソース

- [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
- [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
