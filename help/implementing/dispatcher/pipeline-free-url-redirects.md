---
title: パイプラインを使用しない URL リダイレクト
description: Git パイプラインまたはCloud Manager パイプラインにアクセスせずに 301 または 302 リダイレクトを宣言する方法を説明します。
feature: Dispatcher
role: Admin
source-git-commit: 567c75f456f609dbc254753b439151d0f4100bc0
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# パイプラインを使用しない URL リダイレクト {#pipeline-free-redirects}

>[!NOTE]
>この機能はまだリリースされていません。

様々な理由で、組織は 301 （または 302）リダイレクトを引き起こす方法で URL を書き換えます。つまり、ブラウザーは別のページにリダイレクトされます。

次のようなシナリオが考えられます。

* 削除されたHTMLページ。これにより、`404 Page Not Found` しいエラーが表示されずに代替ページ（場合によってはホームページ）に移動します。
* 名前が変更されたHTMLページ。
* SEO の最適化

AEM as a Cloud Serviceには、クライアントサイドのリダイレクトを実装する [ いくつかのアプローチ ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/url-redirection) がありますが、この記事で説明する方法である、パイプラインを使用しないリダイレクトは、次の場合に適しています。

* リダイレクトを管理するのはビジネスユーザーで、ファイルの変更をソース管理にコミットするために必要なアクセス権限を持たない人、またはCloud Managerの web 階層設定パイプラインを実行できない人です。
* リダイレクトの数は数から数万の範囲です。
* カスタムプロジェクトとして作成するか、[ACS Commons 書き換えマップマネージャ ](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html?lang=ja) を使用して作成する、ユーザーインターフェイスのオプションが必要な場合。

この機能の中核は、AEM Apache/Dispatcherがパブリッシュリポジトリー内の指定された場所に配置された 1 つ以上の書き換えマップファイルを読み込む（または再読み込む）機能です。 ファイルがそこにどのように配置されるかについては、この機能の範囲外であることに注意が必要ですが、次のいずれかの方法を検討できます。

* 書き換えマップをオーサーユーザーインターフェイスでアセットとして取り込み、公開します。
* [ACS Commons 書き換えマップマネージャ ](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html?lang=ja) のインストール。この中には、URL マッピングを管理するユーザーインターフェイスが含まれており、書き換えマップファイルを公開することもできます。
* カスタムアプリケーションを作成することで、高い柔軟性を実現します。 例えば、URL マッピングを管理するユーザーインターフェイスまたはコマンドラインインターフェイス、または書き換えマップをアップロードするフォームで、AEM API を使用して書き換えマップファイルを公開します。

>[!NOTE]
> この機能を使用するには、AEM バージョン **18311 以降が必要** す。

## 書き換えマップ {#rewrite-map}

書き換えマップは、デフォルトでは 300 秒ごとに Apache HTTP サーバーによって再読み込み（変更された場合）されます（値は設定可能）。 ファイル形式は、[Apache ドキュメント ](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html#txt) に記載されているプレーンテキストのキー値マップの RewriteMap ファイル形式に従う必要があります。

書き換えマップファイルの場所を指定する `managed-rewrite-maps.yaml` という名前のファイルを作成し、Cloud Manager フルスタックパイプラインまたは web 階層パイプラインを使用して、1 回デプロイする必要があります。 ファイルは、Dispatcher 設定の [src/opt-in](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud/src/opt-in) フォルダーに作成する必要があります。 必ず [ フレキシブルモードファイル構造 ](/help/implementing/dispatcher/validation-debug.md#flexible-mode-file-structure) を使用してください。

次のパターンで設定できます。

```
maps:
- name: my.map
  path: <path-in-publish-repository>/redirectmap.txt
```

例えば、書き換えマップファイルを配置する方法を選択して、AEMに `mysite-redirectmap.txt` という名前のアセットとして取り込んで公開する場合は、`/content/dam` の下にフォルダーを指定できます。

```
maps:
- name: my.map
  path: /content/dam/redirectmaps/mysite-redirectmap.txt
```

次に、`rewrites/rewrite.rules` や `<yourfile>.vhost` などの Apache 設定ファイルで、name プロパティによって参照されるマップファイルを設定する必要があります（上記のサンプルの `my.map`。

`RewriteMap` ディレクティブは、データが `sdbm` （単純 DBM）形式を使用してデータベース・マネージャ（DBM）ファイル形式で格納されることを示す必要があります。

残りの設定は、`redirectmap.txt` の形式によって異なります。 最も単純な形式は、以下のサンプルに示すように、元の URL とマッピングされた URL を 1 対 1 でマッピングするものです。

```
# RewriteMap from managed rewrite maps
RewriteMap map.foo dbm=sdbm:/tmp/rewrites/my.map
RewriteCond ${map.foo:$1} !=""
RewriteRule ^(.*)$ ${map.foo:$1|/} [L,R=301]
```


## 考慮事項 {#considerations}

次の点に注意してください。

* デフォルトでは、書き換えマップを読み込む場合、完全なマップファイルが読み込まれるのを待たずに Apache が起動します。そのため、完全なマップが読み込まれるまでの間に一時的な不整合が生じる場合があります。 この設定を変更すると、マップの内容がすべて読み込まれるのを Apache が待ちますが、Apache の起動にはより長い時間がかかります。 Apache が待機するようにこの動作を変更するには、`managed-rewrite-maps.yaml` ファイルに `wait:true` を追加します。
* 負荷間の頻度を変更するには、`managed-rewrite-maps.yaml` ファイルに `ttl: <integer>` を追加します。 例：`ttl: 120`
* Apache には、RewriteMap 単一エントリに対して 1024 長の制限があります。
