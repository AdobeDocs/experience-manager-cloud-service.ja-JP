---
title: DNS レコードのステータスを確認
description: Cloud Managerを使用して DNS 設定が正しく解決されているかどうかを判断する方法について説明します。
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8a10634e413ea5c66845dfffa7396a4554a5b3ca
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 39%

---


# DNS レコードのステータスを確認 {#check-dns-record-status}

Cloud Managerを使用して DNS 設定が正しく解決されているかどうかを判断する方法について説明します。

## DNS レコードのステータス {#status}

カスタムドメイン名は、DNS が正しく解決されるまで、ライブトラフィックを提供できません。 Cloud Manager内では、お使いのドメイン名がAEM as a Cloud Service web サイトに正しく対応しているかどうかを判断できます。

## 要件 {#requirements}

Cloud Managerを使用して DNS レコードのステータスを確認する前に、次の要件を満たします。

[ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) の説明に従って、カスタムドメイン名の DNS 設定を既に構成している必要があります。

## DNS レコードのステータスを確認 {#how-to}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。

1. 左側のナビゲーションパネルで「**ドメイン設定**」をクリックします。

1. そのドメイン名の&#x200B;**ステータス**&#x200B;アイコンをクリックします。

Cloud Managerはドメイン名に対して DNS 検索を実行し、それを表示します [ 現在のステータス ](#statuses)。

カスタムドメイン名が最初に正常に検証およびデプロイされると、Cloud Managerによって DNS 参照が自動的にトリガーされます。 それ以降の試行では、ステータスの横にある「**もう一度解決する**」アイコンをアクティブに選択する必要があります。

## Cloud Managerの DNS ステータス {#statuses}

Cloud Manager では、カスタムドメインのステータスは次のいずれかになります。

| ステータス | 説明 |
| --- | --- |
| DNS ステータスが検出されませんでした | カスタムドメイン名が正常に検証およびデプロイされるまで、DNS ステータスは検出されません。 このステータスは、カスタムドメイン名が削除中の場合にも表示されます。 |
| DNS が正しく解決されません | このステータスは、DNS レコードの設定が解決されていないか、間違っていることを示します。 詳しくは、[ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) を参照してください。<br> 準備が整ったら、ステータスの横にある **もう一度解決する** アイコンを選択する必要があります。 |
| DNS 解決が進行中です | 解決が進行中です。 このステータスは、通常、ステータスの横にある「**もう一度解決する**」アイコンを選択した後に表示されます。 |
| DNS が正しく解決されます | DNS 設定が正しく構成されています。 サイトは訪問者にサービスを提供しています。 |

## 次の手順 {#next-steps}

Cloud Manager で使用するカスタムドメインが正常に設定されました。Cloud Managerを使用してカスタムドメイン名を管理する方法について詳しくは、[ カスタムドメイン名の管理 ](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) のドキュメントを参照してください。
