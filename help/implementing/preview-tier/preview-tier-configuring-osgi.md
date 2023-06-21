---
title: プレビュー層の OSGi 設定の指定
description: 運用を開始する前にコンテンツをプレビューするようにAEMプレビューサービスを設定する方法について説明します。
exl-id: 1200bb17-8a3c-4e41-85f4-ed2334b61f69
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 58%

---

# プレビュー層の OSGi 設定の指定 {#configure-osgi-preview-tier}

AEMは、Web サイトのパブリッシュ環境に到達する前に開発者とコンテンツ作成者が Web サイトの最終エクスペリエンスをプレビューし、公開できる Sites プレビューサービスを提供します。

オーサー環境からは表示されない様々なエクスペリエンスを容易にプレビューできます。 例えば、ページ切り替え、エクスペリエンスフラグメント、その他の公開側のみのコンテンツなどです。

プレビュー層の OSGi プロパティ値は、パブリッシュ層から継承されます。ただし、`service` パラメーターを `preview` 値に設定することで、プレビュー層の値をパブリッシュ層と区別することができます。

>[!NOTE]
>
>プレビュー環境について詳しくは、[環境の管理](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)のドキュメントを参照してください。

## プレビュー層の OSGi 設定の指定 {#configuring-osgi-settings-for-the-preview-tier}

次の OSGi プロパティの例では、統合エンドポイントの URL を決定しています。

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

開発者コンソールを使用してプレビュー層をデバッグできるようにするには、次の手順に従います。

* [開発者コンソール](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)で、「**-- すべてのプレビュー --**」または名前に **prev** を含む実稼動環境を選択します。
* プレビューインスタンスの関連情報を生成します。
お使いの環境の URL を取得する方法の詳細については、[環境の管理](/help/implementing/cloud-manager/manage-environments.md)を参照してください。
