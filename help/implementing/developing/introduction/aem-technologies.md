---
title: AEM 技術基盤
description: AEM の構造化および JCR、Sling、OSGi などの基本的なテクノロジーを含む、AEM の技術基盤の概要です。
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '2186'
ht-degree: 100%

---

# AEM 技術基盤 {#aem-technical-foundations}

AEM は、拡張性が高く柔軟なテクノロジーに基づいて構築された実証済みの堅牢なプラットフォームです。このドキュメントは、AEM を構成する様々な部分の詳細な概要を説明し、AEM フルスタックデベロッパー向けの技術的な付録として作成されています。はじめる前のガイドとしての意図はありません。AEM を初めて開発する場合は、最初の手順として『[AEM Sites の開発の手引き - WKND チュートリアル](develop-wknd-tutorial.md)』を参照してください。

>[!TIP]
>
>AEM の中核技術に入る前に、『[AEM Sites の開発の手引き - WKND チュートリアル](develop-wknd-tutorial.md)』を完了することを推奨します。

## 基本事項 {#fundamentals}

最新のコンテンツ管理システムである AEM は次の標準的な Web テクノロジーに依存しています。

* リクエスト応答（XMLHttpRequest／XMLHttpResponse）サイクル
* HTML
* CSS
* JavaScript

基盤となるコンテンツリポジトリーとビジネスロジックレイヤーは、Javaテクノロジーに基づいて構築されています。

* JCR
* Sling
* OSGi

## Java コンテンツリポジトリー {#java-content-repository}

Java コンテンツリポジトリー（JCR）の規格である [JSR 283](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html) では、コンテンツリポジトリー内で、任意の精度レベルでコンテンツに双方向アクセスするための、ベンダーにも実装にも依存しない方法が示されています。仕様を主導しているのは、Adobe Research（スイス）AG です。

[JCR API 2.0](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) パッケージである `javax.jcr.*` が、リポジトリーコンテンツの直接アクセスと操作に使用されます。

AEM は JCR 上に構築されています。

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/) は、JCR 標準に準拠した最新のワールドクラスの Web サイトやその他の要求の厳しいコンテンツアプリケーションの基盤として使用する、スケーラブルで高パフォーマンスの階層コンテンツリポジトリーの実装です。

Jackrabbit Oak（単に Oak とも呼ばれる）は、AEM を構築する JCR 標準の実装です。

## Sling のリクエスト処理 {#sling-request-processing}

