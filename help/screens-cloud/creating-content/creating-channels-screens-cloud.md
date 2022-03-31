---
title: Screens as a Cloud Service でのチャネルの作成と管理
description: ここでは、Screens as a Cloud Service でチャネルを作成および管理する方法について説明します。
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: afcee8019c9b59f3eb1fdcabd569272eeea76dab
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 50%

---

# Screens as a Cloud Service でのチャネルの作成と管理 {#creating-channels-screens-cloud}

AEM Screensプロジェクトを作成したら、チャネルを作成する必要があります。
***チャネル***：コンテンツのシーケンス（画像やビデオ）、Web サイト、または単一ページアプリケーションを表示します。

## 目的 {#objective}

このドキュメントでは、Screens コンテンツプロバイダーでの AEM Screens プロジェクトのチャネルの作成と管理について説明します。読み終わると、次ができるようになります。

* Screens コンテンツプロバイダーへのチャネルを作成する方法を理解する
* チャネル内のコンテンツを管理し編集する
* チャネルのアクティベーションスケジュール

## Screens as a Cloud Service で新しいシーケンスチャネルを作成する手順 {#create-new-channel}

>[!NOTE]
>**前提条件**
>この節を開始する前に、[Screens as a Cloud Service でのプロジェクトの作成と管理](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md)を参照してください。

以下の手順に従って、Screens as a Cloud Service で新しいシーケンスチャネルを作成します。

1. Screens コンテンツプロバイダーに移動します。

1. *FirstDigitalExperience*&#x200B;など、AEM Screens プロジェクトに移動します。

1. プロジェクトから&#x200B;**チャネル**&#x200B;フォルダーを選択（例：**FirstDigitalExperience**／**チャネル**）し、アクションバーの「**作成**」をクリックします。

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. **作成**&#x200B;ウィザードで&#x200B;**シーケンスチャネル**&#x200B;などのテンプレートを選択し、「**次へ**」をクリックします。

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > **作成**&#x200B;ウィザードは、チャネルの作成時に様々なタイプのテンプレートを提供します。詳しくは、作成ウィザードの「[使用可能なテンプレート](#available-templates)」の節を参照してください。

