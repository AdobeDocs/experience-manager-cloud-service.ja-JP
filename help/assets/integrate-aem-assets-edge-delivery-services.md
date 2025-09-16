---
title: ' [!DNL Edge Delivery Services] のコンテンツ作成時の  [!DNL AEM Assets]  の統合'
description: ' [!DNL AEM Assets]  と  [!DNL Edge Delivery Services]. This integration enables you to integrate [!DNL AEM Assets]  と  [!DNL Microsoft Word]  を統合し、 [!DNL Google Docs], integrate [!DNL AEM Assets]  と  [!DNL Universal Editor], integrate [!DNL Dynamic Media]  と  [!DNL Edge Delivery Services], integrate [!DNL Dynamic Media with OpenAPI capabilities]  と  [!DNL Universal Editor]  を統合し、 [!DNL Dynamic Media with OpenAPI capabilities]  と  [!DNL Microsoft Word]  と  [!DNL Google Docs] を統合する方法について説明します。'
tags: AEM Assets, Edge Delivery Services, Dynamic Media, Dynamic Media with OpenAPI capabilities, Universal Editor, Edge Delivery Services with Universal Editor
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: 79213bcfe5c5ccf7c60a31e6cb757f60a0ba87a7
workflow-type: ht
source-wordcount: '628'
ht-degree: 100%

---


# [!DNL Edge Delivery Services] のコンテンツ作成時の [!DNL AEM Assets] の統合 {#integrate-aem-assets-with-edge-delivery-services}

![AEM Assets とユニバーサルエディターの統合](/help/assets/assets/EDS2.png)

[[!DNL Edge Delivery Services]](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/overview) は、web サイト上のコンテンツの柔軟なオーサリングおよび配信を実現する、合成可能なサービスセットです。[AEM コンテンツ管理](/help/sites-cloud/authoring/author-publish.md)と [ [!DNL Universal Editor]  を使用した WYSIWYG オーサリングとドキュメントベースのオーサリング](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)の両方を使用できます。

次のツールでコンテンツを編集できます。

