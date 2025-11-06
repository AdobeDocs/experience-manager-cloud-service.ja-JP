---
title: ページオーサリングのカスタマイズ
description: ページオーサリング機能をカスタマイズするために AEM as a Cloud Service が提供するメカニズムについて説明します。
exl-id: 98d3c7ab-46d2-4e8d-b0da-5c8a7b398135
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 97%

---

# ページオーサリングのカスタマイズ {#customizing-page-authoring}

Adobe Experience Manager as a Cloud Service には、オーサーインスタンスのページオーサリング機能（および[コンソール](/help/implementing/developing/extending/consoles.md)）をカスタマイズできる様々なメカニズムが用意されています。

## Clientlibs {#clientlibs}

クライアントライブラリを使用すると、デフォルトの実装を拡張して新しい機能を有効にしながら、標準の関数、オブジェクト、メソッドを再利用できます。

カスタマイズする際に、独自のクライアントライブラリを `/apps.` に作成できます。新しいクライアントライブラリには次の条件があります。

* オーサリングクライアントライブラリ `cq.authoring.editor.sites.page` を使用する必要があります。
* 適切な `cq.authoring.editor.sites.page.hook` カテゴリに含める必要があります。

[AEM as a Cloud Service でのクライアントサイドライブラリの使用](/help/implementing/developing/introduction/clientlibs.md)を参照してください。

## オーバーレイ {#overlays}

オーバーレイオーバーレイはノード定義に基づいており、`/libs` にある標準の機能に、`/apps` にあるカスタマイズした独自機能を重ねることができます。

