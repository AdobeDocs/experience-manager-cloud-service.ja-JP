---
title: SSL証明書のステータスの確認 — SSL証明書の管理
description: SSL証明書のステータスの確認 — SSL証明書の管理
translation-type: tm+mt
source-git-commit: f426a9a653a3a3ae06abdbd2262e5d8f4beff277
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# SSL証明書のステータスの確認{#checking-status-an-ssl-certificate}

SSL証明書のステータスは、SSL証明書ページから一目で確認できます。

SSL証明書のステータスは、次のカラースキームで確認できます。

* ****
Green証明書が、今後60日以上有効であることを示します。

* **Orange**
Orange 60日以内に証明書の有効期限が切れることを示します。サイトへのアクセスや障害を回避するために、必ず証明書を更新し、Cloud Manager UIで証明書を置き換える予定です。 Cloud Managerは、証明書の有効期限が間もなく切れたことを警告する通知をUIで通知します。

* ****
Red複数の通知にもかかわらず、SSL証明書の有効期限が切れたことを示します。