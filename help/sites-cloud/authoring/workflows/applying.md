---
title: ページへのワークフローの適用
description: オーサリングでは、ワークフローを呼び出して、ページで実行できます。複数のワークフローを適用することもできます。
exl-id: 86e71f0e-e53e-40bc-901d-2a1ab347bd0a
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: ht
source-wordcount: '654'
ht-degree: 100%

---

# ページへのワークフローの適用 {#applying-workflows-to-pages}

オーサリングでは、ワークフローを呼び出して、ページで実行できます。複数のワークフローを適用することもできます。

ワークフローを適用する際には、次の情報を指定します。

* 適用されるワークフロー。

   * （AEM 管理者によって割り当てられた、アクセス権限がある）任意のワークフローを適用できます。
* オプションで、ユーザーのインボックス内のワークフローインスタンスの特定に役立つタイトル。
* ワークフローのペイロード。1 つ以上のページを指定できます。

ワークフローは、次の場所から開始できます。

* [サイトコンソール](#starting-a-workflow-from-the-sites-console)。
* [ページの編集中に「ページ情報](#starting-a-workflow-from-the-page-editor)」から。

>[!NOTE]
>
>関連トピック：
>
>* DAM アセットにワークフローを適用する方法
>* [プロジェクトワークフローの操作](/help/sites-cloud/authoring/projects/workflows.md)

<!-- 
>* [How to apply workflows to DAM assets](/help/assets/assets-workflow.md).
>* [Working with Project Workflows](/help/sites-cloud/authoring/projects/workflows.md).
-->

>[!NOTE]
>
>AEM 管理者は他のいくつかの方法を使用してワークフローを開始できます。

<!-- 
>AEM administrators can [start workflows using several other methods](/help/sites-administering/workflows-starting.md).
-->

## Sites コンソールからのワークフローの開始 {#starting-a-workflow-from-the-sites-console}

ワークフローは以下のいずれかから開始できます。

* [サイトツールバーの「作成」オプション](#starting-a-workflow-from-the-sites-toolbar)。
* [サイトコンソールのタイムラインレール](#starting-a-workflow-from-the-timeline)。

どちらの場合も、[ワークフロー作成ウィザードでワークフローの詳細を指定する](#specifying-workflow-details-in-the-create-workflow-wizard)必要があります。

### Sites ツールバーからのワークフローの開始 {#starting-a-workflow-from-the-sites-toolbar}

**サイト**&#x200B;コンソールのツールバーからワークフローを開始できます。

1. 必要なページに移動して選択します。

1. これでツールバーの「**作成**」オプションで「**ワークフロー**」を選択できます。

   ![ツールバーからのワークフローの作成](/help/sites-cloud/authoring/assets/workflows-create-from-toolbar.png)

1. **ワークフローを作成**&#x200B;ウィザードは、[ワークフローの詳細を指定](#specifying-workflow-details-in-the-create-workflow-wizard)するのに役立ちます。

### タイムラインからのワークフローの開始 {#starting-a-workflow-from-the-timeline}

**タイムライン**&#x200B;から、選択したリソースに適用されるワークフローを開始できます。

1. [リソースを選択](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)し、[タイムライン](/help/sites-cloud/authoring/basic-handling.md#timeline)を開きます（またはタイムラインを開いてからリソースを選択します）。
1. コメントフィールドの横にある矢印を使用すると、「**ワークフローを開始**」が表示されます。

   ![タイムラインからのワークフローの作成](/help/sites-cloud/authoring/assets/workflows-create-from-timeline.png)

1. **ワークフローを作成**&#x200B;ウィザードは、[ワークフローの詳細を指定](#specifying-workflow-details-in-the-create-workflow-wizard)するのに役立ちます。

### ワークフローを作成ウィザードでのワークフローの詳細の指定 {#specifying-workflow-details-in-the-create-workflow-wizard}

**ワークフローを作成**&#x200B;ウィザードは、ワークフローを選択し、必要な詳細を指定するのに役立ちます。

**ワークフローを作成**&#x200B;ウィザードを次のいずれかから開きます。

* [サイトツールバーの「作成」オプション](#starting-a-workflow-from-the-sites-toolbar)。
* [サイトコンソールのタイムラインレール](#starting-a-workflow-from-the-timeline)。

次の詳細を指定できます。

1. **プロパティ**&#x200B;の手順では、ワークフローの基本オプションを定義します。

   * **ワークフローモデル**
   * **ワークフロータイトル**

      * このインスタンスのタイトルを指定して、後の段階で識別しやすくできます。

   ワークフローモデルに応じて、次のオプションも使用できます。これにより、ペイロードとして作成されたパッケージを、ワークフローの完了後も保持できます。

   * **ワークフローパッケージを維持**
   * **パッケージタイトル**

      * 識別に役立つように、パッケージのタイトルを指定できます。

   >[!NOTE]
   >
   >ワークフローがマルチリソースサポートのために設定されており、複数のリソースが選択されている場合は、**ワークフローパッケージを維持**&#x200B;オプションが使用できます。

   <!--
   >The **Keep workflow package** option is available when the workflow has been configured for [Multi Resource Support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) and multiple resources have been selected.
   -->

   完了したら、「**次へ**」を使用して続行します。

   ![ワークフロープロパティの指定](/help/sites-cloud/authoring/assets/workflows-properties.png)

1. **スコープ**&#x200B;ステップで、以下のものを選択できます。

   * 「**コンテンツを追加**」で[パスブラウザー](/help/sites-cloud/authoring/path-selection.md)を開き、追加リソースを選択します。ブラウザーでは、「**選択**」を選択して、コンテンツをワークフローインスタンスに追加します。

   * 追加のアクションを表示するための既存のリソース

      * 「**子を含める**」で、ワークフローに含まれるそのリソースの子を指定します。
ダイアログボックスが開き、以下に従って選択を絞り込むことができます。

         * 直近の子のみを含める。
         * 変更されたページのみを含める。
         * 既に公開済みのページのみを含める。

        指定した子は、ワークフローが適用されるリソースのリストに追加されます。

      * 「**選択項目を削除**」で、そのリソースをワークフローから削除します。

   ![ワークフローの範囲の定義](/help/sites-cloud/authoring/assets/workflows-scope.png)

   >[!NOTE]
   >
   >追加リソースを追加する場合は、「**戻る**」を使用して、**プロパティ**&#x200B;ステップで「**ワークフローパッケージを維持**」の設定を調整できます。

1. 「**作成**」を使用して、ウィザードを閉じ、ワークフローインスタンスを作成します。通知はサイトコンソールに表示されます。

## ページエディターからのワークフローの開始 {#starting-a-workflow-from-the-page-editor}

ページの編集時に、ツールバーから「**ページ情報**」を選択できます。ドロップダウンメニューには、「**ワークフローで開始**」オプションがあります。これによりダイアログが開き、必要なワークフローと、必要な場合はタイトルを指定できます。

![ページエディターからのワークフローの開始](/help/sites-cloud/authoring/assets/workflows-create-page-editor.png)
