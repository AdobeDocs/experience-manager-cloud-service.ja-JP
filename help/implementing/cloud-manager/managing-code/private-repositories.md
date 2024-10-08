---
title: Cloud Manager でのプライベート GitHub リポジトリの追加
description: 独自のプライベート GitHub リポジトリを操作する Cloud Manager を設定する方法について説明します。
exl-id: 5232bbf5-17a5-4567-add7-cffde531abda
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: a5e9b29a8108d5c012d402fda8ff7544e02ca911
workflow-type: ht
source-wordcount: '928'
ht-degree: 100%

---

# Cloud Manager でのプライベート GitHub リポジトリの追加 {#private-repositories}

プライベート GitHub リポジトリと統合するように Cloud Manager をセットアップすると、Cloud Manager を使用して GitHub 内で直接コードを検証できます。この設定により、コードを Adobe リポジトリと定期的に同期する必要がなくなります。

<!-- CONSIDER ADDING MORE DETAIL... THE WHY. Some key points about this capability include the following:

* **Direct Integration**: With this setup, you can directly link your private GitHub repositories to Cloud Manager, allowing for seamless code validation, deployment, and CI/CD (Continuous Integration/Continuous Deployment) pipelines without needing to maintain a separate sync process with Adobe's default Git repository.

* **Customization and Autonomy**: Companies often prefer managing their own source code repositories for security, control, and integration purposes. "Build your own GitHub" allows organizations to maintain their internal development processes while leveraging the full functionality of Cloud Manager for building, testing, and deploying AEM (Adobe Experience Manager) applications.

* **Simplified Workflow**: It reduces the overhead of synchronizing code between multiple repositories by allowing Cloud Manager to access the organization's private repository directly, making the development cycle faster and more efficient.

* **CI/CD Pipelines**: Teams can still benefit from Adobe Cloud Manager's automated build, test, and deployment processes, as the integration allows the CI/CD pipelines to pull code from the organization's own GitHub repository.

In essence, a "Build your own GitHub" in Adobe Cloud Manager empowers teams to manage their own GitHub repositories while still using the robust deployment and validation capabilities of Cloud Manager. -->

>[!NOTE]
>
>この機能は、パブリック GitHub 専用です。自己ホスト型 GitHub のサポートは利用できません。

## 設定 {#configuration}

Cloud Manager でのプライベート GitHub リポジトリの設定は、次の 2 つの手順で構成されます。

