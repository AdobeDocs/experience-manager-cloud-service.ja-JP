---
title: OpenAPI ベースの API
description: OpenAPI ベースの API のAEM as a Cloud Service サポートについて説明します
feature: Developing
role: Admin, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 100%

---

# OpenAPI ベースの API {#openapi-based-apis}

新しいAEM as a Cloud Service API は OpenAPI 仕様に準拠しており、一貫性があり、十分にドキュメント化されている API のセットを提供します。

>[!NOTE]
>
> [ エンドツーエンドのチュートリアル ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s) は、OpenAPI ベースのAEM API を設定して呼び出す方法を学ぶための推奨リソースです。

認証が必要なエンドポイントの場合、認証アプローチはエンドポイントによって異なりますが、OAuth サーバー間、OAuth Web アプリ、OAuth 単一ページアプリ（SPA）のいずれかを使用する場合があります。 資格情報は、[Adobe Developer Console](https://developer.adobe.com/developer-console/) のプロジェクトを通じて設定されます。

一般的な API の利用ケースには、CRM や PIM などのシステムとの統合が含まれ、AEM API を呼び出してデータを取得または保存します。統合実装の一環として、アプリケーションは [AEM が発行するイベント](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-eventing/overview)をサブスクライブできます。これにより、Adobe App Builder または他のインフラストラクチャでビジネスロジックをトリガーできます。

このドキュメントは概要として機能しますが、より詳細なドキュメントは次のページで入手できます。

* [リファレンスドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/)の「OpenAPI ベースの API」セクションからのリンク。各 API のリファレンスドキュメントには、API プレイグラウンド も含まれており、Adobe Developer Console で生成したベアラートークンを使って、エンドポイントを簡単に試すことができます。

* [API の概念と構文](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/)を含む、情報提供のための[ガイド](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/)。

* [認証方式](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/overview#authentication-support)やその他の概念について説明する最上位のチュートリアル。

* [OpenAPI ベースの API の設定方法](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup)に重点を置いたビデオを含むチュートリアル。

* サーバー間認証戦略を用いて、OpenAPI を 設定および呼び出す[エンドツーエンドのチュートリアル](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s)。web アプリおよびシングルページアプリの認証方式についても、同様のチュートリアルが用意されています。

## API アクセスの設定 {#configuring-api-access}

一部の OpenAPI ベースのAEM API には認証が必要で、[Adobe Developer Console](https://developer.adobe.com/developer-console/) を使用して資格情報を生成する必要があります。 設定には次の手順が含まれます。

1. AEM as a Cloud Service 環境の最新化。詳しくは、チュートリアルの手順の [AEM as a Cloud Service 環境の最新化](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup?#modernization-of-aem-as-a-cloud-service-environment)を参照してください。
1. 製品プロファイルを使用してAEM API へのアクセスを有効にします。 製品プロファイルは、サービスに関連付けられています。これは、事前定義されたアクセス制御リスト（ACL）を持つ AEM ユーザーグループを表します。一部のサービスはデフォルトで特定の 製品プロファイルに関連付けられていますが、その他のサービスは明示的に関連付ける必要があります。例えば、AEM Assets API Users Service はどの[製品プロファイル](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles)にも関連付けられていないため、AEM Assets API を使用するには有効化する必要があります。詳しくは、チュートリアルの手順の [AEM API アクセスの有効化](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access)を参照してください。
1. サーバー間認証を追加するには、統合を設定するユーザーが Adobe Admin Console で組織のシステム管理者であるか、またはサービスが関連付けられている製品プロファイルに開発者として追加されている必要があります。詳しくは、チュートリアルの手順の [AEM API アクセスの有効化](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access)を参照してください。
1. Adobe Developer Console（ADC）プロジェクトの作成。
1. ADC プロジェクトの設定。これにより、API の呼び出し時にベアラートークンと交換するために後で使用される資格情報が生成されます。
1. ADC プロジェクト通信を有効にする AEM インスタンスの設定。これは、以下の「[クライアント ID の登録](#registering-a-client-id)」セクションで説明されているように、YAML ファイルを設定およびデプロイして、環境にクライアント ID を登録する作業を伴います。

詳細な段階的手順については、[OpenAPI ベースの API の設定チュートリアル ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup) を参照してください。

### クライアント ID の登録 {#registering-a-client-id}

クライアント ID は、Adobe Developer Console プロジェクト内の API を特定の AEM 環境に限定します。これは以下の方法で実現されます。

1. 以下のように、必要な階層（Author、Publish、Preview）を含めた設定スニペットを記述し、`api.yaml` という名前のファイルまたは同様のファイルを作成します。`Client_id` の値は、Adobe Developer Console の API プロジェクトから取得する必要があります。

   `kind`、`version`、`metadata` のプロパティについては、[設定パイプライン](/help/operations/config-pipeline.md#common-syntax) の記事を参照してください。`kind` プロパティの値は *API* に設定し、`version` プロパティは *1* に設定する必要があります。

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

1. [設定パイプライン](/help/operations/config-pipeline.md#folder-structure)で説明されているように、`config` または類似の名前の最上位フォルダーの下のどこかにファイルを配置します。
1. RDE（コマンドラインツールを使用する環境）以外の環境タイプでは、設定パイプラインの記事の[このセクション](/help/operations/config-pipeline.md#creating-and-managing)で参照されているように、Cloud Manager で対象のデプロイメント設定パイプラインを作成します。フルスタックパイプラインと web 階層設定パイプラインでは、設定ファイルがデプロイされないことに注意してください。
1. 設定をデプロイします。
