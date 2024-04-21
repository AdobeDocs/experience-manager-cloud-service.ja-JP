---
title: AEM Forms Edge 配信サービス用のドキュメントベースのオーサリングを使用してフォームを作成します
description: 完璧なフォームを素早く作成しましょう。⚡ AEM Forms Edge 配信+ ドキュメントベースのオーサリング =かつてないスピードと SEO に対応したフォームで、よりハッピーなユーザーと検索エンジンを実現。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 20%

---


# AEM Forms Edge 配信サービス用のドキュメントベースのオーサリングを使用してフォームを作成します

今日のデジタル時代では、ユーザーにわかりやすいフォームを作成することはどの組織にとっても不可欠です。AEM Forms Edge Delivery のドキュメントベースのオーサリングでは、Word やGoogle ドキュメントなどの使い慣れたツールを使用してフォームを作成できます。これらのフォームはMicrosoft Excel やGoogle Sheets ファイルにデータを直接送信するので、Google Sheets、Microsoft Excel、Microsoft Sharepoint の活発なエコシステムと堅牢な API を使用して、送信されたデータを簡単に処理したり、既存のビジネスワークフローを開始したりできます。

このガイドでは、次の手順について説明します。

* スプレッドシートの準備：データ収集用に Excel またはGoogle シートのファイルを設定し、そのファイルにフォームフィールドを追加する方法を説明します。
* シートへのデータの送信：POSTリクエストを使用してシートにデータを送信する方法を説明します。
* フォームの公開：フォームをAEM Sites ページに統合するか、スタンドアロンページとして公開します。

初心者からプロまで、このガイドを使用すると、ユーザーが気に入る美しく機能的なフォームを作成できます。 効率的なフォームの作成 – 今すぐ始めましょう。

## 事前準備

`WIP`

## データを受け取るスプレッドシートを準備します

1. Microsoft OneDrive またはGoogle Drive のAEM Edge 配信プロジェクトディレクトリの下の任意の場所に、Microsoft Excel ワークブックまたはGoogle シートを作成します。 このドキュメントでは、という名前のGoogle シートを使用します。 `contact-us.xlsx`Adobe Experience Manager（AEM）プロジェクトのルートにあります。

1. プロジェクトに設定されているAEM ユーザー（例：helix@adobe.com）に、シートの編集権限があることを確認します。

1. 作成したブックを開き、既定のシートの名前を [ 受信 ] に変更します。

   >[!NOTE]
   >
   > 「受信」シートが存在しない場合、AEMはこのブックにデータを送信しません。

1. Sidekick でシートをプレビューします。

   >[!NOTE]
   >
   >以前にシートをプレビューしたことがある場合でも、「受信」シートを初めて作成した後にもう一度プレビューする必要があります。

1. 入力するデータに一致するヘッダーを追加して、シートを準備します。 次の例では、「contact-us」フォームのフィールドを表示します。

   ![「お問い合わせ」フォームのフィールド](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

   これは、手動で行うことも、AEM Admin Service のフォームルートへのPOSTリクエストを使用して行うこともできます。 管理サービスはPOST本文内のデータを調べ、データを効果的に取り込んで Forms サービスを最大限に活用するために必要な適切なヘッダー、テーブル、シートを生成します。

   シートを設定する POST リクエストの形式については、[Admin API ドキュメント](https://www.hlx.live/docs/admin.html#tag/form)を参照してください。さらに、以下に示す例も参考にしてください。

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

前述のPOSTリクエストでは、フォームフィールドとそれぞれのサンプル値の両方を含むサンプルデータが提供されます。 このデータは、Admin サービスでフォームの設定に使用されます。

Admin サービスではシートの設定を推奨していますが、ヘッダーを手動で作成する場合は、『 』というドキュメントを参照してください。 [Forms シートの手動設定](https://www.hlx.live/docs/manual-forms-sheet-setup).

POSTリクエストを admin サービスに送信すると、ワークブックに次の変更内容が表示されます。

* 「shared-default」という名前の新しいシートが Excel ブックまたはGoogle シートに追加されます。 「shared-default」シートに存在するデータは、シートに対してGETリクエストを行った際に取得されます。 このシートは、スプレッドシート式を使用して受信データを要約し、他のコンテキストでの消費に役立てるための最適な場所として機能します。

  いかなる状況においても、「共有デフォルト」シートには、個人を特定できる情報や機密データが含まれていて、公開アクセスに不安を感じるようなことはありません。

* 「slack」という名前のシートが Excel ワークブックまたはGoogle シートに追加されます。 このシートでは、新しいデータがスプレッドシートに取り込まれるたびに、指定した Slack チャネルに対する自動通知を設定できます。現在、AEM では、AEM エンジニアリング Slack 組織とアドビエンタープライズサポート組織への通知のみをサポートします。

   1. Slack通知を設定するには、Slackワークスペースの「teamId」と「channel name」または「ID」を入力します。 また、slack ボットに（debug コマンドを使用して）「teamId」と「チャネル ID」を問い合わせることもできます。チャネル名を変更しても残り続けるので、「チャネル名」の代わりに「チャネル ID」を使用することをお勧めします。

      >[!NOTE]
      >
      > 古いフォームには「teamId」列がありませんでした。「teamId」は「#」または「/」で区切られてチャネル列に含まれていました。

   1. 必要なタイトルを入力し、「フィールド」に、Slack通知に表示するフィールドの名前を入力します。 各見出しはコンマで区切る必要があります（名前、メールなど）。

これで、シートがデータを受け取るように設定され、hlx.page、hlx.live、または実稼動ドメインを使用して、シートに直接POSTリクエストを送ることができるようになりました。


## シートへのデータの送信 {#send-data-to-your-sheet}

データを受け取るように設定されたシートに対して、hlx.page、hlx.live、または実稼動ドメインを使用して直接POSTリクエストを送信できます。

```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> URL には、.json 拡張子を付けることはできません。.live または実稼動ドメインでPOSTオペレーションを機能させるには、シートを公開する必要があります。

### EDS Formsのデータのフォーマット

POST本文では、いくつかの異なる方法でフォームデータを書式設定できます。

* 名前：値のペアの配列：

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

* `x-www-form-urlencoded` 本文（`content-type` ヘッダーはに設定する必要があります `application/x-www-form-urlencoded`） &#39;firstname=bruce&amp;lastname=banner&amp;email=bruce%40example.com&#39;



