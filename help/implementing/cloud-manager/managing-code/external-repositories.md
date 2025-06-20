---
title: Cloud Manager での外部リポジトリの追加
description: Cloud Manager に外部リポジトリを追加する方法について説明します。Cloud Manager は、GitHub Enterprise、GitLab、Bitbucket、 Azure DevOps リポジトリとの統合をサポートしています。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="プライベートベータ版" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
exl-id: aebda813-2eb0-4c67-8353-6f8c7c72656c
source-git-commit: 26892959443a16203184f4a0798d9c7fdc75dd8f
workflow-type: tm+mt
source-wordcount: '2292'
ht-degree: 90%

---

# Cloud Manager での外部リポジトリの追加 {#external-repositories}

Cloud Manager に外部リポジトリを追加する方法について説明します。Cloud Manager は、GitHub Enterprise、GitLab、Bitbucket リポジトリとの統合をサポートしています。

また、Azure DevOps Git リポジトリを Cloud Manager にオンボードできるようになりました。これは、最新の Azure DevOps リポジトリとレガシー VSTS（Visual Studio Team Services）リポジトリの両方に対応しています。

* Edge Delivery Services のユーザーは、オンボードされたリポジトリを使用して、サイトコードを同期およびデプロイできます。
* AEM as a Cloud Service および Adobe Managed Services（AMS）のユーザーは、リポジトリをフルスタックパイプラインとフロントエンドパイプラインの両方にリンクできます。

>[!NOTE]
>
>この記事で説明する機能は、非公開のベータ版プログラムでのみ使用できます。 詳細およびプライベートベータ版にサインアップするには、[ 独自の Git の取り込み ](/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket) を参照してください。


## 外部リポジトリの設定

Cloud Manager での外部リポジトリの設定は、次の手順で構成されます。

