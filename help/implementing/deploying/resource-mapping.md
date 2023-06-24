---
title: リソースマッピング
description: リソースマッピングを使用して、AEMのリダイレクト、バニティー URL、仮想ホストを定義する方法について説明します。
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 1a1bb23c-d1d1-4e2b-811b-753e6a90a01b
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 54%

---

# リソースマッピング{#resource-mapping}

リソースマッピングは、AEMのリダイレクト、バニティー URL および仮想ホストを定義するために使用されます。

例えば、これらのマッピングを使用して、次のことをおこなうことができます。

* すべてのリクエストに `/content` というプレフィックスを付けて、web サイトの訪問者に内部構造が表示されないようにする。
* Web サイトの `/content/en/gateway` ページへのリクエストがすべて `https://gbiv.com/` にリダイレクトされるように、リダイレクトを定義する。

HTTP マッピングの一例として、`localhost:4503` に対するすべてのリクエストに `/content` というプレフィックスを指定します。このようなマッピングを使用すると、Web サイトの訪問者に対して内部構造を非表示にすることができます。例えば、次のページの場合は、

`localhost:4503/content/we-retail/en/products.html`

次を使用してアクセスする手順は、次のとおりです。

`localhost:4503/we-retail/en/products.html`

マッピングによってプレフィックスが自動的に追加されるので `/content` から `/we-retail/en/products.html`.

>[!CAUTION]
>
>バニティー URL は regex パターンをサポートしません。

>[!NOTE]
>
>詳しくは、Sling のドキュメントと「[Mappings for Resource Resolution](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)」と「[Resources](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)」を参照してください。

## マッピング定義の表示 {#viewing-mapping-definitions}

このマッピングは、JCR Resource Resolver が（トップダウン）評価して一致を見つける 2 つのリストを形成します。

これらのリストは、Felix コンソールの **JCR ResourceResolver** オプション（例：`https://<*host*>:<*port*>/system/console/jcrresolver`）で（設定情報と一緒に）確認できます。

* Configuration
（[Apache Sling Resource Resolver](/help/overview/seo-and-url-management.md#etc-map) 用に定義された）現在の設定を表示します。

* 設定テスト URL またはリソースパスを入力できます。 クリック **解決** または **マップ** をクリックして、エントリの変換方法を確認します。

* **Resolver Map Entries**
URL をリソースにマップするために ResourceResolver.resolve メソッドが使用するエントリのリストです。

* **Mapping Map Entries**
リソースパスを URL にマップするために ResourceResolver.map メソッドが使用するエントリのリストです。

2 つのリストには、アプリケーションでデフォルトとして定義されたエントリを含む、様々なエントリが表示されます。 これらのエントリは、多くの場合、ユーザーの URL を簡素化することを目的としています。

リストはペア a **パターン**&#x200B;の場合は、リクエストに一致する正規表現と **代替手段** これは、適用するリダイレクトを定義します。

例えば、次のような場合です。

**パターン** `^[^/]+/[^/]+/welcome$`

トリガー:

**リプレースメント** `/libs/cq/core/content/welcome.html`.

リクエストをリダイレクトするには：

`https://localhost:4503/welcome` ``

To:

`https://localhost:4503/libs/cq/core/content/welcome.html`

新しいマッピング定義がリポジトリ内に作成されます。

>[!NOTE]
>
>正規表現の定義方法を説明するリソースが多数あります。例： [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### AEMでのマッピング定義の作成 {#creating-mapping-definitions-in-aem}

AEMの標準インストールでは、次のフォルダーを検索できます。

`/etc/map/http`

このフォルダーは、HTTP プロトコルのマッピングを定義する際に使用される構造です。 マッピングするその他のプロトコル用に別のフォルダー（`sling:Folder`）を `/etc/map` の下に作成できます。

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

このマッピングは、次のような要求を処理します。
`localhost:4503/geometrixx/en/products.html`
次のように：
`localhost:4503/content/geometrixx/en/products.html`
がリクエストされました。

>[!NOTE]
>
>使用可能な sling のプロパティとその設定方法について詳しくは、Sling のドキュメントの「[Resources](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)」を参照してください。
>例： [文字列補間](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html#string-interpolation-for-etcmap) は、環境変数を使用して環境値ごとに取得するマッピングを設定できるので便利です。

>[!NOTE]
>
>`/etc/map.publish` を使用して、パブリッシュ環境の設定を保持する。これらの設定は、新しい場所 ( `/etc/map.publish`) が **マッピング場所** の [Apache Sling Resource Resolver](/help/overview/seo-and-url-management.md#etc-map) パブリッシュ環境の
