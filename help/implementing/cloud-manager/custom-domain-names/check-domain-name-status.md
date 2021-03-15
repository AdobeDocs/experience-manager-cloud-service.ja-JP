---
title: ドメイン名ステータスの確認
description: ドメイン名ステータスの確認
translation-type: tm+mt
source-git-commit: c6fe5e9dab0e119271c6cea272dddabe7babb1e4
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 71%

---


# ドメイン名ステータスの確認 {#check-status}

ドメイン名が正常に検証されたかどうかを確認するには、ドメイン設定ページの「環境」の表にあるドメイン名ステータスアイコンをクリックします。

>[!NOTE]
>Cloud Manager では、カスタムドメイン追加ウィザードの検証手順で「保存」を選択すると、TXT 検証が自動的にトリガーされます。それ以降の検証では、ステータスの横にある&#x200B;**再検証**&#x200B;アイコンをアクティブに選択する必要があります。

Cloud Manager は、TXT 値を使用してドメインの所有権を検証し、次のいずれかのステータスメッセージを表示します。

* **ドメイン検証失敗**
TXT 値が見つからないか、エラーが検出されました。手順に従って、再試行します。準備が整ったら、 
ステータスの横にある&#x200B;*再検証*&#x200B;アイコンを選択します。

* **ドメイン検証中**
検証が進行中です。このステータスは、通常、 
ステータスの横にある&#x200B;*再検証*&#x200B;アイコンを選択します。

* **検証済み、デプロイメント失敗**
TXT の検証に成功しました。ただし、CDN のデプロイメントは失敗しました。Adobe の担当者に自動的に通知が送信されます。

* **ドメインが検証済みでデプロイ済み**
このステータスは、カスタムドメイン名が使用できる状態であることを示します。
   >[!NOTE]
   >この時点で、カスタムドメイン名はテストの準備ができており、Cloud Manager のドメイン名を指すようになっています。詳細については、「[DNS 設定の指定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)」を参照してください。

* **削除**
カスタムドメイン名の削除を実行中です。

* **削除失敗**
カスタムドメイン名の削除に失敗しました。再試行する必要があります。詳しくは、「[カスタムドメイン名の削除](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)」を参照してください。


## IP許可リストの既存のCDN設定{#pre-existing-cdn}

IP許可リスト、SSL証明書、またはカスタムドメイン名のCDN設定を含む環境を使用しているお客様の場合、**IP許可リスト**&#x200B;および&#x200B;**環境**&#x200B;の詳細ページで次のメッセージが表示されます。 UIに表示されるメッセージは、お客様がUIを介して既存の環境設定をすべて移行した後、消えます。メッセージが消えるまでに1 ～ 2営業日かかる場合があります。

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

>[!NOTE]
>既存の設定を表示および管理するには、次の図に示すように、UIを使用して追加する必要があります。

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)
