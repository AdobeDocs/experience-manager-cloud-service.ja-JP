---
Title: How to integrate Marketo Engage with AEM Forms using Form wizard?
Description: Learn how to integrate your Marketo Engage instance with AEM Forms using form wizard.
Keywords: How to connect a Marketo instance with form? , Connect a form to Marketo, Integrate a form with Marketo Engage, Integrate an Adaptive Form with a Marketo instance.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 1fcba628-ffd8-416a-a8b5-76b35d4aabd4
source-git-commit: ce4646d8db1870f8ec85faddeb4e0a6a04f4c46e
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 9%

---

# アダプティブフォームとMarketo Engageの統合

<span class="preview">機能は、早期導入プログラムで利用できます。早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID で aem-forms-ea@adobe.com までメールを送信してください。</span>

![ワークフロー](/help/forms/assets/workflow-marketo-4.png)

Marketo EngageをAEM Formsと統合するためのクラウドサービス設定を作成したら、[Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home) と統合するようにアダプティブフォームを設定できます。

フォームウィザードを使用してMarketo Engageをアダプティブフォームに接続できます。これにより、各手順をガイドして設定プロセスを簡単にできます。 テンプレート、スタイル、データフィールドの選択や、作成したフォームがMarketo Engageと通信できるようにデータマッピングの設定を行います。 フォームウィザードを使用して、送信時にAdobe Marketo Engageに直接データを送信するようにアダプティブフォームを設定することもできます。

## フォーム用のMarketo Engage データソースの設定に関する考慮事項

フォーム用のMarketo Engage データソースを設定する際の考慮事項は次のとおりです。

* Edge Delivery Services FormsをMarketo Engageに接続することはできません。

## Marketo Engageと forms を接続するための前提条件

Marketo Engageを forms に接続するための前提条件：

* Marketo Engageを forms[ と統合するための ](/help/forms/integrate-form-to-marketo-engage.md) クラウドサービス設定を作成します。

## Marketo Engageと統合する新しいアダプティブフォームの設定方法

