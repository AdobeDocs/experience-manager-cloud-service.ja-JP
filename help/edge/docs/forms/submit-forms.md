---
title: データを受け入れるスプレッドシートの準備
description: スプレッドシートとアダプティブフォームブロックフィールドを使用して、強力なフォームをより迅速に作成します。
feature: Edge Delivery Services
exl-id: 0643aee5-3a7f-449f-b086-ed637ae53b5a
role: Admin, Architect, Developer
source-git-commit: 086706a1b9ab211738ea2978b73e1681b04ddac2
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 84%

---

# データの受け入れを開始するための Google Sheets または Microsoft Excel ファイルの設定


[フォームを作成してプレビュー](/help/edge/docs/forms/create-forms.md)したら、対応するスプレッドシートでデータの受信を開始できるようにします。スプレッドシートでデータを受け入れるように手動で有効にすることも、スプレッドシートでデータを受け入れるように Admin API を使用して有効にすることもできます。

![ドキュメントベースのオーサリングエコシステム](/help/edge/assets/document-based-authoring-workflow-enable-sheet-to-accept-data.png)

<!-- 
>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

-->


## スプレッドシートでデータを受け入れるように手動で有効にする

スプレッドシートでデータを受け入れるようにするには

1. フォームがあるスプレッドシートを開き、新しいシートを追加して、名前を `incoming` に変更します。 例えば、「[ 問い合わせ ](/help/edge/assets/enquiry.xlsx)」フォームのMicrosoft Excel ワークブックなどです。

   >[!WARNING]
   >
   > `incoming` シートが存在しない場合、AEM ではスプレッドシートにデータを送信しません。

2. このシートに、「intake_form」という名前のテーブルを挿入します。フォームフィールド名と一致させるために必要な列の数を選択します。次に、ツールバーで挿入／表に移動し、「OK」をクリックします。

3. 表の名前を「intake_form」に変更します。Microsoft Excel で表の名前を変更するには、表を選択し、「表書式」をクリックします。

4. 次に、フォームフィールド名を表ヘッダーとして追加します。フィールドが完全に同じであることを確認するには、「shared-default」シートからフィールドをコピー＆ペーストします。「shared-default」シートで、送信フィールドを除く「Name」列の下にリストされるフォーム ID を選択してコピーします。

