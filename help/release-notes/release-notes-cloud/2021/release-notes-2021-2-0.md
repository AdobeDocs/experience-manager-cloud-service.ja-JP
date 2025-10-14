---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.2.0 リリースのリリースノート。'
description: 「[!DNL Adobe Experience Manager] as a Cloud Service 2021.2.0 のリリースノート」
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 92%

---


# [!DNL Adobe Experience Manager] as a Cloud Service のリリースノート {#release-notes}

[!DNL Experience Manager] as a Cloud Service の一般的なリリースノートの概要を次に説明します。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2021.2.0 のリリース日は 2021 年 2 月 25 日です。次回のリリース（2021.3.0）は、2021 年 3 月 25 日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### ヘッドレスコンテンツ管理 {#headless}

* **[コンテンツフラグメント配信用の GraphQL API](/help/headless/graphql-api/content-fragments.md)**：GraphQL 構文を使用してコンテンツフラグメントのクエリを実行する機能と、JSON 形式で出力するための、コンテンツフラグメントモデルに基づくスキーマが用意されました。

* **[GraphQL API リクエストの認証サポート](/help/headless/security/authentication.md)**：サーバー側 API のアクセストークンで GraphQL API リクエストを認証できるようになりました。

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

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/sites-console/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## [!DNL Assets] の新機能 {#what-is-new-assets}

* アセットは [!DNL Experience Manager Assets Brand Portal] を使用してソーシングできます。これは、新しいマーケティングキャンペーン、撮影、プロジェクトのためにエージェンシーユーザーからアセットをソーシングするのに役立ちます。

* [!DNL Experience Manager Assets] as a [!DNL Cloud Service] には、事前設定済みの [!DNL Brand Portal] インスタンスが用意されています。[!DNL Cloud Manager] ユーザーは、[!DNL Experience Manager Assets] as a [!DNL Cloud Service] 上で [!DNL Brand Portal] をアクティブ化できます。[Brand Portal のライセンス認証](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=ja)を参照してください。

