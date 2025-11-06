---
title: Screens as a Cloud Service でのチャネルの作成と管理
description: ここでは、Screens as a Cloud Service でチャネルを作成および管理する方法について説明します。
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 100%

---

# Screens as a Cloud Service でのチャネルの作成と管理 {#creating-channels-screens-cloud}

AEM Screensプロジェクトを作成したら、チャネルを作成する必要があります。
***チャネル***：コンテンツのシーケンス（画像やビデオ）、Web サイト、または単一ページアプリケーションを表示します。

## 目的 {#objective}

このドキュメントでは、Screens コンテンツプロバイダーでの AEM Screens プロジェクトのチャネルの作成と管理について説明します。読み終わると、次ができるようになります。

* Screens コンテンツプロバイダーへのチャネルを作成する方法を理解する
* チャネル内のコンテンツを管理し編集する
* [Screens サービスプロバイダー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=ja)でチャネルの割り当てとアクティブ化スケジュールを管理する

## Screens as a Cloud Service で新しいシーケンスチャネルを作成する手順 {#create-new-channel}

>[!NOTE]
>**前提条件**
>ガイドのこの節を開始する前に、[Screens as a Cloud Service でのプロジェクトの作成と管理](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md)を確認してください。

以下の手順に従って、Screens as a Cloud Service でシーケンスチャネルを作成します。

1. Screens コンテンツプロバイダーに移動します。

1. *FirstDigitalExperience*&#x200B;など、AEM Screens プロジェクトに移動します。

1. プロジェクトから&#x200B;**チャネル**&#x200B;フォルダーを選択（例：**FirstDigitalExperience**／**チャネル**）し、アクションバーの「**作成**」をクリックします。

   ![channel-create1](/help/screens-cloud/assets/create-content/channel-create1.png)

1. 「**作成**」ウィザードで「**シーケンスチャネル**」などのテンプレートを選択し、「**次へ**」をクリックします。

   ![channel-create2](/help/screens-cloud/assets/create-content/channel-create2.png)

   >[!NOTE]
   > **作成**&#x200B;ウィザードは、チャネルの作成時に様々なタイプのテンプレートを提供します。詳しくは、作成ウィザードの[使用可能なテンプレート](#available-templates)を参照してください。

