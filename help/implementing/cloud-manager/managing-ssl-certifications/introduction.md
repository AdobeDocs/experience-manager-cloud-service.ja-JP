---
title: 概要 — SSL 証明書の管理
description: 概要 — SSL 証明書の管理
translation-type: tm+mt
source-git-commit: 4ab944ad15390f9399138672a024aa30cf4aede8
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 78%

---


# 概要 {#introduction}

Cloud Manager では、セルフサービス機能を使用して、Cloud Manager UI から SSL 証明書をインストールできます。Cloud Managerは、SSL証明書と顧客が所有する秘密鍵を管理するためにプラットフォームTLSサービスを使用します。通常は、*Let’s Encrypt*&#x200B;のように、サードパーティの証明機関から取得します。

## 重要な検討事項 {#important-considerations}


* Cloud Manager では、SSL 証明書や秘密鍵は提供されません。これらは、サードパーティの証明機関から入手する必要があります。詳しくは、[SSL証明書の取得](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md)を参照してください。

* AEMは、セキュアな`https`サイトのみをサポートします。 複数のカスタムドメインがある場合、ドメインを追加するたびに証明書をアップロードしたくはありません。したがって、複数のドメインを持つ 1 つの証明書を取得することで、顧客にはメリットが得られます。

Cloud Manager では、次の顧客向け SSL 証明書の要件をサポートしています。

* SSL 証明書は複数の環境で使用できます。つまり、1 回追加すれば複数回使用できます。
* 各 Cloud Manager 環境は、複数の証明書を使用できます。
* 秘密鍵は、複数の SSL 証明書を発行する場合があります。
* 通常、各証明書には複数のドメインが含まれます。 
* プラットフォーム TLS サービスは、終了に使用された SSL 証明書と、そのドメインをホストする CDN サービスに基づいて、リクエストを顧客の CDN サービスにルーティングします。

権限を持つユーザーは、Cloud Manager UI SSL 証明書ページを使用して、次のようなタスクを実行してプログラムの SSL 証明書を管理できます。

* [SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [SSL証明書の表示、更新または置換](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
   >[!NOTE]
   >これらの操作により、表示の詳細や、期限切れになる証明書の置き換えが可能になります。
* [SSL 証明書の削除](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)