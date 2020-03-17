---
title: AEMプロジェクト構造
description: Adobe Experience Manager Cloud Serviceに展開するパッケージ構造を定義する方法について説明します。
translation-type: tm+mt
source-git-commit: fb398147c5a2635f58250b8de886159b4ace2943

---


# AEMプロジェクト構造

>[!TIP]
>
>基本的な [AEM Project Archetypeの使用と](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)、この記事がこれらの学習と概念に基づいて構築される [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html) FileVault Content Mavenプラグインについてよく理解してください。

この記事では、Adobe Experience Manager MavenプロジェクトでAEMクラウドサービスとの互換性を維持するために必要な変更について、可変コンテンツと不変コンテンツの分割を確実に尊重するように説明します。矛盾しない決定的なデプロイメントを作成するために必要な依存関係が確立され、展開可能な構造でパッケージ化されていることを確認します。

AEMアプリケーションのデプロイメントは、単一のAEMパッケージで構成される必要があります。 次に、このパッケージには、コード、設定、サポートするベースラインコンテンツなど、アプリケーションが機能するのに必要なすべてを構成するサブパッケージが含まれている必要があります。

AEM では&#x200B;**コンテンツ**&#x200B;と&#x200B;**コード**&#x200B;を分離する必要があります。つまり、`/apps` とリポジトリのランタイム書き込み可能領域（例：`/content`、`/conf`、`/home`、または `/apps` 以外）の&#x200B;**両方**&#x200B;に 1 つのコンテンツパッケージをデプロイすることは&#x200B;**できません**。代わりに、アプリケーションは、AEM にデプロイするために、コードとコンテンツを個別のパッケージに分割する必要があります。

このドキュメントで説明したパッケージ構造は、ローカル開発デプロイメントおよび AEM Cloud サービスデプロイメントの&#x200B;**両方**&#x200B;と互換性があります。

