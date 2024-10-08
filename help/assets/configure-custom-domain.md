---
title: Publish層用のカスタムドメインの設定
description: AdobeCloud Managerでパブリッシュ層のカスタムドメインを設定する方法について説明します。
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 7%

---

# パブリッシュ層用のカスタムドメインの設定{#configure-custom-domain}

| [ 検索のベストプラクティス ](/help/assets/search-best-practices.md) | [ メタデータのベストプラクティス ](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えたDynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets開発者向けドキュメント ](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

AdobeCloud Managerでは、カスタムドメインを追加して web サイトを目立たせることができます。 AEM as a Cloud Serviceにはデフォルトドメインが付属していますが、必要に応じてカスタマイズできます。

## 事前準備

* マルチ SAN （サブジェクト代替名）の TLS または SSL 証明書が必要です。
* SSL 証明書には、同じドメイン内のパブリッシュ層用にマッピングされた証明書に対して個別の SAN が必要です。
* 証明書ポリシーは、ドメイン検証（DV）ポリシーではなく、拡張検証（EV）または組織検証（OV）のいずれかに準拠する必要があります。


## パブリッシュ層用のカスタムドメインの設定

1. **[!UICONTROL Cloud ManagerAdobe]**/**[!UICONTROL プログラムの概要]**/**[!UICONTROL SSL 証明書]** に移動して、SSL 証明書を追加します。
   ![ 画像 ](/help/assets/assets/ssl-certificate.png)
AdobeCloud Managerに [SSL 証明書 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) を追加する方法を説明します。

1. SSL 証明書を追加したら、カスタムドメインを追加します。 **[!UICONTROL ドメイン設定]** をクリックし、**[!UICONTROL Publish サービス]** オプションに対してカスタムドメインを指定します。
詳細情報 [ カスタムドメイン ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

1. 公開ドメインに対応する DNS レコードに 2 つの [CNAME レコード ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) を追加します。
DNS の生成遅延が原因で、DNS 検証の処理に数時間かかる場合があります。

1. カスタムドメインの設定を容易にするサポートケースをログに記録し、カスタムドメインが配信層にリダイレクトされるようにします。

>[!NOTE]
>
>許可されたリダイレクト URL リストにカスタムドメインを追加します。 リストは、アセットセレクターの IMS クライアントにあります。<br> 各Adobeチームと調整し、カスタムドメイン文字列を指定して、このタスクを実行します。
