---
title: AEM as a Cloud Service でのクライアントサイドライブラリの使用
description: AEM では、クライアントサイドライブラリフォルダーが提供されています。これにより、クライアントサイドコード（clientlibs）をリポジトリーに格納し、カテゴリ別に整理して、それぞれのカテゴリのコードをクライアントに提供するタイミングと方法を定義できます。
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '2497'
ht-degree: 100%

---


# AEM as a Cloud Service でのクライアントサイドライブラリの使用 {#using-client-side-libraries}

デジタルエクスペリエンスは、複雑な JavaScript や CSS コードを利用したクライアントサイドの処理に大きく依存しています。AEM クライアントサイドライブラリ（clientlibs）を使用すると、これらのクライアントサイドライブラリをリポジトリー内に整理し、一元的に保存できます。[AEM プロジェクトアーキタイプでフロントエンドビルドプロセスと組み合わせる](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html?lang=ja)と、AEM プロジェクトのフロントエンドコードの管理が簡単になります。

AEM で clientlibs を使用する利点は次のとおりです。

* クライアントサイドのコードは、他のすべてのアプリケーションコードやコンテンツと同様に、リポジトリーに保存されます。
* AEM の clientlibs によって、すべての CSS と JS を 1 つのファイルにまとめられます。
* [Dispatcher](/help/implementing/dispatcher/disp-overview.md) 経由でアクセス可能なパスで clientlibs を公開します。
* 参照先ファイルまたは画像のパスの書き換えを許可します。

Clientlibs は、AEM から CSS と JavaScript を配信するための組み込みソリューションです。

>[!TIP]
>
>AEM プロジェクト用に CSS と JavaScript を作成するフロントエンド開発者は、[AEM プロジェクトアーキタイプと、自動化されたフロントエンドビルドプロセス](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html?lang=ja)にも慣れ親しんでおく必要があります。

## クライアントサイドライブラリとは {#what-are-clientlibs}

Sites では、JavaScript と CSS、およびクライアントサイドで処理されるアイコンや web フォントなどの静的リソースが必要です。clientlib は、そのようなリソースを（必要に応じてカテゴリ別に）参照し、提供する AEM のメカニズムです。

AEM は、サイトの CSS と JavaScript を 1 つのファイルにまとめて一元的な場所に配置し、HTML 出力にはリソースのコピーが 1 つだけ含まれるようにします。これにより、配信の効率が最大化され、プロキシを介してリポジトリ内でリソースを一元的に管理し、アクセスの安全性を確保できます。

## AEM as a Cloud Service 向けフロントエンド開発 {#fed-for-aemaacs}

すべての JavaScript、CSS およびその他のフロントエンドアセットは、[AEM プロジェクトアーキタイプの ui.frontend モジュール](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html?lang=ja)で管理する必要があります。アーキタイプの柔軟性により、最新の web ツールを使用して、これらのリソースを作成および管理できます。

次に、アーキタイプは、リソースを単一の CSS ファイルと JS ファイルにコンパイルし、自動的にリポジトリーの `cq:clientLibraryFolder` に埋め込むことができます。

## クライアントサイドライブラリフォルダー構造 {#clientlib-folders}

