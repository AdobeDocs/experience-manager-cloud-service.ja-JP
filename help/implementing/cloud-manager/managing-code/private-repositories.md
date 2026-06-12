---
title: Cloud Manager でのプライベート GitHub リポジトリの追加
description: 独自のプライベート GitHub リポジトリを操作する Cloud Manager を設定する方法について説明します。
exl-id: 5232bbf5-17a5-4567-add7-cffde531abda
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 188201dfaececb21d373450711eb206b8e2323e2
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 47%

---

# Cloud Managerでのプライベート GitHub リポジトリの追加 {#private-repositories}

`github.com`でホストされているプライベート GitHub リポジトリと統合するようにCloud Managerを設定すると、Cloud Managerを使用してGitHub内で直接コードを検証できます。 このページは、GitHub プラン （無料、Pro、チーム、またはエンタープライズ クラウド）に関係なく、`github.com`でホストされているすべてのリポジトリに適用されます。 この設定により、コードを Adobe リポジトリと定期的に同期する必要がなくなります。

>[!IMPORTANT]
>Cloud Managerは、リポジトリのホスト場所に応じて、次の2つの方法のいずれかでGitHub リポジトリの所有権を検証します。
>
>* このページは、GitHub プラン （無料、Pro、チーム、またはエンタープライズ クラウド）に関係なく、`github.com`でホストされているすべてのリポジトリに適用されます。 これらのリポジトリでは、Adobe GitHub アプリを使用して所有権を検証します。 Cloud Managerはアプリを通じて直接統合されるため、Webhookの設定は必要ありません。
>* 次のいずれかのリポジトリタイプを追加する場合は、[Cloud Managerでの外部リポジトリの追加](/help/implementing/cloud-manager/managing-code/external-repositories.md)を参照してください。 これらのリポジトリでは、PAT （個人アクセストークン）と手動で設定されたWebhookを使用して所有権を検証します。
>
>   * GitHub Enterprise Server （GitHubのセルフホスティング版）リポジトリ。
>   * GitLab （`gitlab.com`とGitLabのセルフホスティング版の両方）リポジトリ。
>   * Bitbucket （のみ`bitbucket.org`、クラウドバージョン） リポジトリ。 Bitbucketのセルフホスティング バージョンは、2024年2月15日（PT）をもって非推奨（廃止予定）となりました。
>   * Azure DevOps （`dev.azure.com`） リポジトリ。

## 設定 {#configuration}

Cloud Managerでのプライベート GitHub リポジトリの設定は、次の2つの手順で構成されます。

