---
title: Screens as a Cloud Service でのディスプレイの作成と管理
description: このページでは、Screens as a Cloud Service でディスプレイを作成および管理する方法について説明します。
exl-id: 0f9faa4b-b50e-40f8-a8ed-280f8bd0a9b8
source-git-commit: 9e0ab778e97658bc8d7669b1f582f3bcddd47915
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 37%

---

# Screens as a Cloud Service でのディスプレイの作成と管理 {#create-displays-screens-cloud}

チャネルを公開したら、Screens Services Provider でディスプレイを作成します。

ディスプレイとはスクリーンの仮想グループのことで、通常は隣り合って配置されます。ディスプレイのインストールは通常、永続的です。オブジェクトコンテンツの作成者はこれを操作し、常に物理的なディスプレイの代わりに論理的なディスプレイとして参照します。

## 目的 {#objective}

このドキュメントでは、Screens Services Provider でディスプレイを作成および管理する方法について説明します。 読み終えると、次のことができるようになります。

* ディスプレイの作成および削除方法を説明します
* ディスプレイをフォルダーに整理する方法を説明します

## ディスプレイの作成手順 {#create-display}

次の手順に従って、Screens Services Provider からディスプレイを作成します。

1. AEM Cloud Service インスタンスから Screens Services Provider に移動します。
1. 左側のナビゲーションパネルから「**ディスプレイ**」を選択し、画面の右上隅にある「**作成**」をクリックします。

   ![画像](/help/screens-cloud/assets/display/disp-1.png)

1. アクションバーから「**ディスプレイ**」を選択します。

   ![画像](/help/screens-cloud/assets/display/disp-2.png)

1. 「**表示名**」に「**LoopingChannelDisplay**」と入力し、「**作成**」をクリックします。

   ![画像](/help/screens-cloud/assets/display/disp3.png)

1. **LoopingChannelDisplay** というタイトルのディスプレイが、ディスプレイリストに表示されます。

   ![画像](/help/screens-cloud/assets/display/disp-4.png)

### ディスプレイの削除 {#deleting-display}

ディスプレイは、Screens サービスプロバイダーから削除できます。

ディスプレイを選択し、パネルの下部にある「**削除**」をクリックします（下図を参照）。

![画像](/help/screens-cloud/assets/display/disp-5.png)

## 表示をフォルダーに整理する手順 {#organize-display}

## フォルダーレールの切り替え方法 {#toggle-rail}

フォルダーレールの表示を、すべてのフォルダーから特定のフォルダーに切り替えることができます。

1. 次に示すボタンをクリックして、ディスプレイの在庫表示に移動します。

   ![画像](/help/screens-cloud/assets/display/display-inventory.png)

1. フォルダーのサイドレールが表示されます。

   ![画像](/help/screens-cloud/assets/display/toggle-rail.png)

1. 選択 **フォルダーを非表示** 再び閉じる

## 新しいフォルダーの作成方法 {#create-folder}

フォルダーを作成して、ディスプレイを整理しやすくすることができます。

1. 在庫表示にナビゲートします。
1. 現在フォルダー内にいないことを確認します。次が表示されます。

   ![画像](/help/screens-cloud/assets/display/verify-view.png)

   注意： **すべてのディスプレイ** フォルダーのサイドレールで選択する必要があります。パンくずナビゲーションには、次の項目のみが表示されます **表示**.

1. 右上の「作成」ボタンをクリックし、 **フォルダー** オプション。

   ![画像](/help/screens-cloud/assets/display/Createfolder.png)

1. 新しいフォルダーのタイトルを入力し、 **作成**.

   ![画像](/help/screens-cloud/assets/display/Createfolder2.png)

## ネストされた新しいフォルダーの作成方法 {#nested-folder}

1. 在庫表示にナビゲートします。

1. フォルダーのサイドレールから、または在庫表示で参照して、目的の親フォルダーを選択します。
1. 目的の親フォルダーが選択されていることを確認します。

   ![画像](/help/screens-cloud/assets/display/Nestedview.png)

   * フォルダーのサイドレールでフォルダーを選択する必要があります。
   * パンくずナビゲーションでは、の横に現在のフォルダー名が表示されます。 **表示**.

1. クリック  **作成**  右上で、「 **フォルダー** オプション。

   ![画像](/help/screens-cloud/assets/display/Createfolder.png)

1. 新しいフォルダーのタイトルを入力し、 **作成**.

   ![画像](/help/screens-cloud/assets/display/Createfolder2.png)

## コンテンツを新しいフォルダーに移動する方法 {#move-folder}

コンテンツを新しいフォルダーに移動すると、ディスプレイを整理しやすくなります。

1. 在庫表示にナビゲートします。

1. フォルダーのサイドレールから、または在庫表示からを選択して、目的の親フォルダーを選択します。

1. 目的の親フォルダーを選択したことを確認します。

![画像](/help/screens-cloud/assets/display/movetofolder.png)

**注意**:フォルダーのサイドレールでフォルダーを選択する必要があります。 また、パンくずナビゲーションでは、現在のフォルダー名がの横に表示されます。 **表示**.

## フォルダーからコンテンツを削除する方法 {#delete-folder}

すべてのフォルダ操作には、在庫表示の選択アクションバーからアクセスできます。

1. 親フォルダーに移動するか、サイドレールから選択します。

1. 在庫表示で、削除する子フォルダーを選択し、空にします。

1. 次をクリック： **削除** アクションを選択します。 フォルダーが空でない場合、このアクションは無効になります。


## 次のステップ {#whats-next}

これで、プロジェクトでのディスプレイの作成と管理の方法を学びました。次に、「[Screens as a Cloud Service へディスプレイへのチャネル割り当て](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/assigning-channels-to-display.html?lang=ja)」ドキュメントを確認し、Screens as a Cloud Service のジャーニーを続けてください。
