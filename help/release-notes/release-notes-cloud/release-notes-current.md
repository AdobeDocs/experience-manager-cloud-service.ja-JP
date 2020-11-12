---
title: Cloud Serviceとしての2020.10.0リリース [!DNL Adobe Experience Manager] のリリースノート。
description: '[!DNL Adobe Experience Manager] を2020.10.0のCloud Serviceリリースノートとして追加しました。'
translation-type: tm+mt
source-git-commit: 65752c7c51538de27aa2b21695e8eb6c6695a5f5
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 19%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

The following section outlines the general Release Notes for [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## リリース日 {#release-date}

The Release Date for [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 is October 28, 2020.
次のリリース(2020.11.0)は、2020年12月1日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

<!-- add when release done: * **Core Components 2.12.0**: With Core Components being on auto-update, benefit from the latest improvements contributed by the community. See list of changes since 2.11.1: Release Notes -->

* **プロジェクトアーキタイプ24**:新しいAEMプロジェクトを開始するための推奨基盤が、新しいAdobeクライアントデータレイヤーを含む、AMPにサイトを配信するオプションと、プロジェクトCSS/JSを追加する新しい拡張ポイントを含む、改善されました。

* **ContextHubフォルダ**:ContextHubオファーのターゲット設定機能で使用するオーディエンスセグメントを簡単に整理、検索、選択できるオーディエンスを作成できます。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* **[!DNL Adobe Sensei]powered video smart tagging**:AIモデルを利用して、オブジェクトおよびアクション固有のタグのビデオコンテンツを分析することで、DAMユーザーは、タグの追加に費やす時間を短縮し、公開されたリッチ情報を利用して顧客に適切なエクスペリエンスを提供できます。 詳しくは、 [スマートタグビデオアセット](/help/assets/smart-tags-video-assets.md)。

* **ブランドポータルの強化**:では、次の新機能およびその他の機能を利用でき [!DNL Brand Portal]ます。 詳しくは、「[[!DNL Brand Portal] リリースノート](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html)」を参照してください。

   * [ダウンロード操作が強化され、シンプルで迅速なダウンロードが可能になりました](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) 。 その他のダウンロード設定は、ユーザーや企業のニーズに合ったエクスペリエンスをオファーするために管理者が設定できます。
   * 「ファイル」、「 [コレクション](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)」、「共有リンク」への1クリックナビゲーションが、どのページからでも可能になりました。
   * ユーザーは、特定のレンディションを [選択してダウンロードできる](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) 。 新しいレンディションのダウンロードオプションは、アセットの詳細ページのレンディションパネルで使用できます。
   * ゲストユーザーセッションのタイムアウトを15分に設定すると、すべての同時ユーザーに対して快適なエクスペリエンスが提供されます。

* **[!DNL Adobe Asset Link]バージョン2.1**:、およびの新しいバージョンの [Adobeアセットリンク](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) 拡張 [!DNL Adobe Photoshop]を使用で [!DNL Adobe Illustrator][!DNL Adobe InDesign] きます。 2020年10月にリリースされたバージョン2021の最新 [!DNL Adobe Creative Cloud] アプリケーションとの互換性を追加します。

* **[!DNL Assets]WebPファイルのサポート**: [!DNL Assets] をCloud ServiceがWebP画像形式に対応するようになりました。 WebPは、Googleが作成する新しい画像形式です。 WebPファイル形式の画像は、JPGまたはPNGファイルと区別できず、ファイルサイズは非常に小さくなります。 アセットのファイルサイズが小さくなると、ページ読み込み時間が短縮され、コンテンツ作成者はWebエクスペリエンスをより高速に利用できます。 標準処理プロファイルの [作成を参照してください](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 最新のCIFコアコンポーネントバージョンv1.4.0を含むCIFベニアリファレンスサイト — 2020.10.2をリリースしました。詳細は、『 [CIFベニアリファレンスサイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) 』を参照してください。

* CIFコアコンポーネントv1.4.0をリリースしました。詳しくは、「 [CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) 」を参照してください。

### バグ修正 {#bug-fixes-commerce}

* 製品コンソールとピッカーのGraphQLリクエストは、HTTPPOSTを使用して行われました。 この問題は、Apollo GraphQLクライアントがGraphQLクライアントのOSGi設定内の設定を順守し、設定されている場合にGETリクエストをサポートするように修正されました。

* CIF Cloud config UIで、/libと/apps/の設定用の「保存して閉じる」ボタンが表示される問題を修正しました。 ただし、これらは読み取り専用なので、「閉じる」ボタンのみが表示されるように修正されました。

## Cloud Manager {#cloud-manager}

* 環境ページのデザインが変更されました。

* 環境が休止状態になると、Cloud Manager に個別のステータスが表示されるようになりました。

* Cloud Managerビルドコンテナで、Java 8またはJava 11を使用したプロジェクトのコンパイルがサポートされるようになりました。 Java 11のサポートは、Mavenツールチェーンシステムによって提供されます。

* 環境ごとの環境変数の数が 200 に増えました。

* 概要ページの環境カードには、最大3環境のリストが表示されます。 「すべてを **表示** 」ボタンを選択して環境の概要ページに移動し、環境の完全なリストを含む表を表示できます。
詳しくは、「 [環境の](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 表示」を参照してください。

### バグ修正 {#bug-fixes-cloud-manager}

* 環境が完全に作成される前に、Cloud Manager から開発者コンソールへのリンクが正しくアクティブになっていませんでした。

* Cloud Manager から開発者コンソールへの直接リンクが、サンドボックスプログラムの環境を非休止／休止にするオプションを表示していませんでした。

* 非実稼働パイプライン編集ページの「キャンセル」ボタンと「保存」ボタンが必ずしも表示されていなかった問題を修正しました。

* コード品質プロセスで特定のエラーが発生すると、ログファイルが正しく生成されない場合があります。

* 新しいプログラムを作成する際に、推奨名が既存のプログラム名と重複する場合がありました。

* 一部の大規模なパイプラインステップログは、ユーザーインターフェイスから一貫性のある方法でダウンロードできませんでした。

* 環境名の検証が、1 つずれていました。

* 何も存在しない場合、環境ページにパブリッシュセグメントと Dispatcher セグメントが表示されることがありました。


## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### ワークフロー {#workflows}

* ワークフロータイトル、ワークフローモデル、ステータス、イニシエーター、ペイロードパス、開始日に基づくワークフローインスタンスの検索のサポートが追加されました。 「 [検索ワークフローインスタンス](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)」を参照してください。

## コンテンツ転送ツール {#content-transfer-tool}

Follow this section to learn about what is new and the updates for [Content Transfer Tool](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### 新機能 {#what-is-new-ctt}

* ログのユーザーエクスペリエンスが向上しました。 タイムスタンプが抽出およびインジェストログに追加された。 ログが空かどうかを示すメッセージが追加されました。

### バグ修正 {#ctt-bug-fixes}

* 移行セットに、ファイル名が部分的に類似したパスが含まれている場合、コンテンツ転送ツールはコンテンツファイルをスキップしていました。 この問題は修正されました。
