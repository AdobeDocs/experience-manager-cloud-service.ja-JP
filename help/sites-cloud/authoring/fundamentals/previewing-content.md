---
title: コンテンツのプレビュー
description: AEM プレビューサービスを使用して、運用を開始する前にコンテンツをプレビューする方法を説明します。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 1804eacb5399dc38c97ff953031666711b9a0e4f
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 83%

---


# コンテンツのプレビュー {#previewing-content}

AEM は、web サイトがパブリッシュ環境になって一般公開される前に、開発者とコンテンツ作成者が web サイトの最終的なエクスペリエンスをプレビューできるサイトプレビューサービスを提供しています。

これにより、ページトランジションやその他のパブリッシュ側のコンテンツなど、オーサー環境からは見えないページエクスペリエンスのプレビューが容易になります。

>[!NOTE]
>
>コンテンツが *公開済み* プレビュー環境にアクセスするには、URL を使用します (AEMにアクセスする必要はありません )。

プレビュー環境について詳しくは、 [環境の管理](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## プレビュー用のコンテンツの公開 {#publishing-content-to-preview}

プレビューサービスにコンテンツを公開するには、**公開を管理** UI を使用します。

1. Sites コンソールで、プレビュー用に送信する 1 つ以上のページを選択し、「**公開を管理**」ボタンをクリックします。
1. 次のウィザードで、宛先として「**プレビュー**」を選択します

   ![管理対象公開](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 「**次へ**」をクリックし、「**公開**」をクリックして確定します。

1. プレビュー環境のコンテンツにアクセスするための URL がダイアログに表示されます。

   >[!NOTE]
   >
   >コンテンツが *公開済み* プレビュー環境にアクセスするには、URL を使用します (AEMにアクセスする必要はありません )。

また、ウィザードに表示される URL を使用してプレビューコンテンツを確認する代わりに、実稼動インスタンスのパブリッシュ URL の先頭に `preview-` を付加することもできます。

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

お使いの環境の URL を取得する方法について詳しくは、[環境の管理](/help/implementing/cloud-manager/manage-environments.md)のドキュメントを参照してください。

コンテンツをプレビューに公開するには、`agentId` パラメーターを `preview` に設定した[コンテンツツリーの公開ワークフロー](/help/operations/replication.md#publish-content-tree-workflow)を使用するか、`AgentFilter` をプレビュー用に設定した[レプリケーション API](/help/operations/replication.md#replication-api) を使用することもできます。

## プレビューからコンテンツを非公開にする {#unpublishing-content-from-preview}

**プレビュー**&#x200B;環境からコンテンツを非公開にする方法は、**公開**&#x200B;環境から[ページを非公開にする](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)場合と基本的に同じプロセスです。

唯一の違いは、**プレビュー**&#x200B;する&#x200B;**宛先**&#x200B;を選択できることです。

## その他の情報 {#further-information}

関連トピック：

* [プレビュー層の OSGi 設定の指定](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#configuring-osgi-settings-for-the-preview-tier)

* [開発者コンソールを使用したプレビューのデバッグ](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#debugging-preview-using-the-developer-console)