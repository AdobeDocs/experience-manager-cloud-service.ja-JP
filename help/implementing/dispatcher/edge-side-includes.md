---
title: エッジサイドインクルード
description: アドビが管理する CDN で、エッジレベルの動的 web コンテンツアセンブリ用のマークアップ言語であるエッジサイドインクルード（ESI）がサポートされるようになりました。
feature: Dispatcher
exl-id: 35093477-2788-4f69-80a9-899f43567cae
role: Admin
source-git-commit: d70a8030ca6687b1839adc0ce1becdf366ec7170
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# エッジサイドインクルード {#edge-side-includes}

コンテンツ配信速度は、ページを積極的にキャッシュすることで向上します。これは、キャッシュヘッダーの有効期間（TTL）の値を高く設定することで実現されます。ページに動的コンテンツが含まれていて、頻繁に更新する必要があるか、全くキャッシュできない可能性がある場合、これは困難になる可能性があります。幸いにも、含まれる HTML ページを高い TTL でキャッシュして、クライアントサイドの JavaScript または CDN を使用して、より動的なコンテンツスニペットの取得を後回しにする戦略があります。後者のアプローチは、エッジサイドインクルード（ESI）と呼ばれる標準的な手法で、AEM 公開でレンダリングされたサイトでサポートされています。HTML には ESI タグが含まれており、CDN はブラウザーにページを配信する前にこれらのタグを分析し、オリジン（または TTL が期限切れでない場合は CDN キャッシュ）から追加のより動的な（低い TTL）コンテンツを取得するように指示します。

エッジサイドインクルードが役立つ可能性のあるユースケースを次に示します。

* エンドユーザーの名前、またはエンドユーザーに固有のその他の情報を表示する。
* ニュース記事や株価などの最新情報のリストを表示する。

## ESI 構文 {#esi-syntax}

親ページに`/content/page.html`スニペットが含まれる`content/snippets/mysnippet.html`場合、ESI 構文は次のようになります。

```
<html>
  <head>
      <title>My Site</title>
  </head>
  <body>
    <div id="content">
      <esi:include src="/content/snippets/mysnippet.html" />
    </div>
  </body>
</html>
```

詳しくは、[ESI の仕様](https://www.w3.org/TR/esi-lang/)を参照してください。

### 考慮事項 {#esi-syntax-considerations}

* サポートされている ESI タグは、include、comment、remove です。
* ESI タグは、CDN で同時ではなく順番に処理されるので、TTL が低いページに多数の ESI タグがあると、エンドユーザーのエクスペリエンスに遅延が生じる可能性があります。
* ESI インクルード処理の最大深度は 5 です。
* ESI インクルード処理フラグメントの最大合計は 256 です。


## Apache 設定 {#esi-apache}

ESI タグを含むページがある場合は、Apache 設定で次のプロパティを宣言する必要があります。

```
<LocationMatch "/parent-pages/*content/page.html">
   # disable dispatcher compression
   SetEnv no-gzip 1
   # enable esi processing 
   Header set x-aem-esi "on"
   # enable edgeCDN compression
   Header set x-aem-compress "on"

   # typically the main page is cached at the CDN
   Header always set Cache-Control "max-age=300"
 </LocationMatch>


<LocationMatch "/content/snippets/mysnippet.html">
  SetEnv no-gzip 1

  # typically the included page is either set to a lower TTL than the parent page, or not cached at all, as these 2 commented declarations show, respectively:
  #Header always set Cache-Control "no-cache"
  #Header always set Cache-Control "max-age=50"
 </LocationMatch> 
```

設定済みのプロパティは次のような動作をします。

| プロパティ | 動作 |
|-----------|--------------------------|
| **no-gzip** | 1 に設定すると、HTML ページは非圧縮で Apache から CDN に送信されます。これは ESI を使用するために必須です。CDN が ESI タグを認識して評価できるように、コンテンツを圧縮せずに CDN に送信する必要があるためです。<br/><br/>親ページと含まれているスニペットの両方で、no-gzip を 1 に設定する必要があります。<br/><br/>この設定は、リクエストの `Accept-Encoding` 値に基づいて、Apache が使用していた圧縮設定を上書きします。 |
| **x-aem-esi** | 「オン」に設定すると、CDN は親 HTML ページの ESI タグを評価します。デフォルトでは、ヘッダーは設定されていません。 |
| **x-aem-compress** | 「オン」に設定すると、CDN は コンテンツを圧縮してブラウザーに送信します。ESI が機能するには親ページを圧縮せずに（`no-gzip` を 1 に設定）Apache から CDN に送信する必要があるので、このことが待ち時間の短縮につながります。<br/><br/>このヘッダーが設定されていないと、CDN がオリジンから非圧縮のコンテンツを取得した場合、クライアントにも非圧縮のコンテンツが提供されます。したがって、`no-gzip` が 1 に設定されていて（ESI で必須）、圧縮されたコンテンツを CDN からブラウザーに提供する必要がある場合は、このヘッダーを設定する必要があります。 |

## Sling Dynamic Include {#esi-sdi}

必須ではありませんが、[Sling Dynamic Include](https://sling.apache.org/documentation/bundles/dynamic-includes.html)（SDI）を使用して、CDN で解釈される ESI スニペットを生成できます。
