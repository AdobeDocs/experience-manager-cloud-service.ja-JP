---
title: Screens as a Cloud Service でのチャネルの作成と管理
description: ここでは、Screens as a Cloud Service でチャネルを作成および管理する方法について説明します。
source-git-commit: 3a636a512da40f9a577d25399d33f96d8f6ad8a0
workflow-type: ht
source-wordcount: '550'
ht-degree: 100%

---


# Screens as a Cloud Service でのチャネルの作成と管理 {#creating-channels-screens-cloud}

AEM Screensプロジェクトを作成したら、チャネルを作成する必要があります。
***チャネル***：コンテンツのシーケンス（画像やビデオ）、Web サイト、または単一ページアプリケーションを表示します。

## 目的 {#objective}

このドキュメントでは、Screens コンテンツプロバイダーでの AEM Screens プロジェクトのチャネルの作成と管理について説明します。読み終わると、次ができるようになります。

* Screens コンテンツプロバイダーへのチャネルを作成する方法を理解する
* チャネル内のコンテンツを管理し編集する

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


## 次の手順 {#whats-next}

プロジェクトで AEM Screens チャネルを設定したら、チャネルを公開する必要があります。Screens サービスプロバイダーからプレーヤーを管理する前に、[Screens as a Cloud Service でのチャネルの公開](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/manage-publish.html?lang=ja)を参照してください。