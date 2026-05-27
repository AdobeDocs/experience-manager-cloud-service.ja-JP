---
title: レプリケーション
description: AEM as a Cloud Service での配布とレプリケーションのトラブルシューティングについて説明します。
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
feature: Operations
role: Admin
source-git-commit: d6555eebfa13a400f084ef4edefb92b4471adcac
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 43%

---

# レプリケーション {#replication}

Adobe Experience Manager as a Cloud Service では、[Sling コンテンツ配布](https://sling.apache.org/documentation/bundles/content-distribution.html)機能を使用して、AEM ランタイムの外部にある Adobe Developer で実行されるパイプラインサービスに複製するコンテンツを移動します。

>[!NOTE]
>
>詳しくは、[コンテンツ配布](/help/overview/architecture.md#content-distribution)を参照してください。

## コンテンツの公開方法 {#methods-of-publishing-content}

>[!NOTE]
>
>コンテンツの一括公開に興味がある場合は、大きなペイロードを効率的に処理できる[ツリーアクティベーションワークフローステップ](/help/operations/tree-replication-workflows.md#tree-activation)を使用してワークフローを作成します。
>独自の一括公開カスタムコードを作成することはお勧めできません。
>何らかの理由でカスタマイズする必要がある場合は、既存のワークフロー API を使用して、このステップをトリガーできます。
>常に、公開する必要のあるコンテンツのみを公開することをお勧めします。 また、必要がない場合は、大量のコンテンツを公開しないようにしてください。 ただし、ツリーアクティベーションワークフローステップを使用したワークフローを通じて送信できるコンテンツの量に制限はありません。

### クイック公開／非公開 - 計画的公開／非公開 {#publish-unpublish}

この機能を使用すると、「公開を管理」のアプローチで可能な追加オプションを使用せずに、選択したページを直ちに公開できます。

詳しくは、「[公開を管理](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication)」を参照してください。

### オンタイムとオフタイム - トリガー設定 {#on-and-off-times-trigger-configuration}

**オンタイム**&#x200B;と&#x200B;**オフタイム**&#x200B;の追加設定を[ページのプロパティの「基本」タブ](/help/sites-cloud/authoring/sites-console/page-properties.md#basic)で行えます。

この機能の自動レプリケーションを実現するには、[OSGi 設定](/help/implementing/deploying/configuring-osgi.md)の「**オン／オフトリガー設定**」で「**自動レプリケーション**」を有効にします。

![OSGi オン／オフトリガー設定](/help/operations/assets/replication-on-off-trigger.png)

### 公開を管理 {#manage-publication}

公開を管理には、クイック公開よりも多くのオプションがあります。子ページの追加、参照のカスタマイズ、該当するワークフローの開始、後で公開するためのオプションがあります。

「後で公開」オプションにフォルダーの子を含めると、[&#x200B; ツリーレプリケーションワークフロー](/help/operations/tree-replication-workflows.md#publish-content-tree-workflow)で説明されているコンテンツツリーの公開ワークフローが呼び出されます。

「公開を管理」について詳しくは、 [公開の基本に関するドキュメント](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication) を参照してください。

詳細なコンテンツ階層を一括でレプリケートするには、ワークフローベースのアプローチを使用します。 推奨されるツリーアクティベーションワークフロー手順、設定パラメーター、監視ガイダンスについては、[&#x200B; ツリーレプリケーションワークフロー](/help/operations/tree-replication-workflows.md)を参照してください。 非推奨の「コンテンツツリーを公開」ワークフローも、参照のためにドキュメント化されています。

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
// if you need to get the status for more than 1 resource at once, this approach is more performant
Map<String,ReplicationStatus> allStatus = replicationStatusProvider.getBatchReplicationStatus(enResource,deResource);
```

**レプリケーションエージェント**

AEM as a Cloud Serviceには、作成者からSling Content Distributionを介してターゲット層にコンテンツをルーティングする2つの定義済みレプリケーションエージェントが用意されています。

* **publish** – アクティブ化されたコンテンツをライブ公開層にレプリケートします。 このエージェントはデフォルトで有効になっており、特に指定しない限り、UI、ワークフロー、またはレプリケーション APIから公開するときに使用されます。
* **preview** — コンテンツをプレビュー層に複製して、作成者が公開前に変更内容を確認できるようにします。 このエージェントはデフォルトでは有効になっていません。

両方のエージェントは、**ツール**/**デプロイメント**/**配布**&#x200B;から表示および監視できます。

パブリッシュとプレビューを表示する![配布エージェント &#x200B;](/help/operations/assets/replication-agents.png "配布エージェント ")

エージェント カードを選択すると、ステータス、ログ、キューの詳細[が開きます。](#replication-queues)

**特定のエージェントを使用したレプリケーション**

上記のようにAPIを使用してレプリケートする場合、デフォルトで有効になっているエージェントのみがAEM as a Cloud Serviceで使用されます。つまり、**publish**&#x200B;のみです。 プレビュー層にのみレプリケートするには、プレビューエージェントを選択する`AgentFilter`を渡します。

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

`AgentFilter`なしでレプリケートする場合、**パブリッシュ**&#x200B;のみが使用され、プレビュー層は影響を受けません。

リソースの全体的な`ReplicationStatus`は、レプリケーションにデフォルトで有効になっているエージェントが少なくとも1つ含まれている場合にのみ更新されます。 上記の例では、**preview**&#x200B;のみが使用されているので、`ReplicationStatus.isActivated`は`false`のままです。 `getStatusForAgent()`を使用して、特定のエージェントのステータスを確認します。例えば、プレビューのみのレプリケーションの後の`getStatusForAgent("preview")`や、ライブ公開層の`getStatusForAgent("publish")`などです。

### コンテンツの無効化方法 {#invalidating-content}

コンテンツを直接無効にするには、作成者が Sling コンテンツ無効化（SCD）を使用するか（推奨される方法）、Replication API を使用して公開 Dispatcher フラッシュレプリケーションエージェントを呼び出します。 詳しくは、[キャッシュ](/help/implementing/dispatcher/caching.md)ページを参照してください。

**レプリケーション API容量の制限**

一度にレプリケートするパスは 100 個未満で、上限は 500 個です。 上限を超えると、`ReplicationException` がスローされます。
アプリケーションロジックでアトミックレプリケーションが必要ない場合は、`ReplicationOptions.setUseAtomicCalls`をfalseに設定することで、この制限を克服できます。これにより、任意の数のパスを受け入れることができますが、内部的にこの制限を下回るようにバケットを作成します。

レプリケーション呼び出しごとに送信されるコンテンツのサイズは、`10 MB` を超えてはなりません。 このルールにはノードとプロパティが含まれますが、バイナリは含まれません（ワークフローパッケージとコンテンツパッケージはバイナリと見なされません）。


## レプリケーションキュー {#replication-queues}

各レプリケーションエージェントには、2つのレプリケーションキューが表示されます。 AEM as a Cloud Serviceでは、パブリッシュポッドごとに個別のキューが表示されなくなりました。パブリッシュ層は自動的にスケーリングされるため、ポッドごとのキューは実用的なメリットを得ることなく複雑になりました。 キューのステータスは、次のように統合されます。

* **永続化** – 変更は永続的にパブリッシュ層に保存されます。 アイテムがこのキューをクリアすると、コンテンツは保持されます。公開インスタンスは時間の経過とともに一貫性のある状態に達します。
* **完全に公開された** – 変更はすべての公開ポッドで公開され、影響を受けるパスのDispatcher キャッシュがクリアされます。 アイテムがこのキューをクリアすると、訪問者は更新されたコンテンツを受け取ります。

### レプリケーションキューの監視 {#monitor-replication-queues}

1. AEM [&#x200B; グローバルナビゲーション &#x200B;](/help/sites-cloud/authoring/basic-handling.md#global-navigation)から、**ツール** > **デプロイメント**&#x200B;に移動します。

   ![&#x200B; ツールから配布に移動](/help/operations/assets/replication-agent-navigation.png "配布ナビゲーション ")

1. **配布**&#x200B;を選択し、**公開**&#x200B;または&#x200B;**プレビュー** エージェント カードを開きます。

1. 「**ステータス**」タブで、各キューが正常なステータスを示していることを確認します。 処理待ちの作業については&#x200B;**処理待ちのアイテム**&#x200B;を確認し、最近のアクティビティについては&#x200B;**処理された最後のアイテム**&#x200B;を確認します。

   ![永続および完全に公開されたレプリケーションキュー](/help/operations/assets/replication-queues.png " レプリケーションキュー")

1. エージェントが配信サービスに到達できることを確認するには、**接続をテスト**&#x200B;を選択します。
1. 「**ログ**」タブを選択して、コンテンツ公開の履歴を表示します。

   ![&#x200B; レプリケーションログ &#x200B;](/help/operations/assets/publish-logs.png " ログ ")

## トラブルシューティング {#troubleshooting}

コンテンツを公開できない場合、公開はAEM パブリッシュサービスから元に戻されます。 [&#x200B; レプリケーションキューの監視](#monitor-replication-queues)を使用して、エージェント **ステータス** タブを開き、影響を受けるキューを特定します。

キューに赤いステータスが表示された場合は、保留中の項目を確認して、エラーの原因を特定します。 キューを選択して保留中の項目を表示し、必要に応じて個々の項目またはキュー全体をクリアします。
