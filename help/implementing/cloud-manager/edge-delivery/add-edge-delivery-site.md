---
title: Cloud ManagerへのEdge Delivery サイトの追加
description: 実稼動プログラムまたはサンドボックスプログラムにEdge Delivery サイトを追加する方法を説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 4%

---


## Cloud ManagerへのEdge Delivery サイトの追加 {#eds-add-site}

実稼動プログラムにEdge Delivery Servicesを追加すると、そのプログラムにEdge Delivery Servicesライセンスが適用されます。

概要ページに、**Edge Delivery** というクリック可能なタブが表示されます。 タブをクリックすると、追加した各Edge Delivery サイトを一覧表示するテーブルが表示されます。 左側のナビゲーションパネルの **サービス** グループの下に、**Edge Delivery Sites** という名前のメニューオプションがあります。

![ 左側のナビゲーションパネルに「Edge Delivery Sites」を表示し、「Edge Delivery配信」タブの右側にある「Publish」タブを表示する概要ページ ](/help/implementing/cloud-manager/assets/cm-overview-eds.png)

**Edge Delivery サイトをCloud Managerに追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) でCloud Managerにログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、Edge Delivery Servicesが設定されているプログラムを選択します。このプログラムに、Edge Delivery サイトを追加します。
1. 次のいずれかの操作を行います。
   * **プログラムの概要** ページで、「**Edge Delivery**」タブをクリックします。 次に、ページの右下隅付近にある「**Edge Delivery サイトを追加**」をクリックします。

     ![ 「Edge Delivery」タブからEdge Delivery サイトを追加する ](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

     上の画像に示すように、**Edge Delivery to-do リスト** は、Edge Deliveryの使用を開始する際に役立つオプションのオンボーディングチェックリストガイドです。 [Edge Delivery To Do リストについて ](#ed-todo-list) を参照してください。

   * ページの左上隅にあるハンバーガーアイコンをクリックして、左側のナビゲーションメニューを表示します。 **サービス** 見出しの下の **Edge Delivery Sites** をクリックします。 ページの右上隅付近にある「**サイトを追加**」をクリックします。

     ![ 「Edge Delivery サイト」ボタンから「Edge Delivery サイトを追加」 ](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. **Edge Delivery サイトを追加** ダイアログボックスで、次の操作を行います。

   | テキストフィールド | 実行内容 |
   | --- | --- |
   | サイト名 | 追加するEdge Delivery サイトの名前を入力します。 名前は、Cloud Manager内のサイトの一意の ID として機能します。 |
   | リポジトリ URL | このフィールドは、web サイトのコードが保存されている Git リポジトリーを参照します。<br>Edge Delivery サイトに必要なファイルおよびリソース（HTML、CSS、JavaScript、その他の web アセットなど）を含む Git リポジトリの URL を入力します。 この配置により、Cloud Managerはデプロイメントプロセス中にそのリポジトリからコードを取り込むことができます。 |
   | サイトの説明 (オプション) | 追加するEdge Delivery サイトの簡単な説明を入力します。<br> この説明は、サイトを識別して区別するのに役立ち、追加した他のサイトの管理と認識を容易にします。 サイトの目的、コンテンツ、またはその機能や範囲を明確にするのに役立つその他の関連情報に関する詳細を含めることをお勧めします。 |

1. ダイアログボックスの右下隅にある「**追加**」をクリックします。

1. **リポジトリの所有権を確認** ダイアログボックスで、次の各操作を行います。

   | 手順 | 説明 |
   | --- | --- |
   | 1 | 「**リポジトリ URL**」フィールドにリストされている Git リポジトリの `main` ブランチへのロケーションパスを持つファイルを追加します。 必要に応じて、コピーアイコンをクリックして、パスをクリップボードにコピーします。<br> 場所のパスは <br>`well-known/adobe/cloudmanager-challenge.txt` です。場所のパスの先頭にピリオドを追加する <br><br>*しないでください* は次の場所にあります：<br>`.well-known/adobe/cloudmanager-challenge.txt` |
   | 2 | 生成されたコードを手順 1 で作成したファイルに追加します。 必要に応じて、「コピー」アイコンをクリックして、コードをクリップボードにコピーします。 |
   | 3 | Git リポジトリでプルリクエストを作成し、それを結合してコードをコミットします。 |

1. **確認** をクリックします。 リポジトリが検証されると、Edge配信サイト テーブル内のステータスが緑色の円に変わり、その内側に白いチェックマークが付きます。
