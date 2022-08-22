---
title: コンテンツのプレビュー
description: AEM プレビューサービスを使用して、運用を開始する前にコンテンツをプレビューする方法を説明します。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 66bc262b35f69b7877e4a01df9ab26395afd604d
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 100%

---


# コンテンツのプレビュー {#previewing-content}

AEM は、web サイトがパブリッシュ環境になって一般公開される前に、開発者とコンテンツ作成者が web サイトの最終的なエクスペリエンスをプレビューできるサイトプレビューサービスを提供しています。

これにより、ページトランジションやその他のパブリッシュ側のコンテンツなど、オーサー環境からは見えないページエクスペリエンスのプレビューが容易になります。

プレビュー環境について詳しくは、[環境の管理](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)のドキュメントを参照してください。

>[!NOTE]
>
>エクスペリエンスフラグメントをプレビューに公開する手順は、エクスペリエンスフラグメントコンソールまたはエディターを使用しますが、基本的にはページの場合と同じです。

## プレビュー用のコンテンツの公開 {#publishing-content-to-preview}

プレビューサービスにコンテンツを公開するには、**公開を管理** UI を使用します。

1. Sites コンソールで、プレビュー用に送信する 1 つ以上のページを選択し、「**公開を管理**」ボタンをクリックします。
1. 次のウィザードで、宛先として「**プレビュー**」を選択します

   ![管理対象公開](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 「**次へ**」をクリックし、「**公開**」をクリックして確定します。

1. プレビュー環境のコンテンツにアクセスするための URL がダイアログに表示されます。


また、ウィザードに表示される URL を使用してプレビューコンテンツを確認する代わりに、実稼動インスタンスのパブリッシュ URL の先頭に `preview-` を付加することもできます。

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

お使いの環境の URL を取得する方法について詳しくは、[環境の管理](/help/implementing/cloud-manager/manage-environments.md)のドキュメントを参照してください。

コンテンツをプレビューに公開するには、`agentId` パラメーターを `preview` に設定した[コンテンツツリーの公開ワークフロー](/help/operations/replication.md#publish-content-tree-workflow)を使用するか、`AgentFilter` をプレビュー用に設定した[レプリケーション API](/help/operations/replication.md#replication-api) を使用することもできます。

## プレビュー層の OSGi 設定の指定 {#configuring-osgi-settings-for-the-preview-tier}

プレビュー層の OSGi プロパティ値は、パブリッシュ層から継承されます。ただし、`service` パラメーターを `preview` 値に設定することで、プレビュー層の値をパブリッシュ層と区別することができます。次の OSGi プロパティの例では、統合エンドポイントの URL を決定しています。

```
[
{
"name":"INTEGRATION_URL",
"type":"string",
"value":"http://s2.integrationvendor.com",
"service": "preview"
}
]
```

詳しくは、OSGi 設定ドキュメントの[この節](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration)を参照してください。

## 開発者コンソールを使用したプレビューのデバッグ {#debugging-preview-using-the-developer-console}

開発者コンソールを使用してプレビュー層をデバッグするには、次の手順に従います。

* [開発者コンソール](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)で、「**-- すべてのプレビュー --**」または名前に **prev** を含む実稼動環境を選択します。
* プレビューインスタンスの関連情報を生成します。
お使いの環境の URL を取得する方法の詳細については、[環境の管理](/help/implementing/cloud-manager/manage-environments.md)を参照してください。
