---
title: Adobe Content Package Maven Plugin
description: Content Package Maven Plugin を使用した AEM アプリケーションのデプロイについて説明します
exl-id: d631d6df-7507-4752-862b-9094af9759a0
feature: Developing
role: Admin, Architect, Developer
source-git-commit: d757c94475f257ee4b05092671ae5e6384b8342e
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 97%

---

# Adobe Content Package Maven Plugin {#adobe-content-package-maven-plugin}

パッケージデプロイメントおよび管理タスクを Maven プロジェクトに組み込むには、Adobe Content Package Maven プラグインを使用します。

構築したパッケージは Adobe Content Package Maven プラグインによって AEM にデプロイされ、通常 AEM [Package Manager：](/help/implementing/developing/tools/package-manager.md) を使って実行するタスクの自動化を可能にします。

* ファイルシステム内のファイルから新しいパッケージを作成する。
* AEM にパッケージをインストールまたはアンインストールする。
* AEM で定義済みのパッケージをビルドする。
* AEM にインストールされているパッケージのリストを取得する。
* AEM からパッケージを削除する。

このドキュメントでは、Maven を使用してこれらのタスクを管理する方法について詳しく説明します。また一方、[AEM プロジェクトとそのパッケージの構造](#aem-project-structure)を理解することも重要です。

>[!NOTE]
>
>これらのプラグインの最新バージョンを常に使用してください。

>[!NOTE]
>
>パッケージの&#x200B;**作成**&#x200B;は、[Apache Jackrabbit FileVault Package Maven プラグイン](https://jackrabbit.apache.org/filevault-package-maven-plugin/)で管理されるようになりました。
>
>この記事では、Adobeコンテンツパッケージ Maven プラグインで実行される、構築済みパッケージのAEMへの **デプロイ** について説明します。

## パッケージと AEM プロジェクト構造 {#aem-project-structure}

AEM as a Cloud Service は、最新の AEM プロジェクトアーキタイプによって実装された、パッケージ管理とプロジェクト構造に関する最新のベストプラクティスに従っています。

>[!TIP]
>
>AEM as a Cloud Service のドキュメントの [AEM プロジェクトの構造](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=ja)の記事および [AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)のドキュメントを参照してください。どちらも AEM 6.5 に完全に対応しています。

## Content Package Maven Plugin の入手 {#obtaining-the-content-package-maven-plugin}

このプラグインは [Maven Central リポジトリー](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)から入手できます。

## Content Package Maven Plugin のゴールとパラメーター

Content Package Maven Plugin を使用するには、POM ファイルのビルド要素内に次のプラグイン要素を追加します。

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>1.0.4</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Maven がプラグインをダウンロードできるようにするには、このページの [Content Package Maven Plugin の取得](#obtaining-the-content-package-maven-plugin)の節で提供されているプロファイルを使用します。

## Content Package Maven Plugin の目標 {#goals-of-the-content-package-maven-plugin}

Content Package プラグインが提供する目標と目標のパラメーターについて詳しくは、次の節で説明します。共通パラメーターの節で説明したパラメーターは、ほとんどの目標に使用できます。1 つの目標に適用されるパラメーターについて詳しくは、その目標の節で説明します。

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
| `useProxy` | `boolean` | いいえ | `true` | `true` の値は、Maven は最初に見つかったアクティブなプロキシ設定を使用してパッケージマネージャーへのリクエストをプロキシします。 | `package` を除くすべてのゴール |
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

以下のパラメーターに加えて、 [共通パラメーター](#common-parameters) の説明も参照してください。

| 名前 | 型 | 必須 | デフォルト値 | 説明 |
|---|---|---|---|---|
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
| version | 文字列 | いいえ | なし | インストールするアーティファクトのバージョン |

### ls {#ls}

[パッケージマネージャー](/help/implementing/developing/tools/package-manager.md)にデプロイされているパッケージを一覧表示します。

#### パラメーター {#parameters-2}

ls ゴールのすべてのパラメーターについては、[共通パラメーター](#common-parameters)を参照してください。

### rm {#rm}

[パッケージマネージャー](/help/implementing/developing/tools/package-manager.md)からパッケージを削除します。

#### パラメーター {#parameters-3}

rm ゴールのすべてのパラメーターについては、[共通パラメーター](#common-parameters)を参照してください。

### uninstall {#uninstall}

パッケージをアンインストールします。パッケージは、アンインストールされた状態でサーバーに残ります。

#### パラメーター {#parameters-4}

uninstall ゴールのすべてのパラメーターについては、[共通パラメーター](#common-parameters)を参照してください。


### help {#help}

#### パラメーター {#parameters-6}

| 名前 | 型 | 必須 | デフォルト値 | 説明 |
|---|---|---|---|---|
| `detail` | `boolean` | いいえ | `false` | 各ゴールに設定可能なプロパティをすべて表示するかどうかを指定します |
| `goal` | `String` | いいえ | なし | ヘルプを表示するゴールの名前を指定します。値を指定しない場合は、すべてのゴールのヘルプが表示されます。 |
| `indentSize` | `int` | いいえ | `2` | 各レベルのインデントに使用するスペースの数（指定する場合は正の数にします） |
| `lineLength` | `int` | いいえ | `80` | 表示行の最大長（指定する場合は正の数にします） |

## パッケージへのサムネール画像またはプロパティファイルの追加 {#including-a-thumbnail-image-or-properties-file-in-the-package}

デフォルトのパッケージ設定ファイルを置き換えて、パッケージのプロパティをカスタマイズします。例えば、[パッケージマネージャー](/help/implementing/developing/tools/package-manager.md)でパッケージを区別するためのサムネール画像を含めます。

ソースファイルはファイルシステム内のどこにあっても構いません。POM ファイルでは、ソースファイルを `target/vault-work/META-INF` にコピーするように、パッケージに追加するビルドリソースを定義します。

次の POM コードでは、プロジェクトソースの `META-INF` フォルダー内のファイルをパッケージに追加します。

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail and so on) -->
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
>AEM as a Cloud Service のドキュメントの [AEM プロジェクトの構造](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=ja)の記事および [AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)のドキュメントを参照してください。どちらも AEM 6.5 に完全に対応しています。
