---
title: Cloud Manager 2025.9.0 のリリースノート
description: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.9.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 2b82e3b848be828fbf8c316244031a0e06f512ca
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 89%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.9.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2025.9.0 のリリースについて説明します。

[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2025.9.0 のリリース日は 2025年9月4日木曜日（PT）です。

次回のリリース予定は 2025年10月2日木曜日（PT）です。

## 新機能 {#what-is-new}

* **Adobeが管理するドメイン検証証明書の手動更新**

  Cloud Managerまたはパブリック API からAdobeが管理するドメイン検証（DV）証明書を手動で更新して、証明書を事前に更新できるようになりました。<!-- CMGR-68738 -->

  ![SSL 証明書の更新 ](/help/implementing/cloud-manager/release-notes/assets/ssl-certificate-adobedv-renew.png)

* **プライベートリポジトリ用の Azure DevOps のサポートが追加されました**

  ドキュメントの更新には、Azure DevOps で独自の Git を取り込むための設定手順や、プルリクエストの検証が含まれています。 [Cloud Managerへの外部リポジトリの追加 ](/help/implementing/cloud-manager/managing-code/external-repositories.md) を参照してください。

* **プライベートリポジトリのプルリクエストチェック**

  Cloud Managerは、GitHub、Bitbucket、Azure DevOps、GitLab をまたいだプライベートリポジトリを使用した設定パイプラインをサポートするようになりました。 [ プライベートリポジトリのプルリクエストチェック ](/help/implementing/cloud-manager/managing-code/github-check-config.md) を参照してください。

<!--
### Staging-Only and Production-Only Pipelines {#staging-production-only-pipelines}

Support for [staging-only and production-only pipelines](/help/implementing/cloud-manager/configuring-pipelines/stage-prod-only.md) has been introduced, enabling you to split full-stack production deployment pipelines into smaller, specialized deployments.

If you are interested in testing this new feature and sharing your feedback, send an email to  `Grp-cloudmanager_splitpipelines@adobe.com` from your email address associated with your Adobe ID. -->


## Beta プログラム {#private-beta-program}

Cloud Manager の Beta プログラムに参加すると、一般リリース前の新機能に特別アクセスできます。

現在、以下の機能が利用可能です。
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

### パイプラインデプロイメントのロールバックをワンクリックで実行 {#one-click-rollback}

最新の顧客ソースコードが期待どおりに動作しない場合は、以前のデプロイメントに迅速に戻すことができます。パイプライン全体を再実行したり、コミットを手動で元に戻したりする必要はありません。<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![環境カードから顧客ソースコードを復元](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *上記の環境カードには、選択した環境の&#x200B;**復元**／**以前にデプロイされたコード**&#x200B;オプションが表示されています。*

![以前にデプロイしたコードを復元ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
***以前にデプロイしたコードを復元**&#x200B;ダイアログボックスで、現在デプロイされているバージョンと復元するバージョンを確認し、「**確認***」をクリックします。

![アクティベーションの復元](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
*Cloud Manager は、環境を以前のビルドにロールバックし、コンテンツと設定をそのままの状態に保ち、デプロイメントが完了するまで環境に&#x200B;**復元中**&#x200B;とマークを付けます。*

![使用中のソースコードバージョン](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *環境の詳細ビューには、前述のように、使用中のアクティブなソースコードバージョンも表示されるようになりました。*

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから [restorecode@adobe.com](mailto:restorecode@adobe.com) にメールを送信してください。

[AEM as a Cloud Service に以前にデプロイしたコードの復元](/help/operations/restore-previous-code-deployed.md)を参照してください。

[AEM as a Cloud Service のコンテンツを復元](/help/operations/restore.md)も参照してください。

### 特殊なテスト環境 {#specialized-test-environment}

Cloud Manager は、**専用のテスト環境**&#x200B;という新しい追加の環境タイプをサポートするようになりました。 この環境は、運用開始前に、チームが実稼動環境に近い条件下で機能を検証するのに役立つように設計されています。 この環境タイプは、*実稼動環境とステージング環境*、*開発環境*&#x200B;または&#x200B;*迅速な開発環境*&#x200B;環境とは異なり、高度な検証シナリオを実行することに焦点を当てたスペースが提供されます。

**最新の機能強化**

* よりシンプルで直感的なワークフローにより、実稼動以外のパイプラインで専用のテスト環境を設定できるようになりました。 合理化されたセットアップにより、完了までの時間が短縮され、設定エラーが減少します。
* **コンテンツをコピー**&#x200B;が専用のテスト環境でサポートされるようになりました。 実稼動環境をミラーリングした隔離されたテスト環境で、**コンテンツをコピー**&#x200B;を安全に実行できるようになりました。 <!-- (CMGR‑68900) -->

[専用のテスト環境の追加](/help/implementing/cloud-manager/specialized-test-environment.md)を参照してください。

![「専用のテスト環境」ラジオボタンが選択された「環境を追加」ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

>[!NOTE]
>
>アドビでは、十分な数の参加者に達したので、特殊なテスト環境の Beta アクセスリクエストを終了しました。 この機能は現在、一般提供に向けて準備中です。

<!--
If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID. -->


### Bring Your Own Git (BYOG) {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Azure DevOps Git リポジトリを Cloud Manager にオンボードできるようになりました。これは、最新の Azure DevOps リポジトリとレガシー VSTS（Visual Studio Team Services）リポジトリの両方に対応しています。

* Edge Delivery Services のユーザーは、オンボードされたリポジトリを使用して、サイトコードを同期およびデプロイできます。
* AEM as a Cloud Service および Adobe Managed Services（AMS）のユーザーは、リポジトリをフルスタックパイプラインとフロントエンドパイプラインの両方にリンクできます。

追加のパイプラインタイプと、コード品質パイプラインを通じたプルリクエスト検証のサポートは、近日リリース予定です。

[Cloud Manager でのプライベートリポジトリの追加](/help/implementing/cloud-manager/managing-code/external-repositories.md)を参照してください。

![リポジトリを追加ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. Be sure to include which Git platform you want to use and whether you are on a private/public or enterprise repository structure. -->

**BYOG に関するよくある質問**

| 質問 | 回答 |
|---|---|
| *必要に応じてプロジェクトを Adobe の管理による Git リポジトリに戻すには、どうすれば良いですか？* | 戻すのは簡単です。 [パイプラインを更新](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)して Adobe リポジトリを指し、外部リポジトリが不要になった場合は削除します。 |
| *異なる環境（実稼動と実稼動以外など）に異なるリポジトリを設定して、最初に実稼動以外の環境でテストできるようにすることはできますか？* | はい、個別の環境用に異なるリポジトリを設定できます。 例えば、開発パイプラインまたはコード品質パイプラインは外部リポジトリを指し、実稼動パイプラインは Adobe リポジトリに接続されたままにすることができます。 この設定中は、2 つのリポジトリ間の同期ジョブがアクティブのままであることを確認してください。 |
| *`IP Allow` リストなどの既存の設定は引き続き機能しますか？* | はい、既存の `IP Allow` リストは引き続き通常どおり機能します。 ただし、外部 Git リポジトリがファイアウォールで保護されている場合は、必要な [Adobe IP アドレスを許可リストに追加する必要があります](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *すべての GitLab リポジトリ URL が機能しますか？ 使用するリポジトリ URL は、形式 `https://gitlab_dedicated_url.com/path/repo-name.git` に従いますが、この形式はドキュメントの例とは異なります。* | はい、API V3 または V4 をサポートするどの GitLab リポジトリもサポートされます。これには、[Cloud Manager への外部リポジトリの追加 ](/help/implementing/cloud-manager/managing-code/external-repositories.md)（`https://git-vendor-name.com/org-name/repo-name.git`）に記載されているようなセルフホスト型の GitLab URL が含まれます。 |


#### アクセストークンを管理{#manage-access-tokens}

Cloud Managerで「**アクセストークンの管理**」を使用して、外部 BYOG リポジトリ (GitHub Enterprise、GitLab、Bitbucket、Azure DevOps など) に関連付けられたアクセストークンを表示、名前変更、削除します。

[アクセストークンを管理](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)をご覧ください。

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->

### Edge Delivery設定パイプラインを追加 {#add-eds-pipeline}

Edge Delivery Services を使用して作成されたサイトで設定パイプラインがサポートされるようになりました。これにより、Cloud Service 環境以外でもこの機能を利用できます。 **設定パイプライン**&#x200B;を使用すると、トラフィックフィルタリングルールや web アプリケーションファイアウォール（WAF）設定などの設定を管理できます（該当する場合）。 [サポートされている設定](/help/operations/config-pipeline.md#configurations)を参照してください。

**最近の機能強化**

* Edge Delivery設定パイプラインで、Cloud Manager パイプライン変数を通じてシークレットがサポートされるようになりました。
* Edge Delivery Services パイプラインの&#x200B;**デプロイ済みコード**&#x200B;列に&#x200B;**設定**&#x200B;と表示され、設定専用のデプロイメントを即座に特定できるようになりました。 <!-- CMGR‑69681 -->
* プログラムに 1 つ以上のEdge Delivery サイトと 1 つのマッピング済みドメインが含まれると、Cloud Managerは **Edge Delivery パイプラインを追加**&#x200B;を表示します。 そうでない場合、そのオプションは無効として表示され、ツールチップで不足している要件が説明されます。 <!-- CMGR‑69680 -->
* 「**Edge Delivery**」タブには、新しい「**Edge Delivery パイプライン**」ウィジェットが表示され、各パイプラインの名前、ステータス、リポジトリ、ブランチがリストされます。 <!-- (CMGR-69052) -->

  ![パイプライン名、ステータス、リポジトリー、ブランチを表示する「Edge Delivery パイプライン」ウィジェット](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

* **フィルター**&#x200B;パネルには、「**Edge Delivery**」チェックボックスと「**Publish Delivery**」チェックボックスを含む「**配信タイプ**」セクションが追加されます。 <!-- (CMGR-69682) -->

  ![Edge DeliveryとPublish Deliveryの新しい配信タイプを示すフィルターパネル](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

![「パイプラインを追加」ドロップダウンリストの「Edge Delivery パイプラインを追加」](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png)*「**プログラムの概要**」ページ、「**パイプライン**」カードからのEdge Delivery パイプラインの追加。*

![「Edge Delivery パイプラインを追加」ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png)*「Edge Delivery パイプラインを追加」ダイアログボックス。*

[Edge Delivery パイプラインを追加する](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)をご覧ください。

この新機能をテストしてフィードバックを共有したい場合は、Adobe ID に関連付けられたメールアドレスから [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) にメールを送信してください。

## バグ修正 {#bug-fixes}

9 月のCloud Manager リリースには重要なバグ修正はありません。


<!-- ## Known issues {#known-issues} -->

