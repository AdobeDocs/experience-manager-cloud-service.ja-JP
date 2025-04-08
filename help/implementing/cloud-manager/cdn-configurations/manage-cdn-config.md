---
title: ドメインマッピングの管理
description: Cloud Manager を使用して、Edge Delivery サイトまたは Cloud Manager 環境の CDN 設定を編集、更新、または削除する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: a764a9d1e7d9fcd0be6abf9e2fb409346dc0f549
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 77%

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


## 運用開始準備：カスタムドメインの DNS 設定の指定 {#go-live-readiness}

カスタムドメインがトラフィックを提供する前に、DNS プロバイダーとの DNS 設定を完了する必要があります。 ドメインマッピングをデプロイして **運用開始** をクリックすると、Cloud Managerにダイアログボックスが表示され、DNS レコードのセットアッププロセスを順を追って実行できます。 CNAME レコードタイプまたは A レコードタイプを追加して、実稼動環境に移行するオプションがあります。

<!-- See also [APEX record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record#adobe-managed-cert-apex-record) and [CNAME record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record). -->

**運用開始準備を設定するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。
1. 左側のサイドメニューの&#x200B;**サービス**&#x200B;で、![ソーシャルネットワークアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg)「**ドメインマッピング**」をクリックします。
1. ドメインマッピング テーブルで、設定する運用開始準備を持つ CDN に対応する行の末尾付近にある「**運用開始**」をクリックします。

   ![ 運用開始準備ダイアログボックス ](/help/implementing/cloud-manager/assets/domain-mappings-go-live-readiness.png)

1. **運用開始準備** ダイアログボックスで、次のいずれかの操作を行います。

   | オプション | ステップ |
   | --- | --- |
   | A レコードを設定 | `example.com`<br> などのルートドメインに推奨<ol><li>DNS サービス・プロバイダのポータルにログインします。<li>DNS レコードセクションに移動します。<li>リストされているすべての IP アドレスを指すように A レコードを作成します。</li></ol> |
   | CNAME を設定 | `www.example.com`<br> などのカスタムドメインにお勧め<ol><li>DMS サービス プロバイダのポータルにログインします。<li>DNS レコードセクションに移動します。<li>DNS サービスプロバイダー（カスタムドメイン）の DNS レコードに `cdn.adobeaemcloud.com` （CNAME レコード）をマッピングします。 このマッピングにより、カスタムドメインで受信したリクエストがアドビの CDN にリダイレクトされるようになります。</li></ol> |

1. **運用開始準備** ダイアログボックスで、「**OK**」をクリックしてレコードを保存します。

   DNS の伝達を待ちます。数分から数時間かかる場合があります。

   ドメインマッピングテーブルの **[!UICONTROL ステータス]** 列が **[!UICONTROL 検証済み]** に更新されると、カスタムドメインを使用する準備が整います。 ![ 更新アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) をクリックして、ステータスを更新する必要がある場合があります。

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
