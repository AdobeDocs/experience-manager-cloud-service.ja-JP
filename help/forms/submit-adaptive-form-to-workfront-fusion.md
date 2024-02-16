---
title: Adobe Workfront Fusion とAEM Forms Submission の統合
description: Adobe Workfront Fusion を使用すると、繰り返しのタスクに重点を置くのではなく、新しいタスクに重点を置くことができます。 フォーム送信を使用して、Adobe Workfront Fusion をアダプティブフォームに接続することができます。
keywords: Adobe Workfront Fusion、Adobe Workfront Fusion とAEM Forms Submission の統合、Adobe Workfront Fusion とAEM Forms、Workfront Fusion とAEM Forms、Workfront Fusion とAEM Forms、AEM FormsとWorkfront Fusion の接続、WorkfrontとAEM Forms Fusion とWorkfrontの接続方法、 Fusion と Fusion をフォームに接続する
topic-tags: author, developer
feature: Adaptive Forms
role: Admin, User
exl-id: d3efb450-a879-40ae-8958-0040f99bdafc
source-git-commit: 8546e6286bea5f603b1e011a76c206b178337ab7
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 6%

---

# Adobe Workfront Fusion へのアダプティブフォームの送信

<span class="preview"> この機能は、アーリーアダプタープログラムで利用できます。 早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID から aem-forms-early-adopter-program@adobe.com までメールをお送りください。</span>

[Adobe Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) ドキュメント承認ワークフロー、E メールのフィルタリングや並べ替えなど、同じタスクを繰り返すプロセスを自動化し、繰り返しタスクではなく新しいタスクに焦点を当てることができます。 Adobe Workfront Fusion には、複数のシナリオが含まれています。 シナリオは、アプリケーションと Web サービス間のデータ転送を実行する一連のモジュールで構成されます。 シナリオでは、様々な手順（モジュール）を追加してタスクを自動化します。

例えば、Workfront Fusion を使用すると、アダプティブフォームでデータを収集し、データを処理し、データをアーカイブ用にデータストアに送信するシナリオを作成できます。 シナリオを設定すると、ユーザーがフォームに入力するたびに、Workfront Fusion は自動的にタスクを実行し、データストアをシームレスに更新します。

AEM as a Cloud Serviceには、フォーム送信を処理するための標準の様々な送信アクションが用意されています。 これらのオプションについて詳しくは、 [アダプティブフォーム送信アクション](/help/forms/configure-submit-actions-core-components.md)  記事。


## Adobe Workfront Fusion を使用する利点{#advatages-of-workfront-fusion}

Adobe Workfront Fusion をAEM Formsと組み合わせて使用する利点の一部を次に示します。

* アダプティブFormsで取得したデータをWorkfront Fusion シナリオに送信する
* エラーが発生しにくいタスクを自動化します。
* Workfrontに直接含まれない組織に固有の要件のカスタマイズ。
* 単純なロジックや簡単な決定（例えば、if/then 文）の処理。

## AEM FormsとAdobe Workfront Fusion を統合するための前提条件 {#prerequisites}

Workfront Fusion をAEM Formsに接続するために必要な前提条件は次のとおりです。

