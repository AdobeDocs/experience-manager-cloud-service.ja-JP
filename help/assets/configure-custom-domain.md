---
title: 配信層のカスタムドメインの設定
description: Adobe Cloud Managerで配信層用のカスタムドメインを設定する方法について説明します。
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: b24faf23435948a8f122223bf38227a0936bbeb5
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 46%

---


# 配信層のカスタムドメインの設定{#configure-custom-domain}

Adobe Cloud Manager では、カスタムドメインを追加して web サイトを目立たせることができます。 AEM as a Cloud Service にはデフォルトのドメインが設定されていますが、必要に応じてカスタマイズできます。

>[!NOTE]
>
>Dynamic Media PrimeまたはDynamic Media Ultimate ライセンスをご利用のお客様は、Cloud Managerで利用可能なセルフサービスのカスタムドメイン設定を使用する必要があります。
>詳しくは、[Dynamic Media PrimeおよびUltimate ドキュメント &#x200B;](/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md#configure-custom-domain-in-delivery-tier)を参照してください。
>
>OpenAPI付きDynamic Mediaが手動で有効になっている古いDynamic Media設定を使用しているお客様は、このドキュメントに従ってください。 これらの設定では、カスタムドメインマッピングはAdobe サポートリクエストを通じて完了します。

## 開始する準備を整える

設定プロセスを開始する前に、次の要件を満たしていることを確認します。

* Cloud Manager へのアクセス
* サポートチケットを通じて、環境上でOpenAPIを使用してDynamic Mediaを既に有効にしている
* 配信層で使用されるドメインのEVまたはOV タイプのSSL証明書。 詳しくは、[SSL証明書の概要](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates)を参照してください

## Cloud Manager を使用した配信層でのカスタムドメインの設定

Cloud Managerで次の手順を実行します。

1. [顧客管理SSL証明書の追加](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate#add-customer-managed-ssl-cert)

2. [カスタムドメイン名の追加](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name#adding-cdn-settings)

上記の手順を完了したら、カスタムドメインマッピング用にAdobe サポートチケットを発行します。 Adobeでは、サポートプロセスの一部としてドメインマッピングを実行します。