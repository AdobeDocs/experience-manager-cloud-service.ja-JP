---
title: カスタムドメイン名の管理
description: Cloud Manager を使用して、カスタムドメイン名を表示、更新、置換、削除する方法について説明します。
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1683d53491e06ebe2dfcc96184ce251539ecf732
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 96%

---


# カスタムドメイン名の管理 {#managing-custom-domain-names}

Cloud Manager では、カスタムドメイン名の編集、更新、置換、検証、削除を行うことができます。

## カスタムドメイン名の設定の編集 {#view-and-update}

Adobe Cloud Manager では、次の理由により、カスタムドメイン名の設定を編集する必要がある場合があります。

* **環境の切り替え**：コンテンツをエンドユーザー（パブリッシュ）に提供するか、内部ユーザー（オーサー）に提供するかに応じて、正しい設定を適用します。
* **セキュリティの更新**：セキュリティまたはコンプライアンスを強化するために、新しい SSL 証明書にアップグレードします。
* **デプロイメント戦略の変更**：暗号化とサイトアクセスを適切に行えるよう、正しい SSL 証明書が特定の環境に適用されていることを確認します。

**カスタムドメイン名の設定を編集するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左サイドメニューを表示します。

1. **サービス** 見出しの下の ![ ソーシャルネットワークアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg)**ドメインマッピング** をクリックします。

1. **ドメインマッピング** ページで、CDN を編集する行の最後にある ![ メニューアイコンを表示 ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. 「**編集**」をクリックします。

1. **CDN 設定を編集**&#x200B;ダイアログボックスで、次の操作を行います。

   * **階層**&#x200B;ドロップダウンリストで、使用する層（パブリッシュまたはプレビュー）を選択します。
   * **SSL 証明書**&#x200B;ドロップダウンリストで、使用する SSL 証明書を選択します。

1. 「**更新**」をクリックします。


## カスタムドメイン名の SSL 証明書の更新 {#update-cert}

上記と同じ手順に従って、カスタムドメイン名の SSL 証明書を更新します。

>[!NOTE]
>
>SSL 証明書が有効で、[既に設定されており](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)、更新するカスタムドメイン名を含んでいる必要があります。


## カスタムドメイン名の検証 {#verify-custom-domain-name}

[カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)も参照してください。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;画面から&#x200B;**ドメイン設定**&#x200B;ページに移動します。

1. 検証するカスタムドメイン名の行を特定します。

1. 行の右端にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. ドロップダウンメニューで、「**検証**」をクリックします。

1. **ドメインを検証**&#x200B;ダイアログボックスの&#x200B;**このドメインで使用する予定の証明書タイプは何ですか？**&#x200B;ドロップダウンリストで、次のオプションのいずれかを選択します。

   | 証明書タイプオプション | 説明 |
   | --- | --- |
   | アドビが管理する（DV）SSL 証明書 | DV（ドメイン検証）証明書を使用する場合は、この証明書タイプを選択します。このオプションは、ほとんどの場合に最適で、基本的なドメイン検証を提供します。証明書は、アドビによって管理され、自動的に更新されます。 |
   | 顧客が管理する（OV/EV）SSL 証明書 | EV/OV SSL 証明書を使用してドメインを保護する場合は、この証明書タイプを選択します。このオプションでは、OV（組織検証）または EV（拡張検証）でセキュリティが強化されます。より厳しい検証、より高い信頼レベル、証明書に対するカスタム管理のいずれかが必要な場合に使用します。 |

1. **ドメインを検証**&#x200B;ダイアログボックスで、選択した証明書タイプに応じて、次のいずれかを行います。

   | 選択した証明書タイプ | 説明 |
   | --- | ---  |
   | アドビが管理する証明書 | a. [アドビが管理する証明書の手順](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-steps)を完了します。**ドメインの検証**&#x200B;ダイアログボックスの手順を完了したら、「**検証**」をクリックします。<ul><li>DNS の生成遅延が原因で、DNS 検証の処理に数時間かかる場合があります。</li><li>Cloud Manager は最終的にドメイン名の所有権を確認し、**ドメイン設定**&#x200B;テーブルのステータスを更新します。詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。</li>![ドメインステータスの検証](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b. [アドビが管理する（DV）SSL 証明書を追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-adobe-managed-ssl-cert)する準備が整いました。</li></ul> |
   | 顧客が管理する証明書 | a. 「**OK**」をクリックします。<br>b. これで、[顧客が管理する（OV/EV）SSL 証明書を追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-customer-managed-ssl-cert)する準備が整いました。<br>証明書を追加すると、ドメイン名が&#x200B;**ドメイン設定**&#x200B;テーブルで検証済みとマークされます。詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。</li></ul><br>![顧客が管理する EV/OV 証明書のドメイン検証](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |


## 関連するすべての環境からカスタムドメイン名の削除 {#deleting}

**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーが、Cloud Manager を使用してカスタムドメイン名を削除できます。

### 関連するすべての環境からカスタムドメイン名の削除 {#delete-cdn-all}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;画面から&#x200B;**ドメイン設定**&#x200B;ページに移動します。

1. 削除するカスタムドメイン名の行を特定します。

1. 行の右端にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. 「**削除**」を選択します。

1. 送信を確認します。


### 特定の環境からカスタムドメイン名の削除 {#delete-cdn-specific}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;ページの&#x200B;**環境**&#x200B;画面に移動します。

1. **環境**&#x200B;ページから、対象となる環境の詳細画面に移動します。

1. ドメイン名のテーブルで、削除するカスタムドメイン名の行を見つけます。

1. 行の右端にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. 「**削除**」を選択します。

1. 送信を確認します。
