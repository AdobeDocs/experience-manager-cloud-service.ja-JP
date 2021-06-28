---
title: Screensでのディスプレイへのチャネルの割り当て(Cloud Service)
description: ここでは、ScreensでチャネルをディスプレイにCloud Serviceとして割り当てる方法について説明します。
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 41%

---


# Screensでのディスプレイへのチャネルの割り当て(Cloud Service) {#assign-channel-displays-screens-cloud}

プロジェクトの設定が完了したら、チャネルをディスプレイに割り当てて、コンテンツを表示する必要があります。

## 目的 {#objective}

このドキュメントでは、ディスプレイの準備が整い、チャネルにコンテンツを追加して公開した後に、ディスプレイにチャネルを割り当てる方法を説明します。 読み終えたら、Screensサービスプロバイダーからディスプレイにチャネルを割り当てる方法を理解できるようになります。

## 前提条件 {#prerequisites}

以下の手順を実行してチャネルをディスプレイに割り当てる前に、学習が完了している必要があります。

* ディスプレイの作成と管理
* チャネルの作成と管理

## ディスプレイにチャネルを割り当てる手順 {#assign-channel-to-display}

下の手順に従ってチャネルをディスプレイに割り当てます。

1. Screens Services Providerに移動し、左側のナビゲーションパネルから「**ディスプレイ**」を選択します。

1. 「**チャネルを割り当て**」をクリックします。

   ![画像](/help/screens-cloud/assets/display/assignchannel-1.png)

1. **チャネルの割り当て**&#x200B;ダイアログボックスで以下のフィールドに入力します。

   ![画像](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. ドロップダウンからチャネル名を選択します。
   1. 優先度を選択します。

      >[!NOTE]
      >優先度は、複数の割り当てが再生条件に一致する場合に、割り当ての順序付けをおこなうために使用します。最高値のものが低い値よりも常に優先されます。例えば、2 つのチャネル A と B がある場合、A の優先度が 1 で B の優先度が 2 であるなら、A より優先度が高いために、チャネル B が表示されます。
   1. **Activation**&#x200B;から開始日と終了日を選択します。

1. 「 **+繰り返しを追加** 」をクリックして、チャネルの繰り返しスケジュールを追加します。

   ![画像](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >チャネルには、複数の繰り返しスケジュールを追加できます。繰り返しスケジュールでは、1日の特定の時間に実行される複数のチャネルでグローバルスケジュールを設定でき、また一度にすべてのディスプレイでその設定を再使用できる日分割を導入します。

   以下のオプションを設定できます。

   * **名前**：繰り返しスケジュールのタイトル。
   * **繰り返し**：スケジュールを日別、週別、月別、年別のどれで実行するかを選択します。
   * **開始**：スケジュールの開始時間。
   * **終了**：スケジュールの終了時間。時間または期間別に設定できます。
   * **時間**：スケジュールは指定した時刻に終了します。
   * **期間**：スケジュールは、特定の期間（時間または分単位）に実行されます。

1. 「**作成**」をクリックすると、下の図に示すように、そのディスプレイにチャネルが割り当てられたことがわかります。

   ![画像](/help/screens-cloud/assets/display/assignchannel-3.png)


## 次の手順 {#whats-next}

これでチャネルをディスプレイに割り当てたので、次に『[AEM用のScreens Playerのインストールと設定](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md)』をCloud Serviceとして確認し、ScreensをCloud Serviceジャーニーとして続行する必要があります。
