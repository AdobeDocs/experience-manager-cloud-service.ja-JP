---
title: AEM Assets と Edge Delivery Services 向けコンテンツのオーサリングの統合
description: AEM AssetsをEdge Delivery Servicesと統合する方法について説明します。 この統合により、AEM AssetsとMicrosoft Word およびGoogle Docsの統合、AEM Assetsと Universal Editor の統合、Dynamic Media と OpenAPI 機能と Universal Editor の統合、Dynamic Media と OpenAPI 機能とMicrosoft Word およびGoogle Docsの統合が可能になります。
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: e4a71d1a513bebed67b9571a483871dc16c36daa
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 3%

---

# AEM Assets と Edge Delivery Services 向けコンテンツのオーサリングの統合 {#integrate-aem-assets-while-authoring-for-edge-delivery-services}

![UE でAEM アセット ](/help/assets/assets/EDS2.png)

[Edge Delivery Services](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/overview) は、Web サイト上のコンテンツのオーサリングと配信を高度に柔軟に行える、構成可能なサービスセットです。 ユニバーサルエディターを使用した [AEM コンテンツ管理 ](/help/sites-cloud/authoring/author-publish.md) および [WYSIWYG オーサリングと、ドキュメントベースのオーサリングの両方を使用 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring) きます。

次の場所でコンテンツを編集できます。

* [Microsoft Word またはGoogle Docs](#integrate-aem-assets-with-document-based-authoring-tools)
* [ユニバーサルエディター](#integrate-aem-assets-with-UE-universal-editor)

編集したコンテンツは、Edge Delivery Servicesに公開できます。

## Edge Delivery ServicesのAEM Assetsとドキュメントベースのオーサリングフローとの統合 {#integrate-aem-assets-with-document-based-authoring-tools}

AEM AssetsをMicrosoft Word やGoogle Docsなどのドキュメントベースのオーサリングツールと統合すると、エディターにアセットセレクターが表示されます。 このアセットセレクターを使用してAEM Assetsにアクセスし、承認済みアセットをドキュメントに挿入します。
既にEdge Delivery Servicesの web サイトがある場合は、[AEM Assets プラグイン ](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) を参照して、AEM Assetsを既存のAEM プロジェクトと統合する方法を確認してください。
ドキュメントベースのオーサリングツールで作成したAEM Assetsを含むコンテンツを公開するEdge Delivery Services Web サイトを持っていない場合は、次の [ 前提条件 ](#integrate-aem-assets-with-microsoft-word-and-google-docs) および [ ドキュメントベースのオーサリング環境とのAEM Assetsの統合 ](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs) の節に従ってください。

### 前提条件{#integrate-aem-assets-with-microsoft-word-and-google-docs}

開始する前に、ドキュメントベースのオーサリング環境が準備されていることを確認します。

* AEMをドキュメントベースのオーサリングツールと統合して、オーサリング環境を設定します。 オーサリング環境の設定方法については、[ はじめに – 開発者チュートリアル ](https://www.aem.live/developer/tutorial) を参照してください。

### AEM Assetsとドキュメントベースのオーサリング環境の統合{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

Microsoft Word またはGoogle Docsでコンテンツをオーサリングする際にアセットを使用するように、AEM Assets Sidekick プラグインを設定します。

* Microsoft Word またはGoogle DocsでAdobe Experience Manager Assetsにアクセスして使用する方法については ](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors)[AEM Assets Sidekick プラグイン } を参照してください。
* 設定について詳しくは、[Adobe Experience Manager Assets Sidekick プラグインの設定 ](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin) を参照してください。
  ![ms word および google ドキュメントの openAPI 機能で dynamic media を使用する ](/help/assets/assets/my-assets-sidebar.png)

## OpenAPI 機能を備えた Dynamic Media を使用したアセットの配信 {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

OpenAPI 機能を備えた DM を使用して配信されたアセットを使用することもできます。 次のような多くの利点があります。

* AEM Assets Cloud Services からブランド承認済みアセット（画像、ビデオ、PDF、その他のアセットタイプ）へのアクセスのみ。
* ガバナンス（参照とアセットのコピー）。有効期限、削除、更新などのアセットライフサイクルイベントの自動伝播に役立ちます。
* 動的画像レンディションとスマート切り抜き。
* すぐに使用できるアダプティブビデオストリーミングや PDF 用のオリジナルアセット配信など、リッチメディアの最適化と配信。
* アセットレベルのインプレッションレポート（限定提供 [） ](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)。

機能について詳しくは、[OpenAPI 機能を備えた Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview) ドキュメントを参照してください。

### 前提条件 {#prerequisites-for-dm-with-openapi-capabilities-to-use-aem-assets}

アセット参照を使用するには、以下が必要です。

* Open API 機能を備えた Dynamic Media が有効になっているAssets Cloud Service環境に対する使用権限。
* Dynamic Media ライセンス。
* 画像アセットのコピー参照が有効になっているAEM Assets サイドキックプラグインが有効になりました。 詳しくは、ドキュメントベースのオーサリングでは [this](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode) を、ユニバーサルエディターベースのオーサリングでは [this](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) を参照してください。
* 承認済みのAssets。 承認済みのアセットは、Assets Cloud Services のバックエンドまたは UI のアクションを介して `dam:status=Approved` 認されています。

### OpenAPI 機能を備えた Dynamic Media を使用して配信されるアセットを使用する{#how-to-use-Dynamic-Media-with-OpenAPI-assets}

次のリンクを選択して、Dynamic Media を OpenAPI 機能と共に使用して、画像、ビデオ、その他のアセットタイプをコンテンツに配信する方法について学習してください。

* [ コンテンツへの画像の追加 ](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [ コンテンツへのビデオの追加 ](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [PDF、Zip ファイルなど、画像以外のアセットやビデオアセットをコンテンツに追加します ](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

OpenAPI 機能を備えた Dynamic Media を使用してコンテンツ内のアセットを配信する方法については、このビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## Edge Delivery Services サイトのサンプル{#example-of-an-Edge-Delivery-Services-site}

Edge Delivery Servicesのドキュメントベースのオーサリング機能を使用して構築されたサイトである [WKND Travel](http://bit.ly/3DExLnf) を参照してください。 サイトのコンテンツは [Google Docsで作成され ](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT)OpenAPI 機能を備えた Dynamic Media を使用してコンテンツ内にアセットが配信されます。 オーサリング後、コンテンツはドキュメントから直接公開されます。 この [Git リポジトリー ](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks) を参照して、このEdge Delivery Services（EDS）サイト用の Document-Based Authoring 設定の作成に使用される、すべての重要なファイル、フォルダー、設定、web サイトのスタイル設定と機能コードについて知ります。

## AEM AssetsとEdge Delivery Servicesのユニバーサルエディターベースのオーサリングフローの統合 {#integrate-aem-assets-with-UE-universal-editor}

AEM Assetsと統合するためのユニバーサルエディターを設定します。 この統合により、Dynamic Media を OpenAPI 機能と共に使用してアセットを配信できるようになります。

* ユニバーサルエディターでカスタムのアセットピッカー機能を追加する方法については、[Edge Delivery サイトの設定 ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) を参照してください。 カスタムのアセットピッカーを使用すると、ユニバーサルエディターのコンテンツに直接アセットを挿入できます。
* ユニバーサルエディターでのオーサリング中にAEM Assetsにアクセスしてアセットを挿入する方法については、[ 拡張機能の概要 ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) を参照してください。
