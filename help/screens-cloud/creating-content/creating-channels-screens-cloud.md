---
title: Cloud ServiceとしてのScreensでのチャネルの作成と管理
description: ここでは、ScreensでチャネルをCloud Serviceとして作成および管理する方法について説明します。
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 16%

---


# Cloud ServiceとしてのScreensでのチャネルの作成と管理 {#creating-channels-screens-cloud}

AEM Screensプロジェクトを作成したら、チャネルを作成する必要があります。
***チャネル***、コンテンツのシーケンス（画像やビデオ）、Webサイトまたは単一ページアプリケーションの表示を行います。

## 目的 {#objective}

このドキュメントでは、ScreensコンテンツプロバイダーでのAEM Screensプロジェクトのチャネルの作成と管理について説明します。 読み終えたら、次の操作を行う必要があります。

* Screens Content Providerへのチャネルを作成する方法を説明します。
* チャネル内のコンテンツの管理と編集

## Screensでの新しいシーケンスチャネルのCloud Service {#create-new-channel}

>[!NOTE]
>**前提条件**
>このガイドの節を開始する前に、[Screensでのプロジェクトの作成と管理(Cloud Serviceとして)](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md)を参照してください。

以下の手順に従って、ScreensでCloud Serviceとして新しいシーケンスチャネルを作成します。

1. Screensコンテンツプロバイダーに移動します。

1. *FirstDigitalExperience*&#x200B;など、AEM Screensプロジェクトに移動します。

1. **FirstDigitalExperience** —> **チャネル**&#x200B;など、プロジェクトから&#x200B;**チャネル**&#x200B;フォルダーを選択し、アクションバーの「**作成**」をクリックします。

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. **作成**&#x200B;ウィザードで&#x200B;**シーケンスチャネル**&#x200B;などのテンプレートを選択し、「**次へ**」をクリックします。

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > **作成**&#x200B;ウィザードは、チャネルの作成時に様々なタイプのテンプレートを提供します。 詳しくは、作成ウィザードの「使用可能なテンプレート[」の節を参照してください。](#available-templates)

1. **LoopingChannelOne**&#x200B;などのシーケンスチャネルの名前を入力し、「**作成**」をクリックします。

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   これで、AEM Screensプロジェクトのチャネルフォルダーに&#x200B;**LoopingChannelOne**&#x200B;が表示されます。

   チャネルを作成したら、チャネルにコンテンツを追加できます。 チャネルにアセット（画像/ビデオ）を追加する方法については、 [チャネルへのコンテンツの追加](#add-content)を参照してください。

## チャネルの管理 {#managing-channels}

プロパティおよびダッシュボードを編集および表示でき、またチャネルをコピー、プレビュー、削除できます。

次の図に示すように、プロジェクトからチャネルに移動し、チャネルを選択します。 チャネルの編集、プロパティの表示、コンテンツのプレビュー、公開の管理、チャネルの削除などのオプションをアクションバーから選択できるようになりました。

![](/help/screens-cloud/assets/create-content/channelprop1.png)

### チャネルへのコンテンツの追加 {#add-content}

チャネルにコンテンツを追加するには、下の手順に従います。

1. 次の図に示すように、編集するチャネルを選択します。 アクションバーの左上隅の「**編集**」をクリックして、エディターを開きます。

   ![](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. エディターを使用すると、公開するチャネルにアセットやコンポーネントを追加できます。

1. 左側のパネルからアセットをドラッグ&amp;ドロップし、エディターに追加します。

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


## 次の手順 {#whats-next}

プロジェクトでAEM Screensチャネルを設定したら、チャネルを公開する必要があります。 Screensサービスプロバイダーからプレーヤーを管理する前に、Cloud ServiceとしてのScreensの[チャネルの公開](/help/screens-cloud/creating-content/manage-publish.md)を参照してください。