1. シーケンスチャネルの名前（例：**LoopingChannelOne**）を入力し、「**作成**」をクリックします。

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   AEM Screens プロジェクトの「Channels」フォルダーに **LoopingChannelOne** が表示されます。

   チャネルを作成したら、チャネルにコンテンツを追加できます。チャネルにアセット（画像／ビデオ）を追加する方法については、[チャネルへのコンテンツの追加](#add-content)を参照してください。

## チャネルの管理 {#managing-channels}

プロパティおよびダッシュボードを編集および表示でき、またチャネルをコピー、プレビュー、削除できます。

プロジェクトからチャネルに移動して選択します（下図を参照）。チャネルの編集、プロパティの表示、コンテンツのプレビュー、公開の管理、チャネルの削除などのオプションをアクションバーから選択できるようになります。

![](/help/screens-cloud/assets/create-content/channelprop1.png)

### チャネルへのコンテンツの追加 {#add-content}

チャネルにコンテンツを追加するには、下の手順に従います。

1. 編集するチャネルを選択します（下の図を参照）。アクションバーの左上の「**編集**」をクリックして、エディターを開きます。

   ![](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. エディターでは、アセットやコンポーネントを公開するチャネルに追加できます。

1. 左側のパネルからアセットをドラッグ＆ドロップし、エディターに追加します。

   ![](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >「**プレビュー**」をクリックして、チャネルのコンテンツをプレビューします。
   >![](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## 作成ウィザードで使用可能なテンプレート {#available-templates}

**チャネルの作成**&#x200B;ウィザードの使用中に、次のテンプレートを使用できます。

| 使用可能なテンプレート | 説明 |
|--- |--- |
| チャネルフォルダー | チャネルのコレクションを格納するためのフォルダーを作成できます。 |
| シーケンスチャネル | コンポーネントを連続して（スライドショーで 1 つずつ）再生するチャネルを作成できます。 |
| 左／右 L バー型分割画面チャネル | コンテンツ作成者が、様々な種類のアセットを適切なサイズのゾーンに表示できます。 |

## チャネルのデフォルトの割り当ての詳細を使用 {#default-channels}

この機能を使用すると、チャネルのデフォルトのアクティベーションスケジュールを定義し、ディスプレイのすべての割り当てにデフォルトで使用できます。 これにより、煩雑なスケジュール定義を繰り返す必要がなくなります。

### チャネルのデフォルトの割り当ての詳細を作成する {#create-default}

1. 設定するチャネルの詳細ページに移動します。
1. を **デフォルトの割り当ての詳細** ページ上にタイルを表示します。

   ![画像](/help/screens-cloud/assets/display/Assignment1.png)

1. クリック **デフォルトの詳細を設定**.
1. 優先度、開始日と終了日、およびチャネルの繰り返しパターンを含むデフォルトの割り当ての詳細を設定し、 **割り当て**.

   ![画像](/help/screens-cloud/assets/display/Assignments2.png)

1. 割り当ての詳細が **デフォルトの割り当ての詳細** タイル：

   ![画像](/help/screens-cloud/assets/display/Assignments3.png)

このタイルには、次の情報が表示されます。
* ディスプレイ内のチャネルのデフォルトの優先度。
* チャネルの再生がスケジュールされている場合のアクティベーションの開始日と終了日です。
* 繰り返しの合成ビュー（時間別/日別/週別/月別/年別およびその繰り返しに与えられた名前）。

### ディスプレイに割り当てる際にデフォルトの割り当ての詳細を使用 {#default-display}

デフォルトの割り当て詳細を持つチャネルをに割り当てると、通常のチャネルと同じ方法で表示できます。また、カスタムチャネルを毎回手動で定義する代わりに、デフォルトの割り当て詳細を利用するオプションも追加されました。

1. チャネルを割り当てるディスプレイの詳細ページに移動し、 **チャネルを割り当て**.
または、在庫表示で目的の表示を選択し、 **チャネルを割り当て**.
1. チャネル割り当てダイアログが開きます。

   ![画像](/help/screens-cloud/assets/display/Assignments4.png)

1. デフォルトの割り当ての詳細を持つ目的のチャネルをチャネルピッカーから選択します。
1. チャネル割り当てダイアログが変わり、デフォルトの割り当て詳細を選択したり、カスタムの割り当て詳細を選択したりできます。

   ![画像](/help/screens-cloud/assets/display/Assignments5.png)

1. クリック **割り当て** 割り当てを最終決定するには、 **カスタム割り当ての詳細を設定** 特定の表示のコンテキストで、デフォルトを他の値で上書きする場合。

   ![画像](/help/screens-cloud/assets/display/Assignments6.png)

1. 注意： **割り当てられたチャネル** タイルが新しい割り当てで更新されます。

   ![画像](/help/screens-cloud/assets/display/Assignments7.png)

1. チャネルは、カスタムスケジュール（時計アイコン）を使用しているか、デフォルトの詳細（世界時計アイコン）を継承しているかに応じて異なるアイコンを持ち、それらをクリックするとスケジュールの詳細が表示されます。
1. また、各タイプで使用可能なアクションは異なることに注意してください。

   ![画像](/help/screens-cloud/assets/display/Assignments8.png)

**注意：** デフォルトの割り当ての詳細を利用するチャネル割り当ては、ディスプレイのコンテキストでは編集できません。

* カスタム割り当てに変更する必要がある場合は、まず割り当てを削除し、次に **カスタム割り当ての詳細を設定** オプション。
* デフォルトの割り当ての詳細のプロパティを変更する必要がある場合は、チャネルの詳細ページから直接変更する必要があります。

### チャネルからデフォルトの割り当ての詳細を削除する {#remove-display}

1. デフォルトの割り当て詳細を削除するチャネルの詳細ページに移動します。
1. を **デフォルトの割り当ての詳細** ページ内のタイル
1. 次をクリック： **デフォルトを削除**.

   ![画像](/help/screens-cloud/assets/display/Assignments9.png)

1. 確認ダイアログが表示され、詳細は次の条件のいずれかに一致します。
   **a.** チャネルはどのディスプレイにも使用されていません。

   ![画像](/help/screens-cloud/assets/display/Assignments10.png)

**b.** チャネルは、1 つのディスプレイで使用されます。

![画像](/help/screens-cloud/assets/display/Assignment11.png)

**c.** チャネルは、複数のディスプレイで使用されます。

![画像](/help/screens-cloud/assets/display/Assignments12.png)

1. 次をクリック： *削除* をクリックして変更を検証します。

**注意：** チャネルからデフォルトの割り当ての詳細を削除すると、それを使用していたすべてのディスプレイ上の一致する割り当てが削除されます。
その結果、代替コンテンツがディスプレイに再生されない場合は、空白の画面が表示される可能性があります。

## 次のステップ {#whats-next}

プロジェクトで AEM Screens チャネルを設定したら、チャネルを公開する必要があります。Screens サービスプロバイダーからプレーヤーを管理する前に、[Screens as a Cloud Service でのチャネルの公開](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/manage-publish.html?lang=ja)を参照してください。
