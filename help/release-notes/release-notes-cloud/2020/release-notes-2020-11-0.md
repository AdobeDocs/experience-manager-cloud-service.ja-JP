---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.11.0 リリースのリリースノート。'
description: "[!DNL Adobe Experience Manager] as a Cloud Service 2020.11.0 のリリースノート。"
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 91%

---

# [!DNL Adobe Experience Manager] as a Cloud Service のリリースノート {#release-notes}

[!DNL Experience Manager] as a Cloud Service の一般的なリリースノートの概要を次に説明します。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2020.11.0 のリリース日は 2020 年 12 月 2 日です。次回のリリース（2020.12.0）は、2020 年 12 月 17 日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] の新機能  {#what-is-new-sites}

* **[ローンチ階層管理](/help/sites-cloud/authoring/launches/managing-pages.md)と[将来へのタイムワープ](/help/sites-cloud/authoring/launches/preview.md)**：ローンチ内でページを追加／削除するための新しい UI が追加されました。また、タイムワープを使用してサイトを参照すると、ローンチからの将来の状態が表示されるようになりました。

* **[拡張コンテンツフラグメントモデルおよびエディター](/help/assets/content-fragments/content-fragments-models.md)**：様々なデータタイプの入力検証の新しいオプションが追加され、新しいフォーム視覚化で定義済みリストデータタイプが改善されました。また、Assets UI でコンテンツフラグメントモデル名が表示され検索可能になりました。

* **ロールアウトに使用可能なライブコピーページの並べ替え**：ロールアウトに使用できるライブコピーページを、[!UICONTROL 名前]、[!UICONTROL 最終変更日]、[!UICONTROL 前回のロールアウト日]の各プロパティを使用して並べ替える新しいオプションが追加されました。ページの[!UICONTROL 前回のロールアウト日]は、新しく導入されたプロパティです。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### [!DNL Assets] と [!DNL Dynamic Media] の新機能  {#what-is-new-assets}

* **一括アセット取り込み**：アセットマイクロサービスなどのas a Cloud Serviceのアーキテクチャを使用する、スケーラブルでクラウドネイティブ [!DNL Experience Manager] 取り込みサービスを顧客に提供します。 主な使用例としては、監視、レポート、スケジュール機能を備えた大規模な取り込みや、クラウドデータストアへの初回のアセット転送を一般的なクラウドアップロードツールで行えることなどが挙げられます。詳しくは、[アセット一括取り込みツール](/help/assets/add-assets.md#asset-bulk-ingestor)の説明を参照してください。


  このツールは、システム管理者、コンサルタント、実装パートナーのいずれかのペルソナを対象としています。この機能により、大規模な取り込みが可能になります。これは、初回の取り込み時や大量の取り込みを行うときに使用するのが理想的です。より小規模な取り込みジョブの場合は、[Assets ユーザーインターフェイスを使用したアップロード](/help/assets/add-assets.md#upload-assets)または[[!DNL Experience Manager] デスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=ja)を使用します。

  ![一括読み込みの設定](/help/assets/assets/bulk-import-config-low-res.png)

* デジタルアセットをカード表示と列表示で並べ替えることができるようになりました。

  ![アセットの並べ替え](/help/assets/assets/asset-sort-options.png)

* このリリースでは、[!DNL Experience Manager Assets] のアクセシビリティに関する次の機能強化が行われています。詳しくは、[ [!DNL Assets]](/help/assets/accessibility.md) のアクセシビリティ機能を参照してください。

   * キーボードを使用してタイムラインのナビゲーションを行う場合、Esc キーを押すと、フォーカスを失わずに「すべて表示」オプションを折りたたむことができます。
   * キーボードの Tab キーを使用してナビゲーションを行う場合、追加したタグから最後のタグを削除した後も、フォーカスはそのタグフィールドにとどまります。
   * スクリーンリーダーで使用される名前、役割、値の適切な情報が [!DNL Experience Manager] コンポーネントに含まれるようになりました。
   * 「種類 / サイズ」コンボボックス、「リンク」コンボボックス、「言語」コンボボックス、または「テキスト」編集ボックスを削除すると、キーボードフォーカスは次または前のユーザーインターフェイス要素、またはより関連性の高いユーザーインターフェイス要素に戻ります。
   * オプションの上にポインターを置くと、「選択」や「ダウンロード」などのヒントが表示されます。拡大鏡を使用している場合は、これらのヒントが原因でファイルのサムネールが表示されないことがあります。`Escape` キーを使用してオプションを削除した後に、フォーカスを保持できるようになりました。
   * ページ内にあるグリッドからグリッドセルを選択すると、画面に表示されるアクションバーにフォーカスが移動します。
   * [!DNL Experience Manager] ホームページですべてのソリューションへのリンクに視覚的な手がかり（下線や山形アイコン）が表示されるので、ユーザーは通常のテキストとリンクを区別できます。

* **Dynamic Media のバッチセットプリセット**：アセットファイルを個別にアップロードする場合や一括取り込みを使用してアップロードする場合に、複数のアセットを画像セットまたはスピンセットとして自動的に作成および編成できるようになりました。

  詳しくは、[バッチセットプリセットについて](/help/assets/dynamic-media/batch-set-presets-dm.md)を参照してください。

* [!DNL Dynamic Media] では、アクセシビリティが次のように強化されました。

   * 「埋め込みサイズ」メニューオプションのメニュー項目の名前、役割、状態がスクリーンリーダー（JAWS、ナレーター）で読み上げられます。
   * ユーザーは `Tab` キーを使用してメールリンクダイアログ内を移動できます。
   * スクリーンリーダーの機能が強化されたので、ビデオエンコーディングプロファイルを作成するワークフローが、より使いやすくなりました。
   * インタラクティブビデオを作成するワークフローで `Tab` キーを使用してナビゲートする場合、フォーカスは適切なユーザーインターフェイス要素に移動します。
   * 公開、アセットを編集、スマート切り抜きを編集、画像セットエディターの各ページが、Web 標準に準拠するように改善されました。支援テクノロジー（AT）を使用すると、これらのページを簡単に移動し、画像の切り抜きなどの操作を行えるようになりました。
   * ビューアが改善され、ユーザーがキーボードを使用してナビゲートできるようになりました。
   * キーボードおよびスクリーンリーダーのユーザーは切り抜き機能を使用できます。
   * キーボードユーザーによるホットスポットの管理が向上しました。

  詳しくは、[ [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md)のアクセシビリティを参照してください。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 最新のCIF コアコンポーネント v1.5.0 を含んだCIF Venia 参照サイト 2020.11.05 をリリースしました。詳しくは、[CIF Venia 参照サイト ](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27) を参照してください。

* CIF コアコンポーネント v1.5.0 をリリースしました。詳しくは、[CIF コアコンポーネント ](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) を参照してください。

### バグの修正 {#bug-fixes-commerce}

* Sling CA の設定で直接指定されておらず、親の設定の 1 つで指定されている場合、GraphQL クライアントの設定が正しく読み取られませんでした。この問題が修正されました。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEM as a Cloud Service 2020.11.0 の Cloud Manager のリリース日は 2020 年 11 月 12 日です。

### [!DNL Cloud Manager] の新機能  {#what-is-new-cm}

* **環境**&#x200B;カードおよび&#x200B;**環境**&#x200B;概要ページの環境メニューオプションから、新しいメニューオプション「**ローカルログイン**」が利用できるようになりました。詳しくは、[環境の管理](/help/implementing/cloud-manager/manage-environments.md#login-locally)を参照してください。

* Cloud Manager の「**学習**」タブが更新され、UI に新しい画像が追加されました。

### バグの修正 {#bug-fixes-cloud-manager}

* ビルドの実行に先立って行われる依存関係の読み込みには、Maven プラグインのダウンロードが必要でした。
* 言語を選択するための Cloud Manager フッターからのリンクが、正しい場所を指すようになりました。
* コードスキャン時に SonarQube プロセスが起動しないことがあります。これが自動検出され、再起動が試行されるようになりました。
* 既存のすべての実稼動パイプラインは、エクスペリエンス監査の手順で自動的に有効になります。

## Adobe Experience Manager as a Cloud Service の基盤 {#cloud-service-foundation}

### ワークフロー {#workflows}

* ワークフロータイトル、ワークフローモデル、ステータス、イニシエーター、ペイロードパス、開始日に基づいてワークフローインスタンスを検索できるようになりました。詳しくは、[ワークフローインスタンスの検索](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html?lang=ja)を参照してください。

### パブリッシュ層のユーザーデータ同期 {#user-sync}

* プロファイル属性やグループメンバーシップなどのユーザーデータをパブリッシュ層で保持できます。この機能について詳しくは、[登録、ログイン、ユーザープロファイル](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)を参照してください。

### SDK ビルドアナライザー {#analyzers}

AEM as a Cloud Service の SDK ビルドアナライザー Maven プラグインでは、依存関係の欠落など、Maven プロジェクトの問題を検出します。これを使用すると、ローカル開発中に、Cloud Manager でクラウド環境にデプロイする前に開発者が問題を見つけることができます。詳しくは、[こちら](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=ja#developing)や[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=ja#building-for-the-sdk)のドキュメントを参照してください。

### その他 {#others-foundation}

新しい [ 「httpd -t」構文 ](/help/implementing/dispatcher/disp-overview.md#local-validation)Cloud Managerのビルド時に実行される Apache および Dispatcher 設定の確認。これを、AEM as a Cloud Service SDK のDispatcher Tools を使用して実行することもできます。

## コンテンツ転送ツール {#content-transfer-tool}

この節では、[コンテンツ転送ツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=ja)リリース v1.1.12 の新機能と更新点について説明します。

### 新機能 {#what-is-new-ctt}

* ログのユーザーエクスペリエンスが向上しました。抽出ログと取り込みログにタイムスタンプが追加されました。ログが空かどうかを知らせるメッセージが追加されました。

### バグの修正 {#ctt-bug-fixes}

* 移行セットに含まれているパスのファイル名が部分的に似ている場合、コンテンツ転送ツールがコンテンツファイルをスキップしていました。この問題が修正されました。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザーのリリース日は 2020 年 11 月 13 日です。

### [!DNL Best Practices Analyzer] の新機能  {#what-is-new-bpa}

* Cloud Readiness Analyzer は、ベストプラクティスアナライザー（BPA）になりました。BPA は、現在の AEM 実装のベストプラクティス評価を提供し、既存の AEM インスタンスから AEM as a Cloud Service への移行の準備状況を評価するのに役立ちます。

* `java.io.InputStream` の使用を検出するための新しい機能が追加されましたが、これを AEM as a Cloud Service で使用すると問題が発生する可能性があります。

### バグの修正 {#bpa-bug-fixes}

* *テキストフィールド*&#x200B;基盤コンポーネントに関連する問題の原因となるバグが修正されました。