* [[!DNL Microsoft Word] または  [!DNL Google Docs]](#integrate-dynamic-media-with-edge-delivery-services)
* [[!DNL Universal Editor]](#integrate-aem-assets-with-universal-editor-UE)

コンテンツを編集したら、Edge Delivery Services に公開できます。

## [!DNL AEM Assets] と [!DNL Edge Delivery Services] のドキュメントベースのオーサリングフローの統合 {#integrate-dynamic-media-with-edge-delivery-services}

[!DNL AEM Assets] を [!DNL Microsoft Word] や [!DNL Google Docs] などのドキュメントベースのオーサリングツールと統合すると、オーサリングツールにアセットセレクターが提供されます。このアセットセレクターを使用して [!DNL AEM Assets] にアクセスし、承認済みのアセットをコンテンツに挿入します。
既に [!DNL Edge Delivery Services] web サイトを使用している場合は、[[!DNL AEM Assets]  プラグイン](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md)のドキュメントを参照して、[!DNL AEM Assets] を既存の [!DNL AEM] プロジェクトに統合する方法を確認してください。ドキュメントベースのオーサリングツールで作成した [!DNL AEM Assets] を含むコンテンツを公開するための [!DNL Edge Delivery Services] web サイトがない場合は、次の[前提条件](#integrate-aem-assets-with-microsoft-word-and-google-docs)および[ [!DNL AEM Assets]  とドキュメントベースのオーサリング環境の統合](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs)の節に従ってください。

### 前提条件{#integrate-aem-assets-with-microsoft-word-and-google-docs}

開始する前に、ドキュメントベースのオーサリング環境の準備が整っていることを確認します。

* [!DNL AEM] をドキュメントベースのオーサリングツールと統合して、オーサリング環境を設定します。オーサリング環境の設定方法について詳しくは、[はじめに - 開発者チュートリアル](https://www.aem.live/developer/tutorial)を参照してください。

### [!DNL AEM Assets] とドキュメントベースのオーサリング環境の統合{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

[!DNL Microsoft Word] または [!DNL Google Docs] でコンテンツを作成する際にアセットを使用するように [!DNL AEM Assets] Sidekick プラグインを設定します。

* Microsoft Word または Google Docs で AEM Assets にアクセスして使用する方法について詳しくは、[[!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors) を参照してください。
* 設定について詳しくは、[ [!DNL Adobe Experience Manager Assets Sidekick Plugin] の設定](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin)を参照してください。
  ![MS Word および Google Docs で OpenAPI 機能を備えた Dynamic Mediaを使用](/help/assets/assets/my-assets-sidebar.png)

## [!DNL Dynamic Media with OpenAPI capabilities] を使用したアセットの配信 {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

[!DNL Dynamic Media with OpenAPI capabilities] を使用して配信されたアセットを使用することもできます。これには、次のような多くのメリットがあります。

* [!DNL AEM Assets Cloud Services] から、ブランド承認済みアセット（画像、ビデオ、PDF、その他のアセットタイプ）にのみにアクセス可能。
* ガバナンス（アセットの参照とコピー）により、有効期限、削除、更新などのアセットライフサイクルイベントの自動生成が可能。
* 動的な画像レンディションとスマート切り抜き。
* 標準のアダプティブビデオストリーミングや、PDF のオリジナルアセット配信など、リッチメディアの最適化と配信。
<!--

* Asset-level impressions report ([limited availability](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)).

-->

機能については詳しく、[[!DNL Dynamic Media with OpenAPI capabilities]](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview) ドキュメントを参照してください。

### 前提条件 {#dynamic-media-with-universal-editor-and-edge-delivery-services}

アセット参照を使用するには、以下が必要です。

* [!DNL Dynamic Media with Open API capabilities] が有効になっている Assets Cloud Service 環境への使用権限。
* [!DNL Dynamic Media] ライセンス。
* 画像アセットのコピー参照が有効になっている [!DNL AEM Assets sidekick plugin]。ドキュメントベースのオーサリングについて詳しくは、[このドキュメント](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode)を参照し、ユニバーサルエディターベースのオーサリングについて詳しくは、[このドキュメント](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)を参照してください。
* 承認済みのアセット。承認済みのアセットには、Assets Cloud Services のバックエンドまたは UI アクションを通じて `dam:status=Approved` が設定されます。

### [!DNL Dynamic Media with OpenAPI capabilities] を使用して配信されたアセットの使用{#Using-Dynamic-Media-with-edge-delivery-services}

[!DNL Dynamic Media with OpenAPI capabilities] を使用して、画像、ビデオ、その他のアセットタイプをコンテンツに配信する方法について詳しくは、以下のリンクを選択してください。

* [コンテンツへの画像の追加](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [コンテンツへのビデオの追加](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [PDF、Zip ファイルなど、画像やビデオ以外のアセットのコンテンツへの追加](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

OpenAPI 機能を備えた Dynamic Media を使用してコンテンツ内のアセットを配信する方法について詳しくは、このビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## サンプル [!DNL Edge Delivery Services] サイト{#dynamic-media-with-google-docs-and-ms-word}

[!DNL Edge Delivery Services] のドキュメントベースのオーサリング機能を使用して作成されたサイトの [WKND Travel](https://aem-dynamicmedia-demo--dm--hlxsites.aem.live/travel-hospitality/wknd-trvl-home) を参照してください。サイトのコンテンツは [Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT) で作成され、コンテンツ内のアセットの配信には [!DNL Dynamic Media with OpenAPI capabilities] が使用されます。オーサリング後、コンテンツはドキュメントから直接公開されます。この [!DNL Edge Delivery Services (EDS)] サイトのドキュメントベースのオーサリング設定を作成するために使用されるすべての基本的なファイル、フォルダー、設定、web サイトのスタイルと機能コードについて詳しくは、この [Git リポジトリ](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks)を参照してください。

## [!DNL AEM Assets] と [!DNL Edge Delivery Services] の [!DNL Universal Editor] ベースのオーサリングフローの統合 {#integrate-aem-assets-with-universal-editor-UE}

[!DNL Universal Editor] を設定して、[!DNL AEM Assets] と統合します。この統合により、[!DNL Dynamic Media with OpenAPI capabilities] を使用してアセットを配信できます。

* [!DNL Universal Editor] にカスタムアセットピッカー機能を追加する方法について詳しくは、[ [!DNL Edge Delivery]  サイトの設定](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site)を参照してください。カスタムアセットピッカーを使用すると、[!DNL Universal Editor] コンテンツにアセットを直接挿入できます。
* [!DNL Universal Editor] でオーサリング中に [!DNL AEM Assets] にアクセスしてアセットを挿入する方法について詳しくは、[拡張機能の概要](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)を参照してください。
