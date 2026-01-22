---
title: Cloud Manager 2026.1.0 のリリースノート
description: Adobe Experience Manager as a Cloud Service の Cloud Manager 2026.1.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 54566e3ea99c4ac03e266eab52163a516701b611
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 66%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2026.1.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2026.1.0 のリリースについて説明します。

[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2026.1.0 のリリース日は 2026年1月22日木曜日（PT）です。

次回のリリース予定は 2026年2月5日木曜日（PT）です。

## 新機能 – Cloud Manager {#cloud-manager-whats-new}

* **設定パイプラインで管理シークレットがサポートされるようになりました**

  ユーザーは、Cloud Manager設定パイプラインで直接シークレットを追加および管理できるようになりました。 これらのシークレットは、パイプライン設定仕様の値を安全に上書きし、柔軟な環境固有のデプロイメントをサポートします。

  ![&#x200B; 選択したパイプラインのドロップダウンメニューの「変数を表示/編集」オプション &#x200B;](/help/implementing/cloud-manager/release-notes/assets/view-edit-variables-option.png)
  *選択したパイプラインのドロップダウンメニューの「変数を表示/編集」オプション*

  ![&#x200B; 変数設定ダイアログボックス &#x200B;](/help/implementing/cloud-manager/release-notes/assets/view-edit-variables-variablesconfig-dialogbox.png)*変数設定ダイアログボックス*

* **安定性、パフォーマンス、信頼性の向上**

  このリリースには、Cloud Managerの安定性、パフォーマンス、信頼性を向上させる最適化およびメンテナンスの更新が含まれています。




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

