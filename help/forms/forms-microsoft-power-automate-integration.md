---
title: アダプティブフォームとMicrosoft® Power Automate の統合
description: アダプティブフォームをMicrosoft® Power Automate と統合します。
hide: true
hidefromtoc: true
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
source-git-commit: ccc4d487cb180273284276cf9cdf18680a3efcb8
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 10%

---

# アダプティブフォームとMicrosoft® Power Automate の接続 {#connect-adaptive-form-with-power-automate}

送信時にMicrosoft® Power Automate Cloud Flow を実行するようにアダプティブフォームを設定できます。 設定済みのアダプティブフォームは、キャプチャされたデータ、添付ファイルおよびレコードのドキュメントを Power Automate Cloud Flow に送信して処理します。 Microsoft® Power Automate の機能を活用しながら、カスタムのデータキャプチャエクスペリエンスを構築し、取り込んだデータに関するビジネスロジックを構築し、顧客ワークフローを自動化できます。 アダプティブフォームをMicrosoft® Power Automated と統合した後に実行できる操作の例を以下に示します。

* Power Automate のビジネスプロセスでのアダプティブFormsデータの使用
* Power Automate を使用して、500 を超えるデータソースまたは一般公開されている API にキャプチャしたデータを送信する
* 取得したデータに対して複雑な計算を実行する
* 事前に定義されたスケジュールでアダプティブFormsのデータをストレージシステムに保存する

