---
title: SPAの概要とチュートリアル
description: この記事では、SPAの概念を紹介し、基本的なSPAアプリケーションを使用したオーサリング方法を紹介し、基礎となるAEM SPAエディターとの関連を示します。
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '1930'
ht-degree: 3%

---


# SPAの概要とチュートリアル {#spa-introduction}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

SPA エディターには、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。この記事では、基本的なSPAアプリケーションを使用したオーサリングの手順を説明し、基盤となるAEM SPAエディターとの関連を示します。

## 概要 {#introduction}

### 記事の目的 {#article-objective}

この記事では、読者をSPAエディターのチュートリアルに進める前に、単純なSPAアプリケーションを使用して基本的なコンテンツ編集のデモを行う前に、SPAの基本的な概念について説明します。 次に、ページの構築、およびSPAアプリケーションとAEM SPAエディタとの関連ややややり取りに掘り下げます。

この概要とチュートリアルの目的は、AEM開発者に、SPAが関連する理由、一般的な動作、AEM SPAエディタでのSPAの処理方法、および標準のAEMアプリケーションとの相違点を説明することです。

チュートリアルは、標準的なAEM機能と、サンプルのWKND SPA Projectアプリに基づいています。 続けて行くには、サンプルのWKND SPA ProjectアプリケーションをGitHubから [ダウンロードしてインストールしてください。](https://github.com/adobe/aem-guides-wknd-spa)

>[!CAUTION]
>
>このドキュメントでは、 [WKND SPA Projectアプリケーションをデモ目的でのみ使用します](https://github.com/adobe/aem-guides-wknd-spa) 。 どのプロジェクト作業にも使用しないでください。

>[!TIP]
>
>AEMプロジェクトでは、 [AEM Project Archetype](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)（ReactまたはAngularを使用するSPAプロジェクトをサポートし、SPA SDKを利用する）を活用する必要があります。

### SPAとは {#what-is-a-spa}

シングルページアプリケーション(SPA)は、クライアント側でレンダリングされ、主にJavaScript主導であり、Ajax呼び出しに依存してデータを読み込み、ページを動的に更新する点で、従来のページとは異なります。 ほとんどまたはすべてのコンテンツは、1回のページ読み込みで1回取得され、ユーザーによるページとのやり取りに基づいて、必要に応じて非同期に読み込まれる追加のリソースが含まれます。

これにより、ページを更新する必要が減り、シームレスで高速な、ネイティブのアプリエクスペリエンスに近いエクスペリエンスをユーザーに提供できます。

AEM SPA Editorを使用すると、フロントエンド開発者はAEMサイトに統合できるSPAを作成でき、コンテンツ作成者は他のAEMコンテンツと同様に簡単にSPAコンテンツを編集できます。

### なぜSPAなの？ {#why-a-spa}

SPAは、より高速で流動的で、ネイティブアプリケーションと同様になることで、Webページの訪問者だけでなく、SPAの仕組みの性質上、マーケターや開発者にとっても非常に魅力的なエクスペリエンスとなります。

![SPAの利点](assets/spa-benefits.png)

#### 訪問者数 {#visitors}

* 訪問者は、コンテンツとのやり取りでネイティブなエクスペリエンスを求めています。
* ページが速くなればなるほど、コンバージョンが発生する可能性が高いという明確なデータがあります。

#### マーケター {#marketers}

* マーケターは、豊富でネイティブなエクスペリエンスをオファーして、訪問者にコンテンツに対して十分な関与を促したいと考えています。
* パーソナライゼーションは、これらのエクスペリエンスをさらに魅力的にします。

#### 開発者向け {#developers}

* 開発者は、コンテンツとプレゼンテーションの間の懸念事項を明確に分けておきたいと考えています。
* クリーン分離により、システムの拡張性が向上し、フロントエンドの独立開発も可能になります。

### SPAの動作 {#how-does-a-spa-work}

SPAの主な概念は、サーバーの遅延による遅延を最小限に抑え、SPAがネイティブアプリケーションの応答性に近づくように、サーバーへの呼び出しとサーバーへの依存関係を低減することです。

従来の順次Webページでは、即時ページに必要なデータのみが読み込まれます。 つまり、訪問者が別のページに移動すると、サーバーが追加のリソースを呼び出します。 訪問者がページ上の要素を操作する際に、追加の呼び出しが必要になる場合があります。 これらの複数の呼び出しは、ページが訪問者のリクエストに追い付く必要があるので、遅延や遅延の感覚を与える可能性があります。

![順次エクスペリエンスと流体エクスペリエンス](assets/spa-sequential-vs-fluid.png)

より流動的なエクスペリエンスを実現するためには(モバイルやネイティブのアプリから訪問者が予測する動作に近い)、SPAは、最初の読み込み時に訪問者に必要なすべてのデータを読み込みます。 最初は少し時間がかかる場合がありますが、サーバーコールを追加する必要はありません。

クライアント側でレンダリングすると、ページ要素の反応が速くなり、訪問者によるページとのやり取りが即時に行われます。 ページの速度を最大化するために、必要になる可能性のある追加データはすべて非同期で呼び出されます。

>[!TIP]
>
>AEMでのSPAの動作方法に関する技術的な詳細は、次の記事を参照してください。
>* [AEMでのSPAの使用の手引き(React)](getting-started-react.md)
>* [AEMでのAngularの使用の手引き](getting-started-angular.md)

>
>
SPAエディターの設計、アーキテクチャ、技術的なワークフローについて詳しくは、次の記事を参照してください。
>* [SPA エディターの概要](editor-overview.md).


## SPAを使用したコンテンツ編集エクスペリエンス {#content-editing-experience-with-spa}

AEM SPAエディターを利用するSPAが構築されている場合、コンテンツの編集と作成の際に、コンテンツ作成者は何の違いも認識しません。 共通のAEM機能を利用でき、作成者のワークフローに変更を加える必要はありません。

1. AEMでWKND SPA Projectアプリを編集します。

   `http://localhost:4502/editor.html/content/wknd-spa-react/us/en/home.html`

   ![WKND SPAプロジェクトホーム](assets/wknd-home.png)

1. テキストコンポーネントを選択すると、他のコンポーネントと同様にツールバーが表示されます。 「**編集**」を選択します。

   ![テキストコンポーネントを選択](assets/wknd-text.png)

1. AEM内でコンテンツを通常どおりに編集し、変更内容が保持されることに注意してください。

   ![テキストの編集](assets/wknd-edit-text.png)

1. アセットブラウザを使用して、新しい画像を画像コンポーネントにドラッグ&amp;ドロップします。

   ![画像アセットの削除](assets/wkdn-drop-image.png)

1. 変更は持続されます。

   ![持続イメージ](assets/wknd-change-persisted.png)

追加のコンポーネントをページにドラッグアンドドロップしたり、コンポーネントを並べ替えたり、レイアウトを変更したりするなどの追加のオーサリングツールは、SPA以外のAEMアプリケーションと同様にサポートされます。

>[!NOTE]
>
>SPAエディタは、アプリケーションのDOMを変更しません。 SPA自体がDOMを処理します。
>
>この機能を確認するには、次の記事「 [SPA Apps」とAEM SPA Editorのセクションに進みます](#spa-apps-and-the-aem-spa-editor)。

## SPA AppsとAEM SPAエディタ {#spa-apps-and-the-aem-spa-editor}

SPAがエンドユーザーに対してどのように動作するかを体験し、SPAページを検査すると、AEMのSPAエディターでのSAPアプリの動作をより深く理解できます。

### SPAアプリケーションの使用 {#using-an-spa-application}

1. 公開サーバーで、またはページエディターの **ページ情報** ( **Page Information** )メニューから「公開済み」オプション表示を使用して、WKND SPA Projectアプリケーションを読み込みます。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![プレビューオブWKND SPAプロジェクトホーム](assets/wknd-preview.png)

   子ページへのナビゲーション、メニュー、記事カードなど、ページ構造をメモしておきます。

1. メニューを使用して子ページに移動し、ページが読み込まれるのを確認します。更新は必要ありません。

   ![WKND SPAプロジェクトページ1](assets/wknd-page1.png)

1. ブラウザーに組み込まれている開発者ツールを開き、子ページを移動しながらネットワークアクティビティを監視します。

   ![ネットワークアクティビティ](assets/wknd-network-activity.png)

   アプリ内でページ間を移動する際のトラフィック量は非常に少なくなります。 ページがリロードされず、新しい画像のみが要求されます。

   SPAは、コンテンツとルーティングを完全にクライアント側で管理します。

子ページをナビゲートする際にページがリロードされない場合、どのようにロードされますか。

次の節「SPAアプリケーションの [読み込み](#loading-a-spa-application)」では、SPAの読み込みの仕組みと、コンテンツの同期および非同期的な読み込み方法を詳しく調べます。

### SPAアプリケーションの読み込み {#loading-a-spa-application}

1. まだ読み込まれていない場合は、Web.Retailジャーナルアプリケーションを公開サーバーに読み込むか、ページエディターの **ページ表示****(Page Information** )メニューから「公開済み」オプションを使用します。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![WKND SPAプロジェクトプレビュー](assets/wknd-preview.png)

1. ブラウザーの組み込みツールを使用して、ページのソースを表示します。
1. ソースのコンテンツは制限されます。

   ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8"/>
        <title>WKND SPA React Home Page</title>
   
        <meta name="template" content="spa-page-template"/>
        <meta name="viewport" content="width=device-width, initial-scale=1"/>
   
    <link rel="stylesheet" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-base.min.css" type="text/css">
   
    <meta name="theme-color" content="#000000"/>
    <link rel="icon" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react/resources/favicon.ico"/>
    <link rel="apple-touch-icon" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react/resources/logo192.png"/>
    <link rel="manifest" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react/resources/manifest.json"/>
   
    <!-- AEM page model -->
    <meta property="cq:pagemodel_root_url" content="/content/wknd-spa-react/us/en.model.json"/>
    <link href="//fonts.googleapis.com/css?family=Source+Sans+Pro:400,600|Asar&display=swap" rel="stylesheet"/>
    <meta property="cq:datatype" content="JSON"/>
    <meta property="cq:wcmmode" content="edit"/>
   
    <link rel="stylesheet" href="/libs/cq/gui/components/authoring/editors/clientlibs/internal/page.min.css" type="text/css">
    <link rel="stylesheet" href="/etc.clientlibs/wcm/foundation/clientlibs/main.min.css" type="text/css">
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/internal/messaging.min.js"></script>
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/utils.min.js"></script>
    <script type="text/javascript" src="/libs/granite/author/deviceemulator/clientlibs.min.js"></script>
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/internal/page.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/wcm/foundation/clientlibs/main.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/clientlibs/granite/jquery.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/clientlibs/granite/utils.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/clientlibs/granite/jquery/granite.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/foundation/clientlibs/jquery.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/foundation/clientlibs/shared.min.js"></script>
   
    <!--cq{"decorated":false,"type":"cq/cloudconfig/components/scripttags/header","path":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-header","structurePath":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-header","selectors":null,"servlet":"Script /libs/cq/cloudconfig/components/scripttags/header/header.html","totalTime":2,"selfTime":2}-->
   
    <link rel="stylesheet" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react.min.css" type="text/css">
   
    </head>
   
    <body class="page basicpage">
        <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="spa-root"></div>
   
    <script type="text/javascript" src="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react.min.js"></script>
   
    <script type="text/javascript" src="/etc.clientlibs/core/wcm/components/commons/site/clientlibs/container.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-base.min.js"></script>
   
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/internal/pagemodel/messaging.min.js"></script>
   
    <link rel="stylesheet" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-author.min.css" type="text/css">
   
    <!--cq{"decorated":true,"type":"cq/cloudserviceconfigs/components/servicecomponents","path":"/content/wknd-spa-react/us/en/home/jcr:content/cloudservices","selectors":null,"servlet":"Script /libs/cq/cloudserviceconfigs/components/servicecomponents/servicecomponents.jsp","totalTime":2,"selfTime":2}-->
   
    <!--cq{"decorated":false,"type":"cq/cloudconfig/components/scripttags/footer","path":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-footer","structurePath":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-footer","selectors":null,"servlet":"Script /libs/cq/cloudconfig/components/scripttags/footer/footer.html","totalTime":2,"selfTime":2}-->
   
    </body>
    </html>
    <!--cq{"decorated":false,"type":"wknd-spa-react/components/page","path":"/content/wknd-spa-react/us/en/home/jcr:content","selectors":null,"servlet":"Script /apps/spa-project-core/components/page/page.html","totalTime":39,"selfTime":33}-->
   ```

   ページの本文にはコンテンツが含まれていません。 主にスタイルシートで構成され、などの様々なスクリプトの呼び出しが行われ `clientlib-react.min.js`ます。

   これらのスクリプトは、このアプリケーションの主なドライバーであり、すべてのコンテンツのレンダリングを担当します。

1. ブラウザーに組み込まれているツールを使用して、ページを調べます。 完全に読み込まれたDOMのコンテンツを表示します。

   ![DOM of WKND SPAプロジェクト](assets/wknd-dom.png)

1. [インスペクタ]の[ネットワーク]タブに切り替えて、ページを再読み込みします。

   イメージリクエストを無視した場合、ページに対して読み込まれる主なリソースは、ページ自体、CSS、React Javascript、その依存関係、およびページのJSONデータです。

   ![WKND SPAプロジェクトネットワークアクティビティ](assets/wknd-network.png)

1. を新しいタブ `home.model.json` に読み込みます。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.model.json`

   ![WKND SPAプロジェクトホームページのJSON](assets/wknd-json.png)

   AEM SPA Editorは、 [AEM Content Services](/help/assets/content-fragments/content-fragments.md) を利用して、ページのコンテンツ全体をJSONモデルとして配信します。

   特定のインターフェイスを実装することで、SlingモデルはSPAに必要な情報を提供します。 JSONデータの配信は、各コンポーネント（ページ間、段落間、コンポーネント間など）に下方向に委任されます。

   各コンポーネントは、表示内容とレンダリング方法を選択します（HTLを使用するサーバー側、またはReactやAngularを使用するクライアント側）。 この記事では、Reactを使用したクライアント側のレンダリングについて説明します。

1. また、モデルはページを同期的に読み込むように複数のページをグループ化できるので、必要なページ再読み込み数を減らすことができます。

   Web.Retailジャーナルの例では、訪問者は一般的にこれらのすべてのページを訪問するので、 `home`、、、 `page-1`、 `page-2`および `page-3` ページは同期的に読み込まれます。

   この動作は必須ではなく、完全に定義可能です。

   ![WKND SPAプロジェクト項目のグループ化](assets/wknd-pages.png)

1. この動作の違いを表示するには、 `home` ページを再読み込みし、インスペクタのネットワークアクティビティをクリアします。 ページメニュー `page-1` に移動し、のイメージの要求が唯一のネットワークアクティビティであることを確認 `page-1`します。 `page-1` に含まれているデータを読み込む必要はありません。

   ![WKND SPAプロジェクトページ1ネットワークアクティビティ](assets/wknd-page1-network.png)

### SPAエディタとの対話 {#interaction-with-the-spa-editor}

サンプルのWKND SPA Projectアプリケーションを使用すると、JSONコンテンツ配信のコンテンツサービスを利用し、リソースの非同期的な読み込みを利用して、アプリケーションの動作と読み込み方法が明確になります。

また、コンテンツ作成者の場合、SPAエディターを使用したコンテンツ作成はAEM内でシームレスです。

次のセクションでは、SPAエディタでSPA内のコンポーネントをAEMコンポーネントに関連付け、このシームレスな編集操作を実現できる契約を検討します。

1. エディターでWKND SPA Projectアプリケーションを読み込み、 **プレビュー** モードに切り替えます。

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

1. ブラウザーに組み込まれている開発者ツールを使用して、ページのコンテンツを調べます。 選択ツールを使用して、ページ上の編集可能なコンポーネントを選択し、表示の詳細を要素に選択します。

   コンポーネントには新しいデータ属性があり `data-cq-data-path`ます。

   ![WKND SPAプロジェクト要素の検査](assets/wknd-inspector.png)

   例：

   `data-cq-data-path="/content/wknd-spa-react/us/en/home/jcr:content/root/responsivegrid/text`

   このパスは、各コンポーネントの編集コンテキスト設定オブジェクトの取得と関連付けを可能にします。

   これは、エディタがSPA内の編集可能なコンポーネントとして認識するために必要なマークアップ属性です。 この属性に基づいて、SPAエディタは、どの編集可能な設定がコンポーネントに関連付けられているかを判断し、正しいフレームやツールバーなどを設定します。 が読み込まれます。

   また、マークプレースホルダやアセットのドラッグ&amp;ドロップ機能用に、いくつかの特定のクラス名が追加されています。

   >[!NOTE]
   >
   >この動作は、編集可能な各コンポーネントに `cq` 要素が挿入されるAEMのサーバー側レンダリングページとは異なります。
   >
   >SPAエディターのこの方法では、カスタム要素を挿入する必要がなくなり、追加のデータ属性のみを利用して、フロントエンド開発者にとってマークアップが簡単になります。

## 次の手順 {#next-steps}

AEMでのSPA編集の経験とSPAとSPAエディタとの関係を理解したので、SPAの構築方法を詳しく説明します。

* [AEMでのSPAの使用の手引き](getting-started-react.md) （Reactを使用）:AEMでReactを使用してSPAエディタで動作するように基本SPAを構築する方法を示します。
* [AEMでのSPAの使用の手引き](getting-started-angular.md) （Angularを使用）:AEMでAngularを使用してSPAエディタを使用するために基本SPAを構築する方法を示します
* [「SPA Editor Overview](editor-overview.md) 」では、AEMとSPAの間の通信モデルの詳細について説明しています。
* [AEM向けSPAの開発](developing.md) ：フロントエンド開発者とAEM向けSPAの開発方法、SPAとAEMアーキテクチャとのやり取り方について説明します。
