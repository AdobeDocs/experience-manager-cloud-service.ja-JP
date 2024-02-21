---
title: スプレッドシートからFormsへ — フォームブロックのフィールド検証のマスタリング
description: スプレッドシートとフォームブロックフィールドを使用して、強力なフォームをより迅速に作成できます。 このガイドは、EDS Forms Block フィールドのカスタム検証を構築する場合に役立ちます。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0604838311bb9ab195789fad755b0910e09519fd
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 1%

---


# フォームを有効にしてデータを送信

フォームの作成とプレビューが完了したら、対応するシートを有効にしてデータを受け入れます。 データの受け入れを開始するには、収集するデータに一致するヘッダーを含めるようにスプレッドシートを設定します。 &#39;shared-default&#39;シートに追加されたすべてのヘッダーも、テーブルの下の&#39;incoming&#39;シートに存在する必要があります。

次の例では、「contact-us」フォームのフィールドを表示します。

![連絡先 —Us フォームのフィールド](/help/edge/assets/contact-us-form-excel-sheet-fields.png)


設定が完了すると、フォームは送信を受け入れる準備が整います。 スプレッドシートでデータを受け入れる方法は、次のいずれかです。

* [データを受け入れるスプレッドシートを手動で設定](#manually-configure-a-spreadsheet-to-receive-data)

* [Admin API を使用して、スプレッドシートでのデータ受け取りを有効にします](#use-admin-apis-to-enable-a-spreadsheet-to-receive-data-use-admin-apis-to-enable-a-spreadsheet-to-recieve-data)

## データを受け入れるスプレッドシートを手動で設定

データを受け入れるスプレッドシートを手動で設定するには、次の手順に従います。


1. 作成したワークブックを開き、デフォルトのシートの名前を「受信中」に変更します。

   >[!WARNING]
   >
   > 「受信」シートが存在しない場合、AEMはこのブックにデータを送信しません。

1. 入力するデータに一致するヘッダーを追加して、シートを準備します。 次の例では、「contact-us」フォームのフィールドを表示します。

   ![連絡先 —Us フォームのフィールド](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. サイドキックでシートをプレビューします。

   >[!NOTE]
   >
   >前にシートをプレビューした場合でも、初めて「受信」シートを作成した後で再度プレビューする必要があります。


## Admin API を使用して、スプレッドシートでのデータ受け取りを有効にします

AEM Admin Service 内で、フォームルートへのPOSTリクエストを開始できます。 管理サービスは、POST本文データを受け取ると、そのデータを分析し、データの取り込みに必要な基本的なヘッダー、テーブル、シートを自律的に生成し、forms サービスの機能を最適化します。

Admin API を使用してスプレッドシートでのデータ受け取りを有効にするには：


1. 作成したワークブックを開き、デフォルトのシートの名前を「受信中」に変更します。

   >[!WARNING]
   >
   > 「受信」シートが存在しない場合、AEMはこのブックにデータを送信しません。

1. サイドキックでシートをプレビューします。

   >[!NOTE]
   >
   >前にシートをプレビューした場合でも、初めて「受信」シートを作成した後で再度プレビューする必要があります。

1. 入力するデータに一致するヘッダーを追加して、シートを準備します。

   これをおこなうには、AEM Admin サービスのフォームルートにPOSTリクエストを送信します。 管理サービスは、POST本文のデータを調べ、データを効果的に取り込み、Formsサービスを最大限に活用するために必要な適切なヘッダー、テーブル、シートを生成します。

   シートを設定するPOSTリクエストの形式を設定する方法については、 [管理 API ドキュメント](https://www.hlx.live/docs/admin.html#tag/form). また、次の例を見てみましょう。

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

   前述のPOSTリクエストでは、フォームフィールドとそれぞれのサンプル値を含むサンプルデータが提供されます。 このデータは、Admin サービスでフォームを設定するために使用されます。

   管理サービスにPOSTリクエストを送信すると、ワークブック内で次の変更が確認されます。

* Excel ブックまたはGoogleシートに、「shared-default」という名前の新しいシートが追加されます。 「shared-default」シートに存在するGETは、シートに対してデータリクエストを実行する際に取得されます。 このシートは、スプレッドシートの数式を使用して受信データを要約し、他のコンテキストでの消費に役立てる最適な場所として機能します。

  「共有のデフォルト」シートに、公開アクセスに不安な個人を特定できる情報や機密データを含めないでください。

* Excel ブックまたはGoogleシートに「Slack」という名前のシートが追加されます。 このシートでは、新しいデータがスプレッドシートに取り込まれるたびに、指定したSlackチャネルの自動通知を設定できます。 現在、AEMは、AEMエンジニアリングSlack組織およびAdobeエンタープライズサポート組織にのみ通知をサポートしています。

   1. Slack通知を設定するには、Slackワークスペースの「teamId」と「チャネル名」または「ID」を入力します。 「teamId」と「channel ID」に対して（debug コマンドを使用して）slack-bot に問い合わせることもできます。 チャネルの名前を変更しても存続するので、「チャネル名」の代わりに「チャネル ID」を使用することをお勧めします。

      >[!NOTE]
      >
      > 古いフォームには「teamId」列がありませんでした。 「teamId」が「#」または「/」で区切られたチャネル列に含まれていました。

   1. 必要なタイトルを入力し、「フィールド」に、Slack通知に表示するフィールドの名前を入力します。 各見出しはコンマで区切る必要があります（例：名前、E メール）。

これで、シートがデータを受け取るように設定され、次の操作が可能になります。 [forms ブロックを使用してフォームをプレビューする](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) または [POST要求の使用](#use-admin-apis-to-send-data-to-your-sheet) をクリックして、シートへのデータの送信を開始します。



## シートにデータを送信 {#send-data-to-your-sheet}

シートがデータを受け取るように設定された後、次の操作を実行できます。 [forms ブロックを使用してフォームをプレビューする](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) または [管理 API の使用](#use-admin-apis-to-send-data-to-your-sheet) をクリックして、シートへのデータの送信を開始します。

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

次に、「ありがとうございます」というメッセージをカスタマイズします。 [「ありがとうございます」ページの設定](/help/edge/docs/forms/thank-you-page-form.md)または [リダイレクトの設定](/help/edge/docs/forms/thank-you-page-form.md).

## 詳細を表示する

* [フォームの作成とプレビュー](/help/edge/docs/forms/create-forms.md)
* [フォームからデータを送信できるようにする](/help/edge/docs/forms/submit-forms.md)
* [サイトページにフォームを発行する](/help/edge/docs/forms/publish-eds-forms.md)
* [フォームフィールドに検証機能を追加する](/help/edge/docs/forms/validate-forms.md)
* [フォームのテーマとスタイルを変更する](/help/edge/docs/forms/style-theme-forms.md)