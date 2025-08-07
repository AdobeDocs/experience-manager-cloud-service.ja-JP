---
title: Adobe Workfront Fusion とAEM Forms Submission の統合
description: Adobe Workfront Fusion を使用すると、繰り返しのタスクに重点を置くのではなく、新しいタスクに重点を置くことができます。フォーム送信を使用して、Adobe Workfront Fusion をアダプティブフォームに接続できます。
keywords: Adobe Workfront Fusion へのアダプティブフォームの送信、Adobe Workfront Fusion と AEM Forms Submission の統合、Adobe Workfront Fusion と AEM Forms の統合、Workfront Fusion と AEM Forms の統合、AEM Forms への Workfront Fusion の接続、AEM Forms Fusion への Workfront Fusion の接続 、AEM Forms への Workfront Fusion の接続方法?、フォームへの Workfront Fusion の接続
topic-tags: author, developer
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
role: Admin, User
exl-id: d3efb450-a879-40ae-8958-0040f99bdafc
source-git-commit: dabf8029577c5fb6bb5eebdbf10d77f3d4d95a5d
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 88%

---

# Adobe Workfront Fusion へのアダプティブフォームの送信

<span class="preview">機能は、早期導入プログラムで利用できます。早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID で aem-forms-ea@adobe.com までメールを送信してください。</span>

[Adobe Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html?lang=ja) は、ドキュメント承認ワークフロー、メールのフィルタリングや並べ替えなど、同じタスクを繰り返すプロセスを自動化し、繰り返しタスクではなく新しいタスクに焦点を当てることができます。Adobe Workfront Fusion には、複数のシナリオが含まれています。シナリオは、アプリケーションと web サービス間のデータ転送を実行する一連のモジュールで構成されます。シナリオでは、様々な手順（モジュール）を追加してタスクを自動化します。

例えば、Workfront Fusion を使用すると、シナリオを作成して、アダプティブフォームでデータを収集し、データを処理し、データをアーカイブ用にデータストアに送信できます。シナリオを設定すると、ユーザーがフォームに入力するたびに、Workfront Fusion は自動的にタスクを実行し、データストアをシームレスに更新します。

AEM Forms as a Cloud Service には、アダプティブフォームを Adobe Workfront Fusion に接続して送信するための OOTB コネクタが用意されています。フォームを Adobe Workfront Fusion に送信すると、次のようなメリットがあります。
* フォーム送信データを Workfront Fusion ワークフローへとシームレスに転送できるようになりました。
* フォーム送信によってトリガーされる様々なタスクを自動化するのに役立ちます。これには、プロジェクトの開始、特定のチームメンバーへのタスクの割り当て、通知の送信、プロジェクトステータスの更新などが含まれます。これらはすべて手動介入なしで実行できます。
* Workfront Fusion 内で取り込まれたすべてのフォーム送信では、プロジェクト関連情報の信頼できる単一の情報源を提供します。


<!--  AEM as a Cloud Service offers various out of the box submit actions for handling form submissions. You can learn more about these options in the [Adaptive Form Submit Action](/help/forms/configure-submit-actions-core-components.md)  article.-->

