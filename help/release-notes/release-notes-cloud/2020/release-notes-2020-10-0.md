---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 リリースのリリースノート。'
description: '[!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 のリリースノート。'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 96%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 のリリースノート  {#release-notes}

[!DNL Experience Manager] as a Cloud Service 2020.10.0 の一般的なリリースノートの概要を次に説明します。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 のリリース日は 2020 年 10 月 28 日です。次回のリリース（2020.11.0）は、2020 年 12 月 1 日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] の新機能  {#what-is-new-sites}

* **[コアコンポーネント 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)**：AEM as a Cloud Service には、コアコンポーネントの最新リリースへの自動アップデート機能があります。リリース 2.12.0 では、最新の機能改善がコミュニティからの貢献として含まれています。例えば、[新しい POST フォームハンドラー](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html?lang=ja#post-data)、カスタムの CSS タグ、JavaScript タグ、メタデータタグを[コンテキスト対応の設定](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html?lang=ja#context-aware-loading)で組み込む機能、カスタムコンポーネントで Adobe データレイヤーとの統合を簡単に行うための [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html?lang=ja#enabling-custom-components) ユーティリティなどです。リリース 2.12.0 の[変更点の一覧](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0)を参照してください。

* **[プロジェクトアーキタイプ 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)**：新規 AEM プロジェクトを開始する際の推奨される基盤が改善され、新しい [Adobe Client Data Layer](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=ja)、[AMP でサイトを作成](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html?lang=ja)するオプション、[プロジェクトの CSS／JS を追加するための新しい拡張ポイント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)が含まれるようになりました。

* **[ContextHub フォルダー](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**：ContextHub オファーターゲティング機能に使用するオーディエンスセグメントを容易に整理、検索、選択するためのオーディエンスフォルダーを作成できます。

## [!DNL Adobe Experience Manager Assets] Cloud Service {#assets}

* **[!DNL Adobe Sensei]を活用したビデオスマートタグ**：AI モデルを活用してオブジェクトおよびアクション固有のタグのビデオコンテンツを分析することで、DAM ユーザーはタグ付けに費やす時間を短縮し、公開された豊富な情報を利用して適切なエクスペリエンスを顧客に提供することに多くの時間を割くことができます。[ビデオアセットのスマートタグ](/help/assets/smart-tags-video-assets.md)を参照してください。

* **Brand Portal の機能強化**：次の新機能などが [!DNL Brand Portal] で利用できます。詳しくは、[[!DNL Brand Portal] リリースノート](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html)を参照してください。

   * [ダウンロード機能の強化](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=ja)で、ダウンロードがすばやく簡単に行えるようになりました。追加のダウンロード設定を管理者が指定すれば、ユーザーや企業のニーズに合ったエクスペリエンスを提供できます。
   * どのページからでもワンクリックでファイル、[コレクション](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)、共有リンクに移動できるようになりました。
   * ユーザーは[特定のレンディションを選択してダウンロード](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page)できるようになりました。アセットの詳細ページのレンディションパネルで新しいレンディションダウンロードオプションが使用可能です。
   * ゲストユーザーセッションが 15 分でタイムアウトするので、同時使用中のすべてのユーザーにとってエクスペリエンスが向上します。

* **[!DNL Adobe Asset Link]バージョン 2.1**：[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]、[!DNL Adobe InDesign] 用の [Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) 拡張機能の新しいバージョンが使用可能になりました。2020 年 10 月にリリースされた最新の [!DNL Adobe Creative Cloud] 2021 アプリケーションとの互換性が追加されました。

* **[!DNL Assets]WebP ファイルのサポート**：[!DNL Assets] as a Cloud Service では WebP 画像形式をサポートするようになりました。WebP は、Google が作成した新たな画像形式です。WebP ファイル形式の画像は、JPG ファイルや PNG ファイルと見た目に区別がつきませんが、ファイルははるかに小さくなります。アセットのファイルサイズが小さくなると、ページ読み込み時間が改善され、コンテンツクリエーターが Web エクスペリエンスを高速化するのに役立ちます。WebP の使用方法については、[アセットマイクロサービスと処理プロファイルの使用](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)を参照してください。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 最新の CIF コアコンポーネント v1.4.0 を含んだ CIF Venia 参照サイト 2020.10.2 をリリースしました。詳しくは、[CIF Venia 参照サイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2)を参照してください。

* CIF コアコンポーネント v1.4.0 をリリースしました。詳しくは、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0)を参照してください。

### バグ修正 {#bug-fixes-commerce}

* 製品コンソールおよびピッカーでの GraphQL リクエストは、HTTP POST を使用して実行されていました。これは修正されて、Apollo GraphQL クライアントが GraphQL クライアント OSGi 設定に従って GET リクエストをサポートするようになりました（設定済みの場合）。

* CIF クラウド設定 UI で、/lib および /apps/ 内の設定に「保存して閉じる」ボタンが表示されていました。これらは読み取り専用なので、UI が修正されて「閉じる」ボタンのみ表示されるようになりました。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEM as a Cloud Service 2020.10.0 の Cloud Manager のリリース日は 2020 年 10 月 2 日です。

### [!DNL Cloud Manager] の新機能  {#what-is-new-cm}

* 環境ページのデザインが変更されました。

* 環境が休止状態になると、Cloud Manager に個別のステータスが表示されるようになりました。

* Cloud Manager ビルドコンテナで、Java 8 または Java 11 を使用したプロジェクトのコンパイルがサポートされるようになりました。Java 11 のサポートは、Maven ツールチェーンシステムによって提供されます。

* 環境ごとの環境変数の数が 200 に増えました。

* 概要ページの環境カードには、最大 3 環境のリストが表示されます。「**すべてを表示**」ボタンを選択して環境の概要ページに移動し、環境の完全なリストを含む表を表示できます。
詳しくは、「[環境の表示](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)」を参照してください。

### バグ修正 {#bug-fixes-cloud-manager}

* 環境が完全に作成される前に、Cloud Manager から開発者コンソールへのリンクが正しくアクティブになっていませんでした。

* Cloud Manager から開発者コンソールへの直接リンクが、サンドボックスプログラムの環境を非休止／休止にするオプションを表示していませんでした。

* 非実稼動パイプライン編集ページの「キャンセル」ボタンおよび「保存」ボタンが常には表示されていませんでした。

* コード品質プロセスで特定のエラーが発生すると、ログファイルが正しく生成されない場合があります。

* 新しいプログラムを作成する際に、推奨名が既存のプログラム名と重複する場合がありました。

* 一部の大規模なパイプラインステップログは、ユーザーインターフェイスから一貫性のある方法でダウンロードできませんでした。

* 環境名の検証が、1 つずれていました。

* 何も存在しない場合、環境ページにパブリッシュセグメントと Dispatcher セグメントが表示されることがありました。

## Adobe Experience Manager as a Cloud Service の基盤 {#cloud-service-foundation}

### ワークフロー {#workflows}

* ワークフロータイトル、ワークフローモデル、ステータス、イニシエーター、ペイロードパス、開始日に基づいてワークフローインスタンスを検索できるようになりました。詳しくは、[ワークフローインスタンスの検索](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html)を参照してください。

## コンテンツ転送ツール {#content-transfer-tool}

この節では、[コンテンツ転送ツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)リリース v1.1.12 の新機能と更新点について説明します。

### 新機能 {#what-is-new-ctt}

* ログのユーザーエクスペリエンスが向上しました。抽出ログと取り込みログにタイムスタンプが追加されました。ログが空かどうかを知らせるメッセージが追加されました。

### バグ修正 {#ctt-bug-fixes}

* 移行セットに含まれているパスのファイル名が部分的に似ている場合、コンテンツ転送ツールがコンテンツファイルをスキップしていました。この問題が修正されました。
