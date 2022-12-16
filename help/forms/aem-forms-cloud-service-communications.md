---
title: AEM Forms as a Cloud Service - 通信
description: データを XDP および PDF テンプレートと自動的に結合するか、出力を PCL、ZPL および PostScript 形式で生成します
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 20e54ff697c0dc7ab9faa504d9f9e0e6ee585464
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 50%

---


# 同期処理を使用 {#sync-processing-introduction}

Formsas a Cloud Service — コミュニケーション API を使用すると、ビジネス通信、ドキュメント、声明、請求処理レター、給付通知、請求処理レター、月次請求、ウェルカムキットなど、ブランド指向でパーソナライズされたコミュニケーションを作成、組み立て、提供できます。 通信 API を使用して、テンプレート（XFA または PDF）と顧客データを組み合わせ、PDF、PS、PCL、DPL、IPL、ZPL 形式のドキュメントを生成できます。

例えば、1 つ以上のテンプレートが存在しており、各テンプレートには XML データの複数のレコードがあるシナリオを考えてみましょう。通信 API を使用して、各レコードの印刷用ドキュメントを生成できます。<!-- You can also combine the records into a single document. -->結果は非インタラクティブ PDF ドキュメントになります。非インタラクティブ PDF ドキュメントのフィールドには、ユーザーがデータを入力することはできません。

Formsas a Cloud Service — コミュニケーションは、スケジュールに沿ったドキュメント生成用のオンデマンド API とバッチ API（非同期 API）を提供します。

* 同期 API は、オンデマンド、低遅延および単一レコードドキュメントを生成するユースケースに適しています。これらの API は、ユーザーアクションに基づいたユースケースにより適しています。例えば、ユーザーがフォームに入力した後にドキュメントを生成する場合などです。

* バッチ API（非同期 API）は、スケジュールに沿った高スループットの複数ドキュメント生成のユースケースに適しています。これらの API は、バッチでドキュメントを生成します。例えば、毎月生成される電話料金、クレジットカード明細、給付計算書などです。

## 同期操作を使用 {#batch-operations}

同期操作とは、ドキュメントを線形的に生成するプロセスです。これらの API は、シングルテナント API とマルチテナント API に分類されます。

### シングルテナント API

* ドキュメント生成 API
* ドキュメント操作 API

### マルチテナント API

* ドキュメントユーティリティ API

### シングルテナント API の認証

シングルテナント API 操作は、次の 2 種類の認証をサポートします。

* **基本認証**：基本認証は、HTTP プロトコルに組み込まれたシンプルな認証スキームです。クライアントは、Basic という単語に続いてスペースと、base64 でエンコードされた文字列 username:password を含む Authorization ヘッダーを含む HTTP リクエストを送信します。例えば、管理者／管理者として認証するために、クライアントは Basic [base64 エンコードされたユーザー名文字列]: [base64 でエンコードされたパスワード文字列]を送信します。

