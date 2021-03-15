---
title: ドメイン名ステータスの確認
description: ドメイン名ステータスの確認
translation-type: tm+mt
source-git-commit: 40a0380c6d149d8565dd41a7f48858383c22c5c0
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 59%

---


# ドメイン名ステータスの確認 {#check-status}

ドメイン名が正常に検証されたかどうかを確認するには、ドメイン設定ページの「環境」の表にあるドメイン名ステータスアイコンをクリックします。

>[!NOTE]
>Cloud Manager では、カスタムドメイン追加ウィザードの検証手順で「保存」を選択すると、TXT 検証が自動的にトリガーされます。それ以降の検証では、ステータスの横にある&#x200B;**再検証**&#x200B;アイコンをアクティブに選択する必要があります。

Cloud Manager は、TXT 値を使用してドメインの所有権を検証し、次のいずれかのステータスメッセージを表示します。

* **ドメイン検証失敗**
TXT 値が見つからないか、エラーが検出されました。手順に従って、再試行します。準備が整ったら、 
*ステータスの横* にある「再検証」アイコンをクリックします。

* **ドメイン検証中**
検証が進行中です。このステータスは、通常、 
*ステータスの横* にある「再検証」アイコンをクリックします。

* **検証済み、デプロイメント失敗**
TXT の検証に成功しました。ただし、CDN のデプロイメントは失敗しました。Adobe の担当者に自動的に通知が送信されます。

* **ドメインが検証済みでデプロイ済み**
このステータスは、カスタムドメイン名が使用できる状態であることを示します。
   >[!NOTE]
   >この時点で、カスタムドメイン名をテスト用に準備し、Cloud Managerのドメイン名を指し示すことができます。 詳しくは、[DNS設定の構成](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)を参照してください。

* **削除**
カスタムドメイン名の削除を実行中です。

* **削除失敗**
カスタムドメイン名の削除に失敗しました。再試行する必要があります。詳しくは、[カスタムドメイン名の削除](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)を参照してください。


## IP許可リストの既存のCDN設定{#pre-existing-cdn}

IP許可リストのCDN設定（SSL証明書またはカスタムドメイン名）が既に存在する環境を使用しているお客様の場合、**IP許可リスト**&#x200B;および&#x200B;**環境**&#x200B;の詳細ページで次のメッセージが表示されます。

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

既存の設定を表示および管理するには、UIから追加する必要があります。
![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)
