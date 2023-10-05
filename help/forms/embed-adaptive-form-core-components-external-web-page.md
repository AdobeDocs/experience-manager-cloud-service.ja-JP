---
title: コアコンポーネントに基づくアダプティブフォームを外部 Web ページに埋め込むにはどうすればよいですか？
description: Web サイトにアダプティブFormsを埋め込む方法を説明します。
contentOwner: Khushwant Singh
docset: CloudService
role: Developer
exl-id: 198f6f76-1134-4818-89a0-6ddc84ff956c
source-git-commit: 2d4a81aa0d6755270d4d6efb8649782f4bde4537
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 62%

---

# コアコンポーネントに基づいたアダプティブフォームを外部 Web ページに埋め込む {#embed-adaptive-form-in-external-web-page}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | この記事 |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html?lang=ja) |


AEM の外側にホストされた Web ページか [AEM Sites ページに、アダプティブフォームをシームレスに埋め込む](/help/forms/embed-adaptive-form-aem-sites.md)ことができます。埋め込まれたアダプティブフォームではすべての機能を使用できるので、ユーザーは、ページから移動することなくフォームを記入および送信できます。これにより、ユーザーは web ページの他の要素から離れることなく、同時にフォームの操作も行うことができます。

## 前提条件 {#prerequisites}

アダプティブフォームを外部 Web サイトに埋め込む前に、次の手順を実行します

