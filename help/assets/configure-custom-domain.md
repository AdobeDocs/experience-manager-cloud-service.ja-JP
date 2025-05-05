---
title: パブリッシュ層のカスタムドメインの設定
description: Adobe Cloud Manager でパブリッシュ層のカスタムドメインを設定する方法について説明します。
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 91%

---

# パブリッシュ層のカスタムドメインの設定{#configure-custom-domain}

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

Adobe Cloud Manager では、カスタムドメインを追加して web サイトを目立たせることができます。AEM as a Cloud Service にはデフォルトのドメインが設定されていますが、必要に応じてカスタマイズできます。

## 始める前に

* マルチ SAN（サブジェクト代替名）TLS または SSL 証明書が必要です。
* SSL 証明書には、同じドメイン内のパブリッシュ層にマッピングされた証明書に対して個別の SAN が必要です。
* 証明書ポリシーは、ドメイン検証（DV）ポリシーではなく、拡張検証（EV）または組織検証（OV）のいずれかに準拠する必要があります。


## パブリッシュ層のカスタムドメインの設定

1. **[!UICONTROL Adobe Cloud Manager]**／**[!UICONTROL プログラムの概要]**／**[!UICONTROL SSL 証明書]**&#x200B;に移動し、SSL 証明書を追加します。
   ![画像](/help/assets/assets/ssl-certificate.png)
詳しくは、Adobe Cloud Manager で [SSL 証明書](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)を追加する方法を参照してください。

1. SSL 証明書を追加した後、カスタムドメインを追加します。「**[!UICONTROL ドメイン設定]**」をクリックし、「**[!UICONTROL パブリッシュサービス]**」オプションに対してカスタムドメインを指定します。
詳しくは、[カスタムドメイン](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)を参照してください。

1. パブリッシュドメインに対応する 2 つの [CNAME レコード](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)を DNS レコードに追加します。
DNS の生成遅延が原因で、DNS 検証の処理に数時間かかる場合があります。

1. カスタムドメインの設定を容易にし、配信層に確実に誘導するために、サポートケースをログに記録します。

>[!NOTE]
>
>許可されたリダイレクト URL リストにカスタムドメインを追加します。リストは、アセットセレクターの IMS クライアントにあります。<br>カスタムドメイン文字列を指定して、このタスクを実行するには、それぞれのアドビチームと調整してください。
