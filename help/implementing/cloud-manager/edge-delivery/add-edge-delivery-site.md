---
title: Cloud ManagerへのEdge Delivery サイトの追加
description: 実稼動プログラムまたはサンドボックスプログラムにEdge Delivery サイトを追加する方法を説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: c952e69aa637b30abec4deba0e643b4287d84330
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 3%

---


# Cloud ManagerへのEdge Delivery サイトの追加 {#adding}

Edge Delivery サイトは、実稼動プログラムまたはサンドボックスプログラムに追加できます。

Edge Delivery サイトをCloud Managerに追加するには、[Edge Delivery プロジェクトのサポートチケットを登録 ](/help/edge/overview.md##support-ticket) する必要があります。

[Cloud ManagerのEdge Delivery Servicesの概要 ](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md) も参照してください。

**Edge Delivery サイトをCloud Managerに追加するには：**

1. [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) でCloud Managerにログインし、適切なプログラムを選択します。
1. 次のいずれかの操作を行います。

   * **プログラムの概要** ページで、「**Edge Delivery**」タブをクリックします。 次に、ページの右下隅付近にある「**Edge Delivery サイトを追加**」をクリックします。

     ![ 「Edge Delivery」タブからEdge Delivery サイトを追加する ](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * ページの左上隅にあるハンバーガーアイコンをクリックして、左側のナビゲーションメニューを表示します。 **サービス** 見出しの下の **Edge Delivery Sites** をクリックします。 ページの右上隅付近にある「**サイトを追加**」をクリックします。

     ![ 「Edge Delivery サイト」ボタンから「Edge Delivery サイトを追加」 ](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. **Edge Delivery サイトを追加** ダイアログボックスで、必須フィールドに次の情報を入力します。

   | テキストフィールド | 提供するデータ |
   | --- | --- |
   | サイト名 | 追加するEdge Delivery サイトの名前を入力します。 名前は、Cloud Manager内のサイトの一意の ID として機能します。 |
   | リポジトリ URL | このフィールドは、web サイトのコードが保存されている Git リポジトリーを参照します。 このフィールドを使用すると、Cloud Managerはデプロイメントプロセス中にそのリポジトリからコードを取り込むことができます。 |
   | サイトの説明 (オプション) | 追加するEdge Delivery サイトの簡単な説明を入力します。 この説明は、サイトを識別して区別するのに役立ち、追加した他のサイトの管理と認識を容易にします。 |

1. ダイアログボックスの右下隅にある「**追加**」をクリックします。

1. **リポジトリの所有権を確認** ダイアログボックスが開きます。 ファイルを開いた状態で、次の手順を実行します。

   1. 「**リポジトリ URL**」フィールドにリストされている Git リポジトリの `main` ブランチに、パスと名前が `well-known/adobe/cloudmanager-challenge.txt` のファイルを追加します。
      * 必要に応じて、「**コピー** アイコンをクリックして、パスをクリップボードにコピーします。
      * 場所のパスの先頭にピリオドを追加し *いでください*
   1. **Step &amp;num; 1** フィールドのコードを、前の手順で作成したファイルに追加します。
      * 必要に応じて、「**コピー** アイコンをクリックして、コードをクリップボードにコピーします。
   1. Git リポジトリで、作成した変更のプルリクエストを作成し、`main` に結合します。

1. **確認** をクリックします。

リポジトリが検証されると、Edge配信サイト テーブル内のステータスが緑色の円に変わり、その内側に白いチェックマークが付きます。
