---
title: Dynamic Media のビデオ
description: 失敗したDynamic Media配信 URL のエラーレポートをリクエストする方法を説明します。
contentOwner: Rick Brough
feature: Asset Management
role: User
hide: true
hidefromtoc: true
exl-id: 2488f813-df15-4dbb-8747-f827ee5925e1
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 90%

---

# 失敗したDynamic Media配信 URL のエラーレポートをリクエストします

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

配信時に失敗したDynamic Media URL を識別するエラーレポートを要求できます。 レポートは、最大 5 日間のデータを集計したもので、CSV 形式で利用できます。 エラーレポートには、次の情報が含まれます。

* 失敗したDynamic Media配信 URL — 失敗した URL とは、配信時にコンテンツを生成できない、Dynamic Media生成の URL です。
* リファラー URL — 失敗した配信 URL の呼び出し元のリファラー URL。
* 失敗数 — 配信 URL が読み込まれ、失敗した回数。

エラーレポートをリクエストすると、AdobeのDynamic Mediaチームから CSV 形式でレポートが電子メールで送信されます。 リクエストがおこなわれた日から 5 日間の期間が対象です。

指定した会社に関して、月に 1 回エラーレポートをリクエストできます。

**失敗したDynamic Media配信 URL のエラーレポートをリクエストするには：**

1. [reports-dynamic-media@adobe.comに電子メールを送信](mailto:reports-dynamic-media@adobe.com) を、Dynamic Mediaアカウントに関連付けられている会社名に変更します。

   会社名が不明な場合は、 [Dynamic Media Configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html?lang=ja#configuring-dynamic-media-cloud-services) ページ内 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL ツール]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Dynamic Media Configuration]**. Dynamic Media Configuration Browser ページで、 **[!UICONTROL global]**&#x200B;を選択し、 *[Dynamic_Media_folder_icon]* 「 」チェックボックスをオンにして、「 」を選択します。 **[!UICONTROL 編集]**. Dynamic Media設定ページにアクセスするには、AEMの管理者権限が必要です。

   ![Dynamic Media設定ページへのアクセス](/help/assets/dynamic-media/assets/reporting-accessdmconfig.png)
