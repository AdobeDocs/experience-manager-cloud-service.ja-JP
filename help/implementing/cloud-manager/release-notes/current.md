---
title: Cloud Manager 2025.5.0 のリリースノート
description: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.5.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 3db5ee2852fadc9c86b3a7979ce40296bbaca858
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 16%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.5.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2025.5.0 のリリースについて説明します。

[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2025.5.0 のリリース日は 2025年5月8日木曜日（PT）です。

次回のリリース予定は 2025年6月5日木曜日（PT）です。

## 新機能 {#what-is-new}

### Edge Delivery Services用にワンクリックでコンテンツソースを設定

Adobe Experience Manager（AEM）Edge Delivery Servicesを使用すると、高速でグローバルに分散したエッジネットワークを使用して、Google Drive、SharePoint、AEM自体など複数のソースからコンテンツを配信できます。

コンテンツソースの設定は、次のように Helix 4 と Helix 5 で異なります。

| バージョン | コンテンツソースの設定方法 |
| --- | --- |
| ヘリックス 4 | YAML ファイル （`fstab.yaml`） |
| ヘリックス 5 | 設定サービス API （`fstab.yaml`** なし） |

この記事では、両方のバージョンに対する包括的な設定手順、例および検証手順を説明します。

**事前準備**

[Cloud ManagerでEdge Deliveryを 1 回クリック ](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site) を使用する場合、サイトは 1 つのリポジトリーを持つ Helix 5 になります。 Helix 5 の手順に従い、提供された Helix 4 YAML バージョンの手順をフォールバックとして使用します。

**Helix のバージョンの確認**

* ヘリックス 4 - プロジェクトに `fstab.yaml` ファイルが含まれています。
* ヘリックス 5 - プロジェクトは `fstab.yaml` を使用しており *Edge Delivery Services UI または API を使用して設定されています* 使用していません）。

それでも不明な場合は、リポジトリメタデータを確認するか、管理者に問い合わせてください。

#### Helix 4 のコンテンツソースの設定

Helix 4 では、fstab.yaml ファイルでサイトのコンテンツソースを定義します。 GitHub リポジトリのルートにあるこのファイルは、URL パスのプレフィックス（マウントポイントと呼ばれます）を外部コンテンツソースにマッピングします。 典型的な例を次に示します。

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

この例は説明用です。 実際の URL は、Google ドライブフォルダー、SharePoint ディレクトリ、AEM パスなどのコンテンツソースを指している必要があります。

**ヘリックス 4 のコンテンツソースを設定するには：**

手順は、使用するソースシステムによって異なります。

* **Google Drive**

   1. Google Drive フォルダーを作成します。
   1. フォルダーを `helix@adobe.com` と共有します。
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

   1. AEM コンテンツのパスを特定します。
   1. 次に示すように、AEM コンテンツの書き出し URL を使用します。

      ```yaml
      mountpoints:
        /: https://author.<your-aem-instance>.com/bin/franklin.delivery/<org>/<repo>/main
      ```

   1. 変更をコミットして GitHub にプッシュします。

##### 検証

* AEM Sidekick Chrome拡張機能を使用して、**プレビュー**/**公開**/**ライブサイトをテスト** をクリックします。
* URL を検証：`https://main--<repo>--<org>.hlx.page/`

#### Helix 5 のコンテンツソースの設定

ヘリックス 5 は repoless で `fstab.yaml` を使用せず、同じディレクトリを共有する複数のサイトをサポートします。 設定は、Configuration Service API またはEdge Delivery Services UI を通じて管理されます。 設定は、リポジトリーレベルではなく、サイトレベルで行います。

概念上の違いは次のとおりです。

| 項目 | ヘリックス 4 | ヘリックス 5 |
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

1. 応答を検証します（想定：HTTP 200 OK）。

##### 検証

* AEM Sidekick Chrome拡張機能を使用して、**プレビュー**/**公開**/**ライブサイトをテスト** をクリックします。
* URL を検証：`https://main--<repo>--<org>.aem.page/`
* （オプション）次の `GET` API 呼び出しを使用して、現在の設定を調べます。

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```

<!--
* **AI-powered build summaries now available for internal use**

    Internal users can now use AI-powered build summaries to simplify build log analysis. The feature provides actionable recommendations and helps identify the root causes of build failures.

    ![Build Summary dialog box](/help/implementing/cloud-manager/release-notes/assets/build-summary.png)
-->


## 早期導入プログラム {#early-adoption}

Cloud Managerの早期導入プログラムに参加すると、一般リリース前に今後の機能を独占的に利用できます。

現在、次の早期導入の機会があります。

### Edge Delivery パイプラインを追加 {#add-eds-pipeline}

Edge Delivery Servicesで作成されたサイトで **パイプライン** がサポートされるようになり、Cloud Service環境だけでなく、この機能が拡張されました。 **パイプライン** を使用して、トラフィックフィルタリングルールや Web アプリケーションファイアウォール（WAF）設定などの設定を管理できます（該当する場合）。 [ サポートされる設定 ](/help/operations/config-pipeline.md#configurations) を参照してください。

<!-- ![Add Edge Delivery pipeline in Add Pipeline drop-down list](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png) -->

この新機能のテストやフィードバックの提供に関心がある場合は、Adobe IDに関連付けられたメールアドレスから [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) にメールを送信してください。

### 独自の Git の導入 – Azure DevOps をサポート {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

最新の Azure DevOps リポジトリと従来の VSTS （Visual Studio Team Services）リポジトリの両方をサポートすることで、Azure DevOps Git リポジトリをCloud Managerにオンボーディングできるようになりました。

* Edge Delivery Servicesのユーザーは、オンボーディングされたリポジトリーを使用して、サイトコードを同期およびデプロイできます。
* AEM as a Cloud ServiceおよびAdobe Managed Services（AMS）のユーザーは、リポジトリをフルスタックパイプラインとフロントエンドパイプラインの両方にリンクできます。

コード品質パイプラインを通じた追加のパイプラインタイプとプルリクエスト検証のサポートは、近日中に提供されます。

[Cloud Manager でのプライベートリポジトリの追加](/help/implementing/cloud-manager/managing-code/external-repositories.md)を参照してください。

![リポジトリを追加ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) にメールを送信します。 使用する Git プラットフォームと、プライベート／パブリックまたはエンタープライズリポジトリ構造のいずれを使用するかを必ず含めてください。

#### 独自の Git の導入に関するよくある質問（FAQ）

| 質問 | 回答 |
|---|---|
| *必要に応じてプロジェクトをAdobeの管理による Git リポジトリに戻すには、どうすればよいですか？* | 切り替えは簡単です。 Adobe リポジトリを指すように [ パイプラインを更新 ](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) し、外部リポジトリが不要になった場合は削除します。 |
| *異なる環境（実稼動以外と実稼動など）に異なるリポジトリーを設定して、最初に実稼動以外の環境でテストできるようにすることはできますか？* | はい。個別の環境用に異なるリポジトリを設定できます。 例えば、開発パイプラインまたはコード品質パイプラインは外部リポジトリーを指し、実稼動パイプラインはAdobe リポジトリーに接続されたままにすることができます。 この設定中は、2 つのリポジトリ間の同期ジョブがアクティブのままであることを確認してください。 |
| *IP許可リストなどの既存の設定は引き続き機能しますか？* | はい、既存の IP許可リストは引き続き通常どおり機能します。 ただし、外部 Git リポジトリがファイアウォールで保護されている場合は、必要な [Adobe IP アドレスを許可リストに追加する必要があります ](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *すべての GitLab リポジトリ URL が機能しますか？ 使用するリポジトリ URL は、形式 `https://gitlab_dedicated_url.com/path/repo-name.git` に従いますが、この形式はドキュメントの例とは異なります。* | はい。API V3 または V4 をサポートする任意の GitLab リポジトリーがサポートされます。これには、[Cloud Managerへの外部リポジトリーの追加 ](/help/implementing/cloud-manager/managing-code/external-repositories.md) （`https://git-vendor-name.com/org-name/repo-name.git`）に記載されているように、セルフホスト型の GitLab URL が含まれます。 |


<!--
## Bug fixes

* Issue

* Issue

* Issue
-->

<!-- ## Known issues {#known-issues} -->

