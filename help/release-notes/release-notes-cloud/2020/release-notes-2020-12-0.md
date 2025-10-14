---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 リリースのリリースノート。'
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
feature: Release Information
role: Admin
source-git-commit: 64344b9b2cce8d7c7f05d3e5ba94049346308a9d
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 47%

---

# [!DNL Adobe Experience Manager] as a Cloud Service のリリースノート  {#release-notes}

[!DNL Experience Manager] as a Cloud Service の一般的なリリースノートの概要を次に説明します。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 のリリース日は 2020 年 12 月 17 日です。次回のリリース（2021.1.0）は 2021 年 1 月 28 日（PT）です。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[コンテンツフラグメント HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**：HTTP API を使用して、コンテンツフラグメントのバリエーションを追加、更新、削除する機能を追加します。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Adobe InDesign Server] との統合が [!DNL Cloud Service] as a [!DNL Experience Manager] で利用できるようになりました。[!DNL Adobe InDesign Server] スクリプティングを使用して [!DNL Adobe InDesign] ファイルを処理する自動化機能を提供し、[!DNL Assets] テンプレートユーザーインターフェイスを使用してパンフレットや広告を作成できます。[!DNL Adobe Managed Services] でホストされる [!DNL InDesign Server] のみが [!DNL Experience Manager as a Cloud Service] に対してサポートされます。<!-- TBD: Add link to article. -->

* [!DNL Experience Manager] は、Connected Assets 機能を使用したリモート [!DNL Experience Manager Sites] デプロイメントでアセットが使用された場合に、アセット参照を追跡および表示するように拡張されました。アセットの [!UICONTROL &#x200B; プロパティ &#x200B;] ページに新しい [!UICONTROL &#x200B; 参照 &#x200B;] タブに、アセットのローカル参照とリモート参照がリストされるようになりました。 この参照により、DAM ユーザーは [!DNL Sites] ページ内および [!DNL Assets] 内の複合アセット内のアセットの使用状況を追跡できます。「[Connected Assets の設定と使用](/help/assets/use-assets-across-connected-assets-instances.md)」を参照してください。

* [!DNL Dynamic Media] の機能に、AEM [!DNL Sites] 画像ベースのコアコンポーネントからアクセスできるようになりました。 作成者は、Web ページの作成時に画像プリセット、スマート切り抜き、画像修飾子を使用するように、コンポーネントをすばやく設定できます。[コアコンポーネント 2.13.0 リリース](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0)を参照してください。

* [!DNL Experience Manager] デスクトップアプリケーションを使用すると、デスクトップアプリケーションインターフェイス上の Windows エクスプローラーまたはMac Finder からファイルをドラッグして、ファイルやフォルダーをアップロードできます。 [&#x200B; デスクトップアプリケーションを使用したアセットの追加 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-desktop-app/using/using#upload-and-add-new-assets-to-aem) を参照してください。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 最新のCIF コアコンポーネント v1.6.0 を含んだCIF Venia 参照サイト 2020.12.01 をリリースしました。詳しくは、[CIF Venia 参照サイト &#x200B;](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) を参照してください。

* CIF コアコンポーネント v1.6.0 をリリースしました。詳しくは、[CIF コアコンポーネント &#x200B;](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) を参照してください。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

Adobe Experience Manager（AEM as a Cloud Service）のCloud Manager 2020.12.0 のリリース日は 2020 年 12 月 10 日（PT）です。

### [!DNL Cloud Manager] の新機能 {#what-is-new-cm}

* [SSL 証明書 &#x200B;](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) のセルフサービス管理および [&#x200B; カスタムドメイン名の概要 &#x200B;](/help/implementing/cloud-manager/custom-domain-names/introduction.md)。

* [IP 許可リスト](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)のセルフサービス管理。

* 更新された **環境** の詳細ページで、環境のカスタムドメイン名と IP許可リストを管理できるようになりました。

### バグ修正 {#bug-fixes-cloud-manager}

* 結果が提供されずにコードスキャン段階で発生する場合があったエラーに対処します。

* 環境カードに「**追加**」ボタンが一貫して表示されていませんでした。

## コードリファクタリングツール {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] の新機能  {#what-is-new-crt}

* AIO-CLI プラグインの新しいバージョンがリリースされました。このプラグインの最新バージョンは、AEM Dispatcher コンバーターと Repository Modernizer のバグ修正を含んでいるほか、新しいユーティリティであるインデックスコンバーターもサポートしています。 このプラグインの詳細については、[&#x200B; 統合エクスペリエンス &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience#benefits) を参照してください。

* インデックスコンバーターは、顧客のカスタム Oak インデックス定義をAEM as a Cloud Service互換のOak インデックス定義に変換するために使用できるユーティリティです。 詳しくは、[&#x200B; インデックスコンバーター &#x200B;](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) を参照してください。

* [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) にすべての OSGi 設定を含む個別のパッケージ `ui.config` を作成する新機能が追加されました。

### バグの修正 {#crt-bug-fixes}

* AEM Dispatcher Converter および Repository Modernizer ツールで、いくつかのバグが修正されました。 [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) および [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) を参照してください。

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.1.20 のリリース日は 2021 年 1 月 8 日です。

### [!DNL Content Transfer Tool] の新機能  {#what-is-new-ctt}

* コンテンツ転送ツール（CTT）ユーザーインターフェイスのステータスアイコンにマウスポインターを置くと、アクセストークンの有効期限が切れたかどうかを確認できます。また、Cloud Serviceセットの詳細 UI で、移行インスタンスに接続できないことも通知されます。

### バグ修正 {#ctt-bug-fixes}

* 移行セットの CTT（Content Transfer Tool）ユーザーインターフェイスのステータスが持続せず、非アクティブな期間が続いたた後に変更されていました。この問題は修正されました。
* ログが利用できない場合は、ログを表示するオプションは無効になっています。 この問題が修正され、ログが見つからない理由をユーザーに通知するメッセージが追加されました。
* ユーザーが取り込みを停止すると、コンテンツ転送ツールのユーザーインターフェイスのステータスが *失敗* と表示されました。 この問題は、代わりに *停止* と表示されるように修正されました。
