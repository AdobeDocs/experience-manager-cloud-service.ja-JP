---
title: ページオーサリングのカスタマイズ
description: ページオーサリング機能をカスタマイズするためにAEM as a Cloud Serviceが提供するメカニズムについて説明します。
exl-id: 98d3c7ab-46d2-4e8d-b0da-5c8a7b398135
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 33%

---

# ページオーサリングのカスタマイズ {#customizing-page-authoring}

Adobe Experience Manager as a Cloud Serviceには、ページオーサリング機能 ( および [コンソール](/help/implementing/developing/extending/consoles.md)) を作成します。

## Clientlibs {#clientlibs}

clientlibs を使用すると、デフォルトの実装を拡張して新しい機能を有効にし、標準の関数、オブジェクト、メソッドを再利用できます。

カスタマイズする際に、独自のクライアントライブラリを `/apps.` に作成できます。新しいクライアントライブラリには次の条件があります。

* オーサリング clientlib に依存 `cq.authoring.editor.sites.page`.
* 適切な `cq.authoring.editor.sites.page.hook` カテゴリ。

詳しくは、 [AEMでのクライアント側ライブラリの使用 (as a Cloud Service)](/help/implementing/developing/introduction/clientlibs.md).

## オーバーレイ {#overlays}

オーバーレイはノード定義に基づいており、 `/libs` のカスタマイズされた機能 `/apps`.

オーバーレイを作成する場合、元の 1 対 1 のコピーは不要です。 [sling resource merger](/help/implementing/developing/introduction/sling-resource-merger.md) 継承を許可します。

