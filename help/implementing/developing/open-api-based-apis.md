---
title: OpenAPI ベースの API
description: OpenAPI ベースの API のAEM as a Cloud Service サポートについて説明します
feature: Developing
role: Admin, Architect, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: 320fe55d652b94cd63dfe82d4165c1f957653a63
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 1%

---

# OpenAPI ベースの API {#openapi-based-apis}

新しいAEM as a Cloud Service API は OpenAPI 仕様に従っているので、一貫性があり、十分にドキュメント化されている API のセットを提供します。

>[!NOTE]
>
> [ エンドツーエンドのチュートリアル ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) は、OpenAPI ベースのAEM API を設定して呼び出す方法を学ぶための推奨リソースです。

認証が必要なエンドポイントの場合、認証アプローチはエンドポイントによって異なりますが、OAuth サーバー間、OAuth Web アプリ、OAuth 単一ページアプリ（SPA）のいずれかを使用する場合があります。 資格情報は、[Adobe Developer Console](https://developer.adobe.com/developer-console/) のプロジェクトを通じて設定されます。

一般的な API のユースケースは、CRM や PIM などのシステムとの統合です。AEM API を呼び出してデータを取得または保持します。 統合実装の一環として、アプリケーションは [AEMが発行するイベント ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-eventing/overview) をサブスクライブできます。これにより、Adobe App Builderまたは他のインフラストラクチャのビジネスロジックをトリガーにすることができます。

このドキュメントは概要として機能しますが、より詳細なドキュメントは次のページで入手できます。

* [ リファレンスドキュメント ](https://developer.adobe.com/experience-cloud/experience-manager-apis/) の OpenAPI ベースの API の節からのリンク。 各 API のリファレンスドキュメントには、API プレイグラウンドも含まれています。これにより、Adobe Developer Consoleで生成されたベアラートークンを使用してエンドポイントを簡単に試すことができます。

* [API の概念と構文 ](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/) を含む、情報提供のための [ ガイド ](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/)。

* [ 認証アプローチ ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/overview#authentication-support) やその他の概念について説明する最上位のチュートリアル。

* [OpenAPI ベースの API の設定方法 ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup) に重点を置いたビデオを含むチュートリアルです。

* サーバー間認証戦略を使用した OpenAPI の設定と呼び出しについて [ エンドツーエンドのチュートリアル ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) を参照してください。 Web アプリとシングルページアプリケーションの認証アプローチについても、同様のチュートリアルが見つかります。

## API アクセスの設定 {#configuring-api-access}

一部の OpenAPI ベースのAEM API には認証が必要で、[Adobe Developer Console](https://developer.adobe.com/developer-console/) を使用して資格情報を生成する必要があります。 設定には次の手順が含まれます。

1. AEM as a Cloud Service環境の最新化。 詳しくは、チュートリアルの手順の [AEM as a Cloud Service環境の最新化 ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup?#modernization-of-aem-as-a-cloud-service-environment) を参照してください。
1. 製品プロファイルを使用してAEM API へのアクセスを有効にします。 製品プロファイルは、事前定義されたアクセス制御リスト（ACL）を持つAEM ユーザーグループを表すサービスに関連付けられています。 デフォルトでは一部のサービスは特定の製品プロファイルに関連付けられますが、明示的に関連付ける必要があるサービスもあります。例えば、AEM Assets API Users Service は [ 製品プロファイル ](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles) に関連付けられていないので、AEM Assets API を使用するには有効にする必要があります。 詳しくは、チュートリアルの手順の [AEM API アクセスの有効化 ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access) を参照してください。
1. サーバー間認証を追加するには、integration を設定するユーザーが組織のAdobe Admin Console管理者であるか、サービスが関連付けられている製品プロファイルに開発者として追加されている必要があります。 詳しくは、チュートリアルの手順の [AEM API アクセスの有効化 ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access) を参照してください。
1. Adobe Developer Console（ADC）プロジェクトを作成します。
1. ADC プロジェクトの設定 これにより、API の呼び出し時にベアラートークンと交換するために後で使用される資格情報が生成されます。
1. AEM インスタンスを設定して、ADC プロジェクト通信を有効にします。 これには、以下の [ クライアント ID の登録 ](#registering-a-client-id) の節で説明されているように、YAML ファイルを設定してデプロイすることでクライアント ID を環境に登録することが含まれます。

詳細な手順については、[OpenAPI ベースの API の設定チュートリアル ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup) を参照してください。

### クライアント ID の登録 {#registering-a-client-id}

クライアント ID によって、Adobe Developer Console プロジェクトの API が特定のAEM環境に対応するようになります。 これを行うには、以下の手順を実行します。

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

1. `config` 設定パイプライン [ で説明されているように、ファイルを ](/help/operations/config-pipeline.md#folder-structure) または類似の名前の最上位フォルダーの下のどこかに配置します。
1. コマンドラインツールを使用する RDE 以外の環境タイプの場合は、設定パイプラインの記事の [ この節 ](/help/operations/config-pipeline.md#creating-and-managing) で参照されているように、Cloud Managerでターゲット設定パイプラインを作成します。 フルスタックパイプラインと web 階層設定パイプラインでは、設定ファイルをデプロイしません。
1. 設定をデプロイします。
