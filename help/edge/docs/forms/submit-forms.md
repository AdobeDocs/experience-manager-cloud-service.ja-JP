---
title: データを受け入れるスプレッドシートの準備
description: スプレッドシートとアダプティブフォームブロックフィールドを使用して、強力なフォームをより迅速に作成します。
feature: Edge Delivery Services
exl-id: 0643aee5-3a7f-449f-b086-ed637ae53b5a
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 100%

---

# データの受け入れを開始するための Google Sheets または Microsoft Excel ファイルの設定


[フォームを作成してプレビュー](/help/edge/docs/forms/create-forms.md)したら、対応するスプレッドシートでデータの受信を開始できるようにします。次の操作を実行できます。

- [スプレッドシートでデータを受け入れるように手動で有効にする](#manually-enable-the-spreadsheet-to-accept-data)
- [スプレッドシートでデータを受け入れるように Admin API を使用して有効にする](#use-admin-apis-to-enable-a-spreadsheet-to-accept-data)

![ドキュメントベースのオーサリングエコシステム](/help/edge/assets/document-based-authoring-workflow-enable-sheet-to-accept-data.png)


<!--

>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

-->

## スプレッドシートでデータを受け入れるように手動で有効にする

スプレッドシートでデータを受け入れるようにするには

1. フォームが含まれているスプレッドシートを開き、新しいシートを追加し、名前を `incoming` に変更します。 例：[お問い合わせ](/help/edge/assets/enquiry.xlsx)フォームの Microsoft Excel ワークブック。

   >[!WARNING]
   >
   > `incoming` シートが存在しない場合、AEM ではスプレッドシートにデータを送信しません。

1. このシートに、「intake_form」という名前のテーブルを挿入します。 フォームフィールド名と一致させるために必要な列の数を選択します。 次に、ツールバーで挿入／表に移動し、「OK」をクリックします。

1. 表の名前を「intake_form」に変更します。 Microsoft Excel で表の名前を変更するには、表を選択し、「表書式」をクリックします。

1. 次に、フォームフィールド名を表ヘッダーとして追加します。 フィールドが完全に同じであることを確認するには、「shared-aem」シートからフィールドをコピー＆ペーストします。「shared-aem」シートで、送信フィールドを除く「Name」列の下にリストされるフォーム ID を選択してコピーします。

1. 「incoming」シートで、形式を選択して貼り付け／行/列の入れ替えを選択して、フィールド ID をこの新しいシートの列ヘッダーとしてコピーします。 データを取得する必要があるフィールドのみを保持し、他のフィールドは無視できます。

   `shared-aem` の `Name` 列の各値は、送信ボタンを除き、`incoming` シートのヘッダーとして機能します。 例えば、「お問い合わせ」フォームのヘッダーを示す次の画像を考慮してみましょう。

   ![お問い合わせフォームのフィールド](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 拡張機能を使用して、フォームの更新をプレビューします。 これで、シートはフォームの送信を受け入れる準備が整いました。

   >[!NOTE]
   >
   >以前にシートをプレビューしたことがある場合でも、`incoming` シートを初めて作成した後に再度プレビューする必要があります。


フィールド名が `incoming` シートに追加されると、フォームは送信を受け入れる準備が整います。 フォームをプレビューし、これを使用してデータをシートに送信できます。

データを受信するようにシートを設定したら、[フォームをプレビュー](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page)<!--or [use POST requests](#use-admin-apis-to-send-data-to-your-sheet)-->してシートへのデータの送信を開始できます。

>[!WARNING]
>
>  「shared-aem」シートには、一般にアクセスされることに抵抗のある個人を特定できる情報や機密データを決して含めないでください。


## スプレッドシートでデータを受け入れるように Admin API を使用して有効にする

また、POST リクエストをフォームに送信して、データを受け入れ、`incoming` シートのヘッダーを設定するように有効にすることもできます。POST リクエストを受信すると、サービスではリクエストの本文を分析し、データの取り込みに必要な必須のヘッダーとシートを自律的に生成します。

スプレッドシートでデータを受け入れるように Admin API を使用して有効にするには：


1. 作成したワークブックを開き、デフォルトのシートの名前を `incoming` に変更します。

   >[!WARNING]
   >
   > `incoming` シートが存在しない場合、AEM ではこのワークブックにデータを送信しません。

1. Sidekick でシートをプレビューします。

   >[!NOTE]
   >
   >以前にシートをプレビューしたことがある場合でも、`incoming` シートを初めて作成した後に再度プレビューする必要があります。

1. POST リクエストを送信して `incoming` シートに適切なヘッダーを生成し、`shared-default` シートがまだ存在しない場合はスプレッドシートに追加します。

   シートを設定する POST リクエストの形式については、[Admin API ドキュメント](https://www.aem.live/docs/admin.html#tag/authentication/operation/profile)を参照してください。以下に例を示します。

   **リクエスト**

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

   以下に示すように、cURL や Postman などのツールを使用して、この POST リクエストを実行できます。

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

   上記の POST リクエストでは、フォームフィールドとそれぞれのサンプル値の両方を含むサンプルデータを提供します。このデータは、フォームを設定するために Admin サービスによって使用されます。

   これで、フォームでデータを受け入れるように有効にしました。また、スプレッドシートに次の変更が見られることもわかります。

## データを受け入れるように有効になると、シートが自動的に変更される。

データを受信するようにシートを設定すると、スプレッドシートに次の変更が見られます。

「Slack」という名前のシートが Excel ワークブックまたは Google Sheets に追加されます。このシートでは、新しいデータがスプレッドシートに取り込まれるたびに、指定した Slack チャネルに対する自動通知を設定できます。現在、AEM では、AEM エンジニアリング Slack 組織とアドビエンタープライズサポート組織への通知のみをサポートします。

1. Slack 通知を設定するには、Slack ワークスペースの「teamId」と、「チャネル名」または「ID」を入力します。また、slack ボットに（debug コマンドを使用して）「teamId」と「チャネル ID」を問い合わせることもできます。チャネル名を変更しても残り続けるので、「チャネル名」の代わりに「チャネル ID」を使用することをお勧めします。

   >[!NOTE]
   >
   > 古いフォームには「teamId」列がありませんでした。「teamId」は「#」または「/」で区切られてチャネル列に含まれていました。

1. 必要なタイトルを入力し、フィールドの下に Slack 通知に表示するフィールドの名前を入力します。各見出しはコンマで区切る必要があります（名前、メールなど）。

   >[!WARNING]
   >
   >  「shared-default」シートには、一般にアクセスされることに抵抗のある個人を特定できる情報や機密データを決して含めないでください。



次に、[「ありがとうございます」メッセージをカスタマイズ](/help/edge/docs/forms/thank-you-page-form.md)できます。

