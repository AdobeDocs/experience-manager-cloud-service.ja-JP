---
title: AEM Forms Edge Delivery Service 用のドキュメントベースのオーサリングを使用したフォームの作成
description: クラフトパーフェクトフォーム、高速！ ⚡ AEM Forms Edge Delivery + doc-based authoring =超高速で SEO に対応したフォームで、より幸せなユーザーと検索エンジンを実現。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: f2752673dcaa0762bb55719cee23765aa8ecde96
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---


# AEM Forms Edge Delivery Service 用のドキュメントベースのオーサリングを使用したフォームの作成

今日のデジタル時代では、どの組織でも、使いやすいフォームを作成することが不可欠です。 AEM Forms Edge Delivery のドキュメントベースのオーサリングでは、Word やGoogle Docs などの使い慣れたツールを使用してフォームを作成できます。これらのフォームはMicrosoft Excel やGoogle Sheets ファイルに直接送信され、Googleシート、Microsoft Excel、Microsoft Sharepoint の活発なエコシステムと堅牢な API を使用できます。

このガイドでは、以下の手順について説明します。

* スプレッドシートの準備：データ収集用に Excel またはGoogle Sheet ファイルを設定し、それにフォームフィールドを追加する方法を説明します。
* シートへのデータ送信：POSTリクエストを使用してシートにデータを送信する方法を説明します。
* フォームの公開：フォームをAEM Sitesページに統合するか、スタンドアロンページとして公開します。

初心者でもプロでも、このガイドを使用すると、ユーザーが好む美しい機能的なフォームを構築できます。 効率的なフォーム作成のロックを解除しましょう。すぐに開始します。

## 事前準備

`WIP`

## データを受け取るためのスプレッドシートの準備

1. Microsoft OneDrive またはGoogle Drive のAEM Edge Delivery プロジェクトディレクトリの下の任意の場所で、Microsoft Excel ワークブックまたはGoogleシートを作成できます。 このドキュメントでは、Google Sheet の名前を使用します `contact-us.xlsx`:Adobe Experience Manager(AEM) プロジェクトのルートにあります。

1. プロジェクト用に設定したAEMユーザー ( 例：helix@adobe.com) に、シートの編集権限があることを確認します。

1. 作成したワークブックを開き、デフォルトのシートの名前を「受信中」に変更します。

   >[!NOTE]
   >
   > 「受信」シートが存在しない場合、AEMはこのブックにデータを送信しません。

1. サイドキックでシートをプレビューします。

   >[!NOTE]
   >
   >前にシートをプレビューした場合でも、初めて「受信」シートを作成した後で再度プレビューする必要があります。

1. 入力するデータに一致するヘッダーを追加して、シートを準備します。 次の例では、「contact-us」フォームのフィールドを表示します。

   ![連絡先 —Us フォームのフィールド](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

   これは、手動でおこなうか、AEM Admin サービスのフォームルートへのPOSTリクエストを使用しておこなうことができます。 管理サービスは、POST本文内のデータを調べ、データを効果的に取り込み、forms サービスを最大限に活用するために必要な適切なヘッダー、テーブル、シートを生成します。

   シートを設定するPOSTリクエストの形式を設定する方法については、 [管理 API ドキュメント](https://www.hlx.live/docs/admin.html#tag/form). さらに、次の例を見てみましょう。

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

前述のPOSTリクエストでは、フォームフィールドとそれぞれのサンプル値を含むサンプルデータが提供されます。 このデータは、Admin サービスでフォームの設定に使用されます。

シートの設定をお勧めしますが、ヘッダーを手動で作成する場合は、という名前のドキュメントを参照してください [手動でのFormsシートの設定](https://www.hlx.live/docs/manual-forms-sheet-setup).

管理サービスにPOSTリクエストを送信すると、ワークブックに次の変更が反映されます。

* Excel ブックまたはGoogleシートに、「shared-default」という名前の新しいシートが追加されます。 「shared-default」シートに存在するGETは、シートに対してデータリクエストを実行する際に取得されます。 このシェットは、スプレッドシートの数式を使用して受信データを要約し、他のコンテキストでの消費に役立てる最適な場所として機能します。

  状況によっては、「共有されるデフォルト」シートに、公にアクセスできない個人を特定できる情報や機密データが含まれているはずはありません。

* Excel ブックまたはGoogleシートに、「slack」という名前のシートが追加されます。 このシートでは、新しいデータがスプレッドシートに取り込まれるたびに、指定したSlackチャネルの自動通知を設定できます。 現在、AEMは、AEMエンジニアリングSlack組織およびAdobeエンタープライズサポート組織にのみ通知をサポートしています。

   1. Slack通知を設定するには、Slackワークスペースの「teamId」と、「チャネル名」または「ID」を入力します。 「teamId」と「channel ID」に対して（debug コマンドを使用して）slack-bot に問い合わせることもできます。 チャネルの名前を変更しても存続するので、「チャネル名」の代わりに「チャネル ID」を使用することをお勧めします。

      >[!NOTE]
      >
      > 古いフォームには「teamId」列がありませんでした。 「teamId」が「#」または「/」で区切られたチャネル列に含まれていました。

   1. 必要なタイトルを入力し、「フィールド」に、Slack通知に表示するフィールドの名前を入力します。 各見出しはコンマで区切る必要があります（例：名前、E メール）。

これで、シートはデータを受け取るように設定され、hlx.page、hlx.live、または実稼動ドメインを使用して、POSTリクエストを直接送信できます。


## シートにデータを送信 {#send-data-to-your-sheet}

シートがデータを受け取るように設定されたら、hlx.page、hlx.live、または実稼働ドメインを使用してPOST要求を直接送信し、データを送信できます。

```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> URL には.json 拡張子を使用できません。 POST操作が.live または実稼動ドメインで機能するには、シートをパブリッシュする必要があります。

### EDS Formsのデータの形式設定

POST本文のフォームデータを書式設定する方法はいくつかあります。

* 名前と値のペアの配列：

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

* `x-www-form-urlencoded` 本文 (`content-type` ヘッダーは次のように設定する必要があります： `application/x-www-form-urlencoded`) &#39;firstname=bruce&amp;lastname=banner&amp;email=bruce%40example.com&#39;



