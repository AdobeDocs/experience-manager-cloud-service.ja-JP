---
title: Cloud ManagerへのEdge Delivery サイトの追加
description: 実稼動プログラムまたはサンドボックスプログラムにEdge Delivery サイトを追加する方法と、そのメリットについて説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 68f05c49ebc3d46aa44b3998e6142ab8547e5455
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 2%

---


# Cloud ManagerへのEdge Delivery サイトの追加 {#eds-add-site}

実稼動プログラムまたはサンドボックスプログラムにEdge Delivery サイトを追加する方法と、そのメリットについて説明します。

## はじめに {#introduction}

AEM as a Cloud Serviceを使用したEdge Delivery Servicesプロジェクトの一環として、Edge Delivery サイトをCloud Managerに追加することをお勧めします。 Edge Delivery Web サイトをCloud Managerに追加すると、次の利点があります。

* [Adobe管理による CDN へのアクセス](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)
* [SLA レポートへのアクセス](/help/implementing/cloud-manager/sla-reporting.md)
* [ライセンス使用状況レポートへのアクセス](/help/implementing/cloud-manager/license-dashboard.md)

[Edge Delivery プロジェクトのサポートチケットを登録 ](/help/edge/overview.md##support-ticket) するには、Edge Delivery サイトをCloud Managerに追加する必要があります。

## Cloud ManagerへのおよびEdge Delivery サイトの追加 {#adding}

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

実稼動プログラムにEdge Delivery Servicesを追加すると、そのプログラムにはEdge Delivery Servicesライセンスが適用されます。

各Edge Delivery サイトには、Edge Delivery サイトの作成手順を示す **0}Edge Delivery to-do- リストがあります。**

![Edge Delivery to-do アプリ ](/help/implementing/cloud-manager/assets/edge-delivery-to-do-ist.png)

これらの手順について詳しくは、[Cloud ManagerでのEdge Delivery Servicesの概要 ](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list) を参照してください。
