---
title: Cloud Manager での外部リポジトリの追加（早期導入）
description: Cloud Manager に外部リポジトリを追加する方法について説明します。Cloud Manager は、GitHub、GitLab、Bitbucket リポジトリとの統合をサポートしています。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: aebda813-2eb0-4c67-8353-6f8c7c72656c
source-git-commit: 9d58d9342a8c0337b1fa0c80b40f1cf6d07c2eee
workflow-type: ht
source-wordcount: '717'
ht-degree: 100%

---

# Cloud Manager での外部リポジトリの追加 {#external-repositories}

Cloud Manager に外部リポジトリを追加する方法について説明します。Cloud Manager は、GitHub、GitLab、Bitbucket リポジトリとの統合をサポートしています。

>[!NOTE]
>
>この機能は、[早期導入プログラム](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)でのみ利用できます。

## 外部リポジトリの設定

Cloud Manager での外部リポジトリの設定は、次の 3 つの手順で構成されます。

1. 選択したプログラムに[外部リポジトリを追加](#add-external-repo)します。
1. 外部リポジトリへのアクセストークンを指定します。
1. プライベート GitHub リポジトリの所有権の検証。


## 外部リポジトリの追加 {#add-ext-repo}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、外部リポジトリをリンクするプログラムを選択します。

1. サイドメニューの「**サービス**」で、![フォルダーアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg)、「**リポジトリ**」を選択します。

   ![リポジトリページ](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. **リポジトリ**&#x200B;ページの右上隅付近にある「**リポジトリを追加**」をクリックします。

1. **リポジトリを追加**&#x200B;ダイアログボックスで、外部の Git リポジトリをプログラムにリンクする「**プライベートリポジトリ**」を選択します。

   ![独自のリポジトリの追加](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. 各フィールドに、リポジトリに関する次の詳細を入力します。

   | フィールド | 説明 |
   | --- | --- |
   | **リポジトリ名** | 必須。新しいリポジトリのわかりやすい名前。 |
   | **リポジトリ URL** | 必須。リポジトリの URL。<br><br>GitHub でホストされているリポジトリを使用している場合は、パスの末尾を `.git` にする必要があります。<br>例：*`https://github.com/org-name/repo-name.git`*（URL パスは説明用です）。<br><br>外部リポジトリを使用している場合は、次の URL パス形式を使用する必要があります。<br>`https://git-vendor-name.com/org-name/repo-name.git`<br> または <br>`https://self-hosted-domain/org-name/repo-name.git`<br>。Git ベンダーと一致させる必要があります。 |
   | **リポジトリタイプを選択** | 必須。使用するリポジトリタイプ（**GitHub**、**GitLab**、または **BitBucket**）を選択します。上記のリポジトリ URL パスに GitLab や Bitbucket などの Git ベンダー名が含まれている場合、リポジトリタイプは既に事前に選択されています。 |
   | **説明** | オプション。リポジトリの詳細な説明です。 |

1. 「**保存**」を選択して、リポジトリを追加します。

1. **プライベートリポジトリの所有権の検証**&#x200B;ダイアログボックスで、外部リポジトリの所有権を検証し、アクセスできるようにするアクセストークンを指定します。

   ![リポジトリの既存のアクセストークンの選択](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *BitBucket リポジトリの既存のアクセストークンを選択します。*

   | トークンタイプ | 説明 |
   | --- | --- |
   | **既存のアクセストークンを使用** | 組織にリポジトリアクセストークンを既に指定し、複数のリポジトリにアクセスできる場合は、既存のトークンを選択できます。**トークン名**&#x200B;ドロップダウンリストを使用して、リポジトリに適用するトークンを選択します。それ以外の場合は、新しいアクセストークンを追加します。 |
   | **新しいアクセストークンを追加** | **リポジトリタイプ：GitHub**<br>• 「**トークン名**」テキストフィールドに、作成するアクセストークンの名前を入力します。<br>• [GitHub ドキュメント](https://docs.github.com/ja/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)の指示に従って、個人アクセストークンを作成します。<br>• 必要な権限：<br>  • `Read access to metadata`。<br>  • `Read and write access to code and pull requests`。<br>• 「**アクセストークン**」フィールドに、作成したトークンをペーストします。 |
   |  | **リポジトリタイプ：GitLab**<br>• 「**トークン名**」テキストフィールドに、作成するアクセストークンの名前を入力します。<br>• [GitLab ドキュメント](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html)の指示に従って、個人アクセストークンを作成します。<br>• 必要な権限：<br>  • `api`<br>  • `read_api`<br>  • `read_repository`<br>  • `write_repository`<br>• 「**アクセストークン**」フィールドに、作成したトークンをペーストします。 |
   |  | **リポジトリタイプ：Bitbucket**<br>• 「**トークン名**」テキストフィールドに、作成するアクセストークンの名前を入力します。<br>• [Bitbucket ドキュメント](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/)を使用して、リポジトリアクセストークンを作成します。<br>• 必要な権限：<br>  • `Read and write access to code and pull requests`。 |

   >[!NOTE]
   >
   >**新しいアクセストークンを追加**&#x200B;機能は現在、早期導入フェーズにあります。さらに機能の追加が予定されています。その結果、アクセストークンに必要な権限が変更される場合があります。また、トークンを管理するユーザーインターフェイスが更新され、トークンの有効期限などの機能が含まれる可能性もあります。さらに、リポジトリにリンクされたトークンが有効なままであることを確認する自動チェックが行われます。

1. 「**検証**」をクリックします。

検証後、外部リポジトリを使用してパイプラインにリンクする準備が整います。

## 検証済みの外部リポジトリのパイプラインへのリンク {#validate-ext-repo}

1. 次のように、パイプラインを追加または編集します。
   * [実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [パイプラインの編集](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

   ![パイプラインのソースコードリポジトリと Git 分岐](/help/implementing/cloud-manager/managing-code/assets/pipeline-repo-gitbranch.png)
   *選択したリポジトリと Git 分岐を含む実稼動以外のパイプラインを追加ダイアログボックス。*

1. パイプラインの追加または編集時に、新しいパイプラインまたは既存のパイプラインの&#x200B;**ソースコード**&#x200B;の場所を指定するには、**リポジトリ**&#x200B;ドロップダウンリストから使用する外部リポジトリを選択します。

1. **Git 分岐**&#x200B;ドロップダウンリストで、パイプラインのソースとして分岐を選択します。

1. 「**保存**」をクリックします。


>[!TIP]
>
>Cloud Manager でのリポジトリ管理について詳しくは、[Cloud Manager リポジトリ](/help/implementing/cloud-manager/managing-code/managing-repositories.md)を参照してください。


## 制限事項

外部リポジトリは、設定パイプラインにリンクできません。

<!-- THIS BULLET REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release. THEY CAN NOW START AUTOMATICALLY>
* Pipelines using external repositories (excluding GitHub-hosted repositories) and the **Deployment Trigger** option [!UICONTROL **On Git Changes**], triggers are not automatically started. They must be manually started. -->
