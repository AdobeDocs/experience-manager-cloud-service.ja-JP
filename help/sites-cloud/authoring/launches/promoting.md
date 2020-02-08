---
title: ローンチの昇格
description: 'コンテンツを公開する前にソース（実稼動）に戻すには、ローンチページを昇格させる必要があります。 '
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# ローンチの昇格 {#promoting-launches}

コンテンツを公開する前にソース（実稼動）に戻すには、ローンチページを昇格させる必要があります。ローンチページが昇格されると、ソースページの対応するページが、昇格済みのページのコンテンツに置き換わります。ページを昇格させるときには、次のオプションを使用できます。

* 現在のページのみを昇格させるか、ローンチ全体を昇格させるか。
* 現在のページの子ページを昇格するかどうか。
* すべてのローンチを昇格させるか、変更したページのみを昇格させるか。
* 昇格後にローンチを削除するかどうか。

>[!NOTE]
>
>ローンチページをターゲット（**実稼動**）に昇格させると、（プロセスを高速化するために）**実稼動**&#x200B;ページをエンティティとしてアクティベートできます。ページをワークフローパッケージに追加し、ページのパッケージをアクティベートするワークフローで、このワークフローパッケージをペイロードとして使用します。ローンチを昇格する前に、ワークフローパッケージを作成する必要があります。[AEM ワークフローを使用した昇格済みページの処理](#processing-promoted-pages-using-aem-workflow)を参照してください。

>[!CAUTION]
>
>単一のローンチは同時に昇格させることができません。This means that two promote actions on the same launch at the same time can result in an error - `Launch could not be promoted` (together with conflict errors in the log).

>[!CAUTION]
>
>*変更した*&#x200B;ページのローンチを昇格させる場合は、ソースブランチとローンチブランチの両方での変更が考慮されます。

## ローンチページの昇格 {#promoting-launch-pages}

>[!NOTE]
>
>ここでは、ローンチレベルが 1 つのみのときにローンチページを昇格させる手動のアクションについて説明します。次のページを参照してください。
>
>* 構造に複数のローンチがあるときは、[ネストされたローンチの昇格](#promoting-a-nested-launch)。
>* 自動昇格および公開について詳しくは、[ローンチ - イベントの順序](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events)。
>



ローンチは、**サイト**&#x200B;コンソールまたは&#x200B;**ローンチ**&#x200B;コンソールを使用して昇格させることができます。

1. 次のファイルを開きます。
   * The **Sites** console:
      1. Open the [references rail](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) and select the required source page using [selection mode](/help/sites-cloud/authoring/getting-started/basic-handling.md) (or select and open the references rail, the order is not important). すべての参照が表示されます。
      1. **ローンチ**（例：ローンチ（1））を選択して特定のローンチのリストを表示します。
      1. 特定のローンチを選択して使用可能なアクションを選択します。
      1. 「**ローンチを昇格**」を選択してウィザードを開きます。
   * The **Launches** console:
      1. 対象のローンチを選択（サムネイルをタップまたはクリック）します。
      1. 「**昇格**」を選択します。
1. 最初のステップでは、次のオプションを指定できます。
   * **ターゲット**
      * **昇格後にローンチを削除**
   * **対象範囲**
      * **すべてのローンチを昇格**
      * **変更したページを昇格**
      * **現在のページを昇格**
      * **現在のページとサブページを昇格**
      例えば、変更したページのみを昇格させるには、次のように選択します。

      ![プロモーションの開始](/help/sites-cloud/authoring/assets/launches-promote.png)

      >[!NOTE]
      >
      >ここでは単一のローンチについて説明します。ネストされたローンチがある場合は、[ネストされたローンチの昇格](#promoting-a-nested-launch)を参照してください。
1. 「**次へ**」を選択して先に進みます。
1. 昇格させるページを確認できます。これは、選択したページの範囲によって変わります。

   ![プロモーションのレビュー](/help/sites-cloud/authoring/assets/launches-promote-review.png)

1. 「**昇格**」を選択します。

## 編集中のローンチページの昇格 {#promoting-launch-pages-when-editing}

ローンチページの編集中、**ローンチを昇格**&#x200B;アクションは「**ページ情報**」からも実行できます。これによりウィザードが開き、必要な情報が収集されます。

![サイト情報からの開始を促進](/help/sites-cloud/authoring/assets/launches-promote-page-info.png)

>[!NOTE]
>
>これは単一および[ネストされたローンチ](#promoting-a-nested-launch)で使用できます。

## ネストされたローンチの昇格 {#promoting-a-nested-launch}

ネストされたローンチを作成後、任意のソース（ルートソース（実稼動）を含む）に戻して昇格させることができます。

![ネストされた起動](/help/sites-cloud/authoring/assets/launches-promoting-nested.png)

1. ネストされたローンチを作成するときと同様に、**ローンチ**&#x200B;コンソールまたは&#x200B;**参照**&#x200B;レールのいずれかで必要なローンチに移動して選択します。
1. 「**ローンチを昇格**」を選択してウィザードを開きます。
1. 次の必要な詳細を入力します。
   * **ターゲット**
      * **プロモーション** ・ターゲット — 任意のソースにプロモーションできます。
      * **プロモーション後に起動を削除** — プロモーション後に、選択した起動とその中にネストされた起動が削除されます。
   * **範囲** — ここでは、起動全体をプロモーションするか、実際に編集されたページのみをプロモーションするかを選択できます。 後者の場合、サブページを含めるか除外するかを選択できます。デフォルトの設定では、現在のページのページの変更のみを昇格させます。
      * **すべてのローンチを昇格**
      * **変更したページを昇格**
      * **現在のページを昇格**
      * **現在のページとサブページを昇格**
   ![起動設定の昇格](/help/sites-cloud/authoring/assets/launches-promote-settings.png)

1. 「**次へ**」を選択します。
1. 「**昇格**」を選択する前に、次の昇格の詳細を確認します。

   ![プロモーション設定の確認](/help/sites-cloud/authoring/assets/launches-promote-review-2.png)

   >[!NOTE]
   >
   >リストされるページは、定義した&#x200B;**範囲**&#x200B;と場合によっては実際に編集したページに依存します。

1. 変更は昇格され、**ローンチ**&#x200B;コンソールに反映されます。

   ![起動コンソール内](/help/sites-cloud/authoring/assets/launches-console.png)

## AEM ワークフローを使用した昇格済みページの処理 {#processing-promoted-pages-using-aem-workflow}

次のワークフローモデルを使用して、昇格済みのローンチページの一括処理をおこないます。

1. ワークフローパッケージを作成します。
1. 作成者がローンチページを昇格するとき、ワークフローパッケージにローンチページを保存します。
1. このパッケージをペイロードとして使用し、ワークフローモデルを開始します。

To start a workflow automatically when pages are promoted, configure a workflow launcher for the package node. <!--To start a workflow automatically when pages are promoted, [configure a workflow launcher](/help/sites-administering/workflows-starting.md#workflows-launchers) for the package node.-->

例えば、作成者がローンチページを昇格したとき、ページのアクティベートのリクエストを自動的に生成することができます。パッケージノードが変更されたときにリクエストのアクティベートワークフローを開始するよう、ワークフローランチャーを設定します。

![プロモーションワークフロー](/help/sites-cloud/authoring/assets/launches-create-workflow.png)
