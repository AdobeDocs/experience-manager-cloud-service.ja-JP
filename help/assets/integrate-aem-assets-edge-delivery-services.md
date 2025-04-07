---
title: 統合  [!DNL AEM Assets]  コンテンツのオーサリング中  [!DNL Edge Delivery Services]
description: ' [!DNL AEM Assets] with [!DNL Edge Delivery Services]. This integration enables you to integrate [!DNL AEM Assets] with [!DNL Microsoft Word] and [!DNL Google Docs], integrate [!DNL AEM Assets] with [!DNL Universal Editor], integrate [!DNL Dynamic Media] with [!DNL Edge Delivery Services], integrate [!DNL Dynamic Media with OpenAPI capabilities] with [!DNL Universal Editor] and integrate [!DNL Dynamic Media with OpenAPI capabilities] with [!DNL Microsoft Word] and [!DNL Google Docs] を統合する方法を説明します。'
tags: AEM Assets, Edge Delivery Services, Dynamic Media, Dynamic Media with OpenAPI capabilities, Universal Editor, Edge Delivery Services with Universal Editor
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: fecaefbb6a02e944be38c3dfaa3baea5691219cd
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 6%

---


# [!DNL Edge Delivery Services] 用コンテンツのオーサリング時の [!DNL AEM Assets] の統合 {#integrate-aem-assets-with-edge-delivery-services}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime と Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Dynamic Media Prime と Ultimate の有効化</b></a>
        </td>
         <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

![ ユニバーサルエディターとAEM Assets の統合 ](/help/assets/assets/EDS2.png)

[[!DNL Edge Delivery Services]](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/overview) は、web サイト上のコンテンツの作成と配信を高度に柔軟に行える、構成可能なサービスセットです。 [AEM コンテンツ管理 ](/help/sites-cloud/authoring/author-publish.md) と [WYSIWYG オーサリングの両方を  [!DNL Universal Editor]  を使用して実行できるほか、ドキュメントベースのオーサリングも使用 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring) きます。

次の場所でコンテンツを編集できます。

