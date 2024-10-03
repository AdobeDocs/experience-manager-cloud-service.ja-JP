---
title: CDN 設定の管理
description: Cloud Managerを使用して、Edge Delivery サイトまたはCloud Manager環境の CDN 設定を編集、更新、削除する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ff8c7fb21b4d8bcf395d28c194a7351281eef45b
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 15%

---


# CDN （コンテンツ配信ネットワーク）設定の管理 {#manage-cdn-configurations}

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
1. サイドパネルの「**サービス**」で、「![ ソーシャルネットワークアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg)**CDN 設定**」をクリックします。
1. **CDN 設定** テーブルで、更新する CDN 設定を持つ行の最後にある ![ 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

   ![CDN 設定の編集 ](/help/implementing/cloud-manager/assets/cdn-config-edit.png)

1. ドロップダウンメニューから、「**編集**」をクリックします。
1. **CDN 設定を編集** ダイアログボックスで、それぞれのドロップダウンリストに 1 つ以上のオプションを設定します。

   このダイアログボックスに表示されるオプションは、顧客が管理する CDN と、Adobeが管理する CDN のどちらを使用しているかによって異なる場合があります。

1. 「**更新**」をクリックします。

   編集した CDN のステータスは、「**CDN 設定**」テーブルで更新され、変更が反映されます。

<!-- ## ALTERNATE METHOD FOR EDITING A CDN CONFIGURATION from the Environments page
    
    The steps for adding a custom domain name from the **Environments** page are the same as when [adding a custom domain name from the Domain Settings page](#adding-cdn-settings), but the entry point differs. Follow these steps to add a custom domain name from the **Environments** page.
    
    1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate organization and program.
    
    1. Navigate to the **Environments Detail** detail page for the environment of interest.
    
       ![Entering domain name on the Environment Details page](/help/implementing/cloud-manager/assets/cdn/environments-cdn-config.png)
    
    1. Use the **Domain Names** table to submit the custom domain name.
    
       1. Enter the custom domain name.
       1. Select the SSL certificate associated with this name from the drop-down list.
       1. Click ![Add icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) **Add**.
    
       ![Add a custom domain name](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)
    
    1. The **Add domain name** dialog box opens to the **Domain Name** tab. Continue as you would for [adding a custom domain name from the Domain Settings page](#adding-cdn-settings). -->

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


