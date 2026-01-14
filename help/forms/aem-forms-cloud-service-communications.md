---
title: Forms as a Cloud Service を使用して、XDP や PDF のテンプレートとデータを結合したり、PCL、ZPL および PostScript 形式で出力を生成したりする方法
description: データを XDP および PDF テンプレートと自動的に結合するか、出力を PCL、ZPL および PostScript 形式で生成します
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
feature: Adaptive Forms,APIs & Integrations
role: Admin, Developer, User
source-git-commit: 43b648eb3984867fda35ee04de10b78dd836b481
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 91%

---


# 同期処理を使用 {#sync-processing-introduction}

Forms as a Cloud Service - 通信 API では、ビジネスコミュニケーション、ドキュメント、声明書、請求処理レター、給付通知、請求処理レター、月次請求書、ウェルカムキットなど、ブランド志向でパーソナライズされたコミュニケーションを作成、アセンブリ、配信できます。コミュニケーション API を使用して、テンプレート（XFA または PDF）と顧客データを組み合わせ、PDF、PS、PCL、DPL、IPL、ZPL 形式のドキュメントを生成できます。

例えば、1 つ以上のテンプレートが存在しており、各テンプレートには XML データの複数のレコードがあるシナリオを考えてみましょう。通信 API を使用して、各レコードの印刷用ドキュメントを生成できます。<!-- You can also combine the records into a single document. -->結果は非インタラクティブ PDF ドキュメントになります。非インタラクティブ PDF ドキュメントのフィールドには、ユーザーがデータを入力することはできません。

Formsas a Cloud Service - コミュニケーションは、スケジュールされたドキュメント生成にオンデマンドおよびバッチ API（非同期 API）を提供します。

* 同期 API は、オンデマンド、低遅延および単一レコードドキュメントを生成するユースケースに適しています。これらの API は、ユーザーアクションに基づいたユースケースにより適しています。例えば、ユーザーがフォームに入力した後にドキュメントを生成する場合などです。

* バッチ API（非同期 API）は、スケジュールに沿った高スループットの複数ドキュメント生成のユースケースに適しています。これらの API は、バッチでドキュメントを生成します。例えば、毎月生成される電話料金、クレジットカード明細、給付計算書などです。

## 同期操作を使用 {#batch-operations}

同期操作とは、ドキュメントを線形的に生成するプロセスです。これらの API は、シングルテナント API とマルチテナント API に分類されます。

### シングルテナント API

* ドキュメント生成 API
* ドキュメント操作 API

<!-- 
### Multi-tenant APIs

* Document utility APIs -->


### シングルテナント API の認証

シングルテナント API 操作は、次の 2 種類の認証をサポートしています。

* **基本認証**：基本認証は、HTTP プロトコルに組み込まれたシンプルな認証スキームです。クライアントは、Basic という単語に続いてスペースと、base64 でエンコードされた文字列 username:password を含む Authorization ヘッダーを含む HTTP リクエストを送信します。 例えば、管理者／管理者として認証するために、クライアントは Basic [base64 エンコードされたユーザー名文字列]: [base64 でエンコードされたパスワード文字列]を送信します。

