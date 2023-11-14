---
title: Cloud Manager での独自の GitHub リポジトリーの操作
description: 独自の GitHub リポジトリを操作するように Cloud Manager を設定する方法について説明します。
feature: Release Information
source-git-commit: 8d689ea08ab7caf9cb0fa84df23d7e0fd906f379
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 1%

---


# Cloud Manager での独自の GitHub リポジトリーの操作 {#byo-github}

独自の GitHub リポジトリと連携するように Cloud Manager を設定することで、Cloud Manager を通じて GitHub リポジトリ内で直接コードを検証でき、コードをAdobeリポジトリと一貫して同期する必要がなくなります。

>[!NOTE]
>
>この機能は、次の場合にのみ使用できます。 [アーリーアダプタープログラム。](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## 設定 {#configuration}

設定は、次の 2 つの主な手順で構成されます。

1. [リポジトリを追加](#add-repo)
1. [プライベートリポジトリの所有権の検証](#validate-ownership)

### リポジトリーを追加 {#add-repo}

1. Cloud Manager で、 **プログラムの概要** ページ、タップまたはクリック **リポジトリ** タブをクリックして、 **リポジトリ** ページを開き、をクリックします。 **リポジトリを追加**.

1. Adobe Analytics の **リポジトリを追加** ダイアログ、選択 **プライベートリポジトリ** をリポジトリタイプとして使用します。

1. リポジトリの詳細を指定します

   * **リポジトリ名**  — 表現名
   * **リポジトリ URL**  — リポジトリの URL（で終わる必要があります） `.git`
   * **説明** （オプション） — 必要に応じてリポジトリの長い説明

   ![独自のリポジトリを追加](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. 「**保存**」して閉じるをタップまたはクリックします。

>[!TIP]
>
>Cloud Manager でのリポジトリ管理について詳しくは、このドキュメントを参照してください。 [Cloud Manager リポジトリーを参照してください。](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md)

### プライベートリポジトリの所有権の検証 {#validate-ownership}

Cloud Manager は GitHub リポジトリについて認識しますが、アクセスする必要があります。 アクセス権を付与するには、AdobeGitHub アプリをインストールし、指定したリポジトリを所有していることを確認する必要があります。

1. 独自のリポジトリを追加した後、 **プライベートリポジトリの所有権の検証** ダイアログが開きます。

   ![プライベートリポジトリの所有権の検証](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

1. Cloud Manager では、GitHub アプリを使用して、リポジトリと安全にやり取りします。
   * GitHub 組織の所有者が、次の場所にあるアプリをインストールする必要があります。 `https://github.com/apps/cloud-manager-for-aem-stage` リポジトリへのアクセス権を付与します。
   * この処理の詳細については、GitHub のドキュメントを参照してください。

1. セキュリティを強化するには、リポジトリのデフォルトブランチにシークレットファイルを作成する必要があります。 タップまたはクリック **生成**.

1. 「 」をタップまたはクリックして、秘密鍵ファイルの生成を確認します。 **確認**.

   ![秘密鍵の生成を確認](/help/implementing/cloud-manager/assets/repos/confirm-generation.png)

1. 戻る **プライベートリポジトリの所有権の検証** ウィンドウが開いたら、Cloud Manager が、プライベートファイルのコンテンツを **秘密のファイルコンテンツ** フィールドに入力します。 そのフィールドからコンテンツをコピーします。

   * シークレットファイルの内容は 1 回だけ表示されます。 このウィンドウを閉じる前にコンテンツをコピーしない場合は、秘密鍵を再生成する必要があります。

   ![秘密鍵ファイルの内容をコピー](/help/implementing/cloud-manager/assets/repos/new-secret.png)

1. GitHub リポジトリのデフォルトブランチ ( ) に、という名前の新しいファイルを作成します。 `.well-known/adobe/cloud-manager-challenge` をクリックし、そのファイルに秘密のファイルの内容を貼り付けて保存します。

1. アプリケーションがインストールされ、リポジトリにシークレットファイルが存在したら、をタップまたはクリックできます **検証** （内） **プライベートリポジトリの所有権の検証** ダイアログ。

デスクトップアプリケーションは任意の順序でインストールでき、シークレットファイルを作成できます。 ただし、検証する前に、両方の手順を完了する必要があります。

検証されるまで、リポジトリは赤いアイコンで表示され、まだ検証されておらず、まだ使用できないことを示します。

![未検証のリポジトリ](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

なお、 **タイプ** 列は、Adobeが提供するリポジトリ (**Adobe**) と独自の GitHub リポジトリ (**GitHub**) をクリックします。

検証を完了するために後でリポジトリに戻る必要がある場合は、 **リポジトリ** ページで、追加した GitHub リポジトリを表す行の省略記号ボタンをタップまたはクリックし、「 」を選択します。 **所有権の検証** を選択します。

## Cloud Manager での独自の GitHub リポジトリの使用 {#using}

Cloud Manager で GitHub リポジトリの検証が完了すると、統合が完了し、リポジトリを Cloud Manager で使用できます。

1. プルリクエストを作成すると、GitHub チェックが自動的に開始します。

   ![GitHub のチェック](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. プル要求ごとに、 [フルスタックコード品質パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) が自動的に作成されます。 このパイプラインは、プルリクエストの更新のたびに開始されます。

1. GitHub チェックは、コード品質チェックが完了するまで、実行状態のままです。 コード品質の結果が GitHub チェックに反映されます。

   ![GitHub コード品質チェック](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

プルリクエストが閉じられるかマージされると、作成された完全なスタックコード品質パイプラインが自動的に削除されます。

## 制限事項 {#limitations}

独自の GitHub リポジトリを Cloud Manager で使用する際は、次の制限事項に注意してください。

* GitHub リポジトリを、管理するパイプラインの直接リポジトリソースとして使用することはできません。
   * この機能は、予定されています。
* Cloud Manager の GitHub チェックを使用して、プル要求の検証を一時停止することはできません。
   * GitHub リポジトリが Cloud Manager で検証されている場合、Cloud Manager は常にそのリポジトリ用に作成されたプル要求を検証しようとします。
AdobeGitHub アプリが GitHub 組織から削除されると、すべてのリポジトリのプルリクエスト検証機能が削除されます。
