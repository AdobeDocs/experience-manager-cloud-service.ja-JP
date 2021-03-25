---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
translation-type: tm+mt
source-git-commit: a81fe4a2c7d3c4e0471a961fb51249ac03f27e9c
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 38%

---


# [!DNL Adobe Experience Manager] as a Cloud Service のリリースノート {#release-notes}

[!DNL Experience Manager] as a Cloud Service の一般的なリリースノートの概要を次に説明します。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2021.2.0 のリリース日は 2021 年 2 月 25 日です。次のリリース(2021.3.0)は、2021年3月25日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### ヘッドレスコンテンツ管理 {#headless}

* **[コンテンツフラグメント配信用の GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**：GraphQL 構文を使用してコンテンツフラグメントのクエリを実行する機能と、JSON 形式で出力するための、コンテンツフラグメントモデルに基づくスキーマが用意されました。

* **[GraphQL API リクエストの認証サポート](/help/assets/content-fragments/graphql-authentication-content-fragments.md)**：サーバー側 API のアクセストークンで GraphQL API リクエストを認証できるようになりました。

* **[RemotePage コンポーネント](/help/implementing/developing/hybrid/remote-page.md)**：AEM 内で外部 SPA を表示および編集できるようになりました。

* **[AEM 内での外部 SPA の編集](/help/implementing/developing/hybrid/editing-external-spa.md)**：AEM インスタンスへのスタンドアロン単一ページアプリケーションのアップロード、編集可能なコンテンツセクションの追加、オーサリングの有効化が可能になりました。

* リッチテキストを JSON 形式で出力する機能やロケールなど、GraphQL API からの JSON 出力が強化されました。

* コンテンツフラグメントモデルのネストのサポートにより、専用のコンテンツフラグメント参照データ型またはコンテンツフラグメント参照を使用して、ネストしたコンテンツフラグメント構造を複数行テキストフィールド内にインラインで作成できるようになりました。

* 「一意」、「必須」、「変換可能」など、コンテンツフラグメントモデルのデータ型で使用できる検証ルールが追加されました。

* コンテンツフラグメントモデルにタグ付けでき、タグ別またはパス別のポリシーを使用してフォルダー内でコンテンツフラグメントを作成できるようになりました。

* 公開アクションや、フラグメントのベースとなっているモデルの表示など、コンテンツフラグメントエディターの使いやすさが向上しました。

* コンテンツフラグメントエディターで JSON 出力を直接プレビューできるようになりました。

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## [!DNL Assets] の新機能 {#what-is-new-assets}

* アセットは[!DNL Experience Manager Assets Brand Portal]を使用してソースにできます。 新しいマーケティングキャンペーン、フォトシュート、プロジェクトに関して、エージェンシーユーザーからアセットをソース化するのに役立ちます。

* [!DNL Experience Manager Assets] の値 [!DNL Cloud Service] は、事前設定済み [!DNL Brand Portal] インスタンスを持つ権利が付与されます。[!DNL Cloud Manager]ユーザーは、[!DNL Experience Manager Assets]の[!DNL Brand Portal]を[!DNL Cloud Service]としてアクティベートできます。 「[ブランドポータルのアクティブ化](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=en)」を参照してください。

* [!DNL Brand Portal]を使用してアセットのソースを行えるようになりました。 アセットソーシング機能は、[!DNL Brand Portal]を活用して、新しいマーケティングキャンペーン、フォトシュート、プロジェクトのソースアセットに対して、顧客がエージェンシーユーザーと関わるよう支援します。 [ [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html)のアセットソーシングを参照してください。

* [!DNL Brand Portal]使用状況レポートには、アクティブなユーザーのみが表示されるようになりました。 非アクティブなユーザーは現在表示されません。 アクティブユーザーとは、[!DNL Admin Console]内の製品プロファイルにアカウントが割り当てられているユーザーです。 [[!DNL Brand Portal] レポート](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html)を参照してください。

* [!DNL Brand Portal]には、新しいダウンロード設定が導入されています。この設定を使用すると、フォルダーやコレクションなどをダウンロードする際に、アセットごとに個別のフォルダーを作成できます。 [ダウンロード設定](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)を参照してください。

## [!DNL Assets] {#bug-fixes-assets}のバグ修正

* 複数のアセットを選択してプロパティを更新すると、エラーが発生したり、選択解除されたアセットのプロパティが更新されたりする場合があります。 (CQ-4316532)
* [!UICONTROL アセット管理者の検索レール]を開こうとすると、ページは空白のままになり、[!UICONTROL 編集]/[!UICONTROL 設定]をクリックするとエラーが発生します。 (CQ-4315079)
* 名前の競合を解決した後に既存のアセットの新しいバージョンを作成すると、元のアセットのメタデータが上書きされます。 (CQ-4313594)
* 注釈テキストが長いアセットを印刷すると、空白がある場合でも、注釈テキストはトリミングされます。 (CQ-4314101)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 製品エクスペリエンス管理：エクスペリエンスフラグメントを使用して、商品カタログページを個別に拡張する。

* 関連するコンテンツにすばやく移動するアクションなど、アセットとエクスペリエンスフラグメントのリンクを表示するための製品コンソールプロパティが拡張されました。

* 最新の CIF コアコンポーネント v1.8.0 を含んだ CIF Venia 参照サイト 2021.02.24 をリリースしました。詳しくは、[CIF Venia 参照サイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24)を参照してください。

* CIF コアコンポーネント v1.8.0 をリリースしました。詳しくは、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0)を参照してください。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEM as a Cloud Service 2021.2.0 Cloud Manager のリリース日は 2021 年 2 月 11 日です。

### 新機能 {#what-is-new-cloud-manager}


* アセットのお客様は、Cloud Manager UIを使用してセルフサービスの方法でBrand Portalインスタンスをいつ、どこにデプロイするかを選択できるようになります。 アセットソリューションを使用する通常の（Sandbox以外の）プログラムの場合、Brand Portalを実稼働環境でプロビジョニングできるようになりました。 プロビジョニングは、実稼働環境で1回だけ実行できます。

* プロジェクトとサンドボックスの作成で使用されるAEMプロジェクトアーキタイプがバージョン25に更新されました。

* コードスキャン中に特定された非推奨のAPIのリストが絞り込まれ、最新Cloud ServiceのSDKリリースで非推奨となった追加のクラスとメソッドが含まれるようになりました。

* SonarQubeプロファイル（Cloud Manager用）が更新され、squid:S2142というSonarルールが削除されました。 これは、スレッド割り込みチェックと競合しなくなります。

* Cloud Manager UIは、ドメイン名を一時的に追加/更新できない可能性があるユーザーに通知します。関連付けられた環境には実行中のパイプラインが割り当てられているか、現在、承認手順を待機中です。

* sonarのプリフィックスが付いた顧客`pom.xml`ファイルに設定されたプロパティは、ビルドおよび品質スキャンの失敗を回避するために、動的に削除されるようになりました。

* Cloud Manager UIには、現在展開中のドメイン名でSSL証明書が使用されている場合、SSL証明書を一時的に選択できない可能性があるユーザーに通知されます。

* Cloud Serviceの互換性の問題をカバーするため、コード品質ルールが追加されました。

### バグ修正 {#bug-fixes-cloud-manager}

* ドメイン名に対するSSL証明書の一致で、大文字と小文字が区別されなくなりました。

* 証明書の秘密鍵が2048ビットの制限を満たさない場合に、適切なエラーメッセージが表示されるように、Cloud Manager UIからユーザーに通知されるようになりました。

* Cloud Manager UIには、現在デプロイ中のドメイン名でSSL証明書が使用されている場合、SSL証明書を一時的に選択できない可能性があるユーザーに通知されます。

* 場合によっては、内部の問題が原因で環境の削除が停止することがあります。

* 一部のパイプラインエラーは、誤ってパイプラインエラーとして報告されました。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt}

