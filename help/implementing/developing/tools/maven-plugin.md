---
title: AdobeコンテンツパッケージMavenプラグイン
description: Content Package Mavenプラグインを使用したAEMアプリケーションのデプロイ
translation-type: tm+mt
source-git-commit: 2cdbbe9b8f6608cbdd299889be515d421e3d9ad3
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 33%

---


# AdobeコンテンツパッケージMavenプラグイン {#adobe-content-package-maven-plugin}

AdobeコンテンツパッケージMavenプラグインを使用して、パッケージの展開と管理タスクをMavenプロジェクトに統合します。

構築されたパッケージのAEMへの展開は、AdobeコンテンツパッケージMavenプラグインによって実行され、AEM Package Managerを使用して通常実行されるタスクの自動化を可能にします。

* ファイルシステム内のファイルから新しいパッケージを作成します。
* AEMでパッケージをインストールおよびアンインストールします。
* AEMで既に定義されているパッケージを構築します。
* AEMにインストールされているパッケージのリストを取得します。
* AEMからパッケージを削除します。

このドキュメントでは、Mavenを使用してこれらのタスクを管理する方法について詳しく説明します。 ただし、AEMプロジェクトとそのパッケージの構造化 [方法を理解することも重要です。](#aem-project-structure)

>[!NOTE]
>
>パッケージ作成は、 [Apache Jackrabbit FileVault Package Mavenプラグインが所有するようになりました](https://jackrabbit.apache.org/filevault-package-maven-plugin/)。 構築されたパッケージのAEMへの展開は、ここで説明するAdobeコンテンツパッケージMavenプラグインによって実行されます。

## パッケージとAEMプロジェクト構造 {#aem-project-structure}

AEM 6.5は、オンプレミスとAMSの両方の実装の最新のAEM Project Archetypeによって実装された、パッケージ管理とプロジェクト構造の最新のベストプラクティスに従います。

>[!TIP]
>
>詳しくは、AEMの [AEM Project Structure](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.translate.html) (プロジェクト構造 [)の記事をCloud Serviceドキュメントとして参照し、「](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html) AEM Project Archetype」ドキュメントを参照してください。 どちらもAEM 6.5では完全にサポートされています。

## Content Package Maven Plugin の入手 {#obtaining-the-content-package-maven-plugin}

このプラグインは、 [Maven Central Repositoryから入手できます。](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## コンテンツパッケージMavenプラグインの目標とパラメーター

Content Package Maven Plugin を使用するには、POM ファイルのビルド要素内に次のプラグイン要素を追加します。

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Maven でプラグインをダウンロードできるようにするには、このページの [Content Package Maven Plugin の取得](#obtaining-the-content-package-maven-plugin)で提供されるプロファイルを使用します。

## Content Package Maven Plugin のゴール {#goals-of-the-content-package-maven-plugin}

Content Package Plugin に用意されているゴールおよびゴールパラメーターについては、以降の節で説明します。共通パラメーターの節に示すパラメーターはほとんどのゴールに使用できます。1 つのゴールに適用するパラメーターについては、そのゴールの節を参照してください。

### プラグインプレフィックス {#plugin-prefix}

The plugin prefix is `content-package`. Use this prefix to execute a goal from the command line, as in the following example:

```shell
mvn content-package:build
```

### パラメータープレフィックス {#parameter-prefix}

Unless otherwise noted, the plugin goals and parameters use the `vault` prefix, as in the following example:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### プロキシ {#proxies}

AEMにプロキシを使用する目標は、Maven設定の最初の有効なプロキシ設定を使用します。 プロキシ設定が見つからない場合、プロキシは使用されません。See the `useProxy` parameter in the [Common Parameters](#common-parameters) section.

### 共通パラメーター {#common-parameters}

The parameters in the following table are common to all goals except when noted in the **Goals** column.

| 名前 | 種類 | 必須 | デフォルト値 | 説明 | ゴール |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | 不可 | `false` | 値 `true` を指定すると、エラーの発生時にビルドが失敗します。値 `false` を指定すると、ビルドの際にエラーが無視されます。 | All goals except `package` |
| `name` | `String` | `build`:はい、 `install`:いいえ、 `rm`:はい | `build`:No default, `install`:Mavenプロジェクトの `artifactId` プロパティの値 | 操作するパッケージの名前 | All goals except `ls` |
| `password` | `String` | 可 | `admin` | AEMでの認証に使用するパスワード | All goals except `package` |
| `serverId` | `String` | 不可 | 認証用のユーザー名とパスワードを取得するサーバーID | All goals except `package` |
| `targetURL` | `String` | 可 | `http://localhost:4502/crx/packmgr/service.jsp` | AEMパッケージマネージャーのHTTPサービスAPIのURL | All goals except `package` |
| `timeout` | `int` | 不可 | `5` | パッケージマネージャーサービスとの通信の接続タイムアウト（秒） | All goals except `package` |
| `useProxy` | `boolean` | 不可 | `true` | A value of `true` causes Maven to use the first active proxy configuration found in order to proxy requests to the Package Manager. | All goals except `package` |
| `userId` | `String` | 可 | `admin` | AEMで認証するユーザー名 | All goals except `package` |
| `verbose` | `boolean` | 不可 | `false` | 詳細ログを有効または無効にします | All goals except `package` |

### build {#build}

AEMインスタンスで既に定義されているコンテンツパッケージをビルドします。

>[!NOTE]
>
>Maven プロジェクト内でこのゴールを実行する必要はありません。

#### パラメーター {#parameters}

All parameters for the build goal are described in the [Common Parameters](#common-parameters) section.

### install {#install}

リポジトリにパッケージをインストールします。 このゴールの実行に Maven プロジェクトは不要です。The goal is bound to the `install` phase of the Maven build lifecycle.

#### パラメーター {#parameters-1}

In addition to the following parameters, see the descriptions in the [Common Parameters](#common-parameters) section.

| 名前 | 種類 | 必須 | デフォルト値 | 説明 |
|---|---|---|---|---|---|
| `artifact` | `String` | 不可 | The value of the `artifactId` property of the Maven project | A string of the form `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | 不可 | なし | インストールするアーティファクトの ID |
| `groupId` | `String` | 不可 | なし | The `groupId` of the artifact to install |
| `install` | `boolean` | 不可 | `true` | パッケージがアップロードされたときに、パッケージを自動的に解凍するかどうかを指定します |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | 不可 | The value of the `localRepository` system variable | systemプロパティとしてプラグイン設定を使用して設定できないローカルのMavenリポジトリは常に使用されます |
| `packageFile` | `java.io.File` | 不可 | Mavenプロジェクトに定義された主要アーティファクト | インストールするパッケージファイルの名前 |
| `packaging` | `String` | 不可 | `zip` | インストールするアーティファクトのパッケージ化のタイプ |
| `pomRemoteRepositories` | `java.util.List` | 可 | The value of the `remoteArtifactRepositories` property that is defined for the Maven project | この値はプラグイン設定を使用して設定することはできません。この値はプロジェクトで指定する必要があります。 |
| `project` | `org.apache.maven.project.MavenProject` | 可 | プラグインが設定されているプロジェクト | プロジェクトにプラグイン設定が含まれているので暗黙的なMavenプロジェクト |
| `repositoryId` (POM)、 `repoID` （コマンドライン） | `String` | 不可 | `temp` | アーティファクトの取得元のリポジトリのID |
| `repositoryUrl` (POM)、 `repoURL` （コマンドライン） | `String` | 不可 | なし | アーティファクトの取得元であるリポジトリのURL |
| version | String | 不可 | なし | インストールするアーティファクトのバージョン |

### ls {#ls}

パッケージマネージャーにデプロイされるパッケージを一覧表示します。

#### パラメーター {#parameters-2}

All parameters of the ls goal are described in the [Common Parameters](#common-parameters) section.

### rm {#rm}

パッケージマネージャーからパッケージを削除します。

#### パラメーター {#parameters-3}

All parameters of the rm goal are described in the [Common Parameters](#common-parameters) section.

### uninstall {#uninstall}

パッケージをアンインストールします。このパッケージは、アンインストールされた状態でサーバーに残ります。

#### パラメーター {#parameters-4}

All parameters of the uninstall goal are described in the [Common Parameters](#common-parameters) section.

### package {#package}

コンテンツパッケージを作成します。package ゴールのデフォルト設定には、コンパイルしたファイルを保存するディレクトリのコンテンツが含まれます。package ゴールを実行するには、compile build フェーズを完了しておく必要があります。package ゴールは Maven のビルドライフサイクルの package フェーズにバインドされます。

#### パラメーター {#parameters-5}

In addition to the following parameters, see the description of the `name` parameter in the [Common Parameters](#common-parameters) section.

| 名前 | 種類 | 必須 | デフォルト値 | 説明 |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | 不可 | なし | 使用するアーカイブの設定 |
| `builtContentDirectory` | `java.io.File` | 可 | Mavenビルドの出力ディレクトリの値 | パッケージに含めるコンテンツを含むディレクトリ |
| `dependencies` | `java.util.List` | 不可 | なし |  |
| `embeddedTarget` | `java.lang.String` | 不可 | なし |  |
| `embeddeds` | `java.util.List` | 不可 | なし |  |
| `failOnMissingEmbed` | `boolean` | 可 | `false` | A value of `true` causes the build to fail when an embedded artifact is not found in the project dependencies. A value of `false` causes the build to ignore such errors. |
| `filterSource` | `java.io.File` | 不可 | なし | このパラメーターは、ワークスペースフィルターのソースを指定するファイルを定義します。 設定で指定され、embeddeds または subpackages を使用して挿入されるフィルターはファイルコンテンツと結合されます。 |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | 不可 | なし | このパラメーターには、パッケージコンテンツを定義するフィルター要素が含まれます。 When executed, the filters are included in the `filter.xml` file. See the [Using Filters](#using-filters) section below. |
| `finalName` | `java.lang.String` | 可 | The `finalName` defined in the Maven project (build phase) | The name of the generated package ZIP file, without the `.zip` file extension |
| `group` | `java.lang.String` | 可 | The `groupID` defined in the Maven project | The `groupId` of the generated content package which is part of the target installation path for the content package |
| `outputDirectory` | `java.io.File` | 可 | Mavenプロジェクトで定義されたビルドディレクトリ | コンテンツパッケージが保存されるローカルディレクトリ |
| `prefix` | `java.lang.String` | 不可 | なし |  |
| `project` | `org.apache.maven.project.MavenProject` | 可 | なし | Mavenプロジェクト |
| `properties` | `java.util.Map` | 不可 | なし | これらのパラメーターは、 `properties.xml` ファイルで設定できる追加のプロパティを定義します。 これらのプロパティは、次の定義済みプロパティを上書きできません。 `group` 使用パラメータ `group` ー設定時 `name` 、使用パラメーター設定時、使用パラメーター設定時、使用 `name` パラメーター設定時、使用パラメーター設定時、使用パラメーター設定時、使用プロジェクト記述子 `version``version``description``groupId``groupId``artifactId``artifactId``dependencies``dependencies``createdBy``user.name``created``requiresRoot``requiresRoot``packagePath` 時、使用時。（グループとパッケージ名から） |
| `requiresRoot` | `boolean` | 可 | false | パッケージにルートが必要かどうかを定義します。これが、 `requiresRoot` ファイルの `properties.xml` プロパティになります。 |
| `subPackages` | `java.util.List` | 不可 | なし |  |
| `version` | `java.lang.String` | 可 | Maven プロジェクトで定義されるバージョン | コンテンツパッケージのバージョン |
| `workDirectory` | `java.io.File` | 可 | Mavenプロジェクトで定義されたディレクトリ（ビルドフェーズ） | パッケージに含めるコンテンツを含むディレクトリ |

#### フィルターの使用 {#using-filters}

パッケージのコンテンツを定義するには、フィルター要素を使用します。フィルターがパッケージのフ `workspaceFilter``META-INF/vault/filter.xml` ァイル内の要素に追加されます。

次に示すフィルターの例は、使用する XML 構造を示しています。

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

##### インポートモード {#import-mode}

`mode` 要素は、パッケージが読み込まれる際にリポジトリ内のコンテンツがどのような影響を受けるかを定義します。使用できる値は次のとおりです。

* **merge：**&#x200B;まだリポジトリに含まれていないパッケージのコンテンツが追加されます。パッケージ内およびリポジトリ内のコンテンツは変更されません。コンテンツがリポジトリから削除されることはありません。
* **置換：** リポジトリにないパッケージ内のコンテンツはリポジトリに追加されます。リポジトリ内のコンテンツは、パッケージ内の一致するコンテンツに置き換えられます。コンテンツがパッケージに存在しない場合、コンテンツはリポジトリから削除されます。
* **update：**&#x200B;リポジトリに含まれていないパッケージのコンテンツがリポジトリに追加されます。リポジトリ内のコンテンツは、パッケージ内の一致するコンテンツに置き換えられます。既存のコンテンツはリポジトリから削除されます。

フィルターに `mode` 要素が含まれていない場合は、デフォルト値 `replace` が使用されます。

### help {#help}

#### パラメーター {#parameters-6}

| 名前 | 種類 | 必須 | デフォルト値 | 説明 |
|---|---|---|---|---|
| `detail` | `boolean` | 不可 | `false` | 各目標に対して設定可能なすべてのプロパティを表示するかどうかを指定します |
| `goal` | `String` | 不可 | なし | このパラメーターは、ヘルプを表示する目標の名前を定義します。 値を指定しない場合は、すべてのゴールのヘルプが表示されます。 |
| `indentSize` | `int` | 不可 | `2` | 各レベルのインデントに使用するスペースの数です（正の数を指定する必要があります） |
| `lineLength` | `int` | 不可 | `80` | 表示線の最大長（正の値を指定する必要があります） |

## パッケージへのサムネール画像またはプロパティファイルの追加 {#including-a-thumbnail-image-or-properties-file-in-the-package}

パッケージのプロパティをカスタマイズするには、デフォルトのパッケージ設定ファイルを置き換えます。例えば、パッケージを識別するためのサムネール画像をパッケージマネージャーとパッケージ共有に追加します。

ソースファイルは、ファイルシステムのどこにでも配置できます。 POMファイルで、パッケージに含めるソースファイルをにコピーするビルドリソース `target/vault-work/META-INF` を定義します。

The following POM code adds the files in the `META-INF` folder of the project source to the package:

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

次の POM コードでは、1 つのサムネール画像だけをパッケージに追加します。サムネール画像には名前が付けられ `thumbnail.png`ており、パッケージの `META-INF/vault/definition` フォルダーに存在する必要があります。 In this example, the source file is located in the `/src/main/content/META-INF/vault/definition` folder of the project:

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## AEMプロジェクトのアーキタイプを使用したAEMプロジェクトの生成 {#using-archetypes}

最新のAEMプロジェクトアーキタイプは、オンプレミスとAMSの両方の実装にベストプラクティスパッケージ構造を実装し、すべてのAEMプロジェクトに推奨します。

>[!TIP]
>
>詳しくは、AEMの [AEM Project Structure](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.translate.html) (プロジェクト構造 [)の記事をCloud Serviceドキュメントとして参照し、「](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html) AEM Project Archetype」ドキュメントを参照してください。 どちらもAEM 6.5では完全にサポートされています。
