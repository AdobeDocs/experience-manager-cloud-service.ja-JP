---
title: Screens as a Cloud Service におけるディスプレイへのチャネルの割り当て
description: ここでは、Screens as a Cloud Service でディスプレイにチャネルを割り当てる方法について説明します。
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: ht
source-wordcount: '452'
ht-degree: 100%

---

# Screens as a Cloud Service におけるディスプレイへのチャネルの割り当て {#assign-channel-displays-screens-cloud}

プロジェクトの設定が完了したら、コンテンツを表示するディスプレイにチャネルを割り当てる必要があります。

## 目的 {#objective}

このドキュメントでは、ディスプレイの準備が整い、チャネルにコンテンツを追加して公開した後に、ディスプレイにチャネルを割り当てる方法を説明します。Screens サービスプロバイダーからディスプレイにチャネルを割り当てる方法を理解できるようになります。

## 前提条件 {#prerequisites}

以下の手順を実行してディスプレイにチャネルを割り当てる前に、次のトピックの学習が完了している必要があります。

* ディスプレイの作成と管理
* チャネルの作成と管理

## ディスプレイにチャネルを割り当てる手順 {#assign-channel-to-display}

ディスプレイにチャネルを割り当てるには、次の手順に従います。

1. Screens サービスプロバイダーに移動し、左側のナビゲーションパネルから「**ディスプレイ**」を選択します。

1. 「**チャネルを割り当て**」をクリックします。

   ![画像](/help/screens-cloud/assets/display/assignchannel-1.png)

1. **チャネルの割り当て**&#x200B;ダイアログボックスで以下のフィールドに入力します。

   ![画像](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. ドロップダウンからチャネル名を選択します。
   1. 優先度を選択します。

      >[!NOTE]
      >優先度は、複数の割り当てが再生条件に一致する場合に、割り当ての順序付けを行うために使用します。最高値のものが低い値よりも常に優先されます。例えば、2 つのチャネル A と B がある場合、A の優先度が 1 で B の優先度が 2 であるなら、A より優先度が高いために、チャネル B が表示されます。
   1. **アクティベーション**&#x200B;から開始日と終了日を選択します。

1. 「**+ 繰り返しを追加**」をクリックして、チャネルに繰り返しスケジュールを追加します。

   ![画像](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >チャネルには、複数の繰り返しスケジュールを追加できます。繰り返しスケジュールでは日分割が導入されています。この方式では、特定の時間帯に複数のチャネルが実行されるグローバルスケジュールを設定でき、また一度にすべてのディスプレイでその設定を再利用できます。

   以下のオプションを設定できます。

   * **名前**：繰り返しスケジュールのタイトル。
   * **繰り返し**：スケジュールを日別、週別、月別、年別のどれで実行するかを選択します。
   * **開始**：スケジュールの開始時間。
   * **終了**：スケジュールの終了時間。時間または期間別に設定できます。
   * **時間**：スケジュールは指定した時刻に終了します。
   * **期間**：スケジュールは、特定の期間（時間または分単位）に実行されます。

1. 「**作成**」をクリックすると、そのディスプレイにチャネルが割り当てられたことがわかります（下図を参照）。

   ![画像](/help/screens-cloud/assets/display/assignchannel-3.png)


## 次の手順 {#whats-next}

これでディスプレイにチャネルを割り当てたので、次に [AEM as a Cloud Service の Screens Player のインストールと設定](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md)を参照して、Screens as a Cloud Service のジャーニーを続行してください。
