---
title: Cloud Manager 2025.10.0 のリリースノート
description: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.10.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 673e6a2403026e33c3bbd225b7296a1fb8877404
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 61%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.10.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2025.10.0 のリリースについて説明します。

[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2025.10.0 のリリース日は 2025年10月2日木曜日（PT）です。

次回のリリース予定は 2025年11月6日木曜日（PT）です。

## 新機能 {#what-is-new}

* **専用のステージ専用および実稼動用のデプロイメントパイプライン**

  Cloud Managerには、専用のステージング専用および実稼動用のデプロイメントパイプラインが用意されるようになりました。これにより、ステージング環境と実稼動環境へのデプロイメントを個別に管理する柔軟性が向上します。 [&#x200B; ステージング専用および実稼動専用のパイプラインを分割 &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/stage-prod-only.md) を参照してください。

* **AEM Cloud Health Assessment Service**

  Adobeでは、AEM Cloud Health Assessment Service が導入されています。これは、AEM as a Cloud Service環境を最適化され、セキュリティで保護され、ベストプラクティスに沿った状態に保つ、自動の非侵襲的チェックアップツールです。

  このサービスは次の処理を行います。

   * 環境をスキャンして、パフォーマンスのボトルネック、非効率性、潜在的なリスクを特定
   * コンテンツ構造（ブループリント、ライブコピー）とカスタム設定を分析します。
   * 古い依存関係を特定します（AEM SDK、サードパーティライブラリ）。
   * コード品質の問題（不適切な注釈、非効率的なパターン）をフラグ付けします。
   * **アクションセンター** などのダッシュボードを通じて、実用的なガイダンスを提供します。
   * 問題の早期検出と修復を通じて、プロアクティブな最適化をサポートします。

  チームは、AEM環境を継続的に監視および改善して、パフォーマンスのスムーズ化、セキュリティの強化、長期的なメンテナンス性を実現できます。

  [&#x200B; 実稼動環境およびステージ環境のヘルスアセスメント &#x200B;](/help/implementing/cloud-manager/reports/report-health-assessment.md) を参照してください。

* **設定パイプラインのサポート**

  Edge Delivery Services を使用して作成されたサイトで設定パイプラインがサポートされるようになりました。これにより、Cloud Service 環境以外でもこの機能を利用できます。 **設定パイプライン** を使用して、トラフィックフィルタールールや接触チャネルセレクターなどの CDN 設定を管理できます。 [サポートされている設定](/help/operations/config-pipeline.md#configurations)を参照してください。

  Edge Delivery設定パイプラインは、Cloud Manager パイプライン変数を通じてシークレットもサポートします。

  [Edge Delivery パイプラインの追加 &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md) を参照してください。

* **効率化されたドメインマッピング - CDN セットアップダイアログボックス**

  Cloud Managerでは、**ドメインを CDN にマッピング** フローを簡略化して、混乱を軽減し、設定を高速化しました。 ダイアログボックスで、**Adobeの管理による CDN** （「推奨」バッジが付きます）が強調されるようになりました。

  ![Adobeの管理による CDN ラジオボタンが選択されている状態でドメインを CDN にマッピング ダイアログボックス &#x200B;](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-adobe-managed-cdn.png)

  [&#x200B; ドメインマッピングの追加 &#x200B;](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md) を参照してください。

  このダイアログボックスには、**その他の CDN プロバイダー** カードに関する、以下の操作方法のコンテンツに重点を置いた、単一の簡潔なチェックリストも表示されます。

   * CDN オリジンを `publish-p<PROGRAM_ID>-e<ENV_ID>.adobeaemcloud.com` に指定します。
   * **Host/SNI** を設定して、元のホストを転送します。
   * （Cloud Managerにキーをデプロイした後に） `X-AEM-Edge-Key` を追加します。
   * 顧客対応ドメインに `X-Forwarded-Host` を設定します。
   * AEMに到達する前に、他の `X-Forwarded-*` ヘッダーをクリアします。

  ![&#x200B; 「他の CDN プロバイダー」ラジオボタンを選択した状態で、「ドメインを CDN にマッピング」ダイアログボックス &#x200B;](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-other-cdn-provider.png)

  <!-- (no redundant `Origin` field or "Learn more" clutter) -->付属のフッターには、2 つの役立つリンクがあります。主要な CDN のサンプル設定と、完全なドキュメントへのリンクです。 1 つの確認ボタン（「CDN を設定しました」がフローを完了します）。

  [AEM as a Cloud Serviceの CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) を参照してください。

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

### Experience Hubの拡張性とカスタマイズ {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) は、組織のニーズに合わせてカスタマイズされた、AEMへのエントリポイントとして機能します。 Adobeに既存のAEM UI 拡張機能を通知し、最小限の労力でExperience Hubで有効にできるようにします。

![Experience Hubの拡張性とカスタマイズワークフローの図 &#x200B;](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

カスタムエクスペリエンスをExperience Hubに埋め込むと、組織のダッシュボードを拡張し、パーソナライズすることができます。 Adobeの組み込みウィジェットに加えて、[UI 拡張機能 &#x200B;](https://developer.adobe.com/uix/docs/) フレームワークを使用して独自のウィジェットを追加します。 JavaScript ベースの UI アプリを作成し、ビジネス固有の要件とワークフローを満たすようにユーザーに表示します。

ベータ版に興味がありますか？ Adobeの OrgID と作成するカスタマイズの簡単な説明を [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) にメールで送信します。

### モジュールのキャッシュによるビルドの高速化 {#quick-build-cm-pipelines}

新しいビルドモデルでは、（リポジトリ全体ではなく）変更されたモジュールのみを、モジュールレベルのキャッシュを使用してコンパイルし、ビルド時間を短縮します。 コード品質、フルスタック、ステージ専用のパイプラインに適用されます。

興味ある？ Adobeの OrgID とプログラム ID を記載したメール [0&rbrace;beta_quickbuild_cmpipelines@adobe.com&rbrace; を送信します。](mailto:beta_quickbuild_cmpipelines@adobe.com)

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->



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
| *すべての GitLab リポジトリ URL が機能しますか？ 使用するリポジトリ URL は、形式 `https://gitlab_dedicated_url.com/path/repo-name.git` に従いますが、この形式はドキュメントの例とは異なります。* | はい、API V3 または V4 をサポートするどの GitLab リポジトリもサポートされます。これには、[Cloud Manager への外部リポジトリの追加 &#x200B;](/help/implementing/cloud-manager/managing-code/external-repositories.md)（`https://git-vendor-name.com/org-name/repo-name.git`）に記載されているようなセルフホスト型の GitLab URL が含まれます。 |


#### アクセストークンを管理{#manage-access-tokens}

Cloud Managerで「**アクセストークンの管理**」を使用して、外部 BYOG リポジトリ (GitHub Enterprise、GitLab、Bitbucket、Azure DevOps など) に関連付けられたアクセストークンを表示、名前変更、削除します。

[アクセストークンを管理](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)をご覧ください。

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->


## バグ修正 {#bug-fixes}

10 月のCloud Manager リリースには重要なバグ修正はありません。


<!-- ## Known issues {#known-issues} -->

