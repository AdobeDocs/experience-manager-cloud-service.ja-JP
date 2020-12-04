---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.10.0 リリースのリリースノート。'
description: '[!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 のリリースノート.'
translation-type: tm+mt
source-git-commit: fd271f24e5f8ddbe440dccf5c51c91a46c70dead
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 24%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 のリリースノート {#release-notes}

[!DNL Experience Manager] as a Cloud Service 2020.10.0 の一般的なリリースノートの概要を次に説明します。

## リリース日 {#release-date}

Cloud Service2020.10.0の[!DNL Adobe Experience Manager]のリリース日は2020年10月28日です。
次のリリース(2020.11.0)は、2020年12月1日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] の新機能 {#what-is-new-sites}

* **[コアコンポーネント2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)**:AEMは、コアコンポーネントの最新リリースへの自動アップデートによってCloud Service上のメリットが得られます。リリース2.12.0には、新しいPOSTフォームハンドラ[、カスタムCSS、Javascript、メタデータ[タグを含む機能（コンテキスト対応設定を使用）、](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)、[`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components)ユーティリティなど、コミュニティが提供する最新の機能が含まれています。 ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data)2.12.0の[変更のリスト](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0)を参照してください。

* **[プロジェクトアーキタイプ24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**:新しいAEMプロジェクトを開始するための推奨基盤が、新しい [Adobeクライアントデータレイヤー](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)、AMPにサイトを [配信するオプション](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) 、プロジェクトCSS/JSを追加する新しい [拡張ポイントを含めて、改善されました。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[ContextHubフォルダ](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**:ContextHubオファーのターゲット設定機能で使用するオーディエンスセグメントを簡単に整理、検索、選択できるオーディエンスを作成できます。

## [!DNL Adobe Experience Manager Assets] cloud serviceとして  {#assets}

* **[!DNL Adobe Sensei]powered video smart tagging**:AIモデルを利用して、オブジェクトおよびアクション固有のタグのビデオコンテンツを分析することで、DAMユーザーは、タグの追加に費やす時間を短縮し、公開されたリッチ情報を利用して顧客に適切なエクスペリエンスを提供できます。詳しくは、[ビデオアセットのスマートタグ付け](/help/assets/smart-tags-video-assets.md)を参照してください。

* **ブランドポータルの強化**:では、次の新機能およびその他の機能を利用でき [!DNL Brand Portal]ます。詳しくは、「[[!DNL Brand Portal] リリースノート](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html)」を参照してください。

   * [シンプルで迅速なダウンロードのた](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) めのダウンロード機能が強化されました。その他のダウンロード設定は、ユーザーや企業のニーズに合ったエクスペリエンスをオファーするために管理者が設定できます。
   * 「ファイル」、「[コレクション](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)」、「共有リンク」への1回のクリックによるナビゲーションが、どのページからでも可能になりました。
   * ユーザーは、[特定のレンディション](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page)を選択してダウンロードできるようになりました。 新しいレンディションのダウンロードオプションは、アセットの詳細ページのレンディションパネルで使用できます。
   * ゲストユーザーセッションのタイムアウトを15分に設定すると、すべての同時ユーザーに対して快適なエクスペリエンスが提供されます。

* **[!DNL Adobe Asset Link]バージョン2.1**:、およびの [Adobeアセット](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) リンク拡張機能の新しいバージョン [!DNL Adobe Photoshop]を使用 [!DNL Adobe Illustrator] [!DNL Adobe InDesign] できます。2020年10月にリリースされたバージョン2021の最新の[!DNL Adobe Creative Cloud]アプリケーションとの互換性を追加します。

* **[!DNL Assets]WebPファイルのサポート**: [!DNL Assets] をCloud ServiceがWebP画像形式に対応するようになりました。WebPは、Googleが作成する新しい画像形式です。 WebPファイル形式の画像は、JPGまたはPNGファイルと区別できず、ファイルサイズは非常に小さくなります。 アセットのファイルサイズが小さくなると、ページ読み込み時間が短縮され、コンテンツ作成者はWebエクスペリエンスをより高速に利用できます。 [処理プロファイルの作成](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)のWebPの使い方を参照してください。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 最新のCIFコアコンポーネントバージョンv1.4.0を含むCIFベニアリファレンスサイト — 2020.10.2をリリースしました。詳細は、[CIFベニアリファレンスサイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2)を参照してください。

* CIF コアコンポーネント v1.4.0 をリリースしました。詳しくは、「[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0)」を参照してください。

### バグ修正 {#bug-fixes-commerce}

* 製品コンソールとピッカーのGraphQLリクエストは、HTTPPOSTを使用して行われました。 この問題は、Apollo GraphQLクライアントがGraphQLクライアントのOSGi設定内の設定を順守し、設定されている場合にGETリクエストをサポートするように修正されました。

* CIF Cloud config UIで、/libと/apps/の設定用の「保存して閉じる」ボタンが表示される問題を修正しました。 ただし、これらは読み取り専用なので、「閉じる」ボタンのみが表示されるように修正されました。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEMのCloud ManagerのCloud Service2020.10.0のリリース日は2020年10月2日です。

### [!DNL Cloud Manager] の新機能 {#what-is-new-cm}

* 環境ページのデザインが変更されました。

* 環境が休止状態になると、Cloud Manager に個別のステータスが表示されるようになりました。

* Cloud Managerビルドコンテナで、Java 8またはJava 11を使用したプロジェクトのコンパイルがサポートされるようになりました。 Java 11のサポートは、Mavenツールチェーンシステムによって提供されます。

* 環境ごとの環境変数の数が 200 に増えました。

* 概要ページの環境カードには、最大3環境のリストが表示されます。 「**すべてを表示**」ボタンを選択して環境の概要ページに移動し、環境の完全なリストを含む表を表示できます。
詳しくは、[環境](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)の表示を参照してください。

### バグ修正 {#bug-fixes-cloud-manager}

* 環境が完全に作成される前に、Cloud Manager から開発者コンソールへのリンクが正しくアクティブになっていませんでした。

* Cloud Manager から開発者コンソールへの直接リンクが、サンドボックスプログラムの環境を非休止／休止にするオプションを表示していませんでした。

* 非実稼働パイプライン編集ページの「キャンセル」ボタンと「保存」ボタンが必ずしも表示されていなかった問題を修正しました。

* コード品質プロセスで特定のエラーが発生すると、ログファイルが正しく生成されない場合があります。

* 新しいプログラムを作成する際に、推奨名が既存のプログラム名と重複する場合がありました。

* 一部の大規模なパイプラインステップログは、ユーザーインターフェイスから一貫性のある方法でダウンロードできませんでした。

* 環境名の検証が、1 つずれていました。

* 何も存在しない場合、環境ページにパブリッシュセグメントと Dispatcher セグメントが表示されることがありました。

## Adobe Experience Manager as a Cloud Service の基礎 {#cloud-service-foundation}

### ワークフロー {#workflows}

* ワークフロータイトル、ワークフローモデル、ステータス、イニシエーター、ペイロードパス、開始日に基づくワークフローインスタンスの検索のサポートが追加されました。 「[検索ワークフローインスタンス](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)」を参照してください。

## コンテンツ転送ツール {#content-transfer-tool}

この節では、新機能と[Content Transfer Tool](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)リリースv1.1.12の更新点について説明します。

### 新機能 {#what-is-new-ctt}

* ログのユーザーエクスペリエンスが向上しました。 タイムスタンプが抽出およびインジェストログに追加された。 ログが空かどうかを示すメッセージが追加されました。

### バグ修正 {#ctt-bug-fixes}

* 移行セットに、ファイル名が部分的に類似したパスが含まれている場合、コンテンツ転送ツールはコンテンツファイルをスキップしていました。 この問題は修正されました。
