---
title: Edge Delivery Services のパスマッピング
description: AEM オーサリングインスタンスで使用されるページパスを、web サイトで使用されるパブリックページパスにマッピングし、Edge Delivery Services に公開されるコンテンツを制御する方法について説明します。
feature: Edge Delivery Services
role: User
exl-id: 3d68135d-e84c-4bf4-93d1-38a0be70ce4a
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 100%

---

# Edge Delivery Services のパスマッピング {#path-mapping}

AEM オーサリングインスタンスで使用されるページパスを、web サイトで使用されるパブリックページパスにマッピングし、Edge Delivery Services に公開されるコンテンツを制御する方法について説明します。

## 概要 {#overview}

AEM を使用して WYSIWYG コンテンツをオーサリングし、Edge Delivery Services に公開できるようするには、プロジェクトのパスマッピングを設定する必要があります。このマッピングには 2 つの目的があります。

* AEM オーサリングインスタンスで使用されるページパスと、web サイトで使用されるパブリックページパス間の関係をマッピングして作成します。
* コンテンツ（ページ、シート、アセットなど）の Edge Delivery Services への公開を制御します。

パスマッピングは、プロジェクトごとに、プロジェクトのコンテンツと URL 構造に従って個別に設定する必要があります。これは、コンテンツの公開中や[ユニバーサルエディター](/help/sites-cloud/authoring/universal-editor/navigation.md)でのコンテンツの編集中に AEM によって使用されます。

## 設定形式 {#configuration-format}

パスマッピング設定の形式には、次の例のような 2 つのセクション（`mappings` と `includes`）が含まれます。

```json
{
  "mappings": [
    "/content/aem-boilerplate/:/",
    "/content/aem-boilerplate/configuration:/.helix/config.json"
  ],
  "includes:" [
    "/content/aem-boilerplate/"
  ]
}
```

### マッピング {#mappings}

`mappings` 設定には、内部パス（AEM オーサリングインスタンス上）と外部 URL パス（公開 web サイト上）の配列が保持されます。

形式は、`<internal paths>:<external path>` です。通常、少なくとも 2 つのエントリで構成されます。

1. 例の最初のエントリは、web サイトページのパスマッピングです。
1. 2 番目のエントリは、AEM オーサリングリポジトリ内の対応するスプレッドシートページへの `.helix/config.json` のマッピングを制御します。

この例では、`/content/aem-boilerplate/...` の下に保存されているすべてのページは、`https://main--my-site--org.aem.live/....` の直下にある Edge Delivery Services サイトでパブリックにアクセス可能になります。

>[!TIP]
>
>スプレッドシートとして管理されるすべての表形式データ（メタデータ、リダイレクト、分類など）は、通常、Edge Delivery Services で `.json` API URL として公開されます。これを行うには、マッピング設定に個別にリストする必要があります。
>
>詳しくは、[スプレッドシートを使用した表形式データの管理](/help/edge/wysiwyg-authoring/tabular-data.md)ドキュメントを参照してください。

### インクルード {#includes}

`includes` 設定は、実際に Edge Delivery Services にレプリケートされるコンテンツパスを制御します。任意のパス配列も保持でき、通常はサイトの上位レベルのルートページが含まれます。

Edge Delivery Services ページで使用されるアセットは、通常、web ページと共に公開されます。これらは、AEM オーサリングインスタンスから Edge Delivery Services に自動的に書き出されます。

>[!TIP]
>
>アセットを Edge Delivery Services に直接公開する必要があるユースケースがある場合（例えば、ページコンテキスト外の URL によって画像や PDF に直接アクセスできるようにする場合）、設定の `includes` セクションに DAM パスも追加する必要があります。
>
>例えば、PDF セットを含む `/content/dam/my-site/documents` などのアセットルートフォルダーに `/assets/...` 経由でパブリックにアクセスできるようにするには、設定の `includes` セクションにエントリを追加する必要があります。

## 設定方法 {#how-to-configure}

パスマッピングは、プロジェクトの設定に応じて 2 つの方法のいずれかで設定できます。

1. プロジェクトが `aem.live` 用に設定され、一元化された設定用の[設定サービス](https://www.aem.live/docs/config-service-setup)を使用する場合、各サイトのパスマッピングはこの設定サービスを通じて設定されます。

   * パスマッピングを設定する cURL リクエストの例を以下に示します。

   ```text
   curl --request POST \
     --url https://admin.aem.page/config/{org}/sites/{site}/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: ......' \
     --data '{
       "paths": {
       "mappings": [
         "/content/aem-boilerplate/:/",
         "/content/aem-boilerplate/configuration:/.helix/config.json"
       ],
       "includes": [
         "/content/aem-boilerplate/"
       ]
   }
   }'
   ```

1. プロジェクトで設定サービスを使用しない場合、パスマッピングはプロジェクトの GitHub リポジトリ内の `paths.json` ファイルを通じて設定されます。

   * 例について詳しくは、[`https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json) を参照してください。

どちらの場合も、パスマッピングを設定すると、パブリックにアクセス可能な設定 URL `https://<branch>--<site>--<org>.aem.page/config.json` を通じて設定を確認できます。
