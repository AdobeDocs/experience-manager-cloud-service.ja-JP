---
title: Adobe Experience Manager as a Cloud Service の SEO および URL 管理のベストプラクティス
seo-title: Adobe Experience Manager as a Cloud Service の SEO および URL 管理のベストプラクティス
translation-type: tm+mt
source-git-commit: c8759ba41813a891664c1cf2d12eaeddbd4aabeb
workflow-type: tm+mt
source-wordcount: '3124'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service の SEO および URL 管理のベストプラクティス{#seo-and-url-management-best-practices-for-aem}

検索エンジン最適化（SEO）は、多くのマーケティング担当者にとって重要な課題となっています。その結果、多くの Adobe Experience Manager (AEM) as a Cloud Service プロジェクトで SEO の懸念に対処する必要があります。

このドキュメントでは、まず、AEM as a Cloud Service の実装でこうした目的を達成するための [SEO のベストプラクティス](#seo-best-practices)および推奨事項を説明します。その次に、最初の節で提示するより[複雑な実装手順](#aem-configurations)のいくつかについて詳しく説明していきます。

## SEO のベストプラクティス  {#seo-best-practices}

ここでは、SEO の一般的なベストプラクティスを説明します。

### URL  {#urls}

URL に関して一般的に認められているベストプラクティスがいくつかあります。

AEM プロジェクトで URL を評価するときには、次のことを確認してください。

*「ユーザーが URL を目にしたときに、ページのコンテンツを見なくても、そのページの内容を説明できますか。」*

答えが「はい」であれば、その URL は検索エンジンに効果があります。

SEO に対応した URL を作成する方法について、一般的なヒントを紹介します。

* ハイフンを使用して単語を区切ります。

   * ページに名前を付けるときには、ハイフン（-）を区切り文字として使用します。
   * キャメルケース（単語の先頭を大文字で表記する）、アンダースコアおよびスペースの使用は避けます。

* 可能な場合、クエリーパラメーターの使用は避けます。必要な場合は、パラメーターを 2 つ以下に制限してください。

   * 使用可能な場合、ディレクトリ構造を使用して情報アーキテクチャを示します。
   * ディレクトリ構造を使用できない場合は、クエリー文字列の代わりに、Sling セレクターを URL で使用します。Sling セレクターを使用すると、提供される SEO 値に加えて、Dispatcher でページをキャッシュできるようになります。

* ユーザーにとって URL がわかりやすいほど、効果的です。URL にキーワードを含めると、価値が高まります。

   * ページでセレクターを使用する場合、セマンティック値を提供するセレクターが推奨されます。
   * ユーザーが理解できない URL は、検索エンジンでも理解できません。
   * 次に例を示します。
      `mybrand.com/products/product-detail.product-category.product-name.html`
の方が  より望ましい 
`mybrand.com/products/product-detail.1234.html`

* 検索エンジンではサブドメインは異なるエンティティとして扱われ、サイトの SEO 値が分断されるので、可能な限りサブドメインの使用は避けます。

   * 代わりに、第 1 レベルのサブパスを使用します。例えば、`es.mybrand.com/home.html` の代わりに、`www.mybrand.com/es/home.html` を使用します。

   * このガイドラインに従って、コンテンツの表示形態に合うようにコンテンツ階層を計画します。

* URL が長く、キーワードの位置が後ろになるほど、URL におけるキーワードの効果は低下します。つまり、短いほど効果的です。

   * AEM で提供されている URL 短縮の手法や機能を使用して、不要な URL 部分を削除します。
   * 例えば、`mybrand.com/content/my-brand/en/myPage.html` より `mybrand.com/en/myPage.html` を選択します。

* 正規 URL を使用します。

   * 複数のパスから、または複数のパラメーターやセレクターで 1 つの URL を提供できない場合は必ず、ページで `rel=canonical` タグを使用します。

   * このタグを AEM テンプレートのコードに組み込むこともできます。

* 可能な限り、URL をページのタイトルに合わせます。

   * コンテンツの作成者に対して、この手法に従うよう勧めてください。

* URL 要求で大文字と小文字を区別しない動作をサポートします。

   * すべての受信要求を小文字として書き換えるように Dispatcher を設定します。
   * 小文字を使用してすべてのページを作成するようコンテンツの作成者をトレーニングします。

* 各ページが 1 つのプロトコルから提供されるようにします。

   * サイトが `http` 経由で提供され、ユーザーがチェックアウトまたはログインフォームを使用してページに到達した時点で、`https` に切り替わることがあります。このページからリンクするときに、ユーザーが `http` ページに戻り、`https` 経由でそれらのページにアクセスできる場合、検索エンジンでは、2 つの異なるページとして追跡されます。

   * Google では現在、`https` ページの方が `http` ページよりも推奨されています。こうした理由から、多くの場合、サイト全体を `https` 経由で提供する方が便利です。

### サーバーの設定 {#server-configuration}

サーバーの設定に関しては、次の手段を講じることで、適切なコンテンツのみがクロールされるようにすることができます。

* `robots.txt` ファイルを使用して、インデックスを作成する必要がないコンテンツのクローリングをブロックします。

   * テスト環境では&#x200B;**すべての**&#x200B;クローリングをブロックします。

* 更新した URL を使用して新しいサイトの運用を開始する場合は、既存の SEO ランキングが失われないように 301 リダイレクトを実装します。
* サイトの favicon を挿入します。
* 検索エンジンでコンテンツが容易にクロールされるように XML サイトマップを実装します。モバイルサイトやレスポンシブサイトの場合は、必ずモバイルサイトマップを組み込んでください。

## AEM の設定 {#aem-configurations}

ここでは、SEO に関する前述の推奨事項に従って AEM を設定するために必要な実装手順を説明します。

### Sling セレクターの使用 {#using-sling-selectors}

これまで、エンタープライズ Web アプリケーションを構築する場合、クエリーパラメーターを使用するのが一般的に認められた手法でした。

近年は、URL をよりわかりやすくするために、クエリーパラメーターを削除する傾向にあります。多くのプラットフォームでは、Web サーバーやコンテンツ配信ネットワーク（CDN）へのリダイレクトの実装などがおこなわれますが、Sling を使用すると簡単です。Sling セレクターの特長は次のとおりです。

* URL のわかりやすさが向上します。
* Dispatcher でページをキャッシュでき、多くの場合、セキュリティが強化されます。
* 汎用サーブレットを使用してコンテンツを取得する代わりに、コンテンツを直接アドレス指定できます。これにより、リポジトリに適用する ACL や、ディスパッチャーで適用するフィルターを活用できます。

#### サーブレットでのセレクターの使用  {#using-selectors-for-servlets}

AEM では、サーブレットを作成するときに次の 2 つのオプションが用意されています。

* **bin** サーブレット
* **Sling** サーブレット

次に示す各例では、この両方のパターンに準拠したサーブレットを登録する方法とともに、Sling サーブレットを使用することによって得られる利点を説明します。

#### bin サーブレット（1 レベル下）  {#bin-servlets-one-level-down}

**bin** サーブレットは、多くの開発者が使い慣れている J2EE プログラミングのパターンに準拠しています。このサーブレットは、特定のパスに登録されます。AEM の場合は通常 `/bin` に登録され、必要な要求パラメーターをクエリー文字列から抽出します。

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
* URL にクエリーパラメーターが含まれていることは、Dispatcher で応答をキャッシュできないことを意味します。
* このサーブレットを保護するには、独自のカスタムセキュリティロジックをサーブレットに実装する必要があります。
* `/bin/myApp/myServlet` を公開するように Dispatcher を（慎重に）設定する必要があります。単に `/bin` を公開すると、サイト訪問者に公開してはいけない特定のサーブレットへのアクセスが許可されます。

#### Sling サーブレット（1 レベル下）{#sling-servlets-one-level-down}

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
* クエリーパラメーターがないので、Dispatcher で応答をキャッシュできます。さらに、アドレス指定されたページが更新されていると、ページがアクティベートされたときに、そのキャッシュは無効になります。
* ユーザーがこのサーブレットにアクセスしようとすると、`/content/my-brand/my-page` に適用されているすべての ACL が有効になります。
* Dispatcher は、Web サイトを提供する機能の 1 つとしてこのコンテンツを提供するようにあらかじめ設定されます。追加の設定は必要ありません。

### URL の書き換え {#url-rewriting}

AEM では、すべての Web ページが `/content/my-brand/my-content` に保存されます。これは、リポジトリデータ管理の観点では便利な場合がありますが、必ずしもこの方法で顧客にサイトを表示するわけではなく、URL をできるだけ短くするという SEO のガイダンスと矛盾する可能性があります。さらに、同じ AEM インスタンスや異なるドメイン名から複数の Web サイトを提供している場合もあります。

ここでは、これらの URL を管理し、よりわかりやすく、SEO に適した方法で URL をユーザーに表示するために AEM で使用可能なオプションを検討します。

#### バニティー URL  {#vanity-urls}

作成者が、プロモーション目的で別の場所からアクセス可能なページを作成する場合、ページごとに定義される AEM のバニティー URL が役立つことがあります。ページのバニティー URL を追加するには、**Sites** コンソールで該当するページに移動し、ページのプロパティを編集します。「**基本**」タブの下部に、バニティー URL を追加できるセクションが表示されます。複数の URL を使用してページにアクセスできるようにすると、ページの SEO 値が分断されるので、正規 URL タグをページに追加して、この問題を回避する必要があることに留意してください。

#### ページ名のローカライズ {#localized-page-names}

翻訳されたコンテンツのユーザーに、ローカライズしたページ名を表示できます。次に例を示します。

* スペイン語を話すユーザーが次のページにアクセスするとします。
   `www.mydomain.com/es/home.html`

* この場合、URL を次のように表示した方が効果的です。
   `www.mydomain.com/es/casa.html`.

ページ名のローカライズに伴う課題は、AEM プラットフォームで使用可能なローカリゼーションツールの多くでは、コンテンツを同期しておくためには、ロケール間でページ名を一致させる必要があるという点です。

`sling:alias` プロパティを使用すると、両方を同時に実現できます。`sling:alias` を任意のリソースにプロパティとして追加すると、リソースのエイリアス名を使用することができます。前述の例では、次のようになります。

* JCR の次の場所にページがあるとします。
   `…/es/home`

* プロパティを追加します。
   `sling:alias` = `casa`

これにより、マルチサイトマネージャーなどの AEM 翻訳ツールでは、次のページ間の関係を引き続き維持できます。

* `/en/home`

* `/es/home`

また、エンドユーザーもページ名を母国語で操作できます。

>[!NOTE]
>
>`sling:alias` プロパティは、[ページプロパティ編集時のエイリアスプロパティ](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced)を使用して設定できます。

#### /etc/map {#etc-map}

標準 AEM インストールでは、

* OSGi 設定には
   **Apache Sling Resource Resolver Factory**
( 
`org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* プロパティ
   **マッピング場所**（`resource.resolver.map.location`）

* デフォルト `/etc/map` に設定。

AEM で受信要求のマッピングまたはページ上の URL の書き換え、あるいはその両方をおこなうために、この場所にマッピング定義を追加できます。

新しいマッピングを作成するには、この場所の `sling:Mapping` または `/http` の下に新しい `/https` ノードを作成します。このノードで設定された `sling:match` および `sling:internalRedirect` プロパティに基づいて、AEM は、一致した URL のすべてのトラフィックを `internalRedirect` プロパティで指定された値にリダイレクトします。

これは、AEM および Sling の正式なドキュメントに記載されているアプローチですが、この実装で提供される正規表現のサポートは、`SlingResourceResolver` を直接使用することによって利用可能なオプションと比べると、範囲が限られています。また、この方法でマッピングを実装すると、Dispatcher のキャッシュの無効化に関する問題が生じることがあります。

次に、この問題がどのように生じるかについて例を示します。

1. ユーザーが Web サイトを訪問し、`https://www.mydomain.com/my-page.html` を要求します。
1. Dispatcher が、この要求を公開サーバーに転送します。
1. 公開サーバーが `/etc/map` を使用して、この要求を `/content/my-brand/my-page` に解決し、ページをレンダリングします。

1. Dispatcher が `/my-page.html` に応答をキャッシュし、応答をユーザーに返します。
1. コンテンツの作成者がこのページを変更し、アクティベートします。
1. Dispatcher フラッシュエージェントが `/content/my-brand/my-page`**の無効化要求を送信します。** Dispatcher はこのパスにページをキャッシュしていないので、古いコンテンツがキャッシュされたままになり、更新されません。

キャッシュの無効化を目的として、短い URL を長い URL にマッピングするカスタムのディスパッチフラッシュルールを設定する方法があります。

ただし、より簡単にこれを管理する方法もあります。

1. **SlingResourceResolver ルール**

   Web コンソール（localhost:4502/system/console/configMgr など）を使用して、Sling Resource Resolver を設定できます。

   * **Apache Sling Resource Resolver Factory**

      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.
   URL を短縮するために必要なマッピングを正規表現として構築した後、ビルドに含まれている OsgiConfignode の `config.publish` でこれらの設定を定義することをお勧めします。

   `/etc/map`マッピングを定義する代わりに、プロパティ **URL Mappings**（`resource.resolver.mapping`）に直接割り当てることができます。

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   この簡単な例では、URL に `/content/my-brand/` が存在する場合、URL の先頭から削除されます。

   これにより、URL は次のように変換されます。

   * `/content/my-brand/my-page.html` から
   * ただの `/my-page.html`

   これは、URL をできるだけ短く維持するという推奨事項に準拠しています。

1. **ページに出力される URL のマッピング**

   Apache Sling Resource Resolver でマッピングを定義したら、ページに出力する URL が短く、適切になるように、それらのマッピングをコンポーネントで使用する必要があります。そのためには、`ResourceResolver` のマッピング関数を使用します。

   例えば、現在のページの子をリストするカスタムナビゲーションコンポーネントを実装する場合、次のようなマッピングメソッドを使用できます。

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server の mod_rewrite  {#apache-http-server-mod-rewrite}

これまでに、URL をページに出力するときに、定義したマッピングを使用するために、マッピングをロジックとともにコンポーネントに実装しました。

最後の手順は、短縮された URL の Dispatcher での処理です。ここでは、`mod_rewrite` を使用します。`mod_rewrite` を使用する最大の利点は、URL が、Dispatcher モジュールに送信される前に長い形式に再びマッピングされる点です。**&#x200B;つまり、Dispatcher は公開サーバーに長い URL を要求し、それに応じて URL をキャッシュします。したがって、公開サーバーからの Dispatcher フラッシュ要求により、そのコンテンツを正常に無効にすることができます。

このようなルールを実装するには、Apache HTTP Server の設定で仮想ホストに `RewriteRule` 要素を追加します。前述の例の短縮された URL を拡張する場合は、次のようなルールを実装できます。

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### 正規 URL タグ  {#canonical-url-tags}

正規 URL タグは、コンテンツのインデックスを作成するときに検索エンジンでページをどのように処理する必要があるかを明確化するために、HTML ドキュメントの先頭に配置されるリンクタグです。このタグを使用すると、ページの URL に異なる部分が含まれていても、同じものとしてページ（の様々なバージョン）のインデックスが作成されるという利点があります。

例えば、ページのプリンターフレンドリーなバージョンをサイトで提供する場合、検索エンジンでは、通常のバージョンのページとは別に、このページのインデックスが作成される可能性があります。正規タグを使用すると、同じページであることが検索エンジンで認識されます。

例：

* https://www.mydomain.com/my-brand/my-page.html
* https://www.mydomain.com/my-brand/my-page.print.html

両方について、ページの先頭に次のタグを適用します。

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

`href` は、相対パスとして指定することも、絶対パスとして指定することもできます。ページの正規 URL を確認し、このタグを出力するには、このコードをページマークアップに挿入する必要があります。

### 大文字と小文字を区別しないための Dispatcher の設定 {#configuring-the-dispatcher-for-case-insensitivity}

最善の方法は、小文字を使用してすべてのページを提供することです。ただし、ユーザーが URL に大文字を使用して Web サイトにアクセスしたときに、404 エラーが表示されるのは望ましくありません。こうした理由から、すべての受信 URL を小文字にマッピングするように、Apache HTTP Server の設定に書き換えルールを追加することをお勧めします。さらに、小文字の名前を使用してページを作成するようコンテンツの作成者をトレーニングする必要があります。

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

検索エンジンでは、サイトをクロールする前に、サイトのルートに *ファイルがあるかどうかがチェックされる*`robots.txt`はずです。ただし、Google、Yahoo、Bing などの主要な検索エンジンではすべてこの点が考慮されるのに対し、なじみのない検索エンジンの中には、この点が考慮されないものもあります。

サイト全体へのアクセスをブロックするための最も簡単な方法は、`robots.txt` というファイルに次の内容を指定して、サイトのルートに配置することです。

```xml
User-agent: *
Disallow: /
```

また、実稼働環境では、インデックスが作成されないように特定のパスを禁止することもできます。

ただし、`robots.txt` ファイルをサイトのルートに配置すると、Dispatcher フラッシュ要求によって、このファイルが除去されることがあり、URL マッピングによって、Apache HTTP Server の設定で定義された `DOCROOT` とは異なる場所にサイトのルートが置かれる可能性があります。こうした理由から、このファイルをオーサーインスタンスのサイトのルートに配置し、パブリッシュインスタンスにレプリケートするのが一般的です。

### AEM での XML サイトマップの作成  {#building-an-xml-sitemap-on-aem}

クローラーでは、Web サイトの構造をより的確に把握するために XML サイトマップが使用されます。サイトマップを提供すれば SEO ランキングが上がるという保証はありませんが、ベストプラクティスの 1 つとして認められています。サイトマップとして使用する XML ファイルを Web サーバーで手動で管理することもできますが、作成者が新しいコンテンツを作成すると、変更内容がサイトマップに自動的に反映されるように、プログラムによってサイトマップを生成することをお勧めします。

プログラムによってサイトマップを生成するには、`sitemap.xml` の呼び出しをリスンする Sling サーブレットを登録します。このサーブレットは、サーブレット API によって提供されるリソースを使用して、現在のページおよびその子を確認し、XML を出力します。XML はその後、Dispatcher でキャッシュされます。`robots.txt` ファイルのサイトマッププロパティで、この場所を参照する必要があります。さらに、新しいページがアクティベートされたときには必ず、このファイルがフラッシュされるように、カスタムフラッシュルールを実装する必要があります。

>[!NOTE]
>
>Sling サーブレットを登録すると、拡張子 `sitemap` のセレクター `xml` をリスンできます。これにより、末尾が以下のようになっている URL が要求されると、サーブレットによってリクエストが処理されます。
>    `/<path-to>/page.sitemap.xml`
その後、要求されたリソースをリクエストから取得し、JCR API を使用してコンテンツツリーのその地点からサイトマップを生成できます。
このようなアプローチは、複数のサイトを同じインスタンスから処理している場合にメリットがあります。`/content/siteA.sitemap.xml` に対するリクエストでは `siteA` 用のサイトマップが生成され、`/content/siteB.sitemap.xml` のリクエストでは `siteB` 用のサイトマップが生成されます。コードを追加する必要はありません。

### レガシー URL の 301 リダイレクトの作成 {#creating-redirects-for-legacy-urls}

新しい構造でサイトの運用を開始するときには、次の 2 つの理由から、Apache HTTP Server で 301 リダイレクトを実装し、テストすることが重要です。

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
