---
title: Cloud ServiceとしてのScreensへのプレーヤーの登録
description: ここでは、Screensにプレーヤーを登録する方法について説明します。Cloud Service
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 2%

---


# Cloud ServiceとしてのScreensへのプレーヤーの登録 {#registering-players-screens-cloud}

Screens用のプレーヤーをインストールしてCloud Serviceに設定したら、プレーヤーを登録する必要があります。

## 目的 {#objective}

このドキュメントは、Screensサービスプロバイダーへのプレーヤーの登録について説明します。 読み終えた後、次の操作を実行できます。

* プレーヤーの登録方法を理解する
* Screens Services Providerからの登録プロセスを完了する方法

## Screens Playerの登録手順 {#register-players}

プレーヤーをCloud ServiceとしてScreensにインストールしたら、Screensサービスプロバイダーからプレーヤーを登録する準備が整います。

以下の手順に従って、プレーヤーを登録します。

1. Screensサービスプロバイダーにログインします。

1. 左側のナビゲーションパネルから&#x200B;**プレーヤー管理**&#x200B;の下の&#x200B;**登録コード**&#x200B;に移動し、**コードを作成**&#x200B;をクリックします。

   >[!NOTE]
   >有効なコードまたは期限切れでないコードが存在しない場合は、「コードを作成」をクリックし、コードの名前を入力し、必要に応じて有効期限設定を選択します。

   ![画像](/help/screens-cloud/assets/player/register-player1.png)

1. **登録コード**&#x200B;を作成ダイアログボックスで次のフィールドに値を入力します。

   ![画像](/help/screens-cloud/assets/player/register-player2.png)

   1. **登録コード名**:登録コードの名前
   1. **登録コードの有効期限**:登録コードの有効期限
   1. **使用の制限**:ボタンを切り替えて、登録コードの使用制限を切り替えます。デフォルトでは、「使用量を制限」オプションはオフになっています。
   1. **使用制限**:使用制限の数を選択します

1. 「**作成**」をクリックして、登録コードを作成します。 登録コードがリストに表示されたプレーヤーが表示されます。

   ![画像](/help/screens-cloud/assets/player/register-player3.png)

1. 列&#x200B;**登録コード**&#x200B;の下の値をクリックして、値をクリップボードにコピーします。

1. この値を&#x200B;**「コード** 」フィールドに貼り付け、AEM Screens Playerの管理UIの「**プレーヤーの登録**」タブで、「**登録**」をクリックします。

   ![画像](/help/screens-cloud/assets/player/register-player4.png)


1. コードを追加すると、プレーヤーのAdmin UIから登録済みが表示されます。

   ![画像](/help/screens-cloud/assets/player/register-player5.png)

1. 左側のナビゲーションパネルから、このプレーヤーが&#x200B;**プレーヤー**&#x200B;に表示されます。 Screensサービスプロバイダーに表示されるコードは、プレーヤーコードの下にあるAdmin UIの&#x200B;**システム情報**&#x200B;パネルと一致します。

   ![画像](/help/screens-cloud/assets/player/register-player6.png)

## 次の手順 {#whats-next}

これで、プレーヤーをCloud Serviceモードに設定できました。次に、Screensサービスプロバイダーの「Cloud ServiceとしてのScreensのディスプレイへのプレーヤーの割り当て[」のドキュメントを確認し、Screensをクラウドジャーニーとして続行する必要があります。](/help/screens-cloud/managing-players-registration/assigning-player-display.md)