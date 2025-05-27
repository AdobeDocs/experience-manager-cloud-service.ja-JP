---
title: repoless マルチサイト管理
description: Edge Delivery Services で提供され、1 つのコードベースを活用している複数のローカライズ済みサイトを使用するプロジェクトを repoless 方式で設定する方法に関する、ベストプラクティスの推奨事項を説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: f6b861ed-18e4-4c81-92d2-49fadfe4669a
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '1260'
ht-degree: 100%

---

# repoless マルチサイト管理 {#repoless-msm}

Edge Delivery Services で提供され、1 つのコードベースを活用している複数のローカライズ済みサイトを使用するプロジェクトを repoless 方式で設定する方法に関する、ベストプラクティスの推奨事項を説明します。

## 概要 {#overview}

[マルチサイトマネージャ（MSM）](/help/sites-cloud/administering/msm/overview.md)とそのライブコピー機能を使用すると、同じサイトコンテンツを複数の場所で使用できると同時に、バリエーションを作成することもできます。コンテンツを 1 回作成すると、ライブコピーを作成できます。MSM では、ソースコンテンツとライブコピーの間のライブ関係が維持されるので、ソースコンテンツを変更すると、ソースとライブコピーを同期できます。

MSM を使用すると、ロケールや言語にまたがってブランドのコンテンツ構造全体を作成し、コンテンツを一元的にオーサリングすることができます。ローカライズされたサイトは、一元化されたコードベースを活用して、Edge Delivery Services によって提供されます。

## 要件 {#requirements}

repoless のユースケースで MSM を設定するには、まず次のタスクを実行する必要があります。

* このドキュメントは、[Edge Delivery Services を使用した WYSIWYG オーサリングの開発者向け入門ガイド](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)に基づいて、プロジェクトのサイトを既に作成していることを前提としています。
* [プロジェクトの repoless 機能が既に有効になっている](/help/edge/wysiwyg-authoring/repoless.md)必要があります。

## ユースケース {#use-case}

このドキュメントでは、プロジェクトの基本的なローカライズ済みサイト構造が既に作成されていることを前提としています。例えば、スイスとドイツに活動拠点がある wknd ブランドの場合、次のような構造を使用します。

```text
/content/wknd
/content/wknd/language-masters
/content/wknd/language-masters/en
/content/wknd/language-masters/de
/content/wknd/language-masters/fr
/content/wknd/language-masters/it
/content/wknd/ch
/content/wknd/ch/de
/content/wknd/ch/fr
/content/wknd/ch/it
/content/wknd/ch/en
/content/wknd/de
/content/wknd/de/de
/content/wknd/de/en
```

`language-masters` のコンテンツは、ドイツ（`de`）およびスイス（`ch`）向けにローカライズされたサイトのライブコピーのソースです。このドキュメントの目的は、ローカライズされたサイトごとに同じコードベースを使用する Edge Delivery Services サイトを作成することです。

## 設定 {#configuration}

MSM の repoless のユースケースを設定するには、いくつかの手順があります。

