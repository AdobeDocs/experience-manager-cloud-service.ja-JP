---
title: '[!DNL Experience Manager Assets] と  [!DNL Adobe Workfront] の統合'
description: ' [!DNL Assets] と [!DNL Workfront]の統合の概要'
role: Admin, Leader, Architect
feature: Workfront Integrations and Apps
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 93%

---

# [!DNL Adobe Workfront] との [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] 統合 {#assets-integration-overview}

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

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

[!DNL Adobe Workfront] は作業管理アプリケーションで、作業のライフサイクル全体を一元的に管理するのに役立ちます。[!DNL Workfront] と [!DNL Adobe Experience Manager Assets] の統合により、組織は、作業とデジタルアセット管理を本質的に関連付けることで、コンテンツベロシティを向上させ市場投入までの時間を短縮することができます。Workfront での作業を管理するコンテキスト内で、ユーザーは必要なドキュメントと画像にアクセスできます。

Adobeオファー [統合する [!DNL Workfront] および [!DNL Adobe Experience Manager Assets] ネイティブ ( サポートAssets Essentialsとas a Cloud Service)](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html?lang=ja).

ネイティブ Experience Manager 統合と  を使用すると、以下が可能です。

* Workfront 内で統合をすばやく設定します。

* Workfront と Experience Manager の間でリンクされたフォルダーを自動的に作成します。

* 既存のリンクされたアセットのメタデータを容易に同期します。

* Workfront で変更された場合、プロジェクトメタデータを自動的に更新します。

* 複数の Experience Manager Assets リポジトリを 1 つの Workfront 環境に、または複数の Workfront 環境を 1 つの Experience Manager Assets リポジトリに、組織 ID を横断してスムーズに接続します。


## Workfront for Experience Manager 拡張コネクタに関するセッション {#enhanced-connector-information}


2022年6月に、アドビは Workfront と Adobe Experience Manager Assets as a Cloud Service を接続するための新しいネイティブ統合をリリースしました。この統合は、これら 2 つのソリューションを接続するために必須の方法となりました。Workfront と AEM Assets as a Cloud Service を接続する拡張コネクタ（1.9.8 以降）の今後の新しい実装は、ブロックされます。この統合の設定方法について詳しくは、[Experience Manager Assets as a Cloud Service統合の設定](workfront-connector-configure.md)を参照してください。

>[!NOTE]
>
>アドビでは、Workfront for Experience Manager 拡張コネクタと Experience Manager 統合の並行使用をサポートしていません。

2022 年 6 月より前のインストールでは、次に、のデプロイメントと設定に関する注意事項を示します。 [!DNL Adobe Workfront for Experience Manager enhanced connector]:

* Adobeは、認定パートナーまたは [!DNL Adobe Professional Services] を介してのみ [!DNL Adobe Workfront for Experience Manager enhanced connector] のデプロイメントと構成を必要とします。認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobe ではサポートされません。
* アドビは、このコネクターを冗長にする[!DNL Adobe Workfront]および [!DNL Adobe Experience Manager] の更新をリリースする可能性があります。この場合、お客様はこのコネクターの使用から移行する必要が生じることがあります。
* アドビでは、拡張コネクタバージョン 1.7.4 以降をサポートしています。以前のプレリリースバージョンやカスタムバージョンはサポートされていません。拡張コネクタのバージョンを確認するには、[拡張コネクタのインストール手順](workfront-connector-install.md)の手順 5(a) を参照してください。
* 詳しくは、[Workfront for Experience Manager Assets 拡張コネクタに関するパートナー認定試験](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)を参照してください。試験について詳しくは、[試験ガイド](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)を参照してください。