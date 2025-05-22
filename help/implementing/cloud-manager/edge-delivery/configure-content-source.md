---
title: コンテンツSourceの設定
description: Edge Delivery サイトのコンテンツソースを設定する方法について説明します。 Helix 4 アーキテクチャでは「fstab.yaml」を使用するか、Cloud Manager（または Configuration Service API）のガイド付きウィザードを Helix 5 アーキテクチャで使用します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: f82eafc0-03d0-4c69-9b28-e769a012531b
source-git-commit: 71618a5603328990603db2ee7554048c9020a883
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 40%

---

# Edge Delivery Services用にワンクリックでコンテンツソースを設定 {#config-content-source}

>[!IMPORTANT]
>
>*Helix* は、ドキュメントベースのオーサリングでAEM Sitesを機能させる基盤アーキテクチャの内部名です。 機能名や製品名ではありません。 この記事では、*Helix* とは、Edge Delivery Sites で使用されるアーキテクチャバージョンを指します。 Helix 5 は基礎となるアーキテクチャの現在のバージョンです。Helix 4 は以前のバージョンです。

Adobe Experience Manager（AEM）Edge Delivery Services を使用すると、高速でグローバルに分散した Edge Network を使用して、Google Drive、SharePoint、AEM 自体などの複数のソースからコンテンツを配信できます。

コンテンツソースの設定は、次の 2 つのアーキテクチャバージョンによって異なります。

| バージョン | コンテンツソースの設定方法 |
| --- | --- |
| Helix 4 | YAML ファイル（`fstab.yaml`） |
| Helix 5 | 設定サービス API（*`fstab.yaml`* は使用しない） |

この記事では、両方のバージョンに対する包括的な設定手順、例および検証手順を説明します。

**事前準備**

[Cloud ManagerでEdge Deliveryを 1 回クリック ](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site) を使用する場合、サイトでは 1 つのリポジトリーで Helix 5 が使用されます。 [Helix 5 の手順に従って ](#config-helix5) 指示の提供された Helix 4 YAML バージョンをフォールバックとして使用します。

**Helix のバージョンの確認**

* Helix 4 - プロジェクトに `fstab.yaml` ファイルが含まれます。
* らせん 5 - プロジェクト *使用していません*`fstab.yaml` および [Cloud Managerを通じて、ガイド付きウィザード ](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md) または API を使用して設定されました。

まだ不明な場合は、リポジトリメタデータを確認するか、管理者に問い合わせてください。

## Helix 4 のコンテンツソースの設定

Helix 4 では、`fstab.yaml` ファイルでサイトのコンテンツソースを定義します。 GitHub リポジトリのルートにあるこのファイルは、URL パスのプレフィックス（マウントポイントと呼ばれます）を外部コンテンツソースにマッピングします。 典型的な例を次に示します。

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

上記の例は説明用です。 実際の URL は、Google ドライブフォルダー、SharePoint ディレクトリ、AEM パスなどのコンテンツソースを指している必要があります。

**ヘリックス 4 のコンテンツソースを設定するには：**

手順は、使用するソースシステムによって異なります。

* **Google Drive**

   1. Google Drive フォルダーを作成します。
   1. `helix@adobe.com` とフォルダーを共有します。
   1. 共有可能なフォルダーリンクを取得します。
   1. 次に示すように、`fstab.yaml` を更新します。

      ```yaml
      mountpoints: 
          /: https://drive.google.com/drive/folders/<folder-id>
      ```

   1. 変更をコミットして GitHub にプッシュします。

* **SharePoint**

   1. SharePoint フォルダーまたはドキュメントライブラリを作成します。
   1. `helix@adobe.com` とアクセスを共有します。
   1. フォルダーの URL を取得します。
   1. 次に示すように、`fstab.yaml` を更新します。

      ```yaml
      mountpoints:
        /: https://<tenant>.sharepoint.com/sites/<site>/Shared%20Documents/<folder>
      ```

   1. 変更をコミットして GitHub にプッシュします。

* **AEM**

   1. AEM コンテンツパスを特定します。
   1. 次に示すように、AEM コンテンツの書き出し URL を使用します。

      ```yaml
      mountpoints:
        /: https://author.<your-aem-instance>.com/bin/franklin.delivery/<org>/<repo>/main
      ```

   1. 変更をコミットして GitHub にプッシュします。

### 検証

* AEM Sidekick Chrome 拡張機能を使用して、**プレビュー**／**公開**／**ライブサイトをテスト**&#x200B;の順にクリックします。
* URL を検証：`https://main--<repo>--<org>.hlx.page/`

## Helix 5 のコンテンツソースの設定 {#config-helix5}

ヘリックス 5 は repoless で `fstab.yaml` を使用せず、同じディレクトリを共有する複数のサイトをサポートします。 設定は、Configuration Service API またはEdge Delivery Sites ユーザーインターフェイスで管理されます。 設定は、リポジトリレベルではなく、サイトレベルで行います。

概念上の違いは次のとおりです。

| 項目 | Helix 4 | Helix 5 |
| --- | --- | --- |
| 設定 | `fstab.yaml` で完了 | YAML の代わりに API または UI を通じて実行します。 |
| マウントポイント | `fstab.yaml` で定義されます。 | 必須ではありません。 ルートは暗黙的に理解されています。 |

**ヘリックス 5 のコンテンツソースを設定するには：**

1. 設定サービス API を使用し、API キーまたはアクセストークンを使用して認証します。
1. 次の `PUT` API 呼び出しを行います。

   ```bash {.line-numbering}
   PUT /api/{program}/{programId}/site/{siteId}
   Content-Type: application/json
   
   {
     "sitename": "my-site",
     "branchName": "main",
     "version": "v5",
     "repo": "my-content-repo-link"
   }
   ```

1. 応答を検証します（期待される結果：HTTP 200 OK）。

### 検証

* AEM Sidekick Chrome 拡張機能を使用して、**プレビュー**／**公開**／**ライブサイトをテスト**&#x200B;の順にクリックします。
* URL を検証：`https://main--<repo>--<org>.aem.page/`
* （オプション）次の `GET` API 呼び出しを使用して、現在の設定を調べます。

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```
