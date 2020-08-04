---
title: アセットワークフロー移行ツール
description: 'アセットワークフロー移行ツール '
translation-type: tm+mt
source-git-commit: 3a438de3c460d4dc5a8b8617f0ec0eefc56f1665
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 46%

---


# アセットワークフロー移行ツール {#asset-workflow-migration}

アセットワークフロー移行ツールを使用すると、アセット処理ワークフローを AEM のオンプレミスデプロイメントまたは AMS デプロイメントから処理プロファイルおよび OSGi 設定に自動的に移行して AEM Assets as a Cloud Service で使用できるようになります。

## 概要 {#introduction}

ここでは、アセットワークフロー移行ツールに関するリソースと実装の詳細について説明します。

このユーティリティを使用すると、AEM 開発者は、既存の AEM アセット処理ワークフローを AEM as a Cloud Service に移行できます。

## サポートされるワークフロー {#migration-support-for-workflows}

ワークフローは、さまざまなレベルの移行サポートを備えています。 特定のワークフローの次の [リストを参照してください](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties)。 ワークフローは、提供されるサポートに基づいて次のカテゴリに分類されます。 Adobeでは、、、またはのワークフローーに一覧表示されているカテゴリーの移行 `SUPPORTED`がサポートさ `REQUIRED`れてい `OPTIONAL` ます。 他のカテゴリーで説明されているワークフロー手順はサポートされていません。

* `SUPPORTED`: Cloud Serviceとしてサポートさ [!DNL Experience Manager Assets] れる機能。
* `OPTIONAL`: Cloud Serviceとしてのオプション機能 [!DNL Experience Manager Assets] です。
* `REQUIRED`: ワークフローに追加される必須の手順です。
* `UNNECESSARY`: 機能は、Cloud Serviceとして必要 [!DNL Experience Manager Assets] ではありません。
* `NUI_OOTB`: ア [セット計算サービスが提供する機能](/help/assets/asset-microservices-configure-and-use.md)。
* `DMS7_OOTB`: デフォルトの [!DNL Dynamic Media] コネクタで提供される機能。
* `NUI_MIGRATED`: Asset Compute Serviceの [処理プロファイルに移行済み](/help/assets/asset-microservices-configure-and-use.md)。
* `UNSUPPORTED`: 現在、Cloud Serviceとしてではサポートさ [!DNL Experience Manager Assets] れていません。

## アセットワークフロー移行ツールのインストール {#installing-tool}

ソースのインストールとソースコードのビルドについては、**[Git リソース：AEM Assets as a Cloud Service - Workflow Migration Tool](https://github.com/adobe/aem-cloud-migration)**を参照してください。
