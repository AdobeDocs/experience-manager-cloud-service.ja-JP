---
title: AEM as a Cloud Serviceのツリーレプリケーションワークフロー
description: ツリーのアクティベーションのワークフローステップとAEM as a Cloud Serviceの関連ワークフローを使用して、詳細なコンテンツ階層をレプリケートする方法について説明します。
feature: Operations
role: Admin
source-git-commit: d6555eebfa13a400f084ef4edefb92b4471adcac
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 82%

---

# AEM as a Cloud Serviceのツリーレプリケーションワークフロー {#tree-replication-workflows}

コンテンツツリーの大規模なブランチを公開する必要がある場合、標準的なページごとの公開には時間がかかり、リソースを必要とします。 AEM as a Cloud Serviceは、管理可能なチャンク内のディープコンテンツ階層をレプリケートし、レプリケーションキューがビジー状態の場合は一時停止し、中断された場合は再開するワークフローベースのアプローチを提供します。

一括ツリーレプリケーションには、**ツリーのアクティブ化ワークフロー手順**&#x200B;を使用します。 これは、大規模なペイロードに対する推奨アプローチです。 **コンテンツツリーワークフローの公開**&#x200B;は引き続き参照用に文書化されますが、ツリーのアクティブ化ステップのために非推奨になります。

その他のレプリケーションに関するトピックについては、[ レプリケーション ](/help/operations/replication.md)を参照してください。

## ツリーアクティベーションワークフローステップ {#tree-activation}

ツリーのアクティブ化ワークフローステップは、コンテンツノードの深い階層をパフォーマンスよくレプリケートすることを目的としています。 キューが大きくなりすぎると、他のレプリケーションが最小限の遅延で並行して続行できるように、自動的に一時停止します。

`TreeActivation` プロセスステップを使用するワークフローモデルを作成します。

1. AEM as a Cloud Service のホームページから、**ツール／ワークフロー／モデル**&#x200B;に移動します。
1. ワークフローモデルページで、画面の右上隅にある「**作成**」を押します。
1. モデルにタイトルと名前を追加します。 詳しくは、[ワークフローモデルの作成](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=ja)を参照してください。
1. 作成したモデルをリストから選択し、「**編集**」を押します。
1. 次のウィンドウで、デフォルトで表示されるステップを削除します
1. プロセスステップを現在のモデルフローにドラッグ＆ドロップします。

   ![プロセスステップ](/help/operations/assets/processstep.png)

1. フローのプロセスステップを選択し、レンチアイコンを押して「**設定**」を選択します。
1. 「**プロセス**」タブを選択し、ドロップダウンリストから `Publish Content Tree` を選択し、**ハンドラー処理の設定**&#x200B;チェックボックスをオンにします。

   ![Treeactivation](/help/operations/assets/new-treeactivationstep.png)

1. 「**引数**」フィールドに追加のパラメーターを設定します。 複数のコンマ区切り引数をまとめることができます。 次に例を示します。

   `enableVersion=false,agentId=publish,chunkSize=50,maxTreeSize=500000,dryRun=false,filters=onlyModified,maxQueueSize=10`

   >[!NOTE]
   >
   >パラメーターのリストについては、以下の「**パラメーター**」の節を参照してください。

1. 「**完了**」を押して、ワークフローモデルを保存します。

**パラメーター**

| 名前 | デフォルト | 説明 |
| -------------- | ------- | --------------------------------------------------------------- |
| path |         | 開始するルートパス |
| agentId | publish | レプリケーションを受信するエージェント （`publish`または`preview`） |
| chunkSize | 50 | 単一のレプリケーションにバンドルするパスの数 |
| maxTreeSize | 500000 | 小さいと見なされるツリーの最大ノード数 |
| maxQueueSize | 10 | レプリケーションキューの最大項目数 |
| enableVersion | false | バージョン管理を有効にする |
| dryRun | false | trueに設定した場合、レプリケーションは実際には呼び出されません |
| userId |         | ジョブ専用。 ワークフローでは、ワークフローを呼び出すユーザーが使用される |
| フィルター |         | ノードフィルター名のリスト。 以下のサポートされているフィルターを参照してください |

**サポートされるフィルター**

| 名前 | 説明 |
| ------------- | ------------------------------------------- |
| onlyModified | ノード：新しいノードと、前回のパブリッシュ以降に変更された既存のノードの両方 |
| onlyActivated | ノード：前回のパブリッシュ前にパブリッシュされたノード |


**サポートの再開**

ワークフローはコンテンツをチャンク単位で処理し、各チャンクは、公開される完全なコンテンツのサブセットを表します。  ワークフローがシステムによって停止されると、中断した場所から続行されます。

**ワークフローの進行状況の監視**

