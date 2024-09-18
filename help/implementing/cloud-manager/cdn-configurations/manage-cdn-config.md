---
title: CDN 設定の管理
description: Cloud Managerを使用して、Edge Delivery サイトまたはCloud Manager環境の CDN 設定を編集、更新、削除する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8e2fc0d4ee82e79d1a822a528b1a46acce3c192a
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 15%

---


# CDN 設定の管理 {#manage-cdn-configurations}

Cloud Managerを使用して、Edge Delivery サイトまたはCloud Manager環境の CDN 設定を編集、更新、削除する方法について説明します。

## CDN 設定の編集 {#edit-cdn}

Cloud ManagerのAdobeでは、いくつかの理由で、環境層（Publishまたはプレビュー）や SSL 証明書を含む CDN 設定を編集する必要がある場合があります。

* **環境の変更**：層を調整すると、実稼動（Publish）またはテスト（プレビュー）用に、CDN 設定を正しい環境と一致させることができます。
* **セキュリティの強化**：証明書を更新する場合や、コンプライアンスやセキュリティのニーズに対応する場合は、別の SSL 証明書の選択が必要になる場合があります。
* **パフォーマンスの最適化**：設定を編集すると、運用ニーズの変化に基づいて、コンテンツを配信するための正しい CDN 設定が保証されます。

既存の設定を完全に削除せずに、設定を編集できます。 変更は、選択した環境（ステージングや実稼動など）に適用され、コンテンツの配信およびセキュリティ保護の方法に影響を与える可能性があります。

このタスクを完了するには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つメンバーである必要があります。

**CDN 設定を編集するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。
1. 左側のナビゲーションパネルの **サービス** の下の **CDN 設定** をクリックします。
1. **CDN 設定** テーブルで、CDN 設定を編集する行の最後にある省略記号をクリックします。

   ![CDN 設定の編集 ](/help/implementing/cloud-manager/assets/cdn-config-edit.png)

1. 「**編集**」をクリックします。
1. **CDN 設定を編集** ダイアログボックスで、それぞれのドロップダウンリストに 1 つ以上のオプションを設定します。

   このダイアログボックスに表示されるオプションは、顧客が管理する CDN と、Adobeが管理する CDN のどちらを使用しているかによって異なる場合があります。

1. 「**更新**」をクリックします。

   編集した CDN のステータスは、「**CDN 設定**」テーブルで更新され、変更が反映されます。

## CDN 設定の削除 {#delete-cdn}

AdobeCloud ManagerでAdobe管理または顧客管理の CDN 設定を削除すると、関連するドメインのルーティングと SSL 証明書の設定が削除されます。 ドメインではトラフィック配信に CDN を使用しなくなり、CDN で提供されるセキュリティやパフォーマンスの強化は失われます。 削除した CDN の再追加や新しい CDN の追加など、新しい設定がセットアップされるまで、サービスが中断される場合があります。

このタスクを完了するには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つメンバーである必要があります。

**CDN 設定を削除するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 左側のナビゲーションパネルの **サービス** の下の **CDN 設定** をクリックします。

1. CDN 設定テーブルで、CDN を削除する行の最後にある省略記号をクリックします。

   ![CDN 設定の削除 ](/help/implementing/cloud-manager/assets/cdn-config-delete.png)

1. 「**削除**」をクリックします。
1. もう一度 **削除** をクリックして、サイトの CDN の削除を確認します。


