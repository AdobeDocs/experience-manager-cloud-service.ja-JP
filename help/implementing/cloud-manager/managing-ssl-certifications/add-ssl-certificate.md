---
title: SSL 証明書の追加
description: Cloud Manager のセルフサービスツールを使用して、独自の SSL 証明書またはアドビが管理する DV（ドメイン検証）証明書を追加する方法について説明します。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: bf903736e256bb9275bad6c0271b31b8dbdec625
workflow-type: ht
source-wordcount: '1021'
ht-degree: 100%

---


# SSL 証明書の追加 {#add-ssl-cert}

クラウドを使用して独自の SSL 証明書またはアドビが管理する DV（ドメイン検証）証明書を追加する方法について説明します。

>[!NOTE]
>
>顧客が管理する（OV/EV）SSL 証明書および CDN プロバイダーを使用している場合は、SSL 証明書の追加をスキップして、準備ができたら [CDN 設定の追加](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)に直接進むことができます。

証明書のプロビジョニングには、数日かかる場合があります。したがって、アドビでは、遅延を避けるために、期限や運用開始日に先立って独自の証明書をプロビジョニングすることをお勧めします。

Cloud Manager で SSL 証明書を更新および管理する方法について詳しくは、[SSL 証明書の管理](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)を参照してください。

証明書の追加または管理で問題が発生した場合は、[SSL 証明書エラーのトラブルシューティング](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md)を参照してください。


## 前提条件 {#prerequisites}

* SSL 証明書を追加するには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つメンバーである必要があります。
* 独自の証明書をインストールする場合は、[SSL 証明書の管理の概要](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements)の&#x200B;**証明書の要件**&#x200B;を参照してください。

## 追加する SSL 証明書の選択 {#which-ssl-to-add}

AEM Cloud Manager で [カスタムドメイン名を追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)した後、次の手順は、アドビが管理する（DV）SSL 証明書（推奨）と顧客が管理する（OV/EV）SSL 証明書のどちらを使用するかによって異なります。