1. [選択したプログラムにプライベート GitHub リポジトリ ](#add-repo)を追加します。
1. 次に、[ プライベート GitHub リポジトリの所有権を検証します](#validate-ownership)。



### プライベート GitHub リポジトリをプログラムに追加する {#add-repo}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プライベート Git リポジトリをリンクするプログラムを選択します。

1. サイドメニューの「**サービス**」で、![フォルダーアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg)、「**リポジトリ**」を選択します。

   ![リポジトリページ](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. **リポジトリ**&#x200B;ページの右上隅付近にある「**リポジトリを追加**」をクリックします。

1. **リポジトリを追加**&#x200B;ダイアログボックスで、リポジトリタイプとして「**プライベートリポジトリ**」を選択します。

   ![独自のリポジトリの追加](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. 各フィールドに、リポジトリに関する次の詳細を入力します。

   | フィールド | 説明 |
   | --- | --- |
   | リポジトリ名 | 新しいリポジトリのわかりやすい名前。 |
   | リポジトリ URL | プライベートリポジトリーのURL。末尾は`.git`にする必要があります。<br>例：*`https://github.com/org-name/repo-name.git`* （URL パスはイラスト用のみ）。 |
   | 説明（オプション） | リポジトリの詳細な説明です。 |

1. **保存**を選択します。
これで、[ プライベートリポジトリの所有権を検証できます](#validate-ownership)。

>[!TIP]
>
>Cloud Manager でのリポジトリ管理について詳しくは、[Cloud Manager リポジトリ](/help/implementing/cloud-manager/managing-code/managing-repositories.md)を参照してください。


### プライベート GitHub リポジトリの所有権の検証 {#validate-ownership}

Cloud ManagerがGitHub リポジトリで設定されるようになりましたが、リポジトリにアクセスするには認証が必要です。 アクセス権を付与するには、Adobe GitHub アプリをインストールし、指定したリポジトリを所有していることを確認する必要があります。

**プライベート GitHub リポジトリの所有権を検証するには：**

1. リポジトリを追加したら、**プライベートリポジトリ所有権の検証** ダイアログボックスの残りの手順に従います。

   ![プライベートリポジトリの所有権の検証](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

   |  | 説明 |
   | --- | --- |
   | **手順 1：GitHub アプリ** | Cloud Managerは、GitHub アプリを使用して、プライベートリポジトリと安全にやり取りします。<br>・ GitHub組織の所有者は、`https://github.com/apps/cloud-manager-for-aem`にあるアプリをインストールし、リポジトリへのアクセス権を付与する必要があります。<br>・ インストールとアクセス権の付与の詳細については、GitHubのドキュメントを参照してください。 |
   | **手順 2：秘密鍵ファイル** | セキュリティを強化するには、リポジトリのデフォルトブランチに秘密ファイルを作成する必要があります。<br>・「**Generate**」をクリックし、「**確認**」をクリックします。 Cloud Managerは、**秘密鍵ファイルの内容** テキストフィールドに秘密鍵ファイルの内容を生成します。<br>・「![ コピー」アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)をクリックして、そのフィールドから内容をコピーします。 秘密鍵ファイルのコンテンツは 1 回だけ表示されます。 このダイアログボックスを閉じる前にコンテンツをコピーしない場合は、秘密鍵を再生成します。 |

1. GitHub リポジトリのデフォルトブランチに、という名前の新しいファイルを作成します

   `.well-known/adobe/cloud-manager-challenge`

1. シークレットファイルの内容を新しいファイルに貼り付けて保存します。

   アプリがインストールされ、秘密鍵ファイルがリポジトリに存在したら、手順を続行します。

1. **プライベートリポジトリ所有権の検証**&#x200B;ダイアログボックスで、「**検証**」をクリックします。

アプリはインストールでき、秘密鍵ファイルはどちらの順序でも作成できます。 ただし、検証する前に両方の手順を完了する必要があります。

検証するまで、リポジトリには赤いアイコンが表示され、まだ検証されておらず、使用できないことが示されます。

![未検証のリポジトリ](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

**リポジトリ**&#x200B;ページのテーブルの&#x200B;**タイプ**&#x200B;列は、アドビ提供のリポジトリ（**Adobe**）と独自のプライベートリポジトリ（**GitHub**）を識別します。

後でリポジトリにアクセスして検証を完了するには、**リポジトリ** ページで、追加したGitHub リポジトリを表す行の![詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックします。 ドロップダウンリストで、「**所有権の検証**」を選択します。


## Cloud Managerでプライベート GitHub リポジトリを使用する {#using}

Cloud Manager で GitHub リポジトリが検証されると、統合は完了です。 Cloud Manager でリポジトリを使用できます。

**Cloud Managerでプライベート GitHub リポジトリを使用するには：**

1. プルリクエストを作成すると、GitHub チェックが自動的に開始します。

   ![GitHub チェック](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. プルリクエストごとに、[フルスタックコード品質パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)が自動的に作成されます。 このパイプラインは、プルリクエストの更新のたびに開始されます。

1. GitHub チェックは、コード品質チェックが完了するまで実行状態のままになります。 コード品質の結果は、GitHub チェックに生成されます。

   ![GitHub コード品質チェック](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

プルリクエストが結合されるか閉じられると、作成したフルスタックコード品質パイプラインが自動的に削除されます。

>[!TIP]
>
>プルリクエストチェックの実行時にGitHubから提供される情報について詳しくは、[GitHub Check Annotations](github-annotations.md)を参照してください。

>[!TIP]
>
>プライベートリポジトリに対する各プルリクエストを検証するために自動的に作成されるパイプラインは、制御することができます。 詳しくは、[プライベートリポジトリに対する GitHub チェック設定](github-check-config.md)を参照してください。


## プライベート GitHub リポジトリをパイプラインに関連付ける {#pipelines}

検証済みのプライベートリポジトリは、[フルスタックパイプラインおよびフロントエンドパイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)に関連付けることができます。



## 制限事項 {#limitations}

Cloud Managerでプライベートリポジトリを使用する場合は、次の制限が適用されます。

* 実稼動のフルスタックパイプラインでプライベートリポジトリを使用する場合、Git タグは作成およびプッシュされません。
* Adobe GitHub アプリがGitHub組織から削除された場合、すべてのリポジトリのプルリクエスト検証機能が削除されます。
* プライベート GitHub リポジトリと「on-commit」ビルドトリガーを使用するパイプラインは、選択したブランチに新しいコミットがプッシュされたときに自動的に開始されません。
* [アーティファクト再利用機能](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)は、プライベートリポジトリには適用されません。
* Cloud Manager から GitHub チェックを使用して、プルリクエストの検証を一時停止できません。 GitHub リポジトリが Cloud Manager で検証される場合、Cloud Manager は常に、そのリポジトリに対して作成されたプルリクエストの検証を試みます。
* GitHub 組織で IP 制限が適用されている場合は、サポートケースを開いて、許可する必要がある IP アドレスのリストを取得します。