>[!TIP]
>
>このドキュメントで概要を説明する設定は、 [AEM Project Maven Archetype 21以降で提供されます](https://github.com/adobe/aem-project-archetype/releases)。

## リポジトリの可変領域と不変領域 {#mutable-vs-immutable}

`/apps` と `/libs` は AEM の開始後（例：実行時）に変更（作成、更新、削除）できないため、AEM の&#x200B;**不変**&#x200B;領域と見なされます。実行時に不変領域を変更しようとすると失敗します。

リポジトリ内のその他す `/content`べて、、、、、、、、、、、 `/conf`、、、、、、、な `/var`ど `/etc``/oak:index``/system``/tmp`が、 はすべて可変 **領域で** 、実行時に変更できます。

>[!WARNING]
>
> 以前のバージョンのAEMと同様、変更 `/libs` しないでください。 にデプロイできるのは、AEM製品コードのみで `/libs`す。

## 推奨されるパッケージ構造 {#recommended-package-structure}

![Experience Managerプロジェクトのパッケージ構造](assets/content-package-organization.png)

次の図は、推奨されるプロジェクト構造とパッケージの展開アーティファクトの概要を示しています。

推奨されるアプリケーションのデプロイメント構造は次のとおりです。

+ パッケ `ui.apps` ージ（コンテンツパッケージ）には、展開するすべてのコードが含まれ、展開先のみが含まれま `/apps`す。 パッケージの一般的な要素 `ui.apps` には、次のものが含まれます。
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
      + 任意の `rep:policy` パス( `/apps`
   + Repo Init OSGi設定ディレクティブ（および付属のスクリプト）
      + [AEMアプリケーションの論理的な一部であるコンテンツをデプロイ（可変）する方法として、Repo Initを使用することをお勧めします。](#repo-init) 次を定義するには、Repo Initを使用する必要があります。
         + ベースラインコンテンツ構造
            + `/conf/my-app`
            + `/content/my-app`
            + `/content/dam/my-app`
         + ユーザー
         + サービスユーザ
         + グループ
         + ACL（権限）
            + 任意のパ `rep:policy` ス（ミュート可能または不変）
+ パッケージ `ui.content` （コードパッケージ）には、すべてのコンテンツと設定が含まれています。 パッケージの一般的な要素 `ui.content` には、次のものが含まれます。
   + コンテキストに応じた設定
      + `/conf`
   + 必須で複雑なコンテンツ構造( Repo Initで定義された過去のベースラインコンテンツ構造に基づいて構築され、拡張されるコンテンツの構築。
      + `/content`, `/content/dam`, etc.
   + 管理されるタグ分類
      + `/content/cq:tags`
   + Oakインデックス
      + `/oak:index`
   + Etcレガシーノード
      + `/etc`
+ `all` パッケージは、`ui.apps` および `ui.content` パッケージを埋め込んだコンテナパッケージです。`all` パッケージに独自の&#x200B;**コンテンツ**&#x200B;を含めることはできませんが、リポジトリのすべてのデプロイメントをそのサブパッケージに委任します。

   パッケージは、Maven [FileVaultパッケージMavenプラグインの埋め込み設定を使用して](#embeddeds)、設定ではなく含まれるようになり `<subPackages>` ました。

   複雑なExperience Managerのデプロイメントの場合は、AEMの特定のサイトまたはテナントを表す複数の `ui.apps` プロジェ `ui.content` クト/パッケージを作成することが望ましい場合があります。 これを行う場合は、可変コンテンツと不変コンテンツの分割が考慮され、必要なコンテンツパッケージがコンテナコンテンツパッケージのサブパッケージとして追 `all` 加されます。

   例えば、複雑な展開コンテンツパッケージ構造は次のようになります。

   + `all` コンテンツパッケージには、以下のパッケージが埋め込まれ、単数の展開アーティファクトを作成します。
      + `ui.apps.common` サイトAとサイトBの両方で **必要な** 、コードを導入します。
      + `ui.apps.site-a` サイトAに必要なコードをデプロイします。
      + `ui.content.site-a` サイトAに必要なコンテンツと設定をデプロイします。
      + `ui.apps.site-b` サイトBに必要なコードを導入
      + `ui.content.site-b` サイトBに必要なコンテンツと設定をデプロイします。

## パッケージタイプ {#package-types}

パッケージは、宣言されたパッケージタイプでマークされます。

+ コンテナパッケージにはセットを含めることはで `packageType` きません。
+ コード（不変）パッケージは、をに設定する必要が `packageType` ありま `application`す。
+ コンテンツ（可変）パッケージは、に設定する必要が `packageType` ありま `content`す。

詳しくは、 [Apache Jackrabbit FileVault - Package Maven Pluginのドキュメント](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) 、および以下の [FileVault Maven設定スニペットを参照してください](#marking-packages-for-deployment-by-adoube-cloud-manager) 。

>[!TIP]
>
>完全なスニペットについては、 [以下の「POM XMLスニペット](#xml-package-types) 」の節を参照してください。

## Adobe Cloud Managerによる展開用のパッケージのマーク {#marking-packages-for-deployment-by-adoube-cloud-manager}

デフォルトでは、Adobe Cloud Manager は Maven ビルドで作成されたすべてのパッケージを収集しますが、コンテナ（`all`）パッケージはすべてのコードおよびコンテンツパッケージを含む 1 つのデプロイメントアーティファクトなので、必ずコンテナ（`all`）パッケージ&#x200B;**のみ**&#x200B;をデプロイするようにします。これを確実におこなうには、Maven ビルドで生成される他のパッケージに、FileVault コンテンツパッケージ Maven プラグイン設定 `<properties><cloudManagerTarget>none</cloudManageTarget></properties>` でマークする必要があります。

>[!TIP]
>
>完全なスニペットについては、 [以下の「POM XMLスニペット](#pom-xml-snippets) 」の節を参照してください。

## リポジトリの初期化{#repo-init}

Repo Initは、フォルダーツリーなどの一般的なノード構造から、ユーザー、サービスユーザー、グループ、ACL定義まで、JCR構造を定義する命令（スクリプト）を提供します。

リポジトリ初期化の主な利点は、スクリプトで定義されたすべてのアクションを実行する暗黙の権限があり、デプロイのライフサイクルの早い段階で呼び出され、必要なJCR構造がすべて実行されることです。

Repo Initスクリプト自体はスクリプトとしてプロジェ `ui.apps` クト内に存在しますが、スクリプトは次の可変構造を定義するために使用でき、また使用する必要があります。

+ ベースラインコンテンツ構造
   + Examples: `/content/my-app`, `/content/dam/my-app`, `/conf/my-app/settings`
+ サービスユーザ
+ ユーザー
+ グループ
+ ACL

Repo Initスクリプトは `scripts``RepositoryInitializer` OSGiファクトリ設定のエントリとして保存されるので、実行モードで暗黙的にターゲット化でき、AEM AuthorとAEM Publish ServicesのRepo Initスクリプトの違いや、Envs（開発、ステージ、実行）との違いが生じます。

ユーザーとグループを定義する場合、グループのみがアプリケーションの一部と見なされ、関数に不可欠な要素がここで定義される必要があります。 組織のユーザーとグループは、実行時にAEMで定義する必要があります。例えば、カスタムワークフローが名前付きのグループに作業を割り当てる場合、そのグループはAEMアプリケーションのRepo Initを介して定義する必要がありますが、グループ化が単なる組織（「Wendy&#39;s Team」や「Sean&#39;s Team」など）の場合、これらは最適な定義で、実行時に管理されます。

>[!TIP]
>
>Repo Initスクリプト *は* 、インラインフィールドで `scripts` 定義する必要があり `references` 、設定は機能しません。

Repo Initスクリプトの全語彙は、 [Apache Sling Repo Initドキュメントで入手できます](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)。

>[!TIP]
>
>完全なスニペット [については、下の「初期化レポート](#snippet-repo-init) 」のセクションを参照してください。

## リポジトリ構造パッケージ {#repository-structure-package}

コードパッケージは、（あるコードパッケージが別のコードパッケージにインストールされないように）構造的依存関係の正確性を強制する構造を参照するように、FileVault Mavenプラグインの設定を構成する必要があります。 `<repositoryStructurePackage>` プロジェクト [用に独自のリポジトリ構造パッケージを作成できます](repository-structure-package.md)。

これは、コードパッケージ （`<packageType>application</packageType>` でマークされたパッケージ）に対して&#x200B;**のみ必要**&#x200B;です。

アプリケーション用のリポジトリ構造パッケージの作成方法については、「リポジトリ構造パッケージ [の作成」を参照してくださ](repository-structure-package.md)い。

コンテンツパッケージ(`<packageType>content</packageType>`)には、こ **のリポジトリ構造パッケージ** は必要ありません。

>[!TIP]
>
>完全なスニペットについては、 [以下の「POM XMLスニペット](#xml-repository-structure-package) 」の節を参照してください。

## コンテナパッケージへのサブパッケージの埋め込み{#embeddeds}

コンテンツまたはコードパッケージは、特別な「サイドカー」フォルダに配置され、FileVault Mavenプラグインの設定を使用して、AEM作成者、AEM発行、またはその両方にインストールする対象となり `<embeddeds>` ます。 設定は使用しな `<subPackages>` いでください。

一般的な使用例を次に示します。

+ AEM作成者ユーザーとAEM発行ユーザーとで異なるACL/権限
+ AEM作成者でのみアクティビティをサポートするために使用される設定
+ バックオフィスシステムとの統合など、AEM作成者でのみ実行する必要のあるコード

![パッケージの埋め込み](assets/embeddeds.png)

AEM作成者、AEM発行またはその両方をターゲットにするには、パッケージを次の形式で、特別なフォルダーの場所にあるコンテ `all` ナパッケージに埋め込みます。

`/apps/<app-name>-packages/(content|application)/install(.author|.publish)?`

このフォルダー構造を分類する：

+ 第1レベルのフォルダーが必要 **です**`/apps`。
+ 第2レベルのフォルダーは、フォルダー名にポストフィッ `-packages` クスされたアプリケーションを表します。 多くの場合、すべてのサブパッケージが埋め込まれる2番目のフォルダは1つだけですが、2番目のフォルダはいくつでも作成でき、アプリケーションの論理構造を表すのに最適です。
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`
   >[!WARNING]
   >
   >慣例により、サブパッケージの埋め込みフォルダーの名前には、サフィックス `-packages` が付きます。これにより、サブパッケージ `/apps/<app-name>/...` の対象フォルダーにデプロイメントコードとコンテンツパッケージがデプロイされるのを&#x200B;**防ぎ**、インストールが破壊的かつ周期的におこなわれないようにします。

+ 3番目のフォルダは、
   「`application`」または「`content`」
   + このフォルダー `application` には、コードパッケージが格納されます
   + フォルダ `content` ーにはコンテンツパッケージが格納されます。このフォルダー名は、含まれ [るパッケージ](#package-types) のパッケージタイプに対応している必要があります。
+ 第 4 レベルのフォルダーにはサブパッケージが含まれ、次のいずれに該当する必要があります。
   + `install`：AEM オーサーと AEM 公開の&#x200B;**両方**&#x200B;でインストールする場合
   + `install.author`：AEM オーサーで&#x200B;**のみ**&#x200B;インストールする場合
   + `install.publish` をAEM publishNoteにの **みインストールします** 。ターゲットは、およびのみサ `install.author` ポートさ `install.publish` れています。 その他の実行モードはサポートされて&#x200B;**いません**。

例えば、AEM作成者を含む展開と、特定のパッケージを発行する展開は、次のようになります。

+ `all` コンテナパッケージは、単数の展開アーティファクトを作成するために、次のパッケージを埋め込みます
   + `ui.apps` 埋め込み：AEM `/apps/my-app-packages/application/install` 作成者とAEM発行の両方にコードをデプロイします。
   + `ui.apps.author` 埋め込み：AEMオー `/apps/my-app-packages/application/install.author` サーのみにコードをデプロイします
   + `ui.content` 埋め込み：AEM作 `/apps/my-app-packages/content/install` 成者とAEM発行の両方にコンテンツと設定をデプロイします。
   + `ui.content.publish` 埋め込み：AEM公 `/apps/my-app-packages/content/install.publish` 開のみにコンテンツと設定をデプロイします

>[!TIP]
>
>完全なスニペットについては、 [以下の「POM XMLスニペット](#xml-embeddeds) 」の節を参照してください。

### コンテナパッケージのフィルター定義 {#container-package-filter-definition}

コードとコンテンツのサブパッケージがコンテナパッケージに埋め込まれるので、埋め込みターゲットパスをコンテナプロジェクトのに追加して、埋め込みパッケージがコンテナパッケージの構築時に確実に含まれるようにする必要があります。 `filter.xml`

展開するサブパッ `<filter root="/apps/<my-app>-packages"/>` ケージを含む2番目のフォルダーのエントリを追加するだけです。

>[!TIP]
>
>完全なスニペットについては、 [以下の「POM XMLスニペット](#xml-container-package-filters) 」の節を参照してください。

## サードパーティパッケージの埋め込み {#embedding-3rd-party-packages}

すべてのパッケージは、 [AdobeのパブリックMavenアーティファクトリポジトリまたはアクセス可能なパブリックの](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) 、参照可能なサードパーティのMavenアーティファクトリポジトリを介して使用できる必要があります。

サードパーティパッケージが&#x200B;**アドビのパブリック Maven アーティファクトリポジトリ**&#x200B;にある場合は、それ以上の設定をおこなわなくても、Adobe Cloud Manager でアーティファクトを解決できます。

サードパーティパッケージが&#x200B;**パブリックサードパーティ Maven アーティファクトリポジトリ**&#x200B;にある場合は、このリポジトリをプロジェクトの `pom.xml` に登録し、[上記の方法](#embeddeds)に従って埋め込む必要があります。サードパーティのアプリケーション/コネクタでコードパッケージとコンテンツパッケージの両方が必要な場合は、それぞれをコンテナ（`all`）パッケージ内の正しい場所に埋め込む必要があります。

Maven依存関係の追加は、標準的なMavenの慣行に従い、サードパーティのアーティファクト（コードおよびコンテンツパッケージ）の埋め込みを前述 [していま](#embedding-3rd-party-packages)す。

>[!TIP]
>
>完全なスニペットについては、 [以下の「POM XMLスニペット](#xml-3rd-party-maven-repositories) 」の節を参照してください。

## fromパッケージ間のパッ `ui.apps` ケージの `ui.content` 依存 {#package-dependencies}

パッケージを適切にインストールするために、パッケージ間の依存関係を確立することをお勧めします。

一般的なルールは、可変コンテンツ(`ui.content`)を含むパッケージで、可変コンテンツ(`ui.apps`)がレンダリングされ、可変コンテンツの使用をサポートする不変コンテンツ()に依存する必要があります。

>[!TIP]
>
>完全なスニペットについては、 [以下の「POM XMLスニペット](#xml-package-dependencies) 」の節を参照してください。

コンテンツパッケージの依存関係の一般的なパターンは次のとおりです。

### シンプルな展開パッケージの依存関係 {#simple-deployment-package-dependencies}

簡易ケースは、可変コンテン `ui.content` ツパッケージを、不変コードパッケージに依存す `ui.apps` るように設定する。

+ `all` 依存関係がありません
   + `ui.apps` 依存関係がありません
   + `ui.content` ～に依存する `ui.apps`

### 複雑な展開パッケージの依存関係 {#complex-deploxment-package-dependencies}

複雑な導入は、単純なケースに対して拡張され、対応する可変コンテンツと不変コードパッケージの間の依存関係を設定します。 必要に応じて、不変コードパッケージ間の依存関係も確立できます。

+ `all` 依存関係がありません
   + `ui.apps.common` 依存関係がありません
   + `ui.apps.site-a` ～に依存する `ui.apps.common`
   + `ui.content.site-a` ～に依存する `ui.apps.site-a`
   + `ui.apps.site-b` ～に依存する `ui.apps.common`
   + `ui.content.site-b` ～に依存する `ui.apps.site-b`

## ローカル開発と導入 {#local-development-and-deployment}

この記事で概要を説明するプロジェクト構造と組織は、ローカル開発 **用AEMインスタンス** と完全に互換性があります。

## POM XMLスニペット {#pom-xml-snippets}

以下は、Mavenプロジェ `pom.xml` クトに追加して、上記のレコメンデーションに合わせることができるMaven設定スニペットです。

### パッケージタイプ {#xml-package-types}

サブパッケージとして展開されるコードおよびコンテンツパッケージでは、パッケージに含まれる内容に応じて、**アプリケーション**&#x200B;または&#x200B;**コンテンツ**&#x200B;のパッケージタイプを宣言する必要があります。

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

では、プラ `ui.content/pom.xml`グイン宣 `<packageType>content</packageType>` 言のビルド設定ディレクティブがパッ `filevault-package-maven-plugin` ケージの種類を宣言します。

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

コンテナ（`all`）プロジェクトを&#x200B;**除き**、パッケージを生成するすべてのプロジェクトで、`filevault-package-maven-plugin` プラグイン宣言の `<properties>` 設定に `<cloudManagerTarget>none</cloudManagerTarget>` を追加し、Adobe Cloud Manager によってデプロイされるのを&#x200B;**防ぎます**。コンテナ（`all`）パッケージは、Cloud Manager でデプロイした 1 つのパッケージで、必要なすべてのコードとコンテンツパッケージが埋め込まれます。

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

### リポジトリの初期化{#snippet-repo-init}

Repo Initスクリプトを含むRepo Initスクリプトは、プロパティを介して `RepositoryInitializer` OSGiファクトリ設定で定義さ `scripts` れます。 OSGi設定内で定義されるこれらのスクリプトは、通常のフォルダーセマンティクスを使用して実行モードで簡単にスコープでき `../config.<runmode>` ることに注意してください。

スクリプトは通常複数行の宣言なので、XMLベースの形式よりもファイル内で定義し `.config` やすいことに注意してくだ `sling:OsgiConfig` さい。

`/apps/my-app/config.author/org.apache.sling.jcr.repoinit.RepositoryInitializer-author.config`

```plain
scripts=["
    create service user my-data-reader-service

    set ACL on /var/my-data
        allow jcr:read for my-data-reader-service
    end

    create path (sling:Folder) /conf/my-app/settings
"]
```

OSGiプロ `scripts` パティには、 [Apache SlingのRepo Init言語で定義されたディレクティブが含まれます](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)。

### リポジトリ構造パッケージ {#xml-repository-structure-package}

およびコード `ui.apps/pom.xml` パッケ `pom.xml` ージ(`<packageType>application</packageType>`)を宣言するその他のすべてので、次のリポジトリ構造パッケージ設定をFileVault Mavenプラグインに追加します。 プロジェクト [用に独自のリポジトリ構造パッケージを作成できます](repository-structure-package.md)。

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
              <artifactId>ui.apps.structure</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
```

### コンテナパッケージへのサブパッケージの埋め込み {#xml-embeddeds}

で、次のデ `all/pom.xml`ィレクティブをプラ `<embeddeds>` グイン宣言に `filevault-package-maven-plugin` 追加します。 設定は使 **用しないでください** 。こ `<subPackages>` れはではなくにサブパッケージが含まれるので、この設定を使用 `/etc/packages` しないでくださ `/apps/my-app-packages/<application|content>/install(.author|.publish)?`い。

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

`all` プロジェクトの `filter.xml`（`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`）に、デプロイするサブパッケージを&#x200B;**含む**`-packages` フォルダーを含めます。

```xml
<filter root="/apps/my-app-packages"/>
```

埋め込みターゲ `/apps/*-packages` ットで複数を使用する場合は、すべてここで列挙する必要があります。

### サードパーティMavenリポジトリ {#xml-3rd-party-maven-repositories}

>[!WARNING]
> Mavenリポジトリをさらに追加すると、Mavenリポジトリの依存関係がチェックされるので、Mavenリポジトリのビルド時間が延長される場合があります。

reactorプロジェクトの中で、必要なサ `pom.xml`ードパーティのパブリックMavenリポジトリディレクティブを追加します。 完全な設定は、サ `<repository>` ードパーティのリポジトリプロバイダーから利用できる必要があります。

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

### fromパッケージ間のパッ `ui.apps` ケージの `ui.content` 依存 {#xml-package-dependencies}

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

Mavenビルド `all/pom.xml` の前に `maven-clean-plugin` ターゲットディレクトリをクリーンアップするプラグインを追加します。

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
+ [FileVault Content Package Mavenプラグイン](http://jackrabbit.apache.org/filevault-package-maven-plugin/)