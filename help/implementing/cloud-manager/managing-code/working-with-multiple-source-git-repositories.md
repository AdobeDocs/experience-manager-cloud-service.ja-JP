---
title: 複数のリポジトリの使用
description: Cloud Manager を操作する際に複数の Git リポジトリを管理する方法について説明します。
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 40c7b033edde97cdc826efbe961105ca264525d9
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 61%

---

# 複数のリポジトリの使用 {#working-with-multiple-source-git-repos}

Cloud Manager を操作する際に複数の Git リポジトリを管理する方法について説明します。

## プライベート Git リポジトリの同期 {#syncing-customer-managed-git-repositories}

[お客様は、Cloud ManagerのGit リポジトリを直接操作する代わりに、自分のプライベート Git リポジトリ ](integrating-with-git.md)または複数のプライベート Git リポジトリを操作できます。 Cloud ManagerのGit リポジトリを常に最新の状態に保つには、自動同期プロセスを設定します。

顧客のGit リポジトリがホストされている場所に応じて、GitHub アクションまたはJenkinsのような継続的な統合ソリューションが自動化を設定します。 自動化を導入すれば、お客様が所有するGit リポジトリへのあらゆるプッシュは、Cloud ManagerのGit リポジトリに自動的に転送されます。

単一の顧客所有のGit リポジトリに対するこのような自動化は簡単ですが、複数のリポジトリに対して設定するには、初期設定が必要です。 複数の Git リポジトリのコンテンツは、1 つの Cloud Manager Git リポジトリ内の異なるディレクトリにマッピングする必要があります。 Cloud Manager の Git リポジトリは、ルートの Maven `pom.xml` を使用してプロビジョニングする必要があり、モジュールセクションに様々なサブプロジェクトが一覧表示されています。

顧客が所有する 2 つの Git リポジトリのサンプル `pom.xml` ファイルは次のとおりです。

* 最初のプロジェクトは、`project-a` という名前のディレクトリに格納されます。
* 2 番目のプロジェクトは、`project-b` という名前のディレクトリに格納されます。

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

このようなルート `pom.xml` が、Cloud Manager の Git リポジトリの分岐にプッシュされます。 次に、変更内容を Cloud Manager の Git リポジトリに自動的に転送するように、2 つのプロジェクトを設定する必要があります。

次の解決策が考えられます。

1. プロジェクト A の分岐にプッシュして、GitHub アクションをトリガーします。
1. このアクションでは、プロジェクト A とCloud Manager Git リポジトリがチェックアウトされます。 その後、すべてのコンテンツがプロジェクト A から Cloud Manager の Git リポジトリの `project-a` ディレクトリにコピーされます。
1. そして、アクションがコミットし、変更をプッシュします。

例えば、プロジェクト A のメイン分岐に対する変更は、Cloud Manager の Git リポジトリのメイン分岐に自動的にプッシュされます。 プロジェクト Aの`dev`という名前のブランチへのプッシュが、Cloud ManagerのGit リポジトリの`development`という名前のブランチにプッシュされるなど、ブランチ間にマッピングが存在します。 同様の手順がプロジェクト B にも必要です。

分岐戦略とワークフローに応じて、異なるブランチに対して同期を設定できます。 使用中のGit リポジトリーがGitHub アクションと類似したコンセプトを提供しない場合は、Jenkins （または類似の）を介した統合も可能です。 この場合、WebhookはJenkins ジョブをトリガーし、このジョブがタスクを実行します。

新しい、3番目のソースまたはリポジトリを追加するには、次の手順に従います。

1. そのリポジトリからの変更を Cloud Manager の Git リポジトリにプッシュする GitHub アクションを、新しいリポジトリに追加します。
1. プロジェクトコードがCloud ManagerのGit リポジトリにあることを確認するには、少なくとも1回はそのアクションを実行します。
1. Cloud Manager Git リポジトリで、ルート Maven `pom.xml` の新しいディレクトリへの参照を追加します。



## GitHub アクションの例 {#sample-github-action}

メイン分岐へのプッシュでトリガーされる GitHub アクションのサンプルは、次のとおりです。 次に、Cloud ManagerのGit リポジトリのサブディレクトリにプッシュします。 Cloud ManagerのGit リポジトリに接続してプッシュするには、GitHub アクションに2つのシークレット `MAIN_USER`と`MAIN_PASSWORD`を指定する必要があります。

