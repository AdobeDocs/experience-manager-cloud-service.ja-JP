---
title: クラウドサービスとしてのAdobe Experience ManagerのSEOおよびURL管理のベストプラクティス
seo-title: クラウドサービスとしてのAdobe Experience ManagerのSEOおよびURL管理のベストプラクティス
translation-type: tm+mt
source-git-commit: 70e76205e82b491fa77f65cd4257a79dda17b882

---


# クラウドサービスとしてのAdobe Experience ManagerのSEOおよびURL管理のベストプラクティス{#seo-and-url-management-best-practices-for-aem}

検索エンジン最適化（SEO）は、多くのマーケティング担当者にとって重要な課題となっています。その結果、クラウドサービスプロジェクトとして、多くのAdobe Experience Manager(AEM)でSEOの懸念に対処する必要があります。

This document first describes some [SEO best practices](#seo-best-practices) and recommendations for achieving these on an AEM as a Cloud Service implementation. その次に、最初の節で提示するより[複雑な実装手順](#aem-configurations)のいくつかについて詳しく説明していきます。

## SEO のベストプラクティス {#seo-best-practices}

ここでは、SEO の一般的なベストプラクティスを説明します。

### URL {#urls}

URL に関して一般的に認められているベストプラクティスがいくつかあります。

AEM プロジェクトで URL を評価するときには、次のことを確認してください。

「ユーザーが URL を目にしたときに、ページのコンテンツを見なくても、そのページの内容を説明できますか。」

答えが「はい」であれば、その URL は検索エンジンに効果があります。

SEO に対応した URL を作成する方法について、一般的なヒントを紹介します。

* ハイフンを使用して単語を区切ります。

   * ページに名前を付けるときには、ハイフン（-）を区切り文字として使用します。
   * キャメルケース（単語の先頭を大文字で表記する）、アンダースコアおよびスペースの使用は避けます。

* 可能な場合、クエリーパラメーターの使用は避けます。必要な場合は、パラメーターを 2 つ以下に制限してください。

   * 使用可能な場合、ディレクトリ構造を使用して情報アーキテクチャを示します。
   * ディレクトリ構造を使用できない場合は、クエリー文字列の代わりに、Sling セレクターを URL で使用します。Sling セレクターを使用すると、提供される SEO 値に加えて、ディスパッチャーでページをキャッシュできるようになります。

* ユーザーにとって URL がわかりやすいほど、効果的です。URL にキーワードを含めると、価値が高まります。

   * ページでセレクターを使用する場合、セマンティック値を提供するセレクターが推奨されます。
   * ユーザーが理解できない URL は、検索エンジンでも理解できません。
   * 次に例を示します。
      `mybrand.com/products/product-detail.product-category.product-name.html`
の方が望ましい `mybrand.com/products/product-detail.1234.html`

* 検索エンジンではサブドメインは異なるエンティティとして扱われ、サイトの SEO 値が分断されるので、可能な限りサブドメインの使用は避けます。

   * 代わりに、第 1 レベルのサブパスを使用します。For example, instead of `es.mybrand.com/home.html`, use `www.mybrand.com/es/home.html`.

   * このガイドラインに従って、コンテンツの表示形態に合うようにコンテンツ階層を計画します。

* URL が長く、キーワードの位置が後ろになるほど、URL におけるキーワードの効果は低下します。つまり、短いほど効果的です。

   * AEM で提供されている URL 短縮の手法や機能を使用して、不要な URL 部分を削除します。
   * 例えば、を `mybrand.com/en/myPage.html` 選択します `mybrand.com/content/my-brand/en/myPage.html`。

* 正規 URL を使用します。

   * When a URL can be served from different paths or with different parameters or selectors, make sure to use a `rel=canonical` tag on the page.

   * このタグを AEM テンプレートのコードに組み込むこともできます。

* 可能な限り、URL をページのタイトルに合わせます。

   * コンテンツの作成者に対して、この手法に従うよう勧めてください。

* URL 要求で大文字と小文字を区別しない動作をサポートします。

   * すべての受信要求を小文字として書き換えるようにディスパッチャーを設定します。
   * 小文字を使用してすべてのページを作成するようコンテンツの作成者をトレーニングします。

* 各ページが 1 つのプロトコルから提供されるようにします。

   * サイトが `http` 経由で提供され、ユーザーがチェックアウトまたはログインフォームを使用してページに到達した時点で、`https` に切り替わることがあります。このページからリンクするときに、ユーザーが `http` ページに戻り、`https` 経由でそれらのページにアクセスできる場合、検索エンジンでは、2 つの異なるページとして追跡されます。

   * Google currently prefers `https` pages to `http` ones. こうした理由から、多くの場合、サイト全体を `https` 経由で提供する方が便利です。

### サーバーの設定 {#server-configuration}

サーバーの設定に関しては、次の手段を講じることで、適切なコンテンツのみがクロールされるようにすることができます。

* Use a `robots.txt` file to block crawling of any content that should not be indexed.

   * テスト環境では&#x200B;**すべての**&#x200B;クローリングをブロックします。

* 更新した URL を使用して新しいサイトの運用を開始する場合は、既存の SEO ランキングが失われないように 301 リダイレクトを実装します。
* サイトの favicon を挿入します。
* 検索エンジンでコンテンツが容易にクロールされるように XML サイトマップを実装します。モバイルサイトやレスポンシブサイトの場合は、必ずモバイルサイトマップを組み込んでください。

## AEM の設定 {#aem-configurations}

ここでは、SEO に関する前述の推奨事項に従って AEM を設定するために必要な実装手順を説明します。

### Sling セレクターの使用 {#using-sling-selectors}

これまで、エンタープライズ Web アプリケーションを構築する場合、クエリーパラメーターを使用するのが一般的に認められた手法でした。

近年は、URL をよりわかりやすくするために、クエリーパラメーターを削除する傾向にあります。多くのプラットフォームでは、Web サーバーやコンテンツ配信ネットワーク（CDN）へのリダイレクトの実装などが行われますが、Sling を使用すると簡単です。Sling セレクターの特長は次のとおりです。

* URL のわかりやすさが向上します。
* ディスパッチャーでページをキャッシュでき、多くの場合、セキュリティが強化されます。
* 汎用サーブレットを使用してコンテンツを取得する代わりに、コンテンツを直接アドレス指定できます。これにより、リポジトリに適用する ACL や、ディスパッチャーで適用するフィルターを活用できます。

#### サーブレットでのセレクターの使用 {#using-selectors-for-servlets}

AEM では、サーブレットを作成するときに次の 2 つのオプションが用意されています。

* **bin** サーブレット
* **Sling** サーブレット

次に示す各例では、この両方のパターンに準拠したサーブレットを登録する方法とともに、Sling サーブレットを使用することによって得られる利点を説明します。

#### bin サーブレット（1 レベル下） {#bin-servlets-one-level-down}

**bin** サーブレットは、多くの開発者が使い慣れている J2EE プログラミングのパターンに準拠しています。The servlet is registered at a specific path, which in the case of AEM is usually under `/bin`, and you extract the needed request parameters from the query string.

このタイプのサーブレットの SCR 注釈は、次のようになります。

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

続いて、`SlingHttpServletRequest` メソッドに含まれる `doGet` オブジェクトを使用して、クエリー文字列からパラメーターを抽出します。次に例を示します。

```
String myParam = req.getParameter("myParam");
```

使用される結果の URL は次のようになります。

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

このアプローチで考慮すべき点は次のとおりです。

* URL 自体から SEO 値が失われます。URL は、コンテンツ階層ではなく、プログラムにおけるパスを表すので、検索エンジンを含め、サイトにアクセスするユーザーが URL からセマンティック値を受け取ることはありません。
* URL にクエリーパラメーターが含まれていることは、ディスパッチャーで応答をキャッシュできないことを意味します。
* このサーブレットを保護するには、独自のカスタムセキュリティロジックをサーブレットに実装する必要があります。
* The dispatcher must be configured (carefully) to expose `/bin/myApp/myServlet`. Simply exposing `/bin` would allow access to certain servlets that should not be open to site visitors.

#### Sling servlets (one level down) {#sling-servlets-one-level-down}

**Sling** サーブレットを使用すると、逆の方法でサーブレットを登録できます。サーブレットをアドレス指定し、クエリーパラメーターに基づいてサーブレットでレンダリングするコンテンツを指定するのではなく、目的のコンテンツをアドレス指定し、Sling セレクターに基づいてコンテンツをレンダリングするサーブレットを指定します。

このタイプのサーブレットの SCR 注釈は、次のようになります。

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json”, methods=”GET”)
```

この場合、URL によってアドレス指定されるリソース（`myPageType` リソースのインスタンス）にサーブレットで自動的にアクセスできます。アクセスするには、次のメソッドを呼び出します。

```
Resource myPage = req.getResource();
```

使用される結果の URL は次のようになります。

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

このアプローチの利点は次のとおりです。

* サイト階層およびページ名に存在するセマンティックによって得られた SEO 値でベイクできます。
* クエリーパラメーターがないので、ディスパッチャーで応答をキャッシュできます。さらに、アドレス指定されたページが更新されていると、ページがアクティベートされたときに、そのキャッシュは無効になります。
* All ACLs applied to `/content/my-brand/my-page` will come into effect when a user tries to access this servlet.
* ディスパッチャーは、Web サイトを提供する機能の 1 つとしてこのコンテンツを提供するようにあらかじめ設定されます。追加の設定は必要ありません。

### URL の書き換え {#url-rewriting}

In AEM, all of your web pages are stored under `/content/my-brand/my-content`. これは、リポジトリデータ管理の観点では便利な場合がありますが、必ずしもこの方法で顧客にサイトを表示するわけではなく、URL をできるだけ短くするという SEO のガイダンスと矛盾する可能性があります。また、同じAEMインスタンスと異なるドメイン名から複数のWebサイトを提供する場合もあります。

ここでは、これらの URL を管理し、よりわかりやすく、SEO に適した方法で URL をユーザーに表示するために AEM で使用可能なオプションを検討します。

#### バニティー URL {#vanity-urls}

作成者が、プロモーション目的で別の場所からアクセス可能なページを作成する場合、ページごとに定義される AEM のバニティー URL が役立つことがあります。To add a vanity URL for a page, navigate to it in the **Sites** console and edit the page properties. At the bottom of the **Basic** tab, you see a section where vanity URLs can be added. 複数のURLを介してページにアクセスできるようにすると、ページのSEO値がフラグメント化されるので、この問題を回避するために、正規のURLタグをページに追加する必要があります。

#### ページ名のローカライズ {#localized-page-names}

翻訳されたコンテンツのユーザーに、ローカライズしたページ名を表示できます。次に例を示します。

* スペイン語を話すユーザーが次の場所に移動する代わりに、
   `www.mydomain.com/es/home.html`

* URLは次のようにする方が良いでしょう。
   `www.mydomain.com/es/casa.html` です。

ページ名のローカライズに伴う課題は、AEM プラットフォームで使用可能なローカリゼーションツールの多くでは、コンテンツを同期しておくためには、ロケール間でページ名を一致させる必要があるという点です。

`sling:alias` プロパティを使用すると、両方を同時に実現できます。`sling:alias` を任意のリソースにプロパティとして追加すると、リソースのエイリアス名を使用することができます。前述の例では、次のようになります。

* JCRの次のページ
   `…/es/home`

* 次に、プロパティを追加します。
   `sling:alias` = `casa`

これにより、マルチサイトマネージャーなどの AEM 翻訳ツールでは、次のページ間の関係を引き続き維持できます。

* `/en/home`

* `/es/home`

また、エンドユーザーもページ名を母国語で操作できます。

>[!NOTE]
>
>このプロ `sling:alias` パティは、ページプロパティの編集時に [Aliasプロパティを使用して設定できます](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced)。

#### /etc/map {#etc-map}

標準 AEM インストールでは、

* （OSGi設定用）
   **Apache Sling Resource Resolver Factory**
( `org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* 財産
   **マッピング場所** ( `resource.resolver.map.location`)

