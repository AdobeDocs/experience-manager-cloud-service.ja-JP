---
title: フォームウィザードを使用してMarketo EngageとAEM Formsを統合する方法
description: フォームウィザードを使用してMarketo Engage インスタンスをAEM Formsと統合する方法について説明します。
keywords: Marketo インスタンスをフォームに接続する方法 、Marketoへのフォームの接続、Marketo Engageとのフォームの統合、Marketo インスタンスとのアダプティブフォームの統合。
feature: Adaptive Forms, Form Data Model
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 1fcba628-ffd8-416a-a8b5-76b35d4aabd4
source-git-commit: 60fa6bd9f29e670acb2acf52a40266e699bb99d3
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 7%

---

# アダプティブフォームとMarketo Engageの統合

![ワークフロー](/help/forms/assets/workflow-marketo-4.png)

Marketo EngageとAEM Formsを統合するためのクラウドサービス設定を作成した後、[Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home)と統合するためのアダプティブフォームを設定できます。

フォームウィザードを使用してMarketo Engageをアダプティブフォームに接続できます。これにより、各ステップをガイドして設定プロセスが簡素化されます。 テンプレート、スタイル、データフィールドを選択するだけでなく、データマッピングを設定して、一度作成されたフォームがMarketo Engageと通信できるようにする必要もあります。 フォームウィザードを使用して、送信時にデータをAdobe Marketo Engageに直接送信するようにアダプティブフォームを設定することもできます。

## Marketo Engageとフォームを接続するための前提条件

Marketo Engageをフォームに接続するための前提条件：

* [ クラウドサービス設定を作成して、Marketo Engageとforms](/help/forms/integrate-form-to-marketo-engage.md)を統合します。

## Marketo Engageと統合するように新しいアダプティブフォームを設定する方法

