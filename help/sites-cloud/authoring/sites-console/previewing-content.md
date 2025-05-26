---
title: コンテンツのプレビュー
description: AEM プレビューサービスを使用して、運用を開始する前にコンテンツをプレビューする方法を説明します。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: b93bcb5d26a63babf0b81c92a4fd85d358bfbea7
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 82%

---


# コンテンツのプレビュー {#previewing-content}

AEM は、web サイトがパブリッシュ環境になって一般公開される前に、開発者とコンテンツ作成者が web サイトの最終的なエクスペリエンスをプレビューできるサイトプレビューサービスを提供しています。

これにより、ページトランジションやその他のパブリッシュ側のコンテンツなど、オーサー環境からは見えないページエクスペリエンスのプレビューが容易になります。

>[!IMPORTANT]
>
>プレビュー環境にアクセスするには、IP許可リストを設定する必要があります。 詳しくは、[ プレビューサービスへのアクセス ](/help/implementing/cloud-manager/manage-environments.md#access-preview-service#access-preview-service) を参照してください。
>
>すべての環境について詳しくは、[ 環境の管理 ](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) を参照してください。

>[!NOTE]
>
>コンテンツはプレビュー環境に *公開* されるため、URL でアクセスできます。

## プレビュー用のコンテンツの公開 {#publishing-content-to-preview}

プレビューサービスにコンテンツを公開するには、**公開を管理** UI を使用します。

1. Sites コンソールで、プレビュー用に送信する 1 つ以上のページを選択し、「**公開を管理**」ボタンをクリックします。
1. 次のウィザードで、宛先に「**プレビュー**」を選択します.

   ![管理対象公開](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 「**次へ**」をクリックし、「**公開**」をクリックして確定します。

1. プレビュー環境のコンテンツにアクセスするための URL がダイアログに表示されます。

   >[!NOTE]
   >
   >プレビュー環境に&#x200B;*公開済み*&#x200B;のコンテンツにアクセスするには、URL を使用します（AEMにアクセスする必要はありません）。

また、ウィザードに表示される URL を使用してプレビューコンテンツを確認する代わりに、実稼動インスタンスのパブリッシュ URL の先頭に `preview-` を付加することもできます。

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

お使いの環境の URL を取得する方法について詳しくは、[ 環境の管理 ](/help/implementing/cloud-manager/manage-environments.md) を参照してください。

コンテンツをプレビューに公開するには、`agentId` パラメーターを `preview` に設定した[コンテンツツリーの公開ワークフロー](/help/operations/replication.md#publish-content-tree-workflow)を使用するか、`AgentFilter` をプレビュー用に設定した[レプリケーション API](/help/operations/replication.md#replication-api) を使用することもできます。

## プレビューからコンテンツを非公開にする {#unpublishing-content-from-preview}

**プレビュー**&#x200B;環境からコンテンツを非公開にする方法は、**公開**&#x200B;環境から[ページを非公開にする](/help/sites-cloud/authoring/sites-console/publishing-pages.md#unpublishing-pages)場合と基本的に同じプロセスです。

唯一の違いは、**プレビュー**&#x200B;する&#x200B;**宛先**&#x200B;を選択できることです。
