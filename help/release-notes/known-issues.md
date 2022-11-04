---
title: 既知の問題
description: Adobe Experience Manager as a Cloud Service の既知の問題
exl-id: 897b944a-d320-4d21-91f4-2cd3da6179b1
source-git-commit: 755c0072148ad73486df2ccfed69248b9d73ec2a
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 100%

---

# 既知の問題 {#known-issues}

この記事では、[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] オファリングの既知の問題を掲載しています。このリストは、[!DNL Experience Manager] が継続的にリリースされるたびに改訂および更新されます。

既知の問題について詳しくは、 [サポートまでお問い合わせ](https://experienceleague.adobe.com/?lang=ja&amp;support-solution=Experience+Manager#support) ください。

<!-- 
## Platform {#platform}
-->

## Sites {#sites}

[!DNL Sites] の既知の問題の一部は次のとおりです。

* GraphQL IDE では、[永続クエリのキャッシュを管理](/help/headless/graphql-api/graphiql-ide.md##managing-cache)できます。
   * ユーザーがダイアログでこれらの値を変更していない場合、初回保存時にヘッダー用に保存された値が（ デフォルト値でなく）`0` に設定されます。
   * 後続の保存では、値は正しく保存されます。
   * このため、ユーザーはヘッダーを 2 回保存する必要があります。

## [!DNL Assets] {#assets}

<!-- Jira label: assets-cloud-known-issues -->

[!DNL Assets] の既知の問題の一部は次のとおりです。

* **ダウンロード**：空のフォルダーをダウンロードする場合、[!DNL Experience Manager] は、ZIP アーカイブの作成に関する成功メッセージを伝えますが、アーカイブは作成されません。

* **メタデータスキーマ**：アセット評価ウィジェットが JSP コンパイルエラーを引き起こしていました。メタデータスキーマから削除されました。 <!-- CQ-4282865, CQ-4284633 -->

また、 [注目すべき変更点 [!DNL Experience Manager Assets]](/help/assets/assets-cloud-changes.md) も参照してください。

<!-- This content was added at GA. Not sure if we should continue to have this commitment about upcoming features/enh. in the docs. Commenting it for now.

### Upcoming Assets capabilities {#upcoming-assets-capabilities}

A few capabilities of Adobe Experience Manager Assets that depend on foundation capabilities, which are not yet available in the Experience Manager as a Cloud Service deployment architecture, are expected to be enabled at a later stage:

* Capabilities not enabled at this stage due to dependency on Commerce Integration Framework APIs:
  * Photoshoot workflow models.
  * Product information tab in the asset properties user interface is not populated.

* Capabilities not enabled at this stage due to dependency on InDesign Server integration:
  * Asset Templates and Asset Catalogs.
  * Multi-page preview of Adobe InDesign files.
-->

>[!MORELIKETHIS]
>
>* [主な変更点 [!DNL Experience Manager]](aem-cloud-changes.md)
>* [廃止される機能および削除された機能](deprecated-removed-features.md)
>* [リリースノート](home.md)

