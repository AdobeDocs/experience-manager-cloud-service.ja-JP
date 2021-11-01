---
title: ドメイン名ステータスの確認
description: ドメイン名ステータスの確認
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: 4533cbc689d69cbe126791b4426123f890754507
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 98%

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
TXT の検証に成功しました。ただし、CDN のデプロイメントは失敗しました。担当のAdobe担当者にお問い合わせください。

* **ドメインが検証済みでデプロイ済み**
このステータスは、カスタムドメイン名が使用できる状態であることを示します。
   >[!NOTE]
   >この時点で、カスタムドメイン名はテストの準備ができており、Cloud Manager のドメイン名を指すようになっています。詳細については、「[DNS 設定の指定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)」を参照してください。

* **削除**
カスタムドメイン名の削除を実行中です。

* **削除失敗**
カスタムドメイン名の削除に失敗しました。再試行する必要があります。詳しくは、「[カスタムドメイン名の削除](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)」を参照してください。


## カスタムドメイン名の既存の CDN 設定 {#pre-existing-cdn}

IP 許可リスト、SSL 証明書、カスタムドメイン名のいずれかについて CDN 設定が既に存在している環境のユーザーの場合、**IP 許可リスト**&#x200B;および&#x200B;**環境**&#x200B;の詳細ページに以下のメッセージが表示されます。UI に表示されるメッセージは、顧客が UI から既存の環境設定をすべて移行した後に消えます。メッセージが消えるまでに 1～2 営業日かかる場合があります。

>[!NOTE]
>既存の設定を表示および管理するには、UI を使用して設定を追加する必要があります。詳しくは、[カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)を参照してください。

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