クライアントサイドライブラリフォルダーは、`cq:ClientLibraryFolder` タイプのリポジトリノードです。その [CND 表記](https://jackrabbit.apache.org/node-type-notation.html)での定義は次のとおりです。

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` ノードは、リポジトリーの `/apps` サブツリー内の任意の場所に配置できます。
* ノードの `categories` プロパティを使用して、ノードが属するライブラリカテゴリを特定します。

各 `cq:ClientLibraryFolder` には、JS ファイルや CSS ファイルのセットと、いくつかのサポートファイルが入力されます（以下を参照）。`cq:ClientLibraryFolder` の重要なプロパティは、次のように設定されます。

* `allowProxy`：すべての clientlibs は `apps` に保存する必要があるため、このプロパティを使用すると、プロキシサーブレット経由でクライアントライブラリにアクセスできます。後述の[クライアントライブラリフォルダーの配置とプロキシクライアントライブラリサーブレットの使用](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)の節を参照してください。
* `categories`：`cq:ClientLibraryFolder` に含まれる JS ファイルや CSS ファイルのセットのカテゴリを特定します。`categories` プロパティは複数の値を取るため、ライブラリフォルダーを複数のカテゴリの一部にすることができます（これがどのように役立つかについては以下を参照）。

クライアントライブラリフォルダーに 1 つ以上のソースファイルが含まれている場合は、そのソースファイルが実行時に単一の JS ファイルや CSS ファイルに結合されます。生成されるファイルの名前はノード名で、ファイル名の拡張子は `.js` または `.css` です。例えば、`cq.jquery` という名前のライブラリノードからは、 `cq.jquery.js` または `cq.jquery.css` という名前のファイルが生成されます。

クライアントライブラリフォルダーには次の項目が含まれます。

* JS／CSS ソースファイル（いずれかまたは両方）
* アイコン、web フォントなど、CSS スタイルをサポートする静的リソース
* 生成される JS／CSS ファイルに統合するソースファイルを識別する 1 つの `js.txt` ファイルと 1 つの `css.txt` ファイル（いずれかまたは両方）

![clientlib のアーキテクチャ](assets/clientlib-architecture.drawio.png)

## クライアントサイドライブラリフォルダーの作成 {#creating-clientlib-folders}

クライアントライブラリは、`/apps` に配置する必要があります。このルールは、コードをコンテンツや設定からより適切に分離するために必要です。

`/apps` にあるクライアントライブラリにアクセスできるようにするために、プロキシサーブレットが使用されます。ACL は依然としてクライアントライブラリフォルダーで適用されますが、サーブレットを使用すると、`/etc.clientlibs/` プロパティが `allowProxy` に設定されている場合、`true` を介してコンテンツを読み取ることができます。

1. Web ブラウザーで CRXDE Lite を開きます（`https://<host>:<port>/crx/de`）。
1. `/apps` フォルダーを右クリックして、**作成／ノードを作成**&#x200B;をクリックします。
1. ライブラリフォルダーの名前を入力し、 「**タイプ**」リストで `cq:ClientLibraryFolder` を選択します。「**OK**」をクリックし、「**すべて保存**」をクリックします。
1. ライブラリが所属するカテゴリ（1 つまたは複数）を指定するには、`cq:ClientLibraryFolder` ノードを選択し、次のプロパティを追加して、「**すべて保存**」をクリックします。
   * 名前：`categories`
   * タイプ：String
   * 値：カテゴリ名
   * マルチ：選択
1. クライアントライブラリを `/etc.clientlibs` のプロキシ経由でアクセスできるようにするには、 `cq:ClientLibraryFolder` ノードを選択し、次のプロパティを追加して、「**すべて保存**」をクリックします。
   * 名前：`allowProxy`
   * タイプ：Boolean
   * 値：`true`
1. 静的リソースを管理する必要がある場合は、クライアントライブラリフォルダーの `resources` の下にサブフォルダーを作成します。
   * フォルダー `resources` 以外の場所に静的リソースを格納した場合、静的リソースはパブリッシュインスタンスで参照できません。
1. 追加ソースファイルをライブラリフォルダーに格納します。
   * これは、通常、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html?lang=ja)のフロントエンドビルドプロセスで行われます。
   * 必要に応じて、サブフォルダーを使用してソースファイルを整理できます。
1. クライアントライブラリフォルダーを選択して、**作成／ファイルを作成**&#x200B;をクリックします。
1. ファイル名ボックスに、次のいずれかのファイル名を入力して、「OK」をクリックします。
   * **`js.txt`：** JavaScript ファイルを生成する場合はこのファイル名を使用します。
   * **`css.txt`：** カスケーディングスタイルシート（CSS）を生成する場合はこのファイル名を使用します。
1. ファイルを開き、ソースファイルのパスのルートを識別する次のテキストを入力します。
   * `#base=*[root]*`
   * `[root]` を、ソースファイルが格納されているフォルダーの TXT ファイルに対する相対パスに置き換えます。例えば、ソースファイルが TXT ファイルと同じフォルダーにある場合は、次のテキストを使用します。
      * `#base=.`
   * 次のコードで、`cq:ClientLibraryFolder` ノードの下の mobile という名前のフォルダーをルートに設定します。
      * `#base=mobile`
1. `#base=[root]` の下の行に、ソースファイルのルートに対する相対パスを入力します。各ファイル名を別々の行に配置します。
1. 「**すべて保存**」をクリックします。

## クライアントサイドライブラリの提供 {#serving-clientlibs}