* defaults to `/etc/map`.

AEM で受信要求のマッピングまたはページ上の URL の書き換え、あるいはその両方をおこなうために、この場所にマッピング定義を追加できます。

To create a new mapping, create a new `sling:Mapping` node in this location under `/http` or `/https`. Based on the `sling:match` and `sling:internalRedirect` properties that are set on this node, AEM will redirect all traffic for the matched URL to the value specified in the `internalRedirect` property.

これは、AEM および Sling の正式なドキュメントに記載されているアプローチですが、この実装で提供される正規表現のサポートは、`SlingResourceResolver` を直接使用することによって利用可能なオプションと比べると、範囲が限られています。また、この方法でマッピングを実装すると、ディスパッチャーのキャッシュの無効化に関する問題が生じることがあります。

次に、この問題がどのように生じるかについて例を示します。

1. A user visits your website and requests `https://www.mydomain.com/my-page.html`
1. ディスパッチャーが、この要求を公開サーバーに転送します。
1. Using `/etc/map`, the publish server resolves this request to `/content/my-brand/my-page` and renders the page.

1. The dispatcher caches the response at `/my-page.html` and returns the response to the user.
1. コンテンツの作成者がこのページを変更し、アクティベートします。
1. The dispatcher flush agent sends an invalidation request for `/content/my-brand/my-page`**.**ディスパッチャーにはこのパスにページがキャッシュされていないので、古いコンテンツはキャッシュされたままで、古くなります。

