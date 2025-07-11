---
title: Cloud Manager 2025.7.0 のリリースノート
description: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.7.0 のリリースについて説明します。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 3e7ce0c7f330ba92b57e36ea8fe5bb17b5998cb1
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 60%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.7.0 のリリースノート {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2025.7.0 のリリースについて説明します。

[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)も参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2025.7.0 のリリース日は 2025年7月10日（PT）です。

次回のリリース予定は 2025年8月7日（PT）です。

## 新機能 {#what-is-new}

* **Cloud Managerでは、ECDSA （Elliptic Curve Digital Signature Algorithm） SSL 証明書のサポートが追加されました**

  Cloud Managerで ECDSA 証明書がサポートされるようになりました。 この機能は、より小さな鍵サイズで強力なセキュリティを提供し、お客様が CDN 設定に軽量な最新の暗号化を適用できるようにします。<!-- https://jira.corp.adobe.com/browse/CMGR-62399 -->

* **サイトのライセンス使用状況レポートをダウンロード**

  **Sites の使用状況の詳細** ページ（Cloud Managerでは **ライセンス** をクリックします。 ソリューションテーブルの **サイト** 行で **使用状況の詳細を表示**）をクリックすると、**レポートをダウンロード** をクリックしてデータを CSV ファイルとして書き出すことができるようになりました。 このダウンロードにより、使用状況のトレンドの分析と共有が簡単になります。<!-- https://jira.corp.adobe.com/browse/CMGR-42274 -->

  ![ サイトの使用状況の詳細ページ ](/help/implementing/cloud-manager/release-notes/assets/sites-license-usage-page.png)

  [ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md)をご覧ください。

## 早期導入プログラム {#private-beta-program}

Cloud Managerのアルファおよびベータ版プログラムに参加すると、一般リリース前に、今後の機能に早期に排他的にアクセスできます。

現在、次のオポチュニティを利用できます。

### パイプラインデプロイメントのロールバックをワンクリックで実行できます {#one-click-rollback}

最新の顧客ソースコードが期待どおりに動作しない場合は、すばやく以前のデプロイメントに戻すことができます。パイプライン全体を再実行したり、コミットを手動で戻したりする必要はありません。<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![ 環境カードから顧客ソースコードを復元 ](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png)*選択した環境の上に&#x200B;**復元**/**以前にデプロイされたコード**オプションが表示されている環境カード*


![ 以前にデプロイしたコードを復元ダイアログボックス ](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
***以前にデプロイしたコードを復元**ダイアログボックスで、現在デプロイされているバージョンと復元するバージョンを確認し、「**確認***」をクリックします。


![ アクティベーションの復元 ](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
*Cloud Managerは、環境を以前のビルドにロールバックし、コンテンツと設定はそのままの状態に保ち、デプロイメントが完了するまで環境に&#x200B;**復元中**マークを付けます。*


![ 使用中のSource コードバージョン ](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png)*環境の詳細ビューには、前述のように、使用中のアクティブなソースコードバージョンも表示されるようになりました。*

この新機能のテストやフィードバックの提供に関心がある場合は、Adobe IDに関連付けられたメールアドレスから [restorecode@adobe.com](mailto:restorecode@adobe.com) にメールを送信してください。

[AEM as a Cloud Serviceにデプロイされた以前のコードの復元 ](/help/operations/restore-previous-code-deployed.md) を参照してください。

[AEM as a Cloud Serviceでのコンテンツの復元 ](/help/operations/restore.md) も参照してください。


### 特殊なテスト環境 {#specialized-test-environment}

Cloud Manager は、**専用のテスト環境**&#x200B;という新しい追加の環境タイプをサポートするようになりました。この環境は、運用開始前に、チームが実稼動環境に近い条件下で機能を検証するのに役立つように設計されています。この環境タイプは、*実稼動環境とステージング環境*、*開発環境*&#x200B;または&#x200B;*迅速な開発環境*&#x200B;環境とは異なり、高度な検証シナリオを実行することに焦点を当てたスペースが提供されます。

最近の機能強化：よりシンプルで直感的なワークフローにより、実稼動以外のパイプラインで専用のテスト環境を設定できるようになりました。 合理化されたセットアップにより、完了が迅速化され、設定エラーが削減されます。

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

* Cloud Managerは、環境のアップグレード中にすべてのパイプラインのリリースバージョンを更新し、すべてのパイプラインタイプで一貫したバージョントラッキングを行えるようになりました。<!-- CMGR-69043 -->
* ドメイン検証（DV） SSL 証明書に失敗した場合に、UI にステータスと詳細なエラーメッセージが表示されるようになり、証明書の問題の理解と解決に役立ちます。<!-- CMGR-68872 -->
* ドメインマッピングの編集中に、選択したドメインに一致しない SSL 証明書の選択が UI で禁止されるようになりました。これにより、設定ミスが減り、セットアップ中の信頼性が向上します。<!-- CMGR-64307 -->
* 状況によっては、証明書が正しく削除されず、ドメインがアクティブのままになることがある。<!-- CMGR-69867 -->
* 特定の場合に *Adobe Assetsから* Adobe Assets Ultimate *へのアップグレードをブロックする可能性がある問題を修正し* した。 トランジションがスムーズになり、信頼性が向上しました。<!-- CMGR-69506 -->
* ダウンストリームのサービスやデプロイメントをスムーズにサポートするために複数地域環境を作成する際に、主要な地域フィールドが自動的に設定される問題を修正しました。<!-- CMGR-69471 -->
* 一部の設定パイプラインが実行後に正しく停止しない問題を修正しました。 パイプラインが正常に完了し、期待どおりに閉じられるので、信頼性が向上します。<!-- CMGR-69344 -->


<!-- ## Known issues {#known-issues} -->

