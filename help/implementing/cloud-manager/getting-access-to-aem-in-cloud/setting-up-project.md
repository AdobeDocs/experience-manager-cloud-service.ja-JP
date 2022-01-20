---
title: プロジェクト設定の詳細
description: プロジェクト設定の詳細 - Cloud Services
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
source-git-commit: 4219c8ce30a0f1cd44bbf8e8de46d6be28a1ddf3
workflow-type: tm+mt
source-wordcount: '1254'
ht-degree: 67%

---

# プロジェクトの設定 {#project-setup-details}

## プロジェクト設定の詳細を変更する {#modifying-project-setup-details}

Cloud Manager で正常にビルドおよびデプロイされるために、既存の AEM プロジェクトはいくつかの基本ルールに従う必要があります。

* プロジェクトは Apache Maven を使用してビルドする必要があります。
* Git リポジトリーのルートには *pom.xml* ファイルが必要です。この *pom.xml* ファイルでは、必要な数のサブモジュールを参照できます（それらのサブモジュールでさらに他のサブモジュールなどを参照している場合もあります）。

* 追加の Maven アーティファクトリポジトリーへの参照を *pom.xml* ファイルに追加できます。設定時には、[パスワードで保護されたアーティファクトリポジトリー](#password-protected-maven-repositories)へのアクセスがサポートされます。ただし、ネットワークで保護されたアーティファクトリポジトリーへのアクセスはサポートされていません。
* デプロイ可能なコンテンツパッケージは、*target* という名前のディレクトリに含まれているコンテンツパッケージ *zip* ファイルをスキャンすることで検出されます。任意の数のサブモジュールでコンテンツパッケージを作成することもできます。

* デプロイ可能な Dispatcher アーティファクトは、*conf* および *conf.d* というディレクトリを持つ *zip* ファイル（これも *target* という名前のディレクトリに含まれる）をスキャンすることで検出されます

* 複数のコンテンツパッケージがある場合、パッケージデプロイメントの順序は保証されません。特定の順序が必要な場合は、コンテンツパッケージの依存関係を使用して順序を定義できます。パッケージはデプロイメントから[スキップ](#skipping-content-packages)できます。


## Cloud Manager での Maven プロファイルのアクティブ化 {#activating-maven-profiles-in-cloud-manager}

ごく一部のケースでは、開発用ワークステーションで実行する場合とは異なり、Cloud Manager 内で実行する場合にはビルドプロセスを少し変える必要が出ることもあります。この場合は、[Maven プロファイル](https://maven.apache.org/guides/introduction/introduction-to-profiles.html)を使用して、Cloud Manager を含む環境ごとのビルドの違いを定義できます。

Cloud Manager ビルド環境内での Maven プロファイルのアクティベーションは、前述の CM_BUILD という名前の環境変数があるかどうかを調べて行う必要があります。逆に、Cloud Manager ビルド環境以外でのみ使用するためのプロファイルは、この変数がないかどうかを調べることでアクティブ化する必要があります。

例えば、Cloud Manager 内でビルドが実行されたときにのみ簡単なメッセージを出力する場合は、次のようにします。

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running inside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

>[!NOTE]
>
>開発用ワークステーションでこのプロファイルをテストするには、（`-PcmBuild` を付けた）コマンドラインまたは統合開発環境（IDE）でプロファイルを有効にします。

Cloud Manager 以外でビルドが実行されたときにのみ簡単なメッセージを出力する場合は、次のようにします。

```xml
        <profile>
            <id>notCMBuild</id>
            <activation>
                  <property>
                        <name>!env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running outside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

## パスワードで保護された Maven リポジトリーのサポート {#password-protected-maven-repositories}

>[!NOTE]
>パスワードで保護された Maven リポジトリーのアーティファクトは、慎重に使用する必要があります。これは、現在、このメカニズムを通じてデプロイされるコードは Cloud Manager の品質ゲートを通じて実行されないためです。したがって、まれなケースで、AEM に結び付けられていないコードに対してのみ使用する必要があります。Java ソース、およびプロジェクトのソースコード全体もバイナリとともにデプロイすることをお勧めします。

パスワードで保護された Maven リポジトリーを Cloud Manager から使用するには、パスワード（および任意でユーザー名）を秘密のパイプライン変数として指定し、Git リポジトリーの `.cloudmanager/maven/settings.xml` という名前のファイル内でその秘密を参照します。このファイルは、[Maven Settings File](https://maven.apache.org/settings.html) スキーマに従います。Cloud Manager のビルドプロセス開始時に、このファイル内の `<servers>` 要素が、Cloud Manager が提供するデフォルトの `settings.xml` ファイルに結合されます。`adobe` と `cloud-manager` で始まるサーバー ID は予約済みと見なされるため、カスタムサーバーでは使用しないでください。サーバー ID がこれらのプレフィックスのいずれかに&#x200B;**一致しない**&#x200B;場合、デフォルトの ID `central` は Cloud Manager でミラーリングされません。このファイルを配置すると、サーバー ID は `<repository>` 内や `pom.xml` ファイル内の `<pluginRepository>` 要素から参照されます。一般に、これらの `<repository>` や `<pluginRepository>` 要素は、[Cloud Manager 固有のプロファイル](#activating-maven-profiles-in-cloud-manager)に含まれますが、厳密に必要とは限りません。

例えば、リポジトリーが https://repository.myco.com/maven2 にあり、Cloud Manager が使用するユーザー名が `cloudmanager` で、パスワードが `secretword` だとします。

まず、パスワードをパイプライン上の秘密として設定します。

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

次に、`.cloudmanager/maven/settings.xml` ファイルからこれを参照します。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>
        <server>
            <id>myco-repository</id>
            <username>cloudmanager</username>
            <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
        </server>
    </servers>
</settings>
```

最後に、`pom.xml` ファイル内のサーバー ID を参照します。

```xml
<profiles>
    <profile>
        <id>cmBuild</id>
        <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
        </activation>
        <repositories>
             <repository>
                 <id>myco-repository</id>
                 <name>MyCo Releases</name>
                 <url>https://repository.myco.com/maven2</url>
                 <snapshots>
                     <enabled>false</enabled>
                 </snapshots>
                 <releases>
                     <enabled>true</enabled>
                 </releases>
             </repository>
         </repositories>
         <pluginRepositories>
             <pluginRepository>
                 <id>myco-repository</id>
                 <name>MyCo Releases</name>
                 <url>https://repository.myco.com/maven2</url>
                 <snapshots>
                     <enabled>false</enabled>
                 </snapshots>
                 <releases>
                     <enabled>true</enabled>
                 </releases>
             </pluginRepository>
         </pluginRepositories>
    </profile>
</profiles>
```

### ソースのデプロイ {#deploying-sources}

バイナリと共に Java ソースを Maven リポジトリーにデプロイすることをお勧めします。

プロジェクトで maven-source-plugin を設定します。

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-source-plugin</artifactId>
            <executions>
                <execution>
                    <id>attach-sources</id>
                    <goals>
                        <goal>jar-no-fork</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
```

### プロジェクトソースのデプロイ {#deploying-project-sources}

バイナリと一緒にプロジェクトソース全体を Maven リポジトリーにデプロイすることをお勧めします。これにより、正確なアーティファクトを再構築できます。

プロジェクトで maven-assembly-plugin を設定します。

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <executions>
                <execution>
                    <id>project-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                    <configuration>
                        <descriptorRefs>
                            <descriptorRef>project</descriptorRef>
                        </descriptorRefs>
                    </configuration>
                </execution>
            </executions>
        </plugin>
```

## コンテンツパッケージのスキップ {#skipping-content-packages}

Cloud Manager では、ビルドは、任意の数のコンテンツパッケージを作成できます。
様々な理由により、コンテンツパッケージを作成してもデプロイしないことが望ましい場合があります。例えば、テストのみに使用するコンテンツパッケージを作成する場合や、ビルドプロセスの別のステップで（つまり、別のパッケージのサブパッケージとして）再パッケージ化される場合に便利です。

これらのシナリオに対応するために、Cloud Manager は、ビルドコンテンツパッケージのプロパティで、***cloudManagerTarget*** という名前のプロパティを探します。このプロパティが none に設定されている場合、パッケージはスキップされ、デプロイされません。このプロパティを設定する仕組みは、ビルドがコンテンツパッケージを作成する方法によって異なります。例えば、以下のように filevault-maven-plugin でプラグインを設定する場合、

```xml
        <plugin>
            <groupId>org.apache.jackrabbit</groupId>
            <artifactId>filevault-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

content-package-maven-plugin では、同じようになります。

```xml
        <plugin>
            <groupId>com.day.jcr.vault</groupId>
            <artifactId>content-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

## アーティファクトの再利用を構築 {#build-artifact-reuse}

多くの場合、同じコードが複数のAEM環境にデプロイされます。 可能な限り、Cloud Manager は、複数のフルスタックパイプライン実行で同じ Git コミットが使用されていることを検出した場合に、コードベースを再構築しないようにします。

実行が開始されると、ブランチパイプラインの現在のHEADコミットが抽出されます。 コミットハッシュは、UI と API で表示できます。 ビルド手順が正常に完了すると、結果のアーティファクトはそのコミットハッシュに基づいて保存され、後続のパイプライン実行で再利用できます。 再利用が発生すると、ビルドとコードの品質ステップが、元の実行の結果に効果的に置き換えられます。 ビルドステップのログファイルには、アーティファクトと、最初にアーティファクトのビルドに使用された実行情報が一覧表示されます。

ログ出力の例を次に示します。

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

コード品質ステップのログには、類似した情報が含まれます。

### オプトアウト {#opting-out}

必要に応じて、パイプライン変数を設定して、特定のパイプラインの再利用動作を無効にできます `CM_DISABLE_BUILD_REUSE` から `true`. この変数を設定した場合、コミットハッシュは抽出され、結果のアーティファクトは後で使用するために保存されますが、以前に保存されたアーティファクトは再利用されません。 この動作を理解するには、次のシナリオについて考えてみましょう。

1. 新しいパイプラインが作成されます。
1. パイプラインが実行され ( 実行#1)、現在のHEADコミットが `becdddb`. 実行が成功し、結果のアーティファクトが保存されます。
1. この `CM_DISABLE_BUILD_REUSE` 変数が設定されている。
1. コードを変更せずにパイプラインが再実行されます。 に関連付けられたアーティファクトが保存されていますが、 `becdddb`の場合、 `CM_DISABLE_BUILD_REUSE` 変数を使用します。
1. コードが変更され、パイプラインが実行されます。 HEADコミットは `f6ac5e6`. 実行が成功し、結果のアーティファクトが保存されます。
1. この `CM_DISABLE_BUILD_REUSE` 変数が削除されます。
1. コードを変更せずに、パイプラインが再実行されます。 次に関連付けられた保管済みアーティファクトがあるので、 `f6ac5e6`の場合、それらのアーティファクトは再利用されます。

### 注意事項 {#caveats}

* [Maven バージョンの処理](/help/implementing/cloud-manager/managing-code/project-version-handling.md) 実稼働パイプラインでのみ、プロジェクトのバージョンを置き換えます。 したがって、開発デプロイ実行と実稼動パイプライン実行の両方で同じコミットが使用され、開発デプロイパイプラインが最初に実行される場合、バージョンは変更されることなくステージング環境と実稼動環境にデプロイされます。 ただし、この場合、タグは引き続き作成されます。
* 保存されたアーティファクトの取得が成功しなかった場合、ビルドステップは、アーティファクトが保存されていない場合と同様に実行されます。
* 以外のパイプライン変数 `CM_DISABLE_BUILD_REUSE` 以前に作成したビルドアーティファクトを Cloud Manager で再利用する場合、は考慮されません。
