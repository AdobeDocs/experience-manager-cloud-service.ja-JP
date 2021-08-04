---
title: コンテンツのプレビュー
description: AEM Preview Serviceを使用して、運用を開始する前にコンテンツをプレビューする方法を説明します。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 78c5649c6b9c04cb459f5730161affeb452c916c
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# コンテンツのプレビュー {#previewing-content}

>[!NOTE]
>
>2021年8月3日より前に作成された環境でプレビュー機能を有効にするには、環境のバージョンがAEM 2021.05.5368.20210529T101701Z以上であることを確認してから、顧客が開始するパイプラインを実行します。

AEMは、開発者とコンテンツ作成者が、パブリッシュ環境に到達する前にWebサイトの最終エクスペリエンスをプレビューし、公開されるように設計された、サイトプレビューサービスを提供します。

ページトランジションや他のパブリッシュ側のみのコンテンツなど、オーサー環境からは見えないページエクスペリエンスのプレビューを容易にします。

また、[Previewサービスへのアクセス](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)についてもお読みください。

## プレビュー用のコンテンツの公開 {#publishing-content-to-preview}

次のように、Managed Publication UIを使用して、プレビューサービスにコンテンツを公開できます。

1. サイトコンソールでプレビュー用に送信する1つ以上のページを選択し、「**公開を管理**」ボタンをクリックします
1. 次のウィザードで、宛先として「**プレビュー**」を選択します

   ![管理公開](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 「**次へ**」をクリックし、「**公開**」をクリックして確定します。

1. プレビュー環境のコンテンツにアクセスするためのURLがダイアログに表示されます。

   また、プレビューコンテンツを表示するには、実稼動インスタンスのパブリッシュURLに&#x200B;**プレビュー**&#x200B;を追加することもできます。

   URLは、次のように記述します。

   ```
   https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
   ```

お使いの環境のURLを取得する方法の詳細については、[環境の管理](/help/implementing/cloud-manager/manage-environments.md)を参照してください。

また、[コンテンツツリーの公開ワークフロー](/help/operations/replication.md#publish-content-tree-workflow)を使用して、agentIdパラメーターをプレビューに設定して、または[レプリケーションAPI](/help/operations/replication.md#replication-api)を使用し、プレビュー用に設定したAgentFilterを使用して、コンテンツを公開できます。

## プレビュー層のOSGi設定の指定 {#configuring-osgi-settings-for-the-preview-tier}

プレビュー層のOSGIプロパティ値は、パブリッシュ層から継承されますが、サービスパラメーターを値「preview」で設定する環境固有の値を使用して、プレビュー層値をパブリッシュ層と区別できます。 次の例で、統合エンドポイントのURLを決定するOSGiプロパティを見てみましょう。

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

詳しくは、OSGi設定ドキュメントの[この節](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration)を参照してください。

## 開発者コンソールを使用したプレビューのデバッグ {#debugging-preview-using-the-developer-console}

開発者コンソールを使用してプレビュー層をデバッグするには、次の手順に従います。

* [開発者コンソール](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)で、「**— すべてのプレビュー —**」または名前に&#x200B;**prev**&#x200B;を含む実稼動環境を選択します。
* プレビューインスタンスの関連情報を生成する
お使いの環境のURLを取得する方法の詳細については、[環境の管理](/help/implementing/cloud-manager/manage-environments.md)を参照してください。
