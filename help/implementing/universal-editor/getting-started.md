---
title: AEMのユニバーサルエディターの概要
description: ユニバーサルエディターへのアクセス権を取得する方法と、それを使用する最初のAEMアプリの実装を開始する方法について説明します。
source-git-commit: acafa752c354781e41b11e46ac31a59feb8d94e7
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---


# AEMのユニバーサルエディターの概要 {#getting-started}

ユニバーサルエディターへのアクセス権を取得する方法と、それを使用する最初のAEMアプリの実装を開始する方法について説明します。

>[!TIP]
>
>例に目を通したい場合は、 [GitHub のユニバーサルエディターサンプルアプリ。](https://github.com/adobe/universal-editor-sample-editable-app)

## オンボーディング手順 {#onboarding}

ユニバーサルエディターは任意のソースからコンテンツを編集できますが、このドキュメントではAEMアプリを例として使用します。

AEMアプリをオンボーディングし、ユニバーサルエディターを使用するために実装する手順はいくつかあります。

1. [ユニバーサルエディターへのアクセスをリクエストします。](#request-access)
1. [ユニバーサルエディターのコアライブラリを含めます。](#core-library)
1. [必要な OSGi 設定を追加します。](#osgi-configurations)
1. [ページを実装します。](#instrument-page)

このドキュメントでは、これらの手順を説明します。

## ユニバーサルエディターへのアクセスのリクエスト {#request-access}

最初にユニバーサルエディターへのアクセスをリクエストする必要があります。 次に進んでください： [https://experience.adobe.com/#/aem/editor](https://experience.adobe.com/#/aem/editor) ユニバーサルエディターにアクセスできるかどうかを検証します。

アクセス権がない場合は、同じページにリンクされたフォームからリクエストできます。

## ユニバーサルエディターコアライブラリを含める {#core-library}

アプリをユニバーサルエディターで使用するために実装する前に、次の依存関係を含める必要があります。

```javascript
@adobe/universal-editor-cors
```

計測機能を有効にするには、次のインポートを `index.js`.

```javascript
import "@adobe/universal-editor-cors";
```

### 非 React アプリの代替 {#alternative}

React アプリを実装していない場合や、サーバーサイドでのレンダリングが必要な場合、ドキュメント本文に次の情報を含める方法があります。

```html
<script src="https://cdn.jsdelivr.net/gh/adobe/universal-editor-cors/dist/universal-editor-embedded.js" async></script>
```

## 必要な OSGi 設定の追加 {#osgi-configurations}

ユニバーサルエディターを使用してAEMコンテンツをアプリで編集するには、AEM内で CORS と Cookie の設定をおこなう必要があります。

以下 [OSGi 設定は、AEMオーサリングインスタンスで設定する必要があります。](/help/implementing/deploying/configuring-osgi.md)

* `SameSite Cookies = None`in `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`
* X-FRAME-RemoveOPTIONS:の SAMEORIGIN ヘッダー `org.apache.sling.engine.impl.SlingMainServlet`

### com.day.crx.security.token.impl.impl.TokenAuthenticationHandler {#samesite-cookies}

ログイントークン cookie は、サードパーティドメインとしてAEMに送信する必要があります。 したがって、SameSite cookie をに明示的に設定する必要があります。 `None`.

このプロパティは、 `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler` OSGi 設定。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
          token.samesite.cookie.attr="None" />
```

### org.apache.sling.engine.impl.SlingMainServlet {#sameorigin}

X-Frame-Options:SAMEORIGIN は、iframe 内でAEMページをレンダリングできないようにします。 ヘッダーを削除すると、ページを読み込むことができます。

このプロパティは、 `org.apache.sling.engine.impl.SlingMainServlet` OSGi 設定。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0"
          jcr:primaryType="sling:OsgiConfig"
          sling.additional.response.headers="[X-Content-Type-Options=nosniff]"/>
```

## ページの実装 {#instrument-page}

Universal Editor サービスには、 [URN (Uniform Resource Name)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) 編集中のアプリ内のコンテンツに対して正しいバックエンドシステムを識別し、利用する。 したがって、コンテンツをコンテンツリソースにマッピングし直すには、URN スキーマが必要です。

ページに追加される計測属性は、主に [HTMLマイクロデータ、](https://developer.mozilla.org/en-US/docs/Web/HTML/Microdata) HTMLをより意味的にし、HTMLドキュメントをインデックス付け可能にするなどにも使用できる業界標準

### 接続の作成 {#connections}

アプリで使用される接続は、 `<meta>` ページの `<head>`.

```html
<meta name="urn:auecon:<referenceName>" content="<protocol>:<url>">
```

* `<referenceName>`  — これは、接続を識別するためにドキュメントで再利用される短い名前です。 例： `aemconnection`
* `<protocol>`  — 使用する Universal Editor Persistence Service の永続化プラグインを示します。 例： `aem`
* `<url>`  — 変更が保持されるシステムへの URL です。 例： `http://localhost:4502`

短い識別子 `auecon` は、Universal Editor ConnectionAdobeの略です。

`itemid`が `urn` プレフィックスを使用して識別子を短縮します。

```html
itemid="urn:<referenceName>:<resource>"
```

* `<referenceName>`  — これは、 `<meta>` タグを使用します。 例： `aemconnection`
* `<resource>`  — ターゲットシステム内のリソースへのポインタです。 例：AEMコンテンツのパス `/content/page/jcr:content`

>[!TIP]
>
>ドキュメントを参照 [属性とタイプ](attributes-types.md) に、ユニバーサルエディターで必要なデータ属性とタイプの詳細を示します。

### 接続例 {#example}

```html
<html>
<head>
    <meta name="urn:auecon:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:auecon:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="container">
            <li itemscope itemid="urn:aemconnection/content/example/listitem" itemtype="component">
              <p itemprop="name" itemtype="text">Jane Doe</p>
              <p itemprop="title" itemtype="text">Journalist</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
 
...
 
            <li itemscope itemid="urn:fcsconnection:/documents/mytext" itemtype="component">
              <p itemprop="name" itemtype="text">John Smith</p>
              <p itemid="urn:aemconnection/content/example/another-source" itemprop="title" itemtype="text">Photographer</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

### ユニバーサルエディター翻訳サービス {#translation}

ユニバーサルエディタは、計測メタデータに基づいて翻訳を実行します。

#### 基本翻訳の原則 {#principle}

前の例の次の選択について考えてみましょう。

```html
<meta name="urn:auecon:aemconnection" content="aem:https://localhost:4502">
<ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="urn:fcs:type/list">
```

エディターは置き換えを実行し、内部的に `itemid` が次のように書き換えられます。

```html
itemid="urn:aem:https://localhost:4502/content/example/list"
```

これは、「 `aemconnection` 次の内容に置き換えられる： `<meta>` タグを使用します。

#### クエリセレクター {#query-selector}

この置き換えにより、John Smith の次のクエリ文字列が生成されます。

```html
<ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="urn:fcs:type/list">
  <li itemscope itemid="urn:fcsconnection:/documents/mytext" itemtype="urn:fcs:type/fragment">.  
    <p itemprop="name" itemtype="text">John Smith</p>
    <p itemid="urn:aemconnection/content/example/another-source" itemprop="title" itemtype="text">Photographer</p>
    <img itemprop="avatar" src="urn:fcs:missing" itemtype="image" alt="avatar"/>
  </li>
```

`[itemid="urn:fcs:https://example.franklin.adobe.com/345fcdd/content/example/list][itemprop="name"]`

John Smith のタイルを変更する場合、セレクターは次のようになります。

`[itemid="urn:aem:https://localhost:4502/content/example/another-source"][itemprop="title"]`

の継承の代わりに `itemid`およびリソースの場合、ユニバーサルエディタはスコープと連携します。 スコープは、ノードレベルで定義でき、サブ構造全体で継承されます。

構造内のサブ構造または定義された休暇に異なるスコープが必要な場合は、別の `itemid` を定義できます。

## ユニバーサルエディターを使用する準備が整いました {#youre-ready}

アプリがユニバーサルエディターを使用するように実装されました。

ドキュメントを参照してください [ユニバーサルエディターを使用したコンテンツのオーサリング](authoring.md) コンテンツ作成者がユニバーサルエディターを使用してコンテンツを作成する際に、簡単で直感的な方法を学習します。

## その他のリソース {#additional-resources}

ユニバーサルエディターの詳細については、次のドキュメントを参照してください。

* [ユニバーサルエディターの概要](introduction.md)  — ユニバーサルエディターを使用して、優れたエクスペリエンスを提供し、コンテンツ速度を向上し、最新の開発者エクスペリエンスを提供するために、あらゆる実装のコンテンツのあらゆる側面を編集できる方法を説明します。
* [ユニバーサルエディターを使用したコンテンツのオーサリング](authoring.md)  — コンテンツ作成者がユニバーサルエディターを使用してコンテンツを作成するのが、簡単で直感的な方法について説明します。
* [ユニバーサルエディターのアーキテクチャ](architecture.md)  — ユニバーサルエディターのアーキテクチャと、そのサービスとレイヤー間でのデータのフローについて説明します。
* [属性とタイプ](attributes-types.md)  — ユニバーサルエディターで必要なデータ属性とデータ型について説明します。
* [ユニバーサルエディタ認証](authentication.md)  — ユニバーサルエディターの認証方法を説明します。
