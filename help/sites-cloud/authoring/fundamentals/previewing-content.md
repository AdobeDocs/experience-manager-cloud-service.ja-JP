---
title: コンテンツのプレビュー
description: AEMプレビューサービスを使用して、運用を開始する前にコンテンツをプレビューする方法を説明します。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: e70e6ee055c2542752e66e53aa70a9378b1bc5c0
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 30%

---


# コンテンツのプレビュー {#previewing-content}

AEMオファーの Sites プレビューサービスを使用すると、開発者やコンテンツ作成者は、Web サイトがパブリッシュ環境に到達する前に Web サイトの最終的なエクスペリエンスをプレビューし、公開できます。

ページトランジションや他のパブリッシュ側のみのコンテンツなど、オーサー環境からは表示されないページエクスペリエンスのプレビューを容易にします。

プレビュー環境について詳しくは、ドキュメントを参照してください。 [環境の管理。](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## プレビュー用のコンテンツの公開 {#publishing-content-to-preview}

コンテンツをプレビューサービスに公開するには、 **管理された公開** UI

1. サイトコンソールで、プレビュー用に送信する 1 つ以上のページを選択し、 **公開を管理** ボタン
1. 次のウィザードで、宛先として「**プレビュー**」を選択します

   ![管理対象公開](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 「**次へ**」をクリックし、「**公開**」をクリックして確定します。

1. プレビュー環境でコンテンツにアクセスするための URL がダイアログに表示されます。


また、ウィザードに表示される URL を使用してプレビューコンテンツを確認する場合は、の前にを追加することもできます `preview-` を実稼動インスタンスのパブリッシュ URL に追加します。

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

ドキュメントを参照 [環境の管理](/help/implementing/cloud-manager/manage-environments.md) 環境の URL を取得する方法に関する詳細。

また、 [コンテンツツリーの公開ワークフロー](/help/operations/replication.md#publish-content-tree-workflow) と `agentId` パラメータをに設定 `preview` または、 [レプリケーション API](/help/operations/replication.md#replication-api) と `AgentFilter` プレビュー用に設定されました。

## プレビュー層の OSGi 設定の指定 {#configuring-osgi-settings-for-the-preview-tier}

プレビュー層の OSGi プロパティ値は、パブリッシュ層から継承されます。 ただし、 `service` 値に対するパラメータ `preview`. 次の OSGi プロパティの例では、統合エンドポイントの URL を決定します。

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
