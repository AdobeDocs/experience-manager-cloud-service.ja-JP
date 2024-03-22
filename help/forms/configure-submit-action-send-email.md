---
Title: How to send an email on submission of an Adaptive Form?
Description: Explore the process to set up email notifications when submitting an Adaptive Form.
keywords: アダプティブフォーム用のメールの送信方法、メール送信アクション、アダプティブフォームメール、フォーム送信メール、メールの送信ガイド
feature: Adaptive Forms, Core Components
source-git-commit: f1db04e6cd1f78c1530aefd29f5f036ca5e70873
workflow-type: ht
source-wordcount: '437'
ht-degree: 100%

---


# アダプティブフォームのメール送信アクションの送信を設定する

「**[!UICONTROL メールを送信]**」送信アクションでは、フォームの送信が完了すると同時に、1 人または複数の受信者にメールを送信できます。この送信アクションを使用すると、事前に定義された形式のフォームデータを含むメールを作成できます。例えば、次のテンプレートで、送信されたフォームデータから顧客名、配送先住所、都道府県名、郵便番号が取得されるとします。


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

「メールを送信」送信アクションを使用してアダプティブフォームを設定する利点には、次のようなものがあります。

* 指定されたメール受信者にフォームデータが直接送信されるので、迅速な通信が可能です。
* これにより、フォーム送信をメール通知に直接統合することで、ワークフローを合理化できます。
* これは、組織がメールのコンテンツをカスタマイズするのに役立ち、特定のコミュニケーションニーズに適したものにすることができます。

## 「メールを送信」送信アクションを設定する {#steps-to-configure-send-email-submit-action}

送信アクションを設定するには：

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブをクリックします。
1. **[!UICONTROL 送信アクション]**&#x200B;ドロップダウンリストから「**[!UICONTROL メールを送信]**」を選択します。

   ![「メールを送信」のアクション設定](/help/forms/assets/send-email-action-configuration.gif)
1. **[!UICONTROL 送信者]**&#x200B;テキストボックスで送信者のメール ID を指定します。
1. **[!UICONTROL 宛先]**&#x200B;テキストボックスに受信者のメール ID を追加します。複数の受信者を追加するには「**[!UICONTROL 追加]**」ボタンをクリックします。
1. [オプション] CC および BCC の受信者を追加するには、「**[!UICONTROL 追加]**」ボタンをクリックします。
1. **[!UICONTROL 件名]**&#x200B;テキストボックスで件名行を指定します。
1. メールテンプレートを追加して「メールを送信」送信アクションを設定します。
   * **[!UICONTROL 外部テンプレートのパス]**&#x200B;オプションを使用して、AEM アセットに保存されている外部メールテンプレートのパスを指定できます。
   * また、**[!UICONTROL メールテンプレート]**&#x200B;テキストボックスで、フォーム送信用のカスタムメールテンプレートを追加できます。
1. [オプション] **[!UICONTROL 「メールを送信」]**&#x200B;送信アクションには、メールに添付ファイルと[レコードのドキュメント（DoR）](generate-document-of-record-core-components.md)を含めるオプションが用意されています。
1. 「**[!UICONTROL 完了]**」をクリックします。

## ベストプラクティス {#best-practices}

* メールの内容は明確かつ簡潔にすることをお勧めします。ユーザーは、メールの目的と、実行する必要があるアクションを理解する必要があります。
* フォームフィールドがアダプティブフォーム内の別のパネルに配置されている場合でも、すべてのフォームフィールドに一意の要素名を付けることをお勧めします。
* AEM as a Cloud Serviceを使用する場合、送信電子メールでは暗号化が必要です。 デフォルトでは、送信メールは無効になっています。それを有効にするには、[利用申請](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=ja#sending-email)にサポートチケットを送信します。


## 関連記事

{{af-submit-action}}


