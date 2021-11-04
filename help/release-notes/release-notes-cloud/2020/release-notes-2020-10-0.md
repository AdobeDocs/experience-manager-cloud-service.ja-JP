---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 リリースのリリースノート。'
description: '[!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 のリリースノート。'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: 15908636f916a55008513035e3072cf1b1cc5f1c
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 60%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 のリリースノート  {#release-notes}

[!DNL Experience Manager] as a Cloud Service 2020.10.0 の一般的なリリースノートの概要を次に説明します。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 のリリース日は 2020 年 10 月 28 日です。次回のリリース（2020.11.0）は、2020 年 12 月 1 日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] の新機能  {#what-is-new-sites}

* **[コアコンポーネント2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)**:Adobe Experience Manager as a Cloud Serviceは、コアコンポーネントの最新リリースに対する自動アップデートのメリットを享受できます。 リリース2.12.0には、コミュニティが提供する最新の機能強化が含まれています。 改善点は次のとおりです。 [新しいPOSTフォームハンドラ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html?lang=ja#post-data) カスタム CSS、JavaScript、メタデータを含める機能 [コンテキスト対応設定を介したタグ。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html?lang=ja#context-aware-loading) および [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html?lang=ja#enabling-custom-components) カスタムコンポーネントでAdobeデータレイヤーを簡単に統合するためのユーティリティ。 リリース 2.12.0 の[変更点の一覧](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0)を参照してください。

* **[プロジェクトアーキタイプ 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)**:新しいプロジェクトを開始するための推奨されるExperience Managerが向上しました。 新しい [Adobeクライアントデータレイヤー](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=ja)、オプション [AMP でサイトを配信](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html?lang=ja) および新規 [拡張機能は、プロジェクト CSS/JS を追加するためのポイントです。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[ContextHub フォルダー](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**:オーディエンスフォルダーを作成して、ContextHub オファーのターゲティング機能で使用するオーディエンスセグメントを簡単に整理、検索および選択できます。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

* **[!DNL Adobe Sensei]powered video smart tagging**:AI モデルを適用してオブジェクトおよびアクション固有のタグのビデオコンテンツを分析することで、DAM ユーザーは、公開されたリッチな情報を使用して、タグの追加に費やす時間を短縮し、より多くの時間を費やすことができます。 その結果、お客様に適切なエクスペリエンスを提供できます。 [ビデオアセットのスマートタグ](/help/assets/smart-tags-video-assets.md)を参照してください。

* **Brand Portal の機能強化**：次の新機能などが [!DNL Brand Portal] で利用できます。詳しくは、[[!DNL Brand Portal] リリースノート](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html?lang=ja)を参照してください。

   * [ダウンロード機能の強化](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=ja)で、ダウンロードがすばやく簡単に行えるようになりました。追加のダウンロード設定を管理者が指定すれば、ユーザーや企業のニーズに合ったエクスペリエンスを提供できます。
   * どのページからでもワンクリックでファイル、[コレクション](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html?lang=ja)、共有リンクに移動できるようになりました。
   * ユーザーは[特定のレンディションを選択してダウンロード](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=ja#download-assets-from-asset-details-page)できるようになりました。アセットの詳細ページのレンディションパネルで新しいレンディションダウンロードオプションが使用可能です。
   * ゲストユーザーセッションが 15 分でタイムアウトするので、同時使用中のすべてのユーザーにとってエクスペリエンスが向上します。

* **[!DNL Adobe Asset Link]バージョン 2.1**：[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]、[!DNL Adobe InDesign] 用の [Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html) 拡張機能の新しいバージョンが使用可能になりました。2020 年 10 月にリリースされた最新の [!DNL Adobe Creative Cloud] 2021 アプリケーションとの互換性が追加されました。

* **[!DNL Assets]WebP ファイルのサポート**：[!DNL Assets] as a Cloud Service では WebP 画像形式をサポートするようになりました。WebP は、Google が作成した新たな画像形式です。WebP ファイル形式の画像は、JPG ファイルや PNG ファイルと見た目に区別がつきませんが、ファイルははるかに小さくなります。アセットのファイルサイズが小さくなると、ページ読み込み時間が改善され、コンテンツクリエーターが Web エクスペリエンスを高速化するのに役立ちます。WebP の使用方法については、[アセットマイクロサービスと処理プロファイルの使用](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)を参照してください。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#forms-oct-2021}

### [!DNL Forms] の新機能  {#what-is-new-forms-oct-2021}

* **Analytics for Adaptive Forms**:Adobe Analytics for Adaptive Formsでログイン済みとログインしていない（匿名）の両方の動作を取得および追跡して、エンドユーザーのインサイトを収集できるようになりました。 これにより、ビジネスユーザーは収集されたインサイトに基づいて、十分な情報に基づいて、アダプティブフォームのコンテンツ、レイアウトおよびスタイルに関する決定を下すことができます。

### [!DNL Forms]プレリリースチャネルで利用できる新機能 {#prerelease-features-forms-oct-2021}

* **AEM Workflow データを外部化して処理を保護**:顧客が管理するリポジトリに、機密の個人データ (SPD) 要素を含むプロセス内のAEM Workflow 変数データを保存して、処理を安全に行うことができます。 ワークフローの処理中、ワークフロー変数に保存されたデータはAEMリポジトリに保持されません。 顧客が管理するリポジトリからオンデマンドで取得されます。

### [!DNL Forms] のベータ版機能 {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=ja) は、テンプレートと XML データを組み合わせて、様々な形式のドキュメントを生成する場合に役立ちます。 このサービスを使用すると、同期モードとバッチモードでドキュメントを生成できます。

[!DNL formscsbeta@adobe.com] に書き込んで、ベータ版プログラムにサインアップできます。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 最新の CIF コアコンポーネント v1.4.0 を含んだ CIF Venia 参照サイト 2020.10.2 をリリースしました。詳しくは、[CIF Venia 参照サイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2)を参照してください。

* CIF コアコンポーネント v1.4.0 をリリースしました。詳しくは、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0)を参照してください。

### バグ修正 {#bug-fixes-commerce}

* 製品コンソールとピッカーにあった GraphQL リクエストは、HTTPPOSTを介して実行されました。 この問題は、Apollo GraphQL クライアントが GraphQL クライアント OSGi 設定の設定に従って、GETリクエストを設定した場合にサポートするようにするために修正されました。

* CIF クラウド設定 UI で、/lib および /apps/ 内の設定に「保存して閉じる」ボタンが表示されていました。しかし、これらのインターフェイスは読み取り専用なので、UI は「閉じる」ボタンのみを表示するように修正されました。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

Experience Manageras a Cloud Service2020.10.0の Cloud Manager のリリース日は 2020 年 10 月 2 日です。

### [!DNL Cloud Manager] の新機能  {#what-is-new-cm}

* 環境ページのデザインが変更されました。

* 環境が休止状態になると、Cloud Manager に個別のステータスが表示されるようになりました。

* Cloud Manager の「ビルドコンテナ」で、Java™ 8 または Java™ 11 を使用したプロジェクトのコンパイルがサポートされるようになりました。 Java™ 11 のサポートは、Maven ツールチェーンシステムで提供されます。

* 環境ごとの環境変数の数が 200 に増えました。

* 概要ページの環境カードに、最大 3 つの環境が一覧表示されるようになりました。 「**すべてを表示**」ボタンを選択して環境の概要ページに移動し、環境の完全なリストを含む表を表示できます。
詳しくは、「[環境の表示](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)」を参照してください。

### バグ修正 {#bug-fixes-cloud-manager}

* 環境が完全に作成される前に、Cloud Manager から開発者コンソールへのリンクが正しくアクティブになっていませんでした。

* Cloud Manager から開発者コンソールへの直接リンクが、サンドボックスプログラムの環境を非休止／休止にするオプションを表示していませんでした。

* 非実稼動パイプライン編集ページの「キャンセル」ボタンおよび「保存」ボタンが常には表示されていませんでした。

* コード品質プロセスで特定のエラーが発生すると、ログファイルが正しく生成されない場合があります。

* プログラムを作成する際に、推奨名が既存のプログラム名と重複する場合がありました。

* 一部の大規模なパイプラインステップログは、ユーザーインターフェイスから一貫性のある方法でダウンロードできませんでした。

* 環境名の検証が、1 つずれていました。

* 何も存在しない場合、環境ページにパブリッシュセグメントと Dispatcher セグメントが表示されることがありました。

## Adobe Experience Manager as a Cloud Service の基盤 {#cloud-service-foundation}

### ワークフロー {#workflows}

* ワークフロータイトル、ワークフローモデル、ステータス、イニシエーター、ペイロードパス、開始日に基づいてワークフローインスタンスを検索できるようになりました。詳しくは、[ワークフローインスタンスの検索](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html?lang=ja)を参照してください。

## コンテンツ転送ツール {#content-transfer-tool}

の新機能と更新の詳細 [コンテンツ転送ツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=ja) リリース v1.1.12。

### 新機能 {#what-is-new-ctt}

* ログのユーザーエクスペリエンスが向上しました。抽出ログと取り込みログにタイムスタンプが追加されました。ログが空かどうかを知らせるメッセージが追加されました。

### バグ修正 {#ctt-bug-fixes}

* 移行セットに、部分的に類似したファイル名を持つパスが含まれている場合、コンテンツ転送ツールはコンテンツファイルをスキップしていました。
