---
title: Cloud Serviceとしての [!DNL Adobe Experience Manager] の最新のリリースノートです。
description: Cloud Serviceとしての [!DNL Adobe Experience Manager] の最新のリリースノートです。
translation-type: tm+mt
source-git-commit: 6b001ffb9afe73c09d131ef7901cc2c12c57f164
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 19%

---


# [!DNL Adobe Experience Manager] as a Cloud Service のリリースノート {#release-notes}

次の節では、[!DNL Experience Manager]の一般的なリリースノートをCloud Serviceとしてまとめています。

## リリース日 {#release-date}

Cloud Service2020.12.0の[!DNL Adobe Experience Manager]のリリース日は2020年12月17日です。
次のリリース(2021.1.0)は、2020年1月28日にリリースされます。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[コンテンツフラグメントHTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**:HTTP 追加 APIを使用して、コンテンツフラグメントのバリエーションを追加/更新および削除する機能。

## [!DNL Adobe Experience Manager Assets] として  [!DNL Cloud Service] {#assets}

* [!DNL Adobe InDesign Server]との統合が[!DNL Cloud Service]として[!DNL Experience Manager]で利用できるようになりました。 [!DNL Adobe InDesign Server]スクリプティングを使用して[!DNL Adobe InDesign]ファイルを処理する自動化機能を提供し、[!DNL Assets]テンプレートユーザーインターフェイスを使用してパンフレットや広告を作成できます。 [!DNL Adobe Managed Services]でホストされる[!DNL InDesign Server]のみ[!DNL Experience Manager as a Cloud Service]に対してサポートされます。<!-- TBD: Add link to article. -->

* [!DNL Experience Manager] は、接続されたアセット機能を使用したリモート [!DNL Experience Manager Sites] デプロイメントでアセットが使用された場合に、アセット参照を追跡および表示するように拡張されました。アセットの[!UICONTROL プロパティ]ページに新しい[!UICONTROL 参照]タブが追加され、アセットのローカル参照とリモート参照がリストされるようになりました。 この参照により、DAMユーザーは[!DNL Sites]ページ内および[!DNL Assets]内の複合アセット内のアセットの使用状況を追跡できます。 [接続されたアセットの設定と使用](/help/assets/use-assets-across-connected-assets-instances.md)を参照してください。

* [!DNL Dynamic Media] の機能は、 [!DNL Sites] 画像ベースのコアコンポーネントを介してアクセスできるようになりました。作成者は、Webページの作成時に画像プリセット、スマート切り抜き、画像修飾子を使用するように、コンポーネントをすばやく設定できます。 [コアコンポーネント2.13.0リリース](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0)を参照してください。

* [!DNL Experience Manager] デスクトップアプリを使用すると、ユーザーはデスクトップアプリケーションインターフェイス上のWindowsエクスプローラーまたはMac Finderからファイルをドラッグすることで、ファイルやフォルダーをアップロードできます。詳しくは、[デスクトップアプリを使用したアセットの追加](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)を参照してください。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 最新のCIFコアコンポーネントバージョンv1.6.0が含まれるCIFベニアリファレンスサイト — 2020.12.01をリリースしました。詳細は、[CIFベニアリファレンスサイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01)を参照してください。

* CIF コアコンポーネント v1.6.0 をリリースしました。詳しくは、「[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0)」を参照してください。

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEMのCloud ManagerのCloud Service2020.12.0のリリース日は2020年12月10日です。

### [!DNL Cloud Manager] の新機能 {#what-is-new-cm}

* [SSL証明書](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)と[カスタムドメイン名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)のセルフサービス管理。

* [IP許可リスト](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)のセルフサービス管理。

* **環境**&#x200B;の詳細ページが更新され、環境上のカスタムドメイン名とIP許可リストを管理できるようになりました。

### バグ修正 {#bug-fixes-cloud-manager}

* コードスキャンステージで、解決された結果が提供されず、エラーが発生する場合があります。

* 環境カードに&#x200B;**追加**&#x200B;ボタンが一貫して表示されませんでした。

## コードリファクタリングツール {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] の新機能 {#what-is-new-crt}

* AIO-CLIプラグインの新しいバージョンがリリースされました。 このプラグインの最新バージョンには、AEM Dispatcher ConverterとRepository Modenizerのバグ修正が含まれ、新しいユーティリティIndex Converterもサポートされています。 このプラグインの詳細については、[統合エクスペリエンス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)を参照してください。

* Index Converterは、Cloud Service互換のOAKインデックス定義として、顧客のカスタムOAKインデックス定義をAEMに変換するために使用できるユーティリティです。 詳しくは、[Index Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)を参照してください。

* [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)に追加された新機能。すべてのOSGi設定を含む個別のパッケージ`ui.config`を作成します。

### バグ修正 {#crt-bug-fixes}

* AEM Dispatcher ConverterおよびRepository Modenizerツールで行われたいくつかのバグ修正。 [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)および[Repository Modenizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)を参照してください。
