---
title: プロジェクトのコンテンツパッケージ構造の理解
description: Adobe Experience Managerクラウドサービスへの展開用にパッケージ構造を適切に定義する方法について説明します。
translation-type: tm+mt
source-git-commit: cedc14b0d71431988238d6cb4256936a5ceb759b

---


# Adobe Experience Managerクラウドサービスのプロジェクトコンテンツパッケージの構造について {#understand-cloud-service-package-structure}

>[!TIP]
>
>この記事では、 [AEM Projectの基本的なアーキタイプの使用](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)、およびこれらの学習と概念に基づいて構築される [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html) FileVault Content Mavenプラグインについて理解してください。

この記事では、可変コンテンツと不変コンテンツの分割を確実に尊重し、AEMクラウドサービスとの互換性を確保するためにAdobe Experience Manager Mavenプロジェクトに必要な変更点について説明します。矛盾しない決定論的デプロイメントを作り出すために必要な依存関係が確立され、展開可能な構造にパッケージ化されていることを確認します。

AEMアプリケーションのデプロイメントは、単一のAEMパッケージで構成する必要があります。 次に、このパッケージには、コード、設定、サポートするベースラインコンテンツなど、アプリケーションが機能するのに必要なすべてを構成するサブパッケージが含まれている必要があります。

AEMでは、コンテンツとコ **ードを分離する必要があります** 。つまり、1つのコンテンツパッケージをランタイムと書き込み可能な ************`/apps` エリア(例：リポ `/content`ジトリ `/conf`の、 `/home`、、または何も `/apps`)を表示します。 代わりに、アプリケーションは、AEMにデプロイするために、コードとコンテンツを個別のパッケージに分割する必要があります。

このドキュメントで概要を説明するパッケージ構造は、ローカル開発デプ **ロイメント** 、およびAEMクラウドサービスデプロイメントの両方と互換性があります。

