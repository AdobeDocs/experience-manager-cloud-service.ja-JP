---
title: パイプライン不要の URL リダイレクト
description: Git パイプラインまたは Cloud Manager パイプラインにアクセスせずに 301 または 302 リダイレクトを宣言する方法について説明します。
feature: Dispatcher
role: Admin
exl-id: dacb1eda-79e0-4e76-926a-92b33bc784de
source-git-commit: 8f5dd529b5f317326d9742be1dd3a3104fe6957a
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 82%

---

# パイプライン不要の URL リダイレクト {#pipeline-free-redirects}

様々な理由により、組織は 301（または 302）リダイレクトが発生する（ブラウザーが別のページにリダイレクトされる）方法で URL を書き換えます。

次のようなシナリオが含まれます。

* 削除された HTML ページ。ユーザーには `404 Page Not Found` というエラーは表示されず、ユーザーは代替ページ（またはホームページ）に移動します。
* 名前が変更された HTML ページ。
* SEO の最適化。

AEM as a Cloud Service では、クライアントサイドリダイレクトを実装するための[いくつかのアプローチ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/foundation/administration/url-redirection)が提供されますが、この記事で説明するパイプライン不要のリダイレクト戦略は、次の場合に適しています。

* リダイレクトの管理をビジネスユーザーが担当し、ソース管理にファイルの変更をコミットするために必要なアクセス権や、Cloud Manager web 層設定パイプラインを実行する機能を持っていない場合。
* リダイレクトの件数が数件から数万件に及ぶ場合。
* カスタムプロジェクトとして、または [ACS Commons リダイレクトマップマネージャ ](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html) または [ACS Commons リダイレクトマネージャ ](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/subpages/rewritemap.html) を使用して作成したユーザーインターフェイスのオプションが必要な場合。

この機能の中核は、AEM Apache/Dispatcherが、公開リポジトリ内の指定された場所に配置された 1 つ以上の書き換えマップファイルを読み込む（または再読み込みする）機能です（AEM公開からダウンロードできます）。 ファイルがそこに到達する仕組みはこの機能の範囲外ですが、次のいずれかの方法を検討可能であると明記しておくことが重要です。

* 書き換えマップをアセットとしてオーサーユーザーインターフェイスに取り込み、公開します。
* [ACS Commons リダイレクトマップマネージャー](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html)（[バージョン 6.7.0 以降](https://github.com/Adobe-Consulting-Services/acs-aem-commons/releases)）をインストールします。これには、URL マッピングを管理するユーザーインターフェイスが含まれ、書き換えマップファイルを公開することもできます。
* [ACS Commons リダイレクトマネージャー ](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/subpages/rewritemap.html) （[ 少なくとも 6.10.0 バージョン以降 ](https://github.com/Adobe-Consulting-Services/acs-aem-commons/releases)）をインストールすると、URL マッピングを管理するユーザーインターフェイスが含まれ、書き換えマップファイルを公開することもできます。
* カスタムアプリケーションを作成することで、完全な柔軟性を実現します。例えば、URL マッピングを管理するユーザーインターフェイスまたはコマンドラインインターフェイス、あるいは書き換えマップをアップロードするフォームを使用し、その後 AEM API を使用して書き換えマップファイルを公開します。

>[!NOTE]
> この機能には、AEM バージョン **18311 以降**&#x200B;が必要です。

>[!NOTE]
> この機能を使用してリダイレクトマップマネージャを使用する場合、ACS Commons バージョン **6.7.0 以降が必要です。一方** リダイレクトマネージャを使用する場合は、バージョン **6.10.0 以降** が必要です。

## 書き換えマップ {#rewrite-map}

書き換えマップは、（変更した場合）デフォルトでは 300 秒ごとに Apache HTTP サーバーによって再読み込みされます（値は設定可能です)。ファイル形式は、[Apache ドキュメント](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html#txt)に記載されているプレーンテキストのキー値マップ RewriteMap ファイル形式に従う必要があります。

書き換えマップファイルの場所を指定するには、`managed-rewrite-maps.yaml` という名前のファイルを作成し、Cloud Manager フルスタックパイプラインまたは web 層パイプラインを使用して、このファイルを 1 回デプロイする必要があります。 ファイルは、Dispatcher 設定の [src/opt-in](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud/src/opt-in) フォルダーに作成する必要があります。必ず[フレキシブルモードのファイル構造](/help/implementing/dispatcher/validation-debug.md#flexible-mode-file-structure)を使用してください。

次のパターンで設定できます。

```
maps:
- name: my.map
  path: <path-in-publish-repository>/redirectmap.txt
```

例えば、書き換えマップファイルを配置する際に `mysite-redirectmap.txt` という名前のアセットとして AEM に取り込んでから公開する場合は、`/content/dam` の下にあるフォルダーを指定できます。

```
maps:
- name: my.map
  path: /content/dam/redirectmaps/mysite-redirectmap.txt
```

次に、`rewrites/rewrite.rules` や `<yourfile>.vhost` などの Apache 設定ファイルで、name プロパティによって参照されるマップファイル（上記のサンプルでは `my.map`）を設定する必要があります。読み込まれると、このマップファイルは、**固定**&#x200B;場所`/tmp/rewrites/`の下の Dispatcher ローカルストレージに保存されます。

`RewriteMap` ディレクティブは、データが `sdbm`（シンプル DBM）形式を使用してデータベースマネージャー（DBM）ファイル形式で保存され、ファイルのフルパスは保存場所の接頭辞と name プロパティから導出されることを示す必要があります。

残りの設定は、`redirectmap.txt` の形式によって異なります。最もシンプルな形式は、以下のサンプルに示すように、元の URL とマッピングされた URL を 1 対 1 でマッピングしたものです。

```
# RewriteMap from managed rewrite maps
RewriteMap map.foo dbm=sdbm:/tmp/rewrites/my.map
RewriteCond ${map.foo:$1} !=""
RewriteRule ^(.*)$ ${map.foo:$1|/} [L,R=301]
```


## 考慮事項 {#considerations}

次の点に注意してください。

* デフォルトでは、書き換えマップを読み込むする際、Apache は完全なマップファイルが読み込まれるのを待たずに起動するので、完全なマップが読み込まれるまで一時的に不整合が発生する可能性があります。この設定を変更すると、Apache は完全なマップコンテンツが読み込まれるまで待機しますが、Apache の起動により長い時間がかかります。Apache が待機するようにこの動作を変更するには、`managed-rewrite-maps.yaml` ファイルに `wait:true` を追加します。
* 読み込み間の頻度を変更するには、`managed-rewrite-maps.yaml` ファイルに `ttl: <integer>` を追加します。例：`ttl: 120`。
* Apache では、RewriteMap の単一エントリの長さに 1024 の制限があります。