* 企業が [!DNL Brand Portal] を使用してアセットソーシングを行えるようになりました。アセットソーシング機能では、[!DNL Brand Portal] を使用して顧客とエージェンシーユーザーの連携を支援し、顧客が新しいマーケティングキャンペーン、撮影、プロジェクトのためのアセットソーシングをおこなえるようにします。 詳しくは、[&#x200B; [!DNL Brand Portal] でのアセットソーシング](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=ja)を参照してください。

* [!DNL Brand Portal] 使用状況レポートには、アクティブユーザーのみ表示されるようになりました。非アクティブユーザーは表示されなくなりました。アクティブユーザーとは、[!DNL Admin Console] で製品プロファイルにアカウントが割り当てられているユーザーのことです。詳しくは、[[!DNL Brand Portal] レポート](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html?lang=ja)を参照してください。

* [!DNL Brand Portal] には、フォルダーやコレクションなどをダウンロードする際にアセットごとに別個のフォルダーを作成できる新しいダウンロード設定が導入されました。詳しくは、[ダウンロード設定](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=ja)を参照してください。

## [!DNL Assets] のバグ修正  {#bug-fixes-assets}

* 複数のアセットを選択してプロパティを更新すると、エラーが発生したり、選択されていないアセットのプロパティが更新されたりする場合があります。（CQ-4316532）
* [!UICONTROL アセット管理者の検索レール]を開こうとすると、ページが空白のままで、[!UICONTROL 編集]／[!UICONTROL 設定]をクリックするとエラーが発生します。（CQ-4315079）
* 名前の競合を解決した後で既存のアセットの新しいバージョンを作成すると、元のアセットのメタデータが上書きされます。（CQ-4313594）
* 長い注釈テキストを含むアセットを印刷すると、スペースに余裕があっても、注釈テキストがトリミングされます。（CQ-4314101）

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 製品エクスペリエンス管理：エクスペリエンスフラグメントを使用して製品カタログページを個別に拡充することができます。

* 製品コンソールプロパティを拡張して、関連するコンテンツにすばやく移動するためのアクションなど、アセットやエクスペリエンスフラグメントのリンクを表示するようになりました。

* 最新のCIF コアコンポーネント v1.8.0 を含んだCIF Venia 参照サイト 2021.02.24 をリリースしました。詳しくは、[CIF Venia 参照サイト &#x200B;](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24) を参照してください。

* CIF コアコンポーネント v1.8.0 をリリースしました。詳しくは、[CIF コアコンポーネント &#x200B;](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0) を参照してください。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEM as a Cloud Service 2021.2.0 Cloud Manager のリリース日は 2021 年 2 月 11 日です。

### 新機能 {#what-is-new-cloud-manager}


* Assets ユーザーは、Brand Portal インスタンスをデプロイするタイミングと場所を、Cloud Manager UI を使用してセルフサービス方式で選択できるようになりました。Assets ソリューションを使用する通常の（サンドボックス以外の）プログラムの場合は、Brand Portal を実稼動環境にプロビジョニングできるようになりました。プロビジョニングは、実稼働環境で 1 回だけ行えます。

* プロジェクトとサンドボックスの作成で使用される AEM プロジェクトアーキタイプがバージョン 25 に更新されました。

* コードスキャン中に特定される非推奨（廃止予定）API のリストが改善され、最新の Cloud Service SDK リリースで新たに非推奨となったクラスとメソッドが含まれるようになりました。

* Cloud Manager の SonarQube プロファイルが更新され、squid:S2142 の Sonar ルールが削除されました。これは、スレッド割り込みチェックと競合しなくなりました。

* 関連付けられた環境で、実行中のパイプラインが割り当てられているか、現在、承認ステップ待ちの状態にあるため、一時的にドメイン名を追加／更新できない可能性がある場合は、Cloud Manager UI からユーザーに通知されるようになりました。

* ユーザーの `pom.xml` ファイルで設定されたプロパティのうち、先頭に sonar が付いているものは、ビルドおよび品質スキャン時のエラーを避けるために、動的に削除されるようになりました。

* 現在デプロイ中のドメイン名で使用されている SSL 証明書を一時的に選択できない可能性がある場合は、Cloud Manager UI からユーザーに通知されるようになりました。

* Cloud Service の互換性の問題をカバーするため、コード品質ルールが追加されました。

### バグの修正 {#bug-fixes-cloud-manager}

* ドメイン名に対する SSL 証明書の照合で、大文字と小文字が区別されなくなりました。

* 証明書の秘密鍵が 2048 ビット制限を満たさない場合は、Cloud Manager UI から適切なエラーメッセージでユーザーに通知されるようになりました。

* 現在デプロイ中のドメイン名で使用されている SSL 証明書を一時的に選択できない可能性がある場合は、Cloud Manager UI からユーザーに通知されるようになりました。

* 場合によっては、内部の問題が原因で環境の削除が停止することがあります。

* パイプラインの不具合が誤ってパイプラインエラーとして報告されることがありました。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.2.4 のリリース日は 2021 年 2 月 10 日です。

### バグの修正 {#bug-fixes-ctt}

* 複数のユーザーをマッピングする際に、一部のユーザーの IMS ID が正しくマッピングされていませんでした。 この問題が修正されました。

### リリース日 {#release-date-ctt-feb}

コンテンツ転送ツール v1.2.2 のリリース日は 2021 年 2 月 1 日です。

### コンテンツ転送ツールの新機能 {#what-is-new-ctt}

* コンテンツ転送ツールに、新しい機能および UI であるユーザーマッピングツールが追加されました。この機能は、コンテンツ移行アクティビティの一環として、既存のユーザーおよびグループをそれぞれの Adobe Identity Management System ID に自動的にマッピングします。詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja)を参照してください。
* コンテンツ転送ツールは、移行セットで参照されているすべてのグループとユーザーを子も含めて移行するようになりました。
* 移行セットの作成時に、`/etc` 下の特定のパスを選択できます。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.2 のリリース日は 2021 年 2 月 18 日です。

### ベストプラクティスアナライザーの新機能 {#what-is-new-bpa}

* AEM Forms と AEM Forms 実装が使用されていることを検出し、AEM Forms as a Cloud Service に移行した方がよい部分を指摘できるようになりました。
* カスタムコンポーネントおよびテンプレートの使用状況と使用回数を検出しレポートできるようになりました。
* 使用されているノードストアとデータストアの種類を検出できるようになりました。
* Dynamic Media の使用状況を検出できるようになりました。
* 使用されている Java のバージョンを検出できるようになりました。

## コードリファクタリングツール {#code-refactoring-tools}

### コードリファクタリングツールの新機能 {#what-is-new-crt}

* AIO-CLI プラグインの新しいバージョンがリリースされました。このプラグインの最新バージョンでは、Repository Modernizer のいくつかのバグが修正されています。
このプラグインについて詳しくは、[Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=ja#benefits) を参照してください。

### バグの修正 {#bug-fixes-crt}

* Repository Modernizer で行われたいくつかのバグ修正。
詳しくは、[GitHub リソース：aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) を参照してください。
