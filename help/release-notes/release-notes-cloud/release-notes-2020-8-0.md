---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の 2020.8.0 リリースのリリースノート。'
description: '[!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 のリリースノート.'
translation-type: tm+mt
source-git-commit: cdd92032c627740c66de7b2f3836fa1dcd2ee2ca
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 100%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 のリリースノート {#release-notes}

Experience Manager as a Cloud Service 2020.8.0 の一般的なリリースノートの概要を次に説明します。


## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] の新機能 {#what-is-new-sites}

* [ページとサブページ（ページツリー）を以前のバージョンに戻す](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions)機能。

* AEM [SPA エディター](/help/implementing/developing/hybrid/introduction.md)で[ローンチを作成](/help/sites-cloud/authoring/launches/overview.md)する機能。


## [!DNL Adobe Experience Manager Assets] cloud serviceとして  {#assets}

### [!DNL Assets] の新機能 {#what-is-new-assets}

* アセットマイクロサービスでビデオのトランスコーディングがサポートされるようになりました。[!UICONTROL 処理プロファイル]設定の新しいセクションで、ビデオのビットレートとサイズを設定できます。出力形式は、H.264 コーデックを使用した MP4 です。詳しくは、[ビデオアセットの管理](/help/assets/manage-video-assets.md#transcode-video)を参照してください。その他のトランスコーディングオプションとビデオ配信については、[!DNL Dynamic Media] アドオンを使用してください。

* 新しい Adobe [!DNL Experience Manager Assets] デプロイメントでは、スマートタグ機能がデフォルトで設定されるようになりました。[!DNL Adobe Developer Console] と手動で統合する必要はありません。既存のデプロイメントでは、管理者が以前と同様に[スマートタグ統合の設定](/help/assets/smart-tags-configuration.md#aio-integration)をおこないます。

* 新しい[アセットダウンロードエクスペリエンス](/help/assets/download-assets-from-aem.md)には以下の特長があります。

   * 大規模なダウンロードの場合は非同期的にダウンロードするので、ユーザーは待つ必要がない。
   * 新しいモジュラー API を使用して開発者が機能を拡張できる。

* アセットマイクロサービスのメタデータ抽出のパフォーマンスが向上しました。アセット取り込みの全体的なスループットが向上しました。

* 処理プロファイルを使用して、Compute Service でカスタムメタデータを生成できます。詳しくは、[処理プロファイルを使用したカスタムメタデータ](/help/assets/manage-metadata.md#metadata-compute-service)を参照してください。

* 管理者が設定できる、Brand Portal ユーザー向けのよりシンプルなダウンロードエクスペリエンスが提供されます。詳しくは、[ダウンロードエクスペリエンスの概要](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations)を参照してください。

* ネイティブで高品質な PDF ドキュメントプレビューが Brand Portal で使用できるようになりました。詳しくは、[ドキュメントビューアの概要](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer)を参照してください。

* （[!DNL Dynamic Media Classic] を使用するのではなく）AEM の [!DNL Dynamic Media] から直接 CDN（コンテンツ配信ネットワーク）キャッシュを無効にできるようになりました。これにより、最新のアセットが数時間ではなく数分以内に提供されます。詳しくは、[Dynamic Media を使用した CDN キャッシュの無効化](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)を参照してください。

* [!DNL Assets] のユーザーインターフェイスコントロール、ナビゲーション、参照、検索の操作に、アクセシビリティのサポートが強化されました。

   * 「[!UICONTROL レンディションを追加]」オプションを選択した後に Esc キーを押すと、フォーカスがツールバーに戻ります。<!-- via CQ-4293594-->
   * 電子メールコンボボックスを使用している場合、キーボードフォーカスが期待どおりに機能します。<!-- via CQ-4286215 -->
   * 検索フィルターセクションのアコーディオン要素は、標準の拡大可能なアコーディオンとして解釈されます。<!-- via CQ-4273103 -->
   * タグをアセットに適用すると、タグがダイアログボックスにツリー要素として表示されます。ARIA 属性はツリー要素に適切に適用されて、アクセス可能になりました。<!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] 2.0.3 リリースがリリースされました。[!DNL Experience Manager] 6.5.5 サービスパックとの互換性が向上し、クライアント OS の互換性リストが更新されました。[!DNL Windows] 7 とバージョン 10.14 より前の [!DNL macOS] はサポートされていません。

### [!DNL Assets] で修正されたバグ {#bugs-fixed}

* 「関連付け」と「関連付けを解除」のオプションが、初めてクリックしたときに応答しない。（CQ-4299022）
* アセットをダウンロードする際に電子メールで受け取るオプションを選択した場合、電子メールが送信されない。（CQ-4299146）

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 製品コンソール機能が使用できるようになりました。これにより、AEM でマーケターや作成者が、コマースバックエンドに保存されているカテゴリや製品を表示したりナビゲートしたりできます。製品コンソールでカテゴリや製品のプロパティもサポートされるようになりました。

* 製品およびカテゴリピッカーが改善されて、マーケターが SKU で製品を選択したり、カテゴリ ID でカテゴリを選択したりできるようになりました。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

[!UICONTROL Cloud Manager] バージョン 2020.8.0 のリリース日は 2020 年 8 月 06 日です。

### 新機能 {#what-is-new-cloud-manager}

* コンテンツ監査は、Cloud Manager Sites 実稼動パイプラインで有効な機能です。Sites を使用するプログラムの実稼働パイプライン設定に、**コンテンツ監査**&#x200B;という名前の 3 番目のタブが含まれるようになりました。実稼働パイプラインを実行するたびに、パイプライン内のカスタム機能テストの後に新しいコンテンツ監査ステップが含まれるようになります。このステップでは、パフォーマンス、SEO（検索エンジン最適化）、アクセシビリティ、ベストプラクティス、PWA（プログレッシブ Web アプリ）などの多数のディメンションに照らしてサイトを評価します。


   >[!NOTE]
   >「コンテンツ監査」は、「エクスペリエンス監査」に名称が変更されました。

   詳しくは、[エクスペリエンス監査テスト](/help/implementing/cloud-manager/experience-audit-testing.md)を参照してください。

* Assets プログラムで新しく作成した環境が、スマートコンテンツサービスで自動的に設定されるようになりました。

* 休止状態の環境を Cloud Manager の&#x200B;**概要**&#x200B;ページで休止解除できます。

* Google Lighthouse を活用したエクスペリエンスチェックをページに対して実行できます。Cloud Manager パイプラインの一環として、最大 25 ページをエクスペリエンス KPI に照らしてチェックおよび検証でき、そのスコアが Cloud Manager UI に表示されます。

### バグ修正 {#bug-fixes-cm}

* 不要で望ましくない一部の SonarQube プラグインが、コード品質スキャンの一部として実行されていました。

* パイプラインの実行ページで、ブランチ名の形式が正しくありませんでした。

* 一部のケースで、パイプラインの実行完了が正常に記録されなかったため、パイプラインが新たに実行されないことがありました。

* 内部通信の問題が原因で、パイプラインの実行が&#x200B;*停止*&#x200B;することがあります。

* 新しい組織をプロビジョニングするときに、システム管理者以外の管理者ロールを持つ一部のユーザーに、Cloud Manager へのアクセス権が誤って付与されていました。

* 特定の条件下で、インデックス更新ジョブが複数回並行して開始された結果、デプロイメントエラーが発生していました。

* プログラムカードのツールチップの一貫性が適切に保てていませんでした。

* ユーザーインターフェイスで、削除中の環境に対して誤って操作を試行できていました。

* Cloud Manager の&#x200B;**概要**&#x200B;ページで、色が一致していませんでした。

### 既知の問題 {#known-issues-cm}

* コンテンツ監査平均スコアは、無効なページが含まれているので本来の値を下回っています。

* 「コンテンツ監査」タブに、パブリッシュドメインではなくオーサードメインを使用したベース URL が誤って表示されます。

* コンテンツ監査ステップをアクティブにするには、ユーザーがパイプラインを編集し、必要に応じてページを追加する必要があります。ページが追加されない場合は、ホームページが監査されます。

## コンテンツ転送ツール {#content-transfer-tool}

コンテンツ転送ツールリリース v1.0.4 の新機能と更新点については、このセクションを参照してください。

### 新機能 {#what-is-new-ctt}

* コンテンツ転送ツールで共有 S3 データストアがサポートされるようになりました。

### バグ修正 {#ctt-bug-fixes}

* ツールがアクションを完了するためのタイムアウトが追加されました。

* 旧バージョンの UI で、ログにエラーが示されているにもかかわらず、正常な抽出として表示されることがありました。

## コードリファクタリングツール {#code-refactoring-tools}

コードリファクタリングツールの新機能と更新点については、このセクションを参照してください。

### 新機能 {#what-is-new-refactoring}

* コードリファクタリングツールを統合するための AIO-CLI プラグインがリリースされ、開発者がコードリファクタリングツールを一元的に呼び出して実行できるようになりました。詳しくは、[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) を参照してください。

* AEM Dispatcher コンバーターが拡張されて、オンプレミス設定と Adobe Managed Services Dispatcher 設定を、AEM as a Cloud Service と互換性のある Dispatcher 設定に変換できるようになりました。詳しくは、[Git リソース：AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) を参照してください。

* AEM Dispatcher コンバーターが ` node.js ` で書き換えられ、AIO-CLI プラグインと統合されました。
