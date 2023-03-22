---
title: 通知プロファイル
description: 重要な電子メール通知の受信を管理するAdmin Consoleでユーザープロファイルを作成する方法を説明します。
feature: Onboarding
role: Admin, User, Developer
exl-id: 4edecfcd-6301-4a46-98c7-eb5665f48995
source-git-commit: f7b3dec6380266a35f1bf7d90e0195277dd37335
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 71%

---


# 通知プロファイル {#notification-profiles}

重要な電子メール通知の受信を管理するAdmin Consoleでユーザープロファイルを作成する方法を説明します。

## 概要 {#overview}

アドビでは、場合によって、AEM as a Cloud Service 環境に関してユーザーに連絡する必要があります。アドビは、製品内通知に加えて、通知にメールを使用する場合もあります。 このようなメール通知には、次の 2 種類があります。

* **インシデント通知** - これらの通知は、インシデント発生時またはアドビが AEM as a Cloud Service 環境の可用性に関する潜在的な問題を特定した場合に送信されます。
* **事前通知** - これらの通知は、アドビのサポートチームメンバーが、AEM as a Cloud Service 環境に役立つ、潜在的な最適化や推奨事項に関するガイダンスを提供したい場合に送信されます。

正しいユーザーがこれらの通知を受け取るには、このドキュメントで説明するように、ユーザープロファイルを設定して割り当てる必要があります。

## 前提条件 {#prerequisites}

ユーザープロファイルはAdmin Console内で作成および管理されるので、通知用のプロファイルを作成する前に、次の操作をおこなう必要があります。

* メンバーシップを追加およびプロファイルする権限を持っている。
* 有効な Adobe Admin Console プロファイルがあること。

## 新しい Cloud Manager 製品プロファイルの作成 {#create-profiles}

通知の受信を適切に設定するには、2 つのユーザープロファイルを作成する必要があります。 これらの手順は、1 回のみ実行する必要があります。

1. [`https://adminconsole.adobe.com` ](https://adminconsole.adobe.com) で Admin Console にログインします。

1. 自分が正しい組織に属していることを確認します。

1. **概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」を選択します。

   ![Admin Console内の製品およびサービスのリスト](assets/products_services.png)

1. すべてのインスタンスのリストから **Cloud Manager** インスタンスを選択して、そこに移動します。

   ![Admin Console内のインスタンスのリスト](assets/cloud_manager_instance.png)

1. 設定済みのすべての Cloud Manager 製品プロファイルのリストが表示されます。

   ![Admin Console内の製品プロファイル](assets/cloud_manager_profiles.png)

1. 「**新規プロファイル**」をクリックし、次の詳細を入力します。

   * **製品プロファイル名**：`Incident Notification - Cloud Service`
   * **表示名**：`Incident Notification - Cloud Service`
   * **説明**：インシデント発生時またはアドビが AEM as a Cloud Service 環境の可用性に関する潜在的な問題を特定した場合に通知を受け取るユーザーの Cloud Manager プロファイル

1. 「**保存**」をクリックします。

1. 「**新規プロファイル**」をもう一度クリックし、次の詳細を入力します。

   * **製品プロファイル名**：`Proactive Notification - Cloud Service`
   * **表示名**：`Proactive Notification - Cloud Service`
   * **説明**：アドビのサポートチームメンバーが、AEM as a Cloud Service 環境設定で行う潜在的な最適化や推奨事項に関するガイダンスを提供したい場合に通知を受け取るユーザーの Cloud Manager プロファイル

1. 「**保存**」をクリックします。

2 つの新しい通知プロファイルが作成されます。

>[!NOTE]
>
>Cloud Manager **製品プロファイル名**&#x200B;が指定されたものとまったく同じであることが重要です。 エラーを避けるために、指定された製品プロファイル名をコピー＆ペーストしてください。 逸脱や入力ミスがあれば、通知が意図したとおりに送信されません。
>
>エラーが発生した場合やプロファイルが定義されていない場合、アドビはデフォルトで **Cloud Manager 開発者**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;プロファイルに割り当てられた既存のユーザーに通知します。

## 通知プロファイルにユーザーを割り当てる {#add-users}

プロファイルが作成されたら、適切なユーザーを割り当てる必要があります。 これは、新規ユーザーの作成時または既存ユーザーの更新時に実行できます。

### プロファイルへの新しいユーザーの追加 {#new-user}

Federated ID がまだ設定されていないユーザーを追加するには、次の手順に従います。

1. インシデントまたは事前通知を受け取るユーザーを特定します。

1. まだログインしていない場合は、[`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) で Admin Console にログインします。

1. 適切な組織が選択されていることを確認します。

1. **概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」を選択します。

   ![ユーザー](assets/product_services.png)

1. チームメンバーの Federated ID がまだ設定されていない場合は、上部のナビゲーションから「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。それ以外の場合は、「 」セクションにスキップします。 [既存のユーザーをプロファイルに追加します。](#existing-users)

   ![ユーザー](assets/cloud_manager_add_user.png)

1. **チームにユーザーを追加**&#x200B;ダイアログで、追加するユーザーのメール ID を入力し、「**ID タイプ**」に `Adobe ID` を選択します。

1. **製品を選択**&#x200B;見出しの下にあるプラスボタンをクリックして、製品の選択を開始します。 

1. 選択 **Adobe Experience Manager as a Cloud Service** 新しいプロファイルの 1 つまたは両方をユーザーに割り当てます。

   * **インシデント通知 - Cloud Service**
   * **事前通知 - Cloud Service**

1. 「**保存**」をクリックすると、追加したユーザーにお知らせメールが送信されます。

招待されたユーザーに通知が届くようになります。 通知を受信するチームのユーザーに対して、これらの手順を繰り返します。

### プロファイルへの既存のユーザーの追加 {#existing-user}

Federated ID が既に存在するユーザーを追加するには、次の手順に従います。

1. インシデントまたは事前通知を受け取るユーザーを特定します。

1. まだログインしていない場合は、[`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) で Admin Console にログインします。

1. 適切な組織が選択されていることを確認します。

1. **概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」を選択します。

1. 上部のナビゲーションから「**ユーザー**」タブを選択します。

1. 通知プロファイルに追加するチームメンバーの Federated ID が既に存在する場合は、リストでそのユーザーを探してクリックします。 それ以外の場合は、「 」セクションにスキップします。 [新しいユーザーをプロファイルに追加します。](#add-user)

1. ユーザー詳細ウィンドウの「**製品**」セクションで、省略記号ボタンをクリックし、「**編集**」を選択します。

1. **製品を編集**&#x200B;ウィンドウで、**製品を選択**&#x200B;見出しの下にある鉛筆ボタンをクリックして、製品の選択を開始します。

1. 選択 **Adobe Experience Manager as a Cloud Service** 新しいプロファイルの 1 つまたは両方をユーザーに割り当てます。

   * **インシデント通知 - Cloud Service**
   * **事前通知 - Cloud Service**

1. 「**保存**」をクリックすると、追加したユーザーにお知らせメールが送信されます。

招待されたユーザーに通知が届くようになります。 通知を受信するチームのユーザーに対して、これらの手順を繰り返します。