コンテンツ転送ツールv1.2.4のリリース日は2021年2月10日です。

### バグ修正 {#bug-fixes-ctt}

* 複数のユーザーをマッピングする際に、一部のユーザーのIMS IDが正しくマッピングされない問題を修正しました。 この問題が修正されました。

### リリース日 {#release-date-ctt-feb}

コンテンツ転送ツール v1.2.2 のリリース日は 2021 年 2 月 1 日です。

### コンテンツ転送ツールの新機能{#what-is-new-ctt}

* コンテンツ転送ツールに、新しい機能および UI であるユーザーマッピングツールが追加されました。この機能は、コンテンツ移行アクティビティの一環として、既存のユーザーおよびグループをそれぞれの Adobe Identity Management System ID に自動的にマッピングします。詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja)を参照してください。
* コンテンツ転送ツールは、移行セットで参照されているすべてのグループとユーザーを子も含めて移行するようになりました。
* 移行セットの作成時に、`/etc` 下の特定のパスを選択できます。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa}

Best Practices Analyzer v2.1.2のリリース日は2021年2月19日です。

### ベストプラクティスアナライザの新機能{#what-is-new-bpa}

* AEM FormsとAEM Formsの導入の使用を検出し、AEM Formsへの移行に関連する領域をCloud Serviceとして示す機能。
* カスタムコンポーネントとテンプレートの使用状況と数を検出し、レポートする機能。
* 使用するノードストアとデータストアの種類を検出する機能。
* Dynamic Mediaの使い方を検出する能力。
* 使用するJavaバージョンの検出機能。

## コードリファクタリングツール {#code-refactoring-tools}

### コードリファクタリングツールの新機能{#what-is-new-crt}

* AIO-CLI プラグインの新しいバージョンがリリースされました。このプラグインの最新バージョンには、リポジトリの最新化機能に関するいくつかのバグ修正が含まれています。
このプラグインの詳細については、[統合エクスペリエンス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=ja#benefits)を参照してください。

### バグ修正 {#bug-fixes-crt}

* リポジトリの最新化で行われたいくつかのバグ修正。
[GitHubリソースを参照：aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)を参照してください。

