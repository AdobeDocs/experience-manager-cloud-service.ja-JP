---
title: SSL 証明書の追加
description: Cloud Manager セルフサービスツールを使用して独自の SSL 証明書または DV （Domain Validation）証明書を追加する方法を説明します。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 6fb672e03fe28ae8af6dc873791c7d1ac1fb8fd7
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 20%

---


# SSL 証明書の追加

Cloud Manager セルフサービスツールを使用して、お客様が管理する SSL 証明書、またはAdobeが生成および管理する DV （ドメイン検証）証明書を追加する方法について説明します。

[SSL 証明書エラーのトラブルシューティング ](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md) も参照してください。


## SSL 証明書の追加 {#adding-an-ssl-certificate}

証明書のプロビジョニングには数日かかる場合があります。そのため、Adobeでは、期限や公開日に先立って証明書を適切にプロビジョニングすることをお勧めします。

[SSL 証明書の管理の概要 **の** 証明書要件 ](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements) を確認し、追加する証明書がAEM as a Cloud Serviceでサポートされていることを確認してください。

このタスクを完了するには、ユーザーが **ビジネスオーナー** または **デプロイメントマネージャー** の役割のメンバーである必要があります。

>[!NOTE]
>
>DV （ドメイン検証）証明書をアップロードすることはできません。

**SSL 証明書を追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **概要**&#x200B;ページから、**環境**&#x200B;画面に移動します。

1. 左側のナビゲーションパネルの&#x200B;**サービス**&#x200B;で、「**SSL 証明書**」をクリックします。次の画像に示すような左側のナビゲーションパネルが表示されない場合は、左上隅のハンバーガーアイコンをクリックする必要がある場合があります。

   ![SSL 証明書の追加 ](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. ページの右上隅付近にある「**SSL 証明書を追加**」をクリックします。

1. **SSL 証明書を追加** ダイアログボックスで、[ 特定のユースケース ](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) に応じて、次のいずれかの操作を行います。

   | | ユースケース | 手順 |
   | --- | --- | --- |
   | 1 | **Adobe管理証明書（DV）を追加する** | **Adobe管理証明書（DV）を追加するには：**<br> a.証明書の種類 **Adobe管理（DV）** を選択します。<br>![DV 証明書の追加 ](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b.**ドメインを選択** ドロップダウンリストで、DV 証明書に関連付けるドメインを 1 つ以上選択します。<br> 選択するドメインがありませんか？ その場合は、カスタムドメインを追加する必要があります。 [ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) を参照してください。 カスタムドメイン名の追加が完了したら、このトピックに戻って手順 1 から再度開始します。<br>d.手順 7 に進みます。 |
   | 2 | **顧客管理証明書（OV/EV）の追加** | **顧客管理証明書（OV/EV）を追加するには：**<br> a.証明書のタイプ **顧客管理（OV/EV）** を選択します。<br>b.**証明書名** フィールドに、証明書の名前を入力します。 このフィールドは情報提供のみを目的とし、証明書を簡単に参照するのに役立つ任意の名前を指定できます。<br>c.「**証明書**」、「**秘密鍵**」、「**証明書チェーン**」の各フィールドに、必要な値をそれぞれのフィールドに貼り付けます。<br>![SSL 証明書を追加ダイアログボックス ](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br> 値に検出されたエラーが表示されます。 証明書を保存する前に、すべてのエラーを解決する必要があります。 一般的なエラーのトラブルシューティングについて詳しくは、[ 証明書エラー ](#certificate-errors) を参照してください。<br>d.手順 7 に進みます。 |

<!--
    **Add an SSL certificate:**
    1. Select the certificate type **Customer managed (OV/EV)**.
    1. In **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your certificate easily.
    1. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.

        ![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)
  
    Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate errors](#certificate-errors) to learn more about troubleshooting common errors.

    **Add a DV certificate:**
    1. Select the certificate type **Adobe managed (DV)**.

        ![Adding a DC certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

    1. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV certificate.

        No domains to select? If so, it means that you must add a custom domain. See [Add a custom domain](#add-custom-domain). When you are finished, resume the steps from the beginning again. -->

1. ダイアログボックスの右下隅にある「**保存**」をクリックします。

   証明書が正常に発行されると、「**SSL 証明書** 表に緑色のチェックマークが表示されます。

これで、プロジェクトに作業用 SSL 証明書を追加しました。 この手順は、多くの場合、カスタムドメイン名を設定する最初の手順となります。

* カスタムドメイン名を設定するには、[ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) を参照してください。
* Cloud Managerでの SSL 証明書の更新および管理について詳しくは、[SSL 証明書の管理 ](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) を参照してください。

<!--
### Add a custom domain {#add-custom-domain}

Before you can add an Adobe generated and managed Domain Validated (DV) certificate, you must first add a custom domain. The process for doing so is nearly the same as detailed in [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) and [Add a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). However, that functionality is now slightly expanded, as described below.

1. When adding a custom domain name, in the **Verify domain** dialog box, select an **Adobe managed certificate**.

    ![Choose Adobe-managed](assets/verify-domain-dialog.png)

1. In the **Verify domain** dialog box, add a CNAME verification record to your DNS.

    ![Add CNAME entry](assets/verify-domain-dialog-adobe-managed.png)

1. After the domain is created, click the ellipsis button in the list of domains and select **Verify** to verify the domain.

    ![Verify domain](assets/verify-domain.png) 

1. Resume the task [Add a DV certificate](#adding-an-ssl-certificate). -->


