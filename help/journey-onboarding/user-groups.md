---
title: 通知用のユーザーグループ
description: 重要な電子メール通知の受信を管理するために、Admin Consoleでユーザーグループを作成する方法を説明します。
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 93a5e1b8851353f368a01ea6b50265ec3f2de836
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 17%

---


# 通知用のユーザーグループ {#user-groups}

重要な電子メール通知の受信を管理するために、Admin Consoleでユーザーグループを作成する方法を説明します。

## 概要 {#overview}

時々、Adobeは、AEMのas a Cloud Service環境に関してに連絡する必要があります。 Adobeは、製品内通知に加えて、このような通知に E メールを使用する場合もあります。 このような通知には次の 2 種類があります。

* **インシデント通知 —Cloud Service**  — これらの通知は、インシデント発生時またはAdobeがAEM as a Cloud Service環境で可用性の問題を特定した際に送信されます。
* **事前通知 —Cloud Service**  — これらの通知は、Adobeサポートチームのメンバーが、AEMのas a Cloud Service環境に役立つ潜在的な最適化または推奨事項に関するガイダンスを提供したい場合に送信されます。

正しいユーザーがこれらの通知を受け取るには、ユーザーグループを設定する必要があります。

## 前提条件 {#prerequisites}

ユーザーグループはAdmin Console内で作成および管理されるので、通知用のユーザーグループを作成する前に、次の操作を行う必要があります。

* グループメンバーシップを追加および編集する権限を持っている。
* 有効なAdobe Admin Consoleプロファイルがある。

## 新しい Cloud Manager 製品プロファイルの作成 {#create-groups}

通知の受信を適切に設定するには、2 つのユーザーグループを作成する必要があります。 これらの手順は、1 回のみ実行する必要があります。

1. 次の場所でAdmin Consoleにログイン [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. **概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」を選択します。

   ![ユーザーグループ](assets/products_services.png)

1. すべてのインスタンスのリストから **Cloud Manager** インスタンスを選択して、そこに移動します。

   ![ユーザーグループを作成](assets/cloud_manager_instance.png)

1. 設定済みのすべての Cloud Manager 製品プロファイルのリストが表示されます。 次に例を示します。

   ![ユーザーグループを作成](assets/cloud_manager_profiles.png)

1. クリック **新しいプロファイル** 次の詳細を紹介します。

   * 製品プロファイル名：インシデント通知 —Cloud Service
   * 表示名：インシデント通知 —Cloud Service
   * 説明：インシデント発生時またはAdobeがAEM as a Cloud Service環境で可用性の問題を特定した場合に通知を受け取るユーザーの Cloud Manager プロファイル。

1. クリック **保存** 手順 5 を繰り返し、次の詳細を示します。

   * 製品プロファイル名：事前通知 —Cloud Service
   * 表示名：事前通知 —Cloud Service
   * 説明：AdobeサポートチームメンバーがAEMas a Cloud Service環境の設定に関して潜在的な最適化や推奨事項に関するガイダンスを提供したい場合に通知を受け取るユーザーの Cloud Manager プロファイルです。

>[!NOTE]
>
>Cloud Manager のプロファイル名は、上記とまったく同じにすることが重要です。 提供された説明から製品プロファイル名をコピーして貼り付けてください。 偏差や入力ミスがあれば、通知は必要に応じて送信されません。 エラーが発生した場合や、プロファイルが定義されていない場合、Adobeは、Cloud Manager 開発者（ 、 、または）に割り当てられた既存のユーザーにデフォルトで通知します。

## ユーザーを新しい通知製品プロファイルに割り当て {#add-users}

グループが作成されたら、適切なユーザーを割り当てる必要があります。 これは、新しいユーザーを作成する際に実行するか、既存のユーザーを更新する際に実行できます。

### グループに新しいユーザーを追加 {#new-user}

1. インシデントまたは事前通知を受け取るユーザーを特定します。

1. 次の場所でAdmin Consoleにログイン [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) まだログインしていない場合は、をクリックします。

1. **概要**&#x200B;ページで、**製品とサービス**&#x200B;カードから「**Adobe Experience Manager as a Cloud Service**」を選択します。

   ![ユーザー](assets/product_services.png)

1. 上部ナビゲーションの「**ユーザー**」タブを選択し、「**ユーザーを追加**」を選択します。

![ユーザー](assets/cloud_manager_add_user.png)

1. **チームにユーザーを追加**&#x200B;ダイアログで、追加するユーザーの電子メール ID を入力します。

   * チームメンバーの Federated ID がまだセットアップされていない場合は、「ID タイプ」として「Adobe ID」を選択します。
   * ユーザーが既に存在する場合は、手順 9 を参照してください。

1. の下のプラスボタンをクリックします。 **製品を選択** 製品選択を開始し、「 」を選択する見出し **Adobe Experience Manager as a Cloud Service** を **インシデント通知 —Cloud Service** または **事前通知 —Cloud Service**&#x200B;またはその両方をユーザーに割り当てます。

1. 「**保存**」をクリックすると、追加したユーザー宛に「ようこそ」の電子メールが送信されます。招待されたユーザーに通知が届きます。

1. 通知を受信するチームのユーザーに対して、これらの手順を繰り返します。

1. ユーザーが既に存在する場合は、ユーザーの名前を検索し、次の手順を実行します。

   * ユーザーの名前をクリックします。
   * 内 **製品** セクションで、 **編集**.
   * 鉛筆ボタンをクリックし、 **製品を選択** 製品選択を開始し、「 」を選択する見出し **Adobe Experience Manager as a Cloud Service** を **インシデント通知 —Cloud Service** または **事前通知 —Cloud Service**&#x200B;またはその両方をユーザーに割り当てます。
   * 「**保存**」をクリックすると、追加したユーザー宛に「ようこそ」の電子メールが送信されます。招待されたユーザーに通知が届きます。
