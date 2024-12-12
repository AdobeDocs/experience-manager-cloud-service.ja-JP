---
title: レポートステージと実稼働環境
description: 単一のコードベースをリポジトリで活用して、ステージング環境と実稼動環境用に個別のサイトを設定する方法を説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 709d0661286d023c5cec51be2c51a1123ef7deb6
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---


# レポートステージと実稼働環境 {#repoless-stage-prod}

単一のコードベースをリポジトリで活用して、ステージング環境と実稼動環境用に個別のサイトを設定する方法を説明します。

## 概要 {#overview}

ステージング環境とは別に、実稼動環境用のサイトを設定したい場合があります。 ステージング環境と実稼動環境を個別に設定するための 2 つ目のサイトの設定は、マルチサイト管理に必要な [ 設定に似ています。](/help/edge/wysiwyg-authoring/repoless-msm.md) 実際、必要に応じて、MSM サイト構造と組み合わせることができます。

このドキュメントでは、個別のステージング環境と実稼動環境の典型的な例を使用します。 希望する任意の環境に対して、個別の環境を作成できます。

## 設定 {#configuration}

このドキュメントでは、同じコードベースを使用して、プロジェクトに別の実稼動サイトを設定する方法について説明します。 以下の前提に基づいています。

* ステージングサイトは既に設定済みで、実稼動サイトの設定を作成する必要があります。
* AEM オーサリングのコンテンツ構造は似ています。
* ステージングと実稼動では、同じパスマッピングが使用されます。

この例では、GitHub リポジトリも wknd と呼ばれる wknd というプロジェクトの実稼動サイトが既に作成されていると想定しています。

個別の実稼動サイトを設定するには、次の 2 つの手順があります。

1. [実稼動環境用に新しいEdge Delivery Servicesサイトを作成します。](#create-edge-site)
1. [実稼動サイト用にAEMのクラウド設定を更新します。](#update-cloud-configuration)

### 実稼動環境用の新しいEdge Delivery Servicesサイトの作成 {#create-edge-site}

1. 認証トークンとプログラムのテクニカルアカウントを取得します。
   * プログラムの **アクセストークンを取得** する方法と [ テクニカルアカウント [ について詳しくは ](/help/edge/wysiwyg-authoring/repoless.md#access-token) サイト間でのコードの再利用 ](/help/edge/wysiwyg-authoring/repoless.md#access-control) ドキュメントを参照してください。
1. 設定サービスに対して次の呼び出しを実行して、新しいサイトを作成します。 次の点を考慮してください。
   * POST URL のプロジェクト名は、新しく作成するサイト名にする必要があります。 この例では、`wknd-prod` です。
   * `code` の設定は、最初のプロジェクト作成に使用した設定と同じである必要があります。
   * `content`/`source`/`url` は、作成する新しいサイトの名前に合わせて変更する必要があります。 この例では、`wknd-prod` です。
   * つまり、「POSTURL」のサイト名と「`content`/`source`/`url`」は同じにする必要があります。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-prod.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
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
               "url": "https://author-p<programID>-e<environmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/wknd-prod/main",
               "type": "markup",
               "suffix": ".html"
           }
       },
       "access": {
           "admin": {
               "role": {
                   "admin": [
                       "*@adobe.com"
                   ],
                   "publish": [
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
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-prod/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/wknd/:/"
           ],
           "includes": [
               "/content/wknd/"
           ]
       }
   }'
   ```

`https://main--wknd-prod--<your-github-org>.aem.page/config.json` を呼び出し、返される JSON のコンテンツを確認することで、新しいサイトのパブリック設定が機能していることを確認します。

### 実稼動サイト用のAEMのクラウド設定の更新 {#update-cloud-configuration}

実稼動用AEMは、専用の実稼動サイトに対して前の節で作成した新しいEdge Delivery サイトを使用するように設定されている必要があります。 この例では、実稼動環境の `/content/wknd` 下にあるコンテンツが、作成した `wknd-prod` サイトを使用することを知っている必要があります。

1. AEM実稼動インスタンスにサインインし、**ツール**/**Cloud Service**/**Edge Delivery Services設定** に移動します。
1. プロジェクトのために自動的に作成された設定を選択します。
1. ツールバーの **プロパティ** をタップまたはクリックします。
1. **Edge Delivery Services設定** ウィンドウで、次の操作を行います。
   * 「**組織**」フィールドに GitHub 組織を入力します。
   * サイト名を、前の節で作成したサイトの名前に変更します。 この場合、`wknd-prod` になります。
   * プロジェクトのタイプを「**aem.live with repoless config setup**」に変更します。
1. 「**保存して閉じる**」をタップまたはクリックします。

## 設定の確認 {#verify}

必要な設定の変更をすべて行ったら、すべてが期待どおりに動作していることを確認します。

1. AEM実稼動オーサリングインスタンスにログインします。
1. **ナビゲーション**/**サイト** に移動して **サイトコンソール** に移動します。
1. サイトでページを選択します。
1. ツールバーの **編集** をタップまたはクリックします。
1. ページがユニバーサルエディターで適切にレンダリングされ、サイトルートと同じコードを使用していることを確認します。
1. ページに変更を加えて、再公開します。
1. そのページの新しいEdge Delivery Servicesサイト（`https://main--wknd-prod--<your-github-org>.aem.page`）にアクセスします。

変更を加えた場合は、個別の実稼動サイト設定が正しく機能しています。
