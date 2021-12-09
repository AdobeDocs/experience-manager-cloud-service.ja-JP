---
title: SSL 証明書のステータスの確認 - SSL 証明書の管理
description: SSL 証明書のステータスの確認 - SSL 証明書の管理
exl-id: 59d81356-2fa9-43db-bfa5-c2896c530eaa
source-git-commit: 828490e12d99bc8f4aefa0b41a886f86fee920b4
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 98%

---

# SSL 証明書のステータスの確認 {#checking-status-an-ssl-certificate}

SSL 証明書のステータスは、SSL 証明書ページから一目で確認できます。

SSL 証明書のステータスは、次の配色で識別できます。

* **緑**：
証明書が今後 60 日以上有効であることを示します。

* **オレンジ**：
60 日以内に証明書の有効期限が切れることを示します。サイトへの不正アクセスやサイトの停止を回避するために、Cloud Manager UI で証明書を更新して置き換える計画を必ず立ててください。証明書の有効期限が間もなく切れることを警告する通知が Cloud Manager の UI に定期的に表示されます。

* **赤**：
再三の通知にもかかわらず、SSL 証明書の有効期限が切れたことを示します。

## 既存の CDN 設定 {#pre-existing-cdn}

IP 許可リスト、SSL 証明書、カスタムドメイン名のいずれかについて CDN 設定が既に存在している環境のユーザーの場合、**IP 許可リスト**&#x200B;および&#x200B;**環境**&#x200B;の詳細ページに以下のメッセージが表示されます。UI に表示されるメッセージは、顧客が UI から既存の環境設定をすべて移行した後に消えます。メッセージが消えるまでに 1～2 営業日かかる場合があります。

>[!NOTE]
>既存の設定を表示および管理するには、UI を使用して追加する必要があります。詳しくは、「[SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)」を参照してください。

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
