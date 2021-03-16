---
title: SSL 証明書のステータスの確認 - SSL 証明書の管理
description: SSL 証明書のステータスの確認 - SSL 証明書の管理
translation-type: tm+mt
source-git-commit: 46004eb1925533545605a09f62bbd0e7945227e0
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 58%

---


# SSL 証明書のステータスの確認 {#checking-status-an-ssl-certificate}

SSL 証明書のステータスは、SSL 証明書ページから一目で確認できます。

SSL 証明書のステータスは、次の配色で識別できます。

* **緑**：
証明書が今後 60 日以上有効であることを示します。

* **オレンジ**：
60日 以内に証明書の有効期限が切れることを示します。サイトへの不正アクセスやサイトの停止を回避するために、Cloud Manager UI で証明書を更新して置き換える計画を必ず立ててください。証明書の有効期限が間もなく切れることを警告する通知が Cloud Manager の UI に定期的に表示されます。

* **赤**：
再三の通知にもかかわらず、SSL 証明書の有効期限が切れたことを示します。

## IP許可リストの既存のCDN設定{#pre-existing-cdn}

IP許可リスト、SSL証明書、またはカスタムドメイン名のCDN設定を含む環境を使用しているお客様の場合、**IP許可リスト**&#x200B;および&#x200B;**環境**&#x200B;の詳細ページで次のメッセージが表示されます。 UIに表示されるメッセージは、お客様がUIを介して既存の環境設定をすべて移行した後、消えます。メッセージが消えるまでに1 ～ 2営業日かかる場合があります。

>[!NOTE]
>既存の設定を表示および管理するには、UIから追加する必要があります。 詳しくは、[SSL証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)を参照してください。

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)