* 有効な [Workfront Fusion ライセンス](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/license-automation-vs-integration.html).
* アクセス権を持つAEMユーザー [開発者コンソール](https://my.cloudmanager.adobe.com/) から [サービス資格情報の取得](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja).

## AEM FormsとAdobe Workfront Fusion の統合

>[!VIDEO](https://video.tv.adobe.com/v/3427145/adaptive-forms-adobe-workfront-af-workfront-workfront-aem-forms/?quality=12&learn=on)

接続するには [Workfront fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) フォームに対して、次の手順を実行します。

### 1. Workfrontシナリオの作成 {#workflow-scenario}

Workfrontシナリオを作成するには：
1. ログイン [Workfront Fusion アカウント](https://app-qa.workfrontfusion.com/).
1. クリック **[!UICONTROL シナリオ]** ![共有アイコン](/help/forms/assets/Smock_ShareAndroid_18_N.svg) をクリックします。
1. クリック **[!UICONTROL 新しいシナリオの作成]** をクリックします。 新しいシナリオを作成するページが画面に表示されます。
1. 選択 **[!UICONTROL 新しいシナリオ]** ページの左上隅に、シナリオの適切な名前を入力します。
1. 疑問符をクリックし、最初のモジュールを **[!UICONTROL AEM Forms]**.

   ![AEM Formsモジュールの追加](/help/forms/assets/workfront-aemforms.png)

   The **[!UICONTROL フォームイベントの監視]** ダイアログボックスが表示されます。

   >[!NOTE]
   >
   > 最初のモジュールを **[!UICONTROL AEM Forms]**.

1. を選択します。 **[!UICONTROL フォームイベントの監視]** ダイアログボックスと、ウェブフックを追加するウィンドウが表示されます。

#### 1.1 ウェブフックの追加 {#add-webhook}

![ウェブフックの追加](/help/forms/assets/workfront-add-webhook.png)

Webhook を追加するには：

1. クリック **[!UICONTROL 追加]** および **[!UICONTROL ウェブフックの追加]** ダイアログボックスが表示されます。
1. ウェブフック名を指定します。

   >[!NOTE]
   >
   > 指定した Webhook 名がAEMインスタンスに表示されるので、Webhook 名は慎重に選択することをお勧めします。

1. クリック **[!UICONTROL 追加]** 新しい接続を追加するには、をクリックします。 The **[!UICONTROL 接続の作成]** ダイアログボックスが表示されます。

#### 1.2 ウェブフックへの接続の追加 {#add-connection}

![接続を追加](/help/forms/assets/workfront-add-connection.png)

接続を追加するには：

1. を指定します。 **[!UICONTROL 接続名]** （内） **[!UICONTROL 接続の作成]** ダイアログボックス。

1. 選択 **環境** および **タイプ** 」をドロップダウンリストから選択します。

1. 次を入力します。 **インスタンス URL**.

   >[!NOTE]
   >
   > インスタンス URL は、特定のAEM Formsインスタンスを指す一意の Web アドレスです。

   次を取得： [開発者コンソールからのサービス資格情報](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja) 接続を作成するために必要です。

1. 置換 `ims-na1.adobelogin.com` （内） **IMS エンドポイント** ～の価値を持つ **imsEndpoint** を開発者コンソールのサービス資格情報から削除します。

   >[!NOTE]
   >
   > 保持する `https://` （内） **IMS エンドポイント** 追加中のテキストボックス `imsEndpoint` URL。

1. 次の値を **[!UICONTROL 接続の作成]** ダイアログボックス：
   * 指定 **クライアント ID** 価値を持って **clientId** を開発者コンソールのサービス資格情報から削除します。
   * 指定 **クライアントの秘密鍵** 価値を持って **clientSecret** を開発者コンソールのサービス資格情報から削除します。
   * 指定 **テクニカルアカウント ID**  価値を持って **id** を開発者コンソールのサービス資格情報から削除します。
   * 指定 **組織 ID**  価値を持って **org** を開発者コンソールのサービス資格情報から削除します。
   * **メタスコープ**  価値を持って **メタスコープ** を開発者コンソールのサービス資格情報から削除します。
   * **秘密鍵**  価値を持って **privateKey** を開発者コンソールのサービス資格情報から削除します。

   >[!NOTE]
   >
   >* の場合 **秘密鍵**，削除 `\r\n` 値から。
   >  例えば、秘密鍵の値が次のような場合、
   >`\r\nIJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL\r\nMy1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`を削除してから、 `\r\n` 秘密鍵から、鍵は次のようになります。両方の値が別の行に表示されます。
   >
   >   `IJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL`
   >
   >   `My1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`
   > 
   >* また、ファイルから秘密鍵または証明書を取得するオプションもあります ( **抽出** 」ボタンをクリックします。

1. 「**続行**」をクリックします。

   作成した接続が **[!UICONTROL 接続]** （内） **[!UICONTROL ウェブフックの追加]** ダイアログボックス。

1. 作成した接続を選択 **[!UICONTROL 接続]** 」をドロップダウンリストから選択します。
1. 「**[!UICONTROL 保存]**」をクリックします。
1. クリック **[!UICONTROL OK]** をクリックし、シナリオの変更を保存します。
1. シナリオを有効にするには、シナリオエディターでオン/オフ切り替えボタンをクリックします。

>[!NOTE]
>
> Workfrontシナリオを有効にしない場合、フォームの送信は検出されず、Workfrontに送信アクションを設定すると、送信が失敗します。

### 2. Workfront Fusion 用のアダプティブフォームの送信アクションを設定する

Workfont Fusion の送信アクションは、次の場合に設定できます。
* [新しいアダプティブForms](#new-af-submit-action)
* [既存のアダプティブフォーム](#existing-af-submit-action)

#### Workfront Fusion 用の新しいアダプティブフォームの送信アクションを設定する {#new-af-submit-action}

新しいアダプティブフォームの送信アクションをWorkfront Fusion 用に設定するには：

1. AEMインスタンスにログインします。
1. に移動します。 **[!UICONTROL Forms]** > **[!UICONTROL Formsとドキュメント]** > **[!UICONTROL 作成]** > **[!UICONTROL アダプティブフォーム]**. The **[!UICONTROL フォームを作成]** ウィザードが表示されます。
1. アダプティブフォームテンプレートを **[!UICONTROL ソース]** タブをクリックします。
1. 次からテーマを選択： **[!UICONTROL スタイル]** タブをクリックします。

   ![Workfront Fusion の送信アクション](/help/forms/assets/workfront-scenario-new-af.png)

1. を選択します。 **[!UICONTROL Workfront Fusion シナリオを呼び出す]** から **[!UICONTROL 送信]** タブをクリックします。
1. 作成した Webhook を **[!UICONTROL オプション]** 」タブをクリックします。 **[!UICONTROL プロパティ]** ウィンドウ

   >[!NOTE]
   >
   > Workfrontシナリオの Webhook 名は、 **オプション** 」ドロップダウンリストから選択できます。

1. 「**[!UICONTROL 作成]**」をクリックします。
1. 新しいアダプティブフォームの名前を指定し、 **[!UICONTROL 作成]**.

#### 既存のアダプティブフォームの送信アクションをWorkfront Fusion 用に設定する {#existing-af-submit-action}

既存のアダプティブフォームの送信アクションをWorkfront Fusion 用に設定するには：

1. AEMインスタンスにログインします。
1. **[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択し、編集モードでフォームを開きます。
1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。アダプティブフォームコンテナダイアログボックスが開きます。

   ![Workfront Fusion の送信アクション](/help/forms/assets/workfront-scenario-existing-af.png)

1. 「**[!UICONTROL 送信]**」タブを開きます。
1. を選択します。 **[!UICONTROL 送信アクション]** as **[!UICONTROL Workfront Fusion シナリオを呼び出す]**
1. 選択 **[!UICONTROL Workfront Fusion のシナリオ]** 」をドロップダウンリストから選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

## ベストプラクティス {#best-practices}

* AEMインスタンスでシナリオ名を取得する方法がないので、Webhook 名は慎重に選択することをお勧めします。 後で Webhook 名を変更しても、AEM Formsの送信アクションドロップダウンリストには反映されません。
* 1 つのシナリオに複数の Webhook リンクを含めることができますが、一度にアクティブになる Webhook リンクは 1 つだけです。 リンクされていない Webhook は、AEM Formsの送信アクションドロップダウンリストに表示されないように、削除することをお勧めします。

<!-- During testing or development of Workfront, add the Author URL to the instance URL. However, when deploying Workfront Fusion in a production environment, it is recommended to replicate the scenario URLs for the Publish instance. -->

## 関連記事

{{af-submit-action}}