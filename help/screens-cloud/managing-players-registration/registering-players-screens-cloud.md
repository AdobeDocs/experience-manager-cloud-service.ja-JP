---
title: Cloud ServiceとしてのScreensへのプレーヤーの登録
description: ここでは、Screensにプレーヤーを登録する方法について説明します。Cloud Service
hide: true
hidefromtoc: true
index: false
source-git-commit: c65eeaf74ddfd81d37eb7090b84c8bf6f876dc72
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---


# Cloud Service{#registering-players-screens-cloud}としてのScreensへのプレーヤーの登録

Screens用のプレーヤーをインストールしてCloud Serviceに設定したら、プレーヤーを登録する必要があります。

## 目的 {#objective}

このドキュメントは、Screensサービスプロバイダーへのプレーヤーの登録について説明します。 読み終えた後は、次の操作を行う必要があります。

* プレーヤーの登録方法を説明します。
* 範囲に関して、AEM Screensプロジェクトでチャネルを管理できる。

## Screens Playerの登録手順{#register-players}

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

