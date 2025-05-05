---
title: サイト間でのコードの再利用
description: ほぼ同じように見えて動作する類似サイトが多数あるものの、コンテンツが異なる場合は、レポートモデルで複数のサイト間でコードを共有する方法を説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: a6bc0f35-9e76-4b5a-8747-b64e144c08c4
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 2%

---

# サイト間でのコードの再利用 {#repoless}

ほぼ同じように見えて動作する類似サイトが多数あるものの、コンテンツが異なる場合は、レポートモデルで複数のサイト間でコードを共有する方法を説明します。

## 複数のサイトに対して 1 つのコードベース {#one-codebase}

デフォルトでは、AEMはコードリポジトリに緊密に結び付けられており、ほとんどのユースケースを満たします。 ただし、コンテンツがほとんど異なるものの、同じコードベースを活用できる複数のサイトが存在する場合があります。

AEMでは、複数の GitHub リポジトリーを作成し、各サイトを専用の GitHub リポジトリーから同期を保ちながら実行するのではなく、同じコードベースから複数のサイトを実行することをサポートしています。

この簡略化された設定によって、コードを複製する必要がなくなるので、[ 「repoless」 ](https://www.aem.live/docs/repoless) とも呼ばれます。最初のサイト以外はすべて、GitHub リポジトリを必要としないからです。

プロジェクトでサイト間でのコードの再利用にリポジトリの柔軟性が必要な場合は、この機能をアクティブ化できます。

最終的にリポジトリ方式で作成するサイトの数に関係なく、最初のサイトを作成する必要があります。これはベースサイトの役割を果たします。 このドキュメントでは、リポジトリで使用する最初のサイトの作成方法を説明します。

## 前提条件 {#prerequisites}

この機能を利用するには、必ず次の手順を実行してください。

* サイトは、[Edge Delivery Servicesを使用したWYSIWYG オーサリングの開発者向けスタートガイド ](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) のドキュメントに従って、既に完全に設定されています。
* 少なくともAEM as a Cloud Service 2024.08 を実行している。

また、次の項目の設定をAdobeに依頼する必要もあります。 Slack チャネル経由でお問い合わせいただくか、サポート問題を提起してAdobeに依頼し、以下の変更を行ってください。

* お使いの環境と管理者として設定されている環境で [aem.live configuration サービス ](https://www.aem.live/docs/config-service-setup#prerequisites) をアクティブ化するように依頼します。
* Adobeによるプログラムのリポート機能を有効にするように依頼します。
* Adobeに組織の作成を依頼します。

## リポジトリ機能の有効化 {#activate}

プロジェクトのリソース機能をアクティベートするには、いくつかの手順があります。

1. [アクセストークンの取得](#access-token)
1. [設定サービスの設定](#config-service)
1. [サイト設定とテクニカルアカウントの追加](#access-control)
1. [AEM設定の更新](#update-aem)
1. [サイトの認証](#authenticate-site)

これらの手順では、サイト `https://wknd.site` を例として使用します。 適当にあなた自身の物を入れ替えなさい。

### アクセストークンの取得 {#access-token}

最初に設定サービスを使用してリポジトリのユースケースに合わせて設定するには、アクセストークンが必要です。

1. `https://admin.hlx.page/login` に移動し、`login_adobe` アドレスを使用してAdobe ID プロバイダーにログインします。
1. `https://admin.hlx.page/profile` に転送されます。
1. ブラウザーの開発者ツールを使用して、`admin.hlx.page` ページが設定した JSON web トークン cookie から `x-auth-token` の値をコピーします。

アクセストークンを取得したら、次の形式で cURL リクエストのヘッダーに渡すことができます。

```text
--header 'x-auth-token: <your-token>'
```

### サイト設定のパスマッピングの追加とテクニカルアカウントの設定 {#access-control}

サイト設定を作成し、パスマッピングに追加する必要があります。

1. サイトのルートに新しいページを作成し、[**設定** テンプレート ](/help/edge/wysiwyg-authoring/tabular-data.md#other) を選択します。
   * 設定は空のままにして、事前定義済みの `key` と `value` 列のみを追加できます。 作成するだけで済みます。
1. 次のような cURL コマンドを使用して、パブリック設定に、サイト設定へのマッピングを作成します。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/<your-site-content>/:/",
               "/content/<your-site-content>/configuration:/.helix/config.json"
      ],
           "includes": [
               "/content/<your-site-content>/"
           ]
       }
   }'
   ```

1. 次のような cURL コマンドを使用して、公開設定が使用可能に設定されていることを検証します。

   ```text
   curl 'https://main--<your-aem-project>--<your-github-org>.aem.live/config.json'
   ```

サイト設定がマッピングされたら、公開権限を持つテクニカルアカウントを定義することで、アクセス制御を設定できます。

1. AEM オーサーインスタンスにサインインして **ツール**/**クラウドサービス**/**Edge Delivery Services Configuration** に移動し、サイト用に自動的に作成された設定を選択して、ツールバーの **プロパティ** をタップまたはクリックします。

1. **Edge Delivery Services設定** ウィンドウで、「**認証**」タブを選択し、「**テクニカルアカウント ID**」の値をコピーします。

   * `<tech-account-id>@techacct.adobe.com` のようになります
   * テクニカルアカウントは、1 つのAEM オーサー環境にあるすべてのサイトで同じです。

1. コピーしたテクニカルアカウント ID を使用して、次のような cURL コマンドでリクエスト設定のテクニカルアカウントを設定します。

   * `admin` ブロックを調整して、サイトへの完全な管理アクセス権を持つユーザーを定義します。
      * これはメールアドレスの配列です。
      * ワイルドカード `*` を使用できます。
      * 詳しくは、[ 作成者の認証の設定 ](https://www.aem.live/docs/authentication-setup-authoring#default-roles) ドキュメントを参照してください。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/access.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "admin": {
           "role": {
               "admin": [
                   "<email>@<domain>.<tld>"
               ],
               "config_admin": [
                   "<tech-account-id>@techacct.adobe.com"
               ]
           },
           "requireAuth": "auto"
       }
   }'
   ```

設定サービスを使用するようになったので、Git リポジトリから `fstab.yaml` と `paths.json` を削除できます。

>[!NOTE]
>
>設定サービスを使用し、`config.json` 経由でパスマッピングを公開すると、`path.json` ファイルは無視されます。

AEMをリポジトリで使用するように設定したら、configuration サービスを使用して、有効な `config.json` をパスマッピングに指定する必要があります。

### AEM設定の更新 {#update-aem}

これで、AEMのEdge Delivery Servicesに必要な変更を加える準備が整いました。

1. AEM オーサーインスタンスにサインインして **ツール**/**クラウドサービス**/**Edge Delivery Services Configuration** に移動し、サイト用に自動的に作成された設定を選択して、ツールバーの **プロパティ** をタップまたはクリックします。
1. **Edge Delivery Services設定** ウィンドウで、プロジェクトのタイプを **aem.live with repoless config setup** に変更し、「**保存して閉じる**」をタップまたはクリックします。
   ![Edge Delivery Servicesの設定 ](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. ユニバーサルエディターを使用してサイトに戻り、正しくレンダリングされていることを確認します。
1. コンテンツの一部を変更し、再公開します。
1. 公開済みサイト（`https://main--<your-aem-project>--<your-github-org>.aem.page/`）にアクセスして、変更が正しく反映されていることを確認します。

これで、プロジェクトがリポジトリで使用できるように設定されました。

## 次の手順 {#next-steps}

ベースサイトがリポジトリで使用できるように設定されたので、同じコードベースを活用する追加のサイトを作成できます。 ユースケースに応じて、次のドキュメントを参照してください。

* [Repoless マルチサイト管理](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [Repoless ステージと実稼動環境](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)
* [コンテンツオーサリングのサイト認証](/help/edge/wysiwyg-authoring/site-authentication.md)

## トラブルシューティング {#troubleshooting}

レポートユースケースを設定した後に発生する最も一般的な問題は、ユニバーサルエディター内のページがレンダリングされなくなったり、白いページまたは一般的なAEM as a Cloud Serviceのエラーメッセージが表示されたりすることです。 この場合の解決策は、次のとおりです。

* レンダリングされたページのソースの表示。
   * 何かレンダリングされるもの（`scripts.js`、`aem.js` およびエディター関連の JSON ファイルを使用してHTMLの head を修正してください）はありますか？
* 例外については、オーサーインスタンスのAEM `error.log` を確認してください。
   * 最も一般的な問題は、ページコンポーネントが 404 エラーで失敗することです。
   * `config.json or paths.json` を読み込むことができません
   * `component-definition.json` 等 を読み込めません
