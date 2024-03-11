---
title: データを受け入れるスプレッドシートを準備する
description: スプレッドシートとアダプティブFormsブロックフィールドを使用して、強力なフォームをより迅速に作成できます。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 0643aee5-3a7f-449f-b086-ed637ae53b5a
source-git-commit: d91254b52c257a3758da200a2c74b736ca457884
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 1%

---

# データを受け入れるスプレッドシートを準備する


一度 [フォームの作成とプレビュー](/help/edge/docs/forms/create-forms.md)をクリックした場合、対応するスプレッドシートがデータの受信を開始できるようにします。

![ドキュメントベースのオーサリングエコシステム](/help/edge/assets/document-based-authoring-workflow-enable-sheet-to-accept-data.png)

<!-- 
>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

-->

スプレッドシートを有効にするには：

1. フォームのあるスプレッドシートを開き、新しいシートを追加して、名前をに変更します。 `incoming`.

   >[!WARNING]
   >
   > 次の場合、 `incoming` シートが存在しない場合、AEMはスプレッドシートにデータを送信しません。

1. このシートに、「intake_form」という名前のテーブルを挿入します。 フォームフィールド名と一致させる列数を選択します。 次に、ツールバーで挿入/テーブルに移動し、「OK」をクリックします。

1. テーブルの名前を「intake_form」に変更します。 Microsoft Excel で、テーブルの名前を変更するには、テーブルを選択し、「テーブルデザイン」をクリックします。

1. 次に、フォームフィールド名をテーブルヘッダーとして追加します。 フィールドが完全に同じであることを確認するには、「共有のデフォルト」シートからコピーして貼り付けます。  「共有のデフォルト」シートで、「名前」列の下に表示されるフォーム ID（送信フィールドを除く）を選択してコピーします。

1. 「incoming」シートで、「Paste Special」>「Transpose Rows to Columns」を選択し、この新しいシートの列ヘッダーとしてフィールド ID をコピーします。 その他のデータを取り込む必要があるフィールドのみを無視できます。

   各値 `Name` 列 `shared-default` シート（送信ボタンを除く）は、 `incoming` シート。 例えば、次の画像は「contact-us」フォームのヘッダーを示しています。

   ![連絡先 —Us フォームのフィールド](/help/edge/assets/contact-us-form-excel-sheet-fields.png)



1. AEM Sidekick拡張機能を使用して、フォームの更新をプレビューします。 これで、シートは受信フォーム送信を受け入れる準備が整いました。

   >[!NOTE]
   >
   >前にシートをプレビューした場合でも、作成後に再度プレビューする必要があります。 `incoming` シートを初めて取り出しました。


フィールド名を `incoming` シートが作成され、フォームが送信を受け入れる準備が整います。 フォームをプレビューし、それを使用してデータをシートに送信することができます。

