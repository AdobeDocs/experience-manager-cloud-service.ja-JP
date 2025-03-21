---
title: AEM Assets を Creative Cloud に接続
description: AEM Assets を設定し、Creative Cloud に接続する方法を説明します。別の IMS 組織にプロビジョニングされた Creative Cloud 権限に接続して、Express ライブラリや Creative Cloud ライブラリなどの最新の Creative Cloud 統合を AEM Assets で簡単に使用できます。
exl-id: 880200fe-94b3-49de-802c-34283f7c71bc
feature: Collaboration
role: User
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 91%

---

# AEM Assets を Creative Cloud に接続  {#cross-org-entitlements}

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

Experience Manager Assets には、別の IMS 組織にプロビジョニングされた Creative Cloud 権限に接続する機能があり、この機能を使用すると、Express ライブラリや Creative Cloud ライブラリなどの最新の Creative Cloud 統合を AEM Assets で簡単に使用できます。

Creative Cloud 製品と AEM Assets が別の IMS 組織にプロビジョニングされている場合は、異なる Creative Cloud 組織に接続して、2 つのソリューション間で統合されたワークフローを実行できます。

## 前提条件 {#prerequisites}

* Experience Manager Assets に対する管理者権限

* Creative Cloud と Experience Manager 間で使用される同じユーザー ID に対する Creative Cloud へのアクティブな権限です。同じメールアドレスを持つ個人用 ID と Federated ID に対する権限は、異なるユーザー ID として処理されます。

## 新しい Creative Cloud 組織に対する接続 {#connect-to-creative-cloud-org}

新しい Creative Cloud 組織に接続するには、次の手順を実行します。

1. **[!UICONTROL 設定]**／**[!UICONTROL Creative Cloud]** に移動します。

1. **[!UICONTROL 新しい Creative Cloud 組織 ID を選択]**&#x200B;ドロップダウンリストを使用して、新しい Creative Cloud 組織を選択します。リストには、アクセス権のあるすべての組織が表示されます。アクティブな Creative Cloud 権限を持つ組織を選択します。

1. 「**[!UICONTROL 組織を切り替え]**」をクリックして、新しい組織に切り替えます。

   ![組織をまたいだ権限](assets/cross-org-entitlements.png)

## 制限事項 {#limitations}

* AEM Assets は、一度に 1 つの Creative Cloud 組織に接続できます。一度に複数の Creative Cloud 組織への接続はサポートされていません。

* AEM Assets 内で接続する Creative Cloud 組織は、組織内のすべてのユーザーに適用できます。
