---
title: Cloud Manager 2025.12.0 のリリースノート
description: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.12.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 7c1f1f1022fd63c190a493d312ab1f355859d15a
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 61%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.12.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2025.12.0 のリリースについて説明します。

[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2025.12.0 のリリース日は 2025年12月4日木曜日（PT）です。

次回のリリース予定は 2026年1月22日木曜日（PT）です。

## 新機能 – Experience Hub {#experience-hub-whats-new}

* **Experience Hubへのシンプルなアクセス**

  ユーザーの役割の選択が削除され、**プリセット** の選択用のガイドが追加されました（コンテンツ作成者、アセットライブラリアン、管理者および IT）。

* **お知らせ** および **製品アップデート**

  利用可能なお知らせは、切り替えて繰り返し表示できますが、解除することもできます。

* **最近**

  ページエディター、アセット、プログラム、パイプライン実行の詳細、セキュリティページなど、追加のページやリソースのサポートが追加されました。

* **プログラムリスト**

  AEM Cloud Managerの詳細ページにすばやくアクセスして、組織内のCloud Manager プログラムを表示する。

* **AEM Guides**

  AEM Guides アドオンが有効になっているオーサリング環境用のクイックアクションとショートカット。

## 新機能 – Cloud Manager {#cloud-manager-whats-new}

* **安定性、パフォーマンス、信頼性の向上**

  このリリースには、Cloud Managerの安定性、パフォーマンス、信頼性を向上させる最適化およびメンテナンスの更新が含まれています。

* **特殊なテスト環境**

  >[!NOTE]
  >
  >専用のテスト環境を購入できるようになりました。 Adobeの担当者に連絡して注文してください。

  Cloud Manager は、**専用のテスト環境**&#x200B;という新しい追加の環境タイプをサポートするようになりました。 この環境は、運用開始前に、チームが実稼動環境に近い条件下で機能を検証するのに役立つように設計されています。 この環境タイプは、*実稼動環境とステージング環境*、*開発環境*&#x200B;または&#x200B;*迅速な開発環境*&#x200B;環境とは異なり、高度な検証シナリオを実行することに焦点を当てたスペースが提供されます。

  [専用のテスト環境の追加](/help/implementing/cloud-manager/specialized-test-environment.md)を参照してください。

  ![「専用のテスト環境」ラジオボタンが選択された「環境を追加」ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

<!--
>[!NOTE]
>
>Adobe has closed beta access requests for Specialized Testing Environments, having reached a sufficient number of participants. The feature is now in preparation for general availability.

If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID. -->


* **パイプラインデプロイメントの場合は、ワンクリックロールバック**

  最新のお客様のソースコードが期待どおりに動作しない場合は、すばやく以前のデプロイメントに戻します。 パイプライン全体を再実行したり、コミットを手動で元に戻したりする必要はありません。<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

  [AEM as a Cloud Service に以前にデプロイしたコードの復元](/help/operations/restore-previous-code-deployed.md)を参照してください。

  [AEM as a Cloud Service のコンテンツを復元](/help/operations/restore.md)も参照してください。

* **Edge Delivery ServicesのセルフサービスWAFの設定**

  Cloud ManagerでEdge Delivery Services プログラムを作成する際に、web アプリケーションファイアウォール（WAF）を有効にできます。 この設定は、悪意のあるトラフィックや DDoS 攻撃からサイトを直ちにシールドし、手動の設定作業を減らします。

  [&#x200B; ワンクリックで最初のEdge Delivery サイトを作成する &#x200B;](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md) を参照してください。


## Beta プログラム {#private-beta-program}

Cloud Manager の Beta プログラムに参加すると、一般リリース前の新機能に特別アクセスできます。

>[!IMPORTANT]
>
>Beta リリースには不具合が含まれている場合があり、いかなる保証もなく「現状のまま」提供されます。 Adobeは、ベータ版リリースの保守、修正、更新、変更、またはその他のサポート（Adobe サポートサービスを通じてまたはその他の方法で）を行う義務を負いません。 Adobeでは、お客様に対して、ベータ版リリースが正しく機能するか、パフォーマンスが向上するか、あるいはこれらに付随するドキュメントや資料を使用しないよう、注意して助言しています。 ベータ版の機能と API は、予告なく変更される場合があります。 したがって、ベータ版リリースの使用は、完全にお客様自身の責任で行います。

[AEM Beta プログラム &#x200B;](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs) も参照してください。

現在、次の機能が利用できます。
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

### Experience Hub の拡張性とカスタマイズ {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) は、組織のニーズに合わせてカスタマイズされた、AEM へのエントリポイントとして機能します。アドビに既存の AEM UI 拡張機能を通知すると、最小限の労力で Experience Hub で拡張機能を有効にできるようになります。

![Experience Hub の拡張性とカスタマイズワークフローの図](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

カスタムエクスペリエンスを Experience Hub に埋め込むと、組織のダッシュボードを拡張およびパーソナライズすることができます。アドビの組み込みウィジェットに加えて、[UI 拡張機能](https://developer.adobe.com/uix/docs/)フレームワークを使用して独自のウィジェットを追加します。JavaScript ベースの UI アプリを作成し、ビジネス固有の要件とワークフローに合わせてユーザーに表示します。

ベータ版にご興味がありますか？Adobe OrgID と作成するカスタマイズの簡単な説明を記載して [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) にメールでお問い合わせください。

### モジュールのキャッシュによるビルドの高速化 {#quick-build-cm-pipelines}

新しいビルドモデルでは、（リポジトリ全体ではなく）変更されたモジュールのみを、モジュールレベルのキャッシュを使用してコンパイルし、ビルド時間を短縮します。これは、コード品質、フルスタック、ステージ専用のパイプラインに適用されます。

![&#x200B; フルビルドとスマートビルドの 2 つのビルド戦略オプションが表示されている実稼動以外のパイプラインを編集ダイアログボックス &#x200B;](/help/implementing/cloud-manager/release-notes/assets/non-production-pipeline-edit.png)
*フルビルドとスマートビルドの 2 つのビルド戦略オプションが表示されている実稼動以外のパイプラインを編集ダイアログボックス。*

**パイプラインを追加/編集** ダイアログボックスの「**Sourceコード**」タブにある新しい **ビルド方法** セクションで、次のいずれかのビルドオプションを選択できます。

* **フルビルド** – 実行ごとにリポジトリ内のすべてのモジュールをビルドします。
* **スマートビルド** – 前回のコミット以降に変更されたモジュールのみをビルドし、全体的なビルド時間を短縮します。

使用するパイプラインを制御できます **スマートビルド**。 ベータ版では、このオプションは **コード品質** パイプラインと **開発デプロイメント** パイプラインにのみ表示されます。

ご興味がある場合Adobe OrgID とプログラム ID を記載して [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) にメールでお問い合わせください。

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->

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
| *すべての GitLab リポジトリ URL が機能しますか？ 使用するリポジトリ URL は、形式 `https://gitlab_dedicated_url.com/path/repo-name.git` に従いますが、この形式はドキュメントの例とは異なります。* | はい、API V3 または V4 をサポートするどの GitLab リポジトリもサポートされます。これには、[Cloud Manager への外部リポジトリの追加 &#x200B;](/help/implementing/cloud-manager/managing-code/external-repositories.md)（`https://git-vendor-name.com/org-name/repo-name.git`）に記載されているようなセルフホスト型の GitLab URL が含まれます。 |


#### アクセストークンを管理{#manage-access-tokens}

Cloud Managerで「**アクセストークンの管理**」を使用して、外部 BYOG リポジトリ (GitHub Enterprise、GitLab、Bitbucket、Azure DevOps など) に関連付けられたアクセストークンを表示、名前変更、削除します。

[アクセストークンを管理](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)をご覧ください。

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->


## バグ修正 {#bug-fixes}

2025 年 12 月のCloud Manager リリースには、重要なバグ修正はありません。


<!-- ## Known issues {#known-issues} -->

