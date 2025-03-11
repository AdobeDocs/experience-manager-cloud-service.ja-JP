---
title: Cloud Managerでの外部リポジトリーの追加 – 限定ベータ版
description: Cloud Manager に外部リポジトリを追加する方法について説明します。Cloud Managerは、GitHub Enterprise Server、GitLab、Bitbucket リポジトリとの統合をサポートしています。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: aebda813-2eb0-4c67-8353-6f8c7c72656c
source-git-commit: bfa059ed4e3f04ae6ee1e07910edc62635b03e5a
workflow-type: tm+mt
source-wordcount: '1597'
ht-degree: 44%

---

# Cloud Managerでの外部リポジトリーの追加 – 限定ベータ版 {#external-repositories}

Cloud Manager に外部リポジトリを追加する方法について説明します。Cloud Managerは、GitHub Enterprise Server、GitLab、Bitbucket リポジトリとの統合をサポートしています。

>[!NOTE]
>
>この機能は、早期導入プログラムを通じてのみ使用できます。詳細と早期導入者としての新規登録について詳しくは、[独自の Git の導入 - GitLab と Bitbucket をサポートするようになりました](/help/implementing/cloud-manager/release-notes/2024/2024-10-0.md#gitlab-bitbucket)を参照してください。

## 外部リポジトリの設定

Cloud Manager での外部リポジトリの設定は、次の 3 つの手順で構成されます。

1. 選択したプログラムに[外部リポジトリを追加](#add-external-repo)します。
1. 外部リポジトリへのアクセストークンを指定します。
1. プライベート GitHub リポジトリの所有権の検証。



## 外部リポジトリの追加 {#add-ext-repo}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、外部リポジトリをリンクするプログラムを選択します。

1. サイドメニューの **サービス** で、![ フォルダーの概要アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg)**リポジトリ** をクリックします。

   ![リポジトリページ](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. **リポジトリ**&#x200B;ページの右上隅付近にある「**リポジトリを追加**」をクリックします。

1. **リポジトリを追加**&#x200B;ダイアログボックスで、外部の Git リポジトリをプログラムにリンクする「**プライベートリポジトリ**」を選択します。

   ![独自のリポジトリの追加](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. 各フィールドに、リポジトリに関する次の詳細を入力します。

   | フィールド | 説明 |
   | --- | --- |
   | **リポジトリ名** | 必須。新しいリポジトリのわかりやすい名前。 |
   | **リポジトリ URL** | 必須。リポジトリの URL。<br><br>GitHub でホストされているリポジトリを使用している場合は、パスの末尾を `.git` にする必要があります。<br>例：*`https://github.com/org-name/repo-name.git`*（URL パスは説明用です）。<br><br>外部リポジトリを使用している場合は、次の URL パス形式を使用する必要があります。<br>`https://git-vendor-name.com/org-name/repo-name.git`<br> または <br>`https://self-hosted-domain/org-name/repo-name.git`<br>。Git ベンダーと一致させる必要があります。 |
   | **リポジトリタイプを選択** | 必須。使用するリポジトリタイプを選択します。<ul><li>**GitHub** （GitHub Enterprise Server および GitHub のセルフホストバージョン）</li><li>**GitLab** （`gitlab.com` と GitLab のセルフホストバージョンの両方） </li><li>**Bitbucket** （`bitbucket.org` と Bitbucket サーバーの両方、および Bitbucket の自己ホストバージョン）</li></ul>上記のリポジトリ URL パスに GitLab や Bitbucket などの Git ベンダー名が含まれている場合、リポジトリタイプは既に事前に選択されています。 |
   | **説明** | オプション。リポジトリの詳細な説明です。 |

1. 「**保存**」を選択して、リポジトリを追加します。

1. **プライベートリポジトリの所有権の検証**&#x200B;ダイアログボックスで、外部リポジトリの所有権を検証し、アクセスできるようにするアクセストークンを指定します。

   ![リポジトリの既存のアクセストークンの選択](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *Bitbucket リポジトリの既存のアクセストークンの選択。*

   | トークンタイプ | 説明 |
   | --- | --- |
   | **既存のアクセストークンを使用** | 組織にリポジトリアクセストークンを既に指定し、複数のリポジトリにアクセスできる場合は、既存のトークンを選択できます。**トークン名**&#x200B;ドロップダウンリストを使用して、リポジトリに適用するトークンを選択します。それ以外の場合は、新しいアクセストークンを追加します。 |
   | **新しいアクセストークンを追加** | **リポジトリタイプ：GitHub**<br>• 「**トークン名**」テキストフィールドに、作成するアクセストークンの名前を入力します。<br>• [GitHub ドキュメント](https://docs.github.com/ja/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)の指示に従って、個人アクセストークンを作成します。<br>・必要な権限については、次の情報を参照してください。![GitHub の新しい PAT の作成 ](/help/implementing/cloud-manager/managing-code/assets/webhook-github-enterprise-server.png)<br>・・ **アクセストークン** フィールドに、作成したトークンを貼り付けます。 |
   |  | **リポジトリタイプ：GitLab**<br>• 「**トークン名**」テキストフィールドに、作成するアクセストークンの名前を入力します。<br>• [GitLab ドキュメント](https://docs.gitlab.com/user/profile/personal_access_tokens/)の指示に従って、個人アクセストークンを作成します。<br>・必要な権限については、次の情報を参照してください。![GitLab の新しい PAT を作成する ](/help/implementing/cloud-manager/managing-code/assets/webhook-gitlab.png)<br>・ **アクセストークン** フィールドに、作成したトークンを貼り付けます。 |
   |  | **リポジトリタイプ：Bitbucket**<br>• 「**トークン名**」テキストフィールドに、作成するアクセストークンの名前を入力します。<br>• [Bitbucket ドキュメント](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/)を使用して、リポジトリアクセストークンを作成します。<br>・必要な権限については、次の情報を参照してください ![Bitbucket の新しい PAT の作成 ](/help/implementing/cloud-manager/managing-code/assets/webhook-bitbucket.png)。 |

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

## 外部リポジトリの Webhook の設定 {#configure-webhook}

Cloud Managerでは、追加した外部 Git リポジトリの Webhook を設定できます。 [ 外部リポジトリの追加 ](#add-ext-repo) を参照してください。 これらの Webhook により、Cloud Managerは、Git ベンダーソリューション内の様々なアクションに関連するイベントを受け取ることができます。

例えば、Webhook を使用すると、Cloud Managerは、次のようなイベントに基づいてアクションをトリガー設定できます。

* プルリクエスト（PR）の作成 – PR 検証機能を開始します。
* プッシュイベント – 「Git コミット時」トリガーがオン（有効）になるとパイプラインを開始します。
* 今後のコメントベースのアクション - PR から迅速な開発環境（RDE）への直接デプロイメントなどのワークフローを可能にします。

Cloud Managerは GitHub アプリを介して直接統合されるので、`GitHub.com` でホストされるリポジトリには Webhook 設定は必要ありません。
アクセストークンを使用してオンボードされるその他すべての外部リポジトリ（GitHub Enterprise Server、GitLab、Bitbucket など）では、Webhook 設定を使用できるので、手動で設定する必要があります。

**外部リポジトリの Webhook を設定するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、外部 Git リポジトリの Webhook を設定するプログラムを選択します。

1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左サイドメニューを表示します。

1. 左側のメニューの「**プログラム**」見出しの下の「![ フォルダーアウトラインアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg)**リポジトリ**」をクリックします。

1. **リポジトリ** ページで、「**タイプ**」列を使用して選択をガイドし、必要なリポジトリを見つけて、その横にある ![ 省略記号 – 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

   ![ 選択したリポジトリーのドロップダウンメニューの「設定 Webhook」オプション ](/help/implementing/cloud-manager/managing-code/assets/repository-config-webhook.png)

1. ドロップダウンメニューから、「**Config Webhook**」をクリックします。

   ![Webhook を設定ダイアログボックス ](/help/implementing/cloud-manager/managing-code/assets/config-webhook.png)

1. **Config Webhook** ダイアログボックスで、次の操作を行います。

   1. 「**Webhook URL**」フィールドの横にある「![ コピーアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)」をクリックします。
URL をプレーンテキストファイルに貼り付けます。 コピーした URL は、Git ベンダーの Webhook 設定に必要です。
   1. 「**Webhook 秘密鍵** トークン/キー」フィールドの横にある「**生成**」をクリックし、![ コピーアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) をクリックします。
秘密鍵をプレーンテキストファイルに貼り付けます。 コピーした秘密鍵は、Git ベンダーの Webhook 設定に必要です。
1. 「**閉じる**」をクリックします。
1. Git ベンダーソリューション（GitHub Enterprise、GitLab、Bitbucket）に移動します。

   Webhook 設定と各ベンダーに必要なイベントのすべての詳細は、[ 外部リポジトリの追加 ](#add-ext-repo) を参照してください。 手順 8 の下で、表を参照してください。

1. ソリューションの **Webhook** 設定セクションを見つけます。
1. 前の手順でコピーした Webhook URL を「URL」テキストフィールドに貼り付けます。
   1. Webhook URL の `api_key` クエリパラメーターを独自の実際の API キーに置き換えます。

      API キーを生成するには、Adobe Developer Consoleで統合プロジェクトを作成する必要があります。 詳しくは [API 統合プロジェクトの作成 ](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/) を参照してください。

1. 前にコピーした Webhook 秘密鍵を **秘密鍵** （または **秘密鍵**、または **秘密鍵トークン**）テキストフィールドに貼り付けます。
1. Webhook を設定して、Cloud Managerが想定する適切なイベントを送信します。


### Webhook を使用したプルリクエストの検証

Webhook が正しく設定されると、Cloud Managerは自動的に、リポジトリに対するパイプライン実行または PR 検証チェックをトリガーします。

次の動作が適用されます。

* **GitHub エンタープライズサーバー**

  チェックを作成すると、次のスクリーンショットのように表示されます。 `GitHub.com` との主な違いは、`GitHub.com` がチェック実行を使用するのに対して、GitHub Enterprise Server （個人用アクセストークンを使用）はコミットステータスを生成することです。

  ![GitHub Enterprise Server で PR 検証プロセスを示すコミットステータス ](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-github-pr-validation.png)

* **Bitbucket**

  コード品質検証の実行中：

  ![ コード品質検証の実行中のステータス ](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket1.png)

  PR 検証の進捗の追跡にコミットステータスを使用します。 次の場合、スクリーンショットは、お客様の問題が原因でコード品質の検証に失敗した場合の動作を示しています。 詳細なエラー情報を含んだコメントが追加され、コミットチェックが作成されます。このチェックでは、失敗が示されます（右側に表示）。

  ![Bitbucket のプルリクエスト検証ステータス ](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket2.png)

* **GitLab**

  GitLab のやり取りは、コメントにのみ依存します。 検証が開始されると、コメントが追加されます。 検証が完了（成功または失敗）すると、最初のコメントが削除され、検証結果やエラーの詳細を含む新しいコメントに置き換えられます。

  コード品質検証の実行中：

  ![ コード品質検証が実行中の場合 ](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab1.png)

  コールド品質の検証が終了した場合：

  ![ コールド品質の検証が完了したとき ](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab2.png)

  コード品質検証が次のエラーで失敗した場合：

  ![ エラーでコード品質検証が失敗した場合 ](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab3.png)

  お客様の問題が原因でコード品質の検証に失敗した場合：

  ![ お客様の問題が原因でコード品質の検証に失敗した場合 ](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab4.png)


## Webhook の問題のトラブルシューティング

* Webhook URL に有効な API キーが含まれていることを確認してください。
* Git ベンダー設定で Webhook イベントが正しく設定されていることを確認します。
* PR 検証またはパイプライントリガーが機能しない場合は、Cloud Managerと Git ベンダーの両方で Webhook の秘密鍵が最新であることを確認してください。








## 制限事項

* 外部リポジトリは、設定パイプラインにリンクできません。
* 外部リポジトリ（GitHub でホストされていない）を使用したパイプラインと「Git 変更時」トリガーは自動的には開始されません。これらは手動でのみ開始できます。


<!-- THIS BULLET REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release. THEY CAN NOW START AUTOMATICALLY>
* Pipelines using external repositories (excluding GitHub-hosted repositories) and the **Deployment Trigger** option [!UICONTROL **On Git Changes**], triggers are not automatically started. They must be manually started. -->


