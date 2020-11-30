---
title: レプリケーション
description: 配布とレプリケーションのトラブルシューティング。
translation-type: tm+mt
source-git-commit: abb45225e880f3d08b9d26c29e243037564acef0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 100%

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
