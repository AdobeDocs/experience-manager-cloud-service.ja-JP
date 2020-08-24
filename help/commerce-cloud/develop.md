---
title: Cloud ServiceとしてのAEM向けAEMコマースの開発
description: Cloud ServiceとしてのAEM向けAEMコマースの開発
translation-type: tm+mt
source-git-commit: 19fa6391913f556b80607f8dd5215489082b50ab
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 14%

---


# Cloud ServiceとしてのAEM向けAEMコマースの開発 {#develop}

AEM用のCommerce Integration Framework(CIF)に基づくAEM Commerceプロジェクトの開発は、AEM上の他のAEMプロジェクトと同じルールとベストプラクティスに従い、Cloud Serviceも同様です。 最初に以下を確認してください。

- [AEM プロジェクトの構造](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.translate.html)
- [AEM as a Cloud Service の SDK](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [AEM as a Cloud Service の開発ガイドライン](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## Cloud ServiceSDKとしてのAEMを使用したローカル開発 {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

CIFプロジェクトを使用する場合は、ローカル開発環境を使用することをお勧めします。 AEM用に提供されたCIF追加-Onは、Cloud Service環境としても、ローカル開発にも使用できます。 このファイルは、 [ソフトウェア配布ポータルからダウンロードできます](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html)。

CIF追加オンはSling機能アーカイブとして提供されます。 ソフトウェア配布ポータルで利用できるzipファイルには、2つのSling機能アーカイブファイルが含まれています。1つはAEM作成者用、もう1つはAEM発行インスタンス用です。

**AEMを初めてCloud Serviceに？** AEM [をCloud ServiceSDKとして使用し、ローカル開発環境をセットアップするための、より詳細なガイドを参照してください](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)。

### 必要なソフトウェア

次のファイルをローカルにインストールする必要があります。

- [AEM as a Cloud Service の SDK](https://docs.adobe.com/content/help/en/*experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) （3.3.9以降）
- [Node.js v10 以降](https://nodejs.org/en/)
- [npm 6 以降](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### CIFアドオンへのアクセス

The CIF add-on can be downloaded as a zip file from the [Software Distribution portal](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html). zipファイルには、 **Sling機能アーカイブとしてのCIFアドオンが含まれています**。AEMパッケージではありません。 SDKリストへのアクセスは、AEMがCloud Serviceライセンスとして使用されているものに制限されます。

>[!TIP]
>
>常に最新バージョンのCIF追加-Onを使用していることを確認してください。

### ローカル設定

AEMをCloud ServiceSDKとして使用するローカル追加のCIFオン開発の場合は、次の手順に従います。

1. Cloud ServiceSDKとして最新のAEMを取得する
2. AEM .jarを解凍し、 `crx-quickstart` フォルダーを作成します。次を実行します。

   ```bash
   java -jar <jar name> -unpack
   ```

3. Create a `crx-quickstart/install` folder
4. CIFアドオンの正しいSling機能アーカイブファイルを `crx-quickstart/install` フォルダーにコピーします。

   CIFアドオンのzipファイルには、2つのSling機能アーカイブ `.far` ファイルが含まれています。 ローカルAEMをCloud ServiceSDKとして実行する方法に応じて、AEM AuthorまたはAEM Publishに正しいものを使用してください。

5. MagentoGraphQLエンドポイントを保持するという名前のローカルOS環境変数 `COMMERCE_ENDPOINT` を作成します。

   Mac OSXの例：

   ```bash
   export COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   ウィンドウの例：

   ```bash
   set COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   この変数は、AEMのCloud Service環境としても設定する必要があります。

6. Cloud ServiceSDKとしてのAEMの開始

OSGIコンソールを使用してセットアップを確認します：`http://localhost:4502/system/console/osgi-installer`。 このリストには、機能モデルファイルで定義されているCIFアドオン関連バンドル、コンテンツパッケージ、OSGI設定が含まれている必要があります。

## プロジェクトのセットアップ {#project}

AEM用のCIFプロジェクトをCloud Serviceとしてブートストラップするには、2つの方法があります。

### AEMプロジェクトのアーキタイプを使用

CIFを使い始めるために事前に設定されたプロジェクトをブートストラップするには、 [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) （プロジェクトアーキタイプ）が主なツールです。 CIFコアコンポーネントと必要なすべての設定を、1つの追加オプションで生成されたプロジェクトに含めることができます。

>[!TIP]
>
>プロジェクトを生成するには、 [AEM Project Archetype 24以降を使用し](https://github.com/adobe/aem-project-archetype/releases) ます。

AEMプロジェクトの生成方法については、「AEM Project [のアーキタイプ使用手順](https://github.com/adobe/aem-project-archetype#usage) 」を参照してください。 プロジェクトにCIFを含めるには、この `includeCommerce` オプションを使用します。

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

CIFコアコンポーネントは、提供されているパッケージを含めるか、CIFコンテンツパッケージと関連するOSGIバンルを個別に使用することで、任意のプロジェクトで使用でき `all` ます。 CIFコアコンポーネントを手動でプロジェクトに追加するには、次の依存関係を使用します。

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

### AEM Venia Reference Storeを使用

CIFプロジェクトを開始する2つ目の方法は、 [AEM Venia Reference Storeをコピーして使用する方法で](https://github.com/adobe/aem-cif-guides-venia)す。 AEM Venia Reference Storeは、AEM用のCIFコアコンポーネントの使用方法を示すサンプルの参照ストアフロントアプリケーションです。 これは、例のベストプラクティスのセットとしての意図と、独自の機能を開発するための潜在的な出発点としての役割を果たします。

Venia Reference Storeを使い始めるには、Gitリポジトリをコピーし、必要に応じてプロジェクトをカスタマイズする開始を作成します。

>[!NOTE]
>
>Venia Reference Storeプロジェクトには、AEM用の2つのビルドプロファイルがCloud Serviceとして含まれています。AEM 6.5. [project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) を参照して、その使用方法を確認してください。

## その他のリソース

- [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
- [AEM Veniaリファレンスストア](https://github.com/adobe/aem-cif-guides-venia)
- [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html)
