---
title: Cloud Manager 2025.5.0 のリリースノート
description: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.5.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 8696cf8a7e7cfc439450b34fa6fda10b38cd415e
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 24%

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

コンテンツソースの設定は、Helix 4 と Helix 5 で異なります。 両方のバージョンの違いを説明し、包括的な設定手順、例、検証手順に従います。

[ コンテンツソースの設定 ](/help/implementing/cloud-manager/edge-delivery/configure-content-source.md) を参照してください。


## 早期導入プログラム {#early-adoption}

Cloud Managerの早期導入プログラムに参加すると、一般リリース前に今後の機能を独占的に利用できます。

現在、次の早期導入の機会があります。

### Edge Delivery設定パイプラインを追加 {#add-eds-pipeline}

Edge Delivery Servicesで作成されたサイトで Config パイプラインがサポートされるようになり、Cloud Service環境だけでなく、この機能が拡張されました。 **設定パイプライン** を使用して、トラフィックフィルタリングルールや Web アプリケーションファイアウォール（WAF）設定などの設定を管理できます（該当する場合）。 [ サポートされる設定 ](/help/operations/config-pipeline.md#configurations) を参照してください。

![ パイプラインを追加ドロップダウンリストでEdge Delivery パイプラインを追加 ](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png)

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

