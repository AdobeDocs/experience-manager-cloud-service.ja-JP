---
title: 'リポジトリ構造パッケージの作成   '
description: Adobe Experience ManagerをクラウドサービスMavenプロジェクトとして使用するには、リポジトリ構造サブパッケージ定義が必要です。この定義の唯一の目的は、プロジェクトのコードサブパッケージがデプロイされるJCRリポジトリルートを定義することです。
translation-type: tm+mt
source-git-commit: 46d556fdf28267a08e5021f613fbbea75872ef21

---


# リポジトリ構造パッケージの作成

クラウドサービスとしてのAdobe Experience Manager用のMavenプロジェクトには、リポジトリ構造のサブパッケージ定義が必要です。このサブパッケージ定義の唯一の目的は、プロジェクトのコードサブパッケージのデプロイ先のJCRリポジトリルートを定義することです。 これにより、Experience Managerでのクラウドサービスとしてのパッケージのインストールが、JCRリソースの依存関係に基づいて自動的に順序付けられます。 依存関係が見つからないと、親構造の前にサブ構造がインストールされ、予期せず削除され、配置が中断する場合があります。

コードパッケージがコードパッケージで覆われていない場所にデプロイされる場合 **** 、これらの依存関係を確立するには、リポジトリ構造パッケージに上位のリソース（JCRルートに近いJCRリソース）を列挙する必要があります。

![リポジトリ構造パッケージ](./assets/repository-structure-packages.png)

リポジトリ構造パッケージは、パッケージバリデーターが、標準的なルートとして「潜在的な競合から安全」な領域を判断するために使用する、期待される `/apps` 共通の状態を定義します。

リポジトリ構造パッケージに含める最も一般的なパスは次のとおりです。

+ `/apps` システムが提供するノード
+ `/apps/cq/...`、、 `/apps/dam/...`、お `/apps/wcm/...`よびの共通 `/apps/sling/...` のオーバーレイを提供しま `/libs`す。
+ `/apps/settings` 共有コンテキスト対応設定のルートパス

このサブパッケージはコンテ **ンツを持たず** 、フィルタールートを定義するだけで構成さ `pom.xml` れていることに注意してください。

## リポジトリ構造パッケージの作成

Mavenプロジェクト用のリポジトリ構造パッケージを作成するには、新しい空のMavenサブプロジェクトを作成し、次を使用して、親Mavenプロジェクトに準拠するよ `pom.xml`うにプロジェクトメタデータを更新します。

コードパッケ `<filters>` ージのデプロイ先となるすべてのJCRリポジトリパスを含めるようにを更新します。

この新しいMavenサブプロジェクトは、必ず親プロジェクトリストに追加してく `<modules>` ださい。

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
    <artifactId>my-app.repository-structure</artifactId>
    <packaging>content-package</packaging>
    <name>My App - Adobe Experience Manager Repository Structure Package</name>

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
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!-- Common overlay roots -->
                        <filter><root>/apps/sling</root></filter>
                        <filter><root>/apps/cq</root></filter>
                        <filter><root>/apps/dam</root></filter>
                        <filter><root>/apps/wcm</root></filter>

                        <!-- Immutable context-aware configurations -->
                        <filter><root>/apps/settings</root></filter>

                    </filters>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## リポジトリ構造パッケージの参照

リポジトリ構造パッケージを使用するには、FileVaultコンテンツパッケージMavenプラグイン設定を使用して、すべてのコードパッケージ(Mavenに展開するサブパッケージ `/apps`)を介してMavenプロジェクトを参照 `<repositoryStructurePackage>` します。

およびそ `ui.apps/pom.xml`の他のコードパッケー `pom.xml`ジで、プロジェクトのリポジトリ構造パッケージ(#repository-structure-package)設定への参照をFileVaultパッケージMavenプラグインに追加します。

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
              <artifactId>my-app.repository-structure</artifactId>
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
        <artifactId>my-app.repository-structure</artifactId>
        <version>${project.version}</version>
        <type>zip</type>
    </dependency>
    ...
</dependencies>
```

## マルチコードパッケージの使用例

一般的でなく複雑な使用例は、JCRリポジトリの同じ領域にインストールする複数のコードパッケージのデプロイメントをサポートしています。

次に例を示します。

+ コードパッケージAは、 `/apps/a`
+ コードパッケージBは、 `/apps/a/b`

コードパッケージAのコードパッケージBからパッケージレベルの依存関係が確立されない場合、コードパッケージBは最初にに展開し、次にコードパッケージBに展開してから、に展開して、以前にインストールさ `/apps/a`れたコードを削除しま `/apps/a``/apps/a/b`す。

この場合、次のようになります。

+ コードパッケージAは、プロジェク `<repositoryStructurePackage>` トのリポジトリ構造パッケージ(フィルターを含む必要があ `/apps`る)でを定義します。
+ コードパッケージBはコードパッケージAで共 `<repositoryStructurePackage>` 有されるスペースに展開されるので、コードパッケージBはコードパッケージAでを定義する必要があります。

## エラーとデバッグ

リポジトリ構造パッケージが正しく設定されていない場合、Mavenビルド時に次のエラーが報告されます。

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

これは、無効化コードパッケージに、フィルターリストに含まれ `<repositoryStructurePackage>` る無効化コ `/apps/some/path` ードがないことを示します。

## その他のリソース

+ [FileVaultコンテンツパッケージMavenプラグイン](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
