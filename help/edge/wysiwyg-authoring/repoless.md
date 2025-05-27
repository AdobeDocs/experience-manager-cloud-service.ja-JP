---
title: サイト間でのコードの再利用
description: 外観と動作がほぼ同じで内容が異なる類似サイトが多数ある場合は、repoless モデルで複数のサイト間でコードを共有することができます。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: a6bc0f35-9e76-4b5a-8747-b64e144c08c4
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '1039'
ht-degree: 100%

---

# サイト間でのコードの再利用 {#repoless}

外観と動作がほぼ同じで内容が異なる類似サイトが多数ある場合は、repoless モデルで複数のサイト間でコードを共有することができます。

## 複数のサイトに対して 1 つのコードベース {#one-codebase}

デフォルトでは、AEM はコードリポジトリに緊密に結び付いていて、ほとんどのユースケースに対応します。一方、複数のサイトで、コンテンツはほとんど異なるものの、同じコードベースを活用できることがあります。

AEM では、同じコードベースから複数のサイトを実行することができます。複数の GitHub リポジトリを作成し、各サイトを専用の GitHub リポジトリから同期を保ちながら実行する必要はありません。

この簡略化された設定ではコードを複製する必要がありません。また、最初サイト以外では GitHub リポジトリが必要でなくなるため、[「repoless」](https://www.aem.live/docs/repoless)とも呼ばれます。

プロジェクトで、サイト間でコードを再利用するために repoless の柔軟性が必要となる場合は、この機能をアクティベートします。

最終的に repoless 方式で作成するサイトの数に関係なく、ベースサイトとなる最初のサイトを作成する必要があります。このドキュメントでは、repoless で使用する最初のサイトの作成方法を説明します。

## 前提条件 {#prerequisites}

この機能を利用するには、次の条件を満たしている必要があります。

* [Edge Delivery Services を使用した WYSIWYG オーサリングの開発者用入門ガイド](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)ドキュメントに従って、サイトが完全に設定されている。
* AEM as a Cloud Service 2024.08 以降を実行している。

また、次の項目の設定をアドビに依頼する必要があります。Slack チャネル経由でお問い合わせいただくか、サポート問題を報告して、アドビに以下の変更を行うよう依頼してください。

* お使いの環境で管理者として設定されている [aem.live 設定サービス](https://www.aem.live/docs/config-service-setup#prerequisites)をアクティブ化するよう依頼します。
* プログラムの repoless 機能を有効にするよう依頼します。
* アドビに組織の作成を依頼します。

## repoless 機能の有効化 {#activate}

プロジェクトの repoless 機能をアクティベートするには、いくつかの手順があります。

1. [アクセストークンを取得する](#access-token)
1. [設定サービスを設定する](#config-service)
1. [サイト設定とテクニカルアカウントを追加する](#access-control)
1. [AEM 設定を更新する](#update-aem)
1. [サイトを認証する](#authenticate-site)

これらの手順では、サイト `https://wknd.site` を例として使用します。適宜自分の情報に置き換えてください。

### アクセストークンを取得する {#access-token}

設定サービスを使用して repoless のユースケースに合わせて設定するには、まずアクセストークンが必要です。

1. `https://admin.hlx.page/login` に移動し、`login_adobe` アドレスを使用して、Adobe ID プロバイダーにログインします。
1. `https://admin.hlx.page/profile` に転送されます。
1. ブラウザーの開発者ツールを使用して、`admin.hlx.page` ページで設定された JSON web トークン cookie から `x-auth-token` の値をコピーします。

取得したアクセストークンは、次の形式で cURL リクエストのヘッダーに渡すことができます。

```text
--header 'x-auth-token: <your-token>'
```

### サイト設定のパスマッピングの追加とテクニカルアカウントの設定 {#access-control}

サイト設定を作成し、パスマッピングに追加する必要があります。

1. サイトのルートに新しいページを作成し、[**設定**&#x200B;テンプレート](/help/edge/wysiwyg-authoring/tabular-data.md#other)を選択します。
   * 設定は空のままにして、事前定義済みの `key` 列と `value` 列のみにしておくことができます。作成するだけです。
1. 次のような cURL コマンドを使用して、公開設定に、サイト設定へのマッピングを作成します。

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
1. 次のような cURL コマンドを使用して、公開設定が設定されていて使用可能であることを確認します。

   ```text
   curl 'https://main--<your-aem-project>--<your-github-org>.aem.live/config.json'
   ```

サイト設定がマッピングされたら、公開権限を持つテクニカルアカウントを定義することにより、アクセス制御を設定できます。

1. AEM オーサーインスタンスにログインして、**ツール**／**クラウドサービス**／**Edge Delivery Services 設定**&#x200B;に移動し、サイト用に自動作成された設定を選択して、ツールバーの「**プロパティ**」をタップまたはクリックします。

1. **Edge Delivery Services 設定**&#x200B;ウィンドウで、「**認証**」タブを選択し、「**テクニカルアカウント ID**」の値をコピーします。

   * `<tech-account-id>@techacct.adobe.com` のようになります。
   * テクニカルアカウントは、同じ AEM オーサー環境にあるすべてのサイトで同じです。

1. コピーしたテクニカルアカウント ID を使用して、次のような cURL コマンドで repoless 設定のテクニカルアカウントを設定します。

   * `admin` ブロックを調整して、サイトへの完全な管理アクセス権を持つユーザーを定義します。
      * これはメールアドレスの配列です。
      * ワイルドカード `*` を使用できます。
      * 詳しくは、[作成者の認証の設定](https://www.aem.live/docs/authentication-setup-authoring#default-roles)のドキュメントを参照してください。

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

設定サービスを使用中なので、Git リポジトリから `fstab.yaml` と `paths.json` を削除できます。

>[!NOTE]
>
>設定サービスを使用し、`config.json` 経由でパスマッピングを公開すると、`path.json` ファイルが無視されます。

AEM を repoless で使用するように設定したら、設定サービスを使用して、有効な `config.json` をパスマッピングに指定する必要があります。

### AEM 設定を更新する {#update-aem}

これで、AEM で Edge Delivery Services に必要な変更を行う準備ができました。

1. AEM オーサーインスタンスにログインして、**ツール**／**クラウドサービス**／**Edge Delivery Services 設定**&#x200B;に移動し、サイト用に自動作成された設定を選択して、ツールバーの「**プロパティ**」をタップまたはクリックします。
1. **Edge Delivery Services 設定**&#x200B;ウィンドウで、プロジェクトのタイプを **aem.live with repoless config setup** に変更し、「**保存して閉じる**」をタップまたはクリックします。
   ![Edge Delivery Services 設定](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. ユニバーサルエディターを使用してサイトに戻り、正しくレンダリングされていることを確認します。
1. コンテンツの一部を変更し、再公開します。
1. 公開済みサイト（`https://main--<your-aem-project>--<your-github-org>.aem.page/`）にアクセスして、変更が正しく反映されていることを確認します。

これで、プロジェクトが repoless で使用できるように設定されました。

## 次の手順 {#next-steps}

ベースサイトを repoless で使用できるように設定されたので、同じコードベースを活用する別のサイトを作成できます。ユースケースに応じて、次のドキュメントを参照してください。

* [repoless マルチサイト管理](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [repoless のステージ環境と実稼働環境](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)
* [コンテンツのオーサリングでのサイト認証](/help/edge/wysiwyg-authoring/site-authentication.md)

## トラブルシューティング {#troubleshooting}

repoless のユースケースを設定した後に発生する問題として最も一般的なものは、ユニバーサルエディター内のページがレンダリングされなくなったり、白いページまたは一般的な AEM as a Cloud Service のエラーメッセージが表示されたりすることです。この場合、次のようにします。

* レンダリングされたページのソースを表示します。
   * レンダリングされたもの（`scripts.js`、`aem.js` およびエディター関連の JSON ファイルを使用した正しい HTML の head）はありますか？
* 例外については、オーサーインスタンスの AEM `error.log` を確認してください。
   * 最も一般的な問題は、ページコンポーネントが 404 エラーで失敗することです。
   * `config.json or paths.json` を読み込めない
   * `component-definition.json` などを読み込めない