>[!VIDEO](https://video.tv.adobe.com/v/3442867/marketo-aem-marketo-engage-engage-aem-forms)

<span>このビデオは、コアコンポーネントのみに適用されます。 UE／基盤コンポーネントについて詳しくは、記事を参照してください。</span>

>[!BEGINTABS]

>[!TAB 基盤コンポーネント]

基盤コンポーネントに基づいて新しいアダプティブフォームを設定し、Marketo Engageと統合するには、次の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

   ![Formsとドキュメントを選択](/help/forms/assets/select-forms.png)

1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。 フォーム作成ウィザードが開きます。

   ![AFを選択](/help/forms/assets/select-create-forms.png)

1. **[!UICONTROL Source]** タブで、テンプレートを選択します

   ![ テンプレートの選択](/help/forms/assets/select-template-af1.png)

1. **[!UICONTROL スタイル]**&#x200B;から、テーマを選択します。

   ![テーマを選択](/help/forms/assets/select-form-theme-af1.png)
1. 「**[!UICONTROL データ]**」タブで、データモデルを&#x200B;**Marketo Engage**&#x200B;として選択します。
1. 画面の右側のペインに表示されるドロップダウンリストから「**[!UICONTROL クラウド設定]**」を選択します。
デフォルトでは、関連する設定のすべてのフィールドが表示されます。 このウィザードでは、チェックボックスを使用して、アダプティブフォームに含めるフィールドを選択できる利便性があります。

   ![ データモデルの選択](/help/forms/assets/select-marketo-data-af1.png)

1. 「**[!UICONTROL 送信]**」タブで、「**[!UICONTROL Marketoに送信」アクションを選択します。]**

   データモデルを&#x200B;**Marketo Engage**&#x200B;として選択すると、**Marketoに送信**&#x200B;という送信アクションが自動選択されます。 **[!UICONTROL 送信]** タブから別の送信アクションを選択できます。 「**[!UICONTROL 送信]**」タブには、使用可能なすべての送信アクションが表示されます。

   ![Marketo engageに送信](/help/forms/assets/select-marketo-engage.png)

1. 「**[!UICONTROL 作成]**」を選択します。 アダプティブフォームを保存するタイトル、名前、場所を指定します。

   ![ フォームを作成](/help/forms/assets/create-marketo-form.png)

1. 「**[!UICONTROL 作成]**」を選択します。

アダプティブフォームは、Marketo Engage インスタンスに接続するように設定されました。 または、アダプティブフォームのプロパティを編集して、関連する設定を変更することもできます

>[!TAB コアコンポーネント]

コアコンポーネントに基づいて新しいアダプティブフォームを設定し、Marketo Engageと統合するには、次の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

   ![Formsとドキュメントを選択](/help/forms/assets/select-forms.png)

1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。 フォーム作成ウィザードが開きます。

   ![AFを選択](/help/forms/assets/select-create-forms.png)

1. **[!UICONTROL Source]** タブで、テンプレートを選択します

   ![ テンプレートの選択](/help/forms/assets/select-template.png)

1. **[!UICONTROL スタイル]**&#x200B;から、テーマを選択します。

   ![テーマを選択](/help/forms/assets/select-form-theme.png)


1. 「**[!UICONTROL データ]**」タブで、データモデルを&#x200B;**Marketo Engage**&#x200B;として選択します。

1. 画面の右側のペインに表示されるドロップダウンリストから「**[!UICONTROL クラウド設定]**」を選択します。
デフォルトでは、関連する設定のすべてのフィールドが表示されます。 このウィザードでは、チェックボックスを使用して、アダプティブフォームに含めるフィールドを選択できる利便性があります。

   ![ データモデルの選択](/help/forms/assets/select-marketo-data.png)

1. 「**[!UICONTROL 送信]**」タブで、「**[!UICONTROL Marketoに送信」アクションを選択します。]**

   データモデルを&#x200B;**Marketo Engage**&#x200B;として選択すると、**Marketoに送信**&#x200B;という送信アクションが自動選択されます。 **[!UICONTROL 送信]** タブから別の送信アクションを選択できます。 「**[!UICONTROL 送信]**」タブには、使用可能なすべての送信アクションが表示されます。

   ![Marketo engageに送信](/help/forms/assets/select-marketo-engage.png)

1. 「**[!UICONTROL 作成]**」を選択します。 アダプティブフォームを保存するタイトル、名前、場所を指定します。

   ![ フォームを作成](/help/forms/assets/create-marketo-form.png)

1. 「**[!UICONTROL 作成]**」を選択します。

アダプティブフォームは、Marketo Engage インスタンスに接続するように設定されました。 または、アダプティブフォームのプロパティを編集して、関連する設定を変更することもできます。

>[!TAB ユニバーサルエディター]

ユニバーサルエディターで作成された新しいアダプティブフォームをMarketo Engageと統合するように設定するには、次の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

   ![Formsとドキュメントを選択](/help/forms/assets/select-forms.png)

1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。 フォーム作成ウィザードが開きます。

   ![AFを選択](/help/forms/assets/select-create-forms.png)

1. **[!UICONTROL Source]** タブで、テンプレートを選択します

   ![ テンプレートの選択](/help/forms/assets/select-template-ue.png)

1. 「**[!UICONTROL データ]**」タブで、データモデルを&#x200B;**Marketo Engage**&#x200B;として選択します。

1. 画面の右側のペインに表示されるドロップダウンリストから「**[!UICONTROL クラウド設定]**」を選択します。
デフォルトでは、関連する設定のすべてのフィールドが表示されます。 このウィザードでは、チェックボックスを使用して、アダプティブフォームに含めるフィールドを選択できる利便性があります。

   ![ データモデルの選択](/help/forms/assets/select-marketo-data-ue.png)

1. 「**[!UICONTROL 送信]**」タブで、「**[!UICONTROL Marketoに送信」アクションを選択します。]**

   データモデルを&#x200B;**Marketo Engage**&#x200B;として選択すると、**Marketoに送信**&#x200B;という送信アクションが自動選択されます。 **[!UICONTROL 送信]** タブから別の送信アクションを選択できます。 「**[!UICONTROL 送信]**」タブには、使用可能なすべての送信アクションが表示されます。

   ![Marketo engageに送信](/help/forms/assets/select-marketo-engage-ue.png)

1. 「**[!UICONTROL 作成]**」を選択します。 アダプティブフォームを保存するタイトル、名前、場所を指定します。

   ![ フォームを作成](/help/forms/assets/create-marketo-form.png)

1. 「**[!UICONTROL 作成]**」を選択します。

アダプティブフォームは、Marketo Engage インスタンスに接続するように設定されました。 または、アダプティブフォームのプロパティを編集して、関連する設定を変更することもできます。

>[!ENDTABS]

## よくある質問（FAQ）

**Q: Marketo Engage スキーマに接続するように設定されたフォームの送信アクションを変更できますか？**
**A:** デフォルトでは、フォームがMarketo Engage スキーマに接続するように設定されている場合、**Marketoに送信** アクションが選択されます。 ただし、必要に応じて、フォームの送信アクションを変更できます。


**Q: フォームのコネクタを変更するとどうなりますか？**\
**A:** フォームのコネクタを変更すると、既存のバインディングが無効になります。

**Q: Marketo Engageと統合されたフォームのルールエディターの呼び出しサービスで利用できる3つの操作は何ですか？**\
**A:** Marketo Engageと統合されたフォームの&#x200B;**呼び出しサービス**&#x200B;で使用できる3つの標準操作は次のとおりです。

* リードを同期
* リードをIDで取得
* フィルタータイプでリードを取得

## 次の手順

アダプティブフォームを[Munchkin ライブラリ ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/setup/munchkin)と接続して、訪問回数、クリック数、フォーム送信数を追跡することもできます。

## 関連記事

{{af-submit-action}}

## 関連トピック

{{marketo-engage-see-also}}
