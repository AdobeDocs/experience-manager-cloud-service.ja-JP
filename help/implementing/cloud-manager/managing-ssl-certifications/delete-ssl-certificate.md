---
title: SSL 証明書の削除 - SSL 証明書の管理
description: SSL 証明書の削除 - SSL 証明書の管理
exl-id: 43f66871-cca4-4709-95d0-68aa715c0da2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '168'
ht-degree: 100%

---

# SSL 証明書の削除 {#deleting-an-ssl-certificate}

>[!IMPORTANT]
>Cloud Manager からの証明書の削除は、元に戻すことができない恒久的な操作です。ベストプラクティスとしては、必要な SSL ファイルをローカルに保存してから、Cloud Manager ユーザーインターフェイスでそれらのファイルを削除することをお勧めします。

Cloud Manager で SSL 証明書を削除するには、ユーザーがビジネスオーナーまたはデプロイメントマネージャーの役割を持っている必要があります。Cloud Manager では、1 つ以上のドメインが関連付けられている SSL 証明書を削除できません。SSL 証明書を削除する前に、関連付けられているドメインをすべて削除する必要があります。詳しくは、「[カスタムドメイン名の削除](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)」を参照してください。

SSL 証明書を削除するには、次の手順に従います。

1. **環境**&#x200B;ページから **SSL 証明書**画面に移動します。
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
1. 削除する SSL 証明書名が表示されている行を見つけます。
1. 行の右端から **...** メニューを選択します。
1. 「**削除**」を選択します。
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete01.png)
1. **SSL 証明書の削除**&#x200B;ダイアログボックスから送信を確認します。