クライアントライブラリフォルダーを[必要に応じて設定](#creating-clientlib-folders)したら、clientlibs をプロキシ経由でリクエストできます。次に例を示します。

* clientlib は `/apps/myproject/clientlibs/foo` にあります。
* 静的画像は `/apps/myprojects/clientlibs/foo/resources/icon.png` にあります。

`allowProxy` プロパティを使用して、次をリクエストできます。

* `/etc.clientlibs/myprojects/clientlibs/foo.js` 経由の clientlib
* 静的な画像（`/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png` を介す）

### クライアントライブラリの読み込み（HTL 経由） {#loading-via-htl}

clientlibs がクライアントライブラリフォルダーに正常に保存および管理されると、HTL を介してアクセスできます。

クライアントライブラリは AEM 提供のヘルパーテンプレートを介して読み込まれます。テンプレートには `data-sly-use` を使用してアクセスできます。このファイルには 3 つのヘルパーテンプレートが含まれ、`data-sly-call` で呼び出すことができます。

各ヘルパーテンプレートには、必要なクライアントライブラリを参照するための `categories` オプションを指定できます。このオプションには、文字列値の配列またはコンマ区切り値のリストを含む文字列を指定できます。

HTL を使用した clientlibs の読み込みについて詳しくは、[HTL のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html?lang=ja#loading-client-libraries)を参照してください。

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## オーサーのクライアントライブラリ対パブリッシュのクライアントライブラリ {#clientlibs-author-publish}

ほとんどの clientlibs は、AEM パブリッシュインスタンスで必要です。つまり、clientlibs の大半の目的は、コンテンツのエンドユーザーエクスペリエンスを生み出すことです。パブリッシュインスタンスの clientlibs の場合、[フロントエンドビルドツール](#fed-for-aemaacs)は、[前述のように、クライアントライブラリフォルダー](#creating-clientlib-folders)を介して使用およびデプロイできます。

ただし、オーサリングエクスペリエンスのカスタマイズにクライアントライブラリが必要な場合があります。例えば、ダイアログのカスタマイズには、AEM オーサリングインスタンスに小さな CSS または JS のデプロイが必要になる場合があります。

### オーサークライアントライブラリの管理 {#clientlibs-on-author}

オーサーがクライアントライブラリを使用する必要がある場合は、パブリッシュと同じ方法で `/apps` にクライアントライブラリを作成できますが、管理するプロジェクト全体を作成する代わりに、直接 `/apps/.../clientlibs/foo` に書き込むことができます。

その後、作成したクライアントライブラリをすぐに使用できるクライアントライブラリカテゴリに追加することで、オーサリング JS に「接続」できます。

## デバッグツール {#debugging-tools}

AEM には、クライアントライブラリフォルダーをデバッグおよびテストするためのツールが用意されています。

### クライアントライブラリの確認 {#discover-client-libraries}

`/libs/cq/granite/components/dumplibs/dumplibs` コンポーネントは、システム上のすべてのクライアントライブラリフォルダーに関する情報のページを生成します。`/libs/granite/ui/content/dumplibs` ノードは、コンポーネントをリソースタイプとして持ちます。ページを開くには、次の URL を使用します（必要に応じてホストとポートを変更）。

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

情報には、ライブラリのパスおよびタイプ（CSS または JS）と、categories や dependencies などのライブラリ属性の値が含まれます。ページ上の後続のテーブルは、各カテゴリおよびチャネルに含まれるライブラリを示します。

### 生成される出力の確認 {#see-generated-output}

`dumplibs` コンポーネントには、`ui:includeClientLib` タグ用に生成されたソースコードを表示するテストセレクターが含まれています。このページには、js、css およびテーマの属性の異なる組み合わせのためのコードが含まれています。

1. 次のいずれかの方法で、テスト出力ページを開きます。
   * `dumplibs.html` ページから、「**こちらをクリックして出力テスト**」テキストのリンクをクリックします。
   * Web ブラウザーで次の URL を開きます（必要に応じて別のホストおよびポートを使用）。
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * デフォルトページに、categories 属性の値がないタグの出力が表示されます。
1. 特定のカテゴリの出力を確認するには、クライアントライブラリの `categories` プロパティの値を入力して、「**クエリを送信**」をクリックします。

## その他のクライアントライブラリフォルダー機能 {#additional-features}

AEM のクライアントライブラリフォルダーでは、他にもいくつかの機能がサポートされています。ただし、AEM as a Cloud Service ではこれらは必須ではないので、使用しないでください。完全を期すために、以下に示します。

>[!WARNING]
>
>クライアントライブラリフォルダーのこれらの追加機能は、AEM as a Cloud Service では必要ないので、使用しないでください。完全を期すために、以下に示します。

### Adobe Granite HTML Library Manager {#html-library-manager}

追加のクライアントライブラリ設定は、システムコンソール（`https://<host>:<port>/system/console/configMgr`）の **Adobe Granite HTML Library Manager** パネルで制御できます。

### 追加のフォルダープロパティ {#additional-folder-properties}

フォルダーのプロパティには、依存関係や埋め込みの制御が許可されているものもありますが、通常は不要になっており、使用はお勧めしません。

* `dependencies`：これは、このライブラリカテゴリが依存する他のクライアントライブラリフォルダーのリストです。例えば、`F` と `G` の 2 つの `cq:ClientLibraryFolder` ノードを指定し、`F` のファイルが正しく機能するために、別の `G` にあるファイルが必要な場合、`G` のうち 1 つ以上の `categories` は、`F` の `dependencies` に含まれている必要があります。
* `embed`：他のライブラリからコードを埋め込むために使用します。ノード `F` がノード `G` と `H` を埋め込むと、結果として得られる HTML は、ノード `G` と `H` からのコンテンツの合成になります。

### 依存関係へのリンク {#linking-to-dependencies}

クライアントライブラリフォルダーのコードが他のライブラリを参照する場合、他のライブラリを依存関係として識別します。クライアントライブラリフォルダーを参照する `ui:includeClientLib` タグにより、生成されたライブラリファイルと依存関係へのリンクが HTML コードに組み込まれます。

依存関係は別の `cq:ClientLibraryFolder` でなければなりません。依存関係を識別するには、次の属性を持つプロパティを `cq:ClientLibraryFolder` ノードに追加します。

* **名前：** dependencies
* **タイプ：** String[]
* **値：**&#x200B;現在のライブラリフォルダーの依存先である cq:ClientLibraryFolder ノードの categories プロパティの値。

例えば、`/etc/clientlibs/myclientlibs/publicmain` は `cq.jquery` ライブラリに依存しています。メインのクライアントライブラリを参照するページは、次のコードを含む HTML を生成します。

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 他のライブラリからのコードの埋め込み {#embedding-code-from-other-libraries}

あるクライアントライブラリから別のクライアントライブラリに、コードを埋め込むことができます。実行時に、埋め込み元のライブラリで生成される JS ファイルおよび CSS ファイルには、埋め込み先のライブラリのコードが含まれます。

コードの埋め込みは、リポジトリーのセキュリティ保護された領域に格納されているライブラリへのアクセスを提供する際に便利です。

#### アプリ固有のクライアントライブラリフォルダー {#app-specific-client-library-folders}

アプリケーション関連のすべてのファイルは、`/apps` 内のアプリケーションフォルダーに格納することをお勧めします。Web サイト訪問者の `/apps` フォルダーに対するアクセスを拒否することもお勧めします。両方のベストプラクティスを満たすには、`/etc` にクライアントライブラリフォルダーを作成して、 `/apps` 内のクライアントライブラリを埋め込みます。

埋め込むクライアントライブラリフォルダーを識別するには、categories プロパティを使用します。ライブラリを埋め込むには、次のプロパティ属性を使用して、埋め込み `cq:ClientLibraryFolder` ノードにプロパティを追加します。

* **名前：** embed
* **タイプ：** String[]
* **値：**&#x200B;埋め込む `cq:ClientLibraryFolder` ノードの categories プロパティの値。

#### 埋め込みを使用したリクエストの最小化 {#using-embedding-to-minimize-requests}

場合によっては、パブリッシュインスタンスによって一般的なページ用に生成される最終的な HTML に、比較的多くの `<script>` 要素が含まれていることがあります。

このような場合、必要なすべてのクライアントライブラリコードを 1 つのファイルに組み合わせて、ページ読み込み時のリクエストの行き来の数を減らすと便利です。これを行うには、`cq:ClientLibraryFolder` ノードの embed プロパティを使用して、必要なライブラリをアプリ固有のクライアントライブラリに `embed` します。

#### CSS ファイル内のパス {#paths-in-css-files}

CSS ファイルを埋め込むと、生成される CSS コードは、埋め込みライブラリに対するリソースへの相対パスを使用します。例えば、公開アクセス可能な `/etc/client/libraries/myclientlibs/publicmain` ライブラリによって `/apps/myapp/clientlib` クライアントライブラリが埋め込まれるとします。

`main.css` ファイルには次のスタイルが含まれます。

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

`publicmain` ノードが生成する CSS ファイルには、元の画像の URL を使用した、次のスタイルが含まれます。

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### HTML 出力の埋め込みファイルの確認 {#see-embedded-files}

埋め込みコードの元をトレースする、または埋め込みクライアントライブラリが期待どおりの結果を得られるようにするには、実行時に埋め込まれているファイルの名前を確認できます。ファイル名を確認するには、Web ページの URL に `debugClientLibs=true` パラメーターを追加します。生成されるライブラリには、埋め込みコードの代わりに `@import` ステートメントが含まれています。

前の「[他のライブラリからのコードの埋め込み](#embedding-code-from-other-libraries)」節の例では、クライアントライブラリフォルダーに`/etc/client/libraries/myclientlibs/publicmain`クライアントライブラリフォルダーが埋め込まれています`/apps/myapp/clientlib`。Web ページにパラメーターを追加すると、Web ページのソースコードに次のリンクが作成されます。

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

`publicmain.css` ファイルを開くと、次のコードが表示されます。

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Web ブラウザーのアドレスボックスで、HTML の URL に次のテキストを付加します。
   * `?debugClientLibs=true`
1. ページが読み込まれたら、ページのソースを表示します。
1. リンク要素の href として指定されているリンクをクリックしてファイルを開き、ソースコードを表示します。

### プリプロセッサーの使用 {#using-preprocessors}

AEM では、プラグ可能なプリプロセッサーを使用でき、AEM のデフォルトプリプロセッサーとして、CSS および JavaScript 用の [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) と YUI が定された JavaScript 用の [Google Closure Compiler（GCC）](https://developers.google.com/closure/compiler/)をサポートします。

プラグ可能なプリプロセッサーを使用すると、次のような柔軟な使い方ができるようになります。

* スクリプトソースを処理できる ScriptProcessor を定義
* プロセッサーはオプションを使用して設定できる
* プロセッサーは縮小用に使用できるが、縮小以外の場合にも使用できる
* clientlib は、使用するプロセッサーを定義できる

>[!NOTE]
>
>デフォルトでは、AEM は YUI Compressor を使用します。既知の問題のリストについては、[YUI Compressor GitHub ドキュメント](https://github.com/yui/yuicompressor/issues)を参照してください。特定の clientlibs 用の GCC コンプレッサーに切り替えると、YUI を使用しているときに発生していたいくつかの問題が解決することがあります。

>[!CAUTION]
>
>縮小化したライブラリをクライアントライブラリに配置しないでください。代わりに、未加工のライブラリを提供し、縮小が必要な場合は、プリプロセッサーのオプションを使用します。

#### 使用方法 {#usage}

クライアントライブラリごとに、またはシステム全体でプリプロセッサーを設定できます。

* クライアントライブラリノードで、複数値プロパティ `cssProcessor` および `jsProcessor` を追加します。
* または、**HTML ライブラリマネージャー**&#x200B;の OSGi 設定で、システムのデフォルト設定を定義します。

clientlib ノードのプリプロセッサー設定は、OSGI 設定よりも優先されます。

#### 形式と例 {#format-and-examples}

##### 形式 {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### CSS 縮小用の YUI Compressor と JS 用の GCC {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### 事前処理のための Typescript と縮小および不明化のための GCC {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```javascript
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

##### 追加の GCC オプション {#additional-gcc-options}

```javascript
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

GCC オプションについて詳しくは、[GCC ドキュメント](https://developers.google.com/closure/compiler/docs/compilation_levels)を参照してください。

#### システムのデフォルト縮小ツールの設定 {#set-system-default-minifier}

YUI は、AEM のデフォルトの縮小ツールとして設定されています。これを GCC に変更するには、次の手順に従います。

1. Apache Felix Config Manager（`http://<host>:<port/system/console/configMgr`）に移動します。
1. **Adobe Granite HTML ライブラリマネージャー**&#x200B;を検索して編集します。
1. 「**Minify**」オプションを有効にします（まだ有効でない場合）。
1. **JS Processor Default Configs** の値を `min:gcc` に設定します。
   * セミコロンで区切られている場合、オプションを渡すことができます（例：`min:gcc;obfuscate=true`）。
1. 「**保存**」をクリックして、変更を保存します。
