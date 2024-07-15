---
title: パブリッシュ層のカスタムドメインの設定
description: AdobeCloud Managerでパブリッシュ層のカスタムドメインを設定する方法について説明します。
source-git-commit: f6c0e8e5c1d7391011ccad5aa2bad4a6ab7d10c3
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 6%

---


# パブリッシュ層のカスタムドメインの設定{#configure-custom-domain}

AdobeCloud Managerでは、カスタムドメインを追加して web サイトを目立たせることができます。 AEM as a Cloud Serviceにはデフォルトドメインが付属していますが、必要に応じてカスタマイズできます。

## 事前準備

* マルチ SAN （サブジェクト代替名）の TLS または SSL 証明書が必要です。
* SSL 証明書には、同じドメイン内のパブリッシュ層用にマッピングされた証明書に対して個別の SAN が必要です。
* 証明書ポリシーは、ドメイン検証（DV）ポリシーではなく、拡張検証（EV）または組織検証（OV）のいずれかに準拠する必要があります。


## カスタムドメインを追加

パブリッシュ層のカスタムドメインを設定するには、次の手順に従います。

1. **[!UICONTROL Cloud ManagerAdobe]**/**[!UICONTROL プログラムの概要]**/**[!UICONTROL SSL 証明書]** に移動して、SSL 証明書を追加します。
   ![ 画像 ](/help/assets/assets/ssl-certificate.png)
AdobeCloud Managerに [SSL 証明書 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) を追加する方法を説明します。

1. SSL 証明書を追加したら、カスタムドメインを追加します。 **[!UICONTROL ドメイン設定]** をクリックし、**[!UICONTROL Publish サービス]** オプションに対してカスタムドメインを指定します。
詳細情報 [ カスタムドメイン ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

1. 公開ドメインに対応する DNS レコードに 2 つの [CNAME レコード ](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) を追加します。
DNS の伝播遅延が原因で、DNS 検証の処理に数時間かかる場合があります。

1. カスタムドメインの設定を容易にするサポートケースをログに記録し、カスタムドメインが配信層にリダイレクトされるようにします。

>[!NOTE]
>
> 必ずアセットセレクターの IMS クライアントで許可されているリダイレクト URL のリストにカスタムドメインを追加してください。<br> 各Adobeチームと調整し、カスタムドメイン文字列を指定して、このタスクを実行します。
