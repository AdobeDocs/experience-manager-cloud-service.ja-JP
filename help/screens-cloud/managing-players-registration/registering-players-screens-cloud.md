---
title: Screens as a Cloud Service へのプレーヤーの登録
description: ここでは、Screens as a Cloud Service にプレーヤーを登録する方法について説明します。
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 100%

---

# Screens as a Cloud Service へのプレーヤーの登録 {#registering-players-screens-cloud}

Screens as a Cloud Service にプレーヤーをインストールして設定したら、プレーヤーを登録する必要があります。

## 目的 {#objective}

このドキュメントでは、Screens サービスプロバイダーへのプレーヤーの登録について説明します。学習目標は次のとおりです。

* プレーヤーの登録方法を理解する
* Screens Services Provider からの登録プロセスを完了する

## Screens Player の登録手順 {#register-players}

プレーヤーを Screens as a Cloud Service にインストールしたら、Screens サービスプロバイダーからプレーヤーを登録する準備が整います。

以下の手順に従って、プレーヤーを登録します。

1. Screens サービスプロバイダーにログインします。

1. 左側のナビゲーションパネルから「**プレーヤー管理**」の下の「**登録コード**」に移動し、「**コードを作成**」をクリックします。

   >[!NOTE]
   >有効なコードまたは期限切れでないコードが存在しない場合は、「コードを作成」をクリックし、コードの名前を入力し、必要に応じて有効期限の設定を選択します。

   ![画像](/help/screens-cloud/assets/player/register-player1.png)

1. **登録コードを作成**&#x200B;ダイアログボックスで次のフィールドに値を入力します。

   ![画像](/help/screens-cloud/assets/player/register-player2.png)

   1. **登録コード名**：登録コードの名前
   1. **登録コードの有効期限**：登録録コードの有効期限
   1. **使用制限**：登録コードの使用制限をオフにするには、ボタンで切り替えます。デフォルトでは、「使用制限」オプションはオフになっています。
   1. **使用制限**：使用制限の値を選択します

1. 「**作成**」をクリックして、登録コードを作成します。プレーヤーと登録コードがリストに表示されます。

   ![画像](/help/screens-cloud/assets/player/register-player3.png)

1. 「**登録コード**」列の下の値をクリックしてクリップボードにコピーします。

1. この値を、AEM Screens プレーヤーの管理 UI の「**プレーヤーの登録**」タブの「**コードの入力**」フィールドにペーストし、「**登録**」をクリックします。

   ![画像](/help/screens-cloud/assets/player/register-player4.png)


1. コードを追加すると、プレーヤーの管理 UI からプレーヤーが登録されたことを確認できます。

   ![画像](/help/screens-cloud/assets/player/register-player5.png)

1. このプレーヤーは、左側のナビゲーションパネルの「**プレーヤー**」に表示されます。Screens サービスプロバイダーに表示されるコードは、管理 UI の&#x200B;**システム情報**&#x200B;パネルのプレーヤーコードと一致します。

   ![画像](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >**登録コードを使用する際のセキュリティのベストプラクティスに関するレコメンデーション**
   >ベストプラクティスとして、登録コードの使用を制限できます。登録コードが侵害を受けても、登録数が 100 件に制限されていると、攻撃者はその数までは登録できますが、それ以上は登録できません。登録コードが作成され、顧客のプレーヤーの一部が既に登録されている場合でも、いつでも使用制限を更新できます。特定の登録コードに対して異常な登録アクティビティがあることを顧客が観測した場合、既に登録されているプレーヤーに影響を与えることなく、リアルタイムで制限を下げつつ調査を行い、誤検知の場合は元通りに制限を増やすことができます。


## 次の手順 {#whats-next}

これで、プレーヤーをインストールしてクラウドモードに設定できました。次に、Screens サービスプロバイダーの「[Screens as a Cloud Service のディスプレイへのプレーヤーの割り当て](/help/screens-cloud/managing-players-registration/assigning-player-display.md)」ドキュメントを確認して、Screens as a Cloud Service ジャーニーを続けてください。
