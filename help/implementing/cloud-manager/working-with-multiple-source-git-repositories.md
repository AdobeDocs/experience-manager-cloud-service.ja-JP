---
title: 複数のソース Git リポジトリーの操作
description: 複数のソースGitリポジトリの操作 —Cloud Services
translation-type: tm+mt
source-git-commit: e8cfe8eeec697fe74da02e178a89fc7a0e22d441
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 98%

---


# 複数のソース Git リポジトリーの操作 {#working-with-multiple-source-git-repos}


## 顧客が管理する Git リポジトリーの同期 {#syncing-customer-managed-git-repositories}

顧客は Cloud Manager の Git リポジトリーを直接操作するのではなく、独自の Git リポジトリー（1 つまたは複数）を操作できます。このような場合は、Cloud Manager の Git リポジトリーを常に最新の状態に保つために、自動同期プロセスをセットアップする必要があります。顧客の Git リポジトリーがホストされている場所に応じて、GitHub アクションまたは継続的統合ソリューション（Jenkins など）を使用して、自動処理をセットアップできます。自動処理をセットアップすると、顧客が所有する Git リポジトリーに対するすべてのプッシュを、Cloud Manager の Git リポジトリーに自動的に転送できます。

顧客が所有する Git リポジトリーが １ つだけであれば、このような自動処理は簡単ですが、複数のリポジトリーがある場合に自動処理をセットアップするには、初期設定が必要です。複数の Git リポジトリーの内容を、Cloud Manager の単一 Git リポジトリー内の様々なディレクトリにマッピングする必要があります。Cloud Manager の Git リポジトリーには、ルート Maven POM ファイルをプロビジョニングして、そのモジュールセクションに様々なサブプロジェクトをリストアップする必要があります。

顧客が所有する Git リポジトリーが 2 つある場合のサンプル POM ファイルを以下に示します。最初のプロジェクトは `project-a`、2 番目のプロジェクトは `project-b` という名前のディレクトリにそれぞれ格納されます。

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

このようなルート POM ファイルが、Cloud Manager の Git リポジトリーのブランチにプッシュされます。次に、変更内容を Cloud Manager の Git リポジトリーに自動的に転送するように、2 つのプロジェクトをセットアップする必要があります。

例えば、プロジェクト A のブランチにプッシュすることで GitHub アクションをトリガーできます。このアクションは、プロジェクト A と Cloud Manager の Git リポジトリーをチェックアウトし、プロジェクト A のすべての内容を Cloud Manager の Git リポジトリーの `project-a` ディレクトリにコピーした後、変更をコミットプッシュします。例えば、プロジェクト A のメインブランチに対する変更は、Cloud Manager の Git リポジトリーのメインブランチに自動的にプッシュされます。もちろん、プロジェクト Aの「dev」ブランチへのプッシュが Cloud Manager の Git リポジトリーの「development」ブランチにプッシュされるといった、ブランチ間のマッピングが存在するでしょう。同様の手順がプロジェクト B にも必要です。

分岐戦略とワークフローに応じて、様々なブランチに対して同期を設定できます。使用している Git リポジトリーに GitHub アクションのような概念が用意されていない場合は、Jenkins（または類似のソリューション）を介した統合も可能です。この場合は、Jenkins ジョブが Web フックでトリガーされ、処理をおこないます。

新しい（3 番目の）ソースまたはリポジトリーを追加するには、次の手順に従います。

1. 新しいリポジトリーの変更内容を Cloud Manager の Git リポジトリーにプッシュする新しい GitHub アクションを新しいリポジトリーに追加します。
1. このアクションを少なくとも 1 回実行して、プロジェクトコードが Cloud Manager の Git リポジトリー内に確実に存在するようにします。
1. 新しいディレクトリへの参照を Cloud Manager の Git リポジトリーのルート Maven POM ファイルに追加します。


## GitHub アクションの例 {#sample-github-action}

以下に示すサンプル GitHub アクションは、メインブランチへのプッシュでトリガーされ、Cloud Manager の Git リポジトリーのサブディレクトリにプッシュします。Cloud Manager の Git リポジトリーに接続してプッシュできるように、この GitHub アクションに `MAIN_USER` と `MAIN_PASSWORD` の 2 つのシークレットを提供する必要があります。

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
          git clone -b ${MAIN_BRANCH} https://${{ secrets.PAT }}@github.com/${MAIN_REPOSITORY}.git main 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf main/${PROJECT_DIR} 
          mv sub main/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C main add -f ${PROJECT_DIR}
          git -C main commit -F ../commit.txt
          git -C main push
```

上記のように、GitHub アクションは非常に柔軟に使用できます。個別の Git プロジェクトをメインプロジェクトのディレクトリレイアウトにマッピングするだけでなく、Git リポジトリーのブランチ間のマッピングも実行できます。

>[!NOTE]
>上記のスクリプトでは、`git add` を使用してリポジトリーを更新していますが、この場合は削除が含まれていると仮定しています。Git のデフォルト設定によっては、これを `git add --all` に置き換える必要があります。

## Jenkins ジョブの例 {#sample-jenkins-job}

Jenkins ジョブまたは同種のジョブで使用できるスクリプトの例を以下に示します。これは Git リポジトリー内の変更によってトリガーされます。Jenkins ジョブでは、そのプロジェクトまたはブランチの最新の状態をチェックアウトしてから、このスクリプトをトリガーします。

このスクリプトは Cloud Manager の Git リポジトリーをチェックアウトし、プロジェクトコードをサブディレクトリにコミットします。

Cloud Manager の Git リポジトリーに接続してプッシュできるように、この Jenkins ジョブに `MAIN_USER` と `MAIN_PASSWORD` の 2 つのシークレットを提供する必要があります。

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

上記のように、Jenkins ジョブは非常に柔軟に使用できます。個別の Git プロジェクトをメインプロジェクトのディレクトリレイアウトにマッピングするだけでなく、Git リポジトリーのブランチ間のマッピングも実行できます。

>[!NOTE]
>上記のスクリプトでは、`git add` を使用してリポジトリーを更新していますが、この場合は削除が含まれていると仮定しています。Git のデフォルト設定によっては、これを `git add --all` に置き換える必要があります。