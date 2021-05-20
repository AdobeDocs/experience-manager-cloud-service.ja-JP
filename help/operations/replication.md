---
title: レプリケーション
description: 配布とレプリケーションのトラブルシューティング。
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: eb92c66f2b9e8e6ec859114da2de049747ec251e
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 39%

---

# レプリケーション {#replication}

Adobe Experience Manager as a Cloud Service では、[Sling コンテンツ配布](https://sling.apache.org/documentation/bundles/content-distribution.html)機能を使用して、AEM ランタイムの外部にある Adobe I/O 上で動作するパイプラインサービスに複製するコンテンツを移動します。

>[!NOTE]
>
>詳しくは、[コンテンツ配布](/help/core-concepts/architecture.md#content-distribution)を参照してください。

## コンテンツの公開方法 {#methods-of-publishing-content}

### クイック公開／非公開 - 計画的公開／非公開 {#publish-unpublish}

これらの標準的な作成者向け AEM 機能は、AEM as a Cloud Service でも変わりません。

### オンタイムとオフタイム - トリガー設定 {#on-and-off-times-trigger-configuration}

**オンタイム**&#x200B;と&#x200B;**オフタイム**&#x200B;の追加設定を[ページのプロパティの「基本」タブ](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)でおこなえます。

これの自動レプリケーションを実現するには、[OSGi 設定](/help/implementing/deploying/configuring-osgi.md)の「**On Off Trigger Configuration**」で「**Auto Replicate**」を有効にする必要があります。

![OSGi の On Off Trigger Configuration ダイアログ](/help/operations/assets/replication-on-off-trigger.png)

### ツリーのアクティベーション {#tree-activation}

ツリーのアクティベーションを実行するには：

1. AEM 開始メニューで&#x200B;**ツール／デプロイメント／配布**&#x200B;に移動します。
2. **forwardPublisher** カードを選択します。
3. forwardPublisher Web コンソール UI で「**配布**」を選択します。

   ![配布](assets/distribute.png "配布")
4. パスブラウザーでパスを選択し、必要に応じてノードやツリーの追加または削除を選択し、「**送信**」をクリックします。

### コンテンツツリーの公開ワークフロー{#publish-content-tree-workflow}

次に示すように、 **ツール/ワークフロー/モデル**&#x200B;を選択し、「**コンテンツツリーを公開**」という標準のワークフローモデルをコピーして、ツリーレプリケーションをトリガーできます。

![](/help/operations/assets/publishcontenttreeworkflow.png)

元のモデルを修正または呼び出さないでください。 代わりに、必ずモデルをコピーし、そのコピーを修正または呼び出してください。

すべてのワークフローと同様に、APIを介して呼び出すこともできます。 詳しくは、「[プログラムによるワークフローの操作](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=en#extending-aem)」を参照してください。

または、`Publish Content Tree`プロセスステップを使用するワークフローモデルを作成して、これを実現することもできます。

1. AEM as aCloud Serviceのホームページから、**Tools - Workflow - Models**&#x200B;に移動します。
1. ワークフローモデルページで、画面の右上隅にある「**Create**」を押します。
1. モデルにタイトルと名前を追加します。 詳しくは、[ワークフローモデルの作成](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)を参照してください。
1. リストから新しく作成したモデルを選択し、**編集**&#x200B;を押します。
1. 次のウィンドウで、プロセスステップを現在のモデルフローにドラッグ&amp;ドロップします。

   ![プロセスステップ](/help/operations/assets/processstep.png)

1. フローのプロセスステップをクリックし、レンチアイコンを押して「**設定**」を選択します
1. 「**プロセス**」タブをクリックし、ドロップダウンリストから「`Publish Content Tree`」を選択します

   ![Treeactivation](/help/operations/assets/newstep.png)

1. **引数**&#x200B;フィールドに追加のパラメーターを設定します。 複数のコンマ区切りの引数を弦でつなぐことができます。 以下に例を示します。

   `enableVersion=true,agentId=publish`


   >[!NOTE]
   >
   >パラメーターのリストについては、以下の&#x200B;**パラメーター**&#x200B;の節を参照してください。

1. **「完了」**&#x200B;を押して、ワークフローモデルを保存します。

**パラメーター**

* `replicateAsParticipant` (ブール値、デフォルト： `false`)をクリックします。`true`として設定した場合、レプリケーションは、参加者ステップを実行したプリンシパルの`userid`を使用します。
* `enableVersion` (ブール値、デフォルト： `true`)をクリックします。このパラメーターは、レプリケーション時に新しいバージョンが作成されるかどうかを指定します。
* `agentId` （文字列値。デフォルトは、有効なエージェントがすべて使用されることを意味します）。
* `filters` （文字列値。デフォルトは、すべてのパスがアクティブ化されることを意味します）。使用できる値は次のとおりです。
   * `onlyActivated`  — アクティブ化されていないパスのみがアクティブ化されます。
   * `onlyModified`  — 既にアクティブ化され、有効化日より後の変更日を持つパスのみをアクティブ化します。
   * 上記は、パイプ( | )でOR付けできます。 （例：`onlyActivated|onlyModified`）。

**ログ**

ツリーのアクティベーションワークフローステップが開始すると、その設定パラメータがINFOログレベルに記録されます。 パスがアクティブ化されると、INFO文も記録されます。

最後のINFO文は、ワークフローステップですべてのパスがレプリケートされた後に記録されます。

さらに、`com.day.cq.wcm.workflow.process.impl`以下のロガーのログレベルをDEBUG/TRACEに増やして、さらに多くのログ情報を取得できます。

エラーが発生した場合、ワークフローステップは`WorkflowException`で終了し、基になる例外をラップします。

サンプルのパブリッシュコンテンツツリーワークフロー中に生成されるログの例を以下に示します。

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**サポートの再開**

ワークフローは、コンテンツをチャンク単位で処理し、それぞれが公開する完全なコンテンツのサブセットを表します。 何らかの理由でワークフローがシステムによって停止された場合、ワークフローは再起動し、まだ処理されていないチャンクを処理します。 コンテンツが特定のパスから再開されたことを示すログステートメントが表示されます。

## トラブルシューティング {#troubleshooting}

レプリケーションのトラブルシューティングをおこなうには、AEM オーサーサービス Web UI のレプリケーションキューに移動します。

1. AEM 開始メニューで&#x200B;**ツール／デプロイメント／配布**&#x200B;に移動します。
2. **forwardPublisher** カードを選択します。
   ![ステータス](assets/status.png "ステータス")
3. キューのステータスが緑色かどうかを確認します。
4. レプリケーションサービスへの接続をテストできます。
5. 「**ログ**」タブを選択すると、コンテンツパブリケーションの履歴が表示されます。

![ログ](assets/logs.png "ログ")

コンテンツを公開できなかった場合は、パブリケーション全体が AEM パブリッシュサービスから戻されます。
その場合は、パブリケーションのキャンセル原因となった項目を特定するために、キューを確認する必要があります。赤色のステータスを示すキューをクリックすると、保留中の項目を含んでいるキューが表示され、必要に応じて、そのキューから 1 つまたはすべての項目をクリアできます。
