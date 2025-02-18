---
title: AEM のユニバーサルエディターの概要
description: ユニバーサルエディターへのアクセス権を取得する方法と、これを使用するために最初の AEM アプリのインストルメントを開始する方法について説明します。
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 0ee6689460ac0ecc5c025fb6a940d69a16699c85
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 100%

---


# AEM のユニバーサルエディターの概要 {#getting-started}

ユニバーサルエディターへのアクセス権を取得する方法と、これを使用するために最初の AEM アプリのインストルメントを開始する方法について説明します。

>[!TIP]
>
>すぐに例を確認したい場合は、[GitHub のユニバーサルエディターサンプルアプリ](https://github.com/adobe/universal-editor-sample-editable-app)を参照してください。

ユニバーサルエディターは任意のソースからコンテンツを編集できますが、このドキュメントでは AEM アプリを例として使用します。 このドキュメントでは、これらの手順を説明します。

## ページの実装 {#instrument-page}

ユニバーサルエディターでは、エディターでページをレンダリングおよび編集するために JavaScript ライブラリが必要です。

さらに、ユニバーサルエディターサービスでは、編集中のアプリ内のコンテンツに適したバックエンドシステムを識別して使用するために、[統一リソース名（URN）](https://ja.wikipedia.org/wiki/Uniform_Resource_Name)が必要です。 したがって、コンテンツをコンテンツリソースにマッピングし直すには、URN スキーマが必要です。

### ユニバーサルエディター CORS ライブラリを含める {#cors-library}

ユニバーサルエディターをアプリに接続するには、アプリにユニバーサルエディター CORS ライブラリを含める必要があります。 アプリに次のスクリプトを追加します。

```html
 <script src="https://universal-editor-service.adobe.io/cors.js" async></script>
```

### 接続の作成 {#connections}

アプリで使用する接続は、ページの `<head>` 内に `<meta>` タグとして格納されます。

```html
<meta name="urn:adobe:aue:<category>:<referenceName>" content="<protocol>:<url>">
```

* `<category>` - これは、2 つのオプションを持つ接続の分類です。
   * `system` - 接続エンドポイントの場合
   * `config` - [オプション設定の定義](#configuration-settings)の場合
* `<referenceName>` - 接続を識別するためにドキュメントで再利用される短い名前です。 例：`aemconnection`
* `<protocol>` - 使用するユニバーサルエディター永続化サービスの永続化プラグインを示します。 例：`aem`
* `<url>` - 変更が保持されるシステムの URL です。 例：`http://localhost:4502`

識別子 `urn:adobe:aue:system` は、Adobe Universal Editor の接続を表します。

`data-aue-resource` は `urn` プレフィックスを使用して識別子を短縮します。

```html
data-aue-resource="urn:<referenceName>:<resource>"
```

* `<referenceName>` - `<meta>` タグに記載されている名前付きリファレンスです。 例：`aemconnection`
* `<resource>` - ターゲットシステム内のリソースへのポインターです。 例：`/content/page/jcr:content` などの AEM コンテンツのパス

>[!TIP]
>
>ユニバーサルエディターが必要とするデータ属性とタイプについて詳しくは、ドキュメント[属性とタイプ](attributes-types.md)を参照してください。

### 接続例 {#example}

```html
<meta name="urn:adobe:aue:system:<referenceName>" content="<protocol>:<url>">

<html>
<head>
    <meta name="urn:adobe:aue:system:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:adobe:aue:system:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul data-aue-resource="urn:aemconnection:/content/example/list" data-aue-type="container">
            <li data-aue-resource="urn:aemconnection:/content/example/listitem" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">Jane Doe</p>
              <p data-aue-prop="title" data-aue-type="text">Journalist</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>

...

            <li data-aue-resource="urn:fcsconnection:/documents/mytext" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">John Smith</p>
              <p data-aue-resource="urn:aemconnection:/content/example/another-source" data-aue-prop="title" data-aue-type="text">Photographer</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

### 設定 {#configuration-settings}

接続 URN で `config` プレフィックスを使用して、必要に応じてサービスおよび拡張エンドポイントを設定します。

アドビがホストするユニバーサルエディターサービスを使用しない場合は、これはメタタグで設定できます。 ユニバーサルエディターが提供するデフォルトのサービスエンドポイントを上書きするには、独自のサービスエンドポイントを設定します。

* メタ名 - `urn:adobe:aue:config:service`
* メタコンテンツ - `content="https://adobe.com"`（例）

```html
<meta name="urn:adobe:aue:config:service" content="<url>">
```

ページに対して特定の拡張機能のみを有効にしたい場合は、メタタグで設定できます。 拡張機能を取得するには、拡張機能エンドポイントを設定します。

* メタ名：`urn:adobe:aue:config:extensions`
* メタコンテンツ：`content="https://adobe.com,https://anotherone.com,https://onemore.com"`（例）

```html
<meta name="urn:adobe:aue:config:extensions" content="<url>,<url>,<url>">
```

## ユニバーサルエディターを開くコンテンツパスまたは `sling:resourceType` の定義 （オプション） {#content-paths}

[ページエディター](/help/sites-cloud/authoring/page-editor/introduction.md)を使用する既存の AEM プロジェクトがある場合、コンテンツ作成者がページを編集する際に、ページはページエディターで自動的に開かれます。コンテンツパスまたは `sling:resourceType` に基づいて AEM が開くエディターを定義できるので、選択したコンテンツに必要なエディターに関係なく、作成者にとってシームレスなエクスペリエンスを実現できます。

1. Configuration Manager を開きます。

   `http://<host>:<port>/system/console/configMgr`

1. リストで&#x200B;**ユニバーサルエディター URL サービス**&#x200B;を見つけて、「**設定値を編集**」をクリックします。

1. ユニバーサルエディターを開くコンテンツパスまたは `sling:resourceType` を定義します。

   * 「**ユニバーサルエディターを開くマッピング**」フィールドに、ユニバーサルエディターを開くパスを指定します。
   * 「**ユニバーサルエディターで開く Sling:resourceTypes**」フィールドに、ユニバーサルエディターによって直接開かれるリソースのリストを指定します。

1. 「**保存**」をクリックします。

AEM は、この設定に基づいて、次の順序でページのユニバーサルエディターを開きます。

1. AEM は `Universal Editor Opening Mapping` の下にあるマッピングを確認し、コンテンツがそこに定義されているパスの下にある場合は、ユニバーサルエディターが開かれます。
1. `Universal Editor Opening Mapping` で定義されたパスの下にないコンテンツの場合、AEM はコンテンツの `resourceType` が、**ユニバーサルエディターで開かれる Sling:resourceTypes**&#x200B;で定義されたものと一致するかどうかを確認し、コンテンツがこれらのタイプのいずれかに一致する場合は、`${author}${path}.html` でユニバーサルエディターが開かれます。
1. それ以外の場合は、AEM によってページエディターが開かれます。

「**ユニバーサルエディターを開くマッピング**」フィールドでマッピングを定義するには、次の変数を使用できます。

* `path`：開くリソースのコンテンツパス
* `localhost`：スキーマなしの `localhost` の Externalizer エントリ（例：`localhost:4502`）
* `author`：スキーマなしのオーサーの Externalizer エントリ（例：`localhost:4502`）
* `publish`：スキーマなしのパブリッシュの Externalizer エントリ（例：`localhost:4503`）
* `preview`：スキーマなしのプレビューの Externalizer エントリ（例：`localhost:4504`）
* `env`：定義された Sling 実行モードに基づく `prod`、`stage`、`dev`
* `token`：`QueryTokenAuthenticationHandler` に必要なクエリトークン

### マッピングの例 {#example-mappings}

* AEM オーサーの `/content/foo` の下にあるすべてのページを開きます。

   * `/content/foo:${author}${path}.html?login-token=${token}`
   * これにより、`https://localhost:4502/content/foo/x.html?login-token=<token>` が開きます。

* リモート NextJS サーバー上の `/content/bar` の下にあるすべてのページを開き、すべての変数を情報として指定します。

   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * これにより、`https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>` が開きます。

## ユニバーサルエディターを使用する準備が整いました {#youre-ready}

ユニバーサルエディターを使用するようにアプリのインストルメントが行われました。

コンテンツ作成者が簡単かつ直感的にユニバーサルエディターを使用してコンテンツを作成する方法について詳しくは、[ユニバーサルエディターを使用したコンテンツの作成](/help/sites-cloud/authoring/universal-editor/authoring.md)を参照してください。

## その他のリソース {#additional-resources}

ユニバーサルエディターの詳細については、次のドキュメントを参照してください。

* [ユニバーサルエディターの概要](introduction.md) - ユニバーサルエディターを使用して、優れたエクスペリエンスを提供し、コンテンツベロシティを向上させ、最新のデベロッパーエクスペリエンスを提供するために、あらゆる実装、あらゆるコンテンツ、あらゆる側面の編集を可能にする方法を説明します。
* [ユニバーサルエディターを使用したコンテンツのオーサリング](/help/sites-cloud/authoring/universal-editor/authoring.md) - コンテンツ作成者がユニバーサルエディターを使用して、簡単かつ直感的にコンテンツを作成する方法について説明します。
* [ユニバーサルエディターを使用したコンテンツの公開](/help/implementing/universal-editor/publishing.md) - ユニバーサルエディターでのコンテンツの公開方法と、アプリでの公開済みコンテンツの処理方法を説明します。
* [ユニバーサルエディターのアーキテクチャ](architecture.md) - ユニバーサルエディターのアーキテクチャと、そのサービスとレイヤー間でのデータのフローについて説明します。
* [属性とタイプ](attributes-types.md) - ユニバーサルエディターで必要なデータ属性とデータ型について説明します。
* [ユニバーサルエディターの認証](authentication.md) - ユニバーサルエディターの認証方法について説明します。

