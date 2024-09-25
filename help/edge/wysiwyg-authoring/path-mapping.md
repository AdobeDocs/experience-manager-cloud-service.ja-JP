---
title: Edge Delivery Servicesのパスマッピング
description: AEM オーサーインスタンスで使用されるページパスを web サイトで使用されるパブリックページパスにマッピングし、Edge Delivery Servicesに公開するコンテンツを制御する方法について説明します。
feature: Edge Delivery Services
role: User
source-git-commit: 51a2b453ccce39cb42c927a088bc088083545542
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# Edge Delivery Servicesのパスマッピング {#path-mapping}

AEM オーサーインスタンスで使用されるページパスを web サイトで使用されるパブリックページパスにマッピングし、Edge Delivery Servicesに公開するコンテンツを制御する方法について説明します。

## 概要 {#overview}

AEMを使用してWYSIWYG コンテンツを作成し、Edge Delivery Servicesに公開できるようにするには、プロジェクトのパスマッピングを設定する必要があります。 このマッピングには 2 つの目的があります。

* AEM オーサリングインスタンスで使用されるページパスと web サイトで使用されるパブリックページパスとの間の関係をマッピングおよび作成します。
* コンテンツ（ページ、シート、アセットなど）を制御します。 Edge Delivery Servicesに公開されます。

パスマッピングは、プロジェクトごとに、プロジェクトのコンテンツと URL 構造に従って個別に設定する必要があります。 AEMがコンテンツの公開中や、[ ユニバーサルエディター ](/help/sites-cloud/authoring/universal-editor/navigation.md) でコンテンツを編集する際に使用されます。

## 設定フォーマット {#configuration-format}

パスマッピング設定の形式には、次の例のような 2 つのセクション（`mappings` と `includes`）が含まれています。

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

`mappings` 設定には、（AEM オーサリングインスタンス上の）内部パスと（パブリック web サイト上の）外部 URL パスの配列が格納されます。

形式は `<internal paths>:<external path>` です。 通常、少なくとも 2 つのエントリで構成されます。

1. 例の最初のエントリは、web サイトページのパスマッピングです。
1. 2 つ目のエントリは、AEM オーサリングリポジトリ内の対応するスプレッドシートページへの `.helix/config.json` のマッピングを制御します。

この例では、`/content/aem-boilerplate/...` に保存されたすべてのページが、Edge Delivery Servicesサイトの `https://main--my-site--org.aem.live/....` に直接、公開アクセスできます。

>[!TIP]
>
>スプレッドシートとして管理されるすべての表形式のデータ（メタデータ、リダイレクト、分類など）は、通常、Edge Delivery Services上の API URL`.json` して公開されます。 これを行うには、マッピング設定に個別にリストされる必要があります。
>
>詳しくは、[ スプレッドシートを使用した表形式のデータの管理 ](/help/edge/wysiwyg-authoring/tabular-data.md) のドキュメントを参照してください。

### includes {#includes}

`includes` 設定は、実際にEdge Delivery Servicesにレプリケートされるコンテンツパスを制御します。 パスの任意の配列を保持することもでき、通常はサイトの最上位のルートページを含みます。

Edge Delivery Servicesページで使用されるAssetsは、通常、web ページと共に公開されます。 これらは、AEM オーサリングインスタンスからEdge Delivery Servicesに自動的に書き出されます。

>[!TIP]
>
>Edge Delivery Servicesに直接公開するアセットが必要なユースケースがある場合（例えば、ページコンテキスト以外で画像やPDFにその URL から直接アクセスできるようにする場合）、設定の `includes` セクションにも DAM パスを追加する必要があります。
>
>例えば、`/content/dam/my-site/documents` などのアセットのルートフォルダーが `/assets/...` を介してPDFのセットを含んでいる場合、そのフォルダーに公開アクセスできるようにするには、設定の `includes` セクションにエントリを追加する必要があります。

## 設定方法 {#how-to-configure}

パスマッピングは、プロジェクトの設定に応じて、2 つの方法のいずれかで設定できます。

1. プロジェクトが `aem.live` 用に設定され、一元化された設定に [ 設定サービス ](https://www.aem.live/docs/config-service-setup) を使用する場合、各サイトのパスマッピングは、この設定サービスを介して設定されます。

   * パスマッピングを設定するための cURL リクエストの例を次に示します。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/{org}/sites/{site}/public.json \
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

1. プロジェクトで設定サービスを使用しない場合、パスマッピングはプロジェクト GitHub リポジトリの paths.json ファイルを介して設定されます。

   * 例については、[`https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json`](/https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json) を参照してください。

どちらの場合も、パスマッピングを設定したら、公開アクセス可能な設定 URL `https://<branch>--<site>--<org>.aem.page/config.json` を使用して設定を確認できます。
