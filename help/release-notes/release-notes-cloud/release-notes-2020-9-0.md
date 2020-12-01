---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service の 2020.9.0 リリースのリリースノート。'
description: '[!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 のリリースノート。'
translation-type: tm+mt
source-git-commit: 701d9ff3c9553c28bce0ef417487facedb22373f
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 100%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 のリリースノート {#release-notes}

[!DNL Experience Manager] as a Cloud Service 2020.9.0 の一般的なリリースノートの概要を次に説明します。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 のリリース日は 2020 年 9 月 24 日です。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] の新機能 {#what-is-new-sites}

* 単一ページアプリケーション（SPA）エディター JavaScript SDK が[オープンソース](/help/implementing/developing/hybrid/reference-materials.md)になりました。

## [!DNL Adobe Experience Manager Assets] cloud serviceとして  {#assets}

### [!DNL Assets] の新機能 {#what-is-new-assets}

* 透かし画像ファイルは、アセットマイクロサービスで生成されるレンディションでサポートされています。処理プロファイルとして設定でき、透かしとして PNG ファイルを使用します。「[アセットの透かしの設定](/help/assets/watermark-assets.md)」を参照してください。

* [!DNL Dynamic Media] の機能強化 

   * 選択的公開 - マーケティングチームは、販促用のマテリアルを作成するために、 [!DNL Dynamic Media] に同期する [!DNL Dynamic Media] スマート切り抜き画像と動的レンディションにアクセスできるようになりました。すべて、グローバル配信用にアセットを [!DNL Dynamic Media] に公開する必要はありません。[!DNL Experience Manager] および [!DNL Dynamic Media] の公開は分離されており、別々におこなうことができます。「[選択的公開](/help/assets/dynamic-media/selective-publishing.md)」を参照してください。
   * 管理者は、プロビジョニング時に受け取った [!DNL Dynamic Media] Cloud Service パスワードをリセットできるようになりました。リセットは、[!DNL Dynamic Media Classic] デスクトップアプリケーションを使用せずに、 [!DNL Experience Manager] ユーザーインターフェイスで実行できます。

* 以下の機能強化について詳しくは、「[AEM Assets Brand Portal の新機能](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/introduction/whats-new.html)」を参照してください。

   * Adobe Document Cloud 表示 SDK との統合により、PDF のプレビューが強化されました。
   * シングルクリックによるダウンロード機能。
   * ダウンロードエクスペリエンスの新しい管理設定。

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* CIF コアコンポーネント v1.3.0 をリリースしました。詳しくは、「[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0)」を参照してください。

* 製品／カテゴリテンプレート用の製品／カテゴリプレビュー機能が利用できるようになりました。これにより、AEM のビジネスユーザーやマーケターは、製品／カテゴリのテンプレートに実際のデータを表示できます。

* 製品およびカテゴリにプロパティページが追加されました。これにより、ビジネスユーザーは、製品の SKU／カテゴリ ID に関連付けられた表示の詳細を確認できます。

* 製品コンソールに並び替え機能が追加され、製品／カテゴリを名前または価格属性で並べ替えられるようになりました。

* 製品コンソールに製品検索機能が追加されました。

### バグ修正 {#bug-fixes-commerce}

* Commerce Cloud 構成は継承を尊重しませんでした。この問題は、設定に値が継承されるように修正されました。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

[!UICONTROL Cloud Manager] バージョン 2020.9.0 のリリース日は 2020 年 9 月 03 日です。

### 新機能 {#what-is-new-cloud-manager}

* 「コンテンツ監査」の名称が「エクスペリエンス監査」に変更されました。
* ビルドプロセスは、3 つの Maven コマンドに分けられました。
* git リポジトリーをクローンできない場合は、最大 3 回再試行されます。

### バグ修正 {#bug-fixes-cm}

* 「コンテンツ監査」タブで、ベース URL がパブリッシュドメインではなくオーサードメインを使用していて、正しく表示されませんでした。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Cloud Readiness Analyzer リリース v1.1.0 の新機能と更新点については、このセクションを参照してください。

### 新機能 {#what-is-new-cra}

* Cloud Readiness Analyzer（CRA）には開始状態コンソールがあり、クリックして CRA を実行するための明示的な「**レポートの生成**」ボタンが表示されます。

* CRA UI の実行中は進行状況が表示されます。分析中の項目と実行中に見つかった結果が表示されます。

* CRA レポートには、結果のタイプと重要度レベル別に整理された表形式で、結果の概要と数が表示されます。結果の数をクリックすると、自動的にレポート内のその検索結果の場所にスクロールします。

### バグ修正 {#cra-bug-fixes}

* 場合によっては、更新を強制した後に CRA レポートがアップデートされないことがありました。このバージョンでは修正されました。

## コンテンツ転送ツール {#content-transfer-tool}

コンテンツ転送ツールリリース v1.1.10 の新機能と更新点については、このセクションを参照してください。

### 新機能 {#what-is-new-ctt}

* コンテンツ転送ツール（CTT）は、Azure Blob Store Data Store をサポートしています。

* CTT ユーザーインターフェイスには、30 秒ごとに概要ページをリロードする自動リロード機能があります。

* CTT ユーザーインターフェイスに追加されたボタンにより、*アクセストークン*&#x200B;を簡単に取得できます。

* *URL* および&#x200B;*移行セット名*&#x200B;に対する説明的な検証メッセージが追加されました。

## コードリファクタリングツール {#code-refactoring}

コードリファクタリングツールの新機能と更新点については、このセクションを参照してください。

### 新機能 {#what-is-new-refactoring}

* AIO-CLI プラグインは、Repository Modenizer をサポートしており、ユーザーはこのプラグインを使用してツールを実行できます。

   詳しくは、[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) を参照してください。

* Repository Modenizer ユーティリティを使用すると、既存のプロジェクトパッケージを、AEM as a Cloud Service 用に定義されたプロジェクト構造と互換性のあるパッケージに再構築できます。

   詳しくは、[Git リソース：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) を参照してください。

