---
title: 複数サイト管理のレポート
description: 1 つのコードベースを活用するローカライズされたサイトを使用してリポジトリ方式でプロジェクトを設定する方法に関するベストプラクティスの推奨事項を説明します。各サイトはEdge Delivery Servicesによって提供されます。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: e25e21984ebadde7076d95c6051b8bfca5b2ce03
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 1%

---


# 複数サイト管理のレポート {#repoless-msm}

1 つのコードベースを活用するローカライズされたサイトを使用してリポジトリ方式でプロジェクトを設定する方法に関するベストプラクティスの推奨事項を説明します。各サイトはEdge Delivery Servicesによって提供されます。

## 概要 {#overview}

[ マルチサイトマネージャー（MSM） ](/help/sites-cloud/administering/msm/overview.md) とそのライブコピー機能を使用すると、同じサイトコンテンツを複数の場所で使用できると同時に、バリエーションを作成することもできます。 コンテンツを 1 回作成してライブコピーを作成できます。 MSM では、ソースコンテンツとライブコピーの間にライブ関係を維持するので、ソースコンテンツを変更すると、ソースコピーとライブコピーを同期できます。

MSM を使用すると、ロケールや言語をまたいでブランドのコンテンツ構造全体を作成し、コンテンツを一元的にオーサリングできます。 ローカライズされたサイトは、中央のコードベースを活用して、Edge Delivery Servicesで個別に配信できます。

## 要件 {#requirements}

リポジトリのユースケースで MSM を設定するには、まず複数のタスクを実行する必要があります。

* このドキュメントは、[Edge Delivery ServicesでのWYSIWYG オーサリングのための開発者向けスタートガイド ](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) ガイドに基づいて、プロジェクトのサイトを既に作成していることを前提としています。
* [ プロジェクトのリソース機能を有効にする ](/help/edge/wysiwyg-authoring/repoless.md) 必要があります。

## ユースケース {#use-case}

このドキュメントでは、プロジェクトの基本的なローカライズされたサイト構造が既に作成されていることを前提としています。 例えば、スイスとドイツにある wknd ブランドには次の構造を使用します。

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

`language-masters` のコンテンツは、ローカライズされたサイトのライブコピーのソースです（ドイツ（`de`）およびスイス（`ch`））。 このドキュメントの目的は、ローカライズされたサイトごとに同じコードベースを使用するEdge Delivery Servicesサイトを作成することです。

## 設定 {#configuration}

MSM リポジトリのユースケースを設定するには、いくつかの手順があります。

