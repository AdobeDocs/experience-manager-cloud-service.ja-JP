---
title: 送信アクション
description: アダプティブフォームの送信アクションを設定します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 100%

---

# アダプティブフォーム送信アクション

送信アクションは、アダプティブフォームを通じて収集されたデータの送信先を指定します。送信プロセスは、ユーザーがフォームの「**[!UICONTROL 送信]**」ボタンをクリックすると開始されます。AEM Forms には、以下に説明する 2 つのタイプの送信アクションが用意されており、特定のニーズに合わせてカスタム送信アクションを作成および使用できます。標準の使用できる送信アクションは次のとおりです。

<!--To define a Submit Action for an Adaptive Form, you use the Properties dialog of the **Adaptive Form block** in the **Editor**-->

* [REST エンドポイントに送信](#rest-endpoint-submission-ue)
* [メールを送信](#email-submission-ue)


### REST エンドポイントに送信 {#rest-endpoint-submission-ue}

REST エンドポイントに送信アクションを使用すると、送信したフォームデータを指定された REST エンドポイントに送信できます。エンドポイントは、フォームがホストされている内部サーバーや、相対パスまたは絶対パスを使用して外部サーバーに属することができます。フォームをホストする AEM サーバーにデータを送信するには、AEM サーバーのルートパスに対応する相対パスを使用します。例えば、`/content/forms/af/SampleForm.html` のようになります。他のサーバーにデータを送信するには、絶対パスを使用します。

<!--Configuring the Submit Action to REST Endpoint for Adaptive Forms offers several benefits such as:  
* It facilitates seamless integration of form data with external systems and services via RESTful APIs.  
* Offers flexibility in managing data submissions from Adaptive Forms, accommodating dynamic and complex data structures.  
* Allows dynamic mapping of form fields to parameters within the REST endpoint URL, enabling adaptable and customizable data submissions.
-->



REST エンドポイントを設定するには：

1. アダプティブフォームを&#x200B;**[!UICONTROL エディター]**&#x200B;で開きます。
1. 「**[!UICONTROL アダプティブフォームブロック]**」を選択します。
1. プロパティ ![プロパティ](/help/forms/assets/Smock_Properties_18_N.svg) アイコンをクリックします。
1. **[!UICONTROL 送信アクション]**&#x200B;ドロップダウンリストから「**[!UICONTROL REST エンドポイントに送信]**」を選択します。
1. REST エンドポイント URL を指定します。
1. また、**POST リクエストを有効にする**&#x200B;ことで、リクエストを投稿する URL を指定することもできます。

![アダプティブフォームの POST リクエストを有効にする](/help/forms/assets/enable-post-request-ue.png)

>[!NOTE]
>
> * 内部サーバーにデータを POST 送信するには、リソースのパスを指定します。データは、リソースのパスに POST されます。例えば、`/content/restEndPoint` のようになります。このような POST リクエストには、送信リクエストの認証情報が使用されます。
> * 外部サーバーにデータを POST 送信するには、URL を指定します。URL の形式は、`https://host:port/path_to_rest_end_point` です。POST リクエストを匿名で処理するためのパスを設定してください。

### メールを送信 {#email-submission-ue}

「メールを送信」送信アクションでは、フォームの送信が完了すると同時に、1 人または複数の受信者にメールを送信できます。「メールを送信」設定を使用すると、事前に定義された形式のフォームデータを含むメールを作成できます。例えば、次のテンプレートで、送信されたフォームデータから顧客名、配送先住所、都道府県名、郵便番号が取得されるとします。[詳しくは、アダプティブフォームのメールテンプレートを参照してください](/help/forms/html-email-templates-in-adaptive-forms.md)。「メールを送信」送信アクションを使用してアダプティブフォームを設定する利点には、次のようなものがあります。

1. 指定されたメール受信者にフォームデータが直接送信されるので、迅速な通信が可能です。
1. これにより、フォーム送信をメール通知に直接統合することで、ワークフローを合理化できます。
1. これは、組織がメールのコンテンツをカスタマイズするのに役立ち、特定のコミュニケーションニーズに適したものにすることができます。

![ユニバーサルエディターでのアダプティブフォームのプロパティ](/help/forms/assets/submit-actions-ue.png)


送信アクションをフォーム送信用のメールとして設定するには：

1. アダプティブフォームを&#x200B;**エディター**&#x200B;で開きます。
1. 「**[!UICONTROL アダプティブフォームブロック]**」を選択します。
1. プロパティ ![プロパティ](/help/forms/assets/Smock_Properties_18_N.svg) アイコンをクリックします。
1. **[!UICONTROL 送信アクション]**&#x200B;ドロップダウンリストから「**[!UICONTROL メールを送信]**」を選択します。
1. 「メールを送信」オプションを選択すると、次の画像に示すように次のプロパティを設定できます。

<table>
  <thead>
    <tr>
      <th>画像</th>
      <th>プロパティ</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
    <td rowspan="7"><img src="/help/forms/assets/email-config-ue.png" alt="メール設定"></td> 
    <td><b>送信元</td>
    <td>送信者のメールアドレスを指定します。</td>
    </tr>
    <tr>
      <td><b>宛先</td>
      <td>メールのプライマリ受信者を指定します。複数のメールアドレスを追加する場合は、コンマで区切ります。</td>
    </tr>
    <tr>
      <td><b>CC</td>
      <td>メールのカーボンコピー（CC）を受信する受信者を指定します。</td>
    </tr>
    <tr>
      <td><b>BCC</td>
      <td>メールのブラインドカーボンコピー（BCC）を受信する受信者を指定します。</td>
    </tr>
    <tr>
      <td><b>件名</td>
      <td>メールの件名を指定します。</td>
    </tr>
    <tr>
      <td><b>外部テンプレートを使用</td>
      <td>メールコンテンツの書式設定に外部メールテンプレートを使用できます。外部テンプレートへの URL またはパスを指定して、AEM Assets フォルダーでホストされる事前設計済みのメールテンプレートを統合します。</td>
    </tr>
    <tr>
      <td><b>添付ファイルを含める</td>
      <td>送信されたフォームデータに、フォーム経由でメールに送信された添付ファイルを含める必要があるかどうかを指定します。サポートされている添付ファイル形式は、PDF、XML および JSON です。</td>
    </tr>
  </tbody>
</table>






<!--
        
        * **From**: The email address of the sender.
        * **To**: Specify the primary recipients of the email, multiple email addresses can be added, separated by commas.
        * **CC**: Specify the recipients who should receive a carbon copy (CC) of the email.
        * **BCC**: Specify the recipients who should receive a blind carbon copy (BCC) of the email.
        * **Subject**: Specify the subject line of the email.
        * **Use External Template**: Enables the use of an external email template for formatting the email content. Provide the URL or path to the External template path to integrate a pre-designed email template hosted in your AEM Assets folder.
        * **Include Attachment**: Specifies whether the submitted form data should include an attachment submitted through the form in the email.

    {width=50%,height=50%}![Enable post request for adaptive forms](/help/forms/assets/email-config-ue.png)

-->

## アダプティブフォームの送信時にカスタムのお礼のメッセージを表示 {#submit-action-message-ue}

「送信時」オプションを使用すると、アダプティブフォームの送信時に送信アクションメッセージを設定して、フォームの送信アクションメッセージを設定できます。

1. アダプティブフォームを&#x200B;**エディター**&#x200B;で開きます。
1. 「**[!UICONTROL アダプティブフォームブロック]**」を選択します。
1. プロパティ ![プロパティ](/help/forms/assets/Smock_Properties_18_N.svg) アイコンをクリックします。
1. クリックすると、次のオプションが表示されます。
   * **[!UICONTROL 送信時]**：送信時は、フォームを送信したときに表示されるメッセージをカスタマイズするのに役立ちます。デフォルトでは、フォームが正常に送信されると、「フォームを送信していただきありがとうございます」というカスタムメッセージがユーザーに表示されます。
また、「**[!UICONTROL メッセージを表示]**」オプションを選択してフォームの送信時に「ありがとうございます」メッセージをカスタマイズしたり、リッチテキスト&#x200B;**エディター**&#x200B;でメッセージを追加／編集したりできます。


## 関連トピック

{{universal-editor-see-also}}

