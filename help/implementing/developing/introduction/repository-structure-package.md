---
title: 'AEMプロジェクトリポジトリ構造パッケージ  '
description: Adobe Experience ManagerをクラウドサービスMavenプロジェクトとして使用するには、リポジトリ構造サブパッケージ定義が必要です。この定義の唯一の目的は、プロジェクトのコードサブパッケージがデプロイされるJCRリポジトリルートを定義することです。
translation-type: tm+mt
source-git-commit: fb398147c5a2635f58250b8de886159b4ace2943

---


# AEMプロジェクトリポジトリ構造パッケージ

クラウドサービスとしてのAdobe Experience Manager用のMavenプロジェクトには、リポジトリ構造のサブパッケージ定義が必要です。このサブパッケージ定義の唯一の目的は、プロジェクトのコードサブパッケージのデプロイ先のJCRリポジトリルートを定義することです。 これにより、Experience Managerでのクラウドサービスとしてのパッケージのインストールが、JCRリソースの依存関係によって自動的に順序付けられます。 依存関係が見つからないと、親構造の前にサブ構造がインストールされ、予期せず削除され、配置が中断される場合があります。

コードパッケージで&#x200B;**カバーされていない**&#x200B;場所にコードパッケージをデプロイする場合、これらの依存関係を確立するには、リポジトリ構造パッケージで上位のリソース（JCR ルートに近い JCR リソース）を列挙する必要があります。

![リポジトリ構造パッケージ](./assets/repository-structure-packages.png)

リポジトリ構造パッケージは、パッケージバリデーターが、標準的なルートとして「 `/apps` 競合の可能性がない」領域を判断する際に使用する、期待される共通の状態を定義します。

リポジトリ構造パッケージに含める最も一般的なパスは、次のとおりです。

+ `/apps` システムが提供するノード
+ `/apps/cq/...`、、 `/apps/dam/...`、お `/apps/wcm/...`よびの共通の `/apps/sling/...` オーバーレイを提供しま `/libs`す。
+ `/apps/settings` 共有コンテキスト対応設定のルートパス

このサブパッケージにはコンテ **ンツは含まれず** 、フィルターのルートを定義するだけのもので `pom.xml` 構成されています。

## リポジトリ構造パッケージの作成

Mavenプロジェクト用のリポジトリ構造パッケージを作成するには、新しい空のMavenサブプロジェクトを作成し、次の手順で、親Mavenプロジェクトに適合するよ `pom.xml`うにプロジェクトのメタデータを更新します。

コードパッケ `<filters>` ージのデプロイ先のすべてのJCRリポジトリパスを含めるように、を更新します。

この新しいMavenサブプロジェクトを親プロジェクトリストに追加してく `<modules>` ださい。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- ====================================================================== -->
    <!-- P A R E N T  P R O J E C T  D E S C R I P T I O N                      -->
    <!-- ====================================================================== -->
    <parent>
        <groupId>com.my-company</groupId>
        <artifactId>my-app</artifactId>
        <version>x.x.x</version>
        <relativePath>../pom.xml</relativePath>
    </parent>

    <!-- ====================================================================== -->
    <!-- P R O J E C T  D E S C R I P T I O N                                   -->
    <!-- ====================================================================== -->
    <artifactId>ui.apps.structure</artifactId>
    <packaging>content-package</packaging>
    <name>UI Apps Structure - Repository Structure Package for /apps</name>

    <description>
        Empty package that defines the structure of the Adobe Experience Manager repository the code packages in this project deploy into.
        Any roots in the code packages of this project should have their parent enumerated in the filters list below.
    </description>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.jackrabbit</groupId>
                <artifactId>filevault-package-maven-plugin</artifactId>
                <extensions>true</extensions>
                <properties>
                    <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!--
                        Examples of complex roots


                        Overlays of /libs typically require defining the overlayed structure, at each level here.

                        For example, adding a new section to the main AEM Tools navigation, necessitates the following rules:

                        <filter><root>/apps/cq</root></filter>
                        <filter><root>/apps/cq/core</root></filter>
                        <filter><root>/apps/cq/core/content</root></filter>
                        <filter><root>/apps/cq/core/content/nav/</root></filter>
                        <filter><root>/apps/cq/core/content/nav/tools</root></filter>


                        Any /apps level Context-aware configurations need to enumerated here. 
                        
                        For example, providing email templates under `/apps/settings/notification-templates/com.day.cq.replication` necessitates the following rules:

                        <filter><root>/apps/settings</root></filter>
                        <filter><root>/apps/settings/notification-templates</root></filter>
                        <filter><root>/apps/settings/notification-templates/com.day.cq.replication</root></filter>
                        -->

                    </filters>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## リポジトリ構造パッケージの参照

リポジトリ構造パッケージを使用するには、FileVaultコンテンツパッケージMavenプラグイン設定を介して、すべてのコードパッケージ(デプロイ先のサブパッケージ `/apps`)Mavenプロジェクトを介して参照 `<repositoryStructurePackage>` します。

およびそ `ui.apps/pom.xml`の他のコード `pom.xml`パッケージで、プロジェクトのリポジトリ構造パッケージ(#repository-structure-package)設定への参照をFileVaultパッケージMavenプラグインに追加します。

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
</build>
<dependencies>
    <!-- Add the dependency for the repository structure package so it resolves -->
    <dependency>
        <groupId>${project.groupId}</groupId>
        <artifactId>ui.apps.structure</artifactId>
        <version>${project.version}</version>
        <type>zip</type>
    </dependency>
    ...
</dependencies>
```

## マルチコードパッケージの使用例

一般的でなく複雑な使用例は、JCRリポジトリの同じ領域にインストールする複数のコードパッケージのデプロイをサポートしています。

次に例を示します。

+ コードパッケージAは、 `/apps/a`
+ コードパッケージBは、 `/apps/a/b`

コードパッケージAのコードパッケージBからパッケージレベルの依存関係が確立されない場合、コードパッケージBは最初ににに展開し、次にコードパッケージBに展開してから、に展開して、以前にインストールさ `/apps/a`れたコードを削除しま `/apps/a``/apps/a/b`す。

この場合、次のようになります。

+ コードパッケージAは、プロジェク `<repositoryStructurePackage>` トのリポジトリ構造パッケージ(フィルタを含む必要があ `/apps`る)でを定義します。
+ コードパッケージBはコードパッケージA `<repositoryStructurePackage>` で共有されるスペースに展開されるので、コードパッケージBはコードパッケージAを定義する必要があります。

## エラーとデバッグ

リポジトリ構造パッケージが正しく設定されていない場合、Mavenの構築時に次のエラーが報告されます。

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

これは、改行コードパッケージに、フィルターリストに含まれ `<repositoryStructurePackage>` る改行コードが含ま `/apps/some/path` れていないことを示します。

## その他のリソース

+ [FileVault Content Package Mavenプラグイン](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