アダプティブFormsエディターでは、 **Microsoft® Power Automate フローを呼び出す** 送信アクションを実行してアダプティブフォームのデータ、添付ファイル、レコードのドキュメントが Power Automate Cloud Flow に送信されます。 送信アクションを使用して、取得したデータをMicrosoft® Power Automate に送信するには、次の手順を実行します。 [Formsas a Cloud ServiceインスタンスをMicrosoft® Power Automate に接続する](forms-microsoft-power-automate-integration.md#connect-forms-server-with-power-automate)

## 前提条件

アダプティブフォームをMicrosoft® Power Automate に接続するには、次の手順を実行する必要があります。

* Microsoft® Power Automate Premium ライセンス。
* Microsoft® [電力自動化フロー](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) と `When an HTTP request is received` アダプティブフォームの送信データを受け入れるトリガー。


* FormsオーサーおよびForms管理者権限を持つExperience Managerユーザー。
* Power Automate への接続に使用するアカウントが、Power Automate フローの所有者であることを確認します。


## Formsas a Cloud ServiceインスタンスをMicrosoft® Power Automate に接続する {#connect-forms-server-with-power-automate}

Formsas a Cloud ServiceのインスタンスをMicrosoft® Power Automate に接続するには、次の操作を実行します。

1. Microsoft® Azure Active Directory アプリケーションの作成
1. Microsoft® Power Automate Dataverse クラウド設定を作成します。
1. Microsoft® Power Automate フローサービスクラウド設定を作成
1. Microsoft® Power Automate Dataverse クラウド設定を公開します。

### Microsoft® Azure Active Directory アプリケーションの作成 {#ms-power-automate-application}

1. にログインします。 [Azure Portal](https://portal.azure.com/).
1. 選択 [!UICONTROL Azure Active Directory] をクリックします。
1. デフォルトのディレクトリページで、 [!UICONTROL アプリの登録] を左側のパネルからクリックします。
1. アプリ登録ページで、「新規登録」をクリックします。
1. ページで、名前、サポートされているアカウントタイプおよびリダイレクト URI を指定します。 「リダイレクト URI 」で、次の情報を指定し、「保存」をクリックします。
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/flowservice/config.html`

   ![Azure Active Directory アプリケーションの登録](assets/power-automate-application.png)

   >[!NOTE]
   >必要に応じて、認証ページから追加のリダイレクト URI を指定することもできます。
   > サポートされるアカウントの種類に応じて、使用事例に応じて、単一テナント、複数テナント、または個人のMicrosoftアカウントを選択します


1. 認証ページで、次のオプションを有効にし、「保存」をクリックします。


   * アクセストークン（暗黙のフローに使用）
   * ID トークン（暗黙的なフローとハイブリッドフローに使用）

1. API 権限ページで、「権限を追加」をクリックします。
1. Microsoft® API で、「フローサービス」を選択し、次の権限を選択します。
   * Flows.Manage.All
   * Flows.Read.All

   「権限を追加」をクリックして、権限を保存します。
1. API 権限ページで、「権限を追加」をクリックします。 組織で使用している API を選択して検索 `DataVerse`.
1. user_impersonation を有効にし、「権限を追加」をクリックします。
1. （オプション）「証明書と秘密鍵」ページで、「新しいクライアント秘密鍵」をクリックします。 クライアントシークレットを追加画面で、シークレットの有効期限が切れる説明と期間を入力し、「追加」をクリックします。 秘密の文字列が生成されます。
1. 組織固有のメモを保存する [Dynamics 環境 URL](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests).

### Microsoft® Power Automate Dataverse クラウド設定を作成 {#microsoft-power-automate-dataverse-cloud-configuration}

1. AEM Forms のオーサーインスタンスで、**[!UICONTROL ツール]** ![ハンマー](assets/hammer.png)／**[!UICONTROL 一般]**／**[!UICONTROL 設定ブラウザー]**&#x200B;に移動します。
1. **[!UICONTROL 設定ブラウザー]**&#x200B;ページで「**[!UICONTROL 作成]**」をタップします。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、「**[!UICONTROL クラウド設定]**」を有効にして「**[!UICONTROL 作成]**」をタップします。これにより、Cloud Services 用の設定コンテナが作成されます。フォルダー名にスペースが含まれていないことを確認します。
1. に移動します。 **[!UICONTROL ツール]** ![ハンマー](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** 前の手順で作成した設定コンテナを開きます。

   >[!NOTE]
   >
   >アダプティブフォームを作成する際に、**[!UICONTROL 設定コンテナ]**&#x200B;フィールドにコンテナ名を指定します。
1. 設定ページで「**[!UICONTROL 作成]**」をタップして、AEM Forms 内に [!DNL Microsoft® Power Automate Flow Service] の設定を作成します。
1. の **[!UICONTROL Microsoft® Power Automate の Dataverse Service の設定]** ページで、 **[!UICONTROL クライアント ID]** （アプリケーション ID とも呼ばれます）。 **[!UICONTROL クライアント秘密鍵]**, **[!UICONTROL OAuth URL]** および **[!UICONTROL 動的環境 URL]**. のクライアント ID、クライアントの秘密鍵、OAuth URL および動的環境 URL を使用します。 [Microsoft® Azure Active Directory アプリケーション](#ms-power-automate-application) 前の節で作成した内容。 Microsoft® Azure Active Directory アプリケーション UI の「エンドポイント」オプションを使用して OAuth URL を検索する

![Microsoft Power Automate アプリケーション UI の「エンドポイント」オプションを使用して OAuth URL を検索する](assets/endpoints.png)
Microsoft® Power Automate アプリケーション UI の「エンドポイント」オプションを使用して OAuth URL を検索する

1. タップ **[!UICONTROL 接続]** . 必要に応じて、Microsoft® Azure アカウントにログインします。 「**[!UICONTROL 保存]**」をタップします。

### Microsoft® Power Automate Flow Service のクラウド設定を作成します。

1. に移動します。 **[!UICONTROL ツール]** ![ハンマー](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Flow Service]** 前の節で作成した設定コンテナを開きます。

   >[!NOTE]
   >
   >アダプティブフォームを作成する際に、**[!UICONTROL 設定コンテナ]**&#x200B;フィールドにコンテナ名を指定します。
1. 設定ページで「**[!UICONTROL 作成]**」をタップして、AEM Forms 内に [!DNL Microsoft® Power Automate Flow Service] の設定を作成します。
1. の **[!UICONTROL Microsoft® Power Automate の Dataverse の設定]** ページで、 **[!UICONTROL クライアント ID]** （アプリケーション ID とも呼ばれます）。 **[!UICONTROL クライアント秘密鍵]**, **[!UICONTROL OAuth URL]** および **[!UICONTROL 動的環境 URL]**. クライアント ID、クライアント秘密鍵、OAuth URL、Dynamics 環境 ID を使用します。 Microsoft® Azure Active Directory アプリケーション UI の「エンドポイント」オプションを使用して、OAuth URL を検索します。 を開きます。 [マイフロー](https://us.flow.microsoft.com) リンクをタップし、「マイフロー」をタップします。URL にリストされている ID を「Dynamics 環境 ID」として使用します。
1. タップ **[!UICONTROL 接続]**. 必要に応じて、Microsoft® Azure アカウントにログインします。 「**[!UICONTROL 保存]**」をタップします。

### Microsoft® Power Automate Dataverse とMicrosoft® Power Automate フローサービスクラウド設定の両方を公開します {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. に移動します。 **[!UICONTROL ツール]** ![ハンマー](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** 前の [Microsoft® Power Automate Dataverse クラウド設定を作成](#microsoft-power-automate-dataverse-cloud-configuration) 」セクションに入力します。
1. を選択します。 `dataverse` 設定およびタップします。 **[!UICONTROL 公開]**.
1. 公開ページで、「 」を選択します。 **[!UICONTROL すべての設定]** とタップします。 **[!UICONTROL 公開]**. Power Automate Dataverse と Power Automate Flow Service のクラウド設定の両方を公開します。

Formsas a Cloud ServiceインスタンスがMicrosoft® Power Automate に接続されました。 アダプティブFormsのデータを Power Automate のフローに送信できるようになりました。

## 「Microsoft® Power Automate Flow を起動」送信アクションを使用して、Power Automate Flow にデータを送信します。 {#use-the-invoke-microsoft-power-automate-flow-submit-action}

後 [Formsas a Cloud ServiceインスタンスをMicrosoft® Power Automate に接続する](#connect-forms-server-with-power-automate)では、次の操作を実行して、フォーム送信時に取り込んだデータをMicrosoft®フローに送信するようアダプティブフォームを設定します。

1. オーサーインスタンスにログインし、アダプティブフォームを選択して、 **[!UICONTROL プロパティ]**.
1. 設定コンテナで、「 」セクションで作成したコンテナを参照して選択します [Microsoft® Power Automate Dataverse クラウド設定を作成](#microsoft-power-automate-dataverse-cloud-configuration)をタップし、 **[!UICONTROL 保存して閉じる]**.
1. 編集用にアダプティブフォームを開き、に移動します。 **[!UICONTROL 送信]** 」セクションに表示されます。
1. プロパティコンテナで、 **[!UICONTROL 送信アクション]** を選択します。 **[!UICONTROL Power Automate フローを起動]** オプション。 使用可能な Power Automate フローのリストが使用可能になります **[!UICONTROL 電力自動化フロー]** オプション。 必要なフローを選択し、送信時にアダプティブFormsデータが送信されます。

![送信アクションの設定](assets/submission.png)

>[!NOTE]
>
> アダプティブフォームを送信する前に、 `When an HTTP Request is received` 以下の JSON スキーマを持つトリガーが Power Automate フローに追加されます。

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

