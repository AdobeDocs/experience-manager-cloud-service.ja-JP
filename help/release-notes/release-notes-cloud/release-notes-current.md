---
title: Cloud Serviceの2020.9.0リリース [!DNL Adobe Experience Manager] のリリースノート。
description: '[!DNLAdobe Experience Manager] 2020.9.0のCloud Serviceリリースノートとして。'
translation-type: tm+mt
source-git-commit: 5fb87f82c092552aa5e1c4b569399ec0bbc0da3b
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 11%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

The following section outlines the general Release Notes for [!DNL Experience Manager] as a Cloud Service 2020.9.0.

## リリース日 {#release-date}

The Release Date for [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 is September 24, 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* シングルページアプリケーション(SPA)エディターのJavaScript SDK [がオープンソースになりました。](/help/implementing/developing/spa/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* 透かし画像ファイルは、アセットマイクロサービスで生成されるレンディションでサポートされます。 処理プロファイルとして設定でき、透かしとしてPNGファイルを使用します。 アセットの [透かしを参照してください](/help/assets/watermark-assets.md)。

* 機能強化 [!DNL Dynamic Media]

   * 一部のみの公開 — マーケティングチームは、販促用のマテリアルを作成できるように、 [!DNL Dynamic Media] スマート切り抜き画像とそれに同期する動的レンディションにアクセスでき [!DNL Dynamic Media] るようになりました。すべて、グローバル配信用にアセットを公開する必要はありま [!DNL Dynamic Media] せん。 [!DNL Experience Manager] そして [!DNL Dynamic Media] 出版は切り離され、別々に行われ、それを実現することができる。 「 [一部のみの発行](/help/assets/dynamic-media/selective-publishing.md)」を参照してください。
   * 管理者は、プロビジョニング時に受け取った [!DNL Dynamic Media] Cloud Serviceパスワードをリセットできるようになりました。 リセットは、デスクトップアプリケーションを使用しなくても、 [!DNL Experience Manager] ユーザーインターフェイスで実行でき [!DNL Dynamic Media Classic] ます。

* 以下の機能強化について詳しくは、ブランドポータル [の新機能を参照してください](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/introduction/whats-new.html)。

   * Adobe Document Cloud表示SDKとの統合により、PDFのプレビューが強化されました。
   * シングルクリックによるダウンロード機能
   * ダウンロードエクスペリエンスの新しい管理設定。

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* CIFコアコンポーネントv1.3.0をリリースしました。詳しくは、「 [CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) 」を参照してください。

* 商品やカテゴリテンプレート用の商品/カテゴリに関するプレビュー機能が利用できるようになりました。 これにより、AEMのビジネスユーザーやマーケターは、商品やカテゴリのテンプレートに実際のデータを表示できます。

* 製品およびカテゴリに追加されたプロパティページ。これにより、ビジネスユーザーは、製品のSKU/カテゴリIDに関連付けられた表示の詳細を確認できます。

* 製品コンソールに追加され、製品/カテゴリを名前または価格属性で並べ替えられるようになりました。

* 製品コンソールに追加された製品検索機能。

### バグ修正 {#bug-fixes-commerce}

* Commerce Cloud構成は継承を尊重しませんでした。 この問題は、設定に値が継承されるように修正されました。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

[!UICONTROL Cloud Manager] バージョン 2020.9.0 のリリース日は 2020 年 9 月 03 日です。

### 新機能 {#what-is-new-cloud-manager}

* 「コンテンツ監査」は、「エクスペリエンス監査」という名称に変更されました。
* ビルドプロセスは、3つの Maven コマンドに分けられています。
* Gitリポジトリを複製できない場合は、最大3回再試行されます。

### バグ修正 {#bug-fixes-cm}

* 「コンテンツ監査」タブで、パブリッシュドメインではなく作成者ドメインを使用してベースURLが正しく表示されませんでした。

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Cloud Readiness Analyzer リリース v1.1.0 の新機能と更新点については、このセクションを参照してください。

### 新機能 {#what-is-new-cra}

* Cloud Readiness Analyzer(CRA)には開始状態コンソールがあり、ユーザーがクリックしてCRAを実行するための明示的な「 **レポートの生成** 」ボタンを表示します。

* CRA UIの実行中は進行状況が表示されます。 分析中の項目と実行中に見つかった結果が表示されます。

* CRAレポートには、検索のタイプと重要度レベル別に整理された表形式で、結果の概要と数が表示されます。 その検索結果の数をクリックすると、自動的にレポート内のその検索結果の場所にスクロールします。

### バグ修正 {#cra-bug-fixes}

* 場合によっては、更新を強制した後にCRAレポートが更新されないことがありました。 このバージョンは修正されました。

## コンテンツ転送ツール {#content-transfer-tool}

このセクションでは、新機能とコンテンツ転送ツールリリースv1.1.10の更新点について説明します。

### 新機能 {#what-is-new-ctt}

* コンテンツ転送ツール(CTT)は、Azure Blob Store Data Storeをサポートしています。

* CTTユーザーインターフェイスには、30秒ごとに概要ページをリロードする自動リロード機能があります。

* CTTユーザーインターフェイスに追加されたボタンにより、 *アクセストークンを簡単に取得でき* ます。

* *URL* および *移行セット名に対する説明的な検証メッセージが追加されました*。

## コードリファクタリングツール {#code-refactoring}

この節では、コードリファクタリングツールの新機能と更新点について説明します。

### 新機能 {#what-is-new-refactoring}

[Repository Modenizer](/help/move-to-cloud-service/refactoring-tools/repo-modernizer.md) は、Cloud ServiceとしてAdobe Experience Managerに定義されたプロジェクト構造と互換性を持つように、コンテンツとコードを個別のパッケージに分割して、既存のプロジェクトパッケージを再構築するために開発されたユーティリティです。

* AIO-CLIプラグインは、Repository Modenizerをサポートしており、ユーザーはこのプラグインを使用してツールを実行できます。

   Refer to [Git Resource: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) for more details.

* Repository Modenizerユーティリティを使用すると、既存のプロジェクトパッケージを、AEM用に定義されたプロジェクト構造と互換性のあるパッケージに再構築できます。

   詳しくは、 [Gitリソースを参照してください。リポジトリの最新化](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 」を参照してください。

