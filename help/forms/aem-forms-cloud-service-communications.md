---
title: AEM Forms as a Cloud Service - 通信
description: データを XDP および PDF テンプレートと自動的に結合するか、出力を PCL、ZPL および PostScript 形式で生成します
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: fdbb927dbd7f6d640100d444431f931d95414ebc
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 39%

---


# 同期処理を使用 {#sync-processing-introduction}

コミュニケーション機能により、ブランド承認、パーソナライズ、標準化されたドキュメント（ビジネス通信、明細書、請求処理レター、特典通知、月々の請求、ウェルカムキットなど）を作成できます。

この機能は、ドキュメントを生成および操作するための API を提供します。 ドキュメントをオンデマンドで生成または操作したり、バッチジョブを作成して、定義した間隔で複数のドキュメントを生成することができます。

通信サービスは、オンデマンドおよびスケジュールされたドキュメント生成用に API を提供します。オンデマンドに同期 API を、スケジュールされたドキュメント生成にバッチ API（非同期 API）を使用できます。

* 同期 API は、オンデマンド、低遅延および単一レコードドキュメントを生成するユースケースに適しています。これらの API は、ユーザーアクションに基づいたユースケースにより適しています。例えば、ユーザーがフォームに入力した後にドキュメントを生成する場合などです。

* バッチ API（非同期 API）は、スケジュールに沿った高スループットの複数ドキュメント生成のユースケースに適しています。これらの API は、バッチでドキュメントを生成します。例えば、毎月生成される電話料金、クレジットカード明細、給付計算書などです。

## 同期操作を使用 {#batch-operations}

同期操作とは、ドキュメントを線形的に生成または操作するプロセスです。 次の 2 種類の認証をサポートしています。

* **基本認証**:基本認証は、HTTP プロトコルに組み込まれたシンプルな認証スキームです。 クライアントは、Basic という単語に続いてスペースと、base64 でエンコードされた文字列 username:password を含む Authorization ヘッダーを含む HTTP リクエストを送信します。 例えば、管理者/管理者として認証するために、クライアントが基本を送信する [base64 エンコードされた文字列ユーザー名]: [base64 でエンコードされた文字列パスワード].

* **トークンベースの認証：** トークンベースの認証では、アクセストークン（Bearer 認証トークン）を使用して、as a Cloud ServiceのExperience Managerにリクエストを送信します。 AEM Forms as a Cloud Serviceは、アクセストークンを安全に取得する API を提供します。 トークンを取得して使用し、要求を認証するには、次の手順を実行します。

   1. [開発者コンソールからExperience Managerのas a Cloud Serviceの資格情報を取得します。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [環境にExperience Manageras a Cloud Serviceの資格情報をインストールする](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). クラウドサービスにリクエストを送信（呼び出しをおこなう）ように設定された (AEM Server、Web サーバーまたはその他の非アプリケーションサーバー )。
   1. [JWT トークンを生成し、アクセストークン用のAdobe IMSAPI と交換しました](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. アクセストークンを BearerExperience Managerトークンとして使用して認証 API を実行します。
   1. [テクニカルアカウントユーザーに対して、Experience Manager環境で適切な権限を設定する](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

   >[!NOTE]
   >
   >Adobeでは、実稼動環境でトークンベースの認証を使用することをお勧めします。

### （ドキュメント生成 API のみ）前提条件 {#pre-requisites}

ドキュメント生成に同期 API を使用するには、次の操作が必要です。

* PDF または XDP テンプレート
* [テンプレートと結合するデータ](#form-data)
* Experience Manager 管理者権限を持つユーザー
* テンプレートおよびその他のアセットの Experience Manager Forms Cloud Service インスタンスへのアップロード

#### テンプレートおよびその他のアセットの Experience Manager インスタンスへのアップロード

通常、組織には複数のテンプレートがあります。例えば、クレジットカード明細、福利厚生明細、請求申込用にそれぞれ 1 つずつテンプレートがあります。このような XDP および PDF テンプレートをすべて Experience Manager インスタンスにアップロードします。テンプレートをアップロードするには：

1. Experience Manager インスタンスを開きます。
1. フォーム／フォームとドキュメントに移動します。
1. 作成／フォルダーをクリックし、フォルダーを作成します。フォルダーを開きます。
1. 作成／ファイルをアップロードをクリックし、テンプレートをアップロードします。

### 同期 API を使用したドキュメントの生成

別の API を使用できるようになりました。

* テンプレートからPDFドキュメントを生成し、そのドキュメントにデータを結合します。
* XDP ファイルまたはPDFドキュメントから PostScript(PS)、Printer Command Language(PCL)、Zebra Printing Language(ZPL) ドキュメントを生成します。

API から提供されるすべてのパラメーター、認証方法および各種サービスの詳細については、[API リファレンスドキュメント](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/Communications-Services)を参照してください。API リファレンスドキュメントは、.yaml 形式でも入手できます。の.yaml をダウンロードできます。 [同期 API](assets/sync.yaml) API の機能を確認するには、postman にアップロードします。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>通信 API にアクセスできるのは、forms-users グループのメンバーだけです。
