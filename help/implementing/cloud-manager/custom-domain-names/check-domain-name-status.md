---
title: ドメイン名の状態の確認
description: ドメイン名の状態の確認
translation-type: tm+mt
source-git-commit: f11cb3b56f51046779300626d1deb037dd687309
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# ドメイン名の状態を確認中{#check-status}

ドメイン名が正常に検証されたかどうかを確認するには、ドメイン設定ページの環境の表にあるドメイン名のステータスアイコンをクリックします。

>[!NOTE]
>Cloud Managerでは、カスタムドメインウィザードの検証手順で「保存」を選択すると、TXT追加検証が自動的にトリガーされます。 それ以降の検証では、ステータスの横にある&#x200B;**再検証**&#x200B;アイコンをアクティブに選択する必要があります。

Cloud Managerは、TXT値を使用してドメインの所有権を検証し、次のいずれかのステータスメッセージを表示します。

* **ドメイン検証**
失敗TXT値が見つからないか、エラーが検出されました。手順に従って、再試行します。 準備が整ったら、 
*ステータスの横* にある「再検証」アイコンをクリックします。

* **ドメインの検証中**
ProgressVerificationが進行中です。このステータスは、通常、 
*ステータスの横* にある「再検証」アイコンをクリックします。

* **検証済み、展開**
失敗TXTの検証に成功しました。ただし、CDNのデプロイメントは失敗しました。 Adobe担当者に自動的に通知が送信されます。

* **ドメインが検証済みで**
デプロイ済みこのステータスは、カスタムドメイン名が使用できる状態であることを示します。
   >[!NOTE]
   >この時点で、カスタムドメイン名をテスト用に準備し、Cloud Managerのドメイン名を指し示すことができます。 詳しくは、[DNS設定の構成](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)を参照してください。

* **カスタムドメイン名の**
削除を実行中です。

* **カスタムドメイン名の削除**
に失敗しました。再試行する必要があります。 詳しくは、[カスタムドメイン名の削除](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)を参照してください。

