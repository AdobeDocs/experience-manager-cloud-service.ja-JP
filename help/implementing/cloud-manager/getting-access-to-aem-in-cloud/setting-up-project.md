---
title: プロジェクトのセットアップ
description: Maven を使用して AEM プロジェクトをビルドする方法と、独自のプロジェクトを作成する際に確認する必要がある標準について説明します。
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: e7e12d78ace75ade7a2f3168191c410eecadf9d0
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 66%

---

# プロジェクトのセットアップ {#project-setup}

Maven を使用して AEM プロジェクトをビルドする方法と、独自のプロジェクトを作成する際に確認する必要がある標準について説明します。

## プロジェクトの設定の詳細 {#project-setup-details}

Cloud Manager で正常にビルドおよびデプロイするには、AEM プロジェクトは次のガイドラインに従う必要があります。

* プロジェクトは [Apache Maven](https://maven.apache.org) を使用してビルドする必要があります。
* Git リポジトリーのルートには `pom.xml` ファイルが必要です。 この`pom.xml` ファイルは、必要に応じて多数のサブモジュール （その他のサブモジュールなど）を参照します。
* 追加の Maven アーティファクトリポジトリへの参照を `pom.xml` ファイルに追加できます。 設定時には、[パスワードで保護されたアーティファクトリポジトリー](#password-protected-maven-repositories)へのアクセスがサポートされます。 ただし、ネットワークで保護されたアーティファクトリポジトリーへのアクセスはサポートされていません。
* Cloud Managerは、`target`という名前のディレクトリに含まれているコンテンツパッケージ `.zip` ファイルをスキャンして、デプロイ可能なコンテンツパッケージを検出します。 任意の数のサブモジュールがコンテンツパッケージを生成します。
* Cloud Managerは、`conf`および`conf.d`という名前のディレクトリを持つ`.zip` ファイル（`target`という名前のディレクトリにも含まれる）をスキャンして、デプロイ可能なDispatcher アーティファクトを検出します。
* 複数のコンテンツパッケージがある場合、パッケージデプロイメントの順序は保証されません。 特定の順序が必要な場合は、コンテンツパッケージの依存関係を使用して順序を定義できます。
* デプロイメント中にパッケージが[ スキップ ](#skipping-content-packages)されます。

## Cloud Manager での Maven プロファイルのアクティベート {#activating-maven-profiles-in-cloud-manager}

一部の限られたケースでは、デベロッパーワークステーションで実行する場合とは異なり、Cloud Manager内で実行する場合はビルドプロセスが少し異なります。 このような場合、[Maven プロファイル ](https://maven.apache.org/guides/introduction/introduction-to-profiles.html)は、Cloud Managerを含むさまざまな環境でのビルドの違いを定義します。

Cloud Manager ビルド環境内での Maven プロファイルのアクティベーションは、`CM_BUILD` [環境変数](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)を検索することで行います。 同様に、Cloud Manager ビルド環境の外部でのみ使用することを意図したプロファイルは、この変数がないかどうかを調べることによって設定されます。

例えば、ビルドがCloud Manager内で実行されている場合にのみシンプルなメッセージを出力する場合は、次の操作を行います。

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

また、ビルドがCloud Manager以外で実行されている場合にのみシンプルなメッセージを出力する場合は、次の操作を行います。

```xml
        <profile>
            <id>notCMBuild</id>
            <activation>
                  <property>
                        <name>[!NOTE]nv.CM_BUILD</name>
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

## Cloud Manager 内でのパスワードで保護された Maven リポジトリの使用 {#password-protected-maven-repositories}

>[!NOTE]
>
>Cloud Managerは、このコードを[ コード品質ルール ](/help/implementing/cloud-manager/custom-code-quality-rules.md)で評価しないため、慎重にパスワードで保護されたMaven リポジトリからアーティファクトをデプロイします。 このメソッドは、特定の状況でのみ使用し、AEMに関連しないコードにのみ適用する必要があります。 Adobeでは、Java ソースとプロジェクト全体のソースコードの両方をバイナリと共に含めることをお勧めします。 これにより、デプロイメントプロセス全体の透明性と維持率が向上します。

**パスワードで保護された Maven リポジトリを Cloud Manager 内で使用するには：**

1. パスワード（およびオプションでユーザー名）をシークレットの[パイプライン変数](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)として指定します。
1. 次に、Git リポジトリーの `.cloudmanager/maven/settings.xml` という名前のファイル内でそのシークレットを参照します。このファイルは、[Maven Settings File](https://maven.apache.org/settings.html) スキーマに従います。

Cloud Manager のビルドプロセスが開始したとき、以下が行われます。

* このファイル内の `<servers>` 要素が、Cloud Manager から提供されるデフォルトの `settings.xml` ファイルに結合されます。
   * `adobe` と `cloud-manager` で始まるサーバー ID は予約済みと見なされます。 カスタムサーバーでは使用しないでください。
   * Cloud Manager は、特定の接頭辞またはデフォルトの ID `central` に一致するサーバー ID のみをミラーリングします。その他のサーバー ID はすべてミラーリングから除外されます。
* このファイルを配置した状態で、`pom.xml` ファイル内の`<repository>`および/または`<pluginRepository>`要素の中からサーバーIDを参照します。
* これらの`<repository>`要素と`<pluginRepository>`要素は[Cloud Manager固有のプロファイル ](#activating-maven-profiles-in-cloud-manager)に含まれていますが、厳密には含める必要はありません。

例えば、リポジトリが`https://repository.myco.com/maven2`で、Cloud Managerが使用するユーザー名が`cloudmanager`、パスワードが`secretword`であるとします。 次の手順を実行します。

1. パスワードをパイプライン内のシークレットとして設定します。

   ```text
   $ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`
   ```

1. 次の `.cloudmanager/maven/settings.xml` ファイルからこの秘密鍵を参照します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <settings xmlns="https://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="https://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
       <servers>
           <server>
               <id>myco-repository</id>
               <username>cloudmanager</username>
              <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
           </server>
       </servers>
   </settings>
   ```

1. 最後に、`pom.xml` ファイル内のサーバーIDを参照します。

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

バイナリと一緒にJava ソースをMaven リポジトリにデプロイすることをお勧めします。

これを行うには、プロジェクト内の maven-source-plugin を設定します。

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

バイナリと共にプロジェクトソース全体をMaven リポジトリにデプロイすることをお勧めします。 これにより、正確なアーティファクトを再構築できます。

プロジェクトでmaven-assembly-pluginを次のように設定します。

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

Cloud Managerでは、ビルドは任意の数のコンテンツパッケージを生成します。 様々な理由から、コンテンツパッケージを作成することが望ましいが、デプロイしないことが望ましい。 例えば、テスト目的にのみコンテンツパッケージをビルドする場合や、ビルドプロセスの別の手順でコンテンツパッケージを再パッケージ化する場合が挙げられます。 つまり、別のパッケージのサブパッケージです。

これらのシナリオに対応するため、Cloud Manager はビルドコンテンツパッケージのプロパティで、`cloudManagerTarget` という名前のプロパティを探します。 このプロパティが `none` に設定されている場合、パッケージはスキップされ、デプロイされません。

このプロパティを設定する仕組みは、ビルドがコンテンツパッケージを生成する方法によって異なります。 例えば、`filevault-maven-plugin`では、次のようにプラグインを設定します。

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

`content-package-maven-plugin` にも同様の設定があります。

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

## アーティファクトの再利用の構築 {#build-artifact-reuse}

多くの場合、同じコードが複数の AEM 環境にデプロイされます。 Cloud Manager は、複数のフルスタックパイプライン実行で同じ Git コミットが使用されていることを検出した場合、コードベースの再ビルドを可能な限り避けます。

実行が開始されると、ブランチパイプラインの現在の HEAD コミットが抽出されます。 コミットハッシュは、UI に表示され、API を使用して確認できます。 ビルドステップが正常に完了すると、結果のアーティファクトはそのコミットハッシュに基づいて保存され、後続のパイプライン実行で再利用されます。

同じプログラム内にあるパッケージは、パイプラインをまたいで再利用されます。 再利用可能なパッケージを探す際に、AEM はブランチを無視し、ブランチをまたいでアーティファクトを再利用します。

再利用が行われると、ビルドステップとコード品質ステップが元の実行の結果に事実上置き換えられます。 ビルドステップのログファイルには、アーティファクトと、最初にアーティファクトのビルドに使用された実行情報が一覧表示されます。

そのようなログ出力の例を次に示します。

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

コード品質ステップのログには、類似した情報が含まれます。

### 例 {#example-reuse}

#### 例 1 {#example-1}

プログラムに 2 つの開発パイプラインがあるとします。

* ブランチ `foo` のパイプライン 1
* ブランチ `bar` のパイプライン 2

両方のブランチが同じコミット ID 上にあります。

1. 最初にパイプライン 1 を実行すると、パッケージは通常どおりビルドされます。
1. その後、パイプライン 2 を実行すると、パイプライン 1 で作成されたパッケージが再利用されます。

#### 例 2 {#example-2}

プログラムには次の 2 つのブランチがあるとします。

* ブランチ `foo`
* ブランチ `bar`

両方のブランチのコミット ID が同じです。

1. 開発パイプラインは、`foo` のビルドと実行を行います。
1. その後、実稼動パイプラインが `bar` をビルドおよび実行します。

この場合、同じコミットハッシュが特定されたので、`foo` のアーティファクトは実稼動パイプラインで再利用されます。

### オプトアウト {#opting-out}

必要に応じて、パイプライン変数 `CM_DISABLE_BUILD_REUSE` を `true` に設定して、特定のパイプラインに対して再利用動作を無効にできます。 この変数が設定されている場合、システムではコミットハッシュが抽出され、結果として生成されたアーティファクトは後で使用するために保存されますが、以前に保存されたアーティファクトの再利用はスキップされます。 この動作を理解するには、次のシナリオについて考えます。

1. 新しいパイプラインが作成されます。
1. そのパイプラインが実行され（実行番号 1）、現在の HEAD コミットが `becdddb` となっています。 実行が完了すると、結果として生成されたアーティファクトが保存されます。
1. この `CM_DISABLE_BUILD_REUSE` 変数が設定されます。
1. コードを変更せずにパイプラインが再実行されます。 `becdddb` に関連付けられたアーティファクトが保存されていますが、`CM_DISABLE_BUILD_REUSE` 変数が設定されているので再利用されません。
1. コードが変更され、パイプラインが実行されます。 HEAD コミットは `f6ac5e6` になります。 実行が完了すると、結果として生成されたアーティファクトが保存されます。
1. `CM_DISABLE_BUILD_REUSE` 変数が削除されます。
1. コードを変更せずに、パイプラインが再実行されます。 `f6ac5e6` に関連付けられたアーティファクトが保存されているため、それらのアーティファクトは再利用されます。

### 注意事項 {#caveats}

* コミット ハッシュが同じかどうかに関係なく、ビルド アーティファクトは異なるプログラム間で再利用されません。
* ブランチやパイプラインが異なる場合でも、ビルドアーティファクトは同じプログラム内で再利用されます。
* [Maven バージョン処理](/help/implementing/cloud-manager/managing-code/project-version-handling.md)は、実稼動パイプライン内のプロジェクトバージョンのみを置き換えます。
開発用デプロイメントと実稼動用パイプラインの両方に同じコミットが使用され、開発用デプロイメントが最初に実行された場合、バージョンはステージングおよび実稼動用に変更されずにデプロイされます。ただし、この場合はタグが作成されます。
* 保存されたアーティファクトが正常に取得されなかった場合、ビルドステップは、アーティファクトが保存されていない場合と同じように実行されます。
* 以前に作成したビルドアーティファクトを Cloud Manager で再利用する場合、`CM_DISABLE_BUILD_REUSE` 以外のパイプライン変数は考慮されません。
