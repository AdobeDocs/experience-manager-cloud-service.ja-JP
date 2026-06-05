---
title: アダプティブフォームを外部 Web ページに埋め込む方法
description: 外部 web ページにアダプティブフォームを埋め込む方法を学ぶ
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 198f6f76-1134-4818-89a0-6ddc84ff956c
source-git-commit: 4994babacc862977c5ff4c398027d54546c65212
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 66%

---

# コアコンポーネントに基づくアダプティブフォームの外部 Web ページへの埋め込み {#embed-adaptive-form-in-external-web-page}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | この記事 |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html?lang=ja) |


AEM の外側にホストされた Web ページか [AEM Sites ページに、アダプティブフォームをシームレスに埋め込む](/help/forms/embed-adaptive-form-aem-sites.md)ことができます。 埋め込まれたアダプティブフォームではすべての機能を使用できるので、ユーザーは、ページから移動することなくフォームを記入および送信できます。 これにより、ユーザーは web ページの他の要素から離れることなく、同時にフォームの操作も行うことができます。

## 前提条件 {#prerequisites}

外部 web サイトにアダプティブフォームを埋め込む前に次の手順を実行します。

* AEM Forms サーバーのパブリッシュインスタンスに埋め込むアダプティブフォームを公開します。
* Web サイト上で、アダプティブフォームをホストする web ページを作成するか、特定してください。 その web ページが [CDN から送信される jQuery ファイルを読み取れること](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js)、または web ページに jQuery のローカルコピーが埋め込まれていることを確認してください。 jQuery は、アダプティブフォームのレンダリングに必要です。
* AEM サーバーとweb ページが異なるドメインにある場合は、「[GuideBridgeを使用して絶対リクエスト URLを設定](#configure-base-url)および[AEM Formsを有効にしてクロスドメインサイトにアダプティブフォームを提供する](#cross-site)」の節に記載されている手順を実行します。

## アダプティブフォームの埋め込み {#embed-adaptive-form}

Web ページに数行の JavaScript を挿入することで、アダプティブフォームを埋め込むことができます。 コードの API は AEM サーバーにアダプティブフォームのリソースを求める HTTP リクエストを送信し、指定したフォームコンテナにアダプティブフォームを挿入します。

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

   * *options.path* 変数の値をアダプティブフォームの公開 URL のパスに変更します。 AEM サーバーがコンテキストパス上で実行されている場合は、その URL にコンテキストパスが含まれるようにします。 アダプティブフォームの拡張子を含む完全な名前を必ず指定してください。 例えば、上記のコードとアダプティブフォームは同じAEM Forms Server上に存在するため、この例ではアダプティブフォーム `/content/forms/af/myadaptiveform.html`のコンテキストパスを使用しています。
   * CSS_Selector は、アダプティブフォームが埋め込まれているフォームコンテナの CSS セレクターです。 例えば、上の例では、.customafsection CSS クラスが CSS セレクターです。

アダプティブフォームが web ページに埋め込まれました。 埋め込まれたアダプティブフォームで、以下の点を確認します。

* ドラフトおよび送信済みフォームは、フォームポータル上の「ドラフト」タブと「送信」タブで使用できます。
* 元のアダプティブフォームに構築された送信アクションは、埋め込まれたフォームでも保持されます。
* アダプティブフォームのルールは保持され、埋め込みフォームでも完全に機能します。
* 元のアダプティブフォームで設定されたエクスペリエンスのターゲット設定と A/B テストは、埋め込まれたフォームでは機能しません。
* 元のフォームに Adobe Analytics が構築されている場合、分析データは Adobe Analytics サーバーで取得されます。 ただし、Forms の分析レポートでは使用できません。
* コアコンポーネントをベースとするアダプティブフォームでは、クライアントライブラリ (ClientLibs) が、フォームのヘッダーおよびフッターコンポーネントと共に含まれ、読み込まれます。 そのため、コアコンポーネントに基づくアダプティブフォームを Web ページに埋め込む場合、フォームのヘッダーとフッターが常に含められます。

## GuideBridgeで絶対リクエスト URLを設定する {#configure-base-url}

AEM サーバーとweb ページが異なるドメイン上にある場合は、GuideBridge APIを使用して、guideruntime ライブラリによって生成されたリクエストに絶対AEM パブリッシュオリジンを追加できます。 `baseUrl`設定を使用して、フォーム送信、事前入力データ取得、レコードのドキュメント生成、ファイルのアップロード、内部送信操作などのリクエストに、指定された絶対オリジンを先行するようにguideruntimeに指示します。

次のスニペットを、既存の`guideBridge.connect`実装と共に埋め込みweb ページに追加します。

```javascript
window.guideBridge.connect(function () {
    window.guideBridge.registerConfig("baseUrl", "https://publish.example.com");
});
```

`https://publish.example.com`をAEM Forms Serverの公開URLに置き換えます。

この設定では、次の例のようなリクエスト URLを指定します。

`/content/forms/af/my-form/jcr:content/guideContainer.af.submit.jsp`

は、次のようにAEM サーバーに送信されます。

`https://publish.example.com/content/forms/af/my-form/jcr:content/guideContainer.af.submit.jsp`

AEM サーバーとweb ページが異なるドメイン上にある場合は、AEM パブリッシュインスタンスでCORSも設定する必要があります。 「[&#x200B; AEM Formsでクロスドメインサイトにアダプティブフォームを提供する方法](#cross-site)」の節に記載されている手順を実行します。

## サンプルトポロジ {#sample-topology}

アダプティブフォームを埋め込む外部 web ページは、プライベートネットワークのファイアウォールの内側にある AEM サーバーにリクエストを送信します。 リクエストを安全に AEM サーバーに向けるようにするには、リバースプロキシサーバーを設定することをお勧めします。

Dispatcher なしで Apache 2.4 リバースプロキシサーバーをセットアップする例を示します。 この例では、AEM サーバーを `/forms` コンテキストパスでホストし、リバースプロキシの `/forms` をマッピングします。 これで、Apache サーバーの `/forms` へのすべてのリクエストは、AEM インスタンスにダイレクトされます。 このトポロジにより、接頭辞として `/forms` の付いたすべてのリクエストが AEM サーバー経由になるため、Dispatcher レイヤーのルールの数を減らすことができます。

1. `httpd.conf`設定ファイルを開き、次のコードの行をコメント解除します。 または、これらのコードの行をファイルに追加することができます。

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

Web ページにアダプティブフォームを埋め込む場合、次のベストプラクティスを検討します。

* Web ページの CSS で定義されたスタイルルールが、フォームオブジェクトの CSS と競合しないようにします。 競合を避けるために、AEM クライアントライブラリを使用して、アダプティブフォームテーマで Web ページの CSS を再利用できます。 アダプティブフォームテーマでクライアントライブラリを使用する方法については、[AEM フォームのテーマ](/help/forms/using-themes-in-core-components.md)を参照してください。
* Web ページのフォームコンテナで、ウィンドウの幅全体を使用するようにします。 これにより、モバイルデバイス用に設定された CSS ルールが、変更なしで確実に機能するようになります。 フォームコンテナがウィンドウの幅全体を取らない場合、フォームを様々なモバイルデバイスに適応させるために、カスタム CSS を記述する必要があります。
* `[getData](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` API を使用して、クライアントのフォームデータの XML または JSON 表現を取得してください。
* `[unloadAdaptiveForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` API を使用して、HTML DOM からアダプティブフォームをアンロードします。
* AEM サーバーから応答を送信するときは、access-control-origin ヘッダーを設定します。

## AEM Forms がクロスドメインサイトに対してアダプティブフォームをサーブできるようにする {#cross-site}

AEM サーバーとweb ページが異なるドメイン上にある場合は、次のいずれかのオプションを使用してAEM パブリッシュインスタンスを設定します。

>[!NOTE]
>
> AEM as a Cloud Serviceは、パブリッシュインスタンス上のOSGi Web コンソールへのアクセスを提供しません。 次の設定を`ui.config/src/main/content/jcr_root/apps/<application-folder>/osgiconfig/config.publish`のCloud Manager Git リポジトリに追加し、[Cloud Manager](/help/implementing/cloud-manager/deploy-code.md)を通じて変更をデプロイします。

>[!BEGINTABS]

>[!TAB GuideBridge baseUrl設定の使用]

GuideBridge `baseUrl`設定を使用する場合は、AEM パブリッシュインスタンスでCORSを設定して、AEM サーバーが送信、事前入力、レコードのドキュメントのエンドポイントに適切なヘッダーを返すようにします。

1. Cloud Manager Git リポジトリで、`ui.config/src/main/content/jcr_root/apps/<application-folder>/osgiconfig/config.publish`に移動します。
1. 次の例のように、コンテンツを使用してOSGi設定ファイル `com.adobe.granite.cors.impl.CORSPolicyImpl~embedded-forms.cfg.json`を作成します。 `https://www.example.com`を埋め込みweb ページのオリジンに置き換えます。

   ```json
   {
     "supportscredentials": false,
     "supportedmethods": [
       "GET",
       "HEAD",
       "POST"
     ],
     "exposedheaders": [
       ""
     ],
     "alloworigin": [
       "https://www.example.com"
     ],
     "maxage:Integer": 1800,
     "alloworiginregexp": [
       ""
     ],
     "supportedheaders": [
       "Origin",
       "Accept",
       "X-Requested-With",
       "Content-Type",
       "Access-Control-Request-Method",
       "Access-Control-Request-Headers"
     ],
     "allowedpaths": [
       "/content/forms/af/.*",
       "/libs/granite/csrf/token.json"
     ]
   }
   ```

1. Cloud Manager パイプラインを通じて、設定をコミット、プッシュ、デプロイします。

詳しくは、[&#x200B; クロスオリジン リソース共有（CORS）設定](/help/headless/deployment/cross-origin-resource-sharing.md)を参照してください。

>[!TAB Apache Sling Referrer Filter]

リバース プロキシを使用するか、GuideBridge `baseUrl`設定なしでアダプティブフォームを埋め込む場合は、AEM パブリッシュインスタンスでApache Sling リファラーフィルターを設定します。

1. Cloud Manager Git リポジトリで、`ui.config/src/main/content/jcr_root/apps/<application-folder>/osgiconfig/config.publish`に移動します。
1. 次の例のようなコンテンツを使用して、OSGi設定ファイル `org.apache.sling.security.impl.ReferrerFilter.cfg.json`を作成または更新します。 `www.example.com`を、web ページが存在するドメインに置き換えます。

   ```json
   {
     "allow.empty": false,
     "allow.hosts": [
       "www.example.com"
     ],
     "allow.hosts.regexp": [
       ""
     ],
     "filter.methods": [
       "POST",
       "PUT",
       "DELETE",
       "COPY",
       "MOVE"
     ],
     "exclude.agents.regexp": [
       ""
     ]
   }
   ```

1. Cloud Manager パイプラインを通じて、設定をコミット、プッシュ、デプロイします。

>[!WARNING]
>
> AEM のリファラーフィルターは OSGi 設定ファクトリではありません。つまり、AEM サービスで一度にアクティブになる設定は 1 つだけです。 可能な場合は、AEMのネイティブ設定が上書きされ、製品機能が損なわれる可能性があるため、カスタムリファラーフィルター設定を追加しないでください。

詳しくは、[&#x200B; リファラーフィルター設定](/help/headless/deployment/referrer-filter.md)を参照してください。

>[!ENDTABS]

<!--

>[!MORELIKETHIS]
>
>* [Embed adaptive form based on core components to AEM sites](/help/forms/embed-adaptive-form-core-components-aem-sites.md)

-->