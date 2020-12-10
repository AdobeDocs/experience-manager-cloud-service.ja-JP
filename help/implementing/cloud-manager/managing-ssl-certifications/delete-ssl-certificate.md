---
title: SSL証明書の削除 — SSL証明書の管理
description: SSL証明書の削除 — SSL証明書の管理
translation-type: tm+mt
source-git-commit: 99eb33c3c42094f787d853871aee3a3607856316
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# SSL証明書の削除{#deleting-an-ssl-certificate}

>[!IMPORTANT]
>証明書のCloud Managerからの削除は、元に戻すことができない永久的な操作です。 ベストプラクティスは、必要なSSLファイルをローカルに保存してから、Cloud Managerユーザーインターフェイスで削除することです。

Cloud ManagerでSSL証明書を削除するには、ユーザーがビジネス所有者またはDeployment Managerのロールに属している必要があります。 1つ以上のドメインが関連付けられているSSL証明書は、Cloud Managerでは削除できません。  SSL証明書を削除する前に、関連付けられているドメインをすべて削除する必要があります。 詳しくは、[カスタムドメイン名の削除](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)を参照してください。

SSL証明書を削除するには、次の手順に従います。

1. **環境**&#x200B;ページから&#x200B;**SSL証明書**画面に移動します。
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
1. 削除するSSL証明書名が一覧表示されている行を識別します。
1. **を選択…**&#x200B;メニューを表示します。
1. 「**削除**」を選択します。
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete01.png)
1. **SSL証明書の削除**&#x200B;ダイアログボックスから送信を確認します。
