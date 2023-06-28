---
title: Screens as a Cloud Service におけるディスプレイへのチャネルの割り当て
description: ここでは、Screens as a Cloud Service でディスプレイにチャネルを割り当てる方法について説明します。
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 62%

---

# Screens as a Cloud Service におけるディスプレイへのチャネルの割り当て {#assign-channel-displays-screens-cloud}

プロジェクトの設定が完了したら、チャネルをディスプレイに割り当てて、コンテンツを表示する必要があります。

## 目的 {#objective}

このドキュメントでは、ディスプレイの準備が整い、チャネルにコンテンツを追加して公開した後に、ディスプレイにチャネルを割り当てる方法を説明します。読み終えたら、Screens Services Provider からディスプレイにチャネルを割り当てる方法を理解できるようになります。

## 前提条件 {#prerequisites}

以下の手順を実行してディスプレイにチャネルを割り当てる前に、次のトピックの学習が完了している必要があります。

* ディスプレイの作成と管理
* チャネルの作成と管理

## ディスプレイにチャネルを割り当てる手順 {#assign-channel-to-display}

ディスプレイにチャネルを割り当てるには、次の手順に従います。

1. Screens サービスプロバイダーに移動し、左側のナビゲーションパネルから「**ディスプレイ**」を選択します。

1. クリック **チャネルを割り当て** をディスプレイに追加します。

   ![画像](/help/screens-cloud/assets/display/assignchannel-1.png)

1. **チャネルの割り当て**&#x200B;ダイアログボックスで以下のフィールドに入力します。

   ![画像](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. ドロップダウンからチャネル名を選択します。
   1. 優先度を選択します。

      >[!NOTE]
      >優先度は、複数の割り当てが再生条件に一致する場合に、割り当ての順序付けを行うために使用します。最も大きい値を持つものが、低い値よりも常に優先されます。 例えば、2 つのチャネル A と B がある場合、A の優先度が 1、B の優先度が 2 となると、チャネル B は A よりも優先度が高いので、表示されます。

   1. **アクティベーション**&#x200B;から開始日と終了日を選択します。

1. クリック **+繰り返しを追加** ：チャネルの繰り返しスケジュールを追加します。

   ![画像](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >チャネルには、複数の繰り返しスケジュールを追加できます。繰り返しスケジュールでは、ある日の特定の時間に実行される複数のチャネルでグローバルスケジュールを設定でき、また一度にすべてのディスプレイで設定を再利用できる日分割を導入します。

   以下のオプションを設定できます。

   * **名前**：繰り返しスケジュールのタイトル。
   * **繰り返し**：スケジュールを日別、週別、月別、年別のどれで実行するかを選択します。
   * **開始**：スケジュールの開始時間。
   * **終了**：スケジュールの終了時間。時間または期間別に設定できます。
   * **時間**:スケジュールは指定した時刻に終了します。
   * **期間**：スケジュールは、特定の期間（時間または分単位）に実行されます。

1. 「**作成**」をクリックします。下の図に示すように、そのディスプレイにチャネルが割り当てられています。

   ![画像](/help/screens-cloud/assets/display/assignchannel-3.png)


## 次の手順 {#whats-next}

これでディスプレイにチャネルを割り当てたので、次に [AEM as a Cloud Service の Screens Player のインストールと設定](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md)を参照して、Screens as a Cloud Service のジャーニーを続行してください。
