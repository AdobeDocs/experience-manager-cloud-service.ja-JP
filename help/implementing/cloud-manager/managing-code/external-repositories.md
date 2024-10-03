---
title: Cloud Managerでの外部リポジトリの追加（早期導入）
description: 外部リポジトリをCloud Managerに追加する方法を説明します。 Cloud Managerは、GitHub、GitLab、Bitbucket リポジトリとの統合をサポートしています。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b90ace2250277005d8ac250c841104c93298a605
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 6%

---


# Cloud Managerでの外部リポジトリの追加 {#external-repositories}

外部リポジトリをCloud Managerに追加する方法を説明します。 Cloud Managerは、GitHub、GitLab、Bitbucket リポジトリとの統合をサポートしています。

>[!NOTE]
>
>この機能は、[早期導入プログラム](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)でのみ利用できます。

## 外部リポジトリの設定

Cloud Managerでの外部リポジトリの設定は、次の 3 つの手順で構成されます。

1. 選択したプログラムに [ 外部リポジトリを追加 ](#add-external-repo) します。
1. 外部リポジトリへのアクセストークンを指定します。
1. プライベート GitHub リポジトリの所有権を検証します。


## 外部リポジトリの追加 {#add-ext-repo}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、外部リポジトリをリンクするプログラムを選択します。

1. サイドメニューの **サービス** で、![ フォルダーアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg)**リポジトリ** を選択します。

   ![ リポジトリーページ ](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. **リポジトリ** ページの右上隅付近にある「**リポジトリを追加**」をクリックします。

1. **リポジトリを追加** ダイアログボックスで、「**プライベートリポジトリ**」を選択して、外部 Git リポジトリをプログラムにリンクします。

   ![独自のリポジトリの追加](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. 各フィールドに、リポジトリに関する次の詳細を入力します。

   | フィールド | 説明 |
   | --- | --- |
   | **リポジトリ名** | 必須。新しいリポジトリのわかりやすい名前。 |
   | **リポジトリ URL** | 必須。リポジトリの URL。<br><br> GitHub でホストされるリポジトリーを使用している場合、パスは `.git` で終わる必要があります。<br> 例：*`https://github.com/org-name/repo-name.git`* （URL パスは説明用です）。<br><br> 外部リポジトリを使用している場合は、URL パス形式 <br>`https://git-vendor-name.com/org-name/repo-name.git`<br> または <br>`https://self-hosted-domain/org-name/repo-name.git`<br> を使用し、Git ベンダーと一致させる必要があります。 |
   | リポジトリタイプ **選択します** | 必須。使用するリポジトリタイプ（**GitHub**、**GitLab**、**BitBucket**）を選択します。 上記のリポジトリ URL パスに Git ベンダー名（GitLab や Bitbucket など）が含まれている場合、リポジトリタイプは既に選択されています。 |
   | **説明** | オプション。リポジトリの詳細な説明。 |

1. 「**保存**」を選択して、リポジトリを追加します。

1. **プライベートリポジトリ所有権の検証** ダイアログボックスで、外部リポジトリの所有権を検証してアクセスできるようにするアクセストークンを指定します。

   ![ リポジトリ用の既存のアクセストークンの選択 ](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *BitBucket リポジトリの既存のアクセストークンの選択。*

   | トークンタイプ | 説明 |
   | --- | --- |
   | **既存のアクセストークンを使用** | 組織のリポジトリアクセストークンを既に指定していて、複数のリポジトリにアクセスできる場合、既存のトークンを選択できます。 「**トークン名**」ドロップダウンリストを使用して、リポジトリに適用するトークンを選択します。 そうでない場合は、新しいアクセストークンを追加します。 |
   | **新しいアクセストークンの追加** | **リポジトリタイプ：GitHub**<br>・「**トークン名**」テキストフィールドに、作成するアクセストークンの名前を入力します。<br>・ [GitHub ドキュメント ](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) の手順に従って、個人用アクセストークンを作成します。<br>・必要な権限：<br>  ・ `Read access to metadata`。<br>  ・ `Read and write access to code and pull requests`。<br>・ 「**アクセストークン**」フィールドに、作成したトークンをペーストします。 |
   |  | **リポジトリタイプ：GitLab**<br>・「**トークン名**」テキストフィールドに、作成するアクセストークンの名前を入力します。<br>・ [GitLab ドキュメント ](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html) の指示に従って、個人用アクセストークンを作成します。<br>・必要な権限：<br>  ・ `api`<br>  ・ `read_api`<br>  ・ `read_repository`<br>  ・ `write_repository`<br>・ 「**アクセストークン**」フィールドに、作成したトークンをペーストします。 |
   |  | **リポジトリタイプ：Bitbucket**<br>・「**トークン名**」テキストフィールドに、作成するアクセストークンの名前を入力します。<br>・ [Bitbucket ドキュメント ](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/) を使用して、リポジトリアクセストークンを作成します。<br>・必要な権限：<br>  ・ `Read and write access to code and pull requests`。 |

   >[!NOTE]
   >
   >**新しいアクセストークンの追加** 機能は、現在、早期導入者フェーズにあります。 追加の機能が予定されています。 その結果、アクセストークンに必要な権限が変更される可能性があります。 さらに、トークンを管理するユーザーインターフェイスが更新される可能性があり、トークンの有効期限などの機能が含まれている場合があります。 また、リポジトリにリンクされたトークンが有効なままであることを確認するための自動チェックも行われます。

1. 「**検証**」をクリックします。

検証後、外部リポジトリを使用してパイプラインにリンクする準備が整います。

## 検証済み外部リポジトリのパイプラインへのリンク {#validate-ext-repo}

1. パイプラインを追加または編集：
   * [実稼動パイプラインを追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [実稼動以外のパイプラインを追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [パイプラインを編集](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

   ![ パイプラインのソースコードリポジトリーと Git ブランチ ](/help/implementing/cloud-manager/managing-code/assets/pipeline-repo-gitbranch.png)
   *選択したリポジトリと Git ブランチを含む実稼動以外のパイプラインを追加ダイアログボックス*

1. パイプラインの追加または編集時に、新規または既存のパイプラインの **0}Source コード } の場所を指定するには、「** リポジトリー **」ドロップダウンリストから使用する外部リポジトリーを選択します。**

1. 「**Git ブランチ**」ドロップダウンリストで、パイプラインのソースとしてブランチを選択します。

1. 「**保存**」をクリックします。


>[!TIP]
>
>Cloud Manager でのリポジトリ管理について詳しくは、[Cloud Manager リポジトリ](/help/implementing/cloud-manager/managing-code/managing-repositories.md)を参照してください。


## 制限事項

* 外部リポジトリを設定パイプラインにリンクすることはできません。
* 外部リポジトリ（GitHub でホストされるリポジトリを除く）および **デプロイメントトリガー** オプション [!UICONTROL **Git の変更時**] を使用したパイプラインでは、トリガーは自動的には開始されません。 これらは手動で開始する必要があります。




