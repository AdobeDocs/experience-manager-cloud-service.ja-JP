---
title: パブリッシュ層のカスタムドメインの設定
description: AdobeCloud Manager でパブリッシュ層のカスタムドメインを設定する方法について説明します。
role: null
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---


# パブリッシュ層のカスタムドメインの設定{#configure-custom-domain}

Adobeの Cloud Manager では、カスタムドメインを追加することで web サイトを目立たせることができます。 AEM as a Cloud Serviceにはデフォルトのドメインが付属していますが、必要に応じてカスタマイズできます。
<!-- For example, AEM sites can use `sites.custom_domain.com`, and the AEM publish domain can be accessed via `assets.custom_domain.com`. Additionally, getting an SSL certificate for assets.pmi.com with a SAN entry for `delivery.custom_domain.com` improves security and trustworthiness. -->

## 事前準備

* マルチ SAN （サブジェクト代替名）の TLS または SSL 証明書が必要です。
* SSL 証明書には、同じドメイン内のパブリッシュ層用にマッピングされた証明書に対して個別の SAN が必要です。
* 証明書ポリシーは、ドメイン検証（DV）ポリシーではなく、拡張検証（EV）または組織検証（OV）のいずれかに準拠する必要があります。


## カスタムドメインを追加

パブリッシュ層のカスタムドメインを設定するには、次の手順に従います。

1. に移動 **[!UICONTROL Cloud Manager のAdobe]** > **[!UICONTROL プログラムの概要]** > **[!UICONTROL SSL 証明書]**を選択し、SSL 証明書を追加します。
   ![画像](/help/assets/assets/ssl-certificate.png)
追加方法を学ぶ [SSL 証明書](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) cloud Manager のAdobeで以下を行います。

1. SSL 証明書を追加したら、カスタムドメインを追加します。 クリック **[!UICONTROL ドメイン設定]** およびに対するカスタムドメインを指定します。 **[!UICONTROL パブリッシュサービス]** オプション。
   <br> の詳細情報 [カスタムドメイン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html?lang=en).

1. 公開ドメインに対応する 2 つの CNAME レコードを DNS レコードに追加します。
   <br> DNS の伝播遅延が原因で、DNS 検証の処理に数時間かかる場合があります。

1. カスタムドメインの設定を容易にするサポートケースをログに記録し、カスタムドメインが配信層にリダイレクトされるようにします。

>[!NOTE]
>
> 必ずアセットセレクターの IMS クライアントで許可されているリダイレクト URL のリストにカスタムドメインを追加してください。<br>各Adobeチームと調整し、カスタムドメイン文字列を指定して、このタスクを実行します。
