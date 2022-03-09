---
title: Cloud Manager リポジトリー
description: Cloud Manager で Git リポジトリを作成、表示および削除する方法について説明します。
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 27%

---


# Cloud Manager リポジトリー {#cloud-manager-repos}

Cloud Manager で Git リポジトリを作成、表示および削除する方法について説明します。

>[!NOTE]
>
>任意の会社または IMS 組織のすべてのプログラムに対して、300 個のリポジトリーの制限があります。

## リポジトリーの追加と管理 {#add-manage-repos}

Cloud Manager でリポジトリを表示および管理する手順に従います。

1. **プログラムの概要**&#x200B;ページで、「**リポジトリー**」タブをクリックし、**リポジトリー**&#x200B;ページに移動します。

1. クリック **リポジトリを追加** をクリックして、ウィザードを起動します。

   ![リポジトリ追加ボタン](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. 必要に応じて名前と説明を入力し、「 」をクリックします。 **保存**.

   ![リポジトリを追加ダイアログ](/help/implementing/cloud-manager/assets/repos/repo-1.png)

ウィザードが閉じると、新しいリポジトリがテーブルに表示されます。

テーブル内のリポジトリーを選択し、省略記号ボタンをクリックして、「 」を選択します。 **リポジトリ URL をコピー**, **表示と更新**&#x200B;または **削除**.

![リポジトリオプション](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

Cloud Manager で作成されたリポジトリは、パイプラインの追加や編集の際に選択することもできます。 ドキュメントを参照してください [CI/CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) を参照してください。

どのパイプラインにも 1 つのプライマリリポジトリーまたはブランチがあります。を使用 [git サブモジュールのサポート](#git-submodule-support)で指定した場合、ビルド時に多数のセカンダリブランチを含めることができます。

>[!NOTE]
>
>ユーザーは、の役割を持っている必要があります **デプロイメントマネージャー** または **ビジネスオーナー** を追加して、リポジトリを追加できるようにします。

## リポジトリーの削除 {#delete-repo}

リポジトリーを削除すると、次のようになります。

* 削除したリポジトリー名は、今後作成される可能性のある新しいリポジトリーに使用できなくなります。
   * エラーメッセージ `Repository name should be unique within organization.` この場合、が表示されます。
* 削除したリポジトリを Cloud Manager で使用できなくし、パイプラインへのリンクに使用できなくします。

Cloud Manager でリポジトリを削除するには、次の手順に従います。

1. **プログラムの概要**&#x200B;ページで、「**リポジトリー**」タブをクリックし、**リポジトリー**&#x200B;ページに移動します。

1. リポジトリを選択し、省略記号ボタンをクリックして、「 」を選択します。 **削除** をクリックして、リポジトリを削除します。

   ![リポジトリーを削除](/help/implementing/cloud-manager/assets/repos/delete-repo.png)

## Git サブモジュールのサポート {#git-submodule-support}

Git サブモジュールを使用すると、ビルド時に Git リポジトリー間で複数のブランチのコンテンツを結合できます。

Cloud Manager のビルドプロセスを実行すると、パイプライン用に設定されたリポジトリーのクローンを作成し、設定されたブランチをチェックアウトした後に、ブランチのルートディレクトリに `.gitmodules` ファイルが含まれている場合は、コマンドが実行されます。

次のコマンドは、各サブモジュールを適切なディレクトリにチェックアウトします。

```
$ git submodule update --init
```

この方法は、ドキュメントで説明されているソリューションの代わりに使用できる可能性があります [複数のソース Git リポジトリーの操作](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md) git サブモジュールの使用に慣れており、外部マージプロセスを管理したくない組織向けの機能です。

例えば、3 つのリポジトリがあり、それぞれにという名前の 1 つのブランチがあるとします。 `main`. プライマリリポジトリ（パイプラインで設定されたリポジトリ）では、 `main` ブランチに `pom.xml` 他の 2 つのリポジトリーに含まれるプロジェクトを宣言するファイル。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
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

次に、他の 2 つのリポジトリ用のサブモジュールを追加します。

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

その結果、 `.gitmodules` ファイルの内容は次のようになります。

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

git サブモジュールについて詳しくは、 [Git リファレンスマニュアル](https://git-scm.com/book/ja/v2/Git-Tools-Submodules)

### 制限と Recommendations {#limitations-recommendations}

Git サブモジュールを使用する場合は、次の制限事項に注意してください。

* Git の URL は、前の節で説明した構文に正確に含まれている必要があります。
* ブランチのルートにあるサブモジュールのみがサポートされます。
* セキュリティ上の理由から、資格情報を Git URL に埋め込まないでください。
* 特に必要がない限り、シャローサブモジュールを使用することを強くお勧めします。
   * それには、サブモジュールごとに `git config -f .gitmodules submodule.<submodule path>.shallow true` を実行します。
* Git サブモジュール参照は、特定の Git コミットに保存されます。 その結果、サブモジュールリポジトリを変更する場合は、参照されるコミットを更新する必要があります。
   * 例えば、 `git submodule update --remote`
