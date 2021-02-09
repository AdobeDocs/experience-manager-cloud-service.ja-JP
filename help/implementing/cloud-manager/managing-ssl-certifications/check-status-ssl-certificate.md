---
title: SSL 証明書のステータスの確認 - SSL 証明書の管理
description: SSL 証明書のステータスの確認 - SSL 証明書の管理
translation-type: tm+mt
source-git-commit: f426a9a653a3a3ae06abdbd2262e5d8f4beff277
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 87%

---


# SSL 証明書のステータスの確認 {#checking-status-an-ssl-certificate}

SSL証明書のステータスは、SSL証明書ページから一目で確認できます。

SSL 証明書のステータスは、次の配色で識別できます。

* **緑**：
証明書が今後 60 日以上有効であることを示します。

* **オレンジ**：
60日 以内に証明書の有効期限が切れることを示します。サイトへの不正アクセスやサイトの停止を回避するために、Cloud Manager UI で証明書を更新して置き換える計画を必ず立ててください。証明書の有効期限が間もなく切れることを警告する通知が Cloud Manager の UI に定期的に表示されます。

* **赤**：
再三の通知にもかかわらず、SSL 証明書の有効期限が切れたことを示します。