---
title: Cloud Manager 2025.8.0 のリリースノート
description: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.8.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: c6493d05c60c01b4840c8f12d06aa4508bdbb534
workflow-type: tm+mt
source-wordcount: '1403'
ht-degree: 55%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.8.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2025.8.0 のリリースについて説明します。

[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2025.8.0 のリリース日は 2025年8月7日（PT）です。

次回のリリース予定は 2025年9月4日（PT）です。

## 新機能 {#what-is-new}

* **Adobe Experience Hub近日公開予定**

  2025 年 8 月 19 日（PT）より、AdobeはすべてのAdobe Experience Manager ユーザーに対して新しいExperience Hubの段階的なロールアウトを開始します。

  Experience Hubは、状況に応じたパーソナライズされたエクスペリエンスを提供し、ユーザーの目標達成を支援する統合的な出発点です。 このロールアウトは 2025 年 8 月 26 日（PT）までに終了し、すべてのユーザーが使用できるようになります。 新しいExperience Hubには、[experience.adobe.com](https://experience.adobe.com/) から直接アクセスできます。 詳しくは、[Adobe Experience Hub](/help/implementing/cloud-manager/aem-home.md) を参照してください。

* **Edge Delivery Services ライセンスは、セルフサービス方式で HIPAA プログラムに含めることができます**

  医療機関や機密データの要件がある組織は、Edge Delivery Servicesをセルフサービス方式で使用できるようになり、HIPAA コンプライアンスを実現して厳格な規制基準を満たすことができます。<!-- CMGR-70016 -->

* **Edge Delivery Servicesで BYOG が使用できるようになりました**

  Cloud Managerで外部 Git リポジトリを設定して、柔軟なコード管理ワークフローを有効にできるようになりました。 <!--(CMGR‑69010, CMGR‑70988) --> また、Cloud Manager UI で選択したブランチからコードを直接取り込むことができ、手動のリポジトリタスクを減らすことができます。 [ 外部 Git リポジトリを使用するためのEdge Delivery サイトの設定 ](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md) を参照してください <!-- (CMGR‑68085)(CMGR-69015) --> <!-- KT: https://wiki.corp.adobe.com/display/DMSArchitecture/%5B2025%5D+Cloud+Manager+-+Bring+Your+Own+Git+with+EDS -->

* **新しいForms アドオンの自動プロビジョニング**

  Sites のみのユーザーは、多くの場合、マーケティングフォームを構築するために軽量で低コストな方法を必要とします。 新しいAEM Forms Sites アドオンは、Sites プログラムに限定的なForms機能を追加することで、このニーズを満たします。 また、AEM Formsの全製品への明確なアップグレードパスも作成されます。<!-- (CMGR-64301) --> <!-- KT: CMGR Provisioning Support for AEM Forms Sites Add-On SKU https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3578379797 -->

  アドオン：
   * Sites プログラムに添付して、そのプログラムと共にデプロイします。Forms プログラムや権利付与は分離されません。
   * シンプルなマーケティングフォームのユースケースをターゲットにします。
   * 実稼動プログラムの作成時または実稼動プログラムの編集時に、IMS 組織が使用可能なForms アドオンライセンスを保持している場合にのみ、**ソリューションとアドオン** リストに表示されます。

     ![Forms アドオン ](/help/implementing/cloud-manager/release-notes/assets/forms-add-on.png)*Forms アドオンは、IMS 組織でForms アドオンライセンスが使用可能な場合にのみ、プログラムに追加できます。*

     ![ 実稼動プログラムの作成時のソリューションとアドオンのForms アドオン ](/help/implementing/cloud-manager/release-notes/assets/forms-add-on-creating-production-program.png)*プログラムの作成時に、Sites ソリューション内でForms アドオンを選択できます。*

     ![ 実稼動プログラムの編集時のForms アドオン ](/help/implementing/cloud-manager/release-notes/assets/forms-add-on-editing-production-program.png)***プログラムを編集**で、Sites プログラム用のForms アドオンを選択してから、パイプラインを実行して環境でアクティブ化します。*

     詳しくは、[ 実稼動プログラムの作成 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) を参照してください。

## Beta プログラム {#private-beta-program}

Cloud Managerのベータプログラムに参加すると、一般リリース前に今後リリースされる機能を独占的に利用できます。

現在、以下の機能が利用可能です。

### パイプラインデプロイメントのロールバックをワンクリックで実行 {#one-click-rollback}

最新の顧客ソースコードが期待どおりに動作しない場合は、以前のデプロイメントに迅速に戻すことができます。パイプライン全体を再実行したり、コミットを手動で元に戻したりする必要はありません。<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![環境カードから顧客ソースコードを復元](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *上記の環境カードには、選択した環境の&#x200B;**復元**／**以前にデプロイされたコード**オプションが表示されています。*

![以前にデプロイしたコードを復元ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
***以前にデプロイしたコードを復元**ダイアログボックスで、現在デプロイされているバージョンと復元するバージョンを確認し、「**確認***」をクリックします。

![アクティベーションの復元](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
*Cloud Manager は、環境を以前のビルドにロールバックし、コンテンツと設定をそのままの状態に保ち、デプロイメントが完了するまで環境に&#x200B;**復元中**とマークを付けます。*

![使用中のソースコードバージョン](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *環境の詳細ビューには、前述のように、使用中のアクティブなソースコードバージョンも表示されるようになりました。*

この新機能をテストしてフィードバックを共有することに興味がある場合は、Adobe ID に関連付けられたメールアドレスから [restorecode@adobe.com](mailto:restorecode@adobe.com) にメールを送信してください。

[AEM as a Cloud Service に以前にデプロイしたコードの復元](/help/operations/restore-previous-code-deployed.md)を参照してください。

[AEM as a Cloud Service のコンテンツを復元](/help/operations/restore.md)も参照してください。

### 特殊なテスト環境 {#specialized-test-environment}

Cloud Manager は、**専用のテスト環境**&#x200B;という新しい追加の環境タイプをサポートするようになりました。この環境は、運用開始前に、チームが実稼動環境に近い条件下で機能を検証するのに役立つように設計されています。この環境タイプは、*実稼動環境とステージング環境*、*開発環境*&#x200B;または&#x200B;*迅速な開発環境*&#x200B;環境とは異なり、高度な検証シナリオを実行することに焦点を当てたスペースが提供されます。

**最近の機能強化**

* よりシンプルで直感的なワークフローにより、実稼動以外のパイプラインで専用のテスト環境を設定できるようになりました。 合理化されたセットアップにより、完了までの時間が短縮され、設定エラーが減少します。
* **コンテンツをコピー** が専用のテスト環境でサポートされるようになりました。 実稼動をミラーリングする分離されたテスト環境で、**コンテンツをコピー** を安全に実行できるようになりました。<!-- (CMGR‑68900) -->

[専用のテスト環境の追加](/help/implementing/cloud-manager/specialized-test-environment.md)を参照してください。

![「専用のテスト環境」ラジオボタンが選択された「環境を追加」ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

>[!NOTE]
>
>Adobeでは、十分な数の参加者に達したため、専用テスト環境のクローズドベータ版アクセスリクエストを行いました。 この機能は、一般公開に備えています。

<!--
If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID. -->


### 独自の Git の導入（BYOG） {#gitlab-bitbucket-azure-vsts}

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
| *必要に応じてプロジェクトを Adobe の管理による Git リポジトリに戻すには、どうすれば良いですか？* | 戻すのは簡単です。[パイプラインを更新](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)して Adobe リポジトリを指し、外部リポジトリが不要になった場合は削除します。 |
| *異なる環境（実稼動と実稼動以外など）に異なるリポジトリを設定して、最初に実稼動以外の環境でテストできるようにすることはできますか？* | はい、個別の環境用に異なるリポジトリを設定できます。例えば、開発パイプラインまたはコード品質パイプラインは外部リポジトリを指し、実稼動パイプラインは Adobe リポジトリに接続されたままにすることができます。この設定中は、2 つのリポジトリ間の同期ジョブがアクティブのままであることを確認してください。 |
| *`IP Allow` リストなどの既存の設定は引き続き機能しますか？* | はい、既存の `IP Allow` リストは引き続き通常どおり機能します。 ただし、外部 Git リポジトリがファイアウォールで保護されている場合は、必要な [Adobe IP アドレスを許可リストに追加する必要があります](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *すべての GitLab リポジトリ URL が機能しますか？使用するリポジトリ URL は、形式 `https://gitlab_dedicated_url.com/path/repo-name.git` に従いますが、この形式はドキュメントの例とは異なります。* | はい、API V3 または V4 をサポートするどの GitLab リポジトリもサポートされます。これには、[Cloud Manager への外部リポジトリの追加 ](/help/implementing/cloud-manager/managing-code/external-repositories.md)（`https://git-vendor-name.com/org-name/repo-name.git`）に記載されているようなセルフホスト型の GitLab URL が含まれます。 |


#### アクセストークンを管理{#manage-access-tokens}

Cloud Managerで「**アクセストークンの管理**」を使用して、外部 BYOG リポジトリ (GitHub Enterprise、GitLab、Bitbucket、Azure DevOps など) に関連付けられたアクセストークンを表示、名前変更、削除します。

[アクセストークンを管理](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)をご覧ください。

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->


### Edge Delivery 設定パイプラインを追加する {#add-eds-pipeline}

Edge Delivery Services を使用して作成されたサイトで設定パイプラインがサポートされるようになりました。これにより、Cloud Service 環境以外でもこの機能を利用できます。**設定パイプライン**&#x200B;を使用すると、トラフィックフィルタリングルールや web アプリケーションファイアウォール（WAF）設定などの設定を管理できます（該当する場合）。[サポートされている設定](/help/operations/config-pipeline.md#configurations)を参照してください。

**最近の機能強化**

* Edge Delivery Services パイプラインの **デプロイ済みコード** 列に **設定** と表示され、設定専用のデプロイメントを即座に特定できるようになりました。<!-- CMGR‑69681 -->
* プログラムに 1 つ以上のEdge Delivery サイトと 1 つのマッピング済みドメインが含まれると、Cloud Managerは **Edge Delivery Services パイプラインを追加** を表示します。 それ以外の場合は、このオプションは無効に表示され、不足している要件に関するツールチップが説明されます。<!-- CMGR‑69680 -->
* 「**Edge Delivery**」タブには、新しい「**Edge Delivery パイプライン**」ウィジェットが表示され、各パイプラインの名前、ステータス、リポジトリ、ブランチがリストされます。<!-- (CMGR-69052) -->

  ![ パイプライン名、ステータス、リポジトリー、ブランチを表示するEdge Delivery パイプラインウィジェット ](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

* **フィルター** パネルには、「{4 **Edge配信**」チェックボックスと「**公開配信**」チェックボックスを含む「配信タイプ **」セクションが追加されます。**<!-- (CMGR-69682) -->

  ![Edge配信と公開配信の新しい配信タイプを示すフィルターパネル ](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

![「パイプラインを追加」ドロップダウンリストの「Edge Delivery パイプラインを追加」](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png)*「**プログラムの概要**」ページ、「**パイプライン**」カードからのEdge Delivery パイプラインの追加。*

![「Edge Delivery パイプラインを追加」ダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png)*「Edge Delivery パイプラインを追加」ダイアログボックス。*

[Edge Delivery パイプラインの追加 ](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md) を参照してください。

この新機能をテストしてフィードバックを共有したい場合は、Adobe ID に関連付けられたメールアドレスから [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) にメールを送信してください。


## バグ修正

* パイプラインでは、パイプラインの作成中に削除された設定をスキップして、アクティブなEdge Delivery Services ドメイン設定にのみ変数を配信するようになりました。<!-- (CMGR‑70039) -->
* パイプラインの実行が確実に開始されるようになりました。内部リソース処理エラーが原因で一部のパイプラインの開始に失敗した問題を修正しました。<!-- (CMGR‑58167) -->
* コンテンツのコピーでは、Cloud Managerの権限とブロックの検証を開始しますが、それは Deployment Manager または Administrator の権限がないユーザーが行う必要があります。<!-- (CMGR‑62097) -->


<!-- ## Known issues {#known-issues} -->

