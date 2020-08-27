---
title: Cloud Serviceの2020.8.0リリース [!DNL Adobe Experience Manager] のリリースノート。
description: '[!DNLAdobe Experience Manager] 2020.8.0のCloud Serviceリリースノートとして。'
translation-type: tm+mt
source-git-commit: b47b4d0c84e814a43ca14c2efd4f553694ab6c2b
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 12%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

Experience Manager as a Cloud Service 2020.8.0 の一般的なリリースノートの概要を次に説明します。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* ページとサブページ（ページツリー）を以前のバージョンに復元する機能。

* AEM SPAエディターで起動を作成する機能。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* アセットマイクロサービスでビデオトランスコードがサポートされるようになりました。ビデオのビットレートとサイズの設定をサポートする [!UICONTROL 処理プロファイル] 画面の新しい「ビデオ」セクションが追加されました（出力形式はH.264コーデックのMP4です）。 For details, see [manage video assets](/help/assets/manage-video-assets.md#transcode-video). より多くのトランスコードオプションとビデオ配信 [!DNL Dynamic Media] アドオンを使用できます。

* 新しい [!DNL Experience Manager Assets] デプロイメントでは、スマートタグ機能がデフォルトで設定されるようになりました。 と手動で統合する必要はありま [!DNL Adobe Developer Console]せん。 既存のデプロイメントでは、管理者は以前と同様にスマートタグ統合 [](/help/assets/smart-tags-configuration.md#aio-integration) を設定します。

* 新しい [アセットのダウンロードエクスペリエンス](/help/assets/download-assets-from-aem.md) :

   * 大規模なダウンロードの場合は非同期的にダウンロードするので、ユーザーが待つ必要がありません。

   * 開発者向けの拡張機能用の新しいモジュラーAPI。

* [!DNL Experience Manager] は、アセットマイクロサービスのメタデータ抽出のパフォーマンスを改善しました。 アセット取り込みの全体的なスループットが向上します。

* 処理プロファイルを使用して、Compute Serviceを使用してカスタムメタデータを生成します。 詳しくは、処理プロファイルを使用した [カスタムメタデータを参照してください](/help/assets/manage-metadata.md#metadata-compute-service)

* 管理者が設定できる、Brand Portalユーザー向けのよりシンプルなダウンロード操作です。 「 [ダウンロードエクスペリエンスの概要](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations)」を参照してください。

* ネイティブおよび高品質のPDFドキュメントプレビューがBrand Portalで使用できるようになりました。 「 [ドキュメントビューアの概要](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer)」を参照してください。

* キャッシュを無効にするユーザーインターフェイスが、で使用できるようになり [!DNL Dynamic Media]ました。

* のユーザーインターフェイスコントロール、ナビゲーション、参照、および検索の操作に、アクセシビリティのサポートが強化され [!DNL Assets]ました。

   * 「 [!UICONTROL 追加レンディション] 」オプションを選択した後にEscキーを押すと、フォーカスがツールバーに戻ります。 <!-- via CQ-4293594-->
   * 電子メールコンボボックスを使用する場合、キーボードフォーカスが期待どおりに機能します。 <!-- via CQ-4286215 -->
   * 検索フィルターセクションのアコーディオン要素は、標準の拡大可能なアコーディオンとして解釈されます。 <!-- via CQ-4273103 -->
   * タグをアセットに適用すると、タグがツリー要素として表示されます。 ARIA属性は、ツリー要素に適用され、現在アクセス可能になっています。 <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] 2.0.3リリースがリリースされ、6.5.5との互換性が向上しました。 [!DNL AEM] クライアントOSの互換性リスト [!DNL Service Pack] の更新(10.14より前の7バージョンおよび [!DNL Windows] 7バー [!DNL MacOS] ジョンを削除)を行います。

### 修正されたバグ [!DNL Assets] {#bugs-fixed}

* 関連付けと非関連付けのオプションを初めてクリックした場合に応答しない。 （CQ-4299022）
* アセットをダウンロードする際に、電子メールで受信するオプションを選択した場合、電子メールは送信されません。 （CQ-4299146）

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 製品コンソール機能が使用できるようになりました。 これにより、AEMのマーケターや作成者は、コマースバックエンドに保存されているカテゴリや製品を表示してナビゲートできます。 製品コンソールでのカテゴリおよび製品のプロパティのサポートも提供されました。

* 製品とカテゴリの選択機能が強化され、マーケティング担当者はSKUを使用して製品を選択したり、カテゴリIDを使用してカテゴリを選択したりできるようになりました。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

[!UICONTROL Cloud Manager] バージョン 2020.8.0 のリリース日は 2020 年 8 月 06 日です。

### 新機能 {#what-is-new-cloud-manager}

* 「コンテンツ監査」は、Cloud Managerサイト実稼働パイプラインで有効になる機能です。 Sitesを使用するプログラムの実稼働パイプライン設定に、「 **Content Audit**」という名前の3番目のタブが含まれるようになりました。 実稼働パイプラインを実行するたびに、カスタム機能テストの後、新しいContent Auditステップがパイプラインに含まれます。このステップは、パフォーマンス、SEO(Search Engine Optimization)、アクセシビリティ、ベストプラクティス、PWA(Progressive Web App)など、多数の次元に対してサイトを評価します。

   Refer to [Content Audit Testing](/help/implementing/cloud-manager/content-audit-testing.md) for more details.

* アセットプログラムーで新しく作成した環境が、Smart Content Servicesで自動的に設定されるようになりました。

* 休止状態の環境は、Cloud Managerの **概要** ページで非冬眠にできます。

* Google Lighthouseによるページに対してエクスペリエンスチェックを実行する機能。 Cloud Managerのパイプラインの一部として、エクスペリエンスKPIに対して最大25のページをチェックして検証でき、スコアがCloud Manager UIに表示されます。

### バグ修正 {#bug-fixes-cm}

* 不要で望ましくない一部の SonarQube プラグインが、コード品質スキャンの一部として実行されていました。

* パイプラインの実行ページで、ブランチ名の形式が正しくありませんでした。

* 一部のケースで、パイプラインの実行完了が正常に記録されなかったため、パイプラインが新たに実行されないことがありました。

* 内部通信の問題が原因で、パイプラインの実行が&#x200B;*停止*&#x200B;することがあります。

* 新しい組織をプロビジョニングすると、システム管理者以外の管理者ロールを持つ一部のユーザーに、誤ってCloud Managerへのアクセス権が与えられました。

* 特定の条件下で、更新インデックスジョブが複数回並行して開始され、展開エラーが発生しました。

* プログラムカードのツールチップの一貫性が適切に保てていませんでした。

* ユーザーインターフェイスで、削除中に環境に対して操作を試行することが誤って許可されました。

* There was a color mismatch on the Cloud Manager&#39;s **Overview** page.

### 既知の問題 {#known-issues-cm}

* 無効なページは、コンテンツ監査平均スコアが本来の値を下回る場合に含まれます。

* 「コンテンツ監査」タブに、発行ドメインではなく作成者ドメインを使用したベースURLが正しく表示されません。

* コンテンツ監査手順をアクティブにするには、ユーザーはパイプラインを編集し、必要に応じてページを追加する必要があります。 ページが追加されない場合、ホームページは監査されます。

## コンテンツ転送ツール {#content-transfer-tool}

このセクションでは、新機能とコンテンツ転送ツールリリースv1.0.4の更新点について説明します。

### 新機能 {#what-is-new-ctt}

* コンテンツ転送ツールで共有S3 DataStoreがサポートされるようになりました。

### バグ修正 {#ctt-bug-fixes}

* アクションを完了するための追加のタイムアウトが追加されました。

* 以前のバージョンのUIで、ログにエラーが表示されていたにもかかわらず、正常に抽出されたことがありました。

## コードリファクタリングツール {#code-refactoring-tools}

この節では、コードリファクタリングツールの新機能と更新点について説明します。

### 新機能 {#what-is-new-refactoring}

* AIO-CLIプラグインは、コードリファクタリングツールの統合を目的としてリリースされ、開発者がコードリファクタリングツールを1か所から呼び出して実行できるようになりました。 Refer to [Git Resource: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) for more details.

* AEM Dispatcher Converterが拡張され、オンプレミス設定とAdobe Managed Services Dispatcher設定の、Cloud Service互換のディスパッチャー設定としてのAEMへの変換がサポートされるようになりました。 詳しくは、 [Gitリソースを参照してください。AEMCloud Serviceディスパッチャーコンバーター](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) （英語）を参照してください。

* AEM Dispatcher Converterは、AIO-CLIプラグインに再書き込み ` node.js ` され、統合されています。
