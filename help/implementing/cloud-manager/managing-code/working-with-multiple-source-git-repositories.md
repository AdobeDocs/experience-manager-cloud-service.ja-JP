---
title: 複数のリポジトリの使用
description: Cloud Manager を操作する際に複数の Git リポジトリを管理する方法について説明します。
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
source-git-commit: d67c5c9baafb9b7478f1d1c2ad924f5a8250a1ee
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 47%

---

# 複数のリポジトリの使用 {#working-with-multiple-source-git-repos}

Cloud Manager を操作する際に複数の Git リポジトリを管理する方法について説明します。

## 顧客の管理による Git リポジトリの同期 {#syncing-customer-managed-git-repositories}

Cloud Manager の Git リポジトリを直接操作するのではなく、[顧客が独自の Git リポジトリ（1 つまたは複数）を操作できます](integrating-with-git.md)。このような場合は、Cloud Manager の Git リポジトリを常に最新の状態に保つために、自動同期プロセスを設定する必要があります。

顧客の Git リポジトリがホストされている場所に応じて、GitHub アクションまたは継続的統合ソリューション（Jenkins など）を使用して、自動処理を設定できます。自動処理を実行すると、顧客が所有する Git リポジトリに対するすべてのプッシュを、Cloud Manager の Git リポジトリに自動的に転送できます。

顧客が所有する単一 Git リポジトリの場合のこうした自動処理は簡単ですが、複数のリポジトリの場合に自動処理を設定するには、初期設定が必要になります。複数の Git リポジトリーの内容を、単一の Cloud Manager Git リポジトリー内の異なるディレクトリにマッピングする必要があります。 Cloud Manager の Git リポジトリーには、ルート Maven をプロビジョニングする必要があります。 `pom.xml`、モジュールセクションに様々なサブプロジェクトをリスト表示する。

以下は、顧客が所有する 2 つの Git リポジトリのサンプル `pom.xml` ファイルです。

* 最初のプロジェクトは、 `project-a`.
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

このようなルート `pom.xml` が、Cloud Manager の Git リポジトリのブランチにプッシュされます。次に、変更内容を Cloud Manager の Git リポジトリーに自動的に転送するように、2 つのプロジェクトを設定する必要があります。

考えられる解決策は次のとおりです。

1. GitHub アクションは、プロジェクト A のブランチへのプッシュでトリガーできます。
1. このアクションは、プロジェクト A と Cloud Manager Git リポジトリーをチェックアウトし、すべての内容をプロジェクト A からディレクトリにコピーします `project-a` Cloud Manager の git リポジトリ内。
1. その後、アクションは変更をコミット — プッシュします。

例えば、プロジェクト A のメインブランチに対する変更は、Cloud Manager の Git リポジトリのメインブランチに自動的にプッシュされます。ブランチ間のマッピングが存在する可能性があります。例えば、 `dev` プロジェクト A 内で、 `development` Cloud Manager の git リポジトリ内。 同様の手順がプロジェクト B にも必要です。

分岐戦略とワークフローに応じて、異なるブランチに対して同期を設定できます。使用している Git リポジトリに GitHub アクションと似た概念が用意されていない場合は、Jenkins（または類似の）による統合も可能です。 この場合、webhook が Jenkins ジョブをトリガーし、このジョブが処理を実行します。

次の手順に従って、新しい、3 番目のソースまたはリポジトリを追加できます。

1. 新しいリポジトリーの変更を Cloud Manager の Git リポジトリーにプッシュする GitHub アクションを新しいリポジトリーに追加します。
1. このアクションを少なくとも 1 回実行して、プロジェクトコードが Cloud Manager の Git リポジトリにあることを確認します。
1. Cloud Manager の Git リポジトリのルート Maven `pom.xml` に新しいディレクトリへの参照を追加します。

## GitHub アクションの例 {#sample-github-action}

以下に示すサンプル GitHub アクションは、メインブランチへのプッシュでトリガーされ、Cloud Manager の Git リポジトリーのサブディレクトリにプッシュされます。 この GitHub アクションには、次の 2 つのシークレットを提供する必要があります。 `MAIN_USER` および `MAIN_PASSWORD`Cloud Manager の Git リポジトリに接続してプッシュできるようになります。

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

GitHub アクションは柔軟に使用できます。 Git リポジトリーのブランチ間のマッピングと、個別の Git プロジェクトのメインプロジェクトのディレクトリレイアウトへのマッピングを実行できます。

>[!NOTE]
>
>サンプルスクリプトでは `git add` を使用してリポジトリを更新します。 この場合、削除が含まれていると仮定します。 Git のデフォルト設定に応じて、これをに置き換える必要があります。 `git add --all`.

## Jenkins ジョブの例 {#sample-jenkins-job}

これは、Jenkins ジョブなどで使用できるサンプルスクリプトで、そのフローは次のとおりです。

1. Git リポジトリの変更によってトリガーされます。
1. そのプロジェクトまたはブランチの最新の状態を Jenkins ジョブがチェックアウトします。
1. 次に、ジョブがこのスクリプトをトリガーします。
1. このスクリプトは Cloud Manager の Git リポジトリをチェックアウトし、プロジェクトコードをサブディレクトリにコミットします。

Jenkins ジョブには、2 つのシークレットを提供する必要があります。 `MAIN_USER` および `MAIN_PASSWORD`Cloud Manager の Git リポジトリに接続してプッシュできるようになります。

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

Jenkins ジョブは柔軟に使用できます。 Git リポジトリーのブランチ間のマッピングと、個別の Git プロジェクトのメインプロジェクトのディレクトリレイアウトへのマッピングを実行できます。

>[!NOTE]
>
>サンプルスクリプトでは `git add` を使用してリポジトリを更新します。 この場合、削除が含まれていると仮定します。 Git のデフォルト設定に応じて、これをに置き換える必要があります。 `git add --all`.