:1sling Resource Merger[&#x200B; は継承を許可しているので、オーバーレイを作成するときに、オリジナルの 1](/help/implementing/developing/introduction/sling-resource-merger.md) コピーは必要ありません。

詳しくは、[JS ドキュメントセット](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html)を参照してください。

オーバーレイについて詳しくは、[Adobe Experience Manager as a Cloud Service のオーバーレイ](/help/implementing/developing/introduction/overlays.md)を参照してください。

## 新しいレイヤー（モード）の追加 {#add-new-layer-mode}

ページを編集するときに、さまざまな[モード](/help/sites-cloud/authoring/page-editor/introduction.md#page-modes)を使用できます。これらのモードは、[レイヤー](/help/implementing/developing/introduction/ui-structure.md#layer)を使用して実装されます。これらにより、同じページコンテンツの異なるタイプの機能にアクセスできます。標準の AEM モードには、編集、レイアウト、開発者、タイムワープ、ライブコピーのステータス、およびターゲティングが含まれます。

### レイヤーの例：ライブコピーステータス {#layer-example-live-copy-status}

標準の AEM インスタンスは MSM レイヤーを提供します。これは、[マルチサイト管理](/help/sites-cloud/administering/msm/overview.md)に関連するデータにアクセスし、レイヤーでハイライトします。

実行中に確認するには、[WKND サンプルコンテンツ](/help/implementing/developing/introduction/develop-wknd-tutorial.md)の任意の言語コピーを編集し、**ライブコピーステータス**&#x200B;モードを選択します。

MSM レイヤーの定義（参照用）は、次のファイルにあります。

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### コードサンプル {#code-sample}

これは、MSM ビュー用のレイヤー（モード）の作成方法を示すサンプルパッケージです。

このページのコードは [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode) にあります。

## 新しい選択カテゴリをアセットブラウザに追加 {#add-new-selection-category-to-asset-browser}

アセットブラウザーには、様々なタイプまたはカテゴリのアセット（画像、ドキュメントなど）が表示されます。このようなアセットカテゴリを使用して、アセットをフィルターすることもできます。

### コードサンプル {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` は、新しいグループをアセットファインダーに追加する方法を示すサンプルパッケージです。このサンプルは、[Flickr](https://www.flickr.com) の公開ストリームに接続し、サイドパネルに表示します。

このページのコードは [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr) にあります。

## リソースのフィルタリング {#filtering-resources}

ページをオーサリングする際に、多くの場合、ユーザーはリスト内のリソースから選択する必要があります。

リストを適切なサイズに保ち、使用事例にも関連するように、フィルターをカスタム述語の形式で実装できます。例えば、`pathbrowser` Granite コンポーネントを使用してユーザーが特定のリソースへのパスを選択できるようにするには、表示されるパスを次のようにフィルタリングできます。

* [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/predicate/package-summary.htm) インターフェイスを実装してカスタム述語を実装します。
* 述語の名前を指定し、`pathbrowser`を使用するときにその名前を参照します。

カスタム述語の作成について詳しくは、[この記事](/help/implementing/developing/introduction/query-builder-custom-predicate.md)を参照してください。

## 新しいアクションをコンポーネントツールバーに追加 {#add-new-action-to-a-component-toolbar}

各コンポーネントには、多くの場合、そのコンポーネントに対して実行できるさまざまなアクションを呼び出すためのツールバーがあります。

### コードサンプル {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot`は、コンポーネントをレンダリングするカスタムツールバーアクションを作成する方法を示すサンプルパッケージです。

このページのコードは [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot) にあります。

## 新しいインプレースエディターを追加する {#add-new-in-place-editor}

### 標準インプレースエディター {#standard-in-place-editor}

標準 AEM インストールでは、

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js` には、使用可能な様々なエディターの定義が含まれています。

1. エディターと、エディターを使用できる各リソースタイプは、（コンポーネントと同様に）関連付けられています。

   * `cq:inplaceEditing`

     例：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * プロパティ：`editorType`

           そのコンポーネントに対してインプレース編集が呼び出された場合に使用されるインラインエディターのタイプを定義します（`text`、`textimage`、`image`、`title` など）。

1. エディターの追加の設定の詳細は、設定が含まれている `config` ノード、および必要なプラグイン設定の詳細が含まれている `plugin` ノードを使用して設定できます。


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
>AEM では、切り抜き比率は `ratio` プロパティで設定し、**高さ／幅**&#x200B;として定義します。これは従来の定義である「幅/高さ」とは異なり、レガシー互換性のための設定です。`name` プロパティを明確に定義していれば、UI に表示されるので、オーサリングユーザーは違いを認識しません。

#### 新しいインプレースエディターの作成 {#creating-a-new-in-place-editor}

新しいインプレースエディターを（クライアントライブラリ内に）実装するには、次のようにします。

1. 実装方法：

   * `setUp`
   * `tearDown`

1. エディター（コンストラクタを含む）の登録：

   * `editor.register`

1. エディターと、エディターを使用できる各リソースタイプが（コンポーネントと同様に）関連付けられます。

#### 新しいインプレースエディターを作成するためのコードサンプル {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` は、AEM で新しいインプレースエディターを作成する方法を示すサンプルパッケージです。

このページのコードは [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor) にあります。

## 新しいページアクションの追加 {#add-a-new-page-action}

**サイトに戻る**（コンソール）アクションなどの新しいページアクションを、ページツールバーに追加します。

### コードサンプル {#code-sample-3}

`aem-authoring-extension-header-backtosites` は、サイトコンソールに戻るカスタムヘッダーバーアクションを作成する方法を示すサンプルパッケージです。

このページのコードは [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites) にあります。

## アクティベーションをリクエストワークフローのカスタマイズ {#customizing-the-request-for-activation-workflow}

標準のワークフロー、**アクティベーションのリクエスト**：

* コンテンツ作成者が適切なレプリケーション権限&#x200B;**を持っていない**&#x200B;が DAM-Users および作成者のメンバーシップ&#x200B;**を持っている**&#x200B;場合、適切なメニューに自動的に表示されます 。

* それ以外の場合は、レプリケーション権限が削除されているので、何も表示されません。

そのようなアクティベーションに対する動作をカスタマイズするために、**アクティベーションをリクエスト**&#x200B;ワークフローをオーバーレイできます。

1. `/apps`で **Sites** ウィザードをオーバーレイする`/libs/wcm/core/content/common/managepublicationwizard`

   * これ自体は、`/libs/cq/gui/content/common/managepublicationwizard` の一般的なインスタンスを上書きします。

1. 必要に応じて、ワークフローモデルおよび関連設定／スクリプトを更新します。
1. ユーザーがページを公開（またはレプリケート）しようとする際にこのワークフローをデフォルトのアクションとしてトリガーさせるには、すべての関連するページのすべての適切なユーザーから `replicate` アクションの権限を削除します。
