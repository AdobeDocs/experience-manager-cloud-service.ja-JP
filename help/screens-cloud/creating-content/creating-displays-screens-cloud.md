---
title: Screens as a Cloud Service でのディスプレイの作成と管理
description: このページでは、Screens as a Cloud Service でディスプレイを作成および管理する方法について説明します。
exl-id: 0f9faa4b-b50e-40f8-a8ed-280f8bd0a9b8
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: ht
source-wordcount: '649'
ht-degree: 100%

---

# Screens as a Cloud Service でのディスプレイの作成と管理 {#create-displays-screens-cloud}

チャネルを公開したら、Screens サービスプロバイダーでディスプレイを作成します。

ディスプレイとはスクリーンの仮想グループのことで、通常は隣り合って配置されます。ディスプレイは、通常、インストールに関して永続的です。このオブジェクトコンテンツは、作成者が操作するもので、常に物理ディスプレイではなく論理的なディスプレイとして参照します。

## 目的 {#objective}

このドキュメントでは、Screens サービスプロバイダーでディスプレイを作成および管理する方法について説明します。読み終えると、次のことが習得できます。

* ディスプレイの作成および削除方法
* ディスプレイをフォルダーに整理する方法

## ディスプレイの作成手順 {#create-display}

以下の手順に従って、Screens サービスプロバイダーからディスプレイを作成します。

1. AEM Cloud Service インスタンスから Screens サービスプロバイダーに移動します。
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

## フォルダーパネルの切り替え方法 {#toggle-rail}

フォルダーパネルの表示を、すべてのフォルダーから特定のフォルダーに切り替えることができます。

1. 次に示すボタンをクリックして、ディスプレイの在庫表示に移動します。

   ![画像](/help/screens-cloud/assets/display/display-inventory.png)

1. フォルダーのサイドパネルが表示されます。

   ![画像](/help/screens-cloud/assets/display/toggle-rail.png)

1. 「**フォルダーを非表示**」を選択して閉じます。

## フォルダーの作成方法 {#create-folder}

フォルダーを作成して、ディスプレイを整理しやすくできます。

1. 在庫表示にナビゲートします。
1. 現在フォルダーの中にいないようにします。その場合、次が表示されます。

   ![画像](/help/screens-cloud/assets/display/verify-view.png)

   注意：**すべてのディスプレイ**&#x200B;フォルダーのサイドパネルで選択する必要があります。パンくずナビゲーションには、**ディスプレイ**&#x200B;のみが表示されます。

1. 右上の「作成」ボタンをクリックし、「**フォルダー**」オプションを選択します。

   ![画像](/help/screens-cloud/assets/display/Createfolder.png)

1. 新しいフォルダーのタイトルを入力し、「**作成**」をクリックします。

   ![画像](/help/screens-cloud/assets/display/Createfolder2.png)

## ネストされたフォルダーの作成方法 {#nested-folder}

1. 在庫表示にナビゲートします。

1. フォルダーのサイドパネルから、または在庫表示で参照して、目的の親フォルダーを選択します。
1. 目的の親フォルダーが選択されていることを確認します。

   ![画像](/help/screens-cloud/assets/display/Nestedview.png)

   * フォルダーのサイドパネルでフォルダーを選択する必要があります。
   * パンくずナビゲーションでは、「**ディスプレイ**」の横に現在のフォルダー名が表示されます。

1. 右上の「**作成**」をクリックし、「**フォルダー**」オプションを選択します。

   ![画像](/help/screens-cloud/assets/display/Createfolder.png)

1. 新しいフォルダーのタイトルを入力し、「**作成**」をクリックします。

   ![画像](/help/screens-cloud/assets/display/Createfolder2.png)

## コンテンツを新しいフォルダーに移動する方法 {#move-folder}

コンテンツを新しいフォルダーに移動すると、ディスプレイを整理しやすくなります。

1. 在庫表示にナビゲートします。

1. フォルダーのサイドパネルから、または在庫表示から選択して、目的の親フォルダーを選択します。

1. 目的の親フォルダーを選択したことを確認します。

![画像](/help/screens-cloud/assets/display/movetofolder.png)

**注意**：フォルダーのサイドパネルでフォルダーを選択する必要があります。また、パンくずナビゲーションでは、「**ディスプレイ**」の横に現在のフォルダー名が表示されます。

## フォルダーからコンテンツを削除する方法 {#delete-folder}

すべてのフォルダー操作には、在庫表示の選択アクションバーからアクセスできます。

1. 親フォルダーに移動するか、サイドパネルから選択します。

1. 在庫表示で、削除する子フォルダーを選択し、空であることを確認します。

1. 選択アクションバーの「**削除**」アクションをクリックします。フォルダーが空でない場合、アクションは無効になります。


## 次の手順 {#whats-next}

これで、プロジェクトでのディスプレイの作成と管理の方法を学びました。次に、「[Screens as a Cloud Service へディスプレイへのチャネル割り当て](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/assigning-channels-to-display.html?lang=ja)」ドキュメントを確認し、Screens as a Cloud Service のジャーニーを続けてください。
