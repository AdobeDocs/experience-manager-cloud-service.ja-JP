---
title: コンテンツのプレビュー
description: AEM プレビューサービスを使用して、運用を開始する前にコンテンツをプレビューする方法を説明します。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 78c5649c6b9c04cb459f5730161affeb452c916c
workflow-type: ht
source-wordcount: '387'
ht-degree: 100%

---

# コンテンツのプレビュー {#previewing-content}

>[!NOTE]
>
>2021 年 8 月 3 日より前に作成された環境でプレビュー機能を有効にするには、環境のバージョンが AEM 2021.05.5368.20210529T101701Z 以上であることを確認してから、顧客が開始したパイプラインを実行します。

AEM は、Web サイトがパブリッシュ環境になって一般公開される前に、デベロッパーとコンテンツ作成者が Web サイトの最終エクスペリエンスをプレビューするように設計された、サイトプレビューサービスを提供しています。

これにより、ページトランジションやその他のパブリッシュ側のコンテンツなど、オーサー環境からは見えないページエクスペリエンスのプレビューが容易になります。

[プレビューサービスへのアクセス](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)も参照してください。

## プレビュー用のコンテンツの公開 {#publishing-content-to-preview}

プレビューサービスにコンテンツを公開するには、次のように公開管理の UI を使用します。

1. サイトコンソールでプレビュー用に送信する 1 つ以上のページを選択し、「**公開を管理**」ボタンをクリックします
1. 次のウィザードで、宛先として「**プレビュー**」を選択します

   ![管理対象公開](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 「**次へ**」をクリックし、「**公開**」をクリックして確定します。

1. プレビュー環境のコンテンツにアクセスするための URL がダイアログに表示されます。

   また、プレビューコンテンツを表示するには、実稼動インスタンスのパブリッシュ URL に **preview** を付加することもできます。

   URL は、次のように構成されます。

   ```
   https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
   ```

お使いの環境の URL を取得する方法の詳細については、[環境の管理](/help/implementing/cloud-manager/manage-environments.md)を参照してください。

コンテンツは、agentId パラメーターをプレビューに設定した[コンテンツツリーの公開ワークフロー](/help/operations/replication.md#publish-content-tree-workflow)を使用するか、AgentFilter をプレビュー用に設定した[レプリケーション API](/help/operations/replication.md#replication-api) を使用して、プレビューに公開することもできます。

## プレビュー層の OSGi 設定の指定 {#configuring-osgi-settings-for-the-preview-tier}

プレビュー層の OSGI プロパティ値は、パブリッシュ層から継承されますが、プレビュー層の値は、サービスパラメーターの値を「preview」に設定する環境固有の値を使用して、パブリッシュ層と区別することができます。次の例は、統合エンドポイントの URL を決定する OSGi プロパティを示しています。

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
