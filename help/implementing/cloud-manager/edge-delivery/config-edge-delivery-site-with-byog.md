---
title: 外部 Git リポジトリを使用するために Edge Delivery サイトを設定
description: Edge Delivery サイトをプライベートまたはエンタープライズ Git リポジトリにリンクする方法について説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 1dbaef34-efa3-4287-b7b1-f60db938146d
source-git-commit: e1922bd862a2106a274694ea1d3a98da9c186049
workflow-type: ht
source-wordcount: '325'
ht-degree: 100%

---

# 外部 Git リポジトリを使用するために Edge Delivery サイトを設定

Edge Delivery サイトを設定して、Cloud Manager に既にオンボードされている任意のプライベート Git リポジトリからコードを取り込むことができます。

**サポートされている Git ベンダー**

| サポートレベル | ベンダー | メモ |
| --- | --- | --- |
| 一般提供 | • GitHub Enterprise（セルフホストバージョン）<br>• Bitbucket（クラウドバージョン）<br>• GitLab（クラウドバージョンとセルフホストバージョン） | イネーブルメントリクエストなしでの接続 |
| Alpha プログラム | Azure DevOps（クラウドバージョン） | [アクセスの申請](mailto:grp-cloudmanager_byog@adobe.com) |
| Beta プログラム | アドビがホストするリポジトリ（Cloud Manager で作成） | [利用申請](mailto:grp-cloudmanager_byog@adobe.com) |

**Edge Delivery サイトを設定して、外部 Git リポジトリを使用するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、外部 Git リポジトリを使用するプログラム（Edge Delivery Services が設定されているもの）を選択します。
1. 左側のパネルの&#x200B;**プログラム**&#x200B;見出しの下にある「**![概要アイコン](/help/implementing/cloud-manager/edge-delivery/assets/overview.svg) 概要**」をクリックします。
1. **プログラムの概要**&#x200B;ページで、「**Edge Delivery**」タブをクリックします。
1. **Edge Delivery サイト**&#x200B;のテーブルで、外部リポジトリを使用するように設定するサイトの行の末尾にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックし、「**Bring your own Git**」をクリックします。
1. Bring your own Git ダイアログボックスの&#x200B;**リポジトリ名**&#x200B;ドロップダウンリストで、`READY` ステータスの Git リポジトリを選択し、「**確認**」をクリックします。

   Cloud Manager は、1 回限りの秘密鍵トークンを返します。サイトを再設定すると、Cloud Manager により新しい秘密鍵トークンが生成されます。

1. [BYO Git ガイド](https://www.aem.live/developer/byo-git)の説明に従って、トークンをコピーし、**helix-admin** のサイト設定に追加します。
1. Cloud Manager に戻り、外部リポジトリを使用するように設定したサイトの行の末尾にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックし、「**コードを同期**」をクリックします。
1. 同期する分岐を選択し、「**同期**」をクリックします。

任意の分岐の各コミットで、自動同期がトリガーされるようになりました。完全な手動同期が必要な場合は、**コードを同期**&#x200B;を再度使用します。
