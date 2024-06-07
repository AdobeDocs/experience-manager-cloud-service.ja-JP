---
title: ドメイン検証済み（DV）証明書
description: Cloud Manager でドメイン検証（DV）証明書を管理する方法について説明します。
source-git-commit: 5baeb4012e5aa82a8cd8710b18d9164583ede0bd
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 6%

---


# ドメイン検証済み（DV）証明書 {#domain-validated-certificates}

Cloud Manager でドメイン検証（DV）証明書を管理する方法について説明します。

>[!NOTE]
>
>この機能は、[早期導入プログラム](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)でのみ利用できます。

## はじめに {#introduction}

Cloud Manager では、セルフサービス方式で、ドメイン検証済み（DV） SSL 証明書を生成および管理できます。 これにより、オンラインビジネスに安全な Web サイトを作成するための、最も迅速で簡単でコスト効率に優れたソリューションを提供します。

ドメインで検証された証明書は、両方で利用できます [実稼動およびサンドボックスプログラム。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## カスタムドメインの追加 {#adding-domain}

ドメイン検証済み（DV）証明書を追加するには、まずカスタムドメインを設定する必要があります。 プロセスは、ドキュメントで詳しく説明されたものとほぼ同じです [カスタムドメイン名の概要。](/help/implementing/cloud-manager/custom-domain-names/introduction.md) ただし、その機能は少し拡張されています。

1. ドメインを検証する際に、ドメインでAdobeが管理する証明書または自己管理の証明書を使用できます。 を選択 **Adobe管理証明書** 後で DV 証明書を追加するために使用します。

   ![Adobeが管理するものを選択](assets/verify-domain-dialog.png)

1. Adobeが管理する証明書を使用するには、に記載されているように、CNAME レコードを DNS に追加する必要があります。 **ドメインの検証** ダイアログ。

   ![CNAME エントリを追加](assets/verify-domain-dialog-adobe-managed.png)

1. ドメインを作成したら、ドメインのリストの省略記号ボタンをタップまたはクリックし、選択します。 **検証** ドメインを検証します。

   ![ドメインの検証](assets/verify-domain.png)

## DV 証明書の追加 {#adding}

ドメインを正しく設定したら、「」をタップまたはクリックして、DV 証明書を追加します **SSL 証明書を追加** ボタンをクリックします。

![DC 証明書の追加](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. オプションを選択します **Adobe管理（DV）**.
1. でドメイン名を指定 **ドメインを選択** ドロップダウン。
1. 「**保存**」をタップまたはクリックします。

正常に追加されると、証明書のステータスが保留中になり、黄色の警告サインが内の名前に付きます。 **SSL 証明書** ウィンドウ。

![保留中の DV 証明書](assets/pending-dv-certificate.png)

証明書が正常に発行されると、その名前には緑色のチェックマークが **SSL 証明書** ウィンドウ。

![発行された DV 証明書](assets/issued-dv-certificate.png)

SSL 証明書の追加および SSL 証明書ウィンドウについて詳しくは、ドキュメントを参照してください [SSL 証明書の追加](add-ssl-certificate.md)

## CDN 設定の追加 {#add-cdn}

この手順は、Fastly CDN を使用して SSL でドメインを設定する場合に完了する必要があります。

Cloud Manager を使用して CDN 設定を追加するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 「」を選択します **CDN 設定** tab キーを押しながらクリックまたはタップ **追加** ツールバーで変更します。

1. が含まれる **CDN の設定** ダイアログで、必要な情報を入力します。

   * 「」を選択します **複製元**. 次のことが考えられます。
      * Cloud Service環境
      * Edge Delivery Servicesサイト
   * CDN タイプを選択します。
   * ドメインを選択します。
   * SSL 証明書を選択します。
      * Adobeが管理する CDN の場合にのみ必要です。

   ![CDN を設定ダイアログ](assets/configure-cdn-dialog.png)

>
>
>Adobeが管理する CDN の場合、DV 証明書を使用する場合、ACME 検証が有効なサイトのみ許可されます。