>[!VIDEO](https://video.tv.adobe.com/v/3427145/adaptive-forms-adobe-workfront-af-workfront-workfront-aem-forms/?quality=12&learn=on)

<span> このビデオは、コアコンポーネントにのみ適用されます。 UE/基盤コンポーネントについては、の記事を参照してください。</span>

## AEM Forms と Adobe Workfront Fusion を統合する前提条件 {#prerequisites}

Workfront Fusion と AEM Forms の間の接続を確立するには、以下が必要です。

* 有効な [Workfront および Workfront Fusion ライセンス](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/license-automation-vs-integration.html?lang=ja)。
* [サービス資格情報を取得する](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja)ために[開発者コンソール](https://my.cloudmanager.adobe.com/)へのアクセス権を持つ AEM ユーザー。

## AEM Forms と Adobe Workfront Fusion の統合

### &#x200B;1. Workfront シナリオの作成 {#workflow-scenario}

Workfront シナリオを作成するには、次の手順に従います。

1. [シナリオを作成](#create-scenario)
1. [シナリオに web フックを追加](#add-webhook)
1. [Web フックに接続を追加](#add-connection)

#### シナリオを作成 {#create-scenario}

シナリオを作成するには：

1. [Workfront Fusion アカウント](https://app-qa.workfrontfusion.com/)にログインします。
1. 左側のパネルの「**[!UICONTROL シナリオ]**」![共有アイコン](/help/forms/assets/Smock_ShareAndroid_18_N.svg)をクリックします。
1. ページの右上隅にある「**[!UICONTROL 新規シナリオを作成]**」をクリックします。新しいシナリオを作成するページが画面に表示されます。
1. ページの左上隅にある「**[!UICONTROL 新規シナリオ]**」を選択し、シナリオの適切な名前を入力します。
1. 疑問符をクリックし、**[!UICONTROL AEM Forms]** として最初のモジュールを追加することを確認します。

   ![AEM Forms モジュールの追加](/help/forms/assets/workfront-aemforms.png)

   **[!UICONTROL フォームイベントの監視]**&#x200B;ダイアログボックスが表示されます。

   >[!NOTE]
   >
   > 最初のモジュールを **[!UICONTROL AEM Forms]** として追加することは必須です。

1. **[!UICONTROL フォームイベントの監視]**&#x200B;ダイアログボックスを選択します。Web フックを追加するウィンドウが表示されます。

#### Web フックを追加 {#add-webhook}

![Web フックの追加](/help/forms/assets/workfront-add-webhook.png)

Web フックを追加するには、次の手順に従います。

1. 「**[!UICONTROL 追加]**」をクリックします。**[!UICONTROL Web フックを追加]**&#x200B;ダイアログボックスが表示されます。
1. Web フック名を指定します。

   >[!NOTE]
   >
   > 指定した Web フック名が AEM インスタンスに表示されるので、Web フック名は慎重に選択することをお勧めします。

1. 「**[!UICONTROL 追加]**」をクリックして、新しい接続を追加します。**[!UICONTROL 接続を作成]**&#x200B;ダイアログボックスが表示されます。

>[!NOTE]
>
> テクニカルアカウントが **forms-users** グループのメンバーであることを確認します。それ以外の場合、web フックの追加は失敗します。

#### Web フックに接続を追加 {#add-connection}

![接続の追加](/help/forms/assets/workfront-add-connection.png)

接続を追加するには、次の手順に従います。

1. **[!UICONTROL 接続を作成]**&#x200B;ダイアログボックスで&#x200B;**[!UICONTROL 接続名]**&#x200B;を指定します。

1. ドロップダウンリストから「**環境**」と「**タイプ**」を選択します。

1. **インスタンス URL** を入力します。

   >[!NOTE]
   >
   > インスタンス URL は、特定の AEM Forms インスタンスを指す一意の web アドレスです。

   接続の作成に必要な[サービス資格情報は Developer Console から](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja)取得できます。

1. **IMS エンドポイント**&#x200B;の `ims-na1.adobelogin.com` を、Developer Console のサービス資格情報の **imsEndpoint** の値に置き換えます。

   >[!NOTE]
   >
   > `imsEndpoint` URL の追加中、**IMS エンドポイント**&#x200B;テキストボックスの `https://` を保持します。

1. **[!UICONTROL 接続を作成]**&#x200B;ダイアログボックスで、次の値を指定します。
   * Developer Console のサービス資格情報から **clientId** の値を使用して&#x200B;**クライアント ID** を指定します。
   * Developer Console のサービス資格情報から **clientSecret** の値を使用して&#x200B;**クライアント秘密鍵**&#x200B;を指定します。
   * Developer Console のサービス資格情報から **id** の値を使用して&#x200B;**テクニカルアカウント ID** を指定します。
   * Developer Console のサービス資格情報から **org** の値を使用して&#x200B;**組織 ID** を指定します。
   * Developer Console のサービス資格情報から **metascopes** の値を使用して&#x200B;**メタスコープ**&#x200B;を指定します。
   * Developer Console のサービス資格情報から **privateKey** の値を使用して&#x200B;**秘密鍵**&#x200B;を指定します。

   >[!NOTE]
   >
   >* **秘密鍵**&#x200B;の場合は、値から `\r\n` を削除します。
   >  例えば、秘密鍵が次のような場合があります。
   >`\r\nIJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL\r\nMy1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw` の場合、秘密鍵から `\r\n` を削除すると、鍵は次のようになり、両方の値が別の行に表示されます。
   >
   >   `IJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL`
   >
   >   `My1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`
   > 
   >* また、「**抽出**」ボタンを選択して、ファイルから秘密鍵または証明書を取得するオプションもあります。

1. 「**続行**」をクリックします。

   作成した接続は、**[!UICONTROL Web フックを追加]**&#x200B;ダイアログボックスの&#x200B;**[!UICONTROL 接続]**&#x200B;のドロップダウンリストに表示され始めます。

1. 作成した接続の&#x200B;**[!UICONTROL 接続]**&#x200B;をドロップダウンリストから選択します。
1. 「**[!UICONTROL 保存]**」をクリックします。
1. 「**[!UICONTROL OK]**」をクリックして、シナリオの変更を保存します。
1. シナリオをアクティブ化するには、シナリオエディターのオン／オフ切替スイッチボタンをクリックします。

>[!NOTE]
>
> Workfront シナリオをアクティブ化しない場合、フォームの送信は検出されず、送信アクションを Workfront に設定すると送信が失敗します。

### &#x200B;2. Workfront Fusion 用のアダプティブフォームの送信アクションの設定

>[!BEGINTABS]

>[!TAB 基盤コンポーネント]

Workfront Fusion の基盤コンポーネントに基づいてアダプティブフォームの送信アクションを設定するには：

1. 編集用にアダプティブフォームを開き、アダプティブフォームのコンテナプロパティの「**[!UICONTROL 送信]**」セクションに移動します。
1. **[!UICONTROL 送信アクション]** ドロップダウンリストから、「**[!UICONTROL Workfront Fusion シナリオを呼び出し]**」を選択します。
   ![Workfront Fusion 用の送信アクション](/help/forms/assets/workfront-fusion-fc.png)

1. ドロップダウンリストから「**[!UICONTROL Workfront Fusion のシナリオ]**」を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。


>[!TAB コアコンポーネント]

Workfront Fusion でコアコンポーネントに基づくアダプティブフォームの送信アクションを設定するには：

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブをクリックします。
1. **[!UICONTROL 送信アクション]** ドロップダウンリストから、「**[!UICONTROL Workfront Fusion シナリオを呼び出し]**」を選択します。

   ![Workfront Fusion 用の送信アクション](/help/forms/assets/workfront-scenario-existing-af.png)
1. ドロップダウンリストから「**[!UICONTROL Workfront Fusion のシナリオ]**」を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

>[!TAB ユニバーサルエディター]

ユニバーサルエディターを使用して作成されたアダプティブフォームの送信アクションを設定するには：

1. アダプティブフォームを編集用に開きます。
1. エディターで **フォームプロパティを編集** 拡張機能をクリックします。
**フォームのプロパティ** ダイアログが表示されます。

   >[!NOTE]
   >
   > * ユニバーサルエディターインターフェイスに **フォームプロパティを編集** アイコンが表示されない場合は、Extension Managerで **フォームプロパティを編集** 拡張機能を有効にします。
   > * ユニバーサルエディターで拡張機能を有効または無効にする方法については [&#128279;](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)Extension Manager機能のハイライト &rbrace; の記事を参照してください。

1. 「**送信**」タブをクリックし、「**[!UICONTROL Workfront Fusion シナリオを起動]**」送信アクションを選択します。

   ![Workfront Fusion 用の送信アクション](/help/forms/assets/workfront-fusion-ue.png)

1. ドロップダウンリストから「**[!UICONTROL Workfront Fusion のシナリオ]**」を選択します。
1. **[!UICONTROL 保存して閉じる]** をクリックします。

>[!ENDTABS]

## ベストプラクティス {#best-practices}

* AEM インスタンスでシナリオ名を取得する方法がないので、Web フック名は慎重に選択することをお勧めします。後で Web フック名を変更しても、AEM Forms の送信アクションドロップダウンリストには反映されません。
* 1 つのシナリオに複数の Web フックリンクを含めることができますが、一度にアクティブになる Web フックリンクは 1 つだけです。リンクされていない Web フックは、AEM Forms の送信アクションドロップダウンリストに表示されないように削除することをお勧めします。

<!-- During testing or development of Workfront, add the Author URL to the instance URL. However, when deploying Workfront Fusion in a production environment, it is recommended to replicate the scenario URLs for the Publish instance. -->

## 関連記事

{{af-submit-action}}