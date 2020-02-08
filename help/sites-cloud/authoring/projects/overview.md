---
title: プロジェクト
description: プロジェクトを使用すると、リソースを 1 つのエンティティにグループ化でき、共通の共有環境でプロジェクトを簡単に管理できます
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# プロジェクト {#projects}

プロジェクトを使用すると、リソースを 1 つのエンティティにグループ化できます。共通の共有環境で、プロジェクトを簡単に管理できます。プロジェクトに関連付けることができるリソースのタイプは、AEM ではタイルと呼ばれます。Tiles may include project and team information, assets, workflows, and other types of information, as described in detail in [Project Tiles.](#project-tiles)

>[!CAUTION]
>
>For users in projects to see other users/groups while using Projects functionality like creating projects, creating tasks/workflows, seeing and managing the team, those users need to have read access on `/home/users` and `/home/groups`. The easiest way to implement this is to give the **projects-users** group read access to `/home/users` and `/home/groups`.

次の操作をおこなうことができます。

* プロジェクトの作成
* プロジェクトへのコンテンツフォルダーおよびアセットフォルダーの関連付け
* プロジェクトの削除
* コンテンツリンクのプロジェクトからの削除

次の追加トピックを参照してください。

* [プロジェクトの管理](/help/sites-cloud/authoring/projects/managing.md)
* [タスクの使用](/help/sites-cloud/authoring/projects/tasks.md)
* [プロジェクトワークフローの操作](/help/sites-cloud/authoring/projects/workflows.md)

## プロジェクトコンソール {#projects-console}

プロジェクトコンソールで、AEM 内のプロジェクトにアクセスし、管理します。

![プロジェクトコンソール](/help/sites-cloud/authoring/assets/projects-console.png)

* 「**タイムライン**」を選択してからプロジェクトを選択すると、プロジェクトのタイムラインが表示されます。
* 「**選択**」をクリックまたはタップすると、選択モードに入ります。
* 「**作成**」をクリックして、プロジェクトを追加します。
* 「**アクティブなプロジェクトを切り替え**」を使用して、すべてのプロジェクトとアクティブなプロジェクトのみを切り替えることができます。
* 「**統計ビューを表示**」を使用して、タスクの完了に関するプロジェクト統計を表示できます。

## プロジェクトタイル {#project-tiles}

プロジェクトを使用して、様々なタイプの情報とプロジェクトを関連付けることができます。このような情報は&#x200B;**タイル**&#x200B;と呼ばれます。各タイルと含まれる情報の種類について、このセクションで説明します。

以下のタイルをプロジェクトと関連付けることができます。それぞれについては、以降のセクションで説明します。

* アセットおよびアセットコレクション
* エクスペリエンス
* リンク
* プロジェクト情報
* チーム
* ランディングページ
* 電子メール
* ワークフロー
* ローンチ
* タスク

### アセット {#assets}

**アセット**&#x200B;タイルでは、特定のプロジェクトに使用するすべてのアセットを集めることができます。

![アセットタイル](/help/sites-cloud/authoring/assets/projects-assets-tile.png)

タイル内でアセットを直接アップロードします。さらに、ダイナミックメディアのアドオンがある場合は、画像セット、スピンセットまたは混在メディアセットを作成できます。

![画像セット](/help/sites-cloud/authoring/assets/projects-image-sets.png)

### アセットコレクション {#asset-collections}

アセットと同様に、アセットコレクションをプロジェクトに直接追加できます。You define collections in Assets. <!--Similar to assets, you can add [asset collections](/help/assets/managing-collections-touch-ui.md) directly to your project. You define collections in Assets.-->

![アセットの収集](/help/sites-cloud/authoring/assets/projects-asset-collections.png)

コレクションを追加するには、「**コレクションを追加**」をクリックし、適切なコレクションをリストから選択します。

### エクスペリエンス {#experiences}

**エクスペリエンス**&#x200B;タイルでは、モバイルアプリ、Web サイトまたは公開物をプロジェクトに追加できます。

![エクスペリエンス](/help/sites-cloud/authoring/assets/project-experiences.png)

アイコンが表しているエクスペリエンスの種類（Web サイト、モバイルアプリケーションまたは公開物）を示します。エクスペリエンスを追加するには、「+」記号をクリックするか、「**エクスペリエンスを追加**」をクリックして、エクスペリエンスの種類を選択します。

![エクスペリエンスの追加](/help/sites-cloud/authoring/assets/projects-add-experience.png)

サムネイルのパスを選択し、必要に応じてエクスペリエンスのサムネイルを変更します。Experiences are grouped together in the **Experiences** tile.

### リンク {#links}

リンクタイルでは、外部リンクとプロジェクトを関連付けることができます。

![リンク](/help/sites-cloud/authoring/assets/project-links.png)

リンクにわかりやすい名前を付けたり、サムネイルを変更したりできます。

![リンクを追加](/help/sites-cloud/authoring/assets/projects-add-link.png)

### プロジェクト情報 {#project-info}

プロジェクト情報タイルには、説明、プロジェクトステータス（非アクティブまたはアクティブ）、期限、メンバーなどプロジェクトに関する一般的な情報が表示されます。さらに、メインのプロジェクトページに表示されるプロジェクトサムネイルを追加できます。

![プロジェクト情報](/help/sites-cloud/authoring/assets/project-info.png)

チームタイルと同様に、このタイルからチームメンバーを割り当てたり、削除したり（または役割を変更したり）できます。

![プロジェクトへのチームメンバーの追加](/help/sites-cloud/authoring/assets/projects-add-team.png)

### 翻訳ジョブ {#translation-job}

翻訳ジョブタイルでは、翻訳を開始したり、翻訳のステータスを表示したりもできます。To set up your translation, see Creating Translation Projects. <!--To set up your translation, see [Creating Translation Projects](/help/assets/translation-projects.md).-->

![翻訳ジョブ](/help/sites-cloud/authoring/assets/projects-translation-job.png)

Click the ellipsis at the bottom of the **Translation Job** card to view the assets in the translation workflow. 翻訳ジョブリストには、アセットのメタデータとタグのエントリも表示されます。これらのエントリは、アセットのメタデータとタグも翻訳されることを意味します。

![翻訳ジョブの詳細](/help/sites-cloud/authoring/assets/projects-translation-job-detail.png)

### チーム {#team}

このタイルでは、プロジェクトチームのメンバーを指定できます。編集時に、チームメンバー名を入力して、ユーザーの役割を割り当てることができます。

![チームタイル](/help/sites-cloud/authoring/assets/projects-team-tile.png)

チームメンバーをチームに追加したり、チームから削除したりできます。In addition, you can edit the [user role](#user-roles-in-a-project) assigned to the team member.

![リストからチームを追加](/help/sites-cloud/authoring/assets/projects-add-team-list.png)

### ワークフロー {#workflows}

特定のワークフローに従うように、プロジェクトを割り当てることができます。動作しているワークフローがある場合、そのステータスがプロジェクトの&#x200B;**ワークフロー**&#x200B;タイルに表示されます。

![ワークフロー](/help/sites-cloud/authoring/assets/project-workflows.png)

特定のワークフローに従うように、プロジェクトを割り当てることができます。選択したプロジェクトに応じて、使用可能なワークフローは異なります。

使用可能なワークフローについては、[プロジェクトワークフローの操作](/help/sites-cloud/authoring/projects/workflows.md)で説明します。

### ローンチ {#launches}

ローンチタイルには、[ローンチをリクエストワークフロー](/help/sites-cloud/authoring/projects/workflows.md)を使用してリクエストされたローンチがすべて表示されます。

![ローンチ](/help/sites-cloud/authoring/assets/project-launches.png)

### タスク {#tasks}

タスクを使用して、ワークフローを含む、すべてのプロジェクト関連タスクのステータスを監視できます。Tasks are covered in detail at [Working with Tasks](/help/sites-cloud/authoring/projects/tasks.md).

![タスク](/help/sites-cloud/authoring/assets/projects-tasks.png)

## プロジェクトテンプレート {#project-templates}

AEMには、次の3種類のテンプレートがあらかじめ用意されています。

* 単純なプロジェクト — 他のカテゴリ（包括的）に適合しないプロジェクトのリファレンスサンプル。 3 つの基本的な役割（所有者、エディター、監視者）と 4 つのワークフロー（プロジェクト承認、ローンチをリクエスト、ランディングページをリクエスト、電子メールをリクエスト）が含まれます。
* メディアプロジェクト — メディア関連のアクティビティの参照サンプルプロジェクト。 いくつかのメディア関連プロジェクトの役割（フォトグラファー、エディター、コピーライター、デザイナー、所有者、監視者）が含まれます。また、メディアコンテンツに関連する2つのワークフロー(コピーのリクエスト（テキストのリクエストと確認）と製品撮影（製品関連の写真を管理するため）も含まれます。
* 翻訳プロジェクト - 翻訳関連アクティビティを管理するためのリファレンスサンプルです。3 つの基本的な役割（所有者、エディター、監視者）が含まれます。It includes two workflows that are accessed in the Workflows user interface. <!--* [A translation project](/help/sites-administering/translation.md) - A reference sample for managing translation related activities. It includes three basic roles (Owners, Editors, and Observers). It includes two workflows that are accessed in the Workflows user interface.-->

選択したテンプレートに基づいて、特にユーザーの役割とワークフローに関して使用可能なオプションは異なります。

## プロジェクト内のユーザーの役割 {#user-roles-in-a-project}

プロジェクトテンプレートでは様々なユーザーの役割を設定します。これらの役割は、主に次の目的に使用されます。

1. 権限。ユーザーの役割は、監視者、エディター、所有者という 3 つのカテゴリのいずれかに分類されます。例えば、写真家やコピーライターは編集者と同じ権限を持ちます。 権限によって、ユーザーがプロジェクト内のコンテンツに何をおこなえるかが決定されます。
1. ワークフロー管理。ワークフローによって、プロジェクト内のタスクに誰を割り当てるかが決定されます。タスクは、プロジェクトの役割に関連付けることができます。 例えば、タスクをフォトグラファーに割り当てると、フォトグラファーの役割を持つすべてのチームメンバーがそのタスクを取得します。

セキュリティと権限を管理するために、すべてのプロジェクトが以下のデフォルトの役割をサポートしています。

| ロール | 説明 | 権限 | グループのメンバーシップ |
|---|---|---|---|
| 監視者 | この役割のユーザーは、プロジェクトステータスなどプロジェクトの詳細を表示できます。 | プロジェクトに対する読み取り専用権限 | `workflow-users` group |
| 編集者 | この役割のユーザーは、プロジェクトのコンテンツをアップロードおよび編集できます。 | プロジェクト、関連するメタデータ、および関連アセットに対する読み取りと書き込みのアクセス権撮影リスト、写真撮影、レビューおよび承認の権限/etc/commerceに対する書き込み許可特定のプロジェクトの権限を変更する | workflow-users グループ |
| 所有者 | この役割のユーザーは、プロジェクトを開始できます。所有者は、プロジェクトを作成し、プロジェクトで作業を開始し、承認済みのアセットを実稼働フォルダに移動することもできます。 所有者は、プロジェクト内のその他すべてのタスクも表示および実行できます。 | Write permission on `/etc/commerce` | `dam-users` グループ（プロジェクトを作成できるようにする）プロジェクト管理者グループ（アセットを移動できるようにする） |

>[!NOTE]
>
>プロジェクトを作成してユーザーを各種役割に追加すると、関連する権限を管理するために、プロジェクトに関連付けられたグループが自動的に作成されます。例えば、Myproject というプロジェクトには **Myproject Owners**、**Myproject Editors**、**Myproject Observers** という 3 つのグループがあります。ただし、プロジェクトを削除しても、これらのグループは自動的には削除されません。**ツール**／**セキュリティ**／**グループ**&#x200B;で、管理者が手動でグループを削除する必要があります。
