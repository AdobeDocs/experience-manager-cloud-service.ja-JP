---
Title: How to send an email on submission of an Adaptive Form?
Description: Explore the process to set up email notifications when submitting an Adaptive Form.
keywords: アダプティブフォーム用の電子メールの送信方法、電子メール送信アクション、アダプティブフォーム電子メール、フォーム送信電子メール、電子メールの送信ガイド
feature: Adaptive Forms, Core Components
source-git-commit: f1db04e6cd1f78c1530aefd29f5f036ca5e70873
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 24%

---


# アダプティブフォームの電子メール送信アクションの設定

The **[!UICONTROL メールの送信]** 送信アクションを使用すると、フォームの送信が成功したときに 1 人または複数の受信者に電子メールを送信できます。 この送信アクションを使用すると、事前に定義された形式のフォームデータを含める電子メールを作成できます。 例えば、次のテンプレートで、送信されたフォームデータから顧客名、配送先住所、都道府県名、郵便番号が取得されるとします。


    ```
    こんにちは ${customer_Name} さん、
    
    以下がデフォルトの配送先住所として設定されています。
    ${customer_Name}、
    ${customer_Shipping_Address}、
    ${customer_State}、
    ${customer_ZIPCode}
    
    よろしくお願いいたします。
    WKND
    
    ```


## メリット

「電子メールを送信」送信アクションを使用してアダプティブフォームを設定する利点には、次のようなものがあります。

* フォームデータが指定された電子メール受信者に直接送信されるので、迅速な通信が可能です。
* これにより、フォーム送信を電子メール通知に直接統合することで、ワークフローを合理化できます。
* 組織が E メールコンテンツをカスタマイズし、特定のコミュニケーションニーズに合わせて E メールコンテンツをカスタマイズするのに役立ちます。

## 電子メール送信アクションの設定 {#steps-to-configure-send-email-submit-action}

送信アクションを設定するには：

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブをクリックします。
1. 次から： **[!UICONTROL 送信アクション]** ドロップダウンリストで、「 **[!UICONTROL 電子メールを送信]**.

   ![電子メールを送信のアクション設定](/help/forms/assets/send-email-action-configuration.gif)
1. で送信者の電子メール ID を指定します。 **[!UICONTROL 送信者]** テキストボックス。
1. 受信者の E メール ID を **[!UICONTROL 宛先]** テキストボックス。 複数の受信者を追加するには、 **[!UICONTROL 追加]** 」ボタンをクリックします。
1. [オプション] CC および BCC の受信者を追加するには、 **[!UICONTROL 追加]** 」ボタンをクリックします。
1. 件名行を **[!UICONTROL 件名]** テキストボックス。
1. 電子メール送信アクションを設定する電子メールテンプレートを追加します。
   * AEMアセットに保存されている外部電子メールテンプレートのパスを指定するには、 **[!UICONTROL 外部テンプレートのパス]** オプション。
   * また、 **[!UICONTROL メールテンプレート]** テキストボックス。
1. [オプション] The **[!UICONTROL メールの送信]** 送信アクションには、添付ファイルと [レコードのドキュメント (DoR)](generate-document-of-record-core-components.md) 電子メールに置き換えます。
1. 「**[!UICONTROL 完了]**」をクリックします。

## ベストプラクティス {#best-practices}

* E メールの内容は明確かつ簡潔にすることをお勧めします。 ユーザーは、E メールの目的と、実行する必要があるアクションを理解する必要があります。
* アダプティブフォーム内の別のパネルに配置されている場合でも、すべてのフォームフィールドに一意の要素名を付けることをお勧めします。
* AEM as a Cloud Serviceを使用する場合、送信電子メールでは暗号化が必要です。 デフォルトでは、送信メールは無効になっています。有効化するには、サポートチケットをに送信します。 [アクセスを要求](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=ja#sending-email).


## 関連記事

{{af-submit-action}}