詳しくは、 [JS ドキュメントセット](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

オーバーレイについて詳しくは、 [Adobe Experience Manager as a Cloud Serviceのオーバーレイ](/help/implementing/developing/introduction/overlays.md).

## 新しいレイヤー（モード）の追加 {#add-new-layer-mode}

ページを編集する際には、様々な操作が行われます [モード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 使用可能 これらのモードは、 [レイヤー](/help/implementing/developing/introduction/ui-structure.md#layer). これにより、同じページコンテンツに対して、異なるタイプの機能にアクセスできます。 標準のAEMモードには、編集、レイアウト、開発者、タイムワープ、ライブコピーのステータスおよびターゲティングが含まれます。

### レイヤーの例：ライブコピーステータス {#layer-example-live-copy-status}

標準のAEMインスタンスは MSM レイヤーを提供します。 これにより、 [マルチサイト管理](/help/sites-cloud/administering/msm/overview.md) レイヤでハイライト表示します。

実際に表示するには、 [WKND サンプルコンテンツ](/help/implementing/developing/introduction/develop-wknd-tutorial.md) をクリックし、 **ライブコピーステータス** モード。

MSM レイヤーの定義（参照用）は、次のファイルにあります。

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### コードサンプル {#code-sample}

これは、MSM ビュー用のレイヤー（モード）の作成方法を示すサンプルパッケージです。

このページのコードは、 [GitHub です。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)

## 新しい選択カテゴリをアセットブラウザに追加 {#add-new-selection-category-to-asset-browser}

アセットブラウザーには、様々なタイプ/カテゴリ（画像やドキュメントなど）のアセットが表示されます。 このようなアセットカテゴリを使用して、アセットをフィルターすることもできます。

### コードサンプル {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` は、アセットファインダーにグループを追加する方法を示すサンプルパッケージです。 この例は、 [Flickr](https://www.flickr.com)のパブリックストリームを参照し、サイドパネルに表示します。

このページのコードは、 [GitHub です。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)

## リソースのフィルタリング {#filtering-resources}

ページをオーサリングする際に、多くの場合、ユーザーはリスト内のリソースから選択する必要があります。

リストを適切なサイズに保ち、使用例にも関連するように、フィルターをカスタム述語の形式で実装できます。 例えば、`pathbrowser` Granite コンポーネントを使用してユーザーが特定のリソースへのパスを選択できるようにするには、表示されるパスを次のようにフィルタリングできます。

* [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/predicate/package-summary.html) インターフェイスを実装してカスタム述語を実装します。
* 述語の名前を指定し、`pathbrowser`を使用するときにその名前を参照します。

カスタム述語の作成について詳しくは、 [この記事を参照してください。](/help/implementing/developing/introduction/query-builder-custom-predicate.md)

## 新しいアクションをコンポーネントツールバーに追加 {#add-new-action-to-a-component-toolbar}

通常、各コンポーネントには、そのコンポーネントで実行できる様々なアクションにアクセスできるツールバーがあります。

### コードサンプル {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot`は、コンポーネントをレンダリングするカスタムツールバーアクションを作成する方法を示すサンプルパッケージです。

このページのコードは、 [GitHub です。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)

## 新しいインプレースエディターを追加 {#add-new-in-place-editor}

### 標準インプレースエディタ {#standard-in-place-editor}

標準 AEM インストールでは、

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js` には、使用可能な様々なエディターの定義が含まれています。

1. エディターと、それを使用できる各リソースタイプ（コンポーネントなど）との間には、次のような接続があります。

   * `cq:inplaceEditing`

     次に例を示します。

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * プロパティ：`editorType`

           そのコンポーネントに対してインプレース編集が呼び出された場合に使用されるインラインエディターのタイプを定義します。例： `text`, `textimage`, `image`, `title`.

1. エディターの追加の設定の詳細は、 `config` 設定を含むノード `plugin` 必要なプラグイン設定の詳細を含むノード。


画像コンポーネントの画像切り抜きプラグインの縦横比を定義する例を次に示します。

```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
```

>[!NOTE]
>
>AEMの切り抜き率 ( `ratio` プロパティは、次のように定義されます。 **高さ/幅**. これは従来の定義である「幅/高さ」とは異なり、レガシー互換性のための設定です。`name` プロパティを明確に定義していれば、UI に表示されるので、オーサリングユーザーは違いを認識しません。

#### 新しいインプレースエディターの作成 {#creating-a-new-in-place-editor}

新しいインプレースエディターを（クライアントライブラリ内に）実装するには、次のようにします。

1. 実装方法：

   * `setUp`
   * `tearDown`

1. エディター（コンストラクタを含む）の登録：

   * `editor.register`

1. エディターと、エディターを使用できる各リソースタイプが（コンポーネントと同様に）関連付けられます。

#### 新しいインプレースエディターを作成するためのコードサンプル {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` は、AEMでインプレースエディターを作成する方法を示すサンプルパッケージです。

このページのコードは、 [GitHub です。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)

## 新しいページアクションを追加 {#add-a-new-page-action}

新しいページアクションをページツールバーに追加するには、次の手順を実行します。 **サイトに戻る** （コンソール）アクションを使用します。

### コードサンプル {#code-sample-3}

`aem-authoring-extension-header-backtosites` は、サイトコンソールに戻るカスタムヘッダーバーアクションを作成する方法を示すサンプルパッケージです。

このページのコードは、 [GitHub です。](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)

## アクティベーションをリクエストワークフローのカスタマイズ {#customizing-the-request-for-activation-workflow}

標準のワークフロー、**アクティベーションのリクエスト**：

* コンテンツ作成者が適切なレプリケーション権限&#x200B;**を持っていない**&#x200B;が DAM-Users および作成者のメンバーシップ&#x200B;**を持っている**&#x200B;場合、適切なメニューに自動的に表示されます 。

* レプリケーション権限が削除されているので、何も表示されません。

このようなアクティベーションで動作をカスタマイズするには、 **アクティベーションのリクエスト** ワークフロー：

1. In `/apps` オーバーレイ **Sites** ウィザード `/libs/wcm/core/content/common/managepublicationwizard`

   * これ自体は、の共通のインスタンスを上書きします。 `/libs/cq/gui/content/common/managepublicationwizard`.

1. 必要に応じて、ワークフローモデルおよび関連設定／スクリプトを更新します。
1. の権限を削除します。 `replicate` すべての関連するページに対するすべての適切なユーザーからのアクション。任意のユーザーがアクセスしたときにこのワークフローをデフォルトのアクションとしてトリガーするには、ページを公開（または複製）してみます。
