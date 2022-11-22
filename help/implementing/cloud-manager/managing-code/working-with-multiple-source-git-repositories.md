---
title: 複数のリポジトリーの使用
description: Cloud Manager を操作する際に複数の Git リポジトリを管理する方法について説明します。
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
source-git-commit: a7ae6d75d6820f48d3d45cb5830f888a87d51de1
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 41%

---

# 複数のリポジトリーの使用 {#working-with-multiple-source-git-repos}

Cloud Manager を操作する際に複数の Git リポジトリを管理する方法について説明します。

## 顧客が管理する Git リポジトリーの同期 {#syncing-customer-managed-git-repositories}

Cloud Manager の Git リポジトリを直接操作する代わりに、 [のお客様が独自の git リポジトリを使用する](integrating-with-git.md) または複数の独自の git リポジトリー その場合は、Cloud Manager の Git リポジトリを常に最新の状態に保つために、自動同期プロセスを設定する必要があります。

顧客の Git リポジトリがホストされている場所に応じて、GitHub アクションまたは Jenkins のような継続的な統合ソリューションを使用して、自動処理を設定できます。 自動処理を実行すると、顧客が所有する Git リポジトリに対するすべてのプッシュを、Cloud Manager の Git リポジトリに自動的に転送できます。

顧客が所有する単一の Git リポジトリに対するこのような自動化は簡単ですが、複数のリポジトリに対して自動化を設定するには、初期設定が必要です。 複数の Git リポジトリーの内容を、単一の Cloud Manager Git リポジトリー内の異なるディレクトリにマッピングする必要があります。  Cloud Manager の Git リポジトリーには、ルート Maven をプロビジョニングする必要があります `pom.xml`（モジュールセクションに様々なサブプロジェクトを表示）

以下はサンプルです `pom.xml` 顧客が所有する 2 つの git リポジトリー用のファイル。

* 最初のプロジェクトは、 `project-a`.
* 2 つ目のプロジェクトは、 `project-b`.

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

このようなルート `pom.xml` が、Cloud Manager の Git リポジトリのブランチにプッシュされます。次に、変更を Cloud Manager の Git リポジトリに自動的に転送するように、2 つのプロジェクトをセットアップする必要があります。

考えられる解決策は次のとおりです。

1. GitHub アクションは、プロジェクト A のブランチへのプッシュでトリガーできます。
1. このアクションにより、プロジェクト A と Cloud Manager Git リポジトリーがチェックアウトされ、すべての内容がプロジェクト A からディレクトリにコピーされます `project-a` Cloud Manager の git リポジトリ内。
1. その後、アクションは変更をコミット — プッシュします。

例えば、プロジェクト A のメインブランチに対する変更は、Cloud Manager の git リポジトリーのメインブランチに自動的にプッシュされます。もちろん、プロジェクト A の `dev` というブランチへのプッシュが、Cloud Manager の Git リポジトリにある `development` ブランチにプッシュされるなど、ブランチ間でマッピングがおこなわれる場合があります。プロジェクト B にも同様の手順が必要です。

ブランチの方法とワークフローに応じて、異なるブランチに対して同期を設定できます。使用する Git リポジトリが GitHub アクションと類似した概念を提供しない場合は、Jenkins（またはそれに類似のもの）を介した統合も可能です。この場合、Webhook が Jenkins ジョブをトリガーし、このジョブを実行します。

次の手順に従って、新しい、3 番目のソースまたはリポジトリを追加します。

1. 新しいリポジトリに、そのリポジトリからの変更を Cloud Manager の Git リポジトリにプッシュする新しい GitHub アクション追加します。
1. このアクションを少なくとも 1 回実行して、プロジェクトコードが Cloud Manager の Git リポジトリにあることを確認します。
1. Cloud Manager の Git リポジトリのルート Maven `pom.xml` に新しいディレクトリへの参照を追加します。

## GitHub アクションの例 {#sample-github-action}

以下に示すサンプル GitHub アクションは、メインブランチへのプッシュでトリガーされ、Cloud Manager の Git リポジトリーのサブディレクトリにプッシュされます。 Cloud Manager の Git リポジトリに接続してプッシュできるように、この GitHub アクションに `MAIN_USER` と `MAIN_PASSWORD` の 2 つのシークレットを提供する必要があります。

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

GitHub アクションは非常に柔軟に使用できます。 Git リポジトリのブランチ間のマッピングや個別の Git プロジェクトをメインプロジェクトのディレクトリレイアウトにマッピングも実行できます。

>[!NOTE]
>
>サンプルスクリプトでは `git add` リポジトリを更新します。 この場合、削除が含まれていると仮定します。 Git のデフォルト設定に応じて、これを `git add --all` に置き換える必要がある場合があります。

## Jenkins ジョブの例 {#sample-jenkins-job}

これは、Jenkins ジョブなどで使用できる、次のフローを持つスクリプトの例です。

1. Git リポジトリの変更によってトリガーされます。
1. Jenkins ジョブは、そのプロジェクトまたはブランチの最新の状態をチェックアウトします。
1. 次に、ジョブはこのスクリプトをトリガーにします。
1. 次のスクリプトは Cloud Manager の Git リポジトリーをチェックアウトし、プロジェクトコードをサブディレクトリにコミットします。

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

Jenkins ジョブは非常に柔軟に使用できます。 Git リポジトリのブランチ間のマッピングや個別の Git プロジェクトをメインプロジェクトのディレクトリレイアウトにマッピングも実行できます。

>[!NOTE]
>
>サンプルスクリプトでは `git add` リポジトリを更新します。 この場合、削除が含まれていると仮定します。 Git のデフォルト設定に応じて、これを `git add --all` に置き換える必要がある場合があります。
