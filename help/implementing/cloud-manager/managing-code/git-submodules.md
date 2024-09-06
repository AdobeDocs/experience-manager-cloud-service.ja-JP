---
title: Git サブモジュールのサポート
description: Git サブモジュールを使用して、ビルド時に Git リポジトリ間で複数のブランチのコンテンツを結合する方法について説明します。
exl-id: fa5b0f49-4b87-4f39-ad50-7e62094d85f4
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 97%

---

# Adobe リポジトリに対する Git サブモジュールのサポート {#git-submodule-support}

Git サブモジュールを使用すると、ビルド時に Git リポジトリ間で複数のブランチのコンテンツを結合できます。

Cloud Manager のビルドプロセスを実行すると、パイプライン用に設定されたリポジトリのクローンを作成し、設定されたブランチをチェックアウトした後に、ブランチのルートディレクトリに `.gitmodules` ファイルが含まれている場合は、コマンドが実行されます。

次のコマンドは、各サブモジュールを適切なディレクトリにチェックアウトします。

```
$ git submodule update --init
```

この手法は、Git サブモジュールの使用に慣れていて、外部マージプロセスの管理を望まない組織にとっては、[複数のソース Git リポジトリの操作](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md)に関するドキュメントで説明しているソリューションの代わりになる可能性があります。

例えば、3 つのリポジトリがあり、それぞれに `main` という名前のブランチが 1 つあるとします。プライマリリポジトリ（パイプラインで設定されたもの）の `main` ブランチには、他の 2 つのリポジトリに含まれるプロジェクトを宣言している `pom.xml` ファイルがあります。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
   
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
   
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
   
</project>
```

この状況で、他の 2 つのリポジトリにサブモジュールを追加します。

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

その結果、`.gitmodules` ファイルの内容は次のようになります。

```text
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

Git サブモジュールの詳細については、[Git リファレンスマニュアル ](https://git-scm.com/book/ja/v2/Git-Tools-Submodules) を参照してください。

### 制限事項とレコメンデーション {#limitations-recommendations}

アドビが管理するリポジトリで Git サブモジュールを使用する場合は、次の制限事項に注意してください。

* Git の URL は、前述の節で説明した構文に正確に一致している必要があります。
* ブランチのルートにあるサブモジュールのみがサポートされます。
* セキュリティ上の理由から、Git の URL に資格情報を埋め込まないでください。
* 特に必要がない限り、シャローサブモジュールを使用することを強くお勧めします。
   * それには、サブモジュールごとに `git config -f .gitmodules submodule.<submodule path>.shallow true` を実行します。
* Git サブモジュール参照は、特定の Git コミットに保存されます。その結果、サブモジュールリポジトリに対して変更を加えた場合は、参照されるコミットを更新する必要があります。
   * `git submodule update --remote` を使用する例は、次のとおりです。

## プライベートリポジトリに対する Git サブモジュールのサポート {#private-repositories}

[プライベートリポジトリ](private-repositories.md)を使用する際の Git サブモジュールのサポートは、Adobe リポジトリを使用する際とほとんど同じです。

ただし、`pom.xml` ファイルを設定して `git submodule` コマンドを実行した後、Cloud Manager でサブモジュールの設定を検出するために、集積リポジトリのルートディレクトリに `.gitmodules` ファイルを追加する必要があります。

![.gitmodules ファイル](assets/gitmodules.png)

![集積](assets/aggregator.png)

### 制限事項とレコメンデーション {#limitations-recommendations-private-repos}

プライベートリポジトリで Git サブモジュールを使用する場合は、次の制限事項に注意してください。

* サブモジュールの Git URL は、HTTPS 形式または SSH 形式のいずれかですが、github.com リポジトリにリンクする必要があります
   * Adobe リポジトリサブモジュールを GitHub 集積リポジトリに追加したり、その逆を行ったりすることはできません。
* GitHub サブモジュールは、Adobe GitHub アプリからアクセスできる必要があります。
* また、[アドビが管理するリポジトリで Git サブモジュールを使用する場合の制限事項](#limitations-recommendations)も適用されます。
