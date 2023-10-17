---
title: Cloud Manager リポジトリ
description: Cloud Manager で Git リポジトリを作成、表示および削除する方法について説明します。
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 100%

---


# Cloud Manager リポジトリ {#cloud-manager-repos}

Cloud Manager で Git リポジトリを作成、表示および削除する方法について説明します。

>[!NOTE]
>
>特定の企業または IMS 組織のすべてのプログラムで、使用できるリポジトリは 300 個までです。

## リポジトリの追加と管理 {#add-manage-repos}

Cloud Manager でリポジトリを表示および管理するには、次の手順に従います。

1. **プログラムの概要**&#x200B;ページで、「**リポジトリー**」タブをクリックし、**リポジトリー**&#x200B;ページに移動します。

1. 「**リポジトリーを追加**」をクリックして、ウィザードを起動します。

   ![「リポジトリーを追加」ボタン](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. 必要に応じて名前と説明を入力し、「**保存**」をクリックします。

   ![リポジトリーを追加ダイアログ](/help/implementing/cloud-manager/assets/repos/repo-1.png)

ウィザードが閉じると、新しいリポジトリがテーブルに表示されます。

テーブルでリポジトリを選択し、省略記号ボタンをクリックして、「**リポジトリー URL をコピー**」、「**表示と更新**」または「**削除**」を選択できます。

![リポジトリ関連オプション](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

Cloud Manager で作成されたリポジトリは、パイプラインの追加や編集の際にも選択できます。 詳しくは、[CI／CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を参照してください。

どのパイプラインにも 1 つのプライマリリポジトリまたはブランチがあります。[Git サブモジュールのサポート](#git-submodule-support)を使用すると、ビルド時に多数のセカンダリブランチを含めることができます。

>[!NOTE]
>
>リポジトリを追加するには、**デプロイメントマネージャー**&#x200B;または&#x200B;**ビジネスオーナー**&#x200B;の役割が必要です。

## リポジトリの削除 {#delete-repo}

リポジトリを削除すると、次のようになります。

* 削除したリポジトリ名は、今後作成される可能性のある新しいリポジトリに使用できなくなります。
   * このような場合、「`Repository name should be unique within organization.`」というエラーメッセージが表示されます。
* 削除したリポジトリを Cloud Manager で使用不可にし、パイプラインにリンクできないようにします。

Cloud Manager でリポジトリを削除するには、次の手順に従います。

1. **プログラムの概要**&#x200B;ページで、「**リポジトリー**」タブをクリックし、**リポジトリー**&#x200B;ページに移動します。

1. リポジトリを選択し、省略記号ボタンをクリックして「**削除**」を選択すると、リポジトリが削除されます。

   ![リポジトリの削除](/help/implementing/cloud-manager/assets/repos/delete-repo.png)

## Git サブモジュールのサポート {#git-submodule-support}

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

Git サブモジュールについて詳しくは、[Git リファレンスマニュアル](https://git-scm.com/book/ja/v2/Git-Tools-Submodules)を参照してください。

### 制限事項とレコメンデーション {#limitations-recommendations}

Git サブモジュールを使用する場合は、次の制限事項に注意してください。

* Git の URL は、前述の節で説明した構文に正確に一致している必要があります。
* ブランチのルートにあるサブモジュールのみがサポートされます。
* セキュリティ上の理由から、Git の URL に資格情報を埋め込まないでください。
* 特に必要がない限り、シャローサブモジュールを使用することを強くお勧めします。
   * それには、サブモジュールごとに `git config -f .gitmodules submodule.<submodule path>.shallow true` を実行します。
* Git サブモジュール参照は、特定の Git コミットに保存されます。その結果、サブモジュールリポジトリに対して変更を加えた場合は、 参照されるコミットを更新する必要があります。
   * 使用するコマンドの例：`git submodule update --remote`
