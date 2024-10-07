---
title: SSL 証明書の追加
description: Cloud Managerのセルフサービスツールを使用して、独自の SSL 証明書またはAdobe管理の DV （ドメイン検証）証明書を追加する方法について説明します。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 493c5729c3107f151685a243006b17196b74c1bd
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 74%

---


# SSL 証明書の追加 {#add-ssl-cert}

Cloud を使用して独自の SSL 証明書またはAdobe管理の DV （ドメイン検証）証明書を追加する方法について説明します

>[!TIP]
>
>証明書のプロビジョニングには数日かかる場合があります。そのため、Adobeでは、独自の証明書を提供する場合は、期限や公開日に先立って適切にプロビジョニングすることをお勧めします。

## 前提条件 {#prerequisites}

* 証明書を追加するには、ユーザーが **ビジネスオーナー** または **デプロイメントマネージャー** の役割を持つメンバーである必要があります。
* 独自の証明書をインストールする場合は、**SSL 証明書の管理の概要** の [ 証明書の要件 ](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements) を必ず確認してください。

## SSL 証明書の追加 {#add-certificate}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。
1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、サイドメニューを表示します。
1. **サービス**&#x200B;見出しの下にある ![鍵がかかったアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg)「**SSL 証明書**」をクリックします。

   ![SSL 証明書の追加](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. SSL 証明書ページの右上隅にある「**SSL 証明書を追加**」をクリックします。

1. **SSL 証明書を追加**&#x200B;ダイアログボックスで、[特定のユースケース](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)に基づいて、次のいずれかの操作を行います。

   | | ユースケース | ステップ |
   | --- | --- | --- |
   | 1 | **アドビが管理する（DV）証明書を追加** | **アドビが管理する（DV）証明書を追加するには：**<br> a. **SSL 証明書を追加**&#x200B;ダイアログボックスで、「**アドビが管理する（DV）**」証明書タイプを選択します。<br>![DV 証明書を追加](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. 「**証明書名**」フィールドに、証明書に関連付ける名前を入力します。<br>c. **ドメインを選択**&#x200B;ドロップダウンリストで、DV 証明書に関連付けるドメインを 1 つ以上選択します。<br>選択するドメインがありませんか？その場合は、カスタムドメインを追加する必要があります。詳しくは、[カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)を参照してください。カスタムドメイン名の追加が完了したら、このトピックに戻って手順 1 から再度開始します。<br>d. 手順 7 に進みます。 |
   | 2 | **顧客が管理する（OV／EV）証明書を追加** | **顧客が管理する（OV／EV）証明書を追加するには：**<br> a. **SSL 証明書を追加**&#x200B;ダイアログボックスで、「**顧客が管理する（OV／EV）**」証明書タイプを選択します。<br>b.「**証明書名**」フィールドに、証明書の名前を入力します。このフィールドは情報提供のみを目的とし、証明書を簡単に参照するのに役立つ任意の名前を指定できます。<br>c.「**証明書**」、「**秘密鍵**」、「**証明書チェーン**」の各フィールドに必要な値を貼り付けます。<br>![SSL 証明書を追加ダイアログボックス](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>値で検出されたエラーが表示されます。証明書を保存する前に、すべてのエラーに対処する必要があります。一般的なエラーのトラブルシューティング方法について詳しくは、[証明書エラー](#certificate-errors)を参照してください。<br>d. 手順 7 に進みます。 |

1. ダイアログボックスの右下隅にある「**保存**」をクリックします。

証明書が正常に発行されると、「**SSL 証明書** 表に緑色のチェックマークが付いて表示されます。

これで、プロジェクトに機能する SSL 証明書が追加されました。この手順は、多くの場合、カスタムドメイン名を設定する最初の手順となります。

* カスタムドメイン名を設定する方法について詳しくは、[カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)を参照してください。
* Cloud Manager で SSL 証明書を更新および管理する方法について詳しくは、[SSL 証明書の管理](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)を参照してください。

>[!TIP]
>
>証明書の追加または管理で問題が発生した場合は、[SSL 証明書エラーのトラブルシューティング ](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md) のドキュメントを参照してください。
