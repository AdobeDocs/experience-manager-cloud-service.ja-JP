---
title: カスタムドメイン名の管理
description: Cloud Manager を使用して、カスタムドメイン名を表示、更新、置換、削除する方法について説明します。
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 40a76e39750d6dbeb03c43c8b68cddaf515a2614
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 62%

---


# カスタムドメイン名の管理 {#managing-custom-domain-names}

Cloud Managerでは、カスタムドメイン名を編集、更新、置換、検証、削除できます。

## カスタムドメイン名の設定の編集 {#view-and-update}

AdobeCloud Managerでは、次の理由により、カスタムドメイン名の設定を変更する場合があります。

* **環境の切り替え**：コンテンツをエンドユーザー（パブリッシュ）に提供するか、内部ユーザー（オーサー）に提供するかに応じて、正しい設定を適用します。
* **セキュリティの更新**：セキュリティまたはコンプライアンスを強化するために、新しい SSL 証明書にアップグレードします。
* **デプロイメント戦略の変更**：適切な暗号化とサイトアクセスのために、正しい SSL 証明書が特定の環境に適用されることを確認します。

**カスタムドメイン名の設定を編集するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. ページの左上隅にある ![ アイコンを表示 ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左側のメニューを表示します。

1. **サービス**&#x200B;見出しの下にある「**CDN 設定**」をクリックします。

1. **CDN 設定**&#x200B;ページで、編集する CDN の行の末尾にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. 「**編集**」をクリックします。

1. **CDN 設定を編集** ダイアログボックスで、次の操作を行います。

   * **層**&#x200B;ドロップダウンリストで、使用する層（パブリッシュまたはプレビュー）を選択します。
   * **SSL 証明書** ドロップダウンリストで、使用する SSL 証明書を選択します。

1. 「**更新**」をクリックします。


## カスタムドメイン名の SSL 証明書の更新 {#update-cert}

上記と同じ手順に従って、カスタムドメイン名の SSL 証明書を更新します。

>[!NOTE]
>
>SSL 証明書が有効で、[既に設定されており](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)、更新するカスタムドメイン名を含んでいる必要があります。


## カスタムドメイン名の確認 {#verify-custom-domain-name}

[ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) も参照してください。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;画面から&#x200B;**ドメイン設定**&#x200B;ページに移動します。

1. 検証するカスタムドメイン名の行を見つけます。

1. 行の右端にある ![ その他アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. ドロップダウンメニューで、「**確認**」をクリックします。

1. **ドメインを検証**&#x200B;ダイアログボックスの&#x200B;**このドメインで使用する予定の証明書タイプは何ですか？**&#x200B;ドロップダウンリストで、次のオプションのいずれかを選択します。

   | 証明書タイプオプション | 説明 |
   | --- | --- |
   | Adobe管理（DV） SSL 証明書 | DV（ドメイン検証）証明書を使用する場合は、この証明書タイプを選択します。このオプションは、ほとんどの場合に最適で、基本的なドメイン検証を提供します。証明書は、アドビによって管理され、自動的に更新されます。 |
   | 顧客管理（OV/EV） SSL 証明書 | EV/OV SSL 証明書を使用してドメインを保護する場合は、この証明書タイプを選択します。 このオプションは、OV （組織検証）または EV （拡張検証）によるセキュリティの強化を提供します。 より厳しい検証、より高い信頼レベル、証明書に対するカスタム管理のいずれかが必要な場合に使用します。 |

1. **ドメインを検証**&#x200B;ダイアログボックスで、選択した証明書タイプに応じて、次のいずれかを行います。

   | 選択した証明書タイプ | 説明 |
   | --- | ---  |
   | アドビが管理する証明書 | a. [Adobeが管理する証明書の手順 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-steps) を実行します。 **ドメインの検証** ダイアログボックスの手順を完了したら、「**検証**」をクリックします。<ul><li>DNS の生成遅延が原因で、DNS 検証の処理に数時間かかる場合があります。</li><li>Cloud Managerは最終的にドメイン名の所有権を確認し、「**ドメイン設定**」テーブルのステータスを更新します。 詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。</li>![ ドメインステータスの検証 ](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b. [Adobe管理（DV） SSL 証明書を追加する ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-adobe-managed-ssl-cert) 準備が整いました。</li></ul> |
   | 顧客が管理する証明書 | a. 「**OK**」をクリックします。<br>b.これで、[ 顧客管理（OV/EV） SSL 証明書を追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-customer-managed-ssl-cert) する準備が整いました。<br> 証明書を追加すると、ドメイン名は **ドメイン設定** テーブルで検証済みとマークされます。 詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。</li></ul><br>![顧客が管理する EV/OV 証明書のドメイン検証](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |


## 関連するすべての環境からカスタムドメイン名の削除 {#deleting}

**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーが、Cloud Manager を使用してカスタムドメイン名を削除できます。

### 関連するすべての環境からカスタムドメイン名の削除 {#delete-cdn-all}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;画面から&#x200B;**ドメイン設定**&#x200B;ページに移動します。

1. 削除するカスタムドメイン名の行を特定します。

1. 行の右端にある ![ その他アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. 「**削除**」を選択します。

1. 送信を確認します。


### 特定の環境からカスタムドメイン名の削除 {#delete-cdn-specific}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;ページの&#x200B;**環境**&#x200B;画面に移動します。

1. **環境**&#x200B;ページから、対象となる環境の詳細画面に移動します。

1. ドメイン名のテーブルで、削除するカスタムドメイン名の行を見つけます。

1. 行の右端にある ![ その他アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. 「**削除**」を選択します。

1. 送信を確認します。
