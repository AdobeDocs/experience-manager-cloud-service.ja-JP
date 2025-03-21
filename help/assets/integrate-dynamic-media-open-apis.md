---
title: AEM Assets とダウンストリームアプリケーションの統合
description: AEM Assets とダウンストリームアプリケーションの統合
role: User
exl-id: abd48b5d-2b43-453c-8eb6-31ff509245ca
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 88%

---

# AEM Assets とダウンストリームアプリケーションの統合 {#integrate-dynamic-media-open-apis}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
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

>[!AVAILABILITY]
>
>OpenAPI 機能搭載 Dynamic Media のガイドを、PDF 形式で利用できるようになりました。ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えてください。
>
>[!BADGE OpenAPI 機能搭載 Dynamic Media ガイドの PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Experience Manager Assets リポジトリで使用可能なすべての[承認済みアセット](/help/assets/approve-assets.md)は、ダウンストリームアプリケーションに配信できます。

検索および配信 API を使用して独自のカスタムユーザーインターフェイスを Experience Manager Assets リポジトリと統合するか、アドビのマイクロフロントエンドのアセットセレクターを使用できます。

![AEM Assets リポジトリとの統合](assets/asset-selector-integration.png)

API を使用すると、AEM Assets リポジトリから承認済みアセットを検索し、配信 URL を使用してアセットをダウンストリームアプリケーションに配信できます。詳しくは、[検索](/help/assets/search-assets-api.md)および[配信](/help/assets/deliver-assets-apis.md)の API を参照してください。

アドビのマイクロフロントエンドのアセットセレクターは、[!DNL Experience Manager Assets as a Cloud Service] リポジトリと簡単に統合できるユーザーインターフェイスを提供します。ユーザーはこれにより、リポジトリで使用可能な承認済みデジタルアセットを参照または検索し、アプリケーションのオーサリングエクスペリエンスで使用できるようになります。詳しくは、[マイクロフロントエンドのアセットセレクター](/help/assets/overview-asset-selector.md)を参照してください。

>[!MORELIKETHIS]
>
* [アセットセレクターと様々なアプリケーションの統合](/help/assets/integrate-asset-selector.md)
* [アセットセレクターのプロパティ](/help/assets/asset-selector-properties.md)
* [アセットセレクターのカスタマイズ](/help/assets/asset-selector-customization.md)