* **トークンベースの認証：**&#x200B;トークンベースの認証では、アクセストークン（Bearer 認証トークン）を使用して、Experience Manager as a Cloud Service にリクエストを送信します。AEM Forms as a Cloud Service は、アクセストークンを安全に取得する API を提供します。トークンを取得して使用し、要求を認証するには、次の手順を実行します。

   1. [開発者コンソールからExperience Managerのas a Cloud Serviceの資格情報を取得します。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja).
   1. [環境にExperience Manageras a Cloud Serviceの資格情報をインストールする](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja). Cloud Service にリクエストを送信する（呼び出しを行う）ように設定された（AEM Server、web サーバーまたはその他の非アプリケーションサーバー）。
   1. [JWT トークンを生成し、アクセストークン用の Adobe IMSAPI と交換します](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja)。
   1. アクセストークンを Bearer 認証トークンとして使用して Experience Manager API を実行します。
   1. [Experience Manager 環境のテクニカルアカウントユーザーに適切な権限を設定します](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja#aemでのアクセスの設定)。

   >[!NOTE]
   >
   >アドビでは、実稼動環境でトークンベースの認証を使用することをお勧めします。

### マルチテナント API の認証

#### 認証ヘッダー

Cloud Manager API への受信 HTTP API 呼び出しには、次の 3 つのヘッダーを含める必要があります。

* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

送信する値 `x-api-key` および `x-gw-ims-org-id` ヘッダーは、 [Adobe Developer Console](https://developer.adobe.com/console). の値 `x-api-key` header はクライアント ID で、 `x-gw-ims-org-id` header は組織 ID です。

#### Adobe Developerコンソールを設定してアクセストークンを生成する

認証 API を設定するには、Adobe Developerコンソールでプロジェクトを作成し、Adobe Developerコンソールのプロジェクトに通信 API を追加します。 この統合環境により、API キー、クライアント秘密鍵、ペイロード (JWT) が生成されます。

1. Adobe Developer Console 管理者にお問い合わせください。 管理者に、開発者としてを追加するよう依頼します。
1. `https://developer.adobe.com/console/` にログインします。管理者がプロビジョニングした開発者アカウントを使用して、Adobe Developer Console にログインします。
1. 右上隅で組織を選択します。自分がどの組織に属しているかわからない場合は、管理者に問い合わせてください。
1. 「**[!UICONTROL 新規プロジェクトを作成]**」をタップします。新規プロジェクトを作成する画面が表示されます。「**[!UICONTROL API を追加]**」をタップします。お使いのアカウントで有効になっているすべての API を示す画面が表示されます。
1. 選択 **[!UICONTROL AEM Forms — コミュニケーション]** とタップします。 **[!UICONTROL 次へ]**. API を設定する画面が表示されます。
1. 選択 **[!UICONTROL オプション 1 キーペアを生成する]** とタップします。 **[!UICONTROL キーペアを生成]**. 設定ファイルが作成され、ダウンロードされます。 ダウンロードした設定ファイルには、すべてのアプリ設定と、秘密鍵のコピーのみが含まれています。 Adobeは秘密鍵を記録しません。ダウンロードしたファイルを安全に保存してください。 「**[!UICONTROL 次へ]**」をタップします。
1. 選択 **[!UICONTROL 統合 —Cloud Service]** とタップします。 **[!UICONTROL 設定済み API を保存]**. タップ **[!UICONTROL サービスアカウント (JWT)]** をクリックして、API キー、クライアント秘密鍵、および API へのアクセスに必要なその他の情報を表示します。 トークンを使用して API にアクセスするように設定します。

#### プログラムによるアクセストークンの生成と使用

プログラムによってアクセストークンを生成するには、JSON Web トークン (JWT) を生成し、AdobeのIdentity Managementサービス (IMS) とアクセストークンと交換します。

JWT JSON オブジェクトを構築するには、次のキー（claims と呼ばれます）を使用します。

* `exp` — アクセストークンの要求された有効期限（1970 年 1 月 1 日 GMT からの秒数） ほとんどの使用例では、これは比較的小さい値です。 例えば、5 分（今から 5 分）の場合、この値は1670923791にする必要があります。
* `iss` - Adobe Developer Console プロジェクトの組織 ID( org_ident@AdobeOrgの形式 )。
* `sub` - Adobe Developerコンソール統合からのテクニカルアカウント ID。次の形式で指定します。id@techacct.adobe.com.
* `aud` - Adobe Developerコンソール統合のクライアント ID の前に、 `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing`  — リテラル値に設定 `true`

次に、この JSON オブジェクトは、プロジェクトの秘密鍵を使用して base64 エンコードし、署名する必要があります。 最後に、エンコードされた値がPOSTリクエストの本文でに送信され、 `https://ims-na1.adobelogin.com/ims/exchange/jwt` と共に、プロジェクトのクライアント ID およびクライアント秘密鍵も表示されます。

##### 例

```JSON
    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache
```

#### JWT の言語サポート

カスタムコードでは JWT の生成と交換のプロセス全体を実行できますが、それにはより高レベルのライブラリを使用する方が一般的です。 このようなライブラリの多くは、 [Adobe I/OJWT ドキュメント](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

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

API から提供されるすべてのパラメーター、認証方法および各種サービスの詳細については、[API リファレンスドキュメント](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)を参照してください。API リファレンスドキュメントでは、API 定義ファイルの.yaml 形式も提供しています。 .yaml ファイルをダウンロードし、次の場所にアップロードできます。 [Postman](https://www.postman.com/) をクリックして、API の機能を確認します。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>通信 API にアクセスできるのは、forms-users グループのメンバーだけです。
