---
title: 通知
description: Adobe Experience Cloud通知システムを使用して、パイプラインデプロイメントに関する情報を受け取る方法を説明します。
exl-id: c1c740b0-c873-45a8-9518-a856db2be75b
source-git-commit: 42d4e3bb38e3a7ecb4507d15e2307ed08d752b5c
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---

# 通知 {#notifications}

[!UICONTROL Cloud Manager] 実稼動デプロイメント中に、実稼動パイプラインの開始時および（正常または失敗時に）通知を受け取ることができます。

これらの通知は、Adobe [!UICONTROL Experience Cloud] 役割を持つユーザーへの通知システム **ビジネスオーナー**, **プログラムマネージャ**、および **デプロイメントマネージャー**.

通知は、 [!UICONTROL Cloud Manager] UI およびAdobe全体 [!UICONTROL Experience Cloud].

![メニューバーの通知アイコン](assets/notify-1.png)

新しい通知がある場合、ベルのアイコンにバッジが付きます。 通知を表示するには、通知をクリックしてパネルを開きます。

![通知の表示](assets/notify-2.png)

パネルには、最新の通知のみが表示されます。 クリック **すべて表示** をクリックして、すべての通知を表示します。

## 電子メール通知 {#email-notifications}

デフォルトでは、Adobe [!UICONTROL Experience Cloud] ソリューションの ユーザーインターフェイスで通知を確認できます。また、個々のユーザーは、次の手順に従うことで、これらの通知を電子メールで送信することをオプトできます。

1. 通知を表示するには、ベルアイコンをクリックします。
1. をクリックします。 **環境設定を編集** 通知パネルの上部にあるアイコン（歯車のような形状）。
1. 表示されるウィンドウで、「 **通知** をクリックします。
   ![環境設定ウィンドウを編集](assets/notification-preferences.png)
1. 下にスクロールして **電子メール** 見出し。
   ![E メールオプション](assets/email-preferences.png)
1. メールの受信方法を選択します。
   * E メールを送信しない（デフォルト）
   * インスタント通知
   * 日別ダイジェスト
   * 毎週のダイジェスト

選択を行うと、選択内容が自動的に保存されます。保存ボタンや適用ボタンをクリックする必要はありません。
