---
title: リソースマッピング
description: リソースマッピングを使用して、AEM のリダイレクト、バニティ URL、仮想ホストを定義する方法について説明します。
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 1a1bb23c-d1d1-4e2b-811b-753e6a90a01b
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 97%

---

# リソースマッピング{#resource-mapping}

リソースマッピングは、AEM のリダイレクト、バニティ URL および仮想ホストを定義するために使用します。

例えば、これらのマッピングを使用すると次のことが可能です。

* すべてのリクエストに `/content` というプレフィックスを付けて、web サイトの訪問者に内部構造が表示されないようにする。
* Web サイトの `/content/en/gateway` ページへのリクエストがすべて `https://gbiv.com/` にリダイレクトされるように、リダイレクトを定義する。

HTTP マッピングの一例として、`localhost:4503` に対するすべてのリクエストに `/content` というプレフィックスを指定します。このようなマッピングを使用すると、Web サイトの訪問者に対して内部構造を非表示にすることができます。例えば、次のページの場合は、

`localhost:4503/content/we-retail/en/products.html`

以下を使用してアクセスできます。

`localhost:4503/we-retail/en/products.html`

マッピングによって、`/content` という接頭辞が `/we-retail/en/products.html` に自動的に追加されるからです。

>[!CAUTION]
>
>バニティー URL は regex パターンをサポートしません。

>[!NOTE]
>
>詳しくは、Sling のドキュメントと「[Mappings for Resource Resolution](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)」と「[Resources](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)」を参照してください。

## マッピング定義の表示 {#viewing-mapping-definitions}

マッピングでは 2 つのリストが作成されます。JCR リソースリゾルバーは、これらのリストを（トップダウン）評価して一致項目を探します。

これらのリストは、Felix コンソールの **JCR ResourceResolver** オプション（例：`https://<*host*>:<*port*>/system/console/jcrresolver`）で（設定情報と一緒に）確認できます。

* Configuration
（[Apache Sling Resource Resolver](/help/overview/seo-and-url-management.md#etc-map) 用に定義された）現在の設定を表示します。

* 設定テスト： URL またはリソースパスを入力できます。 「**解決**」または「**マップ**」をクリックして、システムによるエントリの変換方法を確認します。

* **Resolver Map Entries**
URL をリソースにマップするために ResourceResolver.resolve メソッドが使用するエントリのリストです。

* **Mapping Map Entries**
リソースパスを URL にマップするために ResourceResolver.map メソッドが使用するエントリのリストです。

2 つのリストには、アプリケーションでデフォルトとして定義されたエントリなど、様々なエントリが表示されます。これらのエントリは、多くの場合、ユーザーの URL を簡素化することを目的としています。

リストでは、**パターン**（リクエストに適合する正規表現）と&#x200B;**リプレースメント**（適用するリダイレクトを定義）がペアになっています。

例えば、次のようになります。

**パターン** `^[^/]+/[^/]+/welcome$`

以下をトリガーします。

**リプレースメント** `/libs/cq/core/content/welcome.html`.

以下のリクエストをリダイレクトします。

`https://localhost:4503/welcome` &grave;&grave;

次のようになります。

`https://localhost:4503/libs/cq/core/content/welcome.html`

新しいマッピング定義がリポジトリ内に作成されます。

>[!NOTE]
>
>正規表現の定義方法について説明したリソースは多数あります（例：[https://www.regular-expressions.info/](https://www.regular-expressions.info/)）。

### AEM でのマッピング定義の作成 {#creating-mapping-definitions-in-aem}

AEM の標準インストールには、次のフォルダーがあります。

`/etc/map/http`

このフォルダーは、HTTP プロトコル用のマッピングを定義する場合に使用する構造です。マッピングするその他のプロトコル用に別のフォルダー（`sling:Folder`）を `/etc/map` の下に作成できます。

#### /content への内部リダイレクトの設定 {#configuring-an-internal-redirect-to-content}

https://localhost:4503/ に対するリクエストに `/content` というプレフィックスを指定するマッピングを作成するには：

1. CRXDE を使用して `/etc/map/http` に移動します。

1. ノードの作成：

   * **タイプ**：`sling:Mapping`
これは目的のマッピング用のノードタイプですが、必須ではありません。

   * **名前** `localhost_any`

1. 「**すべて保存**」をクリックします。
1. **このノードに次のプロパティを追加します。**

   * **名前** `sling:match`

      * **型** `String`

      * **値** `localhost.4503/`

   * **名前** `sling:internalRedirect`

      * **型** `String`

      * **値** `/content/`

1. 「**すべて保存**」をクリックします。

このマッピングは、
`localhost:4503/geometrixx/en/products.html`
のようなリクエストを、
`localhost:4503/content/geometrixx/en/products.html`
がリクエストされたかのように処理します。

>[!NOTE]
>
>使用可能な sling のプロパティとその設定方法について詳しくは、Sling のドキュメントの[リソース](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)を参照してください。
>例えば、[文字列補間](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html#string-interpolation-for-etcmap)は、環境変数から環境ごとに値を取得するマッピングを設定できるので、便利です。

>[!NOTE]
>
>`/etc/map.publish` を使用して、パブリッシュ環境の設定を保持できます。これらの設定を複製して、パブリッシュ環境の [Apache Sling Resource Resolver](/help/overview/seo-and-url-management.md#etc-map) の&#x200B;**マッピング場所**&#x200B;用に、新しい場所（`/etc/map.publish`）を設定する必要があります。
