---
title: 概要 - SSL 証明書の管理
description: 概要 - SSL 証明書の管理
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: 09a2c24b848364954dc5621995d0d0dc24059011
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 93%

---

# はじめに {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="SSL 証明書の管理"
>abstract="Cloud Manager では、セルフサービス機能を使用して、Cloud Manager UI から SSL 証明書をインストールできます。Cloud Manager は、Platform TLS サービスを使用して、SSL 証明書と、通常はサードパーティの証明機関から取得して顧客が所有しする秘密鍵を管理します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/view-update-replace-ssl-certificate.html?lang=ja" text="SSL 証明書の表示、更新、置換"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/check-status-ssl-certificate.html?lang=ja" text="SSL 証明書のステータスの確認"


Cloud Manager では、セルフサービス機能を使用して、Cloud Manager UI から SSL 証明書をインストールできます。Cloud Manager は、Platform TLS サービスを使用して、SSL 証明書と、通常はサードパーティの証明機関（例：「*Let’s Encrypt*」）から取得して顧客が所有しする秘密鍵を管理します。

## 重要な検討事項 {#important-considerations}

* Cloud Manager からは、SSL 証明書や秘密鍵は提供されません。これらは、サードパーティの証明機関から入手する必要があります。詳しくは、「[SSL 証明書の取得](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md)」を参照してください。

* AEM as a Cloud Service は、セキュリティで保護された `https` サイトのみをサポートしています。複数のカスタムドメインがある場合、ドメインを追加するたびに証明書をアップロードしたくはありません。したがって、複数のドメインを持つ 1 つの証明書を取得することで、顧客にはメリットが得られます。

* AEM as a Cloud Serviceは、OV（組織の検証）または EV（拡張検証）ポリシーに準拠する証明書のみを受け付けます。 DV（ドメイン検証）ポリシーは受け入れられません。 さらに、証明書はすべて、2048 ビットの RSA 秘密鍵と一致する信頼できる証明機関（CA）の X.509 TLS 証明書にする必要があります。

* AEM as a Cloud Service は、ドメインのワイルドカード SSL 証明書を受け入れます。

* Cloud Manager では、1 つ以上の環境に関連付けることができる SSL 証明書は、証明書の有効期限が切れている場合でも、プログラム全体で常に最大 50 個まで許可されます。ただし、Cloud Manager UI では、最大 50 個までの SSL 証明書をプログラムにインストールできます。通常、証明書は複数のドメイン（最大 100 個の SAN）に対応できるので、この制限内に収まるように、複数のドメインを同じ証明書でグループ化することを検討してください。

Cloud Manager では、次の顧客向け SSL 証明書の要件をサポートしています。

* SSL 証明書は複数の環境で使用できます。つまり、1 回追加すれば複数回使用できます。
* 各 Cloud Manager 環境は、複数の証明書を使用できます。
* 秘密鍵は、複数の SSL 証明書を発行する場合があります。
* 通常、各証明書には複数のドメインが含まれます。 
* プラットフォーム TLS サービスは、終了に使用された SSL 証明書と、そのドメインをホストする CDN サービスに基づいて、リクエストを顧客の CDN サービスにルーティングします。

権限を持つユーザーは、Cloud Manager UI SSL 証明書ページを使用して、次のようなタスクを実行してプログラムの SSL 証明書を管理できます。

* [SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [SSL 証明書の表示、更新、置換](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
   >[!NOTE]
   >これらの操作により、表示の詳細や、期限切れになる証明書の置き換えが可能になります。
* [SSL 証明書の削除](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)
