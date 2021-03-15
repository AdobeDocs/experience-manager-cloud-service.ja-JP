---
title: SSL 証明書のステータスの確認 - SSL 証明書の管理
description: SSL 証明書のステータスの確認 - SSL 証明書の管理
translation-type: tm+mt
source-git-commit: ddee11fdfa8cadfcd63472fd3c94cd8af555c856
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 69%

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

IP許可リスト、SSL証明書、またはカスタムドメイン名のCDN設定を含む環境を使用しているお客様の場合、**IP許可リスト**&#x200B;および&#x200B;**環境**&#x200B;の詳細ページで次のメッセージが表示されます。

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

>[!NOTE]
>既存の設定を表示および管理するには、次の図に示すように、UIを使用して追加する必要があります。

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)