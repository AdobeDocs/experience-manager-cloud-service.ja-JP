---
title: AEM Forms as a Cloud Service - 通信
description: データを XDP および PDF テンプレートと自動的に結合するか、出力を PCL、ZPL および PostScript 形式で生成します
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 07b9118b8cfc27bc9e2bfa134fbb57c7ae2728ad
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 99%

---


# 同期処理を使用 {#sync-processing-introduction}

通信サービスでは、ビジネス通信、ドキュメント、声明書、請求処理レター、給付通知、請求処理レター、月次請求書、ウェルカムキットなど、ブランド志向でパーソナライズされたコミュニケーションを作成、組み立て、提供できます。通信 API を使用して、テンプレート（XFA または PDF）と顧客データを組み合わせ、PDF、PS、PCL、DPL、IPL、ZPL 形式のドキュメントを生成できます。

例えば、1 つ以上のテンプレートが存在しており、各テンプレートには XML データの複数のレコードがあるシナリオを考えてみましょう。通信 API を使用して、各レコードの印刷用ドキュメントを生成できます。<!-- You can also combine the records into a single document. -->結果は非インタラクティブ PDF ドキュメントになります。非インタラクティブ PDF ドキュメントのフィールドには、ユーザーがデータを入力することはできません。


通信サービスは、オンデマンドおよびスケジュールされたドキュメント生成用に API を提供します。オンデマンドに同期 API を、スケジュールされたドキュメント生成にバッチ API（非同期 API）を使用できます。

* 同期 API は、オンデマンド、低遅延および単一レコードドキュメントを生成するユースケースに適しています。これらの API は、ユーザーアクションに基づいたユースケースにより適しています。例えば、ユーザーがフォームに入力した後にドキュメントを生成する場合などです。

* バッチ API（非同期 API）は、スケジュールに沿った高スループットの複数ドキュメント生成のユースケースに適しています。これらの API は、バッチでドキュメントを生成します。例えば、毎月生成される電話料金、クレジットカード明細、給付計算書などです。

## 同期操作を使用 {#batch-operations}

同期操作とは、ドキュメントを線形的に生成するプロセスです。別個の API は次の場合に使用可能です。

* テンプレートから PDF ドキュメントを生成し、そのドキュメントにデータを結合する。
* XDP ファイルまたは PDF ドキュメントから PostScript（PS）、Printer Command Language（PCL）、Zebra Printing Language（ZPL）ドキュメントを生成する。
* PDF ドキュメントのアセンブリ
* PDF ドキュメントのディスアセンブリ
* ドキュメントから PDF/A 準拠ドキュメントへの変換
* PDF/A 準拠ドキュメントの検証


### API 呼び出しの認証

同期操作では、次の 2 種類の認証をサポートしています。

* **基本認証**：基本認証は、HTTP プロトコルに組み込まれたシンプルな認証スキームです。クライアントは、Basic という単語に続いてスペースと、base64 でエンコードされた文字列 username:password を含む Authorization ヘッダーを含む HTTP リクエストを送信します。例えば、管理者／管理者として認証するために、クライアントは Basic [base64 エンコードされたユーザー名文字列]: [base64 でエンコードされたパスワード文字列]を送信します。

* **トークンベースの認証：**&#x200B;トークンベースの認証では、アクセストークン（Bearer 認証トークン）を使用して、Experience Manager as a Cloud Service にリクエストを送信します。AEM Forms as a Cloud Service は、アクセストークンを安全に取得する API を提供します。トークンを取得して使用し、要求を認証するには、次の手順を実行します。

   1. [Developer Console から Experience Manager as a Cloud Service の資格情報を取得します](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja)。
   1. [環境に Experience Manager as a Cloud Service の資格情報をインストールします](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html)。Cloud Service にリクエストを送信する（呼び出しを行う）ように設定された（AEM Server、web サーバーまたはその他の非アプリケーションサーバー）。
   1. [JWT トークンを生成し、アクセストークン用の Adobe IMSAPI と交換します](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html)。
   1. アクセストークンを Bearer 認証トークンとして使用して Experience Manager API を実行します。
   1. [Experience Manager 環境のテクニカルアカウントユーザーに適切な権限を設定します](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=ja#aemでのアクセスの設定)。

   >[!NOTE]
   >
   >アドビでは、実稼動環境でトークンベースの認証を使用することをお勧めします。


### （ドキュメント生成 API の場合のみ）アセットと権限の設定

API を使用するために必要なものは、次のとおりです。

* PDF または XDP テンプレート
* [テンプレートと結合するデータ](#form-data)
* Experience Manager 管理者権限を持つユーザー
* テンプレートおよびその他のアセットの Experience Manager Forms Cloud Service インスタンスへのアップロード

### （ドキュメント生成 API の場合のみ）Experience Manager インスタンスへのテンプレートおよび他のアセットのアップロード

通常、組織には複数のテンプレートがあります。例えば、クレジットカード明細、福利厚生明細、請求申込用にそれぞれ 1 つずつテンプレートがあります。このような XDP および PDF テンプレートをすべて Experience Manager インスタンスにアップロードします。テンプレートをアップロードするには：

1. Experience Manager インスタンスを開きます。
1. フォーム／フォームとドキュメントに移動します。
1. 作成／フォルダーをクリックし、フォルダーを作成します。フォルダーを開きます。
1. 作成／ファイルをアップロードをクリックし、テンプレートをアップロードします。


### API の呼び出し

API から提供されるすべてのパラメーター、認証方法および各種サービスの詳細については、[API リファレンスドキュメント](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)を参照してください。また、API リファレンスドキュメントでは、API 定義ファイルを .yaml 形式で提供しています。.yaml ファイルをダウンロードし、postman にアップロードして API の機能を確認できます。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>通信 API にアクセスできるのは、forms-users グループのメンバーだけです。
