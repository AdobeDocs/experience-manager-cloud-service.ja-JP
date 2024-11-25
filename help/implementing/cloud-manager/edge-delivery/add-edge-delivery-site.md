---
title: Cloud Manager への Edge Delivery サイトの追加
description: 実稼動プログラムまたはサンドボックスプログラムに Edge Delivery サイトを追加する方法について説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 17e842c9-599a-4877-9834-1e7220f508a8
source-git-commit: db661281831dcb07491dca16e73e835b487814a6
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 96%

---

# Cloud Manager への Edge Delivery サイトの追加 {#adding}

実稼動プログラムに Edge Delivery サイトを追加すると、Edge Delivery Services ライセンスがそのサイトに適用されます。

[Edge Delivery プロジェクトのサポートチケットを登録](/help/edge/overview.md##support-ticket)するには、Cloud Manager に Edge Delivery サイトを追加する必要があります。

詳しくは、[Cloud Manager の Edge Delivery Services の概要](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)も参照してください。

**Cloud Manager に Edge Delivery サイトを追加するには：**

1. [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. 次のいずれかの操作を行います。

   * **プログラムの概要**&#x200B;ページで、「**Edge Delivery**」タブをクリックします。次に、ページの右下隅付近にある「**Edge Delivery サイトを追加**」をクリックします。

     ![「Edge Delivery」タブからの Edge Delivery サイトの追加](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左側のサイドメニューを表示します。
**サービス**&#x200B;見出しの下にある ![Web ページアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg)「**Edge Delivery サイト**」をクリックします。
ページの右上隅にある「**サイトを追加**」をクリックします。

     ![「Edge Delivery サイト」ボタンからの Edge Delivery サイトの追加](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. **Edge Delivery サイトを追加**&#x200B;ダイアログボックスで、必須フィールドに次の情報を入力します。

   | テキストフィールド | 説明 |
   | - | --- |
   | サイト名 | 追加する Edge Delivery サイトの名前を入力します。<br>名前は、Cloud Manager 内でサイトの一意の ID として機能します。 |
   | リポジトリ URL | Web サイトのコードが保存されている Git リポジトリを入力します。<br>このフィールドにより、Cloud Manager はデプロイメントプロセス中にそのリポジトリからコードを取り込むことができます。 |
   | サイトの説明（オプション） | 追加する Edge Delivery サイトの簡単な説明を入力します。<br>説明は、サイトを識別して区別するのに役立ち、追加した他のサイトの中で管理および認識しやすくなります。 |

1. ダイアログボックスの右下隅にある「**追加**」をクリックします。

1. **リポジトリの所有権を検証**&#x200B;ダイアログボックスで、次の手順を実行してリポジトリの所有権を検証します。

   | 手順番号 | 説明 |
   | - | - |
   | **1** | 「**リポジトリ URL**」フィールドにリストされている Git リポジトリの `main` 分岐に、パスと名前が `well-known/adobe/cloudmanager-challenge.txt` のファイルを追加します。場所のパスの先頭にピリオドを追加&#x200B;*しない*&#x200B;でください。<br>必要に応じて、「![コピー](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)」をクリックして、パスをクリップボードにコピーします。 |
   | **2** | 手順 2 のテキストフィールドに表示されたコードを、手順 1 で作成したファイルに追加します。<br>必要に応じて、「![コピー](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)」をクリックして、コードをクリップボードにコピーします。 |
   | **3** | 作成した変更のプルリクエストを Git リポジトリに作成し、`main` に結合してコードをコミットします。 |

1. 「**確認**」をクリックします。

リポジトリが検証されると、Edge Delivery サイトテーブル内のそのステータスが更新されます。 内側に白色のチェックマークが付いた緑色の円は、ステータスを示します。

同じ表で、![Edge Delivery サイトに関する情報](https://spectrum.adobe.com/static/icons/workflow_18/Smock_InfoOutline_18_N.svg) をクリックして、サイトの詳細を表示します。この情報には、検証済みのリポジトリ URL と、プレビューおよび実稼動 web サイトの URL が含まれます。
