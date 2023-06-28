---
title: レプリケーション
description: レプリケーションの配布とトラブルシューティング。
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 45%

---

# レプリケーション {#replication}

Adobe Experience Manager as a Cloud Serviceは [Sling コンテンツ配布](https://sling.apache.org/documentation/bundles/content-distribution.html) レプリケートするコンテンツを、AEMランタイムの外部にあるAdobe Developerで実行されるパイプラインサービスに移動する機能。

>[!NOTE]
>
>詳しくは、[コンテンツ配布](/help/overview/architecture.md#content-distribution)を参照してください。

## コンテンツの公開方法 {#methods-of-publishing-content}

>[!NOTE]
>
>コンテンツの一括公開に関心がある場合は、 [コンテンツツリーの公開ワークフロー](#publish-content-tree-workflow).
>このワークフローステップは、特にCloud Service向けに構築されており、大きなペイロードを効率的に処理できます。
>独自の一括公開カスタムコードを作成することはお勧めしません。
>何らかの理由でをカスタマイズする必要がある場合は、既存の Workflow API を使用して、このワークフロー/ワークフローステップにトリガーを設定できます。
>常に、公開する必要のあるコンテンツのみを公開することをお勧めします。 また、必要がない場合は、大量のコンテンツを公開しないことをお勧めします。 ただし、コンテンツツリーの公開ワークフローで送信できるコンテンツの量に制限はありません。

### クイック公開／非公開 - 計画的公開／非公開 {#publish-unpublish}

この機能を使用すると、選択したページを直ちに公開できます。公開を管理のアプローチで追加のオプションを使用する必要はありません。

詳しくは、「[公開を管理](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication)」を参照してください。

### オンタイムとオフタイム - トリガー設定 {#on-and-off-times-trigger-configuration}

**オンタイム**&#x200B;と&#x200B;**オフタイム**&#x200B;の追加設定を[ページのプロパティの「基本」タブ](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)で行えます。

この機能の自動レプリケーションを実現するには、を有効にします。 **自動レプリケーション** 内 [OSGi 設定](/help/implementing/deploying/configuring-osgi.md) **オンオフトリガー設定**:

![OSGi の On Off Trigger Configuration ダイアログ](/help/operations/assets/replication-on-off-trigger.png)

### 公開を管理 {#manage-publication}

「公開を管理」には、クイック公開よりも多くのオプションが用意されており、子ページの追加、参照のカスタマイズ、適用可能なワークフローの開始、後で公開するオプションの提供が可能です。

「後で公開する」オプションにフォルダーの子を含めると、コンテンツツリーを公開ワークフローが呼び出されます（この記事で説明）。

「公開を管理」について詳しくは、 [公開の基本に関するドキュメント](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication) を参照してください。

### コンテンツツリーの公開ワークフロー {#publish-content-tree-workflow}

次に示すように、 **ツール／ワークフロー／モデル**&#x200B;を選択し、「**コンテンツツリーを公開**」という標準のワークフローモデルをコピーして、ツリーレプリケーションをトリガーできます。

![「コンテンツツリーを公開」ワークフローカード](/help/operations/assets/publishcontenttreeworkflow.png)

元のモデルを修正したり呼び出さないでください。必ずモデルをコピーして、そのコピーを修正または呼び出してください。

すべてのワークフローと同様に、API を使用して呼び出すこともできます。詳しくは、 [プログラムによるワークフローの操作](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=ja#extending-aem).

または、 `Publish Content Tree` プロセスステップ：

1. AEMas a Cloud Serviceのホームページで、に移動します。 **ツール/ワークフロー/モデル**.
1. ワークフローモデルページで、 **作成** をクリックします。
1. モデルにタイトルと名前を追加します。詳しくは、「[ワークフローモデルの作成](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=ja#extending-aem)」を参照してください。。
1. 新しく作成したモデルをリストから選択し、「**編集**」を押します。
1. 次のウィンドウで、「プロセスステップ」を現在のモデルフローにドラッグ＆ドロップします。

   ![プロセスステップ](/help/operations/assets/processstep.png)

1. フローのプロセスステップを選択し、「 」を選択します。 **設定** レンチアイコンを押すことで、
1. を選択します。 **プロセス** 「 」タブで「 」を選択します。 `Publish Content Tree` ドロップダウンリストから、 **ハンドラー処理の設定** チェックボックス

   ![Treeactivation](/help/operations/assets/newstep.png)

1. 「**引数**」フィールドに追加のパラメーターを設定します。複数のコンマ区切り引数をまとめることができます。 次に例を示します。

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >パラメーターのリストについては、以下の「**パラメーター**」の節を参照してください。

1. 「**完了**」を押して、ワークフローモデルを保存します。

**パラメーター**

* `includeChildren`（ブール値、デフォルト：`false`）。値 `false` は、パスのみが公開されることを意味します。 `true` は、子も公開されることを意味します。
* `replicateAsParticipant`（ブール値、デフォルト：`false`）。`true` に設定した場合、レプリケーションは、参加者ステップを実行したプリンシパルの `userid` を使用します。
* `enableVersion`（ブール値、デフォルト：`true`）。このパラメーターは、レプリケーション時に新しいバージョンが作成されるかどうかを指定します。
* `agentId`（文字列値。デフォルトは、パブリッシュのエージェントのみが使用されることを意味します）。agentId を明確にすることをお勧めします。例えば、値「publish」を設定します。エージェントを `preview` をプレビューサービスにパブリッシュします。
* `filters` （文字列値、デフォルトは、すべてのパスがアクティブ化されることを意味します）。 使用できる値は次のとおりです。
   * `onlyActivated` -（既に）アクティブ化されたページのみアクティブ化します。再アクティブ化の形で動作します。
   * `onlyModified` - 既にアクティブ化されており、変更日がアクティブ化の日付よりも後のパスのみをアクティブ化します。
   * 上記は、パイプ（|）で OR 結合できます。（例：`onlyActivated|onlyModified`）。

**ログ**

ツリーのアクティベーションワークフローステップが開始すると、その設定パラメーターが INFO ログレベルに記録されます。 パスがアクティブ化されると、INFO 文も記録されます。

最後の INFO 文は、ワークフローステップがすべてのパスをレプリケートした後に記録されます。

また、ロガーのログレベルを以下に上げることもできます `com.day.cq.wcm.workflow.process.impl` を DEBUG/TRACEに追加し、さらに多くのログ情報を取得します。

エラーが発生した場合、ワークフローステップは `WorkflowException`：基になる例外をラップします。

サンプルの公開コンテンツツリーワークフロー中に生成されるログの例を次に示します。

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**サポートの再開**

ワークフローは、コンテンツをチャンク単位で処理し、チャンクは公開されるコンテンツ全体のサブセットを表します。ワークフローがシステムによって停止されると、まだ処理されていないチャンクが再起動され、処理されます。 ログステートメントには、コンテンツが特定のパスから再開されたことが示されます。

### レプリケーション API {#replication-api}

AEM as a Cloud Service に備わっている Replication API を使用してコンテンツを公開できます。

詳しくは、 [API のドキュメント](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/com/day/cq/replication/package-summary.html) を参照してください。

**API の基本的な使用法**

```
@Reference
Replicator replicator;
@Reference
ReplicationStatusProvider replicationStatusProvider;

....
Session session = ...
// Activate a single page to all agents, which are active by default
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en");
// Activate multiple pages (but try to limit it to approx 100 at max)
replicator.replicate(session,ReplicationActionType.ACTIVATE, new String[]{"/content/we-retail/en","/content/we-retail/de"});

// ways to get the replication status
Resource enResource = resourceResolver.getResource("/content/we-retail/en");
Resource deResource = resourceResolver.getResource("/content/we-retail/de");
ReplicationStatus enStatus = enResource.adaptTo(ReplicationStatus.class);
// if you need to get the status for more more than 1 resource at once, this approach is more performant
Map<String,ReplicationStatus> allStatus = replicationStatusProvider.getBatchReplicationStatus(enResource,deResource);
```

**特定のエージェントを使用したレプリケーション**

前述の例のように、リソースをレプリケートする場合は、デフォルトでアクティブなエージェントのみが使用されます。 AEM as a Cloud Serviceでは、オーサーをパブリッシュ層に接続する、「パブリッシュ」と呼ばれるエージェントのみを意味します。

プレビュー機能をサポートするために、「プレビュー」と呼ばれる新しいエージェントが追加されました。このエージェントは、デフォルトではアクティブになっていません。このエージェントは、オーサーをプレビュー層に接続するために使用されます。プレビューエージェントを使用してのみレプリケートする場合は、 `AgentFilter`.

次の例を参照してください。

```
private static final String PREVIEW_AGENT = "preview";

ReplicationStatus beforeStatus = enResource.adaptTo(ReplicationStatus.class); // beforeStatus.isActivated == false

ReplicationOptions options = new ReplicationOptions();
options.setFilter(new AgentFilter() {
  @Override
  public boolean isIncluded (Agent agent) {
    return agent.getId().equals(PREVIEW_AGENT);
  }
});
// will replicate only to preview
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en", options);

ReplicationStatus afterStatus = enResource.adaptTo(ReplicationStatus.class); // afterStatus.isActivated == false
ReplicationStatus previewStatus = afterStatus.getStatusForAgent(PREVIEW_AGENT); // previewStatus.isActivated == true
```

このようなフィルターを指定せず、「パブリッシュ」エージェントのみを使用する場合、「プレビュー」エージェントは使用されず、レプリケーションアクションはプレビュー層には影響しません。

リソースの `ReplicationStatus` 全体が変更されるのは、デフォルトでアクティブになっているエージェントがレプリケーションアクションに少なくとも 1 つ含まれている場合のみです。上記の例では、このフローは該当しませんでした。 レプリケーションは、「プレビュー」エージェントを使用しただけです。 したがって、新しい `getStatusForAgent()` メソッド：特定のエージェントのステータスを照会できます。 このメソッドは、「パブリッシュ」エージェントに対しても機能します。指定されたエージェントを使用して実行されたレプリケーションアクションがある場合、このメソッドは null 以外の値を返します。

### コンテンツの無効化方法 {#invalidating-content}

コンテンツを直接無効にするには、オーサーから Sling コンテンツ無効化 (SCD) を使用するか（推奨される方法）、レプリケーション API を使用してパブリッシュ Dispatcher フラッシュレプリケーションエージェントを呼び出します。 詳しくは、 [キャッシュ](/help/implementing/dispatcher/caching.md) ページを参照してください。

**Replication API の容量制限**

1 度に 100 個未満のパスをレプリケートし、500 個が制限されます。 制限を超える場合、 `ReplicationException` がスローされます。
アプリケーションロジックがアトミックレプリケーションを必要としない場合、この制限は、 `ReplicationOptions.setUseAtomicCalls` を false に設定します。この値は任意の数のパスを受け入れますが、内部的にグループを作成して、この制限を下回るようにします。

レプリケーション呼び出しごとに送信されるコンテンツのサイズは、`10 MB` を超えてはなりません。このルールにはノードとプロパティが含まれますが、バイナリは含まれません（ワークフローパッケージとコンテンツパッケージはバイナリと見なされます）。


## トラブルシューティング {#troubleshooting}

レプリケーションのトラブルシューティングを行うには、AEM オーサーサービス Web UI のレプリケーションキューに移動します。

1. 「AEM Start」メニューから、に移動します。 **ツール/導入/配布**
2. **公開**カードを選択します。
   ![ステータス](assets/publish-status.png "ステータス")
3. キューのステータスが緑色かどうかを確認します。
4. レプリケーションサービスへの接続をテストできます。
5. 「**ログ**」タブを選択すると、コンテンツパブリケーションの履歴が表示されます。

![ログ](assets/publish-logs.png "ログ")

コンテンツを公開できなかった場合は、パブリケーション全体が AEM パブリッシュサービスから戻されます。
この場合、メインの編集可能なキューは赤いステータスを表示し、どの項目がパブリケーションのキャンセルの原因となったかを確認する必要があります。 そのキューをクリックすると、保留中の項目が表示され、必要に応じて、1 つの項目またはすべての項目をクリアできます。