1. [AEM サイト設定を更新](#update-aem-configurations)します。
1. [ローカライズしたページ用に新しい Edge Delivery Services サイトを作成](#create-edge-sites)します。
1. [ローカライズしたサイト用に AEM のクラウド設定を更新](#update-cloud-configurations)します。

### AEM サイト設定の更新 {#update-aem-configurations}

[設定](/help/implementing/developing/introduction/configurations.md)は、組織的な目的のために、設定のグループと関連コンテンツを収集するために使用できるワークスペースと考えることができます。AEM でサイトを作成すると、そのサイトの設定が自動的に作成されます。

通常、サイト間で共有されるコンテンツには次のようなものがあります。

* ブループリントのコンテンツから作成されたテンプレート
* コンテンツフラグメントモデル、永続クエリなど

このような共有を容易にするために、追加の設定を作成できます。wknd のユースケースでは、次のパスの設定が必要になります。

```text
/content/wknd
/content/wknd/ch
/content/wknd/de
```

つまり、ブループリントで使用される wknd ブランドのコンテンツのルート（`/content/wknd`）の設定と、ローカライズされた各サイト（スイスとドイツ）で使用される設定があります。

1. AEM オーサリングインスタンスにログインします。
1. **ツール**／**一般**／**設定ブラウザー**&#x200B;から、**設定ブラウザー**&#x200B;に移動します。
1. プロジェクト用に自動的に作成された設定（この場合は wknd）を選択し、ツールバーの「**作成**」をタップまたはクリックします。
1. **設定を作成**&#x200B;ダイアログで、ローカライズされたサイトにわかりやすい&#x200B;**名前**&#x200B;を指定します（`Switzerland` など）。**タイトル**&#x200B;には、ローカライズされたサイトと同じタイトル（この場合は `ch`）を使用します。
1. **クラウド設定**&#x200B;機能と、プロジェクトに必要な追加機能（**編集可能テンプレート**&#x200B;など）を選択します。
1. 「**作成**」をタップまたはクリックします。

必要なローカライズ済みサイトごとに設定を作成します。wknd の場合は、`ch` 設定と共に、`de` 用の設定も作成する必要があります。

設定を作成したら、ローカライズされたサイトでその設定が使用されるようにする必要があります。

1. AEM オーサリングインスタンスにログインします。
1. **ナビゲーション**／**Sites** に移動して、**Sites コンソール**&#x200B;に移動します。
1. `Switzerland` などのローカライズされたサイトを選択します。
1. ツールバーの「**プロパティ**」をタップまたはクリックします。
1. ページのプロパティウィンドウで、「**詳細**」タブを選択し、「**設定**」の見出しの下で「**/content/wknd から継承**」オプションをオフにします。ここで、`wknd` はサイトのルートです。
1. 「**クラウド設定**」フィールドで、パスブラウザーを使用して、ローカライズされたサイト用に作成した設定（`/conf/wknd/ch` の下の `Switzerland` など）を選択します。
1. 「**保存して閉じる**」をタップまたはクリックします。

追加のローカライズ済みサイトにそれぞれの設定を割り当てます。wknd の場合は、`/conf/wknd/de` 設定をドイツのサイトにも割り当てる必要があります。

### ローカライズされたページ用の新しい Edge Delivery Services サイトの作成 {#create-edge-sites}

複数地域、複数言語のサイト設定用にさらに多くのサイトを Edge Delivery Services に接続するには、AEM MSM サイトごとに新しい aem.live サイトを設定する必要があります。Git リポジトリとコードベースを共有する AEM MSM サイトと aem.live サイトは、1 対 1 の関係にあります。

この例では、wknd のスイス拠点について `wknd-ch` サイトを作成します。この拠点のためにローカライズされたコンテンツは、AEM のパス `/content/wknd/ch` の下に配置されます。

1. 認証トークンとプログラム用のテクニカルアカウントを取得します。
   * プログラムの[アクセストークン](/help/edge/wysiwyg-authoring/repoless.md#access-token)と[テクニカルアカウントを取得](/help/edge/wysiwyg-authoring/repoless.md#access-control)する方法について詳しくは、**サイト間でのコードの再利用**&#x200B;のドキュメントを参照してください。
1. 設定サービスに対して次の呼び出しを実行して、新しいサイトを作成します。以下の点を考慮してください。
   * POST URL のプロジェクト名は、作成する新しいサイト名である必要があります。この例では `wknd-ch` です。
   * `code` の設定は、最初のプロジェクト作成に使用した設定と同じである必要があります。
   * `content`／`source`／`url` は、作成する新しいサイトの名前に合わせて変更する必要があります。この例では `wknd-ch` です。
   * つまり、POST URL のサイト名と `content`／`source`／`url` は同じである必要があります。
   * `admin` ブロックを調整して、サイトへの完全な管理アクセス権を持つユーザーを定義します。
      * これはメールアドレスの配列です。
      * ワイルドカード `*` を使用できます。
      * 詳しくは、[作成者の認証設定](https://www.aem.live/docs/authentication-setup-authoring#default-roles)のドキュメントを参照してください。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "code": {
           "owner": "<your-github-org>",
           "repo": "wknd",
           "source": {
               "type": "github",
               "url": "https://github.com/<your-github-org>/wknd"
           }
       },
       "content": {
           "source": {
               "url": "https://author-p<programID>-e<environmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/wknd-ch/main",
               "type": "markup",
               "suffix": ".html"
           }
       },
       "access": {
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
       }
   }'
   ```

1. 設定サービスに対して次の呼び出しを実行して、新しいサイトのパスマッピングを追加します。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "paths": {
           "mappings": [
               "/content/wknd/ch/:/"
           ],
           "includes": [
               "/content/wknd/ch/"
           ]
       }
   }'
   ```

1. `https://main--wknd-ch--<your-github-org>.aem.page/config.json` を呼び出し、返される JSON のコンテンツを確認することで、新しいサイトのパブリック設定が機能していることを確認します。

手順を繰り返して、ローカライズされたサイトを追加で作成します。wknd の場合は、ドイツの拠点に対しても `wknd-de` サイトを作成する必要があります。

### ローカライズしたページ用の AEM のクラウド設定の更新 {#update-cloud-configurations}

AEM のページは、ローカライズのために前の節で作成した新しい Edge Delivery サイトを使用するように設定する必要があります。この例では、`/content/wknd/ch` の下のコンテンツが、作成した `wknd-ch` サイトを使用するように設定されている必要があります。同様に、`/content/wknd/de` の下のコンテンツも `wknd-de` サイトを使用する必要があります。

1. AEM オーサーインスタンスにログインし、**ツール**／**クラウドサービス**／**Edge Delivery Services 設定**&#x200B;に移動します。
1. プロジェクト用に自動的に作成された設定を選択し、その後、ローカライズされたページ用に作成されたフォルダーを選択します。この場合、スイス（`ch`）になります。
1. ツールバーで&#x200B;**作成**／**設定**&#x200B;をタップまたはクリックします。
1. **Edge Delivery Services 設定**&#x200B;ウィンドウで、次の操作を行います。
   * 「**組織**」フィールドに GitHub 組織を入力します。
   * サイト名を、前のセクションで作成したサイトの名前に変更します。この場合は `wknd-ch` です。
   * プロジェクトのタイプを「**aem.live with repoless config setup**」に変更します。
1. 「**保存して閉じる**」をタップまたはクリックします。

## 設定の確認 {#verify}

必要な設定の変更をすべて行ったら、すべてが想定どおりに動作していることを確認します。

1. AEM オーサリングインスタンスにログインします。
1. **ナビゲーション**／**Sites** に移動して、**Sites コンソール**&#x200B;に移動します。
1. `Switzerland` など、ローカライズされたサイトを選択します。
1. ツールバーの「**削除**」をタップまたはクリックします。
1. ページがユニバーサルエディターで適切にレンダリングされ、サイトルートと同じコードを使用していることを確認します。
1. ページを変更して、再公開します。
1. ローカライズされたページ（`https://main--wknd-ch--<your-github-org>.aem.page`）を参照するには、新しい Edge Delivery Services のサイトにアクセスしてください。

変更が反映されている場合は、MSM 設定が正しく機能しています。
