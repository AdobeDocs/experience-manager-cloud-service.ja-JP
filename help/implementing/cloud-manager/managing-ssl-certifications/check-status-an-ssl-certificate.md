---
title: SSL証明書のステータスの確認 — SSL証明書の管理
description: SSL証明書のステータスの確認 — SSL証明書の管理
translation-type: tm+mt
source-git-commit: 295519e8969daec256e5007357b179a30a7932ce
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# SSL証明書のステータスの確認 {#checking-status-an-ssl-certificate}

SSL証明書のステータスは、SSL証明書ページまたは環境の詳細ページから一目で確認できます。

SSL証明書のステータスは、次のカラースキームで確認できます。

* **緑**：証明書が少なくとも60日後に有効であることを示します。

* **Orange**：証明書の有効期限が60日未満であることを示します。 サイトへのアクセスや障害を回避するために、必ず証明書を更新し、Cloud Manager UIで証明書を置き換える予定です。 Cloud Managerは、証明書の有効期限が間もなく切れたことを警告する通知をUIで通知します。

* **赤色**：複数の通知があるにもかかわらず、SSL証明書の有効期限が切れたことを示します。