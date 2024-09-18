---
title: Cloud ManagerへのEdge Delivery サイトの追加
description: 実稼動プログラムまたはサンドボックスプログラムにEdge Delivery サイトを追加する方法を説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ad6a0e13f27839b9900e440d60948158ddf75d99
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 3%

---


# Cloud ManagerへのEdge Delivery サイトの追加 {#adding}

Edge Delivery サイトを実稼動プログラムに追加すると、そのサイトにEdge Delivery Servicesライセンスが適用されます。

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

   | テキストフィールド | 説明 |
   | - | --- |
   | サイト名 | 追加するEdge Delivery サイトの名前を入力します。<br> 名前は、Cloud Manager内のサイトの一意の ID として機能します。 |
   | リポジトリ URL | Web サイトのコードが保存されている Git リポジトリーを入力します。<br> このフィールドを使用すると、Cloud Managerはデプロイメントプロセス中にリポジトリからコードを取り込むことができます。 |
   | サイトの説明 (オプション) | 追加するEdge Delivery サイトの簡単な説明を入力します。<br> 説明は、サイトを識別して区別するのに役立ち、追加した他のサイトの管理と認識を容易にします。 |

1. ダイアログボックスの右下隅にある「**追加**」をクリックします。

1. **リポジトリの所有権の確認** ダイアログボックスで、次の手順を実行してリポジトリの所有権を確認します。

   | ステップ番号 | 説明 |
   | - | - |
   | **1** | 「**リポジトリ URL**」フィールドにリストされている Git リポジトリの `main` ブランチに、パスと名前が `well-known/adobe/cloudmanager-challenge.txt` のファイルを追加します。 場所のパスの先頭にピリオドを追加し *いでください*<br> 必要に応じて、「**コピー** アイコンをクリックして、パスをクリップボードにコピーします。 |
   | **2** | 手順 2 のテキストフィールドに表示されたコードを、手順 1 で作成したファイルに追加します。<br> 必要に応じて、「**コピー** アイコンをクリックして、コードをクリップボードにコピーします。 |
   | **3** | 作成した変更のプルリクエストを Git リポジトリーで作成し、`main` に結合してコードをコミットします。 |

1. **確認** をクリックします。

リポジトリが検証されると、Edge配信サイト テーブル内のステータスが緑色の円に変わり、その内側に白いチェックマークが付きます。
