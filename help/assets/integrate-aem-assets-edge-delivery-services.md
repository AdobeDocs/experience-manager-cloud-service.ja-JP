---
title: AEM Assets と Edge Delivery Services 向けコンテンツのオーサリングの統合
description: AEM AssetsをEdge Delivery Servicesと統合する方法について説明します。 この統合により、AEM AssetsとMicrosoft Word およびGoogle ドキュメントを統合したり、AEM Assetsと Universal Editor を統合したり、Dynamic Mediaと OpenAPI 機能と Universal Editor を統合したり、Dynamic Mediaと OpenAPI 機能をMicrosoft Word およびGoogle ドキュメントと統合したりできます。
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: e6fd7b1d16aac5e7021a8c309f6483f98746e85e
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 3%

---

# AEM Assets と Edge Delivery Services 向けコンテンツのオーサリングの統合 {#integrate-aem-assets-while-authoring-for-edge-delivery-services}

![EDS2](/help/assets/assets/EDS2.png)

[Edge Delivery Services](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/overview) は、Web サイト上のコンテンツの作成と配信を高度に柔軟に行える、構成可能なサービスセットです。 ユニバーサルエディターを使用した [AEM コンテンツ管理 ](/help/sites-cloud/authoring/author-publish.md) および [WYSIWYG オーサリングと、ドキュメントベースのオーサリングの両方を使用 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring) きます。

次の場所でコンテンツを編集できます。

* [Microsoft Word またはGoogle ドキュメント](#integrate-aem-assets-with-document-based-authoring-tools)

* [ユニバーサルエディター](#integrate-aem-assets-with-universal-editor)

コンテンツを編集した後、Edge Delivery Servicesに公開できます。

## Edge Delivery Services向けのAEM Assetsとドキュメントベースのオーサリングフローの統合 {#integrate-aem-assets-with-document-based-authoring-tools}

Microsoft Word やGoogle ドキュメントなどのドキュメントベースのオーサリングツールとAEM Assetsを統合すると、エディターにアセットセレクターが直接表示されます。 このアセットセレクターを使用してAEM Assetsにアクセスし、承認済みアセットをドキュメントに挿入します。

既にEdge Delivery Servicesの web サイトがある場合は、[AEM Assets プラグイン ](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) を参照して、AEM Assetsを既存のAEM プロジェクトに統合します。 Edge Delivery Services Web サイトがない場合は、以下の [ 前提条件 ](#integrate-aem-assets-with-microsoft-word-and-google-docs) および [AEM Assetsとドキュメントベースのオーサリング環境の統合 ](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs) の節を参照してください。

### 前提条件{#integrate-aem-assets-with-microsoft-word-and-google-docs}

開始する前に、ドキュメントベースのオーサリング環境が準備されていることを確認します。

* AEMをドキュメントベースのオーサリングツールと統合して、オーサリング環境を設定します。 オーサリング環境を設定するには、[ はじめに – 開発者チュートリアル ](https://www.aem.live/developer/tutorial) を参照してください。

### AEM Assetsとドキュメントベースのオーサリング環境の統合{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

Microsoft Word ドキュメントまたはGoogle ドキュメントのコンテンツのオーサリング中にアセットを使用するように、AEM Assets Sidekickプラグインを設定します。

* Adobe Experience Manager Assets Word またはGoogle ドキュメントでAEM Assetsにアクセスして使用する方法については ](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors)[Microsoft Sidekickプラグイン } を参照してください。
* 設定について詳しくは、[Adobe Experience Manager Assets Sidekickプラグインの設定 ](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin) を参照してください。
  ![my-assets-sidebar](/help/assets/assets/my-assets-sidebar.png)

## OpenAPI 機能を備えたDynamic Mediaを使用したアセットの配信 {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

OpenAPI 機能を備えた DM を使用して配信されたアセットを使用することもできます。 次のような多くの利点があります。

* AEM Assets Cloud Serviceからブランド承認済みアセット（画像、ビデオ、PDF、その他のアセットタイプ）へのアクセスのみ。
* ガバナンス（参照とアセットのコピー）。有効期限、削除、更新などのアセットライフサイクルイベントの自動伝播に役立ちます。
* 動的画像レンディションとスマート切り抜き。
* すぐに使用できるアダプティブビデオストリーミングやPDF向けのオリジナルアセット配信など、リッチメディアの最適化と配信。
* アセットレベルのインプレッションレポート（限定提供 [） ](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)。

機能について詳しくは、[OpenAPI 機能を備えたDynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview) ドキュメントを参照してください。

### 前提条件 {#prerequisites-for-dm-with-openapi-capabilities-to-use-aem-assets}

アセット参照を使用するには、以下が必要です。

* Open API 機能を備えたAssetsが有効になっているDynamic MediaCloud Service環境に対する使用権限。
* Dynamic Media ライセンス。
* 画像アセットのコピー参照が有効になっているAEM Assets サイドキックプラグインが有効になりました。 詳しくは、ドキュメントベースのオーサリングでは [this](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode) を、ユニバーサルエディターベースのオーサリングでは [this](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) を参照してください。
* 承認済みのAssets。 承認済みのアセットは、Assets Cloud Serviceのバックエンドまたは UI のアクションを介して `dam:status=Approved` 認されます。

### Dynamic Mediaを使用して配信されるアセットを OpenAPI 機能と共に使用する{#how-to-use-Dynamic-Media-with-OpenAPI-assets}

コンテンツのオーサリング中に、Dynamic Mediaを使用して OpenAPI 機能とともに配信されるアセットを使用するには、以下を参照してください。

* [ 画像参照の使用 ](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [ ビデオリファレンスの使用 ](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [PDF、Zip ファイルなどの非画像アセットやビデオアセットに対するアセットリファレンスの使用 ](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

OpenAPI 機能を備えたDynamic Mediaを使用してアセットを配信する方法については、このビデオを参照してください。

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## サンプルEdge Delivery Servicesサイト{#example-of-an-Edge-Delivery-Services-site}

[WKND Travel](https://aem-dynamicmedia-demo--dm--hlxsites.aem.live/travel-hospitality/wknd-trvl-home) を参照してください。 このサイトは、Edge Delivery Servicesのドキュメントベースのオーサリング機能を使用して構築されています。 サイトのコンテンツは、アセット配信用の OpenAPI 機能を備えたDynamic Mediaを使用して、[Google ドキュメント ](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT) でオーサリングされます。 作成したコンテンツは、ドキュメントから直接公開されます。 このドキュメントベースのオーサリング設定の場合、すべての重要なファイル、フォルダー、設定、web サイトのスタイル設定および機能コードがこの [Git リポジトリ ](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks) に保存されます。

## Edge Delivery Services向けのAEM Assetsとユニバーサルエディターベースのオーサリングフローの統合 {#integrate-aem-assets-with-universal-editor}

AEM Assetsと統合するためのユニバーサルエディターを設定します。 この統合により、Dynamic Mediaを OpenAPI 機能と共に使用してアセットを配信できるようになります。

* ユニバーサルエディターにカスタムアセットピッカー機能を追加するには、[Edge Delivery サイトの設定 ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) を参照してください。 カスタムのアセットピッカーを使用すると、ユニバーサルエディターのコンテンツに直接アセットを挿入できます。
* ユニバーサルエディターでのオーサリング中にAEM Assetsにアクセスしてアセットを挿入する方法については、[ 拡張機能の概要 ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) を参照してください。
