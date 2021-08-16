---
title: Cloud Managerリポジトリ
description: Cloud Managerリポジトリ
exl-id: Cloud Manager Repositories
source-git-commit: cebc603aab9c558239588f574f52568d05081b34
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Cloud Managerリポジトリ {#cloud-manager-repos}

Cloud Managerで作成および使用可能なリポジトリーは、リポジトリーページで表示および管理できます。

>[!NOTE]
>特定の会社またはAdobeのIdentity Managementシステム](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/ims.html)([)のすべてのプログラムに対して、300個のリポジトリが制限されています。

## リポジトリの追加と管理 {#add-manage-repos}

Cloud Managerでリポジトリーを表示および管理するには、次の手順に従います。

1. **プログラムの概要**&#x200B;ページで、「**リポジトリ**」タブをクリックし、**リポジトリ**&#x200B;ページに移動します。

1. 「**リポジトリを追加**」をクリックして、ウィザードを起動します。

   >[!NOTE]
   >リポジトリを追加するには、Deployment ManagerまたはBusiness Ownerの役割を持つユーザーがログインする必要があります。

   ![](assets/repos/create-repo2.png)


1. 必要に応じて名前と説明を入力し、「**保存**」をクリックします。

   ![](assets/repos/repo-1.png)

1. 「**保存**」を選択します。次に示すように、新しく作成されたリポジトリがテーブルに表示されます。

   >[!NOTE]
   >1つの&#x200B;*プライマリ*&#x200B;リポジトリまたは任意のパイプラインのブランチがあります。 [Gitサブモジュールのサポート](#git-submodule-support)を使用すると、ビルド時に多数のセカンダリブランチを含めることができます。

   ![](assets/repos/create-repo3.png)

   >[!NOTE]
   >Cloud Managerで作成したリポジトリは、パイプラインの追加または編集手順でも選択できます。 詳しくは、[CI-CDパイプラインの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en)を参照してください。

1. リポジトリを選択し、表の右端にあるメニューオプションをクリックして、リポジトリのURLを&#x200B;**コピー、**&#x200B;表示と更新&#x200B;**、**&#x200B;削除&#x200B;**のいずれかを選択できます（下図を参照）。**

   ![](assets/repos/create-repo3.png)


## Gitサブモジュールのサポート {#git-submodule-support}

Gitサブモジュールを使用すると、ビルド時に複数のGitリポジトリー間で複数のブランチのコンテンツを結合できます。 Cloud Managerのビルドプロセスを実行すると、パイプライン用に設定されたリポジトリのクローンを作成し、設定されたブランチをチェックアウトした後に、ブランチのルートディレクトリに`.gitmodules`ファイルが含まれている場合は、コマンドが実行されます。

```
$ git submodule update --init
```

これにより、各サブモジュールが適切なディレクトリにチェックアウトされます。 この手法は、Gitサブモジュールの使用に慣れており、外部マージプロセスの管理を希望しない組織にとって、 https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/working-with-multiple-source-git-repositories.htmlの代わりに使用できる可能性があります。

例えば、3つのリポジトリがあり、それぞれにmainという名前のブランチが1つあるとします。 「プライマリ」リポジトリ（パイプラインで設定されたもの）では、メインブランチに、他の2つのリポジトリに含まれるプロジェクトを宣言するpom.xmlファイルが含まれます。

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

次に、他の2つのリポジトリ用のサブモジュールを追加します。

```
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

その結果、`.gitmodules`ファイルは次のようになります。

```
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

gitサブモジュールの詳細については、Gitリファレンスマニュアル[を参照してください。](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

Gitサブモジュールを使用する場合は、次の点に注意してください。

* GitのURLは、上記の構文に正確に記述する必要があります。 セキュリティ上の理由から、これらのURLに資格情報を埋め込まないでください。
* ブランチのルートにあるサブモジュールのみがサポートされます。
* Gitサブモジュール参照は、特定のGitコミットに保存されます。 その結果、サブモジュールリポジトリに対して変更を加える場合、`git submodule update --remote`などを使用して、参照されるコミットを更新する必要があります。