5. 「incoming」シートで、形式を選択して貼り付け／行/列の入れ替えを選択して、フィールド ID をこの新しいシートの列ヘッダーとしてコピーします。データを取得する必要があるフィールドのみを保持し、他のフィールドは無視できます。

   `shared-default` の `Name` 列の各値は、送信ボタンを除き、`incoming` シートのヘッダーとして機能します。例えば、「問い合わせ」フォームのヘッダーを示す次の画像について考えてみます。

   ![お問い合わせフォームのフィールド](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

6. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 拡張機能を使用して、フォームの更新をプレビューします。 これで、シートはフォームの送信を受け入れる準備が整いました。

   >[!NOTE]
   >
   >以前にシートをプレビューしたことがある場合でも、`incoming` シートを初めて作成した後に再度プレビューする必要があります。


フィールド名が `incoming` シートに追加されると、フォームは送信を受け入れる準備が整います。フォームをプレビューし、これを使用してデータをシートに送信できます。

データを受信するようにシートを設定したら、[ フォームをプレビュー ](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) して <!--or [use POST requests](#use-admin-apis-to-send-data-to-your-sheet)--> シートへのデータの送信を開始できます。

>[!WARNING]
>
>  「shared-default」シートには、一般にアクセスされることに抵抗のある個人を特定できる情報や機密データを決して含めないでください。

<!--
### Use Admin APIs to enable a spreadsheet to accept data

You can also send a POST request to the form to enable it to accept data and configure headers for the `incoming` sheet. Upon receiving the POST request, the service analyzes the body of request and autonomously generates the essential headers and sheets needed for data ingestion.

To use Admin APIs to enable a spreadsheet to accept data: 


1. Open the workbook that you have created and change the name of the default sheet to `incoming`. 

    >[!WARNING] 
    >
    > If the `incoming` sheet doesn't exist, AEM won't send any data to this workbook.

1. Preview the sheet in the sidekick.

    >[!NOTE] 
    >
    >Even if you have previewed the sheet before, you must preview it again after creating the `incoming` sheet for the first time.

1. Send the POST request to generate the appropriate headers in the `incoming` sheet, and add the `shared-default` sheets to your spread sheet, if it does not exist already.

    To understand how to format the POST request for setting up your sheet, refer to the [Admin API documentation](https://www.aem.live/docs/admin.html#tag/authentication/operation/profile). You can look at the example provided below: 

    **Request** 
    
    ```JSON

    POST 'https://admin.aem.page/form/{owner}/{repo}/{branch}/contact-us.json' \
    --header 'Content-Type: application/json' \
    --data '{
        "data": {
            "Email": "john@wknd.com",
            "Name": "John",
            "Subject": "Regarding Product Inquiry",
            "Message": "I have some questions about your products.",
            "Phone": "123-456-7890",
            "Company": "Adobe Inc.",
            "Country": "United States",
            "PreferredContactMethod": "Email",
            "SubscribeToNewsletter": true
        }
    }'

    ```


    **Response**

    ```JSON

    HTTP/2 200 
    content-type: application/json
    x-invocation-id: 1b3bd30a-8cfb-4f85-a662-4b1f7cf367c5
    cache-control: no-store, private, must-revalidate
    accept-ranges: bytes
    date: Sat, 10 Feb 2024 09:26:48 GMT
    via: 1.1 varnish
    x-served-by: cache-del21736-DEL
    x-cache: MISS
    x-cache-hits: 0
    x-timer: S1707557205.094883,VS0,VE3799
    strict-transport-security: max-age=31557600
    content-length: 138

    {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country",      "PreferredContactMethod","SubscribeToNewsletter"]}%

    ```

    You can use tools like curl or Postman to execute this POST request, as demonstrated below:

    ```JSON

    curl -s -i -X POST 'https://admin.aem.page/form/wkndform/wefinance/main/contact-us.json' \
        --header 'Content-Type: application/json' \
        --data '{
            "data": {
                "Email": "john@wknd.com",
                "Name": "John",
                "Subject": "Regarding Product Inquiry",
                "Message": "I have some questions about your products.",
                "Phone": "123-456-7890",
                "Company": "Wknd Inc.",
                "Country": "United States",
                "PreferredContactMethod": "Email",
                "SubscribeToNewsletter": true
        }
    }'

    ```

    The above mentioned POST request provides sample data, including both form fields and their respective sample values. This data is used by the Admin service to set up the form.

    Your form is now enabled to accept data. You also observe the following changes in your spreadsheet: 

## Automatic changes to sheet once it is enabled to accept data. 

Once the sheet is set to recieve data, you observe the following changes in your spreadsheet: 

A sheet named "Slack" is added to your Excel Workbook or Google Sheet. In this sheet, you can configure automatic notifications for a designated Slack channel whenever new data is ingested into your spreadsheet. At present, AEM supports notifications exclusively to the AEM Engineering Slack organization and the Adobe Enterprise Support organization.

1. To set up Slack notifications enter the "teamId" of the Slack workspace and the "channel name" or "ID". You can also ask the slack-bot (with the debug command) for the "teamId" and the "channel ID". Using the "channel ID" instead of the "channel name" is preferable, as it survives channel renames.

    >[!NOTE] 
    >
    > Older forms didn't have the "teamId" column. The "teamId" was included in the channel column, separated by a "#" or "/".

1. Enter any title that you want and under fields enter the names of the fields you want to see in the Slack notification. Each heading should be separated by a comma (For example name, email).

    >[!WARNING] 
    >
    >  Never should the "shared-default" sheets contain any personally identifiable information or sensitive data that you are not comfortable with being publicly accessible.



<!--
## Send data to your sheet {#send-data-to-your-sheet}

After the sheet is set to receive data, you can [preview the form using Adaptive Forms Block](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) or [use Admin APIs](#use-admin-apis-to-send-data-to-your-sheet) to start sending data to the sheet.

### Use Admin APIs to send data to your sheet

You can send POST requests directly to your form using aem.page, aem.live, or your production domain, to send data. 


```JSON

POST https://branch–repo–owner.aem.(page|live)/email-form
POST https://my-domain.com/email-form

```

>[!NOTE] 
>
> The URL should not have the .json extension. You must publish the sheet for POST operations to function on `.live` or on the production domain.

#### Formatting the form data

There are a few different ways that you can format the form data in the POST body. You can use: 

* array of `name:value` pairs: 
    
    ```JSON
    
    {
      "data": [
        { "name": "name", "value": "Clark Kent" },
        { "name": "email", "value": "superman@example.com" },
        { "name": "subject", "value": "Regarding Product Inquiry" },
        { "name": "message", "value": "I have some questions about your products." },
        { "name": "phone", "value": "123-456-7890" },
        { "name": "company", "value": "Example Inc." },
        { "name": "country", "value": "United States" },
        { "name": "preferred_contact_method", "value": "Email" },
        { "name": "newsletter_subscribe", "value": true }
      ]
    }

    ```

    For example

    ```JSON

    curl -s -i -X POST 'https://main--wefinance--wkndform.aem.page/contact-us' \
        --header 'Content-Type: application/json' \
        --data '{
        "data": [
            { "name": "name", "value": "Clark Kent" },
            { "name": "email", "value": "superman@example.com" },
            { "name": "subject", "value": "Regarding Product Inquiry" },
            { "name": "message", "value": "I have some questions about your        products." },
            { "name": "phone", "value": "123-456-7890" },
            { "name": "company", "value": "Example Inc." },
            { "name": "country", "value": "United States" },
            { "name": "preferred_contact_method", "value": "Email" },
            { "name": "newsletter_subscribe", "value": true }
        ]
    }'

    ```



* an object with `key:value` pairs:

    ```JSON

        {
          "data": {
            "name": "Jessica Jones",
            "email": "jj@example.com",
            "subject": "Regarding Product Inquiry",
            "message": "I have some questions about your products.",
            "phone": "123-456-7890",
            "company": "Example Inc.",
            "country": "United States",
            "preferred_contact_method": "Email",
            "newsletter_subscribe": true
          }
        }

    ```

    For example,

    ```JSON

    curl -s -i -X POST 'https://admin.aem.page/form/wkndform/wefinance/main/contact-us.json' \
    --header 'Content-Type: application/json' \
    --data '{
        "data": {
            "Email": "khushwant@wknd.com",
            "Name": "khushwant",
            "Subject": "Regarding Product Inquiry",
            "Message": "I have some questions about your products.",
            "Phone": "123-456-7890",
            "Company": "Adobe Inc.",
            "Country": "United States",
            "PreferredContactMethod": "Email",
            "SubscribeToNewsletter": true
        }
    }'

    ```

* URL encoded (`x-www-form-urlencoded`) body (with `content-type` header set to `application/x-www-form-urlencoded`)

    ```Shell

    'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&Message=I   +have+some+questions+about+your+products.&Phone=123-456-7890&Company=Adobe+Inc.&   Country=United+States&PreferredContactMethod=Email&SubscribeToNewsletter=true'

    ```

    For example, if your project's repository is named "wefinance", it's located under the account owner "wkndform", and you're using the "main" branch.,

    ```Shell

    curl -s -i -X POST \
      -d 'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&   Message=I+have+some+questions+about+your+products.&Phone=123-456-7890& Company=Adobe+Inc.&Country=United+States&PreferredContactMethod=Email&   SubscribeToNewsletter=true' \
      https://main--wefinance--wkndform.aem.live/contact-us

    ```
-->

次に、[「ありがとうございます」メッセージをカスタマイズ](/help/edge/docs/forms/thank-you-page-form.md)できます。

## 関連トピック

{{see-more-forms-eds}}