* **アドビが管理する（DV）SSL 証明書の場合：**
   * ドメインの検証プロセスは、カスタムドメインが追加され、Cloud Manager で検証されると実行されます。
   * 次に、[アドビが管理する（DV）SSL 証明書を追加](#add-adobe-managed-ssl-cert)する必要があります。
Cloud Manager に追加したら、アドビがユーザーに代わって DV SSL 証明書を発行してインストールするまで待ちます。
   * 証明書がアクティブになると、カスタムドメインを使用する準備が整います。

* **顧客が管理する（OV/EV）SSL 証明書の場合：**

   * 認証機関から OV/EV SSL 証明書を取得します。詳しくは、[顧客が管理する OV/EV SSL 証明書の要件](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements)を確認してください。
   * 証明書を取得したら、[顧客が管理する（OV/EV）SSL 証明書](#add-customer-managed-ssl-cert)の詳細を Cloud Manager に追加します。
   * 追加すると、カスタムドメイン名は検証済みとマークされ、SSL 証明書が適用されます。

どちらの場合でも、証明書の検証とインストールが完了すると、カスタムドメインを環境で安全に使用できるようになります。Cloud Manager インターフェイスで定期的に[ドメインのステータスを確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)し、すべてが期待どおりに動作していることを確認します。

[SSL 証明書の概要](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)も参照してください。

## アドビが管理する（DV）SSL 証明書の追加 {#add-adobe-managed-ssl-cert}

ドメインでアドビが管理する SSL 証明書（推奨）と顧客が管理する SSL 証明書のどちらを使用するかを選択する際にサポートが必要ですか？[追加する SSL 証明書の選択](#which-ssl-to-add)を参照してください。

**アドビが管理する（DV）SSL 証明書を追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。
1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、サイドメニューを表示します。

1. **サービス**&#x200B;見出しの下にある ![鍵がかかったアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg)「**SSL 証明書**」をクリックします。

   ![SSL 証明書の追加](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. SSL 証明書ページの右上隅にある「**SSL 証明書を追加**」をクリックします。

1. **SSL 証明書を追加**&#x200B;ダイアログボックスで、[特定のユースケース](#which-ssl-to-add)に基づいて、「**アドビが管理する（DV）**」を選択します。

   ![DV 証明書の追加](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. 「**証明書名**」フィールドに、DV SSL 証明書に関連付ける名前を入力します。

1. **ドメインを選択**&#x200B;ドロップダウンリストで、DV SSL 証明書に関連付ける検証済みドメインを 1 つ以上選択します。
   * 選択するドメインがありませんか？その場合は、まず[カスタムドメイン名を追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)する必要があります。また、アドビが管理する SSL 証明書を追加する前に、ドメイン名が検証されていることを確認します。
   * カスタムドメイン名の追加が完了したら、このトピックに戻って手順 1 から再度開始します。

1. ダイアログボックスの右下隅にある「**保存**」をクリックします。

   SSL 証明書が正常に発行されると、**SSL 証明書**&#x200B;テーブルに緑色の有効なチェックマークが表示されます。

これで、アドビが管理する有効な DV SSL 証明書がプロジェクトに追加されました。この手順は、多くの場合、カスタムドメイン名を設定する最初の手順となります。

これで、[CDN 設定](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)を追加する準備が整いました。

## 顧客が管理する（OV/EV）SSL 証明書の追加 {#add-customer-managed-ssl-cert}

<!-- IF THIS TOPIC GET UPDATED, REMEMBER TO UPDATE THE STEPS ALSO IN THE "MANAGE SSL CERTIFICATES TOPIC TOO -->

ドメインでアドビが管理する SSL 証明書（推奨）と顧客が管理する SSL 証明書のどちらを使用するかを選択する際にサポートが必要ですか？[追加する SSL 証明書の選択](#which-ssl-to-add)を参照してください。

>[!IMPORTANT]
>
>SSL 証明書を追加または更新する際は、新しい証明書を証明書チェーンに含めないでください。含めると、アップロードが正常に完了しなくなります。

**顧客が管理する（OV/EV）SSL 証明書を追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、サイドメニューを表示します。

1. **サービス**&#x200B;見出しの下にある ![鍵がかかったアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg)「**SSL 証明書**」をクリックします。

   ![SSL 証明書の追加](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. SSL 証明書ページの右上隅にある「**SSL 証明書を追加**」をクリックします。

1. **SSL 証明書を追加**&#x200B;ダイアログボックスで、[特定のユースケース](#which-ssl-to-add)に基づいて、「**顧客が管理する（OV/EV）**」を選択します。

1. 「**証明書名**」フィールドに、証明書の名前を入力します。
このフィールドは情報提供のみを目的とし、SSL 証明書を簡単に参照するのに役立つ任意の名前を指定できます。

1. 「**証明書**」、「**秘密鍵**」、「**証明書チェーン**」フィールドで、OV または EV SSL 証明書から必要な値をコピーして、ダイアログボックスの各フィールドに貼り付けます。

   値で検出されたエラーが表示されます。証明書を保存する前に、すべてのエラーに対処する必要があります。一般的なエラーのトラブルシューティング方法について詳しくは、[証明書エラー](#certificate-errors)を参照してください。

   ![SSL 証明書を追加ダイアログボックス](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)|

1. ダイアログボックスの右下隅にある「**保存**」をクリックします。

   >[!NOTE]
   >
   >* [カスタムドメイン名を追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)中に&#x200B;**顧客が管理する証明書**&#x200B;を選択した場合、顧客が管理する（OV/EV） SSL 証明書が追加され保存された&#x200B;***後***&#x200B;にドメインが検証されます。[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to)も参照してください。

   SSL 証明書が正常に発行されると、**SSL 証明書**&#x200B;テーブルに緑色の検証済みチェックマークが表示されます。

これで、プロジェクトに機能する SSL 証明書が追加されました。この手順は、多くの場合、カスタムドメイン名を設定する最初の手順となります。

これで、[CDN 設定](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)を追加する準備が整いました。























<!--
## Add an SSL certificate {#add-ssl-cert}

1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate program.
1. On the **[My Programs](/help/implementing/cloud-manager/navigation.md#my-programs)** console, select the program.
1. In the upper-left corner of the page, click ![Show menu icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) to reveal the side menu. 
1. Under the **Services** heading, click ![Lock closed icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL Certificates**. 

   ![Adding an SSL certificate](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Near the upper-right corner of the SSL Certificates page, click **Add SSL Certificate**.

1. In the **Add SSL certificate** dialog box, based on [your particular use case](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), do one of the following:

    | | Use case | Steps |
    | --- | --- | --- |
    | 1 | **Add an Adobe managed (DV) certificate** | **To add an Adobe managed (DV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Adobe managed (DV)**.<br>![Add a DV certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. In the **Certificate name** field, enter a name you want associated with the certificate.<br>c. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV SSL certificate.<br>No domains to select? If so, it means that you must first add a custom domain name and ensure it is verified before you can add an SSL certificate. See [Add a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). When you are finished adding a custom domain name, return to this topic and begin at step 1 again.<br>d. Continue to step 7. |
    | 2 | **Add a customer managed (OV/EV) certificate** | **To add a customer managed (OV/EV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Customer managed (OV/EV)**.<br>b. In the **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your SSL certificate easily.<br>c. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.<br>![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate Errors](#certificate-errors) to learn more about troubleshooting common errors.<br>d. Continue to step 7. | 

1. In the lower-right corner of the dialog box, click **Save**.

    >[!NOTE]
    >
    >* If you selected **Adobe managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified with the added certificate when the custom domain is added. 
    >
    >* If you selected **Customer managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified ***after*** the customer managed (OV/EV) SSL certificate is added and saved. See also [Check the status of a custom domain name](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to).

    After the SSL certificate is successfully issued, it is displayed with a green verified check mark in the **SSL Certificates** table. 

    You now have added a working SSL certificate for your project. This step is often the first to set up a custom domain name. 
    

* To learn about updating and managing your SSL certificates in Cloud Manager, see [Manage SSL certificates](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

* If you are having issues adding or managing your certificates, see [Troubleshoot SSL certificate errors](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md). -->