シートがデータを受け取るように設定されたら、次の操作を実行できます。 [アダプティブFormsブロックを使用したフォームのプレビュー](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) または [POST要求の使用](#use-admin-apis-to-send-data-to-your-sheet) をクリックして、シートへのデータの送信を開始します。

>[!WARNING]
>
>  「共有のデフォルト」シートに、公開アクセスに不安な個人を特定できる情報や機密データを含めないでください。


## （オプション） Admin API を使用して、スプレッドシートでのデータ受け取りを有効にします

また、フォームにPOSTリクエストを送信して、フォームがデータを受け入れ、 `incoming` シート。 サービスは、POST要求を受け取ると、要求の本文を分析し、データ取り込みに必要な必須ヘッダーとシートを自律的に生成します。

Admin API を使用してスプレッドシートでのデータ受け取りを有効にするには：


1. 作成したワークブックを開き、デフォルトのシートの名前をに変更します。 `incoming`.

   >[!WARNING]
   >
   > 次の場合、 `incoming` シートが存在しないので、AEMはこのブックにデータを送信しません。

1. サイドキックでシートをプレビューします。

   >[!NOTE]
   >
   >前にシートをプレビューした場合でも、作成後に再度プレビューする必要があります。 `incoming` シートを初めて取り出しました。

1. POSTリクエストを送信し、 `incoming` シートを作成し、 `shared-default` シートをスプレッドシートに追加します（まだ存在しない場合）。

   シートを設定するPOSTリクエストの形式を設定する方法については、 [管理 API ドキュメント](https://www.aem.live/docs/admin.html#tag/authentication/operation/profile). 以下の例を確認できます。

   **リクエスト**

   ```JSON
   POST 'https://admin.hlx.page/form/{owner}/{repo}/{branch}/contact-us.json' \
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


   **応答**

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

   以下に示すように、curl やPostmanなどのツールを使用して、このPOSTリクエストを実行できます。

   ```JSON
   curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
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

   上記のPOSTリクエストでは、フォームフィールドとそれぞれのサンプル値を含むサンプルデータが提供されます。 このデータは、Admin サービスでフォームを設定するために使用されます。

   これで、フォームがデータの受け入れを有効にしました。 また、スプレッドシートには次の変更があります。

## データの受け入れが有効になった後のシートへの自動変更。


データを受け取るようにシートを設定すると、スプレッドシートに次の変更が表示されます。

Excel ブックまたはGoogleシートに「Slack」という名前のシートが追加されます。 このシートでは、新しいデータがスプレッドシートに取り込まれるたびに、指定したSlackチャネルの自動通知を設定できます。 現在、AEMは、AEMエンジニアリングSlack組織およびAdobeエンタープライズサポート組織にのみ通知をサポートしています。

1. Slack通知を設定するには、Slackワークスペースの「teamId」と「チャネル名」または「ID」を入力します。 「teamId」と「channel ID」に対して（debug コマンドを使用して）slack-bot に問い合わせることもできます。 チャネルの名前を変更しても存続するので、「チャネル名」の代わりに「チャネル ID」を使用することをお勧めします。

   >[!NOTE]
   >
   > 古いフォームには「teamId」列がありませんでした。 「teamId」が「#」または「/」で区切られたチャネル列に含まれていました。

1. 必要なタイトルを入力し、「フィールド」に、Slack通知に表示するフィールドの名前を入力します。 各見出しはコンマで区切る必要があります（例：名前、E メール）。

   >[!WARNING]
   >
   >  「共有のデフォルト」シートに、公開アクセスに不安な個人を特定できる情報や機密データを含めないでください。


## シートにデータを送信 {#send-data-to-your-sheet}

シートがデータを受け取るように設定された後、次の操作を実行できます。 [アダプティブFormsブロックを使用したフォームのプレビュー](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) または [管理 API の使用](#use-admin-apis-to-send-data-to-your-sheet) をクリックして、シートへのデータの送信を開始します。

### Admin API を使用してシートにデータを送信する

hlx.page、hlx.live、または実稼動ドメインを使用して、フォームに直接POSTリクエストを送信し、データを送信できます。


```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> URL には.json 拡張子を使用できません。 POST操作が機能するには、シートをパブリッシュする必要があります `.live` または実稼動ドメインの。

#### フォームデータの形式設定

POST本文のフォームデータを書式設定する方法はいくつかあります。 以下を使用できます。

* 配列 `name:value` ペア：

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

  例：

  ```JSON
  curl -s -i -X POST 'https://main--portal--wkndforms.hlx.page/contact-us' \
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



* ～を持つ物 `key:value` ペア：

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

  例：

  ```JSON
  curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
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

* URL エンコード (`x-www-form-urlencoded`) 本文 ( `content-type` ヘッダーをに設定 `application/x-www-form-urlencoded`)

  ```Shell
  'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&Message=I   +have+some+questions+about+your+products.&Phone=123-456-7890&Company=Adobe+Inc.&   Country=United+States&PreferredContactMethod=Email&SubscribeToNewsletter=true'
  ```

  例：

  ```Shell
  curl -s -i -X POST \
    -d 'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&   Message=I+have+some+questions+about+your+products.&Phone=123-456-7890& Company=Adobe+Inc.&Country=United+States&PreferredContactMethod=Email&   SubscribeToNewsletter=true' \
    https://main--portal--wkndforms.hlx.live/contact-us
  ```

次に、「ありがとうございます」メッセージをカスタマイズできます。 [「ありがとうございます」ページの設定](/help/edge/docs/forms/thank-you-page-form.md)または [リダイレクトの設定](/help/edge/docs/forms/thank-you-page-form.md).

