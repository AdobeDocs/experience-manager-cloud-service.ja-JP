---
title: SSL証明書の取得 — SSL証明書の管理
description: SSL証明書の取得 — SSL証明書の管理
translation-type: tm+mt
source-git-commit: e27e5302802e68dce2a5713626950896bb35420a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# SSL証明書の取得 {#getting-an-ssl-certificate}

企業はSSL証明書を使用してWebサイトを保護し、顧客の信頼を確保します。 SSLプロトコルを使用するには、WebサーバーでSSL証明書を使用する必要があります。 Cloud Managerでは、SSL証明書や秘密鍵は提供されません。 これらは、証明機関(CA)から取得する必要があります。

エンティティが認証局(CA)から証明書を要求すると、CAは検証プロセスを完了します。 ドメイン名の制御の検証から、会社登録ドキュメントや加入者契約の収集まで、様々な種類が考えられます。

エンティティの情報が検証されると、CAはCAの秘密鍵を使用して公開鍵に署名します。 主要な認証機関はすべてWebブラウザーでルート証明書を持つので、エンティティの証明書は信頼 *チェーンを介してリンクされ* 、Webブラウザーはそれを信頼済み証明書と認識します。

