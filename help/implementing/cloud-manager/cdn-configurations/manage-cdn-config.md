---
title: ドメインマッピングの管理
description: Cloud Manager を使用して、Edge Delivery サイトまたは Cloud Manager 環境の CDN 設定を編集、更新、または削除する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: 41155a724f48ad28a12aac615a3e9a13bb3afa26
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 100%

---

# ドメインマッピングの管理 {#manage-cdn-configurations}

Cloud Manager を使用して、Edge Delivery サイトまたは Cloud Manager 環境の CDN 設定を編集または削除する方法について説明します。

## ドメインマッピングページからの CDN 設定の編集 {#edit-cdn}

Adobe Cloud Manager では、いくつかの理由により、環境層（パブリッシュまたはプレビュー）や SSL 証明書を含む CDN（コンテンツ配信ネットワーク）設定を編集する必要がある場合があります。

* **環境の変更**：層を調整すると、実稼動（公開）またはテスト（プレビュー）用に、CDN 設定を適切な環境と一致させることができます。
* **セキュリティの強化**：証明書を更新する場合やコンプライアンスまたはセキュリティのニーズに対応する場合は、別の SSL 証明書の選択が必要になる場合があります。
* **パフォーマンスの最適化**：設定を編集すると、変化する運用ニーズに基づいてコンテンツを配信する正しい CDN 設定が確保されます。

既存の設定を完全に削除せずに、設定を編集できます。変更は、ステージング環境や実稼動環境など、選択した環境に適用され、コンテンツの配信方法やセキュリティ保護方法に影響を与える可能性があります。

このタスクを完了するには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つメンバーである必要があります。

**ドメインマッピングページから CDN 設定を編集するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。
1. 左側のサイドメニューの&#x200B;**サービス**&#x200B;で、![ソーシャルネットワークアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg)「**ドメインマッピング**」をクリックします。
1. **ドメインマッピング**&#x200B;テーブルで、CDN 設定を更新する行の末尾にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. ドロップダウンメニューで、「**編集**」をクリックします。

1. **CDN 設定を編集**&#x200B;ダイアログボックスで、それぞれのドロップダウンリストのオプションを 1 つ以上設定します。

   ダイアログボックスに表示されるオプションは、**アドビが管理する CDN** を使用しているか、**その他の CDN プロバイダー**（顧客が管理する CDN）を使用しているかによって異なります。

1. 「**更新**」をクリックします。

   編集した CDN のステータスは、**ドメインマッピング**&#x200B;テーブルで更新され、行った変更が反映されます。


## 環境ページからの CDN 設定の編集

**環境**&#x200B;ページから CDN 設定を編集する手順は、[ドメインマッピングページから CDN 設定を編集](#edit-cdn)する場合とほとんど同じですが、エントリポイントが異なります。

**環境ページから CDN 設定を編集するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 左側のサイドメニューで、![データアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg)「**環境**」をクリックします。

1. **環境**&#x200B;ページで、対象となる環境を選択します。

1. 環境の詳細ページのドメインマッピンググループで、編集する CDN 設定に対応する ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. ポップアップメニューで、「**編集**」をクリックします。

1. **CDN 設定を編集**&#x200B;ダイアログボックスで、それぞれのドロップダウンリストのオプションを 1 つ以上設定します。

   ダイアログボックスに表示されるオプションは、**アドビが管理する CDN** を使用しているか、**その他の CDN プロバイダー**（顧客が管理する CDN）を使用しているかによって異なります。

1. 「**更新**」をクリックします。

<!-- 
## Go live readiness: Configure DNS settings for a custom domain {#go-live-readiness} 

Before a custom domain can serve traffic in Adobe Cloud Manager, you must complete DNS configuration with your DNS provider. After deploying a domain mapping and clicking **Go live**, Cloud Manager displays a dialog box that guides you through the DNS record setup process. You have the option to go live by adding either a CNAME record type or an A record type representing Fastly's IPs, simplifying domain routing. This ability eliminates the restriction of relying solely on CNAME records for domain setup with Fastly.

MAYBE There is support for A record types to improve Go Live readiness for domains using CDN configurations in AEM Cloud Manager. MAYBE

See also [APEX record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record#adobe-managed-cert-apex-record) and [CNAME record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record).

**To configure Go live readiness:**

1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate organization and program.

1. In the left side menu, under **Services**, click ![Social network icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Domain Mappings**.

1. In the Domain Mappings table, click **Go live** near the end of a row that corresponds to a CDN whose Go Live readiness you want to configure. 

1. In the Go live readiness dialog box, do one of the following:

    | Configure  | Steps |
    | --- | --- |
    | A RECORD | Recommended for root domains like `example.com`<br><ol><li>Log in to your DNS service provider's portal.<li>Go to the DNS Records section.<li>Create an A record to point to all the listed IP addresses.<li>In the Go live readiness dialog box, click **OK**.<li>In the Domain Mappings table, under the **Status** column, click ![Refresh icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg).<br>The status is updated to **Verified** when the resolution is complete.</li></ol> |
    | CNAME | Recommended for custom domains like `www.example.com`<br><ol><li>Log in to your DMS service provider's portal.<li>Go to the DNS Records section.<li>Map [cdn.adobeaemcloud.com](http://cdn.adobeaemcloud.com/) (CNAME record) in the DNS record of the DNS service provider (your custom domain). This mapping ensures that requests received at the custom domain are redirected to Adobe's CDN.<li>In the **Go live readiness** dialog box, click **OK** to save the record.<br>Wait for DNS propogation (may take several minutes to a few hours). When the **[!UICONTROL Status]** column in the Domamin Mappings table updates to **[!UICONTROL Verified]**, the custom domain is ready to use. You may need to click ![Refresh icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) to refresh the status.</li></ol> | 
    
-->

## CDN 設定の削除 {#delete-cdn}

Cloud Manager でアドビが管理する CDN または顧客が管理する CDN の設定を削除する際、関連付けられているドメインのルーティングと SSL 証明書の設定が削除されます。ドメインはトラフィック配信に CDN を使用しなくなり、CDN で提供されるセキュリティやパフォーマンスの拡張機能は失われます。削除された CDN の再追加や新しい CDN の追加など、新しい設定を行うまでサービスが中断される可能性があります。

このタスクを完了するには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つメンバーである必要があります。

**CDN 設定を削除するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 左側のサイドメニューの&#x200B;**サービス**&#x200B;で、![ソーシャルネットワークアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg)「**ドメインマッピング**」をクリックします。

1. ドメインマッピングテーブルで、削除する CDN に対応する行の末尾にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックし、「**削除**」をクリックします。

1. **CDN 設定を削除**&#x200B;ダイアログボックスで、「**削除**」をクリックします。

1. 「**削除**」をもう一度クリックして、サイトの CDN の削除を確認します。


## 環境ページからの CDN 設定の削除

**環境**&#x200B;ページから CDN 設定を削除する手順は、[ドメインマッピングページから CDN 設定を削除](#edit-cdn)する場合とほとんど同じですが、エントリポイントが異なります。

**環境ページから CDN 設定を削除するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 左側のサイドメニューで、![データアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg)「**環境**」をクリックします。

1. **環境**&#x200B;ページで、対象となる環境を選択します。

1. 環境の詳細ページの **ドメインマッピング**&#x200B;グループで、削除する CDN 設定に対応する ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックし、「**削除**」をクリックします。

1. **CDN 設定を削除**&#x200B;ダイアログボックスで、「**削除**」をクリックします。

1. 「**削除**」をもう一度クリックして、サイトの CDN の削除を確認します。
