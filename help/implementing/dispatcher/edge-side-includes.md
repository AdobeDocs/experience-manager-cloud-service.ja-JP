---
title: エッジ側インクルード
description: Adobeが管理する CDN で、エッジレベルの動的 web コンテンツアセンブリ用のマークアップ言語であるエッジサイドインクルード（ESI）がサポートされるようになりました。
feature: Dispatcher
source-git-commit: 3aab5d3beb7bedf7a61bc557be349f2aa5ed8a7b
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 4%

---

# エッジ側インクルード {#edge-side-includes}

>[!NOTE]
>この機能はまだ一般提供されていません。早期導入プログラムに参加するには、`aemcs-cdn-config-adopter@adobe.com` にメールを送信し、ユースケースを説明します。

コンテンツ配信速度は、ページを積極的にキャッシュすることでメリットが得られます。これは、Time to Live （TTL）の値を大きくしたキャッシュヘッダーを設定することで達成できます。 ページに動的コンテンツが含まれている場合、これは困難になる可能性があります。動的コンテンツは、頻繁に更新する必要があるか、キャッシュできない可能性があります。 幸いにも、含まれるHTMLページを高い TTL でキャッシュして、クライアントサイド JavaScript または CDN を使用して、より動的なコンテンツスニペットの取得を後で延期する戦略があります。 後者のアプローチは、エッジサイドインクルード （ESI）と呼ばれる標準であり、AEM公開でレンダリングされるサイトに対してサポートされます。 HTMLには ESI タグが含まれており、CDN は、これらのタグを評価するまでページの提供をブラウザーに延期し、オリジン（または TTL が期限切れでない場合は CDN キャッシュ）から追加のより動的な（低い TTL）コンテンツを取得するように指示します。

エッジサイドインクルードが役立つ可能性のあるユースケースを次に示します。

* エンドユーザーの名前、またはエンドユーザーに固有のその他の情報を表示する。
* ニュース記事や株価などの最近の情報のリストを表示します。

## ESI 構文 {#esi-syntax}

ESI 構文は、親ページの場合、次のようになります `/content/page.html` スニペットを含む `content/snippets/mysnippet.html`.

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

を参照してください。 [ESI 仕様](https://www.w3.org/TR/esi-lang/) を参照してください。

### 検討事項（#esi-syntax-considerations}

* 次の ESI タグ（include、comment、remove）がサポートされています。
* ESI タグは、同時ではなく CDN で順番に処理されるので、TTL の低いページに多くの ESI タグがあると、エンドユーザーのエクスペリエンスに遅延が生じる可能性があります。
* ESI:include 処理の最大深度は 5 です。
* ESI:include 処理フラグメントの最大合計は 256 です。


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

設定済みのプロパティには、次の動作があります。

| プロパティ | 動作 |
|-----------|--------------------------|
| **no-gzip** | 1 に設定すると、HTMLページが Apache から CDN に非圧縮で送信されます。 CDN が ESI タグを表示および評価できるように、コンテンツを圧縮せずに CDN に送信する必要があるので、ESI に必要です。<br/><br/>親ページと含まれているスニペットの両方で、no-gzip を 1 に設定する必要があります。<br/><br/>この設定は、リクエストのに基づいて、Apache が使用していた圧縮設定を上書きします。 `Accept-Encoding` 値。 |
| **x-aem-esi** | 「on」に設定すると、CDN は親HTMLページの ESI タグを評価します。  デフォルトでは、ヘッダーは設定されていません。 |
| **x-aem-compress** | 「on」に設定すると、CDN は CDN からブラウザーにコンテンツを圧縮します。 ESI が機能するには、親ページの Apache から CDN への送信を非圧縮（no-gzip を 1 に設定）にする必要があるので、待ち時間を短縮できます。<br/><br/>このヘッダーが設定されていない場合、CDN が圧縮されていないオリジンからコンテンツを取得する際に、圧縮されていないクライアントにもコンテンツが提供されます。 したがって、no-gzip が 1 に設定されている場合（ESI で必要）、このヘッダーを設定する必要があり、CDN からブラウザーに圧縮されたコンテンツを提供することが必要です。 |

## Sling Dynamic Include {#esi-sdi}

必須ではありませんが、 [Sling Dynamic Include](https://sling.apache.org/documentation/bundles/dynamic-includes.html) （SDI）を使用して、CDN で解釈される ESI スニペットを生成できます。

