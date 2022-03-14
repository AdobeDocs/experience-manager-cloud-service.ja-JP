---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 リリースのリリースノート。'
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
source-git-commit: aeee895e4a4b959125d08091619988d0ffa09ace
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service のリリースノート  {#release-notes}

[!DNL Experience Manager] as a Cloud Service の一般的なリリースノートの概要を次に説明します。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 のリリース日は 2020 年 12 月 17 日です。次回のリリース（2021.1.0）は、2021 年 1 月 28 日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[コンテンツフラグメント HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**：HTTP API を使用して、コンテンツフラグメントのバリエーションを追加、更新、削除する機能を追加します。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Adobe InDesign Server] との統合が [!DNL Cloud Service] as a [!DNL Experience Manager] で利用できるようになりました。[!DNL Adobe InDesign Server] スクリプティングを使用して [!DNL Adobe InDesign] ファイルを処理する自動化機能を提供し、[!DNL Assets] テンプレートユーザーインターフェイスを使用してパンフレットや広告を作成できます。[!DNL Adobe Managed Services] でホストされる [!DNL InDesign Server] のみが [!DNL Experience Manager as a Cloud Service] に対してサポートされます。<!-- TBD: Add link to article. -->

* [!DNL Experience Manager] は、Connected Assets 機能を使用したリモート [!DNL Experience Manager Sites] デプロイメントでアセットが使用された場合に、アセット参照を追跡および表示するように拡張されました。アセットの[!UICONTROL プロパティ]ページに新しい「[!UICONTROL 参照]」タブが追加され、アセットのローカル参照とリモート参照がリストされるようになりました。この参照により、DAM ユーザーは [!DNL Sites] ページ内および [!DNL Assets] 内の複合アセット内のアセットの使用状況を追跡できます。「[Connected Assets の設定と使用](/help/assets/use-assets-across-connected-assets-instances.md)」を参照してください。

* [!DNL Dynamic Media] の機能は、 [!DNL Sites] 画像ベースのコアコンポーネントを介してアクセスできるようになりました。作成者は、Web ページの作成時に画像プリセット、スマート切り抜き、画像修飾子を使用するように、コンポーネントをすばやく設定できます。[コアコンポーネント 2.13.0 リリース](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0)を参照してください。

* [!DNL Experience Manager] デスクトップアプリケーションでは、インターフェイス上の Windows エクスプローラーまたは Mac Finder からファイルをドラッグすることで、ファイルやフォルダーをアップロードできます。詳しくは、「[デスクトップアプリケーションを使用したアセットの追加](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja#upload-and-add-new-assets-to-aem)」を参照してください。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 最新の CIF コアコンポーネント v1.6.0 を含んだ CIF Venia 参照サイト 2020.12.01 をリリースしました。詳しくは、[CIF Venia 参照サイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01)を参照してください。

* CIF コアコンポーネント v1.6.0 をリリースしました。詳しくは、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0)を参照してください。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEM as a Cloud Service 2020.12.0 Cloud Manager のリリース日は 2020 年 12 月 10 日です。

### [!DNL Cloud Manager] の新機能  {#what-is-new-cm}

* [SSL 証明書](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)と[カスタムドメイン名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)のセルフサービス管理。

* [IP 許可リスト](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)のセルフサービス管理。

* **環境**&#x200B;の詳細ページが更新され、環境のカスタムドメイン名と IP 許可リストを管理できるようになりました。

### バグ修正 {#bug-fixes-cloud-manager}

* 結果を提供せずに、コードスキャン段階で発生する場合があった障害に対処しました。

* 環境カードに「**追加**」ボタンが一貫して表示されませんでした。

## コードリファクタリングツール {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] の新機能  {#what-is-new-crt}

* AIO-CLI プラグインの新しいバージョンがリリースされました。このプラグインの最新バージョンには、AEM Dispatcher コンバーターと Repository Modenizer のバグ修正が含まれ、新しいユーティリティインデックスコンバーターもサポートされています。このプラグインの詳細については、[Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=ja#benefits) を参照してください。

* インデックスコンバーターは、顧客のカスタム OAK インデックス定義を AEM as a Cloud Service 互換の OAK インデックス定義に変換するために使用できるユーティリティです。詳しくは、[インデックスコンバーター](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)を参照してください。

* [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) にすべての OSGi 設定を含む個別のパッケージ `ui.config` を作成する新機能が追加されました。

### バグ修正 {#crt-bug-fixes}

* AEM Dispatcher コンバーターおよび Repository Modenizer ツールでいくつかのバグ修正が行われました。[AEM Dispatcher コンバーター](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)および [Repository Modenizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) を参照してください。

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.1.20 のリリース日は 2021 年 1 月 8 日です。

### [!DNL Content Transfer Tool] の新機能  {#what-is-new-ctt}

* コンテンツ転送ツール（CTT）ユーザーインターフェイスのステータスアイコンにマウスポインターを置くと、アクセストークンの有効期限が切れたかどうかを確認できます。また、移行セットの詳細 UI で、Cloud Service インスタンスに接続できないことが通知されます。

### バグ修正 {#ctt-bug-fixes}

* 移行セットの CTT（Content Transfer Tool）ユーザーインターフェイスのステータスが持続せず、非アクティブな期間が続いたた後に変更されていました。この問題が修正されました。
* ログが利用できない場合、ログを表示するオプションが無効になっていました。この問題は修正され、ログが見つからない理由をユーザーに通知するメッセージが追加されました。
* コンテンツ転送ツールのユーザーインターフェイスのステータスが、ユーザーが取得を停止したときに、*FAILED* になっていました。この問題は修正され、代わりに *STOPPED* が表示されるようになりました。