* AEM Forms サーバーのパブリッシュインスタンスに埋め込むアダプティブフォームを公開します。
* Web サイト上で、アダプティブフォームをホストする Web ページを作成するか、特定してください。その Web ページが [CDN から送信される jQuery ファイルを読み取ることができること](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js)、または web ページに jQuery のローカルコピーが埋め込まれていることを確認してください。jQuery は、アダプティブフォームのレンダリングに必要です。
* AEM サーバーと web ページが異なるドメイン上に存在する場合、[AEM Forms がクロスドメインサイトに対してアダプティブフォームをサーブできるようにする](#cross-site)節に記載された手順を実行してください。

## アダプティブフォームの埋め込み {#embed-adaptive-form}

Web ページに数行の JavaScript を挿入することで、アダプティブフォームを埋め込むことができます。コードの API は AEM サーバーにアダプティブフォームのリソースを求める HTTP リクエストを送信し、指定したフォームコンテナにアダプティブフォームを挿入します。

アダプティブフォームを埋め込むには、以下のようにします。

1. 次のコードを使用して、web サイト上に web ページを作成します。

   ```html
        <!doctype html>
        <html>
          <head>
            <title>This is the title of the webpage!</title>
            <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
          </head>
          <body>
          <div class="customafsection"/>
            <p>This section is replaced with the adaptive form.</p>
   
         <script>
         var options = {path:"/content/forms/af/myadaptiveform.html", CSS_Selector:".customafsection"};
         alert(options.path);
         var loadAdaptiveForm = function(options){
         //alert(options.path);
            if(options.path) {
                // options.path refers to the path of the adaptive form
                // For Example: /content/forms/af/ABC, where ABC is the adaptive form
                // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
                var path = options.path;
                $.ajax({
                    url  : path ,
                    type : "GET",
                    data : {
                        // wcmmode=disabled is only required for author instance
                        // wcmmode : "disabled"
                    },
                    async: false,
                    success: function (data) {
                        // If jquery is loaded, set the inner html of the container
                        // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not        evaluate the script tag in HTML as per the HTML5 spec
                        // For example: document.getElementById().innerHTML
                        if(window.$ && options.CSS_Selector){
                            // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the        script tag.
                            $(options.CSS_Selector).html(data);
                        }
                    },
                    error: function (data) {
                        // any error handler
                    }
                });
            } else {
                if (typeof(console) !== "undefined") {
                    console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
                }
            }
         }(options);
   
         </script>
          </body>
        </html>
   ```

1. 埋め込まれたコードで、

   * *options.path* 変数の値をアダプティブフォームの公開 URL のパスに変更します。AEM サーバーがコンテキストパス上で実行されている場合は、その URL にコンテキストパスが含まれるようにします。アダプティブフォームの拡張子を含む完全な名前を必ず指定してください。   例えば、上記のコードはアダプティブフォームと同一の AEM Forms サーバー上に存在するため、この例ではアダプティブフォームのコンテキストパスである /content/forms/af/locbasic.html が使用されています。
   * CSS_Selector は、アダプティブフォームが埋め込まれているフォームコンテナの CSS セレクターです。例えば、上の例では、.customafsection CSS クラスが CSS セレクターです。

アダプティブフォームは Web ページに埋め込まれます。 埋め込まれたアダプティブフォームで、以下の点を確認します。

* ドラフトおよび送信済みフォームは、フォームポータル上の「ドラフト」タブと「送信」タブで使用できます。
* 元のアダプティブフォームに設定された送信アクションは、埋め込まれたフォームでも保持されます。
* アダプティブフォームのルールは、埋め込まれたフォームでも保持され、完全に機能します。
* 元のアダプティブフォームで設定されたエクスペリエンスのターゲット設定と A/B テストは、埋め込まれたフォームでは機能しません。
* 元のフォームにAdobe Analyticsが設定されている場合、分析データはAdobe Analyticsサーバーで取り込まれます。 ただし、Forms Analytics レポートでは使用できません。
* コアコンポーネントをベースとするアダプティブFormsでは、クライアントライブラリ (ClientLibs) が、フォームのヘッダーおよびフッターコンポーネントと共にインクルードおよび読み込まれます。 そのため、コアコンポーネントに基づくアダプティブFormsを Web ページに埋め込む場合、フォームのヘッダーとフッターが常に含まれます。

## トポロジのサンプル {#sample-topology}

アダプティブフォームを埋め込んだ外部 Web ページは、AEMサーバーに要求を送信します。このサーバーは通常、プライベートネットワークのファイアウォールの内側に配置されます。 要求がAEMサーバーに安全に送信されるようにするには、リバースプロキシサーバーを設定することをお勧めします。

Dispatcher を使用せずに Apache 2.4 リバースプロキシサーバーを設定する方法の例を見てみましょう。 この例では、AEM サーバーを `/forms` コンテキストパスでホストし、リバースプロキシの `/forms` をマッピングします。これで、Apache サーバーの `/forms` へのすべてのリクエストは、AEM インスタンスにダイレクトされます。このトポロジにより、前に `/forms` の付いたすべてのリクエストが AEM サーバー経由になるため、ディスパッチャーレイヤーのルールの数を低減することができます。

1. `httpd.conf` 設定ファイルを開き、次のコードの行をコメント解除します。または、これらのコードの行をファイルに追加することができます。

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 次のコードの行を `httpd-proxy.conf` 設定ファイルに追加して、プロキシルールをセットアップします。

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   `[AEM_Instance]` を、ルールの AEM サーバー公開 URL で置き換えます。

コンテキストパスに AEM サーバーをマウントしない場合、Apache レイヤーのプロキシルールは次のようになります。

```text
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>その他のトポロジーをセットアップする場合は、ディスパッチャーレイヤーの送信、事前入力、およびその他の URL を必ず許可リストに登録してください。

## ベストプラクティス {#best-practices}

Web ページにアダプティブフォームを埋め込む際は、次のベストプラクティスを考慮してください。

* Web ページの CSS で定義されたスタイルルールが、フォームオブジェクトの CSS と競合しないようにします。 競合を避けるために、AEMクライアントライブラリを使用して、アダプティブフォームテーマで Web ページの CSS を再利用できます。 アダプティブフォームテーマでクライアントライブラリを使用する方法については、 [AEM Formsのテーマ](/help/forms/using-themes-in-core-components.md).
* Web ページのフォームコンテナで、ウィンドウの幅全体を使用するようにします。 これにより、モバイルデバイス用に設定された CSS ルールが、何も変更しなくても確実に機能するようになります。 フォームコンテナがウィンドウの幅全体を取らない場合は、フォームを様々なモバイルデバイスに適応させるために、カスタム CSS を記述する必要があります。
* `[getData](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` API を使用して、クライアントのフォームデータの XML または JSON 表現を取得してください。
* `[unloadAdaptiveForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` API を使用して、HTML DOM からアダプティブフォームをアンロードします。
* AEM サーバーから応答を送信するときは、access-control-origin ヘッダーを設定してください。

## AEM Forms がクロスドメインサイトに対してアダプティブフォームをサーブできるようにする {#cross-site}

1. AEM パブリッシュインスタンスで、AEM Web Console Configuration Manager（`https://'[server]:[port]'/system/console/configMgr`）に移動します。
1. **Apache Sling Referrer Filter** 構成を探して開きます。
1. 「許可済みホスト」フィールドで、web ページが存在するドメインを指定します。これにより、ホストは AEM サーバーに POST リクエストをできるようになります。また、正規表現を使用して、一連の外部アプリケーションドメインを指定することもできます。
