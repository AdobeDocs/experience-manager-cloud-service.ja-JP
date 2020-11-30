---
title: アセットワークフロー移行ツール
description: 'アセットワークフロー移行ツール '
translation-type: tm+mt
source-git-commit: 3a438de3c460d4dc5a8b8617f0ec0eefc56f1665
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 100%

---


# アセットワークフロー移行ツール {#asset-workflow-migration}

アセットワークフロー移行ツールを使用すると、アセット処理ワークフローを AEM のオンプレミスデプロイメントまたは AMS デプロイメントから処理プロファイルおよび OSGi 設定に自動的に移行して AEM Assets as a Cloud Service で使用できるようになります。

## 概要 {#introduction}

ここでは、アセットワークフロー移行ツールに関するリソースと実装の詳細について説明します。

このユーティリティを使用すると、AEM 開発者は、既存の AEM アセット処理ワークフローを AEM as a Cloud Service に移行できます。

## サポートされるワークフロー {#migration-support-for-workflows}

ワークフローは、さまざまなレベルの移行サポートを備えています。こちらの[特定のワークフローのリスト](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties)を参照してください。ワークフローは、提供されるサポートに基づいて次のカテゴリに分類されます。アドビでは、`SUPPORTED`、`REQUIRED`、または `OPTIONAL` カテゴリに一覧表示されているワークフローの移行がサポートされています。他のカテゴリで説明されているワークフロー手順はサポートされていません。

* `SUPPORTED`：[!DNL Experience Manager Assets] as a Cloud Service でサポートされる機能です。
* `OPTIONAL`：[!DNL Experience Manager Assets] as a Cloud Service のオプション機能です。
* `REQUIRED`：ワークフローに追加される必須の手順です。
* `UNNECESSARY`：機能は、 [!DNL Experience Manager Assets] as a Cloud Service で必要ではありません。
* `NUI_OOTB`：[アセット計算サービス](/help/assets/asset-microservices-configure-and-use.md)が提供する機能です。
* `DMS7_OOTB`：デフォルトの [!DNL Dynamic Media] コネクタで提供される機能です。
* `NUI_MIGRATED`：[アセット計算サービスの処理プロファイル](/help/assets/asset-microservices-configure-and-use.md)に移行済みです。
* `UNSUPPORTED`：現在、[!DNL Experience Manager Assets] as a Cloud Service ではサポートされていません。

## アセットワークフロー移行ツールのインストール {#installing-tool}

ソースのインストールとソースコードのビルドについては、**[Git リソース：AEM Assets as a Cloud Service - Workflow Migration Tool](https://github.com/adobe/aem-cloud-migration)** を参照してください。