キャッシュの無効化を目的として、短い URL を長い URL にマッピングするカスタムのディスパッチフラッシュルールを設定する方法があります。

ただし、より簡単にこれを管理する方法もあります。

1. **SlingResourceResolver ルール**

   Web コンソール（localhost:4502/system/console/configMgr など）を使用して、Sling Resource Resolver を設定できます。

   * **Apache Sling Resource Resolver Factory**
      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)` です。
   URL を短縮するために必要なマッピングを正規表現として構築した後、ビルドに含まれている OsgiConfignode の `config.publish` でこれらの設定を定義することをお勧めします。

   Rather than defining your mappings in `/etc/map`, they can be assigned directly to the property **URL Mappings** ( `resource.resolver.mapping`):

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   In this simple example, you are removing `/content/my-brand/` from the beginning of any URL where it is present.

   これにより、URL は次のように変換されます。

   * 追加の `/content/my-brand/my-page.html`
   * ただ `/my-page.html`
   これは、URL をできるだけ短く維持するという推奨事項に準拠しています。

1. **ページに出力される URL のマッピング**

   Apache Sling Resource Resolver でマッピングを定義したら、ページに出力する URL が短く、適切になるように、それらのマッピングをコンポーネントで使用する必要があります。You can do this by using the map function of the `ResourceResolver`.

   例えば、現在のページの子をリストするカスタムナビゲーションコンポーネントを実装する場合、次のようなマッピングメソッドを使用できます。

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server の mod_rewrite {#apache-http-server-mod-rewrite}

これまでは、ページにURLを出力する際に、これらのマッピングを使用するように、コンポーネント内のロジックと共にマッピングを実装してきました。

最後の手順は、短縮された URL のディスパッチャーでの処理です。ここでは、`mod_rewrite` を使用します。`mod_rewrite` を使用する最大の利点は、URL が、ディスパッチャーモジュールに送信される前に長い形式に再びマッピングされる点です。**&#x200B;つまり、ディスパッチャーは公開サーバーに長い URL を要求し、それに応じて URL をキャッシュします。したがって、公開サーバーからのディスパッチャーフラッシュ要求により、そのコンテンツを正常に無効にすることができます。

このようなルールを実装するには、Apache HTTP Server の設定で仮想ホストに `RewriteRule` 要素を追加します。前述の例の短縮された URL を拡張する場合は、次のようなルールを実装できます。

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### 正規 URL タグ {#canonical-url-tags}

正規 URL タグは、コンテンツのインデックスを作成するときに検索エンジンでページをどのように処理する必要があるかを明確化するために、HTML ドキュメントの先頭に配置されるリンクタグです。このタグを使用すると、ページの URL に異なる部分が含まれていても、同じものとしてページ（の様々なバージョン）のインデックスが作成されるという利点があります。

例えば、ページのプリンターフレンドリーなバージョンをサイトで提供する場合、検索エンジンでは、通常のバージョンのページとは別に、このページのインデックスが作成される可能性があります。正規タグを使用すると、同じページであることが検索エンジンで認識されます。

例：

* https://www.mydomain.com/my-brand/my-page.html
* https://www.mydomain.com/my-brand/my-page.print.html

両方について、ページの先頭に次のタグを適用します。

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

`href` は、相対パスとして指定することも、絶対パスとして指定することもできます。ページの正規URLを決定し、このタグを出力するには、ページのマークアップにコードを含める必要があります。

### 大文字と小文字を区別しないためのディスパッチャーの設定 {#configuring-the-dispatcher-for-case-insensitivity}

最善の方法は、小文字を使用してすべてのページを提供することです。ただし、ユーザーが URL に大文字を使用して Web サイトにアクセスしたときに、404 エラーが表示されるのは望ましくありません。このため、アドビでは、Apache HTTP Server設定に書き換えルールを追加して、受信するすべてのURLを小文字にマップすることをお勧めします。 さらに、小文字の名前を使用してページを作成するようコンテンツの作成者をトレーニングする必要があります。

すべての受信トラフィックを強制的に小文字に変換するように Apache を設定するには、次のコードを `vhost` の設定に追加します。

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

さらに、次のコードを `htaccess` ファイルの最上部に追加します。

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### 開発環境を保護するための robots.txt の実装 {#implementing-robots-txt-to-protect-development-environments}

検索エンジンでは、サイトをクロールする前に、サイトのルートに *ファイルがあるかどうかがチェックされる*`robots.txt`はずです。Google、Yahoo、Bingなどの主要検索エンジンはこれをすべて重視しているのに対し、一部の外国語検索エンジンはこの点を重視していないので、ここではShouldを強調する必要があります。

サイト全体へのアクセスをブロックするための最も簡単な方法は、`robots.txt` というファイルに次の内容を指定して、サイトのルートに配置することです。

```xml
User-agent: *
Disallow: /
```

また、実稼働環境では、インデックスが作成されないように特定のパスを禁止することもできます。

The caveat with placing the `robots.txt` file at the site root is that dispatcher flush requests may clear this file out and URL mappings will likely place the site root somewhere different than the `DOCROOT` as defined in the Apache HTTP Server configuration. こうした理由から、このファイルをオーサーインスタンスのサイトのルートに配置し、パブリッシュインスタンスにレプリケートするのが一般的です。

### AEM での XML サイトマップの作成 {#building-an-xml-sitemap-on-aem}

クローラーでは、Web サイトの構造をより的確に把握するために XML サイトマップが使用されます。サイトマップを提供すれば SEO ランキングが上がるという保証はありませんが、ベストプラクティスの 1 つとして認められています。サイトマップとして使用する XML ファイルを Web サーバーで手動で管理することもできますが、作成者が新しいコンテンツを作成すると、変更内容がサイトマップに自動的に反映されるように、プログラムによってサイトマップを生成することをお勧めします。

プログラムによってサイトマップを生成するには、`sitemap.xml` の呼び出しをリスンする Sling サーブレットを登録します。このサーブレットは、サーブレット API によって提供されるリソースを使用して、現在のページおよびその子を確認し、XML を出力します。XML はその後、ディスパッチャーでキャッシュされます。`robots.txt` ファイルのサイトマッププロパティで、この場所を参照する必要があります。さらに、新しいページがアクティベートされたときには必ず、このファイルがフラッシュされるように、カスタムフラッシュルールを実装する必要があります。

>[!NOTE]
>
>You can register a Sling Servlet to listen for the selector `sitemap` with the extension `xml`. これにより、次のURLで終わるURLが要求された場合に、サーブレットが要求を処理するようになります。
>    `/<path-to>/page.sitemap.xml`
その後、要求されたリソースをリクエストから取得し、JCR API を使用してコンテンツツリーのその地点からサイトマップを生成できます。
このようなアプローチは、複数のサイトを同じインスタンスから処理している場合にメリットがあります。A request to `/content/siteA.sitemap.xml` would generate a sitemap for `siteA` while a request for `/content/siteB.sitemap.xml` would generate a sitemap for `siteB` without the need for writing additional code.

### レガシー URL の 301 リダイレクトの作成 {#creating-redirects-for-legacy-urls}

新しい構造でサイトを起動する場合、Apache HTTP Serverに301リダイレクトを実装し、テストすることが重要です。理由は次の2つです。

* レガシー URL では、時間の経過とともに SEO 値が上がっています。リダイレクトを実装すると、検索エンジンでは、この値を新しい URL に適用できます。
* サイトのユーザーが、それらのページへのブックマークを作成している場合があります。リダイレクトを実装すると、古いサイトでアクセスしようとしていたページに最も近い、新しいサイトのページにユーザーがリダイレクトされるようにすることができます。

301 リダイレクトの実装に関する説明や、リダイレクトが正しく機能していることをテストするためのツールについては、次のその他のリソースの節を参照してください。

## その他のリソース {#additional-resources}

詳しくは、以下のその他のリソースを参照してください。

<!--
* [Resource Mapping](/help/sites-deploying/resource-mapping.md)
-->

* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/](https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)
