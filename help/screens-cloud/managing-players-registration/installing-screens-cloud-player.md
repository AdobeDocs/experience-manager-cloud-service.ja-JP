---
title: ScreensでのプレーヤーのインストールとCloud Service
description: ここでは、ScreensでプレーヤーをCloud Serviceとしてインストールおよび設定する方法について説明します。
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 2%

---


# ScreensでのプレーヤーのインストールとCloud Service {#installing-players-screens-cloud}

この節では、オンプレミスのAEMインスタンスに登録されているAEM Screens Playerのインストール方法について説明します。 さらに、既存のプレーヤーのファクトリリセットを実行し、新しいプレーヤーをAEM ScreensにCloud Serviceとして登録する必要があります。

## 目的 {#objective}

このドキュメントでは、プレーヤーを登録する前にプレーヤーを設定する方法を説明します。 読み終えたら、次の内容を理解できるようになります。

* プレーヤーのインストール元
* プレーヤーをクラウドモードに更新する方法

## プレーヤーをクラウドモードに設定する手順 {#cloud-mode-setup}

[AEM Screens Playerのダウンロード](https://download.macromedia.com/screens/)から最新のプレーヤーをダウンロードしたら、プレーヤーをCloudモードに更新する準備が整いました。

以下の手順に従って、プレーヤーを更新します。

1. AEM Screens Playerを開きます。

   >[!NOTE]
   >専用のハードウェアデバイスでテストするか、独自のプレーヤーのWeb拡張機能でテストするかを選択できます。

1. 「**設定**」タブをクリックし、「**リセット**」オプションの下の「**To Factory**」ボタンをクリックします。

   ![画像](/help/screens-cloud/assets/player/installplayer-2.png)

1. **確認**&#x200B;をクリックして、プレーヤーをリセットします。

1. 「**設定**」タブから、「**実行モードを切り替え**」オプションの下の「**クラウドモードに変更**」ボタンをクリックします。

   ![画像](/help/screens-cloud/assets/player/installplayer-1.png)

1. クラウドモードに切り替えると、**確認**&#x200B;をクリックすると、プレーヤーの登録が解除されます。

## 次の手順 {#whats-next}

これで、プレーヤーをCloud Serviceモードに設定できました。次に、Screensサービスプロバイダーの[Cloud ServiceとしてのScreensへのプレーヤーの登録](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md)ドキュメントを確認し、Screensをクラウドジャーニーとして続行する必要があります。