---
title: レプリケーション
description: レプリケーションの配布とトラブルシューティング
translation-type: tm+mt
source-git-commit: 8fba31951276d7e0de1f3bd079e42e431edaff4e

---


# レプリケーション {#replication}

クラウドサービスとしてのAdobe Experience Managerは、 [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) (Sling Content Distribution)機能を使用して、AEMランタイム以外でAdobe I/O上で実行されるパイプラインサービスに複製するコンテンツを移動します。

>[!NOTE]
>
> 詳しくは [配布](/help/core-concepts/architecture.md#content-distribution) (Distribution)を参照してください。

## コンテンツの公開方法 {#methods-of-publishing-content}

### クイック取り消し/公開 — 予定されている取り消し/公開 {#publish-unpublish}

作成者向けのこれらの標準的なAEM機能は、AEMクラウドサービスでは変更されません。

### ツリーのアクティベーション {#tree-activation}

ツリーのアクティブ化を実行するには：

1. AEMのスタートメニューで、ツール/デプロイメ **ント/配布に移動します。**
2. カードforwardPublisherを選択し **ます**
3. forwardPublisher webコンソールのUIに移動したら、「配布」を **選択します。**
   ![DistributeDistribute](assets/distribute.png "")
4. パスブラウザーでパスを選択し、必要に応じてノード、ツリーまたは削除を選択して、「送信」を選択しま **す。**

## トラブルシューティング {#troubleshooting}

レプリケーションのトラブルシューティングを行うには、AEM Author Service Web UIの「Replication Queues」に移動します。

1. AEMのスタートメニューで、ツール/デプロイメ **ント/配布に移動します。**
2. カードforwardPublisherを選択し **ます**
   ![StatusStatus](assets/status.png "")
3. 緑色になるキューの状態を確認します
4. レプリケーションサービスへの接続をテストできます
5. コンテンツパブ **リケーションの履歴を表示する「ログ** 」タブを選択します

![LogsLogs](assets/logs.png "")

コンテンツを公開できなかった場合、パブリケーション全体がAEM発行サービスから元に戻されます。
この場合、パブリケーションのキャンセルの原因となった項目を特定するために、キューを確認する必要があります。 赤のステータスを示すキューをクリックすると、保留中のアイテムを含むキューが表示され、必要に応じて、単一またはすべてのアイテムをクリアできます。