>[!VIDEO](https://video.tv.adobe.com/v/3442867/marketo-aem-marketo-engage-engage-aem-forms)

>[!BEGINTABS]

>[!TAB 基盤コンポーネント]

基盤コンポーネントに基づく新しいアダプティブフォームをMarketo Engageと統合するように設定するには、次の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

   ![Formsとドキュメントの選択 ](/help/forms/assets/select-forms.png)

1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。 フォーム作成ウィザードが開きます。

   ![AF を選択 ](/help/forms/assets/select-create-forms.png)

1. 「**[!UICONTROL Source]**」タブで、テンプレートを選択します

   ![ テンプレートの選択 ](/help/forms/assets/select-template-af1.png)

1. **[!UICONTROL スタイル]** からテーマを選択します。

   ![テーマを選択](/help/forms/assets/select-form-theme-af1.png)
1. 「**[!UICONTROL Data]**」タブで、データモデルを **Marketo Engage** として選択します。
1. 画面の右側のパネルに表示されるドロップダウンリストから **[!UICONTROL クラウド設定]** を選択します。
デフォルトでは、関連付けられた設定のすべてのフィールドが表示されます。 ウィザードでは、チェックボックスを使用してアダプティブフォームに含めるフィールドを選択できる便利な機能が用意されています。

   ![ データモデルを選択 ](/help/forms/assets/select-marketo-data-af1.png)

1. 「**[!UICONTROL 送信]**」タブで、送信アクションを「**[!UICONTROL Marketoに送信]**」として選択します。

   データモデルを **Marketo Engage** として選択すると、送信アクションが **Marketoに送信** として自動選択されます。 「**[!UICONTROL 送信]**」タブから、別の送信アクションを選択できます。 「**[!UICONTROL 送信]**」タブには、使用可能なすべての送信アクションが表示されます。

   ![Marketo engage への送信 ](/help/forms/assets/select-marketo-engage.png)

1. 「**[!UICONTROL 作成]**」を選択します。アダプティブフォームを保存するタイトル、名前、場所を指定します。

   ![ フォームを作成 ](/help/forms/assets/create-marketo-form.png)

1. 「**[!UICONTROL 作成]**」を選択します。

これで、Marketo Engage インスタンスに接続するようにアダプティブフォームが設定されました。 または、アダプティブフォームのプロパティを編集して、関連する設定を変更することもできます

>[!TAB コアコンポーネント]

コアコンポーネントに基づく新しいアダプティブフォームをMarketo Engageと統合するように設定するには、次の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

   ![Formsとドキュメントの選択 ](/help/forms/assets/select-forms.png)

1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。 フォーム作成ウィザードが開きます。

   ![AF を選択 ](/help/forms/assets/select-create-forms.png)

1. 「**[!UICONTROL Source]**」タブで、テンプレートを選択します

   ![ テンプレートの選択 ](/help/forms/assets/select-template.png)

1. **[!UICONTROL スタイル]** からテーマを選択します。

   ![テーマを選択](/help/forms/assets/select-form-theme.png)


1. 「**[!UICONTROL Data]**」タブで、データモデルを **Marketo Engage** として選択します。

1. 画面の右側のパネルに表示されるドロップダウンリストから **[!UICONTROL クラウド設定]** を選択します。
デフォルトでは、関連付けられた設定のすべてのフィールドが表示されます。 ウィザードでは、チェックボックスを使用してアダプティブフォームに含めるフィールドを選択できる便利な機能が用意されています。

   ![ データモデルを選択 ](/help/forms/assets/select-marketo-data.png)

1. 「**[!UICONTROL 送信]**」タブで、送信アクションを「**[!UICONTROL Marketoに送信]**」として選択します。

   データモデルを **Marketo Engage** として選択すると、送信アクションが **Marketoに送信** として自動選択されます。 「**[!UICONTROL 送信]**」タブから、別の送信アクションを選択できます。 「**[!UICONTROL 送信]**」タブには、使用可能なすべての送信アクションが表示されます。

   ![Marketo engage への送信 ](/help/forms/assets/select-marketo-engage.png)

1. 「**[!UICONTROL 作成]**」を選択します。アダプティブフォームを保存するタイトル、名前、場所を指定します。

   ![ フォームを作成 ](/help/forms/assets/create-marketo-form.png)

1. 「**[!UICONTROL 作成]**」を選択します。

これで、Marketo Engage インスタンスに接続するようにアダプティブフォームが設定されました。 または、アダプティブフォームのプロパティを編集して、関連する設定を変更することもできます。

>[!TAB ユニバーサルエディター]

ユニバーサルエディターで作成した新しいアダプティブフォームをMarketo Engageと統合するように設定するには、次の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

   ![Formsとドキュメントの選択 ](/help/forms/assets/select-forms.png)

1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。 フォーム作成ウィザードが開きます。

   ![AF を選択 ](/help/forms/assets/select-create-forms.png)

1. 「**[!UICONTROL Source]**」タブで、テンプレートを選択します

   ![ テンプレートの選択 ](/help/forms/assets/select-template-ue.png)

1. 「**[!UICONTROL Data]**」タブで、データモデルを **Marketo Engage** として選択します。

1. 画面の右側のパネルに表示されるドロップダウンリストから **[!UICONTROL クラウド設定]** を選択します。
デフォルトでは、関連付けられた設定のすべてのフィールドが表示されます。 ウィザードでは、チェックボックスを使用してアダプティブフォームに含めるフィールドを選択できる便利な機能が用意されています。

   ![ データモデルを選択 ](/help/forms/assets/select-marketo-data-ue.png)

1. 「**[!UICONTROL 送信]**」タブで、送信アクションを「**[!UICONTROL Marketoに送信]**」として選択します。

   データモデルを **Marketo Engage** として選択すると、送信アクションが **Marketoに送信** として自動選択されます。 「**[!UICONTROL 送信]**」タブから、別の送信アクションを選択できます。 「**[!UICONTROL 送信]**」タブには、使用可能なすべての送信アクションが表示されます。

   ![Marketo engage への送信 ](/help/forms/assets/select-marketo-engage-ue.png)

1. 「**[!UICONTROL 作成]**」を選択します。アダプティブフォームを保存するタイトル、名前、場所を指定します。

   ![ フォームを作成 ](/help/forms/assets/create-marketo-form.png)

1. 「**[!UICONTROL 作成]**」を選択します。

これで、Marketo Engage インスタンスに接続するようにアダプティブフォームが設定されました。 または、アダプティブフォームのプロパティを編集して、関連する設定を変更することもできます。

>[!ENDTABS]

## よくある質問（FAQ）

**Q:Marketo Engage スキーマに接続するように設定されたフォームの送信アクションを変更できますか？**
**A:** デフォルトでは、Marketo Engage スキーマと接続するようにフォームが設定されている場合、**Marketoに送信** アクションが選択されています。 ただし、必要に応じて、フォームの送信アクションを変更できます。


**Q：フォームのコネクタを変更するとどうなりますか？**\
**A:** フォームのコネクタを変更すると、既存の連結が無効になります。

**Q:Marketo Engageと統合されたフォームのルールエディターの呼び出しサービスで使用できる 3 つの操作を教えてください。**\
**A:** Marketo Engageと統合されたフォームの場合、**サービスの呼び出し** で使用できる 3 つの標準の操作は次のとおりです。

* リードを同期
* リードを ID で取得
* フィルタータイプでリードを取得

## 次の手順

また、アダプティブフォームを [Munchkin ライブラリ ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/setup/munchkin) に接続して、訪問数、クリック数、フォーム送信数をトラッキングすることもできます。

## 関連記事

{{af-submit-action}}

## 関連トピック

{{marketo-engage-see-also}}
