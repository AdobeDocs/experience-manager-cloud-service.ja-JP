---
title: OpenAPI ベースの API
description: OpenAPI ベースの API のAEM as a Cloud Service サポートについて説明します
feature: Developing
role: Admin, Architect, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: e735f7d2a39e3165907969d2e27565639499a636
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 2%

---

# OpenAPI ベースの API {#openapi-based-apis}

>[!NOTE]
>
>OpenAPI は、早期アクセスプログラムの一部として利用できます。 これらにアクセスすることに関心がある場合は、ユースケースの説明を記載した電子メール ](mailto:aem-apis@adobe.com)0}aem-apis@adobe.com} を送信することをお勧めします。[

新しいAEM as a Cloud Service API は OpenAPI 仕様に従っているので、一貫性があり、適切にドキュメント化され、使いやすい API を作成します。 詳しくは、次のページを参照してください。

* サーバー間認証を使用して OpenAPI ベースのAEM API を設定および呼び出す方法について説明する [ エンドツーエンドのチュートリアル ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) です。
* [API の概念と構文 ](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/) を含む、情報提供のための [ ガイド ](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/)。
* API エンドポイント [ リファレンスドキュメント ](https://developer.adobe.com/experience-cloud/experience-manager-apis/)。API の一部は OpenAPI ベースです（例：[this Sites API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)。 リファレンスドキュメントには、Adobe Developer Consoleで生成されたベアラートークンを使用してエンドポイントを簡単に試すことができる API プレイグラウンドも含まれています。

一般的な API のユースケースは、CRM や PIM などのシステムとの統合に関連しています。AEM API を呼び出してデータを取得または保持します。 統合実装の一環として、アプリケーションは [AEMが発行するイベント ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-eventing/overview) をサブスクライブできます。これにより、Adobe App Builderまたは他のインフラストラクチャのビジネスロジックをトリガーにすることができます。

サポートされている API 認証タイプはエンドポイントによって異なりますが、OAuth サーバー間、OAuth Web アプリ、OAuth 単一ページアプリ（SPA）の場合があります。

>[!NOTE]
>
> [ エンドツーエンドのチュートリアル ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) は、OpenAPI ベースのAEM API を設定して呼び出す方法を学ぶための推奨リソースです。


## API アクセスの設定 {#configuring-api-access}

多くの OpenAPI ベースのAEM API には認証が必要で、[Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/) を使用して資格情報を生成する必要があります。 設定には次の手順が含まれます。

1. AEM プログラムの [ 製品プロファイルが更新され ](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles) 目的の API にアクセスするための適切なサービスが有効になっていることを確認します。
1. Adobe Developer Consoleで新しいプロジェクトを作成し、目的の API をプロジェクトに追加して、適切な認証タイプを選択します。
1. 資格情報を生成します。これは、後で API の呼び出し時にベアラートークンと交換するために使用されます。
1. 設定パイプライン（または RDE のコマンドライン）を使用してデプロイされた YAML ファイルを設定して、クライアント ID を環境に登録します。

詳細な手順については、[OpenAPI ベースの API の設定チュートリアル ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/setup) を参照してください。

## クライアント ID の登録 {#registering-a-client-id}

クライアント ID では、Adobe Developer Console プロジェクト内のアプリを特定のAEM環境に対してスコープ化します。 これを行うには、以下の手順を実行します。

1. `api.yaml` または同様の名前を持つファイルを、以下のスニペットのような設定（目的の層（オーサー、パブリッシュ、プレビュー）を含む）で作成します。 値 `Client_id`、Adobe Developer Console API プロジェクトから取得する必要があります。

   `kind`、`version`、`metadata` のプロパティについては、[ 設定パイプライン ](/help/operations/config-pipeline.md#common-syntax) の記事を参照してください。 `kind` プロパティの値は *API* に設定し、`version` プロパティは *1* に設定する必要があります。

   ```
   kind: "API"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     allowedClientIDs:
       author:
         - "<client_id>"
       publish:
         - "<client_id>"
       preview:
         - "<client_id>"
   ```

1. [ 設定パイプライン ](/help/operations/config-pipeline.md#folder-structure) で説明されているように、ファイルを `config` または類似の名前の最上位フォルダーの下のどこかに配置します。
1. コマンドラインツールを使用する RDE 以外の環境タイプの場合は、設定パイプラインの記事の [ この節 ](/help/operations/config-pipeline.md#creating-and-managing) で参照されているように、Cloud Managerでターゲット設定パイプラインを作成します。 フルスタックパイプラインと web 階層設定パイプラインでは、設定ファイルをデプロイしません。
1. 設定をデプロイします。
