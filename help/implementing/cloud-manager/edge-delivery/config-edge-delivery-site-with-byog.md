---
title: 外部 Git リポジトリを使用するためのEdge Delivery サイトの設定
description: Edge Delivery サイトをプライベートまたはエンタープライズ Git リポジトリにリンクする方法について説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 239ee3021057dd108d18ab2d7729680692223403
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 9%

---


# 外部 Git リポジトリを使用するためのEdge Delivery サイトの設定

Edge Delivery サイトを設定して、Cloud Managerで既にオンボーディングされている任意のプライベート Git リポジトリーからコードを取り込むことができます。

**サポートされている Git ベンダー**

| サポートレベル | ベンダー | メモ |
| --- | --- | --- |
| 一般リリース | ・ GitHub Enterprise （セルフホストバージョン） <br>・ Bitbucket （クラウドバージョン） <br>・ GitLab （クラウドおよびセルフホストバージョン） | イネーブルメントリクエストなしでの接続 |
| Alpha プログラム | Azure DevOps （クラウドバージョン） | [アクセスの申請](mailto:grp-cloudmanager_byog@adobe.com) |
| Beta プログラム | Adobeがホストするリポジトリ（Cloud Managerで作成） | [アクセスの申請](mailto:grp-cloudmanager_byog@adobe.com) |

**外部 Git リポジトリーを使用するようにEdge Delivery サイトを設定するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、外部 Git リポジトリを使用するようにEdge Delivery サイトを設定するEdge Delivery Servicesが設定されているプログラムを選択します。

1. 左側のレールの **プログラム** 見出しの下の **![概要アイコン ](/help/implementing/cloud-manager/edge-delivery/assets/overview.svg) 概要** をクリックします。

1. **プログラムの概要**&#x200B;ページで、「**Edge Delivery**」タブをクリックします。

1. **Edge Delivery サイト** テーブルで、外部リポジトリーを使用するように設定するサイトの行の最後にある ![ その他アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックしてから、**独自の Git を用意する** をクリックします。

1. 「独自の Git を取り込む」ダイアログボックスの **リポジトリ名** ドロップダウンリストで、ステータスが `READY` の Git リポジトリを選択し、「**確認**」をクリックします。

   Cloud Managerは、1 回限りの秘密鍵トークンを返します。 サイトを再設定すると、Cloud Managerによって新しい秘密鍵トークンが生成されます。

1. **BYO Git ガイド** の説明に従って、トークンをコピーし、[helix-admin](https://www.aem.live/developer/byo-git) のサイト設定に追加します。

1. Cloud Managerに戻り、外部リポジトリーを使用するようにサイトを設定した行の最後にある ![ その他アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) アイコンをクリックしてから、**コードを同期** をクリックします。

1. 同期するブランチを選択し、「**同期**」をクリックします。

任意のブランチの各コミットで、自動同期がトリガーされるようになりました。 完全な手動同期が必要な場合は必ず、**同期コード** を再度使用します。

