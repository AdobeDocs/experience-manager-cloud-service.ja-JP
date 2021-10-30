---
title: アセットワークフロー移行ツール
description: アセットワークフロー移行ツール
exl-id: 18490295-ead6-4691-8983-a6d4054e4264
source-git-commit: d443ab32e5d2dddded58693483a2bda825ea3048
workflow-type: ht
source-wordcount: '276'
ht-degree: 100%

---

# アセットワークフロー移行ツール {#asset-workflow-migration}

アセットワークフロー移行ツールを使用すると、アセット処理ワークフローを AEM のオンプレミスデプロイメントまたは AMS デプロイメントから処理プロファイルおよび OSGi 設定に自動的に移行して AEM Assets as a Cloud Service で使用できるようになります。

## はじめに {#introduction}

ここでは、アセットワークフロー移行ツールに関するリソースと実装の詳細について説明します。

このユーティリティを使用すると、AEM 開発者は、既存の AEM アセット処理ワークフローを AEM as a Cloud Service に移行できます。

## サポートされるワークフロー {#migration-support-for-workflows}

ワークフローは、様々なレベルの移行サポートを備えています。こちらの[特定のワークフローのリスト](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties)を参照してください。ワークフローは、提供されるサポートに基づいて次のカテゴリに分類されます。アドビでは、`SUPPORTED`、`REQUIRED`、または `OPTIONAL` カテゴリに一覧表示されているワークフローの移行がサポートされています。他のカテゴリで説明されているワークフロー手順はサポートされていません。

* `SUPPORTED`：[!DNL Experience Manager Assets] as a Cloud Service でサポートされる機能です。
* `OPTIONAL`：[!DNL Experience Manager Assets] as a Cloud Service のオプション機能です。
* `REQUIRED`：ワークフローに追加される必須の手順です。
* `UNNECESSARY`：機能は、 [!DNL Experience Manager Assets] as a Cloud Service で必要ではありません。
* `NUI_OOTB`：[アセット計算サービス](/help/assets/asset-microservices-configure-and-use.md)が提供する機能です。
* `DMS7_OOTB`：デフォルトの [!DNL Dynamic Media] コネクタで提供される機能です。
* `NUI_MIGRATED`：[アセット計算サービスの処理プロファイル](/help/assets/asset-microservices-configure-and-use.md)に移行済みです。
* `UNSUPPORTED`：現在、[!DNL Experience Manager Assets] as a Cloud Service ではサポートされていません。

## アセットワークフロー移行ツールの使用 {#use-workflow-migrator}

* **[!DNL Adobe I/O]CLI**：`aio-cli-plugin-aem-cloud-service-migration`（[!DNL Adobe I/O] CLI の [!DNL Experience Manager] as a [!DNL Cloud Service] コードリファクタリングプラグイン）を介してアセットワークフロー移行ツールを使用することをお勧 めします。このプラグインのインストールおよび使用方法については、[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction) を参照してください。

* **スタンドアロンユーティリティ**：アセットワークフロー移行ツールはスタンドアロンユーティリティとして実行することもできます。ソースからのコードのインストールとビルドについては、[Git リソース： [!DNL Experience Manager Assets] as a [!DNL Cloud Service] - Workflow Migration Tool](https://github.com/adobe/aem-cloud-migration) を参照してください。
