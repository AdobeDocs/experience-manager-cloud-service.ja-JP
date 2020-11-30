---
title: Current Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service.
description: Current Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service.
translation-type: tm+mt
source-git-commit: 05184bbf507fe84ffb69da90502190b1a2793ee3
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 17%

---


# [!DNL Adobe Experience Manager] as a Cloud Service のリリースノート {#release-notes}

The following section outlines the general Release Notes for [!DNL Experience Manager] as a Cloud Service.

## リリース日 {#release-date}

The Release Date for [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 is October 28, 2020.
次のリリース(2020.11.0)は、2020年12月1日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] の新機能 {#what-is-new-sites}

<!-- add when release done: * **Core Components 2.12.0**: With Core Components being on auto-update, benefit from the latest improvements contributed by the community. See list of changes since 2.11.1: Release Notes -->

* **プロジェクトアーキタイプ24**:新しいAEMプロジェクトを開始するための推奨基盤が、新しいAdobeクライアントデータレイヤーを含む、AMPにサイトを配信するオプションと、プロジェクトCSS/JSを追加する新しい拡張ポイントを含む、改善されました。

* **ContextHubフォルダ**:ContextHubオファーのターゲット設定機能で使用するオーディエンスセグメントを簡単に整理、検索、選択できるオーディエンスを作成できます。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### [!DNL Assets] の新機能 {#what-is-new-assets}

* **[!DNL Adobe Sensei]powered video smart tagging**:AIモデルを利用して、オブジェクトおよびアクション固有のタグのビデオコンテンツを分析することで、DAMユーザーは、タグの追加に費やす時間を短縮し、公開されたリッチ情報を利用して顧客に適切なエクスペリエンスを提供できます。 詳しくは、 [スマートタグビデオアセット](/help/assets/smart-tags-video-assets.md)。

* **ブランドポータルの強化**:では、次の新機能およびその他の機能を利用でき [!DNL Brand Portal]ます。 詳しくは、「[[!DNL Brand Portal] リリースノート](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html)」を参照してください。

   * [ダウンロード操作が強化され、シンプルで迅速なダウンロードが可能になりました](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) 。 その他のダウンロード設定は、ユーザーや企業のニーズに合ったエクスペリエンスをオファーするために管理者が設定できます。
   * 「ファイル」、「 [コレクション](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)」、「共有リンク」への1クリックナビゲーションが、どのページからでも可能になりました。
   * ユーザーは、特定のレンディションを [選択してダウンロードできる](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) 。 新しいレンディションのダウンロードオプションは、アセットの詳細ページのレンディションパネルで使用できます。
   * ゲストユーザーセッションのタイムアウトを15分に設定すると、すべての同時ユーザーに対して快適なエクスペリエンスが提供されます。

* **[!DNL Adobe Asset Link]バージョン2.1**:、およびの新しいバージョンの [Adobeアセットリンク](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) 拡張 [!DNL Adobe Photoshop]を使用で [!DNL Adobe Illustrator][!DNL Adobe InDesign] きます。 2020年10月にリリースされたバージョン2021の最新 [!DNL Adobe Creative Cloud] アプリケーションとの互換性を追加します。

* **[!DNL Assets]WebPファイルのサポート**: [!DNL Assets] をCloud ServiceがWebP画像形式でのレンディションの作成をサポートするようになりました。 WebPは、Googleが作成する新しい画像形式です。 WebPファイル形式の画像は、JPGまたはPNGファイルと区別できず、ファイルサイズは非常に小さくなります。 アセットのファイルサイズが小さくなると、ページ読み込み時間が短縮され、コンテンツ作成者はWebエクスペリエンスをより高速に利用できます。 標準処理プロファイルの [作成を参照してください](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 最新のCIFコアコンポーネントバージョンv1.4.0を含むCIFベニアリファレンスサイト — 2020.10.2をリリースしました。詳細は、『 [CIFベニアリファレンスサイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) 』を参照してください。

* CIF コアコンポーネント v1.4.0 をリリースしました。詳しくは、「[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0)」を参照してください。

### バグ修正 {#bug-fixes-commerce}

* 製品コンソールとピッカーのGraphQLリクエストは、HTTPPOSTを使用して行われました。 この問題は、Apollo GraphQLクライアントがGraphQLクライアントのOSGi設定内の設定を順守し、設定されている場合にGETリクエストをサポートするように修正されました。

* CIF Cloud config UIで、/libと/apps/の設定用の「保存して閉じる」ボタンが表示される問題を修正しました。 ただし、これらは読み取り専用なので、「閉じる」ボタンのみが表示されるように修正されました。


## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEMのCloud ManagerのCloud Service2020.11.0のリリース日は2020年11月12日です。

### [!DNL Cloud Manager] の新機能 {#what-is-new-cm}

* 新しいメニューオプション **「ローカルログイン** 」が、 **環境カードおよび** 環境 **** 概要ページの環境メニューオプションから利用できるようになりました。
詳しくは、[環境の管理](/help/implementing/cloud-manager/manage-environments.md##login-locally)を参照してください。

* The **Learn** tab in Cloud Manager has been refreshed with new images in the UI.

### バグ修正 {#bug-fixes-cloud-manager}

* ビルドの実行に先立っておこなわれる依存関係の読み込みには、Maven プラグインのダウンロードが必要でした。
* 言語を選択するための Cloud Manager フッターからのリンクが、正しい場所を指すようになりました。
* コードスキャン時に SonarQube プロセスが起動しないことがあります。これが自動検出され、再起動が試行されるようになりました。
* 既存のすべての実稼働パイプラインは、「エクスペリエンス監査」の手順で自動的に有効になります。

## Adobe Experience Manager as a Cloud Service の基礎 {#cloud-service-foundation}

### ワークフロー {#workflows}

* ワークフロータイトル、ワークフローモデル、ステータス、イニシエーター、ペイロードパス、開始日に基づくワークフローインスタンスの検索のサポートが追加されました。 「 [検索ワークフローインスタンス](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)」を参照してください。

## コンテンツ転送ツール {#content-transfer-tool}

Follow this section to learn about what is new and the updates for [Content Transfer Tool](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### 新機能 {#what-is-new-ctt}

* ログのユーザーエクスペリエンスが向上しました。 タイムスタンプが抽出およびインジェストログに追加された。 ログが空かどうかを示すメッセージが追加されました。

### バグ修正 {#ctt-bug-fixes}

* 移行セットに、ファイル名が部分的に類似したパスが含まれている場合、コンテンツ転送ツールはコンテンツファイルをスキップしていました。 この問題は修正されました。

## ベストプラクティスアナライザ {#best-practices-analyzer}

### リリース日 {#release-date-bpa}

Best Practices Analyzerのリリース日は2020年11月14日です。

### [!DNL Best Practices Analyzer] の新機能 {#what-is-new-bpa}

* Cloud Readiness Analyzerは、BPA (Best Practices Analyzer)になりました。 BPAは、現在のAEM実装のベストプラクティスの評価を提供し、既存のAEMインスタンスからAEMにCloud Serviceとして移行する準備を評価するのに役立ちます。

* の使用を検出する新しいディテクターが追加されました。 `java.io.InputStream`これは、AEMでCloud Serviceーとして使用すると問題を引き起こす可能性があります。

### バグ修正 {#bpa-bug-fixes}

* TextField Foundationコンポー *ネントに関連する肯定的な原因となるバグが修正されました* 。
