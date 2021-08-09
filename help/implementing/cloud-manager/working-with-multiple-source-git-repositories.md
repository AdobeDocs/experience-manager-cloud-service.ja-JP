---
title: 複数ソース Git リポジトリーの操作
description: 複数ソース Git リポジトリーの操作 - Cloud Services
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '747'
ht-degree: 100%

---

# 複数ソース Git リポジトリーの操作 {#working-with-multiple-source-git-repos}


## 顧客が管理する Git リポジトリーの同期 {#syncing-customer-managed-git-repositories}

顧客は、Cloud Manager の Git リポジトリーを直接使用するのではなく、独自の Git リポジトリー（複数可）を使用できます。このような場合、Cloud Manager の Git リポジトリーを常に最新の状態に保つために、自動同期プロセスを設定する必要があります。顧客の Git リポジトリーがホストされる場所に応じて、GitHub アクションまたは Jenkins のような継続的な統合ソリューションを使用して自動化をセットアップできます。自動化を導入すると、顧客が所有する Git リポジトリーに対するすべてのプッシュを、Cloud Manager の Git リポジトリーに自動的に転送できます。

顧客が所有する 1 つの Git リポジトリーに対するこのような自動化は簡単ですが、複数のリポジトリーに対して自動化を設定するには、初期設定が必要です。複数の Git リポジトリーのコンテンツは、1 つの Cloud Manager の Git リポジトリー内の別のディレクトリにマッピングする必要があります。  Cloud Manager の Git リポジトリーは、ルートの Maven pom を使用してプロビジョニングする必要があります。モジュールセクションに様々なサブプロジェクトが一覧表示されます。

次に、顧客が所有する 2 つの Git リポジトリーのサンプル pom を示します。最初のプロジェクトは `project-a` という名前のディレクトリに配置され、2 番目のプロジェクトは `project-b` という名前のディレクトリに配置されます。

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

このようなルート pom は、Cloud Manager の Git リポジトリーのブランチにプッシュされます。次に、変更を Cloud Manager の Git リポジトリーに自動的に転送するために、2 つのプロジェクトを設定する必要があります。

例えば、GitHub アクションは、プロジェクト A のブランチへのプッシュによってトリガーされます。このアクションは、プロジェクト A と Cloud Manager Git リポジトリーをチェックアウトし、プロジェクト A から Cloud Manager の Git リポジトリーの `project-a` ディレクトリにすべてのコンテンツをコピーして、変更をコミットプッシュします。例えば、プロジェクト A のメインブランチに対する変更は、Cloud Manager の git リポジトリーのメインブランチに自動的にプッシュされます。もちろん、プッシュなどのブランチ間のマッピングは、プロジェクト A の「dev」ブランチに対して、Cloud Manager の Git リポジトリーの「development」ブランチにプッシュされる場合があります。プロジェクト B にも同様の手順が必要です。

ブランチの方法とワークフローに応じて、異なるブランチに対して同期を設定できます。使用した Git リポジトリーが GitHub アクションと類似した概念を提供しない場合は、Jenkins（やそれに類似したツール）を介した統合も可能です。この場合、webhook が Jenkins ジョブをトリガーし、このジョブが動作します。

次の手順に従って、新しい（3 番目の）ソースまたはリポジトリーを追加します。

1. 新しい GitHub アクション追加を新しいリポジトリーに移動します。この操作により、リポジトリーから Cloud Manager の Git リポジトリーに変更がプッシュされます。
1. この操作を少なくとも 1 回実行して、プロジェクトコードが Cloud Manager の Git リポジトリーにあることを確認します。
1. Cloud Manager の Git リポジトリーでルート Maven pom に新しいディレクトリへの参照を追加します。


## GitHub アクションの例 {#sample-github-action}

これは、メインブランチに対するプッシュの後、Cloud Manager の Git リポジトリーのサブディレクトリにプッシュすることによってトリガーされる GitHub アクションの例です。Cloud Manager の Git リポジトリーに接続してプッシュできるようにするには、GitHub アクションに `MAIN_USER` と `MAIN_PASSWORD` の 2 つのシークレットを提供する必要があります。

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

上に示すように、GitHub アクションの使用は非常に柔軟です。Git リポジトリーのブランチ間のマッピング、およびメインプロジェクトのディレクトリレイアウトへの個別の Git プロジェクトのマッピングを実行できます。

>[!NOTE]
>上記のスクリプトでは、`git add` を使用してリポジトリーを更新していますが、削除が含まれると想定しまています。デフォルトの Git の設定に応じて、`git add --all` に置き換える必要があります。

## Jenkins ジョブの例 {#sample-jenkins-job}

これは、Jenkins ジョブなどで使用できるスクリプトの例です。Git リポジトリーの変更によってトリガーされます。Jenkins ジョブは、そのプロジェクトまたはブランチの最新のステートをチェックアウトし、このスクリプトを実行します。

次に、このスクリプトは Cloud Manager の Git リポジトリーをチェックアウトし、プロジェクトコードをサブディレクトリにコミットします。

Cloud Manager の Git リポジトリーに接続してプッシュできるようにするには、Jenkins ジョブに `MAIN_USER` と ｓ`MAIN_PASSWORD` の 2 つのシークレットが必要です。

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

上に示すように、Jenkins ジョブの使用は非常に柔軟です。Git リポジトリーのブランチ間のマッピング、およびメインプロジェクトのディレクトリレイアウトへの個別の Git プロジェクトのマッピングを実行できます。

>[!NOTE]
>上記のスクリプトでは、`git add` を使用してリポジトリーを更新していますが、削除が含まれると想定しまています。デフォルトの Git の設定に応じて、`git add --all` に置き換える必要があります。