```java
name: SYNC
env:
  # Username/email used to commit to Cloud Manager's Git repository
  USER_NAME: <NAME>
  USER_EMAIL: <EMAIL>
  # Directory within the Cloud Manager Git repository
  PROJECT_DIR: project-a
  # Cloud Manager's Git repository
  MAIN_REPOSITORY: https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
  # The branch in Cloud Manager's Git repository to push to
  MAIN_BRANCH : <BRANCH_NAME>
 
# Only run on a push to this branch
on:
  push:
     branches: [ main ]
 
jobs:
  build:
    runs-on: ubuntu-latest
 
    steps:
      # Checkout this project into a sub folder
      - uses: actions/checkout@v2
        with:
          path: sub
      # Cleanup sub project
      - name: Clean project
        run: |
          git -C sub log --format="%an : %s" -n 1 > commit.txt
          rm -rf sub/.git
          rm -rf sub/.github
      # Set global git configuration
      - name: Set git config
        run: |
          git config --global credential.helper cache
          git config --global user.email ${USER_EMAIL}
          git config --global user.name ${USER_NAME}
      # Checkout the main project
      - name: Checkout main project
        run:
          git clone -b ${MAIN_BRANCH} ${MAIN_REPOSITORY} ${MAIN_BRANCH} 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf ${MAIN_BRANCH}/${PROJECT_DIR} 
          mv sub ${MAIN_BRANCH}/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C ${MAIN_BRANCH} add -f ${PROJECT_DIR}
          git -C ${MAIN_BRANCH} commit -F ../commit.txt
          git -C ${MAIN_BRANCH} push
```

GitHub アクションは柔軟に使用できます。 Git リポジトリのブランチ間のマッピングを実行できるほか、個別の Git プロジェクトをメインプロジェクトのディレクトリレイアウトにマッピングすることもできます。

>[!NOTE]
>
>サンプルスクリプトでは、`git add`を使用してリポジトリ内のファイルをステージングします。 スクリプトは、削除が処理されることを前提としています。 Gitのデフォルト設定に応じて、`git add --all`に置き換えます。

## Jenkins ジョブの例 {#sample-jenkins-job}

次は、Jenkins ジョブなどで使用できるサンプルスクリプトで、そのフローは次のとおりです。

1. Git リポジトリの変更によってトリガーされます。
1. そのプロジェクトまたはブランチの最新の状態を Jenkins ジョブがチェックアウトします。
1. 次に、ジョブがこのスクリプトをトリガーします。
1. 今度は、このスクリプトは Cloud Manager の Git リポジトリをチェックアウトし、プロジェクトコードをサブディレクトリにコミットします。

Cloud Manager の Git リポジトリに接続してプッシュできるように、Jenkins ジョブに `MAIN_USER` と `MAIN_PASSWORD` の 2 つのシークレットを提供する必要があります。

```java
# Username/email used to commit to Cloud Manager's Git repository
export USER_NAME=<NAME>
export USER_EMAIL=<EMAIL>
# Directory within the Cloud Manager Git repository
export PROJECT_DIR=project-a
# Cloud Manager's Git repository
export MAIN_REPOSITORY=https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
# The branch in Cloud Manager's Git repository to push to
export MAIN_BRANCH=<BRANCH_NAME>
 
# clean up and init
rm -rf target
mkdir target
 
# mv project to sub folder
mkdir target/sub
for f in .* *
do
    if [ "$f" != "." -a "$f" != ".." -a "$f" != "target" ]
    then
        mv "$f" target/sub
    fi
done
cd target
 
# capture log and remove git info
cd sub
git log --format="%an : %s" -n 1 > ../commit.txt
rm -rf .git
rm -rf .github
cd ..
 
# checkout main repository
git clone -b $MAIN_BRANCH $MAIN_REPOSITORY main
cd main
 
# configure main repository
git config credential.helper cache
git config user.email $USER_EMAIL
git config user.name $USER_NAME
 
# update project in main
rm -rf $PROJECT_DIR
mv ../sub $PROJECT_DIR
 
# commit changes to main
git add -f $PROJECT_DIR
git commit -F ../commit.txt
git push
```

Jenkins ジョブは柔軟に使用できます。 Git リポジトリの分岐間のマッピングを実行できるほか、個別の Git プロジェクトをメインプロジェクトのディレクトリレイアウトにマッピングすることもできます。

>[!NOTE]
>
>サンプルスクリプトでは `git add` を使用してリポジトリを更新します。 このスクリプトは、削除が処理されることを前提としています。 Git のデフォルト設定によっては、`git add --all` に置き換える必要があります。