* **トークンベースの認証：**&#x200B;トークンベースの認証では、アクセストークン（Bearer 認証トークン）を使用して、Experience Manager as a Cloud Service にリクエストを送信します。AEM Forms as a Cloud Service は、アクセストークンを安全に取得する API を提供します。トークンを取得して使用し、要求を認証するには、次の手順を実行します。

   1. [Developer Console から Experience Manager as a Cloud Service の資格情報を取得する](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja)。
   1. [環境に Experience Manager as a Cloud Service の資格情報をインストールする](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja)。Cloud Service にリクエストを送信する（呼び出しを行う）ように設定された（AEM Server、web サーバーまたはその他の非アプリケーションサーバー）。
   1. [JWT トークンを生成し、アクセストークン用の Adobe IMSAPI と交換します](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja)。
   1. アクセストークンを Bearer 認証トークンとして使用して Experience Manager API を実行します。
   1. [Experience Manager 環境のテクニカルアカウントユーザーに適切な権限を設定します](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja#aemでのアクセスの設定)。

  >[!NOTE]
  >
  >アドビでは、本番環境でトークンベースの認証を使用することをお勧めします。

  >[!IMPORTANT]
  >
  > 詳しくは、[OAuth サーバー間認証 &#x200B;](/help/forms/oauth-api-authetication.md) および [JWT サーバー間認証 &#x200B;](/help/forms/jwt-api-authentication.md) を参照してください。
<!-- 

### Authenticate a multi-tenant API

#### Authentication Headers

Every inbound HTTP API call to the multi-tenant API must contain these three headers:


* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

The values which should be sent in the `x-api-key` and `x-gw-ims-org-id` headers are provided in the Credentials details screen in the [Adobe Developer Console](https://developer.adobe.com/console). The value of the `x-api-key` header is the Client ID and the value for the `x-gw-ims-org-id` header is the Organization ID.

#### Configure Adobe Developer console to generate an access token

To set up authentication APIs, create a project in Adobe Developer Console and add Communication APIs to the project on Adobe Developer Console. The integration generates API Key, Client Secret, Payload (JWT):

1. Contact you Adobe Developer Console administrator. Ask the administrator to add as a developer.
1. Log in to `https://developer.adobe.com/console/`. Use your developer account that your administrator has provisioned to log in to Adobe Developer Console.
1. Select your organization from the top-right corner. If you do not know your organization, contact your administrator.
1. Select **[!UICONTROL Create new project]**. A screen to get started with your new project appears. Select **[!UICONTROL Add API]**. A screen with list of all the APIs enabled for your account appears.
1. Select **[!UICONTROL AEM Forms - Communications]** and select **[!UICONTROL Next]**. A screen to configure the API appears.
1. Select **[!UICONTROL OPTION 1 Generate a key pair]** and select **[!UICONTROL Generate keypair]**. It creates and downloads the configuration file. The downloaded configuration file contains all your app settings, along with the only copy of your private key. Adobe does not record your private key, make sure to securely store the downloaded file. Select **[!UICONTROL Next]**.
1. Select **[!UICONTROL Integrations - Cloud Service]** and select **[!UICONTROL Save configured API]**. Select **[!UICONTROL Service Account (JWT)]** to view the API Key, Client Secret, and other information required to access the APIs. You set to use the token to access the APIs.

#### Programmatically generate and use an access token

To programmatically generate an access token, generate a JSON Web Token (JWT) and exchange it with the Adobe Identity Management Service (IMS) for an access token.

Use the following keys, referred to as claims, to construct JWT JSON object:


* `exp`- the requested expiration of the access token, expressed as several seconds since January 1, 1970 GMT. For most use cases, this is a relatively small value. For example, 5 minutes, for five minutes from now, this value should be 1670923791.
* `iss` - the Organization ID from the Adobe Developer Console project, in the format org_ident@AdobeOrg.
* `sub` - the Technical Account ID from the Adobe Developer Console integration, in the format: id@techacct.adobe.com.
* `aud` - the Client ID from the Adobe Developer Console integration prepended with `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing` - set to the literal value `true`

This JSON object must be then base64 encoded and signed using the private key for the project. Finally, the encoded value is sent in the body of a POST request to `https://ims-na1.adobelogin.com/ims/exchange/jwt` along with the Client ID and Client Secret for the project.

##### Example

```JSON

    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache

```

#### Language Support for JWT

While it is possible to do the entire JWT generation and exchange process in custom code, it is more common to use a higher-level library to do so. A number of such libraries are listed on the [Adobe I/O JWT Documentation](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

-->

### （ドキュメント生成 API の場合のみ）アセットと権限の設定

API を使用するために必要なものは、次のとおりです。

* Experience Manager 管理者権限を持つユーザー
* テンプレートおよびその他のアセットの Experience Manager Forms Cloud Service インスタンスへのアップロード

### （ドキュメント生成 API の場合のみ）Experience Manager インスタンスへのテンプレートおよび他のアセットのアップロード

通常、組織には複数のテンプレートがあります。例えば、クレジットカード明細、福利厚生明細、請求申込用にそれぞれ 1 つずつテンプレートがあります。このような XDP および PDF テンプレートをすべて Experience Manager インスタンスにアップロードします。テンプレートをアップロードするには：

1. Experience Manager インスタンスを開きます。
1. フォーム／フォームとドキュメントに移動します。
1. 作成／フォルダーをクリックし、フォルダーを作成します。フォルダーを開きます。
1. 作成／ファイルをアップロードをクリックし、テンプレートをアップロードします。

### API の呼び出し

API から提供されるすべてのパラメーター、認証方法および各種サービスの詳細については、[API リファレンスドキュメント](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)を参照してください。また、API リファレンスドキュメントでは、API 定義ファイルを .yaml 形式で提供しています。.yaml ファイルをダウンロードし、[Postman](https://www.postman.com/) にアップロードして API の機能を確認できます。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
> AEM Forms Communication API を呼び出す詳細な手順については、[OAuth サーバー間認証を使用したAEM Forms Communications API の呼び出し &#x200B;](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md) を参照してください。

>[!MORELIKETHIS]
>
>* [AEM Forms as a Cloud Service の概要](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [アダプティブフォームおよび通信 API 用のAEM Forms as a Cloud Service アーキテクチャ](/help/forms/aem-forms-cloud-service-architecture.md)
>* [通信処理 - 同期 API](/help/forms/aem-forms-cloud-service-communications.md)
>* [通信処理 - バッチ API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [Forms Communications API - チュートリアル &#x200B;](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)