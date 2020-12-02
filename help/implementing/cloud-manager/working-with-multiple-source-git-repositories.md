---
title: 複数のソースGitリポジトリの操作
description: 複数のソースGitリポジトリの操作 —Cloud Services
translation-type: tm+mt
source-git-commit: 8e470ed1ea30fd2fa59617fdb6755abf9a0d74a2
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# 複数のソースGitリポジトリの操作{#working-with-multiple-source-git-repos}


## お客様が管理するGitリポジトリを同期{#syncing-customer-managed-git-repositories}

Cloud ManagerのGitリポジトリを直接操作する代わりに、ユーザーは独自のGitリポジトリまたは複数の独自のGitリポジトリを操作できます。 このような場合は、Cloud ManagerのGitリポジトリを常に最新の状態に保つために、自動同期プロセスを設定する必要があります。 お客様のGitリポジトリがホストされる場所に応じて、GitHubアクションまたはJenkinsのような継続的な統合ソリューションを使用して自動化をセットアップできます。 自動化を導入すると、顧客が所有するGitリポジトリに対するすべてのプッシュを、Cloud ManagerのGitリポジトリに自動的に転送できます。

1人の顧客が所有するGitリポジトリに対するこのような自動化はまっすぐ進みますが、複数のリポジトリに対してこの自動化を設定するには、初期設定が必要です。 複数のGitリポジトリのコンテンツは、1つのCloud ManagerのGitリポジトリ内の別のディレクトリにマッピングする必要があります。  Cloud ManagerのGitリポジトリをルートのMaven pomでプロビジョニングする必要があります。モジュールセクションに様々なサブプロジェクトがリストされています。下に、2つの顧客所有Gitリポジトリ用のサンプルpomを示します。最初のプロジェクトは`project-a`という名前のディレクトリに配置され、2番目のプロジェクトは`project-b`という名前のディレクトリに配置されます。

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

このようなルートpomは、Cloud Managerのgitリポジトリのブランチにプッシュされます。 次に、変更をCloud Managerのgitリポジトリに自動的に転送するために、2つのプロジェクトを設定する必要があります。 例えば、GitHubアクションは、プロジェクトAのブランチへのプッシュによってトリガーされます。このアクションは、プロジェクトAとCloud Manager Gitリポジトリをチェックアウトし、プロジェクトAからCloud ManagerのGitリポジトリの`project-a`ディレクトリにすべてのコンテンツをコピーして、変更をコミットプッシュします。 例えば、プロジェクトAのメインブランチに対する変更は、Cloud Managerのgitリポジトリのメインブランチに自動的にプッシュされます。 もちろん、プッシュなどのブランチ間のマッピングは、プロジェクトAの「dev」というブランチに対して、Cloud ManagerのGitリポジトリの「development」というブランチにプッシュされる場合があります。  プロジェクトBに対しても同様の設定を行う必要があります。

分岐の方法とワークフローに応じて、異なる分岐に対して同期を設定できます。 使用したGitリポジトリがGitHubアクションと類似した概念を提供しない場合は、Jenkins（または類似）を介した統合も可能です。 この場合、ウェブフックがJenkinsジョブをトリガし、このジョブが動作します。

次の手順に従って、新しい（3番目の）ソースまたはリポジトリを追加します。

1. 新しいGitHubアクション追加を新しいリポジトリに移動します。この操作により、リポジトリからCloud ManagerのGitリポジトリに変更がプッシュされます。
1. この操作を少なくとも1回実行して、プロジェクトコードがCloud ManagerのGitリポジトリにあることを確認します。
1. Cloud Manager GitリポジトリのルートMaven pomの新し追加いディレクトリへの参照です。


## 付録A:GitHubアクションの例{#sample-github-action}

これは、メインブランチに対するプッシュの後、Cloud ManagerのGitリポジトリのサブディレクトリにプッシュすることによってトリガーされるGitHubアクションのサンプルです。 Cloud ManagerのGitリポジトリに接続してプッシュできるようにするには、githubアクションに`MAIN_USER`と`MAIN_PASSWORD`の2つのシークレットを設定する必要があります。

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

上記のように、GitHubアクションを使用すると非常に柔軟に対応できます。 Gitリポジトリのブランチ間のマッピングは、別のgitプロジェクトをメインプロジェクトのディレクトリレイアウトにマッピングするだけでなく、すべて実行できます。

>[!NOTE]
>上記のスクリプトでは、`git add`を使用してリポジトリを更新します。リポジトリは、削除が含まれると想定します。デフォルトのGitの設定に応じて、`git add --all`に置き換える必要があります。

## 付録B:Jenkinsジョブの例{#sample-jenkins-job}

これは、Jenkinsジョブなどで使用できるサンプルスクリプトです。 Gitリポジトリの変更によってトリガーされます。 Jenkinsジョブは、そのプロジェクトまたはブランチの最新の状態をチェックアウトし、このスクリプトを実行します。

次に、このスクリプトはCloud ManagerのGitリポジトリをチェックアウトし、プロジェクトコードをサブディレクトリにコミットします。

Cloud ManagerのGitリポジトリに接続してプッシュできるようにするには、Jenkinsジョブに`MAIN_USER`と`MAIN_PASSWORD`の2つの秘密が必要です。

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

上記のように、Jenkinsの仕事を使うのは非常に柔軟です。 Gitリポジトリのブランチ間のマッピングは、別のgitプロジェクトをメインプロジェクトのディレクトリレイアウトにマッピングするだけでなく、すべて実行できます。

>[!NOTE]
>上記のスクリプトでは、`git add`を使用してリポジトリを更新します。リポジトリは、削除が含まれると想定します。デフォルトのGitの設定に応じて、`git add --all`に置き換える必要があります。