1. シーケンスチャネルの名前（例：**LoopingChannelOne**）を入力し、「**作成**」をクリックします。

   ![channel-create3](/help/screens-cloud/assets/create-content/channel-create3.png)

   AEM Screens プロジェクトの「Channels」フォルダーに **LoopingChannelOne** が表示されます。

   チャネルを作成したら、チャネルにコンテンツを追加できます。チャネルにアセット（画像／ビデオ）を追加する方法について詳しくは、[チャネルへのコンテンツの追加](#add-content)を参照してください。

## チャネルの管理 {#managing-channels}

プロパティおよびダッシュボードを編集および表示でき、またチャネルをコピー、プレビュー、削除できます。

プロジェクトからチャネルに移動して選択します（下図を参照）。チャネルの編集、プロパティの表示、コンテンツのプレビュー、公開の管理、チャネルの削除などのオプションをアクションバーから選択できるようになります。

![channelprop1](/help/screens-cloud/assets/create-content/channelprop1.png)

### チャネルへのコンテンツの追加 {#add-content}

チャネルにコンテンツを追加するには、下の手順に従います。

1. 編集するチャネルを選択します（下の図を参照）。アクションバーの左上の「**編集**」をクリックして、エディターを開きます。

   ![edit-channel1](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. エディターでは、公開するチャネルにアセットやコンポーネントを追加できます。

1. 左側のパネルからアセットをドラッグ＆ドロップし、エディターに追加します。

   ![edit-channel2](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >「**プレビュー**」をクリックして、チャネルのコンテンツをプレビューします。
   >![edit-channelpreview](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## 作成ウィザードで使用可能なテンプレート {#available-templates}

**チャネルの作成**&#x200B;ウィザードの使用中に、次のテンプレートを使用できます。

| 使用可能なテンプレート | 説明 |
|--- |--- |
| チャネルフォルダー | チャネルのコレクションを保存するフォルダーを作成できます。 |
| シーケンスチャネル | コンポーネントを連続して（スライドショーで 1 つずつ）再生するチャネルを作成できます。 |
| 左／右 L バー型分割画面チャネル | コンテンツ作成者が、様々な種類のアセットを適切なサイズのゾーンに表示できます。 |

## チャネルのデフォルトの割り当ての詳細を使用 {#default-channels}

この機能を使用すると、チャネルのデフォルトのアクティブ化スケジュールを定義し、ディスプレイのすべての割り当てにデフォルトとして使用できるようになります。これにより、煩雑なスケジュール定義を繰り返す必要がなくなります。

1. [Screens サービスプロバイダー](https://experience.adobe.com/screens)に移動します。

### チャネルのデフォルトの割り当ての詳細を作成 {#create-default}

1. 設定するチャネルの詳細ページに移動します。
1. ページの&#x200B;**デフォルトの割り当ての詳細**&#x200B;タイルを見つけます。

   ![画像](/help/screens-cloud/assets/display/Assignment1.png)

1. 「**デフォルトの詳細を設定**」をクリックします。
1. 優先度、開始日と終了日、チャネルの繰り返しパターンなど、デフォルトの割り当ての詳細を設定し、「**割り当て**」をクリックします。

   ![画像](/help/screens-cloud/assets/display/Assignments2.png)

1. 割り当ての詳細が、**デフォルトの割り当ての詳細**&#x200B;タイルに表示されます。

   ![画像](/help/screens-cloud/assets/display/Assignments3.png)

このタイルには、次の情報が表示されます。

* ディスプレイ内のチャネルのデフォルトの優先度。
* チャネルの再生がスケジュールされている場合のアクティベーションの開始日と終了日。
* 繰り返しの合成ビュー（時間／日／週／月／年ごと、およびその繰り返しに付けられた名前）。

### ディスプレイに割り当てる際にデフォルトの割り当ての詳細を使用 {#default-display}

デフォルトの割り当て詳細があるチャネルは、通常のチャネルと同じ方法で表示でき、カスタムチャネルを毎回手動で定義する代わりに、デフォルトの割り当て詳細を使用するオプションが追加されます。

1. チャネルを割り当てるディスプレイの詳細ページに移動し、「**チャネルを割り当て**」をクリックします。
または、[在庫](https://experience.adobe.com/screens/displays)表示で目的のディスプレイを選択し、「**チャネルを割り当て**」をクリックします。
1. チャネル割り当てダイアログが開きます。

   ![画像](/help/screens-cloud/assets/display/Assignments4.png)

1. デフォルトの割り当ての詳細がある目的のチャネルをチャネルピッカーから選択します。
1. チャネル割り当てダイアログが変わり、デフォルトまたはカスタムの割り当て詳細を選択できます。

   ![画像](/help/screens-cloud/assets/display/Assignments5.png)

1. 「**割り当て**」をクリックして割り当てを最終決定するか、特定の表示のコンテキストで、デフォルトを他の値で上書きする場合は、「**カスタム割り当ての詳細を設定**」をクリックします。

   ![画像](/help/screens-cloud/assets/display/Assignments6.png)

1. **割り当てられたチャネル**&#x200B;タイルが新しい割り当てで更新されます。

   ![画像](/help/screens-cloud/assets/display/Assignments7.png)

1. チャネルは、カスタムスケジュール（時計アイコン）を使用しているか、デフォルトの詳細（世界時計アイコン）を継承しているかに応じて異なるアイコンが表示され、アイコンをクリックするとスケジュールの詳細が表示されます。
1. また、各タイプで使用可能なアクションは異なることに注意してください。

   ![画像](/help/screens-cloud/assets/display/Assignments8.png)

**メモ：**&#x200B;デフォルトの割り当ての詳細を使用するチャネル割り当ては、ディスプレイのコンテキストでは編集できません。

* カスタム割り当てに変更する必要がある場合は、まず割り当てを削除し、次に「**カスタム割り当ての詳細を設定**」オプションを使用して再度追加する必要があります。
* デフォルトの割り当ての詳細のプロパティを変更する必要がある場合は、チャネルの詳細ページから直接変更します。

### チャネルからデフォルトの割り当ての詳細を削除 {#remove-display}

1. デフォルトの割り当て詳細を削除するチャネルの詳細ページに移動します。
1. ページの&#x200B;**デフォルトの割り当ての詳細**&#x200B;タイルを見つけます
1. 「**デフォルトを削除**」をクリックします。

   ![画像](/help/screens-cloud/assets/display/Assignments9.png)

1. 確認ダイアログが表示され、詳細が次の条件のいずれかに一致します。
   **a.** チャネルはどのディスプレイにも使用されていません。

   ![画像](/help/screens-cloud/assets/display/Assignments10.png)

**b.** チャネルは 1 つのディスプレイで使用されています。

![画像](/help/screens-cloud/assets/display/Assignment11.png)

**c.** チャネルは複数のディスプレイで使用されています。

![画像](/help/screens-cloud/assets/display/Assignments12.png)

1. 「*削除*」をクリックして変更を確定します。

**注意：**チャネルからデフォルトの割り当ての詳細を削除すると、それを使用していたすべてのディスプレイの一致する割り当てが削除されます。
その結果、代替コンテンツがディスプレイに再生されない場合は、空白の画面が表示される可能性があります。

## 次の手順 {#whats-next}

プロジェクトで AEM Screens チャネルを設定したら、チャネルを公開する必要があります。Screens サービスプロバイダーからプレーヤーを管理する前に、[Screens as a Cloud Service でのチャネルの公開](manage-publish.md)を参照してください。