1. 選択したプログラムへの [ 外部リポジトリの追加 ](#add-external-repo)
1. [検証済みの外部リポジトリのパイプラインへのリンク](#validate-ext-repo)
   <!-- 1. Provide an access token to the external repository.
    1. Validate ownership of the private GitHub repository. -->
1. 外部リポジトリに [webhook を設定](#configure-webhook)します。


## 外部リポジトリの追加 {#add-ext-repo}

>[!NOTE]
>
>外部リポジトリは、設定パイプラインにリンクできません。

<!-- THIS BULLET REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release. THEY CAN NOW START AUTOMATICALLY>
* Pipelines using external repositories (excluding GitHub-hosted repositories) and the **Deployment Trigger** option [!UICONTROL **On Git Changes**], triggers are not automatically started. They must be manually started. -->


1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、外部リポジトリをリンクするプログラムを選択します。

1. サイドメニューの&#x200B;**プログラム**&#x200B;で、![フォルダーアウトラインアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **リポジトリ**&#x200B;をクリックします。

   ![リポジトリページ](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. **リポジトリ**&#x200B;ページの右上隅付近にある「**リポジトリを追加**」をクリックします。

1. **リポジトリを追加**&#x200B;ダイアログボックスで、外部の Git リポジトリをプログラムにリンクする「**プライベートリポジトリ**」を選択します。

   ![独自のリポジトリの追加](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. 各フィールドに、リポジトリに関する次の詳細を入力します。

   | フィールド | 説明 |
   | --- | --- |
   | **リポジトリ名** | 必須。新しいリポジトリのわかりやすい名前。 |
   | **リポジトリ URL** | 必須。リポジトリの URL。<br><br>GitHub でホストされているリポジトリを使用している場合は、パスの末尾を `.git` にする必要があります。<br>例：*`https://github.com/org-name/repo-name.git`*（URL パスは説明用です）。<br><br>外部リポジトリを使用している場合は、次の URL パス形式を使用する必要があります。<br>`https://git-vendor-name.com/org-name/repo-name.git`<br> または <br>`https://self-hosted-domain/org-name/repo-name.git`<br>。Git ベンダーと一致させる必要があります。 |
   | **リポジトリタイプを選択** | 必須。使用するリポジトリタイプを選択します。リポジトリ URL パスに GitLab や Bitbucket などの Git ベンダー名が含まれている場合、リポジトリタイプは既に事前に選択されています。：<ul><li>**GitHub**（GitHub Enterprise と自己ホスト型バージョンの GitHub）</li><li>**GitLab**（`gitlab.com` と自己ホスト型バージョンの GitLab の両方） </li><li>**Bitbucket**（`bitbucket.org`（クラウドバージョン））のみがサポートされています。Bitbucket の自己ホスト型バージョンは、2024年2月15日（PT）以降に非推奨（廃止予定）になりました。）</li><li>**Azure DevOps**（`dev.azure.com`） </ul> |
   | **説明** | オプション。リポジトリの詳細な説明です。 |

1. 「**保存**」を選択して、リポジトリを追加します。

   次に、外部リポジトリの所有権を検証するアクセストークンを提供します。

1. **プライベートリポジトリ所有権検証** ダイアログボックスで、外部リポジトリの所有権を検証してアクセスできるようにするためのアクセストークンを指定し、「**検証**」をクリックします。

   ![リポジトリの既存のアクセストークンの選択](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *Bitbucket リポジトリ用の既存のアクセストークンの選択（説明用のみ）*

>[!BEGINTABS]

>[!TAB GitHub Enterprise]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/github -->

| アクセストークンオプション | 説明 |
| --- | --- |
| **既存のアクセストークンを使用** | 組織にリポジトリアクセストークンを既に指定し、複数のリポジトリにアクセスできる場合は、既存のトークンを選択できます。**トークン名**&#x200B;ドロップダウンリストを使用して、リポジトリに適用するトークンを選択します。それ以外の場合は、新しいアクセストークンを追加します。 |
| **新しいアクセストークンを追加** | <ul><li> 「**トークン名**」テキストフィールドに、作成するアクセストークンの名前を入力します。<li>[GitHub ドキュメント](https://docs.github.com/ja/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)の指示に従って、個人アクセストークンを作成します。<li>GitHub Enterprise 個人アクセストークン（PAT）に必須の権限<br>これらの権限により、Cloud Manager でプルリクエストの検証、コミットステータスチェックの管理、必要なリポジトリ詳細へのアクセスが可能になります。<br>GitHub Enterprise で PAT を生成する場合は、次のリポジトリ権限が含まれていることを確認します。<ul><li>プルリクエスト（読み取りおよび書き込み）<li>コミットステータス（読み取りおよび書き込み）<li>リポジトリメタデータ（読み取り専用）</li></li></ul></li></ul></ul></ul><ul><li>「**アクセストークン**」フィールドに、作成したトークンをペーストします。 |

検証後、外部リポジトリを使用してパイプラインにリンクする準備が整います。

[ アクセストークンの管理 ](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md) も参照してください。

>[!TAB GitLab]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/gitlab -->

| アクセストークンオプション | 説明 |
| --- | --- |
| **既存のアクセストークンを使用** | 組織にリポジトリアクセストークンを既に指定し、複数のリポジトリにアクセスできる場合は、既存のトークンを選択できます。**トークン名**&#x200B;ドロップダウンリストを使用して、リポジトリに適用するトークンを選択します。それ以外の場合は、新しいアクセストークンを追加します。 |
| **新しいアクセストークンを追加** | <ul><li>「**トークン名**」テキストフィールドに、作成するアクセストークンの名前を入力します。<li>[GitLab ドキュメント](https://docs.gitlab.com/user/profile/personal_access_tokens/)の指示に従って、個人アクセストークンを作成します。<li>GitLab 個人アクセストークン（PAT）に必須の権限<br>これらのスコープにより、Cloud Manager で検証と webhook 統合の必要に応じてリポジトリデータとユーザー情報へのアクセスが可能になります。<br>GitLab で PAT を生成する場合、次のトークンスコープが含まれていることを確認します。<ul><li>api<li>read_user</li></li></ul></li></li></ul></ul></ul><ul><li>「**アクセストークン**」フィールドに、作成したトークンをペーストします。 |

検証後、外部リポジトリを使用してパイプラインにリンクする準備が整います。

[ アクセストークンの管理 ](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md) も参照してください。

>[!TAB Bitbucket]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/bitbucket -->

| アクセストークンオプション | 説明 |
| --- | --- |
| **既存のアクセストークンを使用** | 組織にリポジトリアクセストークンを既に指定し、複数のリポジトリにアクセスできる場合は、既存のトークンを選択できます。**トークン名**&#x200B;ドロップダウンリストを使用して、リポジトリに適用するトークンを選択します。それ以外の場合は、新しいアクセストークンを追加します。 |
| **新しいアクセストークンを追加** | <ul><li>「**トークン名**」テキストフィールドに、作成するアクセストークンの名前を入力します。<li>[Bitbucket ドキュメント](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/)を使用して、リポジトリアクセストークンを作成します。<li>Bitbucket 個人アクセストークン（PAT）に必須の権限<br>これらの権限により、Cloud Manager でリポジトリコンテンツへのアクセス、プルリクエストの管理、webhook イベントの構成または反応が可能になります。<br>Bitbucket でアプリパスワードを作成する場合は、次の必須のアプリパスワード権限が含まれていることを確認します。<ul><li>リポジトリ（読み取り専用）<li>プルリクエスト（読み取りおよび書き込み）<li>webhook（読み取りおよび書き込み）</li></li></ul></li></li></ul></ul></ul><ul><li>「**アクセストークン**」フィールドに、作成したトークンをペーストします。 |

検証後、外部リポジトリを使用してパイプラインにリンクする準備が整います。

[ アクセストークンの管理 ](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md) も参照してください。

>[!TAB Azure DevOps]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/azure_devops -->

| アクセストークンオプション | 説明 |
| --- | --- |
| **既存のアクセストークンを使用** | 組織にリポジトリアクセストークンを既に指定し、複数のリポジトリにアクセスできる場合は、既存のトークンを選択できます。**トークン名**&#x200B;ドロップダウンリストを使用して、リポジトリに適用するトークンを選択します。それ以外の場合は、新しいアクセストークンを追加します。 |
| **新しいアクセストークンを追加** | <ul><li>「**トークン名**」テキストフィールドに、作成するアクセストークンの名前を入力します。<li>[Azure DevOps ドキュメント](https://learn.microsoft.com/ja-jp/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=Windows)を使用して、リポジトリアクセストークンを作成します。<li>Azure DevOps 個人アクセストークン（PAT）に必須の権限。<br>これらの権限により、Cloud Manager でリポジトリコンテンツへのアクセス、プルリクエストの管理、webhook イベントを構成または反応できるようになります。<br>Azure DevOps でアプリパスワードを作成する場合は、次の必須のアプリパスワード権限が含まれていることを確認します。<ul><li>リポジトリ（読み取り専用）</li></ul></li></li></ul></ul></ul><ul><li>「**アクセストークン**」フィールドに、作成したトークンをペーストします。 |

検証後、外部リポジトリを使用してパイプラインにリンクする準備が整います。

[ アクセストークンの管理 ](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md) も参照してください。

>[!ENDTABS]


## 検証済みの外部リポジトリのパイプラインへのリンク {#validate-ext-repo}

1. 次のように、パイプラインを追加または編集します。
   * [実稼動パイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [実稼動以外のパイプラインの追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [パイプラインの編集](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

   <!-- Add an Edge Delivery Pipeline -->

   ![パイプラインのソースコードリポジトリと Git 分岐](/help/implementing/cloud-manager/managing-code/assets/pipeline-repo-gitbranch.png)
   *選択したリポジトリと Git 分岐を含む実稼動以外のパイプラインを追加ダイアログボックス。*

1. パイプラインの追加または編集時に、新しいパイプラインまたは既存のパイプラインの&#x200B;**ソースコード**&#x200B;の場所を指定するには、**リポジトリ**&#x200B;ドロップダウンリストから使用する外部リポジトリを選択します。

1. **Git 分岐**&#x200B;ドロップダウンリストで、パイプラインのソースとして分岐を選択します。

1. 「**保存**」をクリックします。


>[!TIP]
>
>Cloud Manager でのリポジトリ管理について詳しくは、[Cloud Manager リポジトリ](/help/implementing/cloud-manager/managing-code/managing-repositories.md)を参照してください。


## 外部リポジトリの webhook の設定 {#configure-webhook}

Cloud Manager では、追加した外部 Git リポジトリの webhook を設定できます。詳しくは、[外部リポジトリの追加](#add-ext-repo)を参照してください。これらの webhook により、Cloud Manager は Git ベンダーソリューション内の様々なアクションに関連するイベントを受信できます。

例えば、webhook を使用すると、Cloud Manager は次のようなイベントに基づいてアクションをトリガーできます。

* プルリクエスト（PR）の作成 - PR 検証機能を開始します。
* プッシュイベント -「Git コミット時」トリガーがオン（有効）になると、パイプラインを開始します。
* 今後のコメントベースのアクション - PR から高速開発環境（RDE）への直接デプロイメントなどのワークフローを可能にします。

Cloud Manager は GitHub アプリを通じて直接統合されるので、`GitHub.com` でホストされているリポジトリでは webhook 設定は必要ありません。

アクセストークン（GitHub Enterprise、GitLab、Bitbucket、Azure DevOps など）でオンボードされているその他すべての外部リポジトリの場合、Webhook 設定を使用できるので、手動で設定する必要があります。

**外部リポジトリの webhook を設定するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、外部 Git リポジトリの webhook を設定するプログラムを選択します。

1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左サイドメニューを表示します。

1. 左側のサイドメニューの&#x200B;**プログラム**&#x200B;見出しで、![フォルダーアウトラインアイコ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **リポジトリ**&#x200B;をクリックします。

1. **リポジトリ**&#x200B;ページで、**タイプ**&#x200B;列を使用して選択し、必要なリポジトリを見つけて、その横にある ![省略記号 - その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

   ![ 選択したリポジトリのドロップダウンメニューの「Webhook を設定」オプション](/help/implementing/cloud-manager/managing-code/assets/repository-config-webhook.png)

1. ドロップダウンメニューから、「**Webhook を設定**」をクリックします。

   ![Webhook を設定ダイアログボックス](/help/implementing/cloud-manager/managing-code/assets/config-webhook.png)

1. **Webhook を設定**&#x200B;ダイアログボックスで、次の操作を行います。

   1. 「**Webhook URL**」フィールドの横にある ![コピーアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) をクリックします。
URL をプレーンテキストファイルにペーストします。コピーした URL は、Git ベンダーの webhook 設定に必要です。
   1. 「**Webhook 秘密鍵**&#x200B;トークン／キー」フィールドの横にある「**生成**」をクリックし、![コピーアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) をクリックします。
秘密鍵をプレーンテキストファイルにペーストします。コピーした秘密鍵は、Git ベンダーの webhook 設定に必要です。
1. 「**閉じる**」をクリックします。
1. Git ベンダーソリューション（GitHub Enterpriser、GitLab、Bitbucket、Azure DevOps）に移動します。

   各ベンダーに必要な web フック設定とイベントについて詳しくは、[外部リポジトリの追加](#add-ext-repo)を参照してください。手順 8 の下で、タブ付き表を参照してください。

1. ソリューションの **webhook** 設定セクションを見つけます。
1. 前の手順でコピーした webhook URL を「URL」テキストフィールドにペーストします。
   1. Webhook URL の `api_key` クエリパラメーターを独自の実際の API キーに置き換えます。

      API キーを生成するには、Adobe Developer Console で統合プロジェクトを作成する必要があります。詳しくは、[API 統合プロジェクトの作成](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)を参照してください。

1. 前の手順でコピーした webhook 秘密鍵を「**秘密鍵**」（または「**秘密鍵**」、あるいは「**秘密鍵トークン**」）テキストフィールドにペーストします。
1. Webhook を設定して、Cloud Managerが必要とするイベントを送信します。 次の表を使用して、Git プロバイダーの正しいイベントを判断します。

>[!BEGINTABS]

>[!TAB GitHub Enterprise]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/github -->

| 必須の webhook イベント |
| --- |
| これらのイベントにより、Cloud Manager でプルリクエストの検証、パイプラインのプッシュベースのトリガー、Edge Delivery Services のコード同期などの GitHub アクティビティに応答できます。<br>次の必須の webhook イベントで webhook がトリガーするように設定されていることを確認します。<ul><li>プルリクエスト<li>プッシュ<li>コメントを発行</li></li></li></ul></ul></ul> |

>[!TAB GitLab]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/gitlab -->

| 必須の webhook イベント |
| --- |
| これらの webhook イベントにより、コードをプッシュした際や結合リクエストを送信した際に、Cloud Manager でパイプラインをトリガーできます。また、プルリクエストの検証に関連するコメントも（メモイベントを通じて）追跡します。<br>次の必須の webhook イベントで webhook がトリガーするように設定されていることを確認します。<ul><li>プッシュイベント<li>結合リクエストイベント<li>メモイベント</li></li></li></ul></ul></ul> |

>[!TAB Bitbucket]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/bitbucket -->

| 必須の webhook イベント |
| --- |
| これらのイベントにより、Cloud Manager でプルリクエストの検証、コードプッシュへの応答、パイプライン調整用のコメントでのやり取りが可能になります。<br>次の必須の webhook イベントで webhook がトリガーするように設定されていることを確認します。<ul><li>プルリクエスト：作成済み<li>プルリクエスト：更新済み<li>プルリクエスト：結合済み<li>プルリクエスト：コメント<li>リポジトリ：プッシュ</li></li></li></ul></ul></ul> |

>[!TAB Azure DevOps]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/azure_devops -->

| 必須の webhook イベント |
| --- |
| これらのイベントにより、Cloud Manager でプルリクエストの検証、コードプッシュへの応答、パイプライン調整用のコメントでのやり取りが可能になります。<br>次の必須の webhook イベントで webhook がトリガーするように設定されていることを確認します。<ul><li>リポジトリ：プッシュ</li></li></ul></ul></ul> |

>[!ENDTABS]


### Webhook を使用したプルリクエストの検証

Webhook を正しく設定すると、Cloud Manager ではリポジトリに対するパイプライン実行または PR 検証チェックを自動的にトリガーします。

以下に説明するように、動作は使用する Git プロバイダーによって異なります。

>[!BEGINTABS]


>[!TAB GitHub Enterprise]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/github -->

チェックを作成すると、次のスクリーンショットのように表示されます。`GitHub.com` との主な違いは、`GitHub.com` はチェック実行を使用するのに対して、GitHub Enterprise（個人用アクセストークンを使用）はコミットステータスを生成することです。

![GitHub Enterprise で PR 検証プロセスを示すコミットステータス](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-github-pr-validation.png)


>[!TAB GitLab]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/gitlab -->

GitLab のインタラクションは、コメントにのみ依存します。検証を開始すると、コメントが追加されます。検証が完了すると（成功または失敗に関係なく）、最初のコメントは削除され、検証結果やエラーの詳細を含む新しいコメントに置き換えられます。

コード品質検証が実行中の場合：

![コード品質検証が実行中の場合](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab1.png)

コード品質検証が終了した場合：

![コード品質検証が終了した場合](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab2.png)

コード品質検証がエラーで失敗した場合：

![コード品質検証がエラーで失敗した場合](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab3.png)

コード品質検証が顧客の問題により失敗した場合：

![コード品質検証が顧客の問題により失敗した場合](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab4.png)


>[!TAB Bitbucket]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/bitbucket -->

コード品質検証が実行中の場合：

![コード品質検証が実行中のステータス](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket1.png)

PR 検証の進行状況のトラッキングにコミットステータスを使用します。次の場合、スクリーンショットは、コード品質検証がお客様の問題により失敗した場合の動作を示しています。詳細なエラー情報を含むコメントが追加され、失敗を示すコミットチェックが作成されます（右側に表示）。

![Bitbucket のプルリクエスト検証ステータス](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket2.png)



>[!ENDTABS]


## Web フックの問題のトラブルシューティング

* Web フック URL に有効な API キーが含まれていることを確認します。
* Git ベンダー設定で web フックイベントが正しく設定されていることを確認します。
* PR 検証またはパイプライントリガーが機能しない場合は、Cloud Manager と Git ベンダーの両方で web フックの秘密鍵が最新であることを確認します。