AEM は、コンテンツ指向アプリケーションの開発を容易にする REST 原則に基づく Web アプリケーションフレームワーク [Sling](https://sling.apache.org/site/index.html) を使用して構築されています。Sling は、Apache Jackrabbit Oak などの JCR リポジトリーをデータストアとして使用します。Sling は Apache Software Foundation に貢献してきました。詳しい情報は Apache にあります。

### Sling の概要 {#introduction-to-sling}

Sling を使用する場合、レンダリングされるコンテンツのタイプは、処理に関する第一の考慮事項ではありません。主な考慮事項は、URL を解決して得られるコンテンツオブジェクト用に、レンダリングを実行するためのスクリプトが見つかるかどうかです。このことは、要件に合わせて簡単にカスタマイズ可能なページを Web コンテンツ作成者が構築する際に非常に役立ちます。

この柔軟性の利点は、様々なコンテンツ要素を持つアプリ、または容易にカスタマイズできるページが必要な場合に明らかです。特に、AEM などの Web コンテンツ管理システムを実装する場合です。

Sling を使用した開発の概要について詳しくは、『[15 分間でわかる Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html)』を参照してください。

次の図は、Sling のスクリプト解決の説明です。HTTP リクエストからコンテンツノード、コンテンツノードからリソースタイプ、リソースタイプからスクリプトを得る方法と、使用可能なスクリプト変数を示しています。

![Apache Sling スクリプトの解決について](assets/sling-cheatsheet-01.png)

次の図は、`SlingPostServlet` を扱う際に使用できる、非表示ながらも強力なリクエストパラメーターの説明です。リポジトリーでノードを作成、変更、削除、コピーおよび移動するためのオプションを際限なしに提供する、すべての POST リクエストのデフォルトハンドラーです。

![SlingPostServlet の使用](assets/sling-cheatsheet-02.png)

### Sling はコンテンツ中心型 {#sling-is-content-centric}

Sling はコンテンツ中心型です&#x200B;*。*&#x200B;つまり、（HTTP）要求がそれぞれ JCR リソース（リポジトリーノード）の形式でコンテンツにマップされるので、コンテンツに焦点を当てた処理が行われるということです。

* 最初のターゲットは、コンテンツを保持しているリソース（JCR ノード）です。
* 次に、表現、つまりスクリプトが、リソースプロパティから、リクエストの一部（セレクターや拡張子など）と組み合わせて配置されます。

### RESTful Sling {#restful-sling}

コンテンツ中心型の原理により、Sling は REST 指向のサーバーを実装するので、Web アプリケーションフレームワークの新しい概念を特徴としています。メリットは次のとおりです。

* 表面上だけでなく、非常に RESTful であり、リソースや表現をサーバー内で正しくモデリングします。
* 1 つ以上のデータモデルを削除します。
   * その他のコンテンツ管理フレームワークでは、リソースにアクセスするために URL 構造、ビジネスオブジェクト、DB スキーマが必要になる場合があります。
   * Sling を使用すると、これは「URL = リソース = JCR 構造」になります。

### URL の分解 {#url-decomposition}

Sling では、処理はユーザーリクエストの URL によって駆動されます。これにより、適切なスクリプトによって表示されるコンテンツが定義されます。これを行うために、URL から情報が抽出されます。

次の URL を分析する場合、

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

以下の複合部分に分割できます。

| プロトコル | ホスト |  | コンテンツのパス | セレクター | 拡張子 |  | サフィックス |  | パラメーター |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **プロトコル** - HTTPS
* **ホスト** - サイトのドメイン
* **コンテンツパス** - レンダリングされるコンテンツを指定するパス。拡張子と共に使用します。この例では、`tools/spy.html` です。
* **セレクター** - コンテンツのレンダリングの代替方法として使用します。この例では、A4 形式のプリンターに対応するバージョンです。
* **拡張子** - 拡張コンテンツの形式。これも、レンダリングに使用するスクリプトを指定します。
* **サフィックス** - 追加情報を指定するために使用できます。
* **パラメーター** - 動的コンテンツに必要なパラメーターです。

#### URL からコンテンツおよびスクリプトへ {#from-url-to-content-and-scripts}

URL 分解の原則を使用します。

* マッピングはリクエストから抽出されたコンテンツパスを使用してリソースを見つけます。
* 適切なリソースが見つかると、Sling リソースタイプが抽出され、コンテンツのレンダリングに使用するスクリプトを見つけるために使用されます。

下の図は、使用するメカニズムを示しています。これについては、以下の各項で詳細に説明します。

![URL マッピングメカニズム](assets/url-mapping.png)

Sling を使用して、特定のエンティティをレンダリングするスクリプトを指定します（JCR ノードで `sling:resourceType` プロパティを設定します）。このメカニズムは、リソースが複数のレンディションを持つことができるため、スクリプトがデータエンティティにアクセスするメカニズム（PHP スクリプトの SQL 文のように）よりも自由度が高くなります。

#### リクエストのリソースへのマッピング {#mapping-requests-to-resources}

リクエストは分解され、必要な情報が抽出されます。リポジトリーで、リクエストされたリソース（コンテンツノード）の検索が行われます。

* 最初の Sling では、リクエストで指定されている場所（例：`../content/corporate/jobs/developer.html`）にノードが存在するかどうかを確認します。
* ノードが見つからない場合は、拡張子なしで検索を繰り返します（例：`../content/corporate/jobs/developer`）。
* それでもノードが見つからない場合、Sling は HTTP コード 404（Not Found）を返します。

Sling では JCR ノード以外のものをリソースとすることもできますが、これは高度な機能です。

### スクリプトの検索 {#locating-the-script}

適切なリソース（コンテンツノード）が見つかると、**sling リソースタイプ**&#x200B;が抽出されます。これは、コンテンツのレンダリングに使用するスクリプトを見つけるパスです。

`sling:resourceType` によって指定されるパスは、次のいずれかです。

* 絶対パス
* 設定パラメーターに対する相対パス

>[!TIP]
>
>移植性を高めるため、相対パスが推奨されます。

すべての Sling スクリプトは、`/apps`（可変、ユーザースクリプト）または`/libs`（不可変、システムスクリプト）のサブフォルダーに格納され、この順序で検索されます。

その他の注意点は次のとおりです。

* メソッド（GET、POST）が必要なときは、HTTP の仕様に従って大文字で指定します（例：`jobs.POST.esp`）。
* 様々なスクリプトエンジンがサポートされていますが、一般的な推奨スクリプトは HTL と JavaScript です。

AEM の特定のインスタンスでサポートされているスクリプトエンジンのリストは、Felix Management Console（`http://<host>:<port>/system/console/slingscripting`）にあります。

以前の例を使用すると、`sling:resourceType` が `hr/jobs` の場合は、次のようになります。

* `.html`で終わる GET/HEAD リクエストと URL（デフォルトのリクエストタイプ、デフォルトの形式）
   * スクリプトは `/apps/hr/jobs/jobs.esp` です。`sling:resourceType` の最後のセクションがファイル名になります。
* POST 要求（GET/HEAD を除くすべての要求タイプ。メソッド名は大文字にする必要があります）
   * スクリプト名に POST が使用されます。
   * スクリプトは `/apps/hr/jobs/jobs.POST.esp` です。
* `.html`で終わらない、他の形式の URL
   * 例：`../content/corporate/jobs/developer.pdf`
   * スクリプトは `/apps/hr/jobs/jobs.pdf.esp` です。スクリプト名にサフィックスが追加されます。
* セレクターを含む URL
   * セレクターを使用して、同じコンテンツを別の形式で表示できます。例：プリンターに適したバージョン、rss フィード、概要など。
   * プリンターに適したバージョンでは、セレクターが `print` である可能性がります。例：`../content/corporate/jobs/developer.print.html` 
   * スクリプトは `/apps/hr/jobs/jobs.print.esp` です。セレクターがスクリプト名に追加されます。
* `sling:resourceType` が定義されていない場合は、次のようになります。
   * コンテンツパスは、適切なスクリプトを検索するために使用されます（パスに基づいた `ResourceTypeProvider` がアクティブな場合）。
   * 例えば、`../content/corporate/jobs/developer.html` のスクリプトは、`/apps/content/corporate/jobs/` で検索を生成します。
   * プライマリノードタイプが使用されます。
* スクリプトがまったく見つからない場合は、デフォルトのスクリプトが使用されます。
   * デフォルトのレンディションは現在、プレーンテキスト（`.txt`）、HTML（`.html`）、JSON（`.json`）としてサポートされています。これらのレンディションでは、ノードのプロパティ（適切な形式）がリストされます。拡張子 `.res` のデフォルトのレンディション、または要求拡張子のない要求は、（可能な場合は）リソースをスプールします。
* HTTP エラー処理（コード 403 または 404）の場合、Sling は以下のいずれかの場所でスクリプトを検索します。
   * カスタマイズされたスクリプトの場所 `/apps/sling/servlet/errorhandler`
   * または標準スクリプトの場所 `/libs/sling/servlet/errorhandler/404.jsp`

特定のリクエストに複数のスクリプトが該当する場合は、一致率が最も高いスクリプトが選択されます。一致は具体的であるほど良くなります。つまり、リクエスト拡張子であれ、メソッド名の一致であれ、セレクターの一致が多いほど良くなります。

例えば、次のリソースにアクセスするためのリクエストについて考えます。

* `/content/corporate/jobs/developer.print.a4.html`

リソースのタイプは次のとおりとします。

* `sling:resourceType="hr/jobs"`

また、次のリストのスクリプトが正しい場所にあると仮定します。

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

この場合、優先順位は (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1) となります。

リソースタイプ（主に `sling:resourceType` プロパティで定義）に加えて、リソーススーパータイプもあります。これは通常、`sling:resourceSuperType` プロパティで示されます。これらのスーパータイプは、スクリプトを検索する際にも検討されます。リソーススーパータイプの利点は、（デフォルトのサーブレットで使用される）デフォルトのリソースタイプ `sling/servlet/default` が事実上のルートになるリソースの階層を形成できる点です。

リソースのリソーススーパータイプは次の 2 つの方法で定義できます。

* リソースの `sling:resourceSuperType` プロパティを使用。
* `sling:resourceSuperType` が示すノードの `sling:resourceType` プロパティを使用。

次に例を示します。

* `/`
   * `a`
   * `b`
      * `sling:resourceSuperType = a`
   * `c`
      * `sling:resourceSuperType = b`
   * `x`
      * `sling:resourceType = c`
   * `y`
      * `sling:resourceType = c`
      * `sling:resourceSuperType = a`

タイプの階層：

* `/x`
   * `[ c, b, a, <default>]` です
* 一方、`/y` では
   * `[ c, a, <default>]` です

これは、`/y` には `sling:resourceSuperType` プロパティがあるのに対して、`/x` にはなく、スーパータイプがリソースタイプから継承されているからです。

#### Sling スクリプトを直接呼び出しできない {#sling-scripts-cannot-be-called-directly}

Sling 内では、スクリプトを直接呼び出しできません。REST サーバーの厳格な概念に違反して、リソースと表現を混在させることになるからです。

表現（スクリプト）を直接呼び出す場合、リソースがスクリプト内に隠され、フレームワーク（Sling）では認識できなくなります。これにより、次のような機能が失われます。

* GET 以外の HTTP メソッドの自動処理。これには以下が含まれます。
   * Sling のデフォルトの実装で処理される POST、PUT、DELETE
   * `sling:resourceType` 内の `POST.jsp` スクリプト
* コードアーキテクチャに必要なクリーン性や明確な構造が失われます。これは大規模な開発では最も重要です。

### Sling API {#sling-api}

Sling API パッケージ、`org.apache.sling.*`、およびタグライブラリを使用します。

### sling:include を使用した既存の要素の参照 {#referencing-existing-elements-using-sling-include}

最後の考慮事項は、スクリプト内にある既存の要素の参照の必要性です。

より複雑なスクリプト（集計スクリプト）は、複数のリソース（ナビゲーション、サイドバー、フッター、リストの要素など）へのアクセスが必要になる場合があり、そのために&#x200B;*リソース*&#x200B;を含めます。

これを行うには、`sling:include("/<path>/<resource>")` コマンドを使用します。これにより、参照されるリソースの定義を効果的に含めることができます。

## OSGi {#osgi}

OSGi（Open Services Gateway Initiative）は、モジュラー型アプリケーションとライブラリを開発および展開するためのアーキテクチャを定義します（Java 用 Dynamic Module System とも呼ばれます）。OSGi コンテナを使用すると、アプリケーションを個々のモジュール（追加のメタ情報を含む jar ファイルで、OSGi 用語でバンドルと呼ばれます）に分割し、それらの間の相互依存関係を次の機能で管理できます。

* コンテナ内に実装されているサービス
* コンテナとアプリケーションの間の契約

これらのサービスおよび契約によって提供されるアーキテクチャでは、コラボレーションのために個々の要素が相互に動的に検出し合うことができます。

その後、OSGi フレームワークによって、これらのバンドルの動的読み込み／読み込み解除、設定および制御が可能になります。再起動は不要です。

>[!NOTE]
>
>OSGi テクノロジーについて詳しくは、[OSGi Web サイト](https://www.osgi.org)を参照してください。
>
>特に、基礎教育に関するページには、プレゼンテーションやチュートリアルのコレクションが収められています。

このアーキテクチャにより、Sling をアプリケーション固有のモジュールで拡張できます。Sling、つまり AEM は、OSGi の [Apache Felix](https://felix.apache.org/) 実装を使用します。どちらも、OSGi フレームワーク内で実行される OSGi バンドルの集まりです。

これにより、インストール内のどのパッケージでも、以下のアクションを実行できます。

* インストール
* 開始
* 停止
* アップデート
* アンインストール
* 現在のステータスの確認
* 特定のバンドルに関する詳細情報（記号名、バージョン、場所など）へのアクセス

詳しくは、「[AEM as a Cloud Service の OSGI の設定](/help/implementing/deploying/configuring-osgi.md)」を参照してください。

## リポジトリー内の構造 {#structure-within-the-repository}

以下のリストは、リポジトリー内で見られる構造の概要を示しています。

* `/apps` - アプリケーション関連。Web サイトに固有のコンポーネント定義が含まれます。開発するコンポーネントは、`/libs/core/wcm/components` で提供されている標準搭載のコンポーネントに基づくことができます。
* `/content` - 
Web サイト用に作成されたコンテンツ。
* `/etc`
* `/home` - ユーザーおよびグループの情報。
* `/libs` - AEM のコアに属するライブラリと定義。`/libs` 内のサブフォルダーは、標準搭載の AEM 機能を表します。`/libs` 内のコンテンツは変更できません。Web サイトに固有の機能は、`/apps` の下に作成する必要があります。
* `/tmp` - 一時作業領域。
* `/var` - システムによって変更および更新されるファイル監査ログ、統計、イベント処理など。

>[!CAUTION]
>
>この構造、またはその中のファイルの変更は、注意して行う必要があります。変更が及ぼす影響を十分に理解しておく必要があります。
>
>`/libs` パス内のものは一切変更しないでください。設定やその他の変更の場合は、項目を `/libs` から `/apps` にコピーし、`/apps` 内で変更を行います。
