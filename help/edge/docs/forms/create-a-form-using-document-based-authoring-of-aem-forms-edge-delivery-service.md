---
title: AEM Forms Edge Delivery Service のドキュメントベースのオーサリングを使用したフォームの作成
description: 完璧なフォームを素早く作成しましょう。⚡ AEM Forms Edge Delivery + ドキュメントベースのオーサリング = 超高速かつ SEO に対応したフォームで、高い顧客満足度と検索エンジンを実現。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: ht
source-wordcount: '889'
ht-degree: 100%

---


# AEM Forms Edge Delivery Service のドキュメントベースのオーサリングを使用したフォームの作成

今日のデジタル時代では、ユーザーにわかりやすいフォームを作成することはどの組織にとっても不可欠です。AEM Forms Edge Delivery のドキュメントベースのオーサリングでは、Word や Google ドキュメントなどの使い慣れたツールを使用してフォームを作成できます。これらのフォームは、Microsoft Excel または Google Sheets ファイルに直接データを送信します。これにより、Google Sheets、Microsoft Excel、Microsoft SharePoint の活発なエコシステムと堅牢な API を使用して、送信されたデータを簡単に処理したり、既存のビジネスワークフローを開始したりできます。

このガイドでは、次の方法について説明します。

* スプレッドシートの準備：データ収集用に Excel または Google Sheets ファイルを設定し、フォームフィールドを追加する方法について説明します。
* シートへのデータの送信：POST リクエストを使用してシートにデータを送信する方法について説明します。
* フォームの公開：フォームを AEM Sites ページに統合するか、スタンドアロンページとして公開します。

初心者でもプロでも、このガイドを参照すると、ユーザーに好まれる美しく機能的なフォームを作成できます。効率的なフォーム作成を今すぐ実現しましょう。

## 事前準備

`WIP`

## データを受信するスプレッドシートの準備

1. Microsoft OneDrive または Google Drive 上の AEM Edge Delivery プロジェクトディレクトリ下の任意の場所で、Microsoft Excel ワークブックまたは Google Sheets を作成します。このドキュメントでは、Adobe Experience Manager（AEM）プロジェクトのルートにある `contact-us.xlsx` という名前の Google Sheets を使用します。

1. プロジェクト用に設定された AEM ユーザー（helix@adobe.com など）にシートの編集権限をあることを確認します。

1. 作成したワークブックを開き、デフォルトのシートの名前を「incoming」に変更します。

   >[!NOTE]
   >
   > 「incoming」シートが存在しない場合、AEM ではこのワークブックにデータを送信しません。

1. Sidekick でシートをプレビューします。

   >[!NOTE]
   >
   >以前にシートをプレビューしたことがある場合でも、「incoming」シートを初めて作成した後に再度プレビューする必要があります。

1. 入力するデータに一致するヘッダーを追加してシートを準備します。次の例では、「お問い合わせ」フォームのフィールドを表示します。

   ![お問い合わせフォームのフィールド](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

   これは、手動で行うことも、AEM Admin サービスのフォームルートへの POST リクエストを使用して行うこともできます。Admin サービスでは、POST 本文内のデータを検査し、データを効果的に取り込んでフォームサービスを最大限に活用するのに必要な適切なヘッダー、テーブル、シートを生成します。

   シートを設定する POST リクエストの形式について詳しくは、[Admin API ドキュメント](https://www.hlx.live/docs/admin.html#tag/form)を参照してください。また、以下の例も参照してください。

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
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country","PreferredContactMethod","SubscribeToNewsletter"]}%
   ```

   以下に示すように、cURL や Postman などのツールを使用して、この POST リクエストを実行できます。

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

上記の POST リクエストでは、フォームフィールドとそれぞれのサンプル値の両方を含むサンプルデータを提供します。このデータは、フォームの設定のために Admin サービスによって使用されます。

Admin サービスではシートの設定を推奨していますが、ヘッダーを手動で作成する場合は、[手動でのフォームシートの設定](https://www.hlx.live/docs/manual-forms-sheet-setup)というタイトルのドキュメントを参照してください。

POST リクエストを Admin サービスに送信すると、ワークブックに次の変更内容が表示されます。

* 「shared-default」という新しい名前のシートが Excel ワークブックまたは Google Sheets に追加されます。「shared-default」シートに存在するデータは、シートに対して GET リクエストを行うと取得されます。このシートは、スプレッドシートの数式を使用して受信データを要約するための最適な場所として機能し、他のコンテキストでの利用に役立ちます。

  いかなる状況でも、「shared-default」シートには、一般にアクセスされることに抵抗のある個人を特定できる情報や機密データを決して含めないでください。

* 「Slack」という名前のシートが Excel ワークブックまたは Google Sheets に追加されます。このシートでは、新しいデータがスプレッドシートに取り込まれるたびに、指定した Slack チャネルに対する自動通知を設定できます。現在、AEM では、AEM エンジニアリング Slack 組織とアドビエンタープライズサポート組織への通知のみをサポートします。

   1. Slack 通知を設定するには、Slack ワークスペースの「teamId」と、「チャネル名」または「ID」を入力します。また、slack ボットに（debug コマンドを使用して）「teamId」と「チャネル ID」を問い合わせることもできます。チャネル名を変更しても残り続けるので、「チャネル名」の代わりに「チャネル ID」を使用することをお勧めします。

      >[!NOTE]
      >
      > 古いフォームには「teamId」列がありませんでした。「teamId」は「#」または「/」で区切られてチャネル列に含まれていました。

   1. 必要なタイトルを入力し、フィールドの下に Slack 通知に表示するフィールドの名前を入力します。各見出しはコンマで区切る必要があります（名前、メールなど）。

これで、シートがデータを受け取るように設定され、hlx.page、hlx.live または実稼動ドメインを使用して、シートに POST リクエストを直接送信できるようになりました。


## シートへのデータの送信 {#send-data-to-your-sheet}

データを受け取るように設定されたシートに対して、hlx.page、hlx.live または実稼動ドメインを使用して POST リクエストを直接送信し、データを送信できます。

```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> URL には、.json 拡張子を付けることはできません。POST 操作が .live または実稼動ドメインで機能するには、シートを公開する必要があります。

### EDS Forms データの書式設定

POST 本文のフォームデータを書式設定するには、いくつかの方法があります。

* 名前の配列：値のペア：

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
              { "name": "message", "value": "I have some questions about your products." },
              { "name": "phone", "value": "123-456-7890" },
              { "name": "company", "value": "Example Inc." },
              { "name": "country", "value": "United States" },
              { "name": "preferred_contact_method", "value": "Email" },
              { "name": "newsletter_subscribe", "value": true }
              ]
          }'
  
* キーと値のペアを持つオブジェクト

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

* `x-www-form-urlencoded` 本文（`content-type` ヘッダーは `application/x-www-form-urlencoded` に設定する必要があります）
&#39;firstname=bruce&amp;lastname=banner&amp;email=bruce%40example.com&#39;