1. [AEM サイト設定を更新します。](#update-aem-configurations)
1. [ローカライズしたページ用に新しいEdge Delivery Servicesサイトを作成します。](#create-edge-sites)
1. [ローカライズしたサイトに合わせて、AEMのクラウド設定を更新します。](#update-cloud-configurations)

### AEM サイト設定の更新 {#update-aem-configurations}

[ 設定 ](/help/implementing/developing/introduction/configurations.md) は、組織的な目的で設定のグループと関連コンテンツを収集するために使用できるワークスペースと考えることができます。 AEMでサイトを作成すると、そのサイトの設定が自動的に作成されます。

通常、次のようなサイト間で特定のコンテンツを共有します。

* ブループリントのコンテンツから作成されたテンプレート
* コンテンツフラグメントモデル、永続クエリなど。

このような共有を容易にするために、追加の設定を作成できます。 wknd のユースケースでは、次のパスの設定が必要になります。

```text
/content/wknd
/content/wknd/ch
/content/wknd/de
```

つまり、ブループリントで使用される wknd ブランドのコンテンツ（`/content/wknd`）のルートの設定と、ローカライズされた各サイト（スイスとドイツ）で使用される設定があります。

1. AEM オーサリングインスタンスにログインします。
1. **ツール**/**一般**/**設定ブラウザー** に移動して **設定ブラウザー** に移動します。
1. プロジェクト用に自動的に作成された設定（この場合は wknd）を選択し、ツールバーの **作成** をタップまたはクリックします。
1. **設定を作成** ダイアログで、ローカライズされたサイトのわかりやすい **名前** を指定します（`Switzerland` など）。**タイトル** には、ローカライズされたサイズと同じタイトル（この場合は `ch`）を使用します。
1. **クラウド設定** 機能と、プロジェクトに必要な追加機能（**編集可能テンプレート** など）を選択します。
1. 「**作成**」をタップまたはクリックします。

必要なローカライズ済みサイトごとに設定を作成します。 wknd の場合は、`ch` 設定と共に、`de` 用の設定も作成する必要があります。

設定を作成したら、ローカライズされたサイトで使用されるようにする必要があります。

1. AEM オーサリングインスタンスにログインします。
1. **ナビゲーション**/**サイト** に移動して **サイトコンソール** に移動します。
1. `Switzerland` など、ローカライズされたサイトを選択します。
1. ツールバーの **プロパティ** をタップまたはクリックします。
1. ページのプロパティ ウィンドウで、「**詳細**」タブを選択し、「**設定**」見出しの下で「**/content/wknd から継承**」オプションの選択を解除します。ここで、`wknd` はサイトのルートです。
1. 「**クラウド設定**」フィールドで、パスブラウザーを使用して、ローカライズされたサイト用に作成した設定（`/conf/wknd/ch` の下の `Switzerland` など）を選択します。
1. 「**保存して閉じる**」をタップまたはクリックします。

追加のローカライズされたサイトにそれぞれの設定を割り当てます。 wknd の場合は、`/conf/wknd/de` 設定をドイツのサイトにも割り当てる必要があります。

### ローカライズされたページ用に新しいEdge Delivery Servicesサイトを作成する {#create-edge-sites}

複数地域、複数言語のサイト設定でEdge Delivery Servicesにサイトを接続する場合は、AEM MSM サイトごとに新しい aem.live サイトを設定する必要があります。 共有 Git リポジトリとコードベースを持つAEM MSM サイトと aem.live サイトは、1 対 1 の関係にあります。

この例では、wknd がスイス拠点に存在する場合のサイト `wknd-ch` を作成します。スイス拠点のローカライズされたコンテンツは、AEM パス `/content/wknd/ch` の配下に配置されます。

1. 認証トークンとプログラムのテクニカルアカウントを取得します。
   * プログラムの **アクセストークンを取得** する方法と [ テクニカルアカウント [ について詳しくは ](/help/edge/wysiwyg-authoring/repoless.md#access-token) サイト間でのコードの再利用 ](/help/edge/wysiwyg-authoring/repoless.md#access-control) ドキュメントを参照してください。
1. 設定サービスに対して次の呼び出しを実行して、新しいサイトを作成します。 次の点を考慮してください。
   * POST URL のプロジェクト名は、新しく作成するサイト名にする必要があります。 この例では、`wknd-ch` です。
   * `code` の設定は、最初のプロジェクト作成に使用した設定と同じである必要があります。
   * `content`/`source`/`url` は、作成する新しいサイトの名前に合わせて変更する必要があります。 この例では、`wknd-ch` です。
   * つまり、「POSTURL」のサイト名と「`content`/`source`/`url`」は同じにする必要があります。

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

手順を繰り返して、ローカライズされたサイトを追加で作成します。 wknd の場合は、ドイツ語プレゼンス用の `wknd-de` サイトも作成する必要があります。

### ローカライズしたページへのAEM クラウド設定の更新 {#update-cloud-configurations}

AEMのページは、ローカライズされた表示域で、前の節で作成した新しいEdge Delivery Sites を使用するように設定する必要があります。 この例では、`/content/wknd/ch` の配下のコンテンツが、作成した `wknd-ch` サイトを使用することを知っている必要があります。 同様に、`/content/wknd/de` 下のコンテンツも `wknd-de` サイトを使用する必要があります。

1. AEM オーサーインスタンスにログインし、**ツール**/**Cloud Service**/**Edge Delivery Services設定** に移動します。
1. プロジェクト用に自動的に作成された設定を選択し、ローカライズされたページ用に作成されたフォルダーを選択します。 この場合、スイス（`ch`）になります。
1. ツールバーで **作成**/**設定** をタップまたはクリックします。
1. **Edge Delivery Services設定** ウィンドウで、次の操作を行います。
   * 「**組織**」フィールドに GitHub 組織を入力します。
   * サイト名を、前の節で作成したサイトの名前に変更します。 この場合、`wknd-ch` になります。
   * プロジェクトのタイプを「**aem.live with repoless config setup**」に変更します。
1. 「**保存して閉じる**」をタップまたはクリックします。

## 設定の確認 {#verify}

必要な設定の変更をすべて行ったら、すべてが期待どおりに動作していることを確認します。

1. AEM オーサリングインスタンスにログインします。
1. **ナビゲーション**/**サイト** に移動して **サイトコンソール** に移動します。
1. `Switzerland` など、ローカライズされたサイトを選択します。
1. ツールバーの **編集** をタップまたはクリックします。
1. ページがユニバーサルエディターで適切にレンダリングされ、サイトルートと同じコードを使用していることを確認します。
1. ページに変更を加えて、再公開します。
1. ローカライズされたページ（`https://main--wknd-ch--<your-github-org>.aem.page`）を参照するには、新しいEdge Delivery Servicesのサイトにアクセスしてください。

行った変更が表示される場合は、MSM の設定が正しく動作しています。
