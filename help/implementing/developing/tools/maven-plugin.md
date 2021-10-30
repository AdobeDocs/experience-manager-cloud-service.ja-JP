---
title: Adobe Content Package Maven Plugin
description: Content Package Maven Plugin を使用した AEM アプリケーションのデプロイについて説明します
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: ht
source-wordcount: '1847'
ht-degree: 100%

---

# Adobe Content Package Maven Plugin {#adobe-content-package-maven-plugin}

パッケージデプロイメントおよび管理タスクを Maven プロジェクトに組み込むには、Adobe Content Package Maven Plugin を使用します。

構築したパッケージは Adobe Content Package Maven Plugin で AEM にデプロイされます。その結果、通常は AEM パッケージマネージャーを使用して実行する以下のタスクを自動化できるようになります。

* ファイルシステム内のファイルから新しいパッケージを作成する。
* AEM にパッケージをインストールまたはアンインストールする。
* AEM で定義済みのパッケージをビルドする。
* AEM にインストールされているパッケージのリストを取得する。
* AEM からパッケージを削除する。

このドキュメントでは、Maven を使用してこれらのタスクを管理する方法について詳しく説明します。また一方、[AEM プロジェクトとそのパッケージの構造](#aem-project-structure)を理解することも重要です。

>[!NOTE]
>
>パッケージの作成は、[Apache Jackrabbit FileVault パッケージ Maven プラグイン](https://jackrabbit.apache.org/filevault-package-maven-plugin/)で管理されるようになりました。構築したパッケージは、ここで説明するように、Adobe Content Package Maven Plugin で AEM にデプロイされます。

## パッケージと AEM プロジェクト構造 {#aem-project-structure}

AEM as a Cloud Service は、最新の AEM プロジェクトアーキタイプによって実装された、パッケージ管理とプロジェクト構造に関する最新のベストプラクティスに従っています。

>[!TIP]
>
>詳しくは、AEM as a Cloud Service のドキュメントの [AEM プロジェクトの構造](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=ja)と、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)のドキュメントを参照してください。どちらも AEM 6.5 に完全に対応しています。

## Content Package Maven Plugin の入手 {#obtaining-the-content-package-maven-plugin}

このプラグインは [Maven Central リポジトリー](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)から入手できます。

## Content Package Maven Plugin のゴールとパラメーター

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

プラグインプレフィックスは `content-package` です。次の例に示すように、コマンドラインからゴールを実行するには、このプレフィックスを使用します。

```shell
mvn content-package:build
```

### パラメータープレフィックス {#parameter-prefix}

特に指定がない限り、プラグインのゴールおよびパラメーターでは、次の例に示すように `vault` プレフィックスを使用します。

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### プロキシ {#proxies}

AEM にプロキシを使用するゴールでは、Maven 設定で最初に見つかった有効なプロキシ設定を使用します。プロキシ設定が見つからない場合、プロキシは使用されません。[共通パラメーター](#common-parameters)の節の `useProxy` パラメーターを参照してください。

### 共通パラメーター {#common-parameters}

次の表に示すパラメーターは、すべてのゴールに共通です（**ゴール**&#x200B;列に記載されている場合を除く）。

| 名前 | 型 | 必須 | デフォルト値 | 説明 | ゴール |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | いいえ | `false` | 値 `true` を指定すると、エラーの発生時にビルドが失敗します。値 `false` を指定すると、ビルドの際にエラーが無視されます。 | `package` を除くすべてのゴール |
| `name` | `String` | `build`：はい、`install`：いいえ、`rm`：はい | `build`：デフォルト値なし、`install`：Maven プロジェクトの `artifactId` プロパティの値 | 処理をおこなうパッケージの名前 | `ls` を除くすべてのゴール |
| `password` | `String` | はい | `admin` | AEM での認証に使用するパスワード | `package` を除くすべてのゴール |
| `serverId` | `String` | いいえ | 認証用のユーザー名とパスワードの取得元のサーバー ID | `package` を除くすべてのゴール |
| `targetURL` | `String` | はい | `http://localhost:4502/crx/packmgr/service.jsp` | AEM パッケージマネージャーの HTTP サービス API の URL | `package` を除くすべてのゴール |
| `timeout` | `int` | いいえ | `5` | パッケージマネージャーサービスとの通信の接続タイムアウト（秒） | `package` を除くすべてのゴール |
| `useProxy` | `boolean` | いいえ | `true` | 値 `true` を指定すると、Maven は最初に見つかったアクティブなプロキシ設定を使用してパッケージマネージャーへのリクエストをプロキシします。 | `package` を除くすべてのゴール |
| `userId` | `String` | はい | `admin` | AEM で認証するユーザー名 | `package` を除くすべてのゴール |
| `verbose` | `boolean` | いいえ | `false` | 詳細ログを有効または無効にします | `package` を除くすべてのゴール |

### build {#build}

AEM インスタンスで既に定義されているコンテンツパッケージをビルドします。

>[!NOTE]
>
>Maven プロジェクト内でこのゴールを実行する必要はありません。

#### パラメーター {#parameters}

build ゴールのすべてのパラメーターについては、[共通パラメーター](#common-parameters)を参照してください。

### install {#install}

リポジトリー内のパッケージをインストールします。このゴールの実行に Maven プロジェクトは不要です。このゴールは Maven のビルドライフサイクルの `install` フェーズにバインドされます。

#### パラメーター {#parameters-1}

以下のパラメーターに加えて、[共通パラメーター](#common-parameters)の説明も参照してください。

| 名前 | 型 | 必須 | デフォルト値 | 説明 |
|---|---|---|---|---|---|
| `artifact` | `String` | いいえ | Maven プロジェクトの `artifactId` プロパティの値 | `groupId:artifactId:version[:packaging]` 形式の文字列 |
| `artifactId` | `String` | いいえ | なし | インストールするアーティファクトの ID |
| `groupId` | `String` | いいえ | なし | インストールするアーティファクトの `groupId` |
| `install` | `boolean` | いいえ | `true` | アップロード時にパッケージを自動的に解凍するかどうかを指定します |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | いいえ | `localRepository` システム変数の値 | ローカルの Maven リポジトリー（常にシステムプロパティが使用されるので、プラグイン設定を使用してこのパラメーターを設定することはできません） |
| `packageFile` | `java.io.File` | いいえ | Maven プロジェクト用に定義されているプライマリアーティファクト | インストールするパッケージファイルの名前 |
| `packaging` | `String` | いいえ | `zip` | インストールするアーティファクトのパッケージ化のタイプ |
| `pomRemoteRepositories` | `java.util.List` | はい | Maven プロジェクト用に定義されている `remoteArtifactRepositories` プロパティの値 | この値は、プラグイン設定を使用して設定することはできず、プロジェクトで指定する必要があります。 |
| `project` | `org.apache.maven.project.MavenProject` | はい | プラグインが設定されるプロジェクト | Maven プロジェクト（プラグイン設定が格納されているので、これは暗黙的なプロジェクトです） |
| `repositoryId`（POM）、`repoID`（コマンドライン） | `String` | いいえ | `temp` | アーティファクトの取得元リポジトリーの ID |
| `repositoryUrl`（POM）、`repoURL`（コマンドライン） | `String` | いいえ | なし | アーティファクトの取得元リポジトリーの URL |
| version | String | いいえ | なし | インストールするアーティファクトのバージョン |

### ls {#ls}

パッケージマネージャーにデプロイされているパッケージを一覧表示します。

#### パラメーター {#parameters-2}

ls ゴールのすべてのパラメーターについては、[共通パラメーター](#common-parameters)を参照してください。

### rm {#rm}

パッケージマネージャーからパッケージを削除します。

#### パラメーター {#parameters-3}

rm ゴールのすべてのパラメーターについては、[共通パラメーター](#common-parameters)を参照してください。

### uninstall {#uninstall}

パッケージをアンインストールします。パッケージは、アンインストールされた状態でサーバーに残ります。

#### パラメーター {#parameters-4}

uninstall ゴールのすべてのパラメーターについては、[共通パラメーター](#common-parameters)を参照してください。

### package {#package}

コンテンツパッケージを作成します。package ゴールのデフォルト設定には、コンパイルしたファイルを保存するディレクトリの内容が含まれます。package ゴールを実行するには、compile build フェーズを完了しておく必要があります。package ゴールは Maven のビルドライフサイクルの package フェーズにバインドされます。

#### パラメーター {#parameters-5}

以下のパラメーターに加えて、[共通パラメーター](#common-parameters)の `name` パラメーターの説明も参照してください。

| 名前 | 型 | 必須 | デフォルト値 | 説明 |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | いいえ | なし | 使用するアーカイブ設定 |
| `builtContentDirectory` | `java.io.File` | はい | Maven ビルドの出力ディレクトリの値 | パッケージに含める内容を格納するディレクトリ |
| `dependencies` | `java.util.List` | いいえ | なし |  |
| `embeddedTarget` | `java.lang.String` | いいえ | なし |  |
| `embeddeds` | `java.util.List` | いいえ | なし |  |
| `failOnMissingEmbed` | `boolean` | はい | `false` | 値 `true` を指定すると、埋め込みアーティファクトがプロジェクトの依存関係に見つからない場合にビルドが失敗します。値 `false` を指定すると、ビルドの際にこのエラーが無視されます。 |
| `filterSource` | `java.io.File` | いいえ | なし | パラメーターワークスペースフィルターのソースを指定するファイルを定義します。設定で指定され、embeddeds または subpackages を使用して挿入されるフィルターはファイル内容と結合されます。 |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | いいえ | なし | パッケージ内容を定義するフィルター要素を格納します。実行すると、`filter.xml` ファイルにフィルターが追加されます。以下の[フィルターの使用](#using-filters)の節を参照してください。 |
| `finalName` | `java.lang.String` | はい | Maven プロジェクト（build フェーズ）で定義される `finalName` | 生成されるパッケージの ZIP ファイルの名前（ファイル拡張子 `.zip` を除く） |
| `group` | `java.lang.String` | はい | Maven プロジェクトで定義される `groupID` | 生成されるコンテンツパッケージの `groupId`（コンテンツパッケージのターゲットインストールパスに含まれます） |
| `outputDirectory` | `java.io.File` | はい | Maven プロジェクトで定義されるビルドディレクトリ | コンテンツパッケージが保存されるローカルディレクトリ |
| `prefix` | `java.lang.String` | いいえ | なし |  |
| `project` | `org.apache.maven.project.MavenProject` | はい | なし | Maven プロジェクト |
| `properties` | `java.util.Map` | いいえ | なし | これらのパラメーターは、`properties.xml` ファイルに設定できる追加のプロパティを定義します。これらのプロパティで次の定義済みプロパティを上書きすることはできません。`group`（`group` パラメーターを使用して設定）、`name`（`name` パラメーターを使用して設定）、`version`（`version` パラメーターを使用して設定）、`description`（プロジェクトの説明から設定）、`groupId`（Maven プロジェクト記述子の `groupId`）、`artifactId`（Maven プロジェクト記述子の `artifactId`）、`dependencies`（`dependencies` パラメーターを使用して設定）、`createdBy`（システムプロパティ `user.name` の値）、`created`（現在のシステム時刻）、`requiresRoot`（`requiresRoot` パラメーターを使用して設定）、`packagePath`（グループ名とパッケージ名から自動的に生成） |
| `requiresRoot` | `boolean` | はい | false | パッケージにルートが必要かどうかを定義します。これは `properties.xml` ファイルの `requiresRoot` プロパティになります。 |
| `subPackages` | `java.util.List` | いいえ | なし |  |
| `version` | `java.lang.String` | はい | Maven プロジェクトで定義されるバージョン | コンテンツパッケージのバージョン |
| `workDirectory` | `java.io.File` | はい | Maven プロジェクト（build フェーズ）で定義されるディレクトリ | パッケージに含める内容を格納するディレクトリ |

#### フィルターの使用 {#using-filters}

パッケージ内容を定義するには、フィルター要素を使用します。フィルターはパッケージの `META-INF/vault/filter.xml` ファイルの `workspaceFilter` 要素に追加されます。

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

`mode` 要素は、パッケージが読み込まれる際にリポジトリー内の内容がどのような影響を受けるかを定義します。使用できる値は次のとおりです。

* **merge：**&#x200B;まだリポジトリーに含まれていないパッケージ内容が追加されます。パッケージとリポジトリーの両方に含まれている内容は変更されません。リポジトリーの内容が削除されることはありません。
* **replace：**&#x200B;リポジトリーに含まれていないパッケージ内容がリポジトリーに追加されます。リポジトリー内の内容が、パッケージ内の一致する内容に置き換えられます。パッケージ内に存在しない内容はリポジトリーから削除されます。
* **update：**&#x200B;リポジトリーに含まれていないパッケージ内容がリポジトリーに追加されます。リポジトリー内の内容が、パッケージ内の一致する内容に置き換えられます。既存の内容はリポジトリーから削除されます。

フィルターに `mode` 要素が含まれていない場合は、デフォルト値 `replace` が使用されます。

### help {#help}

#### パラメーター {#parameters-6}

| 名前 | 型 | 必須 | デフォルト値 | 説明 |
|---|---|---|---|---|
| `detail` | `boolean` | いいえ | `false` | 各ゴールに設定可能なプロパティをすべて表示するかどうかを指定します |
| `goal` | `String` | いいえ | なし | ヘルプを表示するゴールの名前を指定します。値を指定しない場合は、すべてのゴールのヘルプが表示されます。 |
| `indentSize` | `int` | いいえ | `2` | 各レベルのインデントに使用するスペースの数（指定する場合は正の数にします） |
| `lineLength` | `int` | いいえ | `80` | 表示行の最大長（指定する場合は正の数にします） |

## パッケージへのサムネール画像またはプロパティファイルの追加 {#including-a-thumbnail-image-or-properties-file-in-the-package}

パッケージのプロパティをカスタマイズするには、デフォルトのパッケージ設定ファイルを置き換えます。例えば、パッケージを識別するためのサムネール画像をパッケージマネージャーとパッケージ共有に追加します。

ソースファイルはファイルシステム内のどこにあっても構いません。POM ファイルでは、ソースファイルを `target/vault-work/META-INF` にコピーするように、パッケージに追加するビルドリソースを定義します。

次の POM コードでは、プロジェクトソースの `META-INF` フォルダー内のファイルをパッケージに追加します。

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

次の POM コードでは、1 つのサムネール画像だけをパッケージに追加します。サムネール画像の名前を `thumbnail.png` と指定して、パッケージの `META-INF/vault/definition` フォルダーに配置してください。この例では、ソースファイルはプロジェクトの `/src/main/content/META-INF/vault/definition` フォルダーにあります。

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

## AEM プロジェクトアーキタイプを使用した AEM プロジェクトの生成 {#using-archetypes}

最新の AEM プロジェクトアーキタイプでは、オンプレミス実装でも AMS 実装でも、ベストプラクティスに従ったパッケージ構造を実装しているので、すべての AEM プロジェクトにこのプロジェクトアーキタイプを使用することをお勧めします。

>[!TIP]
>
>詳しくは、AEM as a Cloud Service のドキュメントの [AEM プロジェクトの構造](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=ja)と、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)のドキュメントを参照してください。どちらも AEM 6.5 に完全に対応しています。
