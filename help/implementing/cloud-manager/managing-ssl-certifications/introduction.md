---
title: 概要 — SSL証明書の管理
description: 概要 — SSL証明書の管理
translation-type: tm+mt
source-git-commit: 99eb33c3c42094f787d853871aee3a3607856316
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---


# 概要 {#introduction}

Cloud Managerでは、セルフサービス機能を使用して、Cloud Manager UIからSSL証明書をインストールできます。 Cloud Managerは、SSL証明書と、お客様が所有する秘密鍵を管理するプラットフォームTLSサービスを使用します。通常は、サードパーティの証明機関（例：「Let’s Encrypt」）から取得します。

## 重要な検討事項 {#important-considerations}


* Cloud Managerでは、SSL証明書や秘密鍵は提供されません。 これらは、第三者の証明機関から入手する必要があります。 詳しくは、[SSL証明書の取得](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md)を参照してください。

* AEMは、セキュアな`https`サイトのみをサポートします。 複数のカスタムドメインを持つ顧客は、ドメインを追加するたびに証明書をアップロードする必要はありません。 したがって、複数のドメインを持つ1つの証明書を取得することで、このような顧客のメリットが得られます。

Cloud Managerでは、次のお客様向けSSL証明書の要件をサポートしています。

* SSL証明書は複数の環境が使用できます。つまり、1回追加して複数回使用します。
* 各Cloud Manager環境は、複数の証明書を使用できます。
* 秘密鍵は、複数のSSL証明書を発行する場合があります。
* 通常、各証明書には複数のドメインが含まれます。
* プラットフォームTLSサービスは、終了に使用されたSSL証明書と、そのドメインをホストするCDNサービスに基づいて、要求を顧客のCDNサービスにルーティングします。

権限を持つユーザーは、Cloud Manager UI SSL証明書ページを使用して、次のようなタスクを実行してプログラムのSSL証明書を管理できます。

* [SSL証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [SSL証明書の表示、更新または置換](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
   >[!NOTE]
   >これらの操作により、表示の詳細や、期限切れになる証明書の置き換えが可能になります。
* [SSL証明書の削除](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)