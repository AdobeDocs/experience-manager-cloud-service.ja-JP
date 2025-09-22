---
title: 配信層用のカスタムドメインの設定
description: Adobe Cloud Managerで配信層用のカスタムドメインを設定する方法について説明します。
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: d2859c547c87bd1856ba0e05fac835db434d824c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 78%

---

# 配信層用のカスタムドメインの設定{#configure-custom-domain}

Adobe Cloud Manager では、カスタムドメインを追加して web サイトを目立たせることができます。AEM as a Cloud Service にはデフォルトのドメインが設定されていますが、必要に応じてカスタマイズできます。

## 始める前に

* マルチ SAN（サブジェクト代替名）TLS または SSL 証明書が必要です。
* SSL 証明書には、同じドメイン内の配信層用にマッピングされた証明書に対して個別の SAN が必要です。
* 証明書ポリシーは、ドメイン検証（DV）ポリシーではなく、拡張検証（EV）または組織検証（OV）のいずれかに準拠する必要があります。


## 配信層用のカスタムドメインの設定

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
