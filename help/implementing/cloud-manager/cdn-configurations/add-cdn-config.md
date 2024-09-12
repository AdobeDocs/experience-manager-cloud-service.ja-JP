---
title: CDN 設定の追加
description: Edge Delivery サイトまたはCloud Manager環境用の CDN 設定を追加する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: 70f99cfb2cd00278d9ebbb7972ef455af7a87a1b
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 6%

---


# CDN 設定の追加 {#add-cdn}

プログラム内でAdobeが管理する CDN の SSL 証明書にドメインをリンクするには、CDN （コンテンツ配信ネットワーク）設定を追加する必要があります。

Adobeが管理する CDN の場合、DV 証明書を使用する場合、ACME 検証が有効なサイトのみ許可されます。

>[!IMPORTANT]
>
>[ カスタムドメイン名を追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) と [SSL 証明書を追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) したことがありますか？ そうでない場合、CDN 設定を追加する前に、これら 2 つのタスクを完了する必要があります。

**CDN 設定を追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 左側のナビゲーションパネルの **サービス** の下の **CDN 設定** をクリックします。

1. CDN 設定ページの右上隅付近にある「**追加**」をクリックします。

   ![CDN を設定ダイアログボックス ](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

1. **CDN を設定** ダイアログボックスの **接触チャネル** ドロップダウンリストで、次のいずれかを選択します。

   | 接触チャネル | 説明 |
   | --- | --- |
   | Sites | Edge Delivery サイトを選択します。 |
   | 環境 | AEM設定内でターゲットとする特定のCloud Service環境を選択します。<br> 「**層**」ドロップダウンリストで、次のいずれかを選択します。<br>・ コンテンツがエンドユーザーに配信される、ライブの実稼動環境をターゲットにするには、**Publish** を選択します。<br>・変更を運用開始前にテストするステージング環境または非実稼動環境の場合は、「**プレビュー**」を選択します。 |

1. 次のいずれかを選択して、CDN タイプを選択します。

   | CDN タイプ | 説明 |
   | --- | --- |
   | アドビが管理する CDN | a. **ドメイン** ドロップダウンリストで、使用するドメイン名を選択します。<br> ドロップダウンリストに利用可能な検証済みドメインがありませんか？ [ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) を参照してください。<br>b.「SSL 証明書」ドロップダウンリストで、使用する証明書を選択します。<br> ドロップダウンリストに SSL 証明書は表示されませんか？ [SSL 証明書の追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) を参照してください。 |
   | その他の CDN プロバイダー。 | 使用可能なAdobe管理の CDN ではなく独自の CDN プロバイダーを使用している場合は、このオプションを選択します。<br> 「**ドメイン**」ドロップダウンリストで、使用するドメイン名を選択します。<br> ドロップダウンリストに使用可能な SSL 証明書がありませんか？ [ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) を参照してください。 |

1. 「**保存**」をクリックします。