* [[!DNL Microsoft Word] または  [!DNL Google Docs]](#integrate-dynamic-media-with-edge-delivery-services)
* [[!DNL Universal Editor]](#integrate-aem-assets-with-universal-editor-UE)

編集したコンテンツは、Edge Delivery Servicesに公開できます。

## [!DNL Edge Delivery Services] 向けの [!DNL AEM Assets] とドキュメントベースのオーサリングフローの統合 {#integrate-dynamic-media-with-edge-delivery-services}

[!DNL AEM Assets] が [!DNL Microsoft Word] や [!DNL Google Docs] などのドキュメントベースのオーサリングツールと統合されると、オーサリングツールでアセットセレクターが提供されます。 このアセットセレクターを使用してア [!DNL AEM Assets] ットにアクセスし、承認済みのアセットをコンテンツに挿入します。
既に [!DNL Edge Delivery Services] web サイトがある場合は、[[!DNL AEM Assets]  プラグイン ](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) のドキュメントを参照して、既存の [!DNL AEM] プロジェクト [!DNL AEM Assets] 統合する方法を確認してください。
ドキュメントベースのオーサリングツールで作成した包括的なコンテンツを公開する [!DNL Edge Delivery Services] web サイトがない場合は、次の [ 前提条件 ](#integrate-aem-assets-with-microsoft-word-and-google-docs) および [ [!DNL AEM Assets]  ドキュメントベースのオーサリング環境との統合 ](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs) の節に従 [!DNL AEM Assets] ます。

### 前提条件{#integrate-aem-assets-with-microsoft-word-and-google-docs}

開始する前に、ドキュメントベースのオーサリング環境が準備されていることを確認します。

* [!DNL AEM] とドキュメントベースのオーサリングツールを統合して、オーサリング環境を設定します。 オーサリング環境の設定方法については、[ はじめに – 開発者チュートリアル ](https://www.aem.live/developer/tutorial) を参照してください。

### [!DNL AEM Assets] とドキュメントベースのオーサリング環境の統合{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

[!DNL Microsoft Word] または [!DNL Google Docs] でのコンテンツのオーサリング中にアセットを使用するように、[!DNL AEM Assets] Sidekick プラグインを設定します。

* Microsoft Word またはGoogle DocsでAEM Assetsにアクセスして使用する方法については、[[!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors) を参照してください。
* 設定について詳しくは、[ 設定  [!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin) を参照してください。
  ![ms word および google ドキュメントの openAPI 機能で dynamic media を使用する ](/help/assets/assets/my-assets-sidebar.png)

## [!DNL Dynamic Media with OpenAPI capabilities] を使用したアセットの配信 {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

[!DNL Dynamic Media with OpenAPI capabilities] を使用して配信されたアセットを使用することもできます。 次のような多くの利点があります。

* [!DNL AEM Assets Cloud Services] からブランド承認済みアセット（画像、ビデオ、PDF、その他のアセットタイプ）へのアクセスのみ。
* ガバナンス（参照とアセットのコピー）。有効期限、削除、更新などのアセットライフサイクルイベントの自動伝播に役立ちます。
* 動的画像レンディションとスマート切り抜き。
* すぐに使用できるアダプティブビデオストリーミングや PDF 用のオリジナルアセット配信など、リッチメディアの最適化と配信。
* アセットレベルのインプレッションレポート（限定提供 [） ](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)。

機能について詳しくは、ドキュメントを参照 [[!DNL Dynamic Media with OpenAPI capabilities]](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview) てください。

### 前提条件 {#dynamic-media-with-universal-editor-and-edge-delivery-services}

アセット参照を使用するには、以下が必要です。

* [!DNL Dynamic Media with Open API capabilities] が有効になっているAssets Cloud Service環境の使用権限。
* [!DNL Dynamic Media] ライセンス。
* 画像アセットのコピー参照を有効にした [!DNL AEM Assets sidekick plugin]。 詳しくは、ドキュメントベースのオーサリングについては [ このドキュメント ](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode) を、ユニバーサルエディターベースのオーサリングについては [ このドキュメント ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) を参照してください。
* 承認済みのAssets。 承認済みのアセットは、Assets Cloud Services のバックエンドまたは UI のアクションを介して `dam:status=Approved` 認されています。

### [!DNL Dynamic Media with OpenAPI capabilities] を使用して配信されるアセットの使用{#Using-Dynamic-Media-with-edge-delivery-services}

次のリンクを選択して、[!DNL Dynamic Media with OpenAPI capabilities] を使用してコンテンツに画像、ビデオ、その他のアセットタイプを配信する方法について確認してください。

* [ コンテンツへの画像の追加 ](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [ コンテンツへのビデオの追加 ](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [PDF、Zip ファイルなど、画像以外のアセットやビデオアセットをコンテンツに追加します ](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

OpenAPI 機能を備えた Dynamic Media を使用してコンテンツ内のアセットを配信する方法については、このビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## サンプル [!DNL Edge Delivery Services] サイト{#dynamic-media-with-google-docs-and-ms-word}

[!DNL Edge Delivery Services] のドキュメントベースのオーサリング機能を使用して構築されたサイトである [WKND Travel](http://bit.ly/3DExLnf) を参照してください。 サイトのコンテンツは [Google Docsで作成され ](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT) コンテンツ内のアセットを配信するために使用さ [!DNL Dynamic Media with OpenAPI capabilities] ます。 オーサリング後、コンテンツはドキュメントから直接公開されます。 この [Git リポジトリー ](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks) を参照して、この [!DNL Edge Delivery Services (EDS)] サイトのドキュメントベースのオーサリング設定の作成に使用される、すべての重要なファイル、フォルダー、設定、web サイトのスタイル設定および機能コードについて確認します。

## [!DNL Edge Delivery Services] 用の [!DNL Universal Editor] ベースのオーサリングフローとの [!DNL AEM Assets] の統合 {#integrate-aem-assets-with-universal-editor-UE}

[!DNL AEM Assets] と統合する [!DNL Universal Editor] を設定します。 この統合により、[!DNL Dynamic Media with OpenAPI capabilities] を使用してアセットを配信できるようになります。

* [!DNL Universal Editor] でカスタムアセットピッカー機能を追加する方法については、[Site [!DNL Edge Delivery]  の設定 ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) を参照してください。 カスタムのアセットピッカーを使用すると、[!DNL Universal Editor] コンテンツに直接アセットを挿入できます。
* [!DNL Universal Editor] でのオーサリング中に [!DNL AEM Assets] にアクセスしてアセットを挿入する方法については、[ 拡張機能の概要 ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) を参照してください。
