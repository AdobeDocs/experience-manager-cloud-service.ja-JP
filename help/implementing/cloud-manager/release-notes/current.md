---
title: Cloud Manager 2025.6.0 のリリースノート
description: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.6.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 169de7971fba829b0d43e64d50a356439b6e57ca
workflow-type: ht
source-wordcount: '954'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.6.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2025.6.0 のリリースについて説明します。

[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2025.6.0 のリリース日は 2025年6月5日（PT）です。

次回のリリース予定は 2025年7月10日（PT）です。

## 新機能 {#what-is-new}

* **ライセンスダッシュボードにEdge Delivery Services ライセンスが含まれるようになりました**

  Edge Delivery Services ライセンスの使用状況がライセンスダッシュボードに表示され、使用権限とステータスをより明確に把握できるようになりました。<!-- CMGR-67686 -->

  ![ライセンスダッシュボード](/help/implementing/cloud-manager/assets/license-dashboard.png)

  [ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md)をご覧ください。

* **Edge Delivery サイト設定が更新されました**

  **Repository URL** ではなく **Edge Delivery Origin** をリクエストすることで、Edge Delivery サイトを追加するフローが簡略化され、オンボーディングと設定がより迅速かつ直感的になりました<!-- CMGR-67686 -->

  ![「Edge Delivery サイトを追加」ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-site.png)

  [Edge Delivery サイトの追加](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)を参照してください。

* **お気に入りのパイプライン**

  このリリースでは、Cloud Manager で特定のパイプラインをピン留めしてお気に入りとしてマークし、「**パイプライン**」ページのリストの上部に表示できるようになりました。この機能強化により、頻繁にアクセスするパイプラインをより容易に見つけて実行しやすくなっています。<!-- CMGR-68293 -->

  ![お気に入りとしてマークされたパイプライン](/help/implementing/cloud-manager/release-notes/assets/pipeline-favorites.png)*お気に入りとしてマークされた 2 つのパイプライン。*

  [パイプラインのお気に入りをマークする](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipeline-favorites)を参照してください。


## Private Beta プログラム {#private-beta-program}

Cloud Manager の Private Beta プログラムに参加すると、一般リリース前の新機能に特別にアクセスできます。

現在利用可能な Private Beta プログラムの機会は、次のとおりです。


### 特殊なテスト環境 {#specialized-test-environment}

Cloud Manager は、**専用のテスト環境**&#x200B;という新しい追加の環境タイプをサポートするようになりました。この環境は、運用開始前に、チームが実稼動環境に近い条件下で機能を検証するのに役立つように設計されています。この環境タイプは、*実稼動環境とステージング環境*、*開発環境*&#x200B;または&#x200B;*迅速な開発環境*&#x200B;環境とは異なり、高度な検証シナリオを実行することに焦点を当てたスペースが提供されます。

[専用のテスト環境の追加](/help/implementing/cloud-manager/specialized-test-environment.md)を参照してください。

![「専用のテスト環境」ラジオボタンが選択された「環境を追加」ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

この新機能をテストしてフィードバックを共有することに関心がある場合は、Adobe ID に関連付けられたメールアドレスから [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com)にメールを送信してください。


### Bring Your Own Git (BYOG) - Azure DevOps でサポート開始 {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Azure DevOps Git リポジトリを Cloud Manager にオンボードできるようになりました。これは、最新の Azure DevOps リポジトリとレガシー VSTS（Visual Studio Team Services）リポジトリの両方に対応しています。

* Edge Delivery Services のユーザーは、オンボードされたリポジトリを使用して、サイトコードを同期およびデプロイできます。
* AEM as a Cloud Service および Adobe Managed Services（AMS）のユーザーは、リポジトリをフルスタックパイプラインとフロントエンドパイプラインの両方にリンクできます。

追加のパイプラインタイプと、コード品質パイプラインを通じたプルリクエスト検証のサポートは、近日リリース予定です。

[Cloud Manager でのプライベートリポジトリの追加](/help/implementing/cloud-manager/managing-code/external-repositories.md)を参照してください。

![リポジトリを追加ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) にメールを送信します。 使用する Git プラットフォームと、プライベート／パブリックまたはエンタープライズリポジトリ構造のいずれを使用するかを必ず含めてください。


**BYOG に関するよくある質問**

| 質問 | 回答 |
|---|---|
| *必要に応じてプロジェクトを Adobe の管理による Git リポジトリに戻すには、どうすれば良いですか？* | 戻すのは簡単です。[パイプラインを更新](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)して Adobe リポジトリを指し、外部リポジトリが不要になった場合は削除します。 |
| *異なる環境（実稼動と実稼動以外など）に異なるリポジトリを設定して、最初に実稼動以外の環境でテストできるようにすることはできますか？* | はい、個別の環境用に異なるリポジトリを設定できます。例えば、開発パイプラインまたはコード品質パイプラインは外部リポジトリを指し、実稼動パイプラインは Adobe リポジトリに接続されたままにすることができます。この設定中は、2 つのリポジトリ間の同期ジョブがアクティブのままであることを確認してください。 |
| *IP 許可リストなどの既存の設定は引き続き機能しますか？* | はい、既存の IP 許可リストは引き続き通常どおり機能します。ただし、外部 Git リポジトリがファイアウォールで保護されている場合は、必要な [Adobe IP アドレスを許可リストに追加する必要があります](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *すべての GitLab リポジトリ URL が機能しますか？使用するリポジトリ URL は、形式 `https://gitlab_dedicated_url.com/path/repo-name.git` に従いますが、この形式はドキュメントの例とは異なります。* | はい、API V3 または V4 をサポートするどの GitLab リポジトリもサポートされます。これには、[Cloud Manager への外部リポジトリの追加 ](/help/implementing/cloud-manager/managing-code/external-repositories.md)（`https://git-vendor-name.com/org-name/repo-name.git`）に記載されているようなセルフホスト型の GitLab URL が含まれます。 |


#### アクセストークンを管理{#manage-access-tokens}

Cloud Managerで「**アクセストークンの管理**」を使用して、外部 BYOG リポジトリ (GitHub Enterprise、GitLab、Bitbucket、Azure DevOps など) に関連付けられたアクセストークンを表示、名前変更、削除します。

[アクセストークンを管理](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)をご覧ください。

この新機能をテストしてフィードバックを共有することに関心がある場合は、Adobe ID に関連付けられたメールアドレスから [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) にメールを送信してください。


### Edge Delivery 設定パイプラインを追加する {#add-eds-pipeline}

Edge Delivery Services を使用して作成されたサイトで設定パイプラインがサポートされるようになりました。これにより、Cloud Service 環境以外でもこの機能を利用できます。**設定パイプライン**&#x200B;を使用すると、トラフィックフィルタリングルールや web アプリケーションファイアウォール（WAF）設定などの設定を管理できます（該当する場合）。[サポートされている設定](/help/operations/config-pipeline.md#configurations)を参照してください。

![「パイプラインを追加」ドロップダウンリストの「Edge Delivery パイプラインを追加」](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png)*「**プログラムの概要**」ページ、「**パイプライン**」カードからのEdge Delivery パイプラインの追加。*

![「Edge Delivery パイプラインを追加」ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png)*「Edge Delivery パイプラインを追加」ダイアログボックス。*

この新機能をテストしてフィードバックを共有したい場合は、Adobe ID に関連付けられたメールアドレスから [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) にメールを送信してください。


## バグ修正

* 以前に `HIBERNATED` とマークされたサンドボックス環境はその状態のままではなくなり、パイプラインの実行やデプロイメントを期待どおりに続行できます。<!-- CMGR-67705 -->
* AEM Cloud Managerは、お客様のアーティファクトを取得する際に、409 エラー（競合）が原因で発生した Maven ビルドエラーをお客様が原因のエラーに正しくマッピングするようになりました。この変更により、内部エラーとお客様の環境の設定に関連する問題が区別され、エラーメッセージが改善されます。<!-- CMGR-66673 -->


<!-- ## Known issues {#known-issues} -->

