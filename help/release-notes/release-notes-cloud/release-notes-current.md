---
title: Cloud Serviceとしての [!DNL Adobe Experience Manager] の最新のリリースノートです。
description: Cloud Serviceとしての [!DNL Adobe Experience Manager] の最新のリリースノートです。
translation-type: tm+mt
source-git-commit: d115f5ce463257af54ae0ff48749df455b863dfd
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 9%

---


# [!DNL Adobe Experience Manager] as a Cloud Service のリリースノート {#release-notes}

次の節では、[!DNL Experience Manager]の一般的なリリースノートをCloud Serviceとしてまとめています。

## リリース日 {#release-date}

Cloud Service2020.11.0の[!DNL Adobe Experience Manager]のリリース日は2020年12月2日です。
次のリリース(2020.12.0)は、2020年12月18日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] の新機能 {#what-is-new-sites}

* **[階層管理](/help/sites-cloud/authoring/launches/managing-pages.md) &amp; [将来のタイムワープを起動](/help/sites-cloud/authoring/launches/preview.md)**:起動内にページを追加/削除する新しいUIと、Timewarpを使用してサイトを参照すると、起動からの将来の状態が表示されます。

* **[拡張コンテンツフラグメントモデルとエディタ](/help/assets/content-fragments/content-fragments-models.md)**:様々なデータタイプに対する入力検証の新しいオプション、新しいフォームのビジュアライゼーションでの定義済みリストデータタイプの改善、アセットUIにコンテンツフラグメントモデル名が表示され、検索可能になりました。

* **展開可能なライブコピーページを並べ替え**:[ [!UICONTROL 名前]]、[ [!UICONTROL 最終変更日]]、[ [!UICONTROL 最終ロールアウト日]の各] プロパティを使用して、ロールアウトに使用できるライブコピーページを並べ替える新しいオプションが追加されました。ページの[!UICONTROL 最後のロールアウト日]は、新しく導入されたプロパティです。

## [!DNL Adobe Experience Manager Assets] cloud serviceとして  {#assets}

### [!DNL Assets]と[!DNL Dynamic Media] {#what-is-new-assets}の新機能

* **一括アセット取り込み**:アセットマイクロサービスを含むCloud Serviceアーキテクチャ [!DNL Experience Manager] として活用する、拡張性の高いクラウドネイティブの取り込みサービスを提供します。主な使用例として、監視、レポート、スケジュール機能を使用した大規模な取り込みが挙げられます。また、一般的なクラウドアップロードツールを使用して、クラウドデータストアにアセットを初期的に転送できます。 [アセットバルクインジェスタツール](/help/assets/add-assets.md#asset-bulk-ingestor)を参照してください。
このツールは、システム管理者、コンサルタント、または導入パートナーの担当者を対象としています。 この機能により、大規模な取り込みが可能になり、初回の取り込み時や時折大量の取り込み時に使用するのが理想的です。 取り込みジョブを小さくするには、[[!DNL Experience Manager] デスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=ja)または[アセットユーザーインターフェイス](/help/assets/add-assets.md#upload-assets)を使用したアップロードを使用します。

   ![一括インポーターの設定](/help/assets/assets/bulk-import-config-low-res.png)

* カードと列の表示ーでデジタルアセットを並べ替えることができるようになりました。

   ![アセットの並べ替え](/help/assets/assets/asset-sort-options.png)

* このリリースでは、[!DNL Experience Manager Assets]のアクセシビリティに関する次の機能強化が行われました。 詳しくは、 [!DNL Assets]](/help/assets/accessibility.md)の[アクセシビリティ機能を参照してください。

   * キーボードを使用してタイムラインを移動する場合、Escキーを押すと、フォーカスを失わずに「すべて表示」オプションを折りたたむことができます。
   * キーボードのTabキーを使用して移動する場合、追加したタグから最後のタグを削除した後も、タグフィールドはフォーカスを保持します。
   * [!DNL Experience Manager] コンポーネントに、スクリーンリーダーで使用する名前、役割、値に適切な情報が含まれるようになりました。
   * 「種類/サイズ」コンボボックス、「リンク」コンボボックス、「言語」コンボボックス、または「テキスト」編集ボックスを削除すると、キーボードフォーカスは次または前のユーザーインターフェイス要素、またはより関連性の高いユーザーインターフェイス要素に戻ります。
   * オプションの上にポインターを置くと、選択やダウンロードなどのヒントが表示されます。 画面の虫めがねを使用している場合、これらのヒントが原因でファイルのサムネールが表示されないことがあります。 `Escape`キーを使用してオプションを削除した後に、フォーカスを保持できるようになりました。
   * ページ内にあるグリッドからグリッドセルを選択すると、フォーカスが画面に表示されるアクションバーに移動します。
   * ビジュアルユーザーは、[!DNL Experience Manager]ホームページ内のすべてのソリューションへのリンクに視覚的な手がかり（下線や山形のアイコン）が表示されるので、通常のテキストとリンクを区別できます。

* **Dynamic Mediaのバッチセットプリセット**:アセットファイルを個別にアップロードする場合や一括取り込みを使用する場合に、画像セットまたはスピンセット内の複数のアセットの作成と編成を自動化できるようになりました。

   詳しくは、[バッチセットプリセットについて](/help/assets/dynamic-media/batch-set-presets-dm.md)を参照してください。

* [!DNL Dynamic Media]では、次のアクセシビリティ機能が強化されました。

   * スクリーンリーダー（JAWS、ナレーター）は、埋め込みサイズメニューオプションのメニュー項目の名前、役割、状態をナレーションします。
   * ユーザーは`Tab`キーを使用して電子メールリンクダイアログを移動できます。
   * スクリーンリーダーの機能が強化されたので、ビデオエンコーディングプロファイルを作成するワークフローは、より使いやすくなりました。
   * `Tab`キーを使用してナビゲーションする場合、フォーカスはワークフロー内の適切なユーザーインターフェイス要素に移動し、インタラクティブビデオを作成します。
   * 発行ページ、アセットを編集ページ、スマートトリミングを編集ページ、および画像セットエディタページが、Web標準に準拠するように改善されました。 支援技術(AT)を使用すると、簡単にページ内を移動して、画像の切り抜きなどの操作を行うことができるようになりました。
   * ビューアが改善され、ユーザーがキーボードを使用してナビゲートできるようになりました。
   * キーボードおよびスクリーンリーダーのユーザーは切り抜き機能を使用できます。
   * キーボードユーザーは、ホットスポットをより適切に管理できます。

   [ [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md)のアクセシビリティを参照してください。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 最新のCIFコアコンポーネントバージョンv1.5.0を含むCIFベニアリファレンスサイト — 2020.11.05をリリースしました。詳細については、[CIFベニアリファレンスサイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27)を参照してください。

* CIF コアコンポーネント v1.5.0 をリリースしました。詳しくは、「[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0)」を参照してください。

### バグ修正 {#bug-fixes-commerce}

* Sling CAの設定で設定が直接指定されていないが、親の設定の1つで設定が指定されている場合、GraphQLクライアントの設定が正しく読み取られませんでした。 この問題は修正されました。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEMのCloud ManagerのCloud Service2020.12.0のリリース日は2020年12月10日です。

### [!DNL Cloud Manager] の新機能 {#what-is-new-cm}

* [SSL証明書](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)と[カスタムドメイン名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)のセルフサービス管理。

* [IP許可リスト](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)のセルフサービス管理。

* **環境**&#x200B;の詳細ページが更新され、環境上のカスタムドメイン名とIP許可リストを管理できるようになりました。

### バグ修正 {#bug-fixes-cloud-manager}

* 結果を提供せずに、コードスキャン段階でエラーが発生する場合があります。

* 環境カードに&#x200B;**追加**&#x200B;ボタンが一貫して表示されませんでした。

## Adobe Experience Manager as a Cloud Service の基礎 {#cloud-service-foundation}

### ワークフロー {#workflows}

* ワークフロータイトル、ワークフローモデル、ステータス、イニシエーター、ペイロードパス、開始日に基づくワークフローインスタンスの検索のサポートが追加されました。 「[検索ワークフローインスタンス](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)」を参照してください。

### 公開層ユーザーデータ同期{#user-sync}

* プロファイル属性やグループのメンバーシップを含むユーザーデータは、発行層に保持できます。 この機能の詳細については、[登録、ログイン、ユーザープロファイルドキュメント](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)を参照してください。

### SDKビルドアナライザー{#analyzers}

Cloud ServiceSDKビルドアナライザーMavenプラグインとしてのAEMは、Mavenプロジェクト内の問題（依存関係の欠落など）を検出します。 開発者は、ローカル開発中に問題を発見し、Cloud Managerを使用してCloud環境に展開する前に、問題を発見できます。 詳しくは、[ここ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)と[ここ](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk)のドキュメントを参照してください。

### その他 {#others-foundation}

新しい[&quot;httpd -t&quot;構文](/help/implementing/dispatcher/disp-overview.md#local-validation)は、Cloud Managerのビルド中に実行されるApache設定とディスパッチャー設定を確認します。これは、AEMをCloud ServiceSDKのDispatcher Toolsとして使用して実行することもできます。

## コードリファクタリングツール {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] の新機能 {#what-is-new-crt}

* AIO-CLIプラグインの新しいバージョンがリリースされました。 このプラグインの最新バージョンには、AEM Dispatcher ConverterとRepository Modenizerのバグ修正が含まれ、新しいユーティリティIndex Converterもサポートされています。
このプラグインの詳細については、[統合エクスペリエンス](/help/move-to-cloud-service/unified-experience.md)を参照してください。

* [Index ](/help/move-to-cloud-service/refactoring-tools/index-converter.md) Converterは、顧客のCustom OAK Index Definitionsを、Cloud Service互換のOAK Index DefinitionsとしてAEMに変換するために使用できるユーティリティです。詳しくは、[Index Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)を参照してください。

* [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)に追加された新機能。すべてのOSGi設定を含む個別のパッケージ`ui.config`を作成します。

### バグ修正 {#crt-bug-fixes}

* AEM Dispatcher ConverterおよびRepository Modenizerツールで行われたいくつかのバグ修正。
[AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)と[Repository Modenizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)を参照してください。