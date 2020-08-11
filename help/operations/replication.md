---
title: レプリケーション
description: 分布 レプリケーションのトラブルシューティング
translation-type: tm+mt
source-git-commit: abb45225e880f3d08b9d26c29e243037564acef0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 3%

---


# レプリケーション {#replication}

Cloud ServiceとしてAdobe Experience Managerは、 [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) (Sling Content Distribution)機能を使用して、AEMランタイムの外部にあるAdobeI/O上で実行されるパイプラインサービスに複製するコンテンツを移動します。

>[!NOTE]
>
>詳しくは、 [配布版を参照してください](/help/core-concepts/architecture.md#content-distribution) 。

## コンテンツの公開方法 {#methods-of-publishing-content}

### クイック非公開/公開 — 計画されている非公開/公開 {#publish-unpublish}

作成者向けのこれらの標準的なAEM機能は、AEMCloud Serviceでは変更されません。

### オン/オフ時間 — トリガー設定 {#on-and-off-times-trigger-configuration}

「 **オン時間** 」と「 **オフ時間** 」の追加機能は、ページプロパティの「 [基本」タブから利用できます](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)。

この自動レプリケーションを実現するには、 **OSGi構成** On Off Trigger構成で [自動レプリケーションを有効にする必要があります](/help/implementing/deploying/configuring-osgi.md)****。

![OSGiオンオフトリガーの設定](/help/operations/assets/replication-on-off-trigger.png)

### ツリーのアクティベーション {#tree-activation}

ツリーアクティベーションを実行するには：

1. AEM開始メニューで、 **ツール/導入/配布に移動します。**
2. カードの **forwardPublisherを選択します**
3. forwardPublisher WebコンソールのUIを表示したら、「配布」を **選択します。**

   ![](assets/distribute.png "DistributeDistribute")
4. パスブラウザーでパスを選択し、必要に応じてノード、ツリーまたは削除を追加するか、「 **送信」を選択します**

## トラブルシューティング {#troubleshooting}

レプリケーションのトラブルシューティングを行うには、AEM Author Service Web UIのReplication Queuesに移動します。

1. AEM開始メニューで、 **ツール/導入/配布に移動します。**
2. カードの **forwardPublisherを選択します**
   ![](assets/status.png "StatusStatus")
3. 緑であるはずのキューステータスを確認します
4. レプリケーションサービスへの接続をテストできます
5. コンテンツパブリケーションの履歴を表示する **「ログ** 」タブを選択します

![](assets/logs.png "LogsLogs")

コンテンツを公開できない場合は、パブリケーション全体がAEM発行サービスから戻されます。
この場合、パブリケーションがキャンセルされた原因となった項目を特定するために、キューを確認する必要があります。 赤いステータスを示すキューをクリックすると、保留中のアイテムを含むキューが表示され、必要に応じて、このキューから単一またはすべてのアイテムをクリアできます。
