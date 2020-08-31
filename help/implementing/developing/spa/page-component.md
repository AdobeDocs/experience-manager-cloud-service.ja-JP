---
title: SPAページコンポーネント
description: SPAでは、ページコンポーネントは子コンポーネントのHTML要素を提供せず、代わりにSPAフレームワークに委任します。 このドキュメントでは、これによってSPAのページコンポーネントが一意になる方法を説明します。
translation-type: tm+mt
source-git-commit: c075bcc415b68ba0deaeca61d6d179bd7263ca5f
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 11%

---


# SPAページコンポーネント {#spa-page-component}

SPAのページコンポーネントは、JSPまたはHTLファイルとリソースオブジェクトを介して、子コンポーネントのHTML要素を提供しません。 この処理は SPA フレームワークに委任されます。子コンポーネントの表現は、JSONデータ構造（例：モデル）としてフェッチされます。 次に、指定されたJSONモデルに従ってSPAコンポーネントがページに追加されます。 そのため、ページコンポーネントの初期ボディの構成は、その対応するプリレンダリングHTMLとは異なります。

## ページモデルの管理 {#page-model-management}

The resolution and the management of the page model is delegated to a provided [`PageModelManager`](blueprint.md#pagemodelmanager) module. SPAは、初期化時に `PageModelManager` モジュールとやり取りし、初期ページモデルを取得し、モデル更新の登録を行う必要があります。主に、作成者がページエディターを使用してページを編集する際に生成されます。 は、SPAプロジェクト `PageModelManager` からnpmパッケージとしてアクセスできます。 AEMとSPAの間のインタプリタとして、はSPAに付き添うこと `PageModelManager` を意図しています。

ページを作成できるようにするには、という名前のクライアントライブラリを追加し `cq.authoring.pagemodel.messaging` て、SPAとページエディター間の通信チャネルを提供する必要があります。 SPAページコンポーネントがページwcm/coreコンポーネントから継承している場合は、次のオプションを使用してクライアントライブラリカテゴリを使用できるように `cq.authoring.pagemodel.messaging` します。

* テンプレートが編集可能な場合は、クライアントライブラリカテゴリをページポリシーに追加します。
* ペ追加ージコンポーネント `customfooterlibs.html` の「」を使用したクライアントライブラリカテゴリ。

カテゴリの組み込みをページエディターのコンテキストに制限することを忘れないでください。 `cq.authoring.pagemodel.messaging`

## 通信データタイプ {#communication-data-type}

通信データ型は、属性を使用してAEM Pageコンポーネント内にHTML要素を設定し `data-cq-datatype` ます。 通信データ型がJSONに設定されている場合、GET要求はコンポーネントのSlingモデルエンドポイントに届きます。 ページエディターで更新が実行されると、更新されたコンポーネントの JSON 表記がページモデルのライブラリに送信されます。次に、ページモデルライブラリがSPAに更新の警告を表示します。

**SPAページコンポーネント —`body.html`**

```
<div id="page"></div>
```

DOMの生成を遅らせないことをお勧めしますが、SPAフレームワークでは、本文の末尾にスクリプトを追加する必要があります。

**SPAページコンポーネント —`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

SPAコンテンツを記述するメタリソースプロパティ。

**SPAページコンポーネント —`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>コンポーネントのSlingモデル表現を要求する際、デフォルトのモデルセレクターは静的に設定されます。

## メタプロパティ {#meta-properties}

* `cq:wcmmode`:エディターのWCMモード（ページ、テンプレートなど）
* `cq:pagemodel_root_url`:アプリのルートモデルのURL。 子ページモデルはアプリのルートモデルのフラグメントなので、子ページに直接アクセスする場合に重要です。 次 `PageModelManager` に、アプリケーションの初期モデルを、そのルートエントリポイントからアプリケーションに入るときに体系的に再構成する。
* `cq:pagemodel_router`:ライブラリ [`ModelRouter`](routing.md)`PageModelManager` の有効化または無効化
* `cq:pagemodel_route_filters`:無視する必要があるルートを指定するための、カンマ区切りのリストまたは正規式 [`ModelRouter`](routing.md) 。

## ページエディターオーバーレイの同期 {#page-editor-overlay-synchronization}

オーバーレイの同期は、 `cq.authoring.page` カテゴリが提供するのと同じ変異オブザーバー(Mutation Observer)が保証します。

## SlingモデルJSONが書き出した構造の設定 {#sling-model-json-exported-structure-configuration}

ルーティング機能が有効な場合、AEMナビゲーションコンポーネントのJSONエクスポートのおかげで、SPAのJSONエクスポートにアプリケーションの様々なルートが含まれていることが前提となります。 AEM ナビゲーションコンポーネントの JSON 出力は、次の 2 つのプロパティを使用し、SPA のルートページのコンテンツポリシーで設定することができます。

* `structureDepth`：書き出されたツリーの深度に対応する数字。
* `structurePatterns`:書き出すページに対応する正規表現