1. 選択したプログラムに[プライベート GitHub リポジトリを追加](#add-repo)します。
1. 次に、[プライベート GitHub リポジトリの所有権を検証](#validate-ownership)します。

### プログラムへのプライベート GitHub リポジトリの追加 {#add-repo}

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
   | リポジトリ URL | プライベートリポジトリの URL（`.git` で終了する必要があります）。<br>例：*`https://github.com/org-name/repo-name.git`*（URL パスは説明用です）。 |
   | 説明（オプション） | リポジトリの詳細な説明です。 |

1. 「**保存**」を選択します。
これで、[プライベートリポジトリの所有権を検証](#validate-ownership)できるようになりました。

>[!TIP]
>
>Cloud Manager でのリポジトリ管理について詳しくは、[Cloud Manager リポジトリ](/help/implementing/cloud-manager/managing-code/managing-repositories.md)を参照してください。



### プライベート GitHub リポジトリの所有権の検証 {#validate-ownership}

Cloud Manager は GitHub リポジトリを認識しましたが、引き続きアクセスする必要があります。アクセス権を付与するには、Adobe GitHub アプリをインストールし、指定したリポジトリを所有していることを確認する必要があります。

**プライベート GitHub リポジトリの所有権を検証するには：**

1. 独自のリポジトリを追加した後、**プライベートリポジトリ所有権の検証**&#x200B;ダイアログボックスで残りの手順に従います。

   ![プライベートリポジトリの所有権の検証](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

   |  | 説明 |
   | --- | --- |
   | **手順 1：GitHub アプリ** | Cloud Manager は、GitHub アプリを使用して、プライベートリポジトリと安全にやり取りします。<br>• GitHub 組織の所有者は、`https://github.com/apps/cloud-manager-for-aem` にあるアプリをインストールし、リポジトリへのアクセス権を付与する必要があります。<br>• インストールとアクセス権の付与に関する詳細については、GitHub のドキュメントを参照してください。 |
   | **手順 2：秘密鍵ファイル** | セキュリティを強化するには、リポジトリのデフォルトのブランチに秘密鍵ファイルを作成する必要があります。<br>• 「**生成**」をクリックし、「**確認**」をクリックします。Cloud Manager は、「**秘密鍵ファイルコンテンツ**」テキストフィールドに秘密鍵ファイルのコンテンツを生成します。<br>• ![コピーアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) をクリックして、そのフィールドからコンテンツをコピーします。秘密鍵ファイルのコンテンツは 1 回だけ表示されます。このダイアログボックスを閉じる前にコンテンツをコピーしない場合は、秘密鍵を再生成します。 |

1. GitHub リポジトリのデフォルトブランチに、次の名前の新しいファイルを作成します。

   `.well-known/adobe/cloud-manager-challenge`

1. 秘密鍵ファイルのコンテンツを、先ほど作成した新しいファイルに貼り付けて保存します。

   アプリがインストールされ、秘密鍵ファイルがリポジトリに存在する場合は、手順を続行します。

1. **プライベートリポジトリ所有権の検証**&#x200B;ダイアログボックスで、「**検証**」をクリックします。

アプリのインストールと秘密鍵ファイルの作成は、任意の順序で行うことができます。ただし、検証する前に両方の手順を完了する必要があります。

検証されるまで、リポジトリは赤色のアイコンで表示されます。これは、リポジトリがまだ検証されておらず、まだ使用できないことを示します。

![未検証のリポジトリ](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

**リポジトリ**&#x200B;ページのテーブルの&#x200B;**タイプ**&#x200B;列は、アドビ提供のリポジトリ（**Adobe**）と独自のプライベートリポジトリ（**GitHub**）を識別します。

後でリポジトリに戻って検証を完了する必要がある場合は、**リポジトリ**&#x200B;ページで、自身が追加した GitHub リポジトリを表す行の![ 詳細アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックします。ドロップダウンリストで、「**所有権の検証**」を選択します。



## Cloud Manager でのプライベート GitHub リポジトリの使用 {#using}

Cloud Manager で GitHub リポジトリが検証されると、統合は完了です。Cloud Manager でリポジトリを使用できます。

**Cloud Manager でプライベートリポジトリを使用するには：**

1. プルリクエストを作成すると、GitHub チェックが自動的に開始します。

   ![GitHub チェック](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. プルリクエストごとに、[フルスタックコード品質パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)が自動的に作成されます。このパイプラインは、プルリクエストの更新のたびに開始されます。

1. GitHub チェックは、コード品質チェックが完了するまで実行状態のままになります。コード品質の結果は、GitHub チェックに生成されます。

   ![GitHub コード品質チェック](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

プルリクエストが結合されるか閉じられると、作成したフルスタックコード品質パイプラインが自動的に削除されます。

>[!TIP]
>
>プルリクエストチェックの実行時に GitHub 経由で提供される情報について詳しくは、[GitHub チェック注釈](github-annotations.md)を参照してください。

>[!TIP]
>
>プライベートリポジトリに対する各プルリクエストを検証するために自動的に作成されるパイプラインは、制御することができます。詳しくは、[プライベートリポジトリに対する GitHub チェック設定](github-check-config.md)を参照してください。



## プライベートリポジトリとパイプラインの関連付け {#pipelines}

検証済みのプライベートリポジトリは、[フルスタックパイプラインおよびフロントエンドパイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)に関連付けることができます。



## 制限事項 {#limitations}

Cloud Manager でプライベートリポジトリを使用する場合は、特定の制限が適用されます。

* Web 階層および設定パイプラインは、プライベートリポジトリではサポートされていません。
* 実稼動のフルスタックパイプラインでプライベートリポジトリを使用する場合、Git タグは作成およびプッシュされません。
* Adobe GitHub アプリを GitHub 組織から削除すると、すべてのリポジトリのプルリクエスト検証機能が削除されます。
* プライベートリポジトリとコミット時のビルドトリガーを使用するパイプラインは、選択したブランチに新しいコミットがプッシュされた場合に自動的に開始されません。
* [アーティファクト再利用機能](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)は、プライベートリポジトリには適用されません。
* Cloud Manager の GitHub チェックを使用して、プルリクエストの検証を一時停止することはできません。
GitHub リポジトリが Cloud Manager で検証される場合、Cloud Manager は常に、そのリポジトリに対して作成されたプルリクエストの検証を試みます。