>[!TIP]
>
>このドキュメントで概要を説明する設定は、 [AEM Project Maven Archetype 21以降で提供されます](https://github.com/adobe/aem-project-archetype/releases)。

## リポジトリの可変領域と不変領域 {#mutable-vs-immutable}

`/apps` また `/libs` 、AEMの **** 開始後（例：実行時）に変更（作成、更新、削除）できないため、AEMの不変領域と見なされます。 実行時に不変領域を変更しようとすると失敗します。

リポジトリ、、、、、、、、 `/content``/conf``/var``/home``/etc``/oak:index``/system``/tmp`、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、などのすべてです。 はすべて可 **変領域で** 、実行時に変更できます。

>[!WARNING]
>
> AEMの以前のバージョンと同様、変更しな `/libs` いでください。 にデプロイできるのは、AEM製品コードのみで `/libs`す。

## 推奨パッケージ構造 {#recommended-package-structure}

![Experience Managerプロジェクトパッケージ構造](assets/content-package-organization.png)

次の図は、推奨されるプロジェクト構造とパッケージ展開アーティファクトの概要を示しています。

推奨されるアプリケーションのデプロイメント構造は次のとおりです。

+ パッケ `ui.apps` ージ（コンテンツパッケージ）には、展開するすべてのコードが含まれ、展開先のみが含まれま `/apps`す。 パッケージの共通の要素 `ui.apps` は次のとおりです。
   + OSGiバンドル
      + `/apps/my-app/install`
   + OSGi設定
      + `/apps/my-app/config`
   + HTLスクリプト
      + `/apps/my-app/components`
   + JavaScriptとCSS（クライアントライブラリを使用）
      + `/apps/my-app/clientlibs`
   + /libsのオーバーレイ
      + `/apps/cq`, `/apps/dam/`, etc.
   + 代替のコンテキスト対応設定
      + `/apps/settings`
   + ACL（権限）
      + 任 `rep:policy` 意のパス `/apps`
+ パッケー `ui.content` ジ（コードパッケージ）には、すべてのコンテンツと設定が含まれます。 パッケージの共通の要素 `ui.content` は次のとおりです。
   + コンテキスト対応設定
      + `/conf`
   + ベースラインコンテンツ構造（アセットフォルダ、サイトのルートページ）
      + `/content`, `/content/dam`, etc.
   + 管理されるタグ分類
      + `/content/cq:tags`
   + サービスユーザー
      + `/home/users`
   + ユーザーグループ
      + `/home/groups`
   + Oakインデックス
      + `/oak:indexes`
   + Etcレガシーノード
      + `/etc`
   + ACL（権限）
      + 次の値 `rep:policy` を含まな **いパス** : `/apps`
+ パッケ `all` ージは、およびパッケージを埋め込んだコンテ `ui.apps` ナパッ `ui.content` ケージです。 パッケ `all` ージに独自のコンテ **ンツを含めることはできず** 、リポジトリのすべてのデプロイメントをそのサブパッケージに委任します。

   パッケージは、Maven [FileVaultパッケージMavenプラグインの埋め込み設定を使用して](#embeddeds)、設定ではなく含まれるようにな `<subPackages>` りました。

   複雑なExperience Managerのデプロイメントの場合は、AEMで特定のサイトまたはテナントを表す複数 `ui.apps` のプロジ `ui.content` ェクト/パッケージを作成することが望ましい場合があります。 これを行う場合は、可変コンテンツと不変コンテンツの分割が考慮され、必要なコンテンツパッケージがコンテナコンテンツパッケージ内のサブパッケージとして追 `all` 加されます。

   例えば、複雑な展開コンテンツパッケージ構造は次のようになります。

   + `all` コンテンツパッケージには、単数の展開アーティファクトを作成するために、次のパッケージが埋め込まれています
      + `ui.apps.common` サイトAとサイトBの両方で **必要な** 、コードを導入します。
      + `ui.apps.site-a` サイトAに必要なコードを導入
      + `ui.content.site-a` サイトAに必要なコンテンツと設定をデプロイします。
      + `ui.apps.site-b` サイトBに必要なコードをデプロイします
      + `ui.content.site-b` サイトBに必要なコンテンツと設定をデプロイします。

## パッケージタイプ {#package-types}

パッケージは、宣言されたパッケージタイプでマークされます。

+ コンテナパッケージにはセットを含めることはで `packageType` きません。
+ コード（不変）パッケージは、をに設定する必要が `packageType` ありま `application`す。
+ コンテンツ（可変）パッケージは、をに設定する必要が `packageType` ありま `content`す。

詳しくは、 [Apache Jackrabbit fileVault - Package Maven pluginのドキュメントと](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) 、以下の [FileVault Maven設定スニペットを参照してください](#marking-packages-for-deployment-by-adoube-cloud-manager) 。

>[!TIP]
>
>完全なスニペットについては [](#xml-package-types) 、以下の「POM XMLスニペット」の節を参照してください。

## Adobe Cloud Managerによる展開用のパッケージのマーク {#marking-packages-for-deployment-by-adoube-cloud-manager}

デフォルトでは、Adobe Cloud ManagerはMavenビルドで作成されたすべてのパッケージをハーベストしますが、コンテナ(`all`)パッケージはすべてのコードおよびコンテンツパッケージを含む単数の展開アーティファクトなので、必ずコンテナ **(**`all`)パッケージのみを展開します。 これを確実に行うには、Mavenビルドで生成される他のパッケージに、のFileVaultコンテンツパッケージMavenプラグイン設定でマークする必要がありま `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`す。

>[!TIP]
>
>完全なスニペットについては [](#pom-xml-snippets) 、以下の「POM XMLスニペット」の節を参照してください。

## リポジトリ構造パッケージ {#repository-structure-package}

コードパッケージは、（あるコードパッケージが別のコードパッケージにインストールされないように）構造的依存関係の正確性を強制する設定を参照するように、FileVault Mavenプラグインの設定を行う必要があります。 `<repositoryStructurePackage>` プロジェクト [用に独自のリポジトリ構造パッケージを作成できます](repository-structure-package.md)。

これは、コード **パッケージ** （「」でマークされたパッケージ）に対してのみ必要で `<packageType>application</packageType>`す。

アプリケーション用のリポジトリ構造パッケージの作成方法については、「リポジトリ構造パッケ [ージの作成」を参照してください](repository-structure-package.md)。

コンテンツパッケージ(`<packageType>content</packageType>`)には、このリポ **ジトリ構造パッケージ** は必要ありません。

>[!TIP]
>
>完全なスニペットについては [](#xml-repository-structure-package) 、以下の「POM XMLスニペット」の節を参照してください。

## コンテナパッケージへのサブパッケージの埋め込み{#embeddeds}

コンテンツまたはコードパッケージは、特別な「サイドカー」フォルダに配置され、FileVault Mavenプラグインの設定を使用して、AEM作成者、AEM発行、またはその両方にインストールする対象とすることができ `<embeddeds>` ます。 設定は使用しな `<subPackages>` いでください。

一般的な使用例を次に示します。

+ AEM作成者ユーザーとAEM発行ユーザーで異なるACL/権限
+ AEM作成者でのみアクティビティをサポートするために使用される設定
+ バックオフィスシステムとの統合など、AEM作成者でのみ実行する必要のあるコード

![パッケージの埋め込み](assets/embeddeds.png)

AEM作成者、AEM発行またはその両方をターゲットにするには、パッケージを次の形式で特別なフォルダー内のコンテナ `all` パッケージに埋め込みます。

`/apps/<app-name>-packages/(content|application)/install(.author|.publish)?`

このフォルダー構造を分類する：

+ 第1レベルのフォルダーが必要 **です**`/apps`。
+ 第2レベルのフォルダーは、フォルダー名にポストフィック `-packages` スされたアプリケーションを表します。 多くの場合、すべてのサブパッケージが埋め込まれる2番目のフォルダーは1つだけですが、アプリケーションの論理構造を最も適切に表すために、任意の数の2番目のフォルダーを作成できます。
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`
   >[!WARNING]
   >
   >慣例により、サブパッケージの埋め込みフォルダーには、のサフィックスを付けて名前が付けられま `-packages`す。 これにより、展開コードとコンテンツパッケージが **** 、サブパッケージの対象フォルダーに展開されなくなり、インストールが破壊的で `/apps/<app-name>/...` 循環的に行われることがなくなります。

+ 3番目のレベルのフォルダーは、
   「`application`」または「`content`」
   + このフォル `application` ダーにはコードパッケージが格納されます
   + フォルダ `content` ーはコンテンツパッケージを収集します。このフォルダー名は、含まれ [るパッケージ](#package-types) のパッケージタイプに対応している必要があります。
+ 第4レベルのフォルダーにはサブパッケージが含まれ、次のいずれかである必要があります。
   + `install` aem作成者とAEM発行 **の両方に** 、をインストールするには
   + `install.author` AEM作成者 **にのみ** 、インストールするには
   + `install.publish` をAEM **publishNoteにのみインストールする場合は、ターゲッ** トのみと `install.author``install.publish` がサポートされます。 その他の実行モードはサ **ポートされていませ** ん。

例えば、AEM作成者を含む展開と特定のパッケージを発行する展開は、次のようになります。

+ `all` コンテナパッケージは、単数の展開アーティファクトを作成するために、次のパッケージを埋め込みます
   + `ui.apps` 埋め込み：AEM `/apps/my-app-packages/application/install` 作成者とAEM発行の両方にコードをデプロイします
   + `ui.apps.author` 「組み込み」を選択す `/apps/my-app-packages/application/install.author` ると、AEM作成者のみにコードがデプロイされます。
   + `ui.content` 埋め込み：コン `/apps/my-app-packages/content/install` テンツと設定をAEM作成者とAEM発行の両方にデプロイします
   + `ui.content.publish` 埋め込み：コン `/apps/my-app-packages/content/install.publish` テンツと設定をAEM発行のみにデプロイ

>[!TIP]
>
>完全なスニペットについては [](#xml-embeddeds) 、以下の「POM XMLスニペット」の節を参照してください。

### コンテナパッケージのフィルター定義 {#container-package-filter-definition}

コンテナパッケージにコードとコンテンツのサブパッケージが埋め込まれるので、埋め込まれたターゲットパスをコンテナプロジェクトのに追加して、埋め込まれたパッケージがコンテナパッケージの構築時に確実に含まれるようにする必要があります。 `filter.xml`

展開するサブパ `<filter root="/apps/<my-app>-packages"/>` ッケージを含む2番目のフォルダーのエントリを追加するだけです。

>[!TIP]
>
>完全なスニペットについては [](#xml-container-package-filters) 、以下の「POM XMLスニペット」の節を参照してください。

## サードパーティパッケージの埋め込み {#embedding-3rd-party-packages}

すべてのパッケージは、 [AdobeのパブリックMavenアーティファクトリポジトリまたはアクセス可能なパブリックな、参照可能な](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) 、サードパーティのMavenアーティファクトリポジトリを介して使用できる必要があります。

サードパーティパッケージがアドビのパブリックMavenアーティファクトリポジトリにある場合 ****、Adobe Cloud Managerでアーティファクトを解決するためには、それ以上の設定は必要ありません。

サードパーティパッケージがパブリックサードパーティ **Mavenアーティファクトリポジトリにある場合は**、このリポジトリをプロジェクトのリポジトリに登録し、上述の方法に従って埋め込む `pom.xml` 必要が [あります](#embeddeds)。 サードパーティのアプリケーション/コネクターにコードパッケージとコンテンツパッケージの両方が必要な場合は、それぞれコンテナ(`all`)パッケージ内の正しい場所に埋め込む必要があります。

Maven依存関係の追加は、標準的なMavenの手法に従い、サードパーティのアーティファクト（コードおよびコンテンツパッケージ）の埋め込みは、上記 [で説明しま](#embedding-3rd-party-packages)す。

>[!TIP]
>
>完全なスニペットについては [](#xml-3rd-party-maven-repositories) 、以下の「POM XMLスニペット」の節を参照してください。

## fromパッケージ間のパッケ `ui.apps` ージの `ui.content` 依存 {#package-dependencies}

パッケージの適切なインストールを確実に行うために、パッケージ間の依存関係を確立することをお勧めします。

一般的なルールは、可変コンテンツ(`ui.content`)を含むパッケージで、可変コンテンツ(`ui.apps`)のレンダリングと使用をサポートする不変コンテンツ()に依存します。

>[!TIP]
>
>完全なスニペットについては [](#xml-package-dependencies) 、以下の「POM XMLスニペット」の節を参照してください。

コンテンツパッケージの依存関係の一般的なパターンは次のとおりです。

### シンプルな展開パッケージの依存関係 {#simple-deployment-package-dependencies}

簡易ケースは、不変コードパッ `ui.content` ケージに依存する可変コンテンツパッケージ `ui.apps` を設定する。

+ `all` 依存関係がありません
   + `ui.apps` 依存関係がありません
   + `ui.content` ～に依存する `ui.apps`

### 複雑な展開パッケージの依存関係 {#complex-deploxment-package-dependencies}

複雑な導入は、単純なケースに対して拡張され、対応する可変コンテンツと不変コードパッケージの間に依存関係を設定します。 必要に応じて、不変コードパッケージ間の依存関係も確立できます。

+ `all` 依存関係がありません
   + `ui.apps.common` 依存関係がありません
   + `ui.apps.site-a` ～に依存する `ui.apps.common`
   + `ui.content.site-a` ～に依存する `ui.apps.site-a`
   + `ui.apps.site-b` ～に依存する `ui.apps.common`
   + `ui.content.site-b` ～に依存する `ui.apps.site-b`

## ローカル開発と展開 {#local-development-and-deployment}

この記事で概要を説明するプロジェクト構造と組織は、ローカル開発 **用AEMインスタンス** と完全に互換性があります。

## POM XMLスニペット {#pom-xml-snippets}

以下は、Mavenプロジェ `pom.xml` クトに追加して、上記のレコメンデーションに合わせることができるMaven設定スニペットです。

### パッケージタイプ {#xml-package-types}

サブパッケージとして展開されるコードおよびコンテンツパッケージでは、パッケージに含まれる内容に応じて **** 、アプリケーションまたは ****&#x200B;コンテンツのパッケージタイプを宣言する必要があります。

#### コンテナパッケージタイプ {#container-package-types}

コンテナプロジ `all/pom.xml` ェクト **では** 、を宣言しませ `<packageType>`ん。

#### コード（不変）パッケージタイプ {#immutable-package-types}

コードパッケージでは、をに設定する必要 `packageType` がありま `application`す。

では、プラ `ui.apps/pom.xml`グイン宣 `<packageType>application</packageType>` 言のビルド設定ディレク `filevault-package-maven-plugin` ティブがパッケージ型を宣言します。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>${my-app.ui.apps}</name>
        <packageType>application</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

#### コンテンツ（可変）パッケージタイプ {#mutable-package-types}

コンテンツパッケージでは、をに設定する必要 `packageType` がありま `content`す。

では、プラ `ui.content/pom.xml`グイン宣 `<packageType>content</packageType>` 言のビルド設定ディレクティブがパッ `filevault-package-maven-plugin` ケージ型を宣言します。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>${my-app.ui.content}</name>
        <packageType>content</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Adobe Cloud Manager展開用のパッケージのマーク {#cloud-manager-target}

パッケージを生成するすべてのプロジェクトで **、** container`all`( `<cloudManagerTarget>none</cloudManagerTarget>` )プロジェクトを除き、Adobe Cloud Managerによって展開されないように、プラグイン宣言の設定に `<properties>` 追 `filevault-package-maven-plugin`**** 加してください。 コンテナ(`all`)パッケージは、Cloud Managerを使用して展開した単数パッケージで、必要なすべてのコードおよびコンテンツパッケージが埋め込まれます。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### リポジトリ構造パッケージ {#xml-repository-structure-package}

と、コー `ui.apps/pom.xml` ドパッケー `pom.xml` ジ(`<packageType>application</packageType>`)を宣言するその他の任意のコードで、次のリポジトリ構造パッケージ設定をFileVault Mavenプラグインに追加します。 プロジェクト [用に独自のリポジトリ構造パッケージを作成できます](repository-structure-package.md)。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <repositoryStructurePackages>
          <repositoryStructurePackage>
              <groupId>${project.groupId}</groupId>
              <artifactId>repository-structure-pkg</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
```

### コンテナパッケージへのサブパッケージの埋め込み {#xml-embeddeds}

で、次のデ `all/pom.xml`ィレクティブをプラ `<embeddeds>` グイン宣言に `filevault-package-maven-plugin` 追加します。 この設定 **は** 、ではな `<subPackages>` くにサブパッケージを含むので、使用しないで `/etc/packages` ください `/apps/my-app-packages/<application|content>/install(.author|.publish)?`。

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          <!-- Include the application's ui.apps and ui.content packages -->
          <!-- Ensure the artifactIds are correct -->

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys ONLY to AEM Author -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps.author</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install.author</target>
          </embedded>

          <!-- Content package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install</target>
          </embedded>

          <!-- Content package that deploys ONLY to AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content.publish-only</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install.publish</target>
          </embedded>

          <!-- Include any other extra packages such as AEM WCM Core Components -->
          <embedded>
              <groupId>com.adobe.cq</groupId>
              <!-- Not to be confused; WCM Core Components' Code package's artifact is named `.content` -->
              <artifactId>core.wcm.components.content</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/application/install</target>
          </embedded>

          <embedded>
              <groupId>com.adobe.cq</groupId>
              <!-- Not to be confused; WCM Core Components' Content package's artifact is named `.conf` -->
              <artifactId>core.wcm.components.conf</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/content/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

### コンテナパッケージのフィルター定義 {#xml-container-package-filters}

プロジェク `all` トの( `filter.xml` )に、展開す`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`るサ **ブ**`-packages` パッケージを含むフォルダーを含めます。

```xml
<filter root="/apps/my-app-packages"/>
```

埋め込まれたタ `/apps/*-packages` ーゲットで複数を使用する場合は、すべてここに列挙する必要があります。

### サードパーティMavenリポジトリ {#xml-3rd-party-maven-repositories}

reactorプロジェクトの中に、必要なサ `pom.xml`ードパーティのパブリックMavenリポジトリディレクティブを追加します。 完全な設定は、サ `<repository>` ードパーティのリポジトリプロバイダーから利用できる必要があります。

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public 3rd Party Repository</name>
      <url>https://repo.3rdparty.example.com/...</url>
      <releases>
          <enabled>true</enabled>
          <updatePolicy>never</updatePolicy>
      </releases>
      <snapshots>
          <enabled>false</enabled>
      </snapshots>
  </repository>
  ...
</repositories>
```

### fromパッケージ間のパッケ `ui.apps` ージの `ui.content` 依存 {#xml-package-dependencies}

で、次のデ `ui.content/pom.xml`ィレクティブをプラ `<dependencies>` グイン宣言に `filevault-package-maven-plugin` 追加します。

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <dependencies>
        <!-- Declare the content package dependency in the ui.content/pom.xml on the ui.apps project -->
        <dependency>
            <groupId${project.groupId}</groupId>
            <artifactId>my-app.ui.apps</artifactId>
            <version>${project.version}</version>
        </dependency>
      </dependencies>
    ...
  </configuration>
</plugin>
...
```

### コンテナプロジェクトのターゲットフォルダのクリーニング {#xml-clean-container-package}

に、Mavenビル `all/pom.xml` ドの前にタ `maven-clean-plugin` ーゲットディレクトリをクリーンアップするプラグインを追加します。

```xml
<plugins>
  ...
  <plugin>
    <artifactId>maven-clean-plugin</artifactId>
    <executions>
      <execution>
        <id>auto-clean</id>
        <!-- Run at the beginning of the build rather than the default, which is after the build is done -->
        <phase>initialize</phase>
        <goals>
          <goal>clean</goal>
        </goals>
      </execution>
    </executions>
  </plugin>
  ...
</plugins>
```

## その他のリソース {#additional-resources}

+ [Maven を使用したパッケージの管理](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html)
+ [FileVaultコンテンツパッケージMavenプラグイン](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