1. AEM as a Cloud Service のホームページから、**ツール／一般／ジョブ**&#x200B;に移動します。
1. ワークフローに対応する行を確認します。 *進行状況*&#x200B;列には、レプリケーションの進行状況が示されます。 例えば、41/564 と表示され、更新すると 52/564 に更新される場合があります。

   ![Treeactivation の進行状況](/help/operations/assets/treeactivation-progress.png)


1. 行を選択して開くと、ワークフロー実行のステータスに関する追加の詳細が表示されます。

   ![Treeactivation のステータスの詳細](/help/operations/assets/treeactivation-progress-details.png)



## コンテンツツリーの公開ワークフロー {#publish-content-tree-workflow}

>[!NOTE]
>
>この機能は非推奨（廃止予定）となり、代わりにカスタムワークフローに含めることができる、よりパフォーマンスの高いツリーアクティベーションステップに置き換わりました。

+++ 廃止された機能について詳しくは、こちらをクリックしてください。

次に示すように、 **ツール／ワークフロー／モデル**&#x200B;を選択し、「**コンテンツツリーを公開**」という標準のワークフローモデルをコピーして、ツリーレプリケーションをトリガーできます。

![コンテンツツリーを公開ワークフローカード](/help/operations/assets/publishcontenttreeworkflow.png)

元のモデルを呼び出さないでください。 その代わりに、最初にモデルをコピーして、そのコピーを呼び出してください。

すべてのワークフローと同様に、API を使用して呼び出すこともできます。 詳しくは、[プログラムによるワークフローの操作](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=ja#extending-aem)を参照してください。

または、`Publish Content Tree` プロセスステップを使用するワークフローモデルを作成することもできます。

1. AEM as a Cloud Service のホームページから、**ツール／ワークフロー／モデル**&#x200B;に移動します。
1. ワークフローモデルページで、画面の右上隅にある「**作成**」を押します。
1. モデルにタイトルと名前を追加します。 詳しくは、[ワークフローモデルの作成](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=ja)を参照してください。
1. 作成したモデルをリストから選択し、「**編集**」を押します。
1. 次のウィンドウで、「プロセスステップ」を現在のモデルフローにドラッグ＆ドロップします。

   ![プロセスステップ](/help/operations/assets/processstep.png)

1. フローのプロセスステップを選択し、レンチアイコンを押して「**設定**」を選択します。
1. 「**プロセス**」タブを選択し、ドロップダウンリストから `Publish Content Tree` を選択し、**ハンドラー処理の設定**&#x200B;チェックボックスをオンにします。

   ![Treeactivation](/help/operations/assets/newstep.png)

1. 「**引数**」フィールドに追加のパラメーターを設定します。 複数のコンマ区切り引数をまとめることができます。 次に例を示します。

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >パラメーターのリストについては、以下の「**パラメーター**」の節を参照してください。

1. 「**完了**」を押して、ワークフローモデルを保存します。

**パラメーター**

* `includeChildren`（ブール値、デフォルト：`false`）。 値 `false` では、パスのみが公開され、`true` では、子も公開されます。
* `replicateAsParticipant`（ブール値、デフォルト：`false`）。 `true` に設定した場合、レプリケーションは、参加者ステップを実行したプリンシパルの `userid` を使用します。
* `enableVersion`（ブール値、デフォルト：`false`）。 このパラメーターは、レプリケーション時に新しいバージョンが作成されるかどうかを指定します。
* `agentId`（文字列値。デフォルトは、パブリッシュのエージェントのみが使用されることを意味します）。 ターゲットエージェントを明示的に指定します。例えば、ライブ公開層には`publish`、プレビュー層には`preview`を指定します。
* `filters`（文字列値。デフォルトは、すべてのパスがアクティブ化されることを意味します）。 使用できる値は次のとおりです。
   * `onlyActivated` -（既に）アクティブ化されたページのみアクティブ化します。 再アクティブ化の形で動作します。
   * `onlyModified` - 既にアクティブ化されており、変更日がアクティブ化の日付よりも後のパスのみをアクティブ化します。
   * 上記は、パイプ（|）で OR 結合できます。 （例：`onlyActivated|onlyModified`）。

**ログ**

ツリーのアクティベーションワークフローステップが開始されると、その設定パラメーターが INFO ログレベルで記録されます。 パスがアクティブ化されると、INFO 文も記録されます。

最後の INFO ステートメントは、すべてのパスがワークフローステップでレプリケートされた後にログに記録されます。

また、`com.day.cq.wcm.workflow.process.impl` の下のロガーのログレベルを DEBUG/TRACE に上げると、さらに多くのログ情報を取得できます。

エラーが発生した場合、ワークフローステップは `WorkflowException` で終了し、基になる例外をラップします。

サンプルのコンテンツツリーの公開ワークフローで生成されるログの例を以下に示します。

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

+++
