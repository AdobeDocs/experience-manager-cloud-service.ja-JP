---
title: Git サブモジュールのサポート
description: Git サブモジュールを使用して、ビルド時に Git リポジトリ間で複数のブランチのコンテンツを結合する方法について説明します。
exl-id: fa5b0f49-4b87-4f39-ad50-7e62094d85f4
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: dc4008a33f6a786884a9aad30096ff4f0561346c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 24%

---

# Adobe リポジトリに対する Git サブモジュールのサポート {#git-submodule-support}

Git サブモジュールを使用すると、ビルド時に Git リポジトリ間で複数のブランチのコンテンツを結合できます。

Cloud Managerのビルドプロセスを実行すると、パイプラインのリポジトリを複製し、ブランチをチェックアウトします。 ブランチのルートディレクトリに `.gitmodules` ファイルが存在する場合は、対応するコマンドが実行されます。

次のコマンドは、各サブモジュールを適切なディレクトリにチェックアウトします。

```
$ git submodule update --init
```

この手法は、[ 複数のSource Git リポジトリーの操作 ](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md) で説明しているソリューションの代わりになります。 Git サブモジュールに慣れており、外部マージプロセスを管理しないことを好む組織に最適です。

例えば、3 つのリポジトリがあるとします。 各リポジトリには、`main` という名前のブランチが 1 つ含まれます。 プライマリリポジトリ（パイプラインで設定されたもの）の `main` ブランチには、他の 2 つのリポジトリに含まれているプロジェクトを宣言している `pom.xml` ファイルが含まれています。

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

次に、他の 2 つのリポジトリー用のサブモジュールを追加します。

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

結果は、次のような `.gitmodules` ファイルになります。

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

Git サブモジュールについて詳しくは、[Git リファレンスマニュアル ](https://git-scm.com/book/ja/v2/Git-Tools-Submodules) も参照してください。

## 制限事項と推奨事項 {#limitations-recommendations}

Adobeが管理するリポジトリで Git サブモジュールを使用する場合は、次の制限事項に注意してください。

* Git の URL は、前の節で説明した構文に正確に一致している必要があります。
* ブランチのルートにあるサブモジュールのみがサポートされます。
* セキュリティ上の理由から、Git の URL に資格情報を埋め込まないでください。
* 特に必要がない限り、Adobeでは、次のコマンドを実行してシャローサブモジュールを使用することをお勧めします。
  各サブモジュールの `git config -f .gitmodules submodule.<submodule path>.shallow true`。
* Git サブモジュール参照は、特定の Git コミットに保存されます。その結果、サブモジュールリポジトリに対して変更を加えた場合は、参照されるコミットを更新する必要があります。
例えば、以下を使用します。

  `git submodule update --remote`

## プライベートリポジトリに対する Git サブモジュールのサポート {#private-repositories}

[ プライベートリポジトリ ](private-repositories.md) での Git サブモジュールのサポートは、通常、Adobeリポジトリでの使用に似ています。

ただし、`pom.xml` ファイルを設定し、`git submodule` コマンドを実行した後、サブモジュールの設定を認識するために、Cloud Managerの集約リポジトリのルートディレクトリに `.gitmodules` ファイルを追加する必要があります。

![.gitmodules ファイル](assets/gitmodules.png)

![集積](assets/aggregator.png)

### 制限事項と推奨事項 {#limitations-recommendations-private-repos}

プライベートリポジトリで Git サブモジュールを使用する場合、次の制限に注意してください。

* サブモジュール Git の URL は、HTTPS 形式または SSH 形式にすることができますが、GitHub.com リポジトリを指す必要があります。 Adobeリポジトリサブモジュールを GitHub アグリゲータリポジトリーに追加する、またはその逆の操作はサポートされていません。
* GitHub サブモジュールは、Adobe GitHub アプリからアクセスできる必要があります。
* また、[アドビが管理するリポジトリで Git サブモジュールを使用する場合の制限事項](#limitations-recommendations)も適用されます。
