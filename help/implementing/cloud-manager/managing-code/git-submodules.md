---
title: Adobe リポジトリのGit サブモジュールのサポート
description: Git サブモジュールを使用して、ビルド時に Git リポジトリ間で複数のブランチのコンテンツを結合する方法について説明します。
exl-id: fa5b0f49-4b87-4f39-ad50-7e62094d85f4
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 85ad7a7de35033b4b975c51c5f2f228cfdfa0152
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 67%

---

# Adobe リポジトリに対する Git サブモジュールのサポート {#git-submodule-support}

Git サブモジュールを使用すると、ビルド時に Git リポジトリ間で複数のブランチのコンテンツを結合できます。

Cloud Manager のビルドプロセスを実行すると、パイプラインのリポジトリが複製され、分岐がチェックアウトされます。 `.gitmodules` ファイルが分岐のルートディレクトリに存在する場合、対応するコマンドが実行されます。

次のコマンドは、各サブモジュールを適切なディレクトリにチェックアウトします。

```
$ git submodule update --init
```

この手法は、[複数のソース Git リポジトリの操作](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md)で説明しているソリューションの代わりになります。 Git サブモジュールに慣れ、外部マージ プロセスを管理しないことを好む組織に適しています。

例えば、3 つのリポジトリがあるとします。 各リポジトリには、`main` という名前の分岐が 1 つ含まれています。 プライマリリポジトリ（パイプラインで設定されたリポジトリ）で、`main` ブランチには、他の2つのリポジトリに含まれるプロジェクトを宣言する`pom.xml` ファイルがあります。

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

他の2つのリポジトリのサブモジュールを追加します。

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

Git サブモジュールについて詳しくは、[Git リファレンスマニュアル](https://git-scm.com/book/ja/v2/Git-Tools-Submodules)も参照してください。

## Adobe リポジトリの使用上のメモ {#usage-notes-recommendations-adobe-repos}

* Git URLは、前の節で説明した構文に従う必要があります。
* 分岐のルートにあるサブモジュールのみがサポートされます。
* セキュリティ上の理由から、Git の URL に資格情報を埋め込まないでください。
* 特に必要がない限り、アドビでは、以下を実行してシャローサブモジュールを使用することをお勧めします。
  各サブモジュールの `git config -f .gitmodules submodule.<submodule path>.shallow true`。
* Git サブモジュールの参照は、特定のGit コミットに保存されます。サブモジュールリポジトリに変更を加えた場合、参照されたコミットを更新する必要があります。
例えば、次を使用します。

  `git submodule update --remote`

## プライベートリポジトリに対する Git サブモジュールのサポート {#private-repositories}

[ プライベートリポジトリ ](private-repositories.md)でのGit サブモジュールのサポートは、Adobe リポジトリでの使用と同様です。

ただし、Cloud Managerでサブモジュール設定を認識するには、`pom.xml` ファイルを設定して`git submodule` コマンドを実行した後、`.gitmodules` ファイルをアグリゲータリポジトリのルートディレクトリに追加します。

![.gitmodules ファイル](assets/gitmodules.png)

![集積](assets/aggregator.png)

### 使用上のメモ {#usage-notes-recommendations-private-repos}

* サブモジュール Git の URL は、HTTPS 形式または SSH 形式にすることができますが、GitHub.com リポジトリを指す必要があります。 Adobe リポジトリサブモジュールを GitHub 集積リポジトリに追加すること、またはその逆はサポートされていません。
* GitHub サブモジュールには、Adobe GitHub アプリからアクセスできる必要があります。
* また、[アドビが管理するリポジトリで Git サブモジュールを使用する場合の制限事項](#usage-notes-recommendations-adobe-repos)も適用されます。
