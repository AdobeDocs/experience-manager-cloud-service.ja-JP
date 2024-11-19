---
title: AEM Assetsとダウンストリームアプリケーションの統合
description: AEM Assetsとダウンストリームアプリケーションの統合
role: User
exl-id: abd48b5d-2b43-453c-8eb6-31ff509245ca
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 8%

---

# AEM Assetsとダウンストリームアプリケーションの統合 {#integrate-dynamic-media-open-apis}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>OpenAPI 機能ガイドのDynamic MediaがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE OpenAPI 機能ガイドPDFのDynamic Media]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Experience Managerアセットリポジトリで使用可能なすべての [ 承認済みアセット ](/help/assets/approve-assets.md) を、ダウンストリームアプリケーションに配信できます。

検索および配信 API を使用して独自のカスタムユーザーインターフェイスをExperience Manager Assets リポジトリと統合するか、Adobeのマイクロフロントエンドアセットセレクターを使用できます。

![AEM Assets リポジトリとの統合 ](assets/asset-selector-integration.png)

API を使用すると、AEM Assets リポジトリから承認済みアセットを検索し、配信 URL を使用してダウンストリームアプリケーションにそのアセットを配信できます。 詳しくは、[ 検索 ](/help/assets/search-assets-api.md) および [ 配信 ](/help/assets/deliver-assets-apis.md) API を参照してください。

Adobeのマイクロフロントエンドアセットセレクターは、[!DNL Experience Manager Assets as a Cloud Service] リポジトリと簡単に統合できるユーザーインターフェイスを提供します。ユーザーはこれにより、リポジトリで使用可能な承認済みデジタルアセットを参照または検索し、アプリケーションのオーサリングエクスペリエンスで使用できるようになります。 詳しくは、[ マイクロフロントエンドアセットセレクター ](/help/assets/overview-asset-selector.md) を参照してください。

>[!MORELIKETHIS]
>
* [ アセットセレクターと様々なアプリケーションの統合 ](/help/assets/integrate-asset-selector.md)
* [ アセットセレクターのプロパティ ](/help/assets/asset-selector-properties.md)
* [ アセットセレクターのカスタマイズ ](/help/assets/asset-selector-customization.